# ~~Milestone: PSCertutil~~
- ~~Must collect all data needed for Locksmith 1
- ~~Must output structured objects
- Should collect full CA names 
- Should collect issuance history
- Should collect recently issued certs (default timespan = 30 days, but configurable)
- Should collect recently failed cert requests
- Should get pending requests
- Should get active/effective certs
- Should get suspicious enrollments
	- All requests w/SAN of Tier 0 objects
	* Compare total enrollment volume vs issued w/SAN
	* Compare typical requestor vs individual requests
	* Compare volume of Requestor = SAN vs Requestor != SAN
	* Identify non-standard issuance times (either time of day of time of year)
	* Identify Manager Approval bypass (temp disable of Manager Approval)
# Milestone: Tactical Speed Square
- Must create objects/templates of correct type, probably via AD CS cmdlets
- Should deploy AD CS role if not installed
- Should use PS AD module
# Milestone: Snapshot Tool
- Must collect full objects in PKS container + + all principals in all ACLs
- Must collect as XML or JSON
# Milestone: ESCalator
- Should be completed by October
- Not specifically needed for Locksmith 2, but logic will be useful in LS2
# Milestone: TUI
- Should be completed by October