# Expert Investigation Guides
 
## Threat Hunting Guides

These investigation guides are based on the article: 

 *  ["Threat Hunting like a PRO" by Ismael Valenzuela & Douglas Frosst, McAfee Labs Quarterly Threat Report, September 2017](TBD)


This hunting guides describes some of the most effective hunts you can employ based on some logs commonly found in an average organization. None of these should be considered in isolation, but rather as part of a process that incorporates the key elements the article cited before includes. Please refer to the published article for additional context.

Each hunting example describes a hypothesis, the questions that hunters need to ask to prove or disprove the hypothesis, the data or specific artifacts used to answer those questions, the source of that data, and the hunting technique or analytic suggested to implement it. This format follows the taxonomy and guidelines shared in:

*  ["The Need for Investigation Playbooks at the SOC" by Francisco Matias Cuenca-Acuna & Ismael Valenzuela, SANS SOC Summit 2017](https://www.sans.org/summit-archives/file/summit-archive-1496695240.pdf) 

*   [“Generating Hypotheses for Successful Threat Hunting", from David Bianco and Robert M. Lee](https://www.sans.org/reading-room/whitepapers/threats/generating-hypotheses-successful-threat-hunting-37172)


## Additional References

*   [MITRE ATT&CK Tactics](https://attack.mitre.org/wiki/) 
*	[Identifying Malware Traffic with Bro](http://blog.opensecurityresearch.com/2014/03/identifying-malware-traffic-with-bro.html)
*	[Detecting Random - Finding Algorithmically chosen DNS names (DGA)](https://isc.sans.edu/forums/diary/Detecting+Random+Finding+Algorithmically+chosen+DNS+names+DGA/19893/)
*	[Network Forensics with Windows DNS Analytical Logging](https://blogs.technet.microsoft.com/teamdhcp/2015/11/23/network-forensics-with-windows-dns-analytical-logging/)
*   [Game Changer: Identifying and Defending Against Data Exfiltration Attempts, by Ismael Valenzuela, SANS Cyber Defense Summit 2015](https://www.sans.org/summit-archives/file/summit-archive-1493840468.pdf) 
*   [DeepBlueCLI by Eric Conrad](https://github.com/sans-blue-team/DeepBlueCLI)
*   [Long Tail Analysis of Windows Event Logs by Eric Conrad](http://www.ericconrad.com/2015/01/long-tail-analysis-with-eric-conrad.html)
*   ["Targeted Ransomware No Longer a Future Threat", by Christiaan Beek and Andrew Furtak](https://www.mcafee.com/us/resources/reports/rp-targeted-ransomware.pdf)
*   [Lateral movement indicators in Petya attack, by McAfee](https://kc.mcafee.com/corporate/index?page=content&id=KB89540)

*   [Research Report Released: Detecting Lateral Movement through Tracking Event Logs, by JPCERT/CC](http://blog.jpcert.or.jp/2017/06/1-ae0d.html)


## Questions

1.  *An infected system on the network is generating outbound command and control traffic that has not yet been detected.* 

    1.  Does the endpoint contain evidence of suspicious outbound network connections?

        1. Are there any outbound DNS requests with a high degree of entropy?

        <details>
        <summary>Implementation</summary>

	    	*   Collect dns requests from DNS server or NSM logs.
			*   Run them against "freq.py" to determine degree of entropy.

        </details>
        
        2. Is there a large volume of incoming NX (nonexistent) domain responses coming back into the network?

        3. Are there any abnormally long TXT records in either DNS requests or responses?

        4. Are there any abnormal user-agent strings in HTTP requests?

        <details>
        <summary>Implementation</summary>

            *   Collect user agents from HTTP requests from the proxy or NSM logs.
            *	Sort from most common to least common.
            *	Inspect the outliers (the least frequent).

        </details>

        5. Are there any outbound connections generated at regular intervals?

2.  *At least one system is infected by some malware variant that has established itself to autostart and that has not yet been detected.*  

    1.  Are there any new items set to autostart in the investigated system, across this subnet, or in critical servers?

    <details>
    <summary>Implementation</summary>

            *   Collect entries daily from a subset of systems.
            *   Employ least-frequent analysis to sort from most common to least common. 
            *   Inspect the least common ones and look for evidence of:
                *   Random strings in binary names.
                *   Binaries set to autostart from temp locations such as %USER%\APPDATA\Local\temp, the recycle bin, or any other unusual locations. 
                * Unsigned binaries
                * Abnormally short or long filenames.
                * Other rare executable filenames or directories. 
                
    </details>

3.  *An attacker already present on a compromised system is trying to elevate privileges by adding a user to a privileged group.*  

    1.  Is there a new user in a privileged local or domain group? 

4.  *An attacker already present on a compromised system is trying to elevate privileges by exploiting a local vulnerability.*  

    1.  Are there any missing patches that could have been used to attempt a local privilege escalation? 

5.  *An attacker already present on a compromised system is trying to elevate privileges by exploiting file system permission weaknesses.*  

    1.  Is there any binary set as a service that could have been replaced due to poor file-system permissions?

6.  *There’s an active attacker on the network trying to move laterally by employing PsExec.*  

	1. Is there any evidence of PsExec use? 

	2. Is there a new service on any critical servers? 

    <details>
    <summary>Implementation</summary>

			*	Get-WinEvent -FilterHashtable @{logname='system'; id=7045} 
	
	</details>

	3. Are there any errors associated with the start of new services? 

	4. Is there any workstation-to-workstation traffic on my network?

7.  *An attacker is attempting to exfiltrate a large volume of data to a nonbusiness-related geolocation.* 

    1.  Is any workstation or server sending a large volume of data outside the network? 

    2.  Are there any outbound connections to nonbusiness-related geolocations? 
    
    3.  Is data being sent at abnormal times? 
    
    4.  Are there any connections that remain pinned for an abnormally long time?

