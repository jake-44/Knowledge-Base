<h2> Introduction </h2>
This detection is specifically looking for the execution of scripting files spawning from a .LNK file. Shortcut files (.LNK) are typically used to quickly access a program or folder from your personal computer desktop. Threat actors can sneak a malicious script in the scripting command of the LNK file's target path. As soon as the user opens the LNK file, the malware infects their computer, in most cases without the user realizing anything is amiss. There are a few ways these files can land onto a target's system such as embedded hyperlinks in .DOCX files, phishing emails, malicious websites, .ISO files, and USB drives. These are all forms of social engineering in attempt to bypass network security for the most successful and quickest way to load malware onto a machine. Very famous and relevant malware within this family is EMOTET which is identified by the kill chain sequence below:

![image](https://github.com/jake-44/Knowledge-Base/assets/72994837/fb2f8ebe-e04c-4c1f-beae-5984a13255f7)

Before diving into any indicators of compromise and tactics, techniques and procedures, please visit the sites below if you require any additional explanation of .LNK files, or malware associated with this activity.

- https://success.trendmicro.com/dcx/s/solution/1118391-malware-awareness-emotet-resurgence?language=en_US#:~:text=Emotet%20evolved%20multiple%20times%20over,%2C%20QBOT%2C%20and%20RYUK%20Ransomware.
- https://www.opswat.com/blog/shortcut-lnk-files-may-contain-malware

<h2> IOCs and TTPs </h2>
Now that we understand the origins of this malicious activity and the functionality of the file types which carry the embedded code, we can start to breakdown the attack chain into identifiable parts. 

The reason why VB scripting is being used by the actor instead of PowerShell in this type of malware is because VBScript is "lighter" than PowerShell. It utilizes less memory and is generally "faster" than PowerShell at doing the same tasks. This means that the threat actors want it completed quickly and silently. However, after recent activity, Emotet has adopted the use of PowerShell seen below:

- https://www.bleepingcomputer.com/news/security/emotet-malware-now-installs-via-powershell-in-windows-shortcut-files/

Outlined in red are the parameters we are looking for "cmd", "lnk", and "vbs". From this detection, it looks like a desktop game is being utilized called "Goodgame Empire" located in the user's "\AppData\Romaing" directory. From an analyst's standpoint. This activity does not indicate malicious nature but rather detection identified a potentially unwanted program being ran. It is recommended that checking for additionally activity surrounding this detection is good practice in the case that this activity was obfuscation for other scripting.

![image](https://github.com/jake-44/Knowledge-Base/assets/72994837/42d436d9-843a-4393-b5bd-b5b53ee45ffe)

<h2> References </h2>

https://blog.cyble.com/2022/04/27/emotet-returns-with-new-ttps-and-delivers-lnk-files-to-its-victims/
https://devblogs.microsoft.com/oldnewthing/20190403-00/?p=102381
https://attack.mitre.org/techniques/T1204/002/
https://success.trendmicro.com/dcx/s/solution/1118391-malware-awareness-emotet-resurgence?language=en_US#:~:text=Emotet%20evolved%20multiple%20times%20over,%2C%20QBOT%2C%20and%20RYUK%20Ransomware.
https://www.opswat.com/blog/shortcut-lnk-files-may-contain-malware
