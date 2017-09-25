# Playbook: Hunting for Exfiltration

## Hypothesis

An attacker is attempting to exfiltrate a large volume of data (... see list of hyphotesis below).

## Why

Exfiltration is the last step in a data breach caused by a motivated attacker. Attackers may send a large volume of data outside of the network using different protocols. 

## Artifacts

Network session data (flows).  

## Source

Border router, switches, or other collectors (SiLK, Argus, etc.). Firewalls, proxies and NSM devices can also provide similar information.

## How to

Profile what normal looks like on your network and hunt for connections that remain pinned for a long time, connections to foreign countries, and connections with a high volume of data sent. 

## Additional References

*	[MITRE ATT&CK Tactics: Lateral Exfiltration](https://attack.mitre.org/wiki/Exfiltration) 
*	[Game Changer: Identifying and Defending Against Data Exfiltration Attempts, by Ismael Valenzuela, SANS Cyber Defense Summit 2015](https://www.sans.org/summit-archives/file/summit-archive-1493840468.pdf) 


## Questions

1.  *An attacker is attempting to exfiltrate a large volume of datato a nonbusiness-related geolocation.*  

	1.	Is any workstation or server sending a large volume of data outside the network? 

	2. 	Are there any outbound connections to nonbusiness-related geolocations? 
	
	3.	Is data being sent at abnormal times? 
	
	4.	Are there any connections that remain pinned for an abnormally long time? 


