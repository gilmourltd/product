# Installation
- A user runs
``` powershell
Install-Module -Name Locksmith2 -Scope CurrentUser -Force
```
- A welcome message appears:
```
Thank you for installing Locksmith 2: An AD CS Auditing Toolkit!
To get started, run Locksmith2
```
# Full Version
## How to Run
- A user runs `Locksmith2` from the command line.
### PowerShell Check
- CHECK silently (no PwshSpectreConsole functionality required):
	- Host is Windows
	- Windows version is Server 2016+ or Windows 10 1607+
	- PowerShell version is 5.1 or 7.4+
	- Host version is not ISE/conshost.exe
	- Required Modules are installed
	- UTF-8 is enabled
	- NerdFont is installed
- IF any checks fail:
	- WRITE all failed health check information to console.
	- START remediation functions
	- IF not Windows: Fail (v2: cross-platform)
	- If not Server 2016+ or Windows 10 1607+ (TODO: test versions): Fail 
	- {
		- IF PowerShell version = 5.1: warn only headless version is supported in 5.1
		- ELSEIF PowerShell version <7.4: provide upgrade instructions
	- }
	- IF Host is not Windows Terminal: recommend Windows Terminal
	- WHEN Modules not installed: offer to install missing modules
		- IF PSSQLite refused: Fail
		- IF PwshCertutil refused: Fail
		- IF PwshSpectreConsole refused: Fail and recommend Headless Version
		- IF PSWriteHTML refused: Warn no HTML/PDF/Excel/CSV Output
	- IF UTF-8 not enabled: offer to update $PROFILE automatically
		- IF accepted 
			- Update `$PROFILE`
			- Exit Locksmith 2 with notice on how to reload profile and restart Locksmith 2: `. $PROFILE; Locksmith2`
		- ELSE: warn about degraded TUI quality
	- IF NerdFont not installed: suggest installing NerdFont
		- NOTE: https://stackoverflow.com/questions/62458016/detect-which-font-is-in-use-by-powershell-session only works in conhost.exe and method is deprecated
- ELSE: continue
### Domain/Forest Check
- {
	- IF neither computer nor user is a member of a domain: ask for domain user credentials and attempt authentication
		- IF successful: continue in **domain user context**
		- ELSE: fail
	- ELSE IF the user is not a member of a domain: check if local admin
		- IF the user is a local admin: attempt to elevate to SYSTEM
			- IF successful: continue in **computer context**
			- ELSE: fail
		- ELSE Ask for domain user credentials and attempt authentication
			- IF successful: continue in **domain user context**
			- ELSE: fail
	- ELSE: continue
- }
### Main Loop
- IF first run
	- Ask to do tutorial
	- Set color theme
- WRITE current environmental information:
	- Current username in NTAccount format
	- Member of BA/DA/EA (single-domain) or EA (multi-domain)?
	- Local admin?
	- Elevated prompt?
	- Current computername in NTAccount format
	- Current forest root domain in FQDN and NetBIOS formats
		- Example: `Forest root domain: horse.ad (HORSE)`
	- Other domains in FQDN and NetBIOS forest
		- Example:
```
			Other domains in forest:
			- foal.horse.ad    (FOAL)
			- colt.horse.ad    (COLT)
			- filly.horse.ad   (FILLY)
			- gelding.horse.ad (GELDING)
```
- {
	- IF SQLite DB exists: offer to refresh data
		- IF accepted: CPAP as if new
		- ELSE: skip CPA, do P again
	- ELSE create SQLite DB
- }
- ASK user to enter custom AD & PKI Admin groups. Accept Name, DN, CN, UPN, NTAccount
- COLLECT data off-screen but show progress bars
	- All objects from Public Key Services container
	- All CA host computer object(s)
	- All PKI Admin group(s)
	- All members of custom AD & PKI Admin group(s)
	- All Cert Publishers group(s)
	- All members of Cert Publishers group(s)
	- All Certificate Service DCOM Access group(s)?
	- Auditing configuration from all CA hosts
	- OfficerRights from all CA hosts
	- SAN flag from all CA hosts
	- RPC Encryption flag from all CA hosts
	- Certificate Issuance Database from all CA hosts
- PROCESS collected data and write to SQLite DB off-screen but show progress bars
- ANALYZE collected data off-screen to create findings but show progress bars
- ASK user what kind of output they want:
	- PRESENT results in console:
		- Header: show environmental rating equal to highest severity finding
		- Individual Finding View (Default): sorted by Severity
		- Template/Object View: sorted by number of principals that can abuse
		- Principal View: sorted by number of findings that can be abused
	- PRESENT results in browser (PSWriteHTML):
		- Header: show environmental rating equal to highest severity finding
		- Multi-column sort
		- CSV/PDF/Excel output also
	- PRESENT results in both console & browser

# Headless Version
## How to Run
- A user runs `Invoke-Locksmith2` from the command line, a script, or a scheduled task.
### PowerShell Check
- CHECK silently:
	- Host is Windows
	- Windows version is Server 2016+ or Windows 10 1607+
	- PowerShell version is 5.1 or 7.4+
-  IF any checks fail:
	- WRITE all failed health check information to console.
	- START remediation functions
	- IF not Windows: Fail (v2: cross-platform)
	- IF not rServer 2016+ or Windows 10 1607+ (TODO: test versions): Fail 
	- {
		- IF PowerShell version less than 5.1: Fail and provide instructions for upgrading
		- ELSE IF PowerShell version = 5.1: Continue
		- ELSE IF PowerShell version 
		- ELSEIF PowerShell version <7.4: provide upgrade instructions
	- }
### Domain/Forest Check
- {
	- IF neither computer nor user is a member of a domain: ask for domain user credentials and attempt authentication
		- IF successful: continue in **domain user context**
		- ELSE: fail
	- ELSE IF the user is not a member of a domain: check if local admin
		- IF the user is a local admin: attempt to elevate to SYSTEM
			- IF successful: continue in **computer context**
			- ELSE: fail
		- ELSE Ask for domain user credentials and attempt authentication
			- IF successful: continue in **domain user context**
			- ELSE: fail
	- ELSE: continue
- }
### Main Loop
- COLLECT data off-screen but show progress bars
	- All objects from Public Key Services container
	- All CA host computer object(s)
	- All PKI Admin group(s)
	- All members of custom AD & PKI Admin group(s)
	- All Cert Publishers group(s)
	- All members of Cert Publishers group(s)
	- All Certificate Service DCOM Access group(s)?
	- Auditing configuration from all CA hosts
	- OfficerRights from all CA hosts
	- SAN flag from all CA hosts
	- RPC Encryption flag from all CA hosts
	- Certificate Issuance Database from all CA hosts
- PROCESS collected data and write to SQLite DB off-screen but show progress bars
- ANALYZE collected data off-screen to create findings but show progress bars
- RETURN Finding objects
# Cmdlets
## Find-LS2VulnerableTemplates
- `[string[]]$PriorityInfo` Info, Low, Medium, High, Critical
- `[string]$MinimumPriority` Info, Low, Medium, High, Critical
- `[string[]]$ESC` ESC1, ESC2, ESC3, ESC4, ESC9, ESC10, ESC13, ESC14, ESC15
## Find-LS2VulnerableObjects
- `[string[]]PriorityInfo` Info, Low, Medium, High, Critical
- `[string]MinimumPriority` Info, Low, Medium, High, Critical
## Find-LS2VulnerableCAs
- `[string[]]$PriorityInfo` Info, Low, Medium, High, Critical
- `[string]$MinimumPriority` Info, Low, Medium, High, Critical
- `[string[]]$ESC` ESC6, ESC7, ESC8, ESC11
## Find-LS2MostAbusableTemplates
- `[switch]$Ascending`
## Find-LS2MostDangerousPrincipals
- `[switch]$Ascending`
## Find-LS2DangerousCombinations
- `[string[]]$PriorityInfo` Info, Low, Medium, High, Critical
- `[string]$MinimumPriority` Info, Low, Medium, High, Critical