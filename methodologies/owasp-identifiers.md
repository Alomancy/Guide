# OWASP v4 Checklist

## Testing Checklist <a id="testing-checklist"></a>

The following is the list of controls to test during the assessment:

| Ref. No. | Category | Test Name |
| :--- | :--- | :--- |
| 4.2 |  | **Information Gathering** |
| 4.2.1 | OTG-INFO-001 | Conduct Search Engine Discovery and Reconnaissance for Information Leakage |
| 4.2.2 | OTG-INFO-002 | Fingerprint Web Server |
| 4.2.3 | OTG-INFO-003 | Review Webserver Metafiles for Information Leakage |
| 4.2.4 | OTG-INFO-004 | Enumerate Applications on Webserver |
| 4.2.5 | OTG-INFO-005 | Review Webpage Comments and Metadata for Information Leakage |
| 4.2.6 | OTG-INFO-006 | Identify application entry points |
| 4.2.7 | OTG-INFO-007 | Map execution paths through application |
| 4.2.8 | OTG-INFO-008 | Fingerprint Web Application Framework |
| 4.2.9 | OTG-INFO-009 | Fingerprint Web Application |
| 4.2.10 | OTG-INFO-010 | Map Application Architecture |
|  |  |  |
| 4.3 |  | **Configuration and Deploy** Management Testing |
| 4.3.1 | OTG-CONFIG-001 | Test Network/Infrastructure Configuration |
| 4.3.2 | OTG-CONFIG-002 | Test Application Platform Configuration |
| 4.3.3 | OTG-CONFIG-003 | Test File Extensions Handling for Sensitive Information |
| 4.3.4 | OTG-CONFIG-004 | Backup and Unreferenced Files for Sensitive Information |
| 4.3.5 | OTG-CONFIG-005 | Enumerate Infrastructure and Application Admin Interfaces |
| 4.3.6 | OTG-CONFIG-006 | Test HTTP Methods |
| 4.3.7 | OTG-CONFIG-007 | Test HTTP Strict Transport Security |
| 4.3.8 | OTG-CONFIG-008 | Test RIA cross domain policy |
|  |  |  |
| 4.4 |  | **Identity Management** Testing |
| 4.4.1 | OTG-IDENT-001 | Test Role Definitions |
| 4.4.2 | OTG-IDENT-002 | Test User Registration Process |
| 4.4.3 | OTG-IDENT-003 | Test Account Provisioning Process |
| 4.4.4 | OTG-IDENT-004 | Testing for Account Enumeration and Guessable User Account |
| 4.4.5 | OTG-IDENT-005 | Testing for Weak or unenforced username policy |
| 4.4.6 | OTG-IDENT-006 | Test Permissions of Guest/Training Accounts |
| 4.4.7 | OTG-IDENT-007 | Test Account Suspension/Resumption Process |
|  |  |  |
| 4.5 |  | **Authentication Testing** |
| 4.5.1 | OTG-AUTHN-001 | Testing for Credentials Transported over an Encrypted Channel |
| 4.5.2 | OTG-AUTHN-002 | Testing for default credentials |
| 4.5.3 | OTG-AUTHN-003 | Testing for Weak lock out mechanism |
| 4.5.4 | OTG-AUTHN-004 | Testing for bypassing authentication schema |
| 4.5.5 | OTG-AUTHN-005 | Test remember password functionality |
| 4.5.6 | OTG-AUTHN-006 | Testing for Browser cache weakness |
| 4.5.7 | OTG-AUTHN-007 | Testing for Weak password policy |
| 4.5.8 | OTG-AUTHN-008 | Testing for Weak security question/answer |
| 4.5.9 | OTG-AUTHN-009 | Testing for weak password change or reset functionalities |
| 4.5.10 | OTG-AUTHN-010 | Testing for Weaker authentication in alternative channel |
|  |  |  |
| 4.6 |  | **Authorization Testing** |
| 4.6.1 | OTG-AUTHZ-001 | Testing Directory traversal/file include |
| 4.6.2 | OTG-AUTHZ-002 | Testing for bypassing authorization schema |
| 4.6.3 | OTG-AUTHZ-003 | Testing for Privilege Escalation |
| 4.6.4 | OTG-AUTHZ-004 | Testing for Insecure Direct Object References |
|  |  |  |
| 4.7 |  | **Session Management Testing** |
| 4.7.1 | OTG-SESS-001 | Testing for Bypassing Session Management Schema |
| 4.7.2 | OTG-SESS-002 | Testing for Cookies attributes |
| 4.7.3 | OTG-SESS-003 | Testing for Session Fixation |
| 4.7.4 | OTG-SESS-004 | Testing for Exposed Session Variables |
| 4.7.5 | OTG-SESS-005 | Testing for Cross Site Request Forgery |
| 4.7.6 | OTG-SESS-006 | Testing for logout functionality |
| 4.7.7 | OTG-SESS-007 | Test Session Timeout |
| 4.7.8 | OTG-SESS-008 | Testing for Session puzzling |
|  |  |  |
| 4.8 |  | **Data Validation Testing** |
| 4.8.1 | OTG-INPVAL-001 | Testing for Reflected Cross Site Scripting |
| 4.8.2 | OTG-INPVAL-002 | Testing for Stored Cross Site Scripting |
| 4.8.3 | OTG-INPVAL-003 | Testing for HTTP Verb Tampering |
| 4.8.4 | OTG-INPVAL-004 | Testing for HTTP Parameter pollution |
| 4.8.5 | OTG-INPVAL-005 | Testing for SQL Injection |
| 4.8.5.1 |  | Oracle Testing |
| 4.8.5.2 |  | MySQL Testing |
| 4.8.5.3 |  | SQL Server Testing |
| 4.8.5.4 |  | Testing PostgreSQL |
| 4.8.5.5 |  | MS Access Testing |
| 4.8.5.6 |  | Testing for NoSQL injection |
| 4.8.6 | OTG-INPVAL-006 | Testing for LDAP Injection |
| 4.8.7 | OTG-INPVAL-007 | Testing for ORM Injection |
| 4.8.8 | OTG-INPVAL-008 | Testing for XML Injection |
| 4.8.9 | OTG-INPVAL-009 | Testing for SSI Injection |
| 4.8.10 | OTG-INPVAL-010 | Testing for XPath Injection |
| 4.8.11 | OTG-INPVAL-011 | IMAP/SMTP Injection |
| 4.8.12 | OTG-INPVAL-012 | Testing for Code Injection |
| 4.8.12.1 |  | Testing for Local File Inclusion |
| 4.8.12.2 |  | Testing for Remote File Inclusion |
| 4.8.13 | OTG-INPVAL-013 | Testing for Command Injection |
| 4.8.14 | OTG-INPVAL-014 | Testing for Buffer overflow |
| 4.8.14.1 |  | Testing for Heap overflow |
| 4.8.14.2 |  | Testing for Stack overflow |
| 4.8.14.3 |  | Testing for Format string |
| 4.8.15 | OTG-INPVAL-015 | Testing for incubated vulnerabilities |
| 4.8.16 | OTG-INPVAL-016 | Testing for HTTP Splitting/Smuggling |
|  |  |  |
| 4.9 |  | **Error Handling** |
| 4.9.1 | OTG-ERR-001 | Analysis of Error Codes |
| 4.9.2 | OTG-ERR-002 | Analysis of Stack Traces |
|  |  |  |
| 4.10 |  | **Cryptography** |
| 4.10.1 | OTG-CRYPST-001 | Testing for Weak SSL/TSL Ciphers, Insufficient Transport Layer Protection |
| 4.10.2 | OTG-CRYPST-002 | Testing for Padding Oracle |
| 4.10.3 | OTG-CRYPST-003 | Testing for Sensitive information sent via unencrypted channels |
|  |  |  |
| 4.11 |  | **Business Logic Testing** |
| 4.11.1 | OTG-BUSLOGIC-001 | Test Business Logic Data Validation |
| 4.11.2 | OTG-BUSLOGIC-002 | Test Ability to Forge Requests |
| 4.11.3 | OTG-BUSLOGIC-003 | Test Integrity Checks |
| 4.11.4 | OTG-BUSLOGIC-004 | Test for Process Timing |
| 4.11.5 | OTG-BUSLOGIC-005 | Test Number of Times a Function Can be Used Limits |
| 4.11.6 | OTG-BUSLOGIC-006 | Testing for the Circumvention of Work Flows |
| 4.11.7 | OTG-BUSLOGIC-007 | Test Defenses Against Application Mis-use |
| 4.11.8 | OTG-BUSLOGIC-008 | Test Upload of Unexpected File Types |
| 4.11.9 | OTG-BUSLOGIC-009 | Test Upload of Malicious Files |
|  |  |  |
| 4.12 |  | **Client Side Testing** |
| 4.12.1 | OTG-CLIENT-001 | Testing for DOM based Cross Site Scripting |
| 4.12.2 | OTG-CLIENT-002 | Testing for JavaScript Execution |
| 4.12.3 | OTG-CLIENT-003 | Testing for HTML Injection |
| 4.12.4 | OTG-CLIENT-004 | Testing for Client Side URL Redirect |
| 4.12.5 | OTG-CLIENT-005 | Testing for CSS Injection |
| 4.12.6 | OTG-CLIENT-006 | Testing for Client Side Resource Manipulation |
| 4.12.7 | OTG-CLIENT-007 | Test Cross Origin Resource Sharing |
| 4.12.8 | OTG-CLIENT-008 | Testing for Cross Site Flashing |
| 4.12.9 | OTG-CLIENT-009 | Testing for Clickjacking |
| 4.12.10 | OTG-CLIENT-010 | Testing WebSockets |
| 4.12.11 | OTG-CLIENT-011 | Test Web Messaging |
| 4.12.12 | OTG-CLIENT-012 | Test Local Storage |

