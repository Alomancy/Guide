---
description: Outline of a internal Infrastructure. In no way complete!
---

# Internal Infrastructure

## Pre-Test Checks

### Arrange a kick-off meeting with the primary contact or network/system architects

Understand the customer's requirements and expectations. Outline any issues the test may cause as well as limitations, discuss potential alternatives. Understand how the system works either via speaking with the designers of via system's schematics, and identify the areas that should be tested. Discuss with the client.

### Define a scope tailored to customer's requirements

As a general guideline avoid the use of tools that are not included in the Approved Test Tools list on the intranet and avoid any techniques and exploits that may directly cause a denial-of-service condition, unless otherwise agreed. A number of approved tools may cause a denial-of-service condition depending on servers' configuration and design \(i.e. nikto\), these tools are allowed under the condition that the customer is aware of the potential consequences, has agreed to their use and the target systems are not business critical.

### Define an "alert system"

Identify when and how the customer would like to be notified of any findings, and what type of findings should be raised. If no preference is given, refer to our standard policy. E.g. Critical issues are raised as they are identified High and medium risk are rasied during the final washup meeting before concluding the engagement. Low risk issues can be directly shown in the final report.

### Obtain a signed consent form containing IP addresses/hostnames of all the targets in scope

Define the targets in scope and a contact to refer to in case of any problems.

### Obtain network connectivity

Either via wifi or via plugging into the internal LAN \(this should be defined during kick-off meeting\). Check connectivity and make sure the targets in scope are visible. Make sure DHCP or a static IP address is provided. If access controls are in place \(i.e. 802.1x\), make sure exceptions have been made to allow connectivity \(unless access controls checks are within testing scope\)

### Where relevant, obtain Windows AD credentials

### Create a log file and record all the outcome from the previous steps

In particular, record targets, customers' concerns and expectations and emergency contacts. Also keep track of all the steps below. Each tool used and technique should be recorded with a timestamp

### Setup any of the tools that will be used to log attacks and outputs

### Confirm with the client whether there are delicate targets or critical servers and services we need to be particularly aware of

## Active Recon

### Enumerate services and versions

Tools:

* Nmap
* Metasploit

Discover services running on the discovered devices, enumerate versions. Using the MSF database is a good way to keep track of it all.

### Identify software banners, path levels and fingerprint

Tools:

* Nmap
* Metasploit

Identifying software banners is the first step to identify valid exploits and default credentials. This can also assist in identifying targets roles

### Identify clear text authentication

Tools:

* Nmap
* Metasploit
* Nessus

Discover services accepting clear text authentication such as ftp, telnet, http

### HTTP Screenshots

Tools:

* Httpscreenshot: [https://github.com/breenmachine/httpscreenshot](https://github.com/breenmachine/httpscreenshot)
* Eyewitness: [https://github.com/FortyNorthSecurity/EyeWitness](https://github.com/FortyNorthSecurity/EyeWitness)

Run HTTP screenshot scripts to grab screenshots of the identified HTTP services and identify any further interesting targets and issues \(i.e. old software, unencrypted logons, consoles not requiring credentials\)

### Vulnerability scanning

Tools:

* Nessus

Select targets for vulnerability scanning, this list will depend on the context of the test, client wishes and 'gut feel' of the tester.

### Manual Vulnerability identification

Tools:

* Metasploit
* Searchsploit
* Web Browsers
* Nikto
* Dirbuster
* SNMP tools
* etc.

Using the information gathered in the previous steps attempt to identify vulnerabilities within the network which aren't picked up by automated scanners.

### Share browsing

Tools:

* File Browsers
* Hyena: [https://www.systemtools.com/hyena/](https://www.systemtools.com/hyena/)
* SMBtools

After enumerating all shares available, either unauthenticated or with compromised accounts, gather any interesting documents \(passwords in doc/xlsx, IT config docs, board level docs etc.\).

## Exploitation

### Password guessing \[if in scope\]

Tools:

* Hydra
* Metasploit

If brute forcing is in scope and a valid list of domain users was found, attempt to brute force discovered usernames, bearing in mind any lockout policies. A good password to start with is Password1 if that matches their policy. Also CompanyName1 typically returns great results. Other passwords to consider: Summer2021, Password123, Company123, etc.

### Check default passwords

Tools:

* Hydra
* Metasploit
* Manual

Where appropriate identify and test default credentials, internal web interfaces in particular tend to be left with default settings \(i.e. printers, storage devices, etc.\) N.B. Make sure to limit the risk of locking accounts out and check with client if unsure

### Check default SNMP strings

Tools:

* onesixtyone
* snmp-check

Verify whether the default public or private strings are accepted. If relevant and in scope more strings can be attempted \(i.e. using a dictionary attack\)

### Attempt DNS Zone Transfers

Tools:

* nslookup
* dnsenum

DNS Zone Transfers will in most cases be possible internally. A successful attack can provide precious details on network layout and more rewarding targets

### Compromise internal services

Tools:

* Web Browser
* Brain

Using compromised accounts attempt to authenticate to internal services \(OWA, sharepoint etc.\) to extract more info.

### Collate all viable exploits

Tools:

* Brain

Collect all the information and list the viable exploits, this could be as simple as default passwords, or more technical attacks using publically available or custom code.

### Exploit targets \[if in scope, confirm with customer first or as per initial pre-test agreements\]

Tools:

* Multiple tools
* Code Samples
* exploitdb
* google

Run exploits to gain access to systems if appropriate. N.B. if any of the exploits affects a critical server or may cause a denial-of-service state you need to verify with the client if they are happy to carry out the test

## Post-Exploitation

### Alert customer

Alert the customer of the finding if relevant \(as per initial agreement\) and discuss further options and tests

### Collect data

Collect information from exploited machines, such as ssh keys, password hashes, documents and screenshots for records.

### Escalate privileges \[if in scope\]

Tools:

* Linpeas
* WinPeas

If required and within scope, attempt to identify further exploits and vectors to gain full admin privileges.

### Browse shares and file system with elevated privileges

Repeat the collect data step with the new elevated privileges. Browse the file system for scripts which may contain credentials

### Pivot \[if in scope\]

Use the exploited target to pivot through further network segments and targets if in scope

### Re-Iterate

Using the information collected consider repeating any relevant step which may produce extra results

