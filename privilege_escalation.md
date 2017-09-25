# Playbook: Hunting for Privilege Escalation

## Hypothesis

An attacker already present on a compromised system is trying to elevate privileges by (... see list of hyphotesis below).

## Why

As a result of a successful exploitation, an attacker may have obtained nonprivileged credentials, forcing the attacker to elevate the privilege level to achieve their goals.

## Artifacts

Windows Event Logs (IDs 4728, 4732, 4756).

## Source

Windows endpoints and servers.

## How to

Examine the creation of Event IDs 4728, 4732, and 4756 on enterprise domain controllers (or individual computers in nondomain environments). 

## Additional References

*	[MITRE ATT&CK Tactics: Privilege Escalation](https://attack.mitre.org/wiki/Privilege_Escalation) 
*   [DeepBlueCLI by Eric Conrad](https://github.com/sans-blue-team/DeepBlueCLI)
*   [Long Tail Analysis of Windows Event Logs by Eric Conrad](http://www.ericconrad.com/2015/01/long-tail-analysis-with-eric-conrad.html)


## Questions

1.  *An attacker already present on a compromised system is trying to elevate privileges by adding a user to a privileged group.*  

    1.  Is there a new user in a privileged local or domain group? 

2.  *An attacker already present on a compromised system is trying to elevate privileges by exploiting a local vulnerability.*  

    1.  Are there any missing patches that could have been used to attempt a local privilege escalation? 

3.  *An attacker already present on a compromised system is trying to elevate privileges by exploiting file system permission weaknesses.*  

    1.  Is there any binary set as a service that could have been replaced due to poor file-system permissions?
