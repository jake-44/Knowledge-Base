<h1> Introduction </h1>
This activity appears to be adware. Although metadata is very limited, we have identified a Toolbar Extension program and the associated activity to be related to the publisher **Blaze Media**.

Heading into the indicators of compromise and some common tactics, techniques, and procedures, it is important to understand that the process tree is usually very large and can be overwhelming, but this KB is intended to make it more manageable. 

<h1> Introduction </h1>
Please note that there is A LOT of data to look at in these cases from persistence beaconing, to identifying the download, or observing an update for the adware. **Again, to reiterate, the process tree for this detection is usually very large and can some times vary depending on what stage of the kill chain is detected. However, this KB is intended to make it more manageable.**

1.	Most instances will be show tactics of two activities.

- Powershell download cradle

- New scheduled task created through powershell

2.	The parent process is msiexec.exe and the child process is PowerShell which indicates some kind of installation is occurring.

3.	There are usually around 20 command scripts that are a part of the payload. We intended to investigate the contents of the scripts for what exactly was downloaded or visit the process tree.

**<p align="center"> [Removed Image] </p>**

![image](https://github.com/jake-44/Knowledge-Base/assets/72994837/41b5e7a2-e603-4ae2-bddf-15d5c2279985)

After expanding the process tree, you will see numerous amounts of PowerShell scripting, temp file executions and instances of msiexec. Follow the process flow from start to finish to find out what exactly is being downloaded here.
**Please note that the malicious downloaded file will be different from case to case. The malicious domains will be different as well.**

4. We can observe that this installation is originating from the internet by looking at the command msiexec spawning from chrome.exe
- The downloaded file in this case is a “setup” file look-a-like for no specific program, which lands in the user’s “\Downloads” directory noted below:
- 
  **"C:\Windows\System32\msiexec.exe" /i "C:\Users\[redacted]\Downloads\Setup_40552697.msi"**
  
  _It is recommended that during investigation, these .msi files are opened within the sandbox to conduct further
  behavioral analysis_

After identifying the suspicious file that was downloaded, we still don’t understand what exactly is being installed onto the system.

5. We can continue to follow the process tree to the next event which takes us to our first .tmp file that appears to be spawning chrome.exe **(Reaching out to the internet)**

- The command line observed in the temp file is reaching out to the domain **malicious1[.]com/ext/ruftyp/40552797** which when accessed in the sandbox, redirects the user to **malicious2[.]com/ext/ruftyp/40552697** then downloads a randomly named executable, finally landing on the page **malicious3[.]cloudfront.net/exeflow/thankyou/download.html** **[edited]**
 
_This is clearly NOT good given that the domains are not registered and cannot be associated with a legitimate organization._

6. After sifting through the msexec.exe files, you will find two that have the command line below and each spawn a temp file.

- **"C:\Windows\system32\msiexec.exe" /i "C:\Users\[redacted]\AppData\Roaming\Eclipse Media Inc\Installer   Assistant\prerequisites\WCSetup_ExeWC.msi" /q**
- The temp files include the below commands:

**"C:\Windows\Installer\MSID762.tmp" /DontWait /HideWindow /dir "C:\Users\[redacted]\AppData\Roaming\BBWC\" C:\Windows\SysWOW64\WindowsPowerShell\v1.0\powershell.exe -noninteractive -ExecutionPolicy bypass -c "$w="$env:APPDATA"+'/BBWC/'; [Reflection.Assembly]::Load([System.IO.File]::ReadAllBytes($w+'WebCompanion.dll'));[WebCompanion.StartUp]::Start()"**

_<p align="center">This is installing contents into a directory located in "C:\Users\[redacted]\AppData\Roaming\BBWC\"</p>_

And

**"C:\Windows\Installer\MSIF1DB.tmp" /DontWait /HideWindow /dir "C:\Users\[redacted]\\AppData\Roaming\Browser Extension\" C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy bypass -c "$w="$env:APPDATA"+'/Browser Extension/';[Reflection.Assembly]::Load([System.IO.File]::ReadAllBytes($w+'BrowserExtension.dll'));[WebCompanion.BrowserExtension.S]::Start()"**

_<p align="center">This is installing contents into a directory located in "C:\Users\[redacted]\AppData\Roaming\Browser Extension"</p>_

7. At least one of the PowerShell scripts creates a scheduled task by the name of “**\WC ScheduledTask**” which is stored in the Windows default scheduled task directory, “**C:\Windows\System32\Tasks**”. This task is scheduled to create persistence on the system and to check for software updates.

To confirm your findings, remote into the host in question and navigate to C:\Users\[ user ]\AppData\Roaming and C:\Windows\System32\Tasks and locate the activity. 

<h2> Pertinent Information </h2>

**File Paths**
  C:\Users\[ user ]\AppData\Roaming\BBWC
  C:\Users\[ user ]\AppData\Roaming\Browser Extension
  C:\Users\[ user ]\AppData\Roaming\Eclipse Media Inc (If Observed)

**Scheduled Task**      
  C:\Windows\System32\Tasks\WC ScheduledTask


<h1> References </h1>
- https://www.joesandbox.com/analysis/627595/0/html
