# MySqlForMyself
My MySQL journey!


 ### Basic
 
 #### Creating a database
    - CREATE DATABASE <name>
 
 #### Start using that database
    - USE <nameOfTheDatabase>
 
 #### Show Warnings
    - SHOW WARNINGS;
 
 ## Tables
 
 #### Creating a Table
    - CREATE TABLE <TableName> ( 
        col1 datatype,
        col2 datatype,
        .
        .
        coln datatype
        );
 
 #### Drop table
    - DROP TABLE <tablename>
    
 #### Inserting into table
    - INSERT INTO table_name(column_name) VALUES (data);

#### Multiple insert into table
    - INSERT INTO table_name 
            (column_name, column_name) 
      VALUES      (value, value), 
            (value, value), 
            (value, value);

 #### View data in table
    - SELECT * FROM <tableName>
    
## Constraints    
    
 #### Null and not null
    - INSERT INTO table_name (
        column_name datatype NOT NULL
        );
     
     SIDENOTE: Violating those will result in warning and auto apply default value.

#### Default
    - INSERT INTO table_name (
        column_name datatype DEFAULT <value based on type>
        );
    // If value is not specified it will take default value. But you can explicitly pass NULL as a value.
    
    
    - INSERT INTO table_name (
        column_name datatype NOT NULL DEFAULT <value based on type>
        );
    // Explicitly passing NULL will throw an error.
    
#### Primary key
    - INSERT INTO table_name (
        id INT NOT NULL AUTO_INCREMENT,
        col_name data_type NOT NULL,
        PRIMARY KEY (id)
        );
        
#### READ 
    - SELECT * FROM table_name;
    
    SIDENOTE: The order in which columns is based on how to defined the table if you use '*' for select.
                But if you use comma seperated col_name then it follows that order.
    
#### READ only specific things OR WHERE clause
    - SELECT * FROM table_name 
        WHERE condition;
    
    SIDENOTE: Its case-insensitive search.
    

#### UPDATE
    - UPDATE table_name SET colname = value WHERE colname = value;

#### Delete
    - DELETE FROM table_name WHERE col_name = value;
    
    SIDENOTE: 
        DROP TABLE table_name;   ---> Dropping the table, table doesn't exist anymore.
        DELETE TABLE table_name; ---> Deleting all the entries in the table, table still exists.

#### Extras 

    ###### AS
        SELECT cat_id AS id FROM table_name;
        
