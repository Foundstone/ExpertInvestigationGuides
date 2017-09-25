# Playbook: Hunting for Persistence

## Hypothesis

At least one system is infected by some malware variant that has established itself to autostart and that has not yet been detected.  

## Why

In most cases, attackers need to establish some persistent mechanism in their malware so they can control the infected system across sessions and survive a reboot to achieve their objectives.

## Artifacts

Windows Auto Start Extensibility Points (ASEPs).

## Source

Windows Registry, output of Microsoft Sysinternals Autoruns.

## How to

Take daily snapshots and run diffs and least-frequent analysis, focusing on the outliers. 

## Additional References

*	[MITRE ATT&CK Tactics: Persistence](https://attack.mitre.org/wiki/Persistence) 
*   [DeepBlueCLI by Eric Conrad](https://github.com/sans-blue-team/DeepBlueCLI)
*   [Long Tail Analysis of Windows Event Logs by Eric Conrad](http://www.ericconrad.com/2015/01/long-tail-analysis-with-eric-conrad.html)


## Questions

1.  *At least one system is infected by some malware variant that has established itself to autostart and that has not yet been detected.*  

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




