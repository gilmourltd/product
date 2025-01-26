## Features In
#### Full Testing Coverage
- Lab Creation Script v1 (A)[^1] - Uses AD/ADCS cmdlets, creates known set of issues.
- Lab Snapshot Tool (A) - create CliXML objects for each issue to be used for unit testing
- Unit Tests for Everything Possible (M)
- Integration Testing
#### Detections
- Auditing (M)[^2]
- ESC1-8, 11, 13, 15 (M)
- Excellent Error Handling for Failed Detections (M)
	- i.e. should never see 'Not applicable' or 'Not available'
- Missing Auditing GPOs
- Certifried
- ESC9, 10, 12, 14
#### Remediation
- Fix Code for Most Detections (M)
	- If fix code not possible, LS2 should provide multiple options and include the relative risk associated with each.
- Interactive Guidance for Detections that Require it (M)
	- Provide background information where necessary to help user make informed decision.
	  Example: Instead of asking "Is this template frequently used?", Locksmith 2 should look at all CA databases to find issuance frequency and suggest the most likely answer. (M)
- Revert Code for All Code-Based Fixes (M)
	-  If fix code not possible, LS2 should provide a path to undo any changes made manually.
- Automated Fix for Most Detections
	- Highlight operational impact.
	- Ask for permission to perform each action.
	- Provide background information where necessary to help user make informed decision whether to proceed.
	  Example: Instead of saying "This may cause operational impact", Locksmith 2 should look at all CA databases to find issuance frequency and say something like "This template has been used to issue average of 120 certficates/day. Enabling Manager Approval will require a large investment in human resources."
- Automated Revert for All Automated Fixes
- Fixes should show likely change in risk rating(s)
#### Risk Ratings
- Per-Issue Ratings (like LS1) (M)
- Show Per-Issue Risk Calculation (like LS1) (M)
	- Include risks presented by other misconfigurations. (M)
	- Evaluate ACL-based risks on principals that can abuse issues.
- Additional Risk Ratings:
	- Per-template: count total number of individual principals that can abuse a specific template/object/CA/configuration.
	- Per-principal: show principals that wield the most power in the PKI
#### Output
- Objects (M)
- TUI/Console (M)
	- Color theming
	- Dark/Light switch
	- Auto-theming based on current scheme (start with default 5.1 and 7+ schemes)
- HTML
- CSV
- PDF
#### Interactive Health Check
- PowerShell version (M) - if not >= 7.4 warn of possibly degraded experience
- Installed modules (M) - if missing, offer installation code
- User privileges (M) - if not AD Admin, tell which checks may not work
- Forest-joined status
  Example:
```
[!] This computer doesn't seem to be a member of a forest.
	  
[?] Do you believe this computer is a member of a forest? [Yes/No/Unsure]
No
	  
[?] From which forest would you like to retrieve AD CS information? (Enter
the FQDN of the target forest's root domain.)
horse.ad
	  
[?] Do you have credentials for the 'horse.ad' forest? [Yes/No]
Yes

Username: jake@dotdot.horse
Password: hunter2
	  
[!] Attempting to retrieve AD CS information from ad.dotdot.horse
[===============          55/90 objects ]
```
#### Configuration Storage
- Create JSON config file on first run unless runtime parameters sufficiently define configuration (M)
#### Supporting/Educational Information
- Every issue should include multiple levels of detail:
	- Title (M)
	- Description (M)
	- Details
	- ELI5 - link to online knowledge base
- Lab Creation Script
	- Known Issues (same as Alpha requirement above) (A)
	- Unknown Issues (semi-randomized)
#### Headless Mode
- PowerShell 5.1
- No 3rd party modules required
- No TUI/GUI
- Single command: `Invoke-LS2Headless`
- Returns full-featured objects to pipeline for further processing

[^1]: (A) denotes alpha/pre-MVP requirement
[^2]:(M) denotes minimum viable product requirement

*Note: Some of these features will have their own separate specs with more detailed prioritization and requirement breakdown. This doc is keeping an overall higher-level view of prioritization by just saying must have or not. In general, the categories are in priority order.*
## Features Out
What features have you explicitly decided not to do and why?
- #### Automatic Attacks
	- Could we make evil Locksmith 2? Obvi. But we will not.
- #### Feature 2 
- #### Feature 3 
## Design
Include any needed early sketches, and throughout the project, link to the actual designs once they’re available.
## Technical Considerations
#### Primary Language:
- PowerShell
#### Target Powershell Version:
- PowerShell 7.4 LTS
#### Third-party PowerShell modules likely to be used:
- PSSQLite
- PwshSpectreConsole
- PSWriteHTML
- PwshCertutil
**Any third-party modules _must_ be includable in distribution.**
#### Possible Additional Languages Required:
- SQL
- JSON
- HTML
- CSS
- JavaScript
- C# (if GUI instead of TUI)
## Success Metrics
What are the [success metrics](https://productschool.com/blog/data-analytics/metrics-product-managers-measure/) that indicate you’re achieving your internal goals for the project? How will you measure success? You can use any goal-setting and tracking system you prefer (OKRs, KPIs, etc). 

Note: Link to Analytics requirements and approach document.
## GTM Approach
What’s the product messaging that your  marketing department will use to describe this product to existing and new customers? How do you plan to launch this product to the market with marketing and sales teams?

Note: Link to a larger GTM brief if available. 
## Open Issues
What factors do you still need to figure out? What problems may arise and how do you plan on addressing them? 
## Q&A
What are common questions about the product along with the answers you’ve decided? This is a good place to note key decisions.

| Asked by | Question | Answer |
| -------- | -------- | ------ |
|          |          |        |
|          |          |        |
|          |          |        |
## Feature Timeline and Phasing

| Feature | Status         | Dates        |
| ------- | -------------- | ------------ |
|         | Backlog        | Nov 23, 2022 |
|         | In Development |              |
|         | In Review      |              |
|         | Shipped        |              |
|         | Blocked        |              |

# PRD Checklist:

| Order | Topic                              | Done        |
| ----- | ---------------------------------- | ----------- |
| 1.    | Title                              | Done        |
| 2.    | Author                             | Done        |
| 3.    | Decision Log                       | In Progress |
| 4.    | Change History                     | Backlog     |
| 5.    | Overview                           | Done        |
| 6.    | Success Overview                   | Backlog     |
| 7.    | Messaging                          | Backlog     |
| 8.    | Timeline/Release Planning          | Backlog     |
| 9.    | Personas                           | Done        |
| 10.   | User Scenarios                     | Done        |
| 11.   | User Stories/Features/Requirements | Backlog     |
| 12.   | Features In                        | In Progress |
| 13.   | Features Out                       | In Progress |
| 14.   | Design                             | Backlog     |
| 15.   | Open Issues                        | Backlog     |
| 16.   | Q&A                                | Backlog     |
| 17.   | Other Considerations               | Backlog     |
