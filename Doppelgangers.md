# **Doppelgangers**

<h2 align="center"> Introduction </h2>
If you want to know how a Doppelganger works, we need to be able to understand what domain names are and how they work. Domain names are in place to help translate one, or many IP addresses into a name that uniquely identifies the business’ domain being accessed. This naming system is better known as the domain naming system (DNS) which is often referred to as "the phonebook of the internet". Where a contact list holds phone numbers for names of phone number owners, the DNS holds IP addresses for unique domain names. However, domain names that are currently not in use can be purchased or sometimes acquired for free. This opens the door for potential threat actors being able to get a hold of domain names that look similar to, but are not owned by, a legitimate business organization.Threat actors register these look-alike domains to impersonate well-known companies in order to leverage their credibility and make a profit from scamming users.

<h2 align="center"> IOCs and TTPs </h2>
If you have your Security+, you have probably heard of the term “typo squatting”. If you haven’t heard of it, you have most likely experienced the pain of trying to access websites such as amzon.com or gooogle.com and misspelled the name by accident… Did you catch those naming errors? It’s that simple. Threat actors take advantage of the fact that humans are not perfect and tend to overlook their mistypes. Misspelling the domain you wish to access can actually lead you to a threat actor’s domain, instead of the legitimate one, if they have it registered. If you haven’t caught your mistake yet, you might have no idea if you're visiting a malicious website or not. The domain is usually set up to look EXACTLY like the domain you wanted to initially access, hence the name Doppelganger!

Below are a few naming techniques that attackers use to hide their doppelgangers in plain sight **(referencing phishlabs.com)**:

![image](https://github.com/jake-44/Knowledge-Base/assets/72994837/7acd454c-fd4e-4eec-ae6b-cee1ef99f07f)

<p align="center">
These techniques take advantage of every domain of a website URL address including the subdomain, second-level domain, and top-level domain.
</p>

![image](https://github.com/jake-44/Knowledge-Base/assets/72994837/c605d69b-5239-4065-8ce3-9b83b401f500)

**Tools you’ll need to set yourself up for success:**
- **https://centralops.net/co/** - The Domain Dossier tool generates reports from public records about domain names and IP addresses to help solve problems, investigate cybercrime, or just better understand how things are set up. These reports may show you:
  - Owner’s contact information
  - Registrar and registry information
  - The company that is hosting a Web site
  - Where an IP address is geographically located
  - What type of server is at the address
  - The upstream networks of a site

This information is critical to provide to our clients so that they are aware of these sophisticated social engineering attacks and can assist their business in evading them.

Both of these tools are useful when centralops does not provide the information you need for your investigation:
- MX record search https://mxtoolbox.com/
- Whois.domaintools.com

Now that we have unveiled the attacker’s primary TTPs and how to identify a legitimate look-a-like domain, we can verify a doppelganger case by going through the following investigation procedure below.

<h2 align="center"> Investigation </h2>

**Domain’s Physical Appearance**

1.	Some things to consider:
- Does the domain load as an active web server?
  - Can the legitimacy of this web server be correlated with another business?
    - Usually if the domain names are almost identical, such as google.com and goggle.com, this should warrant an alert so       the client can avoid mistyping their own domain name
  - Is the domain secure?
  - What is the domain asking for and what services does it provide **(if any)**?
- If there is an error loading the domain, what information is provided?
2.	Now, by using the original domain we noted before from the log, it is beneficial to compare the domain in question with the client verified and owned domain name **(followed by .com, .org, ect.)**.
 
**Domain’s Operations** 

At this point, we should have a general idea about whether the domain is a true doppelganger but to confirm our suspicions, there are a few more tactics that are crucial to our investigation.
- Navigate back to the case in Aegis and click on the link provided in each doppelganger alert, centralops.net/co/
a. Most domains will have an ‘A record’ indicating their claim on an IPv4 address or an ‘AAAA record’ for a mobile IPv6 address
b. Confirm if this domain has any ‘NS records’ which usually indicates if this domain is an active web server
c. Viewing any ‘MX records’ identifies this domain as an active mail server

_**<p align="center"> This supporting documentation will be beneficial for reporting </p>**_

- Viewing the page sources can help in some cases where you cannot identify the differences between the two domains. (This will require some knowledge about HTML, CSS and JavaScript languages)
- Google is always your friend as an analyst. We can research what the target domain is or who it is owned by (stay within the sandbox when clicking on links associated with the domain)
 
**Closure**

There are a few actions we can make at this point:
- Report the information you have found for the domain name in question
  - Web Server (Yes / No)
  - Mail Server (Yes / No)
  - Doppelganger Domain Name
- Close the investigation with supporting details.

References:
- https://www.phishlabs.com/blog/what-is-a-look-alike-domain/
- https://attack.mitre.org/techniques/T1583/001/
- https://unit42.paloaltonetworks.com/cybersquatting/#:~:text=Executive%20Summary&text=This%20is%20known%20as%20cybersquatting,.%5Dcom%20for%20WhatsApp).


