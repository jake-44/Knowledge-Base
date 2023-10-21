# Killing Tasks For Evasion or Enumeration --- T1489 

## **Introduction**

This detection is essential for detecting the early steps in the ransomware and malware kill chain. Specifically, this detection catches the disablement of any security services or defenses with the “taskkill” command so that malicious activity can not be observed or denied execution. 

It is said that 98% of ransomware and malware attackers gain initial access through some form of social engineering. The tactics used by these attackers usually include common digital phishing via email, phone, SMS, ect. which grants the user access to the system. 

Although this detection is an essential TTP of malware / ransomware attacks, this particular watchlist was created based on the well-known ransomware, Nefilim, which is a ransomware as a service (RaaS). Nefilim’s main attack vector is through vulnerable and unpatched Citrix software as well as exposed Remote Desktop Protocols (RDP) 3389.

Along with a new wave of double extortion ransomware families, Nefilim affiliates are particularly vicious when victims don’t immediately pay the ransom, leaking their sensitive data over an extended period of time. They are one of few groups that host leaked victim data long-term, for months to years, using it to deliver a chilling message to future victims.

The main stages of the ransomware kill chain are as follows:

![image](https://github.com/jake-44/Knowledge-Base/assets/72994837/5dd77b21-f2ca-4329-9e9c-42b11906451f)

The attacker can be seen lowering defenses of systems within an environment after initial access but before the infection stage. Downloading malware, offensive scripting, and enumeration can be relatively easy to catch for even the average antivirus program. Therefore, the attacker will want to bring down these defenses with the use of taskkill or another process killer before committing any malicious actions, to avoid detection. After successfully lowering these defenses. The attacker is free to download their malware, scripts and toolkits that will effectively run their operation.

## **IOCs & TTPs**  

The Nefilim ransomware uses a batch file to stop services and kill processes in the local host. This batch file abuses taskill.exe using CMD to kill predefined services and processes in the target host. Nefilim distributes this batch file to multiple hosts using two batch files. One of the batch files uses the ‘copy’ command, and the other one uses WMI with hard-coded admin credentials.

![image](https://github.com/jake-44/Knowledge-Base/assets/72994837/22f5aa9b-d6f8-4338-9373-e4efc39a7585)

A batch file that utilizes WMI to distribute the batch file that stops services/kills processes and run the ransomware to multiple hosts, on c:\Windows\Temp. The file contains hard-coded admin credentials.
•	Start wmic /node:[node]/user:[user]/password:[pass] process call create “cmd.exe /c copy \\c$\windows\temp.[file].bat c:\windows\temp\”

A batch file that executes psexec.exe to remotely execute the batch file to stop services/kill processes. The file contains hard-coded admin credentials.
•	**Start psexec.exe \\[file] -u [username] -p [password] -d -h -r upsrv -s -accepteula -nobanner c:\windows\temp\[file].bat**

**[Specific watchlist description and detection tuning as well as specific investigation procedures, redacted for security purposes]**

References:
- https://attack.mitre.org/techniques/T1562/001/
- https://attack.mitre.org/techniques/T1489/exabeam.com/wp-content/uploads/2017/07/Exabeam_Ransomware_Threat_Report_Final.pdf
- https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/taskkill
- https://www.trendmicro.com/vinfo/us/security/news/cybercrime-and-digital-threats/updated-analysis-on-nefilim-ransomware-s-behavior

