<h1> Introduction </h1>

**Server-Level Firewall Rules**

Azure SQL Database creates a firewall at the server level for single and pooled databases. These rules enable clients to access your entire server, that is, all the databases managed by the server. This firewall blocks connections from IP addresses that do not have permission to access all of these databases. To connect to an Azure SQL database from an IP address outside of Azure, you need to create a firewall rule. You can use rules to open a firewall for a specific IP address or for a range of IP addresses.

<br> **Database-Level Firewall Rules**

Database-level IP firewall rules enable clients to access certain (secure) databases. You create the rules for each database (including the master database), and they're stored in the individual database. This creates a relatively simple way of segregating access control to the individual databases. By using the database firewall, you can ensure only the IP addresses you define can access the databases it is assigned to access while denying access to restricted databases.

_<p align="center"> Below is a flow chart detailing firewall controls to the databases.</p>_

![image](https://github.com/jake-44/Knowledge-Base/assets/72994837/6e0768f8-9d26-43c8-a8c0-42599060ecfb)


<h1> IOCs and TTPs </h1>
User making an update to an Azure SQL Server Firewall Rule. Although in other cases, this tactic conducted in the wild is usually followed up with unusual traffic either to or from malicious addresses, involving unwanted activity (Data Exfiltration), other indicators will be based on the traffic allowed and traffic denied. Disabling traffic coming through the firewall can lead to a successful denial of service attack that blocks all legitimate communications between an Azure tenant and the databases or traffic to and from the internet. Unfortunately for this AlienVault detection we do not have insight as to what is being updated within the rule. We don't know if malicious IP address are being added or if legitimate ones are being removed. 

<br> As for common tactics, techniques, and procedures for modifying a firewall rule, they mostly occur following a breach. Although in some cases there are known vulnerabilities which target flaws within Microsoft Azure specifically, other avenues of exploitation are conducted after initial access to the Azure tenant. Modifying firewall rules are used to lower the defenses of internal hosts, databases and networks so that the threat actor can conduct further malicious operations.

<h1> Resources </h1>
- https://virtual-dba.com/blog/firewalls-database-level-azure-sql/
<br> - https://learn.microsoft.com/en-us/azure/azure-sql/database/firewall-create-server-level-portal-quickstart?view=azuresql
<br> - https://learn.microsoft.com/en-us/azure/azure-sql/database/firewall-configure?view=azuresql
