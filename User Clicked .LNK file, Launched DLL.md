<h1> Introduction </h1>
This detection is specifically looking for the execution of .DLL binaries spawning from a .LNK file. Shortcut files (.LNK) are typically used to quickly access a program or folder from your personal computer desktop. Threat actors can sneak a malicious code in the command line of the LNK file's target path. An adversary may rely upon a user opening a malicious file in order to gain execution. Users may be subjected to social engineering to get them to open a file that will lead to code execution. This user action will typically be observed as follow-on behavior from a Spear phishing Attachment. As soon as the user opens the LNK file or the parent file such as an .ISO file, the malware infects their computer, in most cases without the user realizing anything is amiss.

Adversaries may employ various forms of Masquerading and Obfuscated Files or Information to increase the likelihood that a user will open and successfully execute a malicious file. These methods may include using a familiar naming convention and/or password protecting the file and supplying instructions to a user on how to open it. The most popular malware family tree is the BumbleBee malware shown below:

![image](https://github.com/jake-44/Knowledge-Base/assets/72994837/276c8545-e5f6-44dd-b960-61fd7ab024f4)

Before diving into any indicators of compromise and tactics, techniques and procedures, please visit the sites below if you require any additional explanation of .LNK files, or malware associated with this activity.

- https://www.cynet.com/blog/orion-threat-alert-flight-of-the-bumblebee/

- https://www.mcafee.com/blogs/other-blogs/mcafee-labs/rise-of-lnk-shortcut-files-malware/

<h1> IOCs and TTPs </h1>
Now that we understand the origins of this malicious activity and the functionality of the file types which carry the embedded DLLs, we can start to breakdown the attack chain into identifiable parts.

**[Specific watchlist description and detection tuning as well as specific investigation procedures, redacted for security purposes]**

C:\Windows\System32\cmd.exe /c start rundll32 namr.dll,IternalJob

This is an example of the BumbleBee malware noted above which runs the Windows tool rundll32 to execute the custom created binary and calls the function "InternalJob" to start the process. Therefore the strings noted above are important to detect.

<h1> References </h1>
- https://thedfirreport.com/2022/08/08/bumblebee-roasts-its-way-to-domain-admin/
- https://www.cynet.com/blog/orion-threat-alert-flight-of-the-bumblebee/
- https://www.mcafee.com/blogs/other-blogs/mcafee-labs/rise-of-lnk-shortcut-files-malware/
- https://attack.mitre.org/techniques/T1204/002/

