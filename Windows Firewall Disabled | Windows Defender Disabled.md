<h1> Introduction </h1>
<h2>Windows Defender</h2>
Microsoft Windows Defender is a very powerful security application. It provides real-time protection against various types of malicious software, including viruses, spyware and other types of malware. Windows Defender continuously monitors system activity, passively and actively scanning files and applications as they are accessed or downloaded. Over the years, it has evolved since its creation to include many different services such as browser protection, network protection, and firewall protection.

<h2>Windows Defender Firewall</h2>
Windows Defender Firewall is a Windows Defender provided tool within its suite of security tools that monitors and controls incoming and outgoing network traffic. The firewall uses a set of rules to control network traffic, allowing or denying specific types of traffic based on the source and destination IPs, ports, ect. of the communication. Serving as an endpoint firewall, the Defender Firewall can have a multitude of different configurations than the network's, perimeter firewall. This greatly reduces the attack surface of a device, providing an extra layer to the defense-in-depth model. Reducing the attack surface of a device increases manageability and decreases the likelihood of a successful attack.

<h1> IOCs and TTPs </h1>
This tactic conducted in the wild is usually followed up with unusual traffic either to or from malicious addresses, involving unwanted activity.

As for common tactics, techniques, and procedures for disabling Windows Defender services, mostly occur following a breach. Although in some cases there are known vulnerabilities which target flaws within Microsoft Windows Defender, other avenues of exploitation are conducted after initial access. This occurrence could stem from malicious software by any means of infiltration such as phishing, embedded USB drives in which contain instructions to disable Windows Defender. Another popular avenue within the kill chain of most ransomware attacks is following a successful privilege escalation, the mass dissemination of PowerShell scripting is then used to lower the defenses of internal hosts including their firewall so that the threat actor can conduct further malicious operations without being detected.

<h1> Resources </h1>
- https://learn.microsoft.com/en-us/windows/security/threat-protection/windows-firewall/windows-firewall-with-advanced-security
- https://attack.mitre.org/techniques/T1562/004/

