# Expert Investigation Guides
 
## Threat Hunting Guides

These investigation guides are based on the article: 

 *  ["Threat Hunting like a PRO" by Ismael Valenzuela & Douglas Frosst, McAfee Labs Quarterly Threat Report, September 2017](TBD)

The following section describes some of the most effective hunts you can employ based on some logs commonly found in an average organization. None of these should be considered in isolation, but rather as part of a process that incorporates the key elements we have described. 

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


                


