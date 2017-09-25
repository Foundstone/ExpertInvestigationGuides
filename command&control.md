# Playbook: Hunting for Command and Control

## Hypothesis

An infected system on the network is generating outbound command and control traffic that has not yet been detected. 

## Why

Malware does not run in a vacuum. It needs to contact the attacker’s infrastructure to download additional payloads, receive instructions on which actions to execute on the endpoints, and to report information from the victim’s network. This requires outbound connections originating from the compromised hosts to the attacker’s control server.

## Artifacts

DNS requests and responses, user-agent strings in HTTP requests.

## Source

NS logs from DNS servers with Microsoft DNS Analytics/Proxy logs, or Network Security Monitor (NSM) data from Bro sensors.

## How to

Perform least-frequent analysis on both DNS and user agentes

## Additional References

*	[MITRE ATT&CK Tactics: Command and Control](https://attack.mitre.org/wiki/Command_and_Control) 
*	[Threat Hunting Project](https://github.com/ThreatHuntingProject/ThreatHunting/tree/master/hunts) 
*	[Identifying Malware Traffic with Bro](http://blog.opensecurityresearch.com/2014/03/identifying-malware-traffic-with-bro.html)
*	[Detecting Random - Finding Algorithmically chosen DNS names (DGA)](https://isc.sans.edu/forums/diary/Detecting+Random+Finding+Algorithmically+chosen+DNS+names+DGA/19893/)
*	[Network Forensics with Windows DNS Analytical Logging](https://blogs.technet.microsoft.com/teamdhcp/2015/11/23/network-forensics-with-windows-dns-analytical-logging/)


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


                


