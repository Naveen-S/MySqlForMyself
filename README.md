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
