Newer DBMSs support xml By 2 functions:

    -updatexml(xml_frag,SQL-QUERY)
    
    -extractvalue(xml_frag,SQL-QUERY,xml_frag)

Note: Of course, the hacker should test other methods(UNION SELECT,Double Query,...) for SQLi and if it doesn't work, go to XMLi.
