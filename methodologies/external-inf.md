---
description: Needs updated!
---

# External Inf



## Prior to test starting

1. Check for signed consent and PO in Client Docs.
2. Check ownership of IP addresses.
3. Check third-parties have been made aware of testing, and client has provided evidence.
4. Get testing authorisation signed.
5. Confirm with the client whether there are delicate targets or critical services we need to be aware of and more in general if there is anything that may suffer under intensive scanning

## Tools to run \(all tests\)

1. [ ] Nessus
2. [ ] Nmap
3. [ ] Subdomain brute force \(sublist3r\)/Google dork search \(site:\) for any discovered domains, and check subdomains on IP addresses in scope

## Tools to run \(HTTP services\)

* [ ] Nikto
* [ ] Dirbuster/Gobuster/ffuf
* [ ] testssl/sslscan
* [ ] WPscan
* [ ] CMSmap
* [ ] eyewitness

## Test Services

| Category | Service | Test | Test Description |
| :--- | :--- | :--- | :--- |
| Scanning |  | Qualys |  |
|  |  | Nessus |  |
|  |  | Nmap TCP |  |
|  |  | Nmap UDP |  |
| Testing |  |  |  |
|  | FTP | Anonymous access | Nmap script scan should pick this up, as will Qualys and Nessus. Can also check it manually. |
|  | FTP | Software version \(banner grab\) & check vulnerabilities | Nessus, Nmap and Qualys should pick this up. Can also check manually using Ncat or Telnet. Search for applicable software vulnerabilities as well.  |
|  | FTP | Insecure \(plaintext\) connection | Qualys will pick this up, but should be confirmed manually as well. Check you can send credentials without providing AUTH TLS. Can be verified with FileZilla, as some companies run and use an FTPS service normally but the plain text version may also be available and accept creds. |
|  | FTP | Bounce attack | Nmap script scan should pick this up, as will Qualys. |
|  | FTP | Brute-force attack | Manual check using FTP client, send several requests and see whether or not you get blocked. Nmap also has a script. |
|  | SSH | Brute-force attack | Connect to the service and launch several authentication requests, you'll get disconnected and the available authentication methods should be shown in brackets. The service should be vulnerable if Password authentication is permitted. Try again, and see whether or not you can reconnect and send requests. |
|  | SSH | Software version \(banner grab\) & check vulnerabilities | Nessus, Nmap and Qualys should pick this up. Can also check manually using Ncat or Telnet. Search for applicable software vulnerabilities as well.  |
|  | Telnet | Brute-force attack | Connect to the service and launch several requests, keep going until you get locked out or hit a minimum threshold \(e.g. 10\). |
|  | Telnet | Software version \(banner grab\) & check vulnerabilities | Nessus, Nmap and Qualys should pick this up. Can also check manually using Ncat. Search for applicable software vulnerabilities as well.  |
|  | Telnet | Search for and try default credentials for identified version | search Google for &lt;software&gt; default credentials and try them as appropriate. |
|  | Telnet | Insecure \(plaintext\) connection | Qualys and Nessus should pick this up, but should be confirmed manually too. |
|  | SMTP | Mail relay | For manual testing follow this link \( http://www.cs.cf.ac.uk/Dave/PERL/node175.html \). Nmap also has a script to check for this.  |
|  | SMTP | SMTP VRFY User Enumeration | Nmap has a script for this. |
|  | SMTP  POP  IMAP | Brute-force attack | Nmap and Metasploit have modules for this, can also check manually by repeatedly connecting to the service and supplying false credentials. |
|  | SMTP  POP  IMAP | Insecure \(plaintext\) connection | The tools should pick this up, however you can check manually simply by connecting to the service using ncat/telnet.  |
|  | SMTP  POP  IMAP | Software version \(banner grab\) & check vulnerabilities | Nessus, Nmap and Qualys should pick this up. Can also check manually using Ncat. Search for applicable software vulnerabilities as well.  |
|  | SIP | Check for plaintext and/or over UDP | Plaintext SIP runs over 5060/tcp and TLS SIP runs over 5061/tcp |
|  | SIP | Check for method enumeration | It is a text-based request/response protocol like HTTP, request methods include REGISTER/INVITE/ACK/BYE |
|  | DNS | DNS Zone Transfer | Qualys should pick this up and nmap also has a script for it. For manual verification type: \#host -t ns domainname, then, \#host -l domainname dnsservername  |
|  | DNS | Software version \(banner grab\) & check vulnerabilities | Nessus, Nmap and Qualys should pick this up. Can also check manually using Ncat. Search for applicable software vulnerabilities as well.  |
|  | HTTP/S | Software version \(banner grab\) & check vulnerabilities | Nessus, Nmap and Qualys should pick this up. Can also check manually using Ncat. Search for applicable software vulnerabilities as well.  |
|  | HTTP/S | Web inteface examination | For a large number of discovered web interfaces on a number of Ips, EyeWitness can be used to do a scan of all of these for a bulk examination of the ones discovered |
|  | HTTP/S | Brute-force attack | Check directories discovered by Nmap/Dirbuster/Qualys and browse to them. Is there any clear sign of two-factor authentication enabled? Is the interface accessible over HTTP?  Do any of the interfaces look as though they might lead to administrative functions? |
|  | HTTP/S | Look for Basic and NTLM authentication prompts | Check directories discovered by Nmap/Dirbuster/Qualys and browse to them.Is the interface accessible over HTTP? Check the server response using ncat/telnet/burp and see if Basic or NTLM is mentioned. Is there an internal IP address in the Basic header? |
|  | HTTP/S | NTLM authentication information disclosure | If NTLM login prompts are discovered, it's likely that NTLM authentication will diclose information about the server. Nmap has a script to check for this, you might need to specify the folder for the NTLM login prompt.  |
|  | HTTP/S | Run Dirbuster to check for directories.  | Let dirbuster run in the background while you perform other tests. Don't let the number of threads go too high otherwise you may crash the server. 3 threads is usually a good number, it shouldn't exceed about 70 requests/second |
|  | HTTP/S | Run nikto | Nikto checks for a variety of web-based vulnerabilites and should be run on all web services. |
|  | HTTP/S | Check robots.txt | These tools should locate the file if it exists. Browse to it and see if you can find anything sensitive.  |
|  | HTTP/S | Internal IP address disclosure | All the tools should find this. You can confirm using ncat or telnet |
|  | HTTP/S | Error messages | Dirbuster may find 500 responses, check these for software version leakage. For IIS servers, request /\|.aspx and see what is returned.  |
|  | HTTP/S | WordPress | If you find WordPress, run wpscan and explore its findings, such as vulnerabilites for installed plugins, username enumeration, administrative login etc. |
|  | HTTP/S | HTTP methods | Check HTTP methods, looking for PUT/DELETE or other WebDAV methods. The tools should pick this up manually. If you find PUT, use Metasploit module. However with modern web apps running on the server, these methods are sometimes reserved for APIs within the applications |
|  | LDAP | Check for network enumeration | Nmap and Qualys will both pick up information if it exists. Use the Ldap browser in Windows to look at this manually |
|  | HTTPS | Look at certificate to determine host name | browse to the 443/tcp port. Click on the small icon to the left of the url to reveal the name of the certification used. Does this indicate another potential target \(i.e. url?\). This can also be retrieved by running SSLScan and looking at the URI in the subject name. Sometimes browsing to this URI will reroute to an interface when simply using the IP won't, due to virtual hosting. Try to browse to this and record your findings |
|  | HTTPS | Check strength of SSL certificate | These tools will find issues with the certificate such as expired or weak signing. |
|  | HTTPS | Run SSL Labs | Browse to https://www.ssllabs.com and enter the domain name \(if one has been identified\). Also remember to tick the box which prevents results from showing on the board. |
|  | HTTPS | Check SSL ciphers | Qualys and Nessus will pick this up, you can double check using sslscan.  |
|  | HTTPS | BREACH Attack | Qualys will pick this up as an informational finding. Can also use openssl to verify - if the following commands return a compressed message, it's vulnerable. Openssl s\_client -connect \[IP:port\]  GET / HTTP/1.1  Host: \[IP\]  Accept-Encoding: compress, gzip  CRLF x2 |
|  | SMB | Run nmap SMB scripts | Run the following scripts http://nmap.org/nsedoc/scripts/smb-check-vulns.html, http://nmap.org/nsedoc/scripts/smb-enum-shares.html, http://nmap.org/nsedoc/scripts/smb-enum-users.html and http://nmap.org/nsedoc/scripts/smb-brute.html.  |
|  | PPTP | Check service | Both tools will find this automatically. |
|  | RDP | Check connection, NLA and weak ciphers | Run rdp-sec-check and see if you can connect to the service via rdesktop. If so it can be brute-forced, if it returns a CredSSP error it may be vulnerable to DoS |
|  | RDP | Run nmap MS12-020 module to check for vuln | run the following: nmap -sV --script=rdp-ms12-020 -p 3389 &lt;target&gt; . For more details browse to http://nmap.org/nsedoc/scripts/rdp-vuln-ms12-020.html |
|  | NTP | Gather information | Qualys and Nmap have options to check for this.  |
|  | SNMP | Default community strings | Qualys and Nmap have options to check for this.  |
|  | SNMP | Check SNMP version | Nmap -sV should determine the version of SNMP running. This can also be done by looking at Wireshark stream when you do nmap scan. |
|  | ISAKMP | Check Aggressive mode and weak psk | The tools should pick this up.  |
|  |  |  |  |
|  | \#\#\# | Software version \(banner grab\) & check vulnerabilities | For all unrecognised ports, check what Nmap and Qualys have returned, and check the port online. Try connecting to it, and checking whether or not SSL is supported. If it is, run through the typical SSL tests. |
|  | \#\#\# | Check firewall rules | Do you notice a large number of closed ports after a full nmap scan? Does it look like a perimeter device, such as a router? If not, it should be reported on. If it's something like a home or business router that has 135/tcp-139/tcp filtered but most other things closed then this is not reported on |
|  | ICMP | Check ICMP replies | We only care about echo, timestamp and address mask. |

## Tools

| Tool | Type | Location |
| :--- | :--- | :--- |
| Bursuite | Web Page Analysis | Kali |
| Dirbuster | HTTP directory brute force | Kali |
| iker.py | VPN checker | Portcullis |
| ike-scan | VPN checker | Kali |
| Metasploit | Vulnerablity Exploitation | Kali |
| Ncat | Connect to services | Kali |
| Nessus | Vulnerability Scanner | Test laptop |
| Nikto | HTTP service scanner | Kali |
| Nmap | Port and script scans | Kali |
| Qualys | Vulnerability Scanner | Cloud-based |
| rdp-sec-check.pl | RDP checker | Portcullis |
| SSLlabs | Check HTTPS ciphers | Web |
| SSLscan | Check SSL/TLS ciphers | Kali |
| Wireshark | Packet capture | Kali |
| WPscan | WordPress interface scanner | Kali |

## Useful Sites



| Site | Purpose | URL |
| :--- | :--- | :--- |
| SSLlabs | Check HTTPS strength | [https://www.ssllabs.com/ssltest/](https://www.ssllabs.com/ssltest/) |
| ARIN.net | Check IP ownership \(America\) | [https://www.arin.net/](https://www.arin.net/) |
| RIPE.net | Check IP ownership \(Europe\) | [https://www.ripe.net/](https://www.ripe.net/) |
| rdp-sec-check download | Check RDP services | [https://labs.portcullis.co.uk/tools/rdp-sec-check/](https://labs.portcullis.co.uk/tools/rdp-sec-check/) |
| iker download | Check ISAKMP services | [https://labs.portcullis.co.uk/tools/iker/](https://labs.portcullis.co.uk/tools/iker/) |
| ASafaWeb | IIS Server Scanner | [https://asafaweb.com/](https://asafaweb.com/) |
| Microsoft Security Bulletin | Microsoft Vulnerability Searcher | [https://technet.microsoft.com/en-us/security/bulletin/](https://technet.microsoft.com/en-us/security/bulletin/) |
| Wikipedia | List of TCP and UDP ports | [https://en.wikipedia.org/wiki/List\_of\_TCP\_and\_UDP\_port\_numbers](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers) |

