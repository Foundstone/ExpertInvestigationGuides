# Playbook: Hunting for Lateral Movement

## Hypothesis

There’s an active attacker on the network trying to move laterally by (... see list of hyphotesis below).

## Why

As a result of a successful exploitation, an attacker may have obtained nonprivileged credentials, forcing the attacker to elevate the privilege level to achieve their goals.

## Artifacts

Windows Event Logs (IDs 7045, 7030, 4624).

## Source

Windows endpoints and servers.

## How to

Examine the creation of Event IDs 4728, 4732, and 4756 on enterprise domain controllers (or individual computers in nondomain environments). 

## Additional References

*	[MITRE ATT&CK Tactics: Lateral Movement](https://attack.mitre.org/wiki/Lateral_Movement) 
*   [DeepBlueCLI by Eric Conrad](https://github.com/sans-blue-team/DeepBlueCLI)
*   [Long Tail Analysis of Windows Event Logs by Eric Conrad](http://www.ericconrad.com/2015/01/long-tail-analysis-with-eric-conrad.html)
*   ["Targeted Ransomware No Longer a Future Threat", by Christiaan Beek and Andrew Furtak](https://www.mcafee.com/us/resources/reports/rp-targeted-ransomware.pdf)
*	[Lateral movement indicators in Petya attack, by McAfee](https://kc.mcafee.com/corporate/index?page=content&id=KB89540)

## Questions

1.  *There’s an active attacker on the network trying to move laterally by employing PsExec.*  

	1. Is there any evidence of PsExec use? 

	2. Is there a new service on any critical servers? 

            <details>
            <summary>Implementation</summary>

				Get-WinEvent -FilterHashtable @{logname='system'; id=7045} 
	
			</details>

	3. Are there any errors associated with the start of new services? 

	4. Is there any workstation-to-workstation traffic on my network?



