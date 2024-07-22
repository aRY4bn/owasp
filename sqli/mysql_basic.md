MySql Basics : 


-Access MySQL:

    sudo mysql -u root -p

-Manage MySQL Users and Privileges

    --Create a New MySql user:
    CREATE USER 'test'@'localhost' IDENTIFIED BY 'password';
    
    --Grant Privileges to  the new user:
    GRANT ALL PRIVILEGES ON EXAMPLE_DB.* TO 'test'@'localhost';
    
    --Apply the Privileges: 
    FLUSH PRIVILEGES;


-Lists Databases: 

    SHOW DATABASES;
    

-Drop the Database:

    DROP DATABASE <db_name>;


-Use a Database:
 
    USE <db_name>;


-Create a Table: 

    CREATE TABLE users ( 
        id INT AUTO_INCREMENT PRIMARY KEY,
        name VARCHAR(100),
        email VARCHAR(100)
    );


-Insert Data Into a Table:

     INSERT INTO users (name , email) VALUES ("test","test@gmail.com");

-Select Data from a Table: 

     SELECT * FROM users;

-Update the Value:

    UPDATE table_name
    SET column1 = value1 , column2 = value2 , ...
    WHERE condition;
