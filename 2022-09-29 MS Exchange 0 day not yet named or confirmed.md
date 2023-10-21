<h1> Introduction </h1>
Microsoft Exchange Servers are mail servers and calendaring servers developed by Microsoft. They run exclusively on Windows Server operating systems. This is a widely used exchange server by very small businesses to large corporations around the world. A zero day involving the end result of successful remote code execution was discover in the wild, first observed in the beginning of August by a Security Operations Center based in Vietnam called GTSC and was later included in a patch distributed by Microsoft. However, between August and November, many organizations experienced the power of this exploitation, and some even post-patch.

An honorable mention includes a well known cloud service provider Rackspace in early December 2022. Though unconfirmed, experts have reason to believe that Rackspace was running a Microsoft Exchange server version that is vulnerable to the “ProxyNotShell” vulnerability which is what this zero-day is being tagged as. This exploit discovered in the wild just two months ago, installs web shells on Microsoft Exchange servers. Although Microsoft had patched this vulnerability in November, Rackspace did not keep up to date with their patches and was running the previous server patch version from August that did not cover the specific zero-day vulnerability. Four days after the release of a potential breach, Rackspace confirmed that the affected exchange server is the result of ransomware and is too early to tell what data might have been accessed and how much revenue will be lost. Not to mention the lingering loss of business following the event, all due to patch management.

- https://www.bleepingcomputer.com/news/technology/rackspace-ongoing-exchange-outage-caused-by-security-incident/ - Rackspace Initial Report
- https://www.bleepingcomputer.com/news/security/rackspace-confirms-outage-was-caused-by-ransomware-attack/ - Rackspace Incident Report
- https://msrc-blog.microsoft.com/2022/09/29/customer-guidance-for-reported-zero-day-vulnerabilities-in-microsoft-exchange-server/ - Microsoft Zero-Day Report and Mitigation

<h1> IOCs and TTPs </h1>
Identification - 
GTSC's Blueteam discovered exploit requests in IIS logs with the same format as the long-known ProxyShell vulnerability. Kevin Beaumont writes here that the attackers pretend to be an Exchange EWS to set up a backdoor. The attack is done via the following request:
<br>

![image](https://github.com/jake-44/Knowledge-Base/assets/72994837/3f21fbac-9d49-448c-8b58-0f3a1f0cc1dc)

The link above is used to access a component in the backend where the remote code exploit (RCE) could then be implemented. According to GTSC, the attackers make use of various techniques to insert backdoors into the affected Exchange system and then move laterally on the network to other servers in the system.

During the investigation, the security researchers discovered webshells, most of which were created hidden on the infected Exchange servers. Based on the user agent, the GTSC team was able to determine that the attacker was using Antsword. This is an active cross-platform open-source website management tool used by China's hackers to help manage webshells. Here is a JScript about it:

![image](https://github.com/jake-44/Knowledge-Base/assets/72994837/1ff88625-672b-488b-8aba-d6f235e28499)

The security team suspects that these backdoors originated from a Chinese attack group because the webshell uses code page 936, a Microsoft character encoding for simplified Chinese. Another notable feature, security researchers said, is that the hacker also modified the contents of the RedirSuiteServiceProxy.aspx file for the webshell. RedirSuiteServiceProxy.aspx is a legitimate file name available on the Exchange server.

![image](https://github.com/jake-44/Knowledge-Base/assets/72994837/9624efc1-2bf2-4972-b0f5-ea121cf558f5)

The image above shows in detail the kill chain taken to exploit this vulnerability including the two Common Vulnerabilities and Exposures below:

https://msrc.microsoft.com/update-guide/vulnerability/CVE-2022-41040 - Server Elevation of Privilege Vulnerability (Server-Side Request Forgery)
https://msrc.microsoft.com/update-guide/vulnerability/CVE-2022-41082 - Server Remote Code Execution Vulnerability 


The GTSC security researchers have also provided some Indicators of Compromise (IOCs) that can be used to identify an infection assocaited with the webshell and IP addresses involved in the links below


<h1> Resources </h1>
- https://msrc.microsoft.com/update-guide/vulnerability/CVE-2022-41040 - Server Elevation of Privilege Vulnerability (Server-Side Request Forgery)
- https://msrc.microsoft.com/update-guide/vulnerability/CVE-2022-41082 - Server Remote Code Execution Vulnerability 
- https://www.bleepingcomputer.com/news/security/rackspace-confirms-outage-was-caused-by-ransomware-attack/ - Rackspace Incident Report
- https://www.bleepingcomputer.com/news/technology/rackspace-ongoing-exchange-outage-caused-by-security-incident/ - Rackspace Initial Report
