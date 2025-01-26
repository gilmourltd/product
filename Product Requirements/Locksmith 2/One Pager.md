## Overview
Locksmith 2 is intended to be the next generation in the Locksmith line of open-source PowerShell tooling. It will super-charge the basic Locksmith "find and fix" experience by adding a GUI and a granular set of cmdlets to help end users perform more targeted AD CS security-related tasks. In additional to new new features, Locksmith 2 will improve existing features with better reporting, more educational resources, clearer remediation guidance, and deeper risk analysis. Finally, Locksmith 2 should make development processes much easier by eliminating duplicate code and introducing unit testing.
## Problem 
1. The current version of Locksmith is clearly a standalone script that was converted into a module and grew organically. It does its basic job admirably, but there are many features that the core development team would love to add that are too complex for the current design.
2. AD CS is a complex topic that most people are unfamiliar with and/or actively avoid. Current Locksmith does not provide enough educational info or reporting to help ease anxiety around AD CS.
## Objectives
1. Re-architect Locksmith in a way that improves developer experience and adheres to PowerShell (and possibly C#) best practices.
2. Improve user experience with focus on guidance, remediation, education, and reporting.
## Constraints
1. This work is unpaid side work.
2. There is only one primary developer - and he doesn't know C# yet.
3. The primary developer has a history of taking on too much work, getting stressed out, and shutting down for a while.
## Personas
| Persona                          | Description                                                                                                                                                                                                        |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| AD/IAM Professionals             | AD/IAM Pros administer AD as their primary job function. Because AD CS is part of most AD forests, most AD/IAM Pros (especially in SMB space) do not have enough technical understanding to properly secure AD CS. |
| Defensive Security Professionals | DSPs include SOC analysts, asessors/auditors, threat hunters. They need tools that help them find dangerous configurations/vulnerabilities and remediate them.                                                     |
| Offensive Security Professionals | OSPs include pen testers and red teamers. They need tools that help them quickly find dangerous configurations/vulnerabilities and allow them to help their customers fix the issues.                              |
## Use Cases
### Scenario 1
AD Admins can use Locksmith 2 to regularly check the state of their AD CS environment. If any issues are identified, they can use the guidance and code snippets provided by Locksmith 2 to resolve the issues.
### Scenario 2
DSPs can use Locksmith 2 to provide less security-minded AD/IAM Pros about AD CS issues identified during course of work.
### Scenario 3
OSPs can use Locksmith 2 to easily identify ways to attack customer forests. Then, they can use guidance provided by LS2 to inform the customer about the best way to resolve the identified vulnerabilities.