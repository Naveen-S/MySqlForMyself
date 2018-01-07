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


## String functions
  
  #### CONCAT 
    - Use to concat n number of column's data and any separator.
    
    SELECT CONCAT( col1, seperator ,col2, col3, ...., coln) FROM table_name; 

  #### CONCAT_WS
    - Concat with a common separator
    
    SELECT CONCAT_WS(" - ", title, lastname, firstname) FROM books;
    
  #### SUBSTRING or SUBSTR
        SELECT SUBSTRING( string, startIndex, endIndex );
        
        SIDENOTE: index starts with 1 in sql.
  
 #### REPLACE
 
        SELECT REPLACE( string, partOfTheString, toBeReplacedWith );
        
 #### REVERSE
    
        SELECT REVERSE(string);
        
        ex: SELECT REVERSE(title) FROM books;
 
#### CHAR_LENGTH
    SELECT author, CHARLENGTH(author) FROM books;

#### UPPER and LOWER
    
    SELECT UPPER(title) FROM books;
    SELECT LOWER(title) FROM books;
    
#### DISTINCT
    
    SELECT DISTINCT colname FROM table;
    
    SIDENOTE: If you want distinct of combination of two or more things
    
    SELECT DISTINCT col1, col2 FROM table;
    
#### ORDER BY
    
    SELECT colname FROM table ORDER BY colname;
    
    Variations:
        SELECT author_fname, author_lname, title  FROM books ORDER BY 2;  // same as saying order by author_lname
        
        SELECT * FROM books ORDER BY author_lname, author_fname;  // Orders by author_lname if there is conflict its resolved by ordering those by author_fname.
        
#### LIMIT 
    
    SELECT * FROM table LIMIT 5;
    
    SELECT * FROM table LIMIT start_row, noOfRows;  // Row starts from 0.
    
    SIDENOTE: string counting starts from 1. (Its confusing I know ) 
    
    
 #### LIKE
 
    SELECT * FROM table WHERE title LIKE "%the%"; 
    % - wildcard 0 or n occurance of any character.
    
    %the% --> title which has "the" in it anywhere.
    %the  --> title ending with "the".
    the%  --> title starting with "the"._    
    SELECT * FROM table WHERE stock LIKE "____"; // Where stock is 4 digits more than or equal to 1000.
    _  - wildcard to match exactly one character
    
    SIDENOTE: Ok how do I match % and  _ if they are special character?
    Fuss not missy, \ (backslash) to your rescue.
    
    SELECT * FROM books WHERE title LIKE "%\%%"; // Search for book with title of one % in it.
    SELECT * FROM books WHERE title LIKE "%\_%"; // Search for book with title of one _ in it.
    
    
    
    
    
#### Extras 

    ###### AS
        SELECT cat_id AS id FROM table_name;
        
