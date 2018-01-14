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

#### DELETE
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
    
    
## Refining Selection    

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
    
 
 ## Aggregate functions
 
 #### COUNT
    SELECT COUNT(*) FROM table;
    
    In conjunction with other functions
        SELECT COUNT(DISTINCT(author_lname, author_fname)) FROM books;
    
 #### GROUP BY
    
    SELECT * FROM table GROUP BY colname; // Doesn't give any useful info, each row is a super row with only preview displayed.
    
    SELECT colname, COUNT(*) FROM table GROUP BY colname;
    
    
 #### MIN and MAX
    
    SELECT MAX(colname) FROM table;
    SELECT MIN(colname) FROM table;
    
   *SIDENOTE: Potential problem*
   
            SELECT MAX(pages), title FROM books; // ERRR doesn't give right title which has maximum number of pages.
            
            SOLUTION:
                
                // Subquery approch (time consuming)
                SELECT * FROM books WHERE pages = (SELECT MAX(pages) FROM books);
                
                //Normal query
                SELECT * FROM books ORDER BY pages DESC limit 1;
                
#### MIN and MAX with GROUPBY
    
    SELECT author_fname, author_lname, MAX(released_year) FROM books GROUP BY author_lname, author_fname;
    
#### SUM
    
    SELECT author_fname, author_lname, SUM(pages) FROM books GROUP BY author_lname, author_fname;
    
#### AVG
    
    SELECT author_fname, author_lname, AVG(pages) FROM books GROUP BY author_lname, author_fname;
    

## Data types in depth!

#### CHAR and VARCHAR
    
    CHAR - Takes up fixed length (fixed number of bytes), if given input is less than the specified length it pads the input with spaces, if input length is more than it truncate to the specified length.
    You can specify length anywhere between 0-255.
    
    SIDENOTE: When retrieved to display data padding is removed.
    
    VARCHAR - No of bytes occupied depends on user input but it does truncate when input length exceeds the specified length.
    
    CHAR are faster than VARCHAR.
    
#### DECIMAL

    Syntax
        DECIMAL(5,2) : 5 digit allowed in which 2 are after decimal.
        ex: 234.89
        
        If huge value is specified it converts it into maximum allowed value.
        Ex: 
        DECIMAL(6,2)
        Input value     Stored value
        67367388        9999.99
        1               1.00
        123.9999        124.00
        
#### DOUBLE and FLOAT
    
    FLOAT   : precision is ~7  -> greater than this, number gets fucked.
    DOUBLE  : precision is ~15 -> greater than this, number gets fucked. 

#### DATE, TIME and DATETIME
    
    DATE gives you date in YYYY MM DD format.
    TIME gives yoy time in HH MM SS format.
    DATETIME is the mix of both.
    
    CURDATE()   : gives DATE
    CURTIME()   : gives TIME
    NOW()       : gives DATETIME
    
#### Date formatting
    
    Can be used on DATE and DATETIME:
    DAY() gives the day. (too fancy :P)
    DAYNAME() gives the name of the day ( monday, tuesday,...)
    DAYOFWEEK() gives the number (sunday:1, monday:2 ... )
    DAYOFYEAR() gives the day count of the year.
    
    DATE_FORMAT(date, specifiers);
    
    specifiers - https://dev.mysql.com/doc/refman/5.5/en/date-and-time-functions.html#function_date-format
    
    
#### DATE MATH
    
    DATEDIFF    : To find difference between two dates. 
    syntax: 
            SELECT DATEDIFF( NOW(), birthday ) FROM people;
      
    DATE_ADD    : Add date (how can I explain ? :P)
    syntax: 
            SELECT DATE_ADD( birthday, INTERVAL 1 UNITS ) FROM people;
            
            units: https://dev.mysql.com/doc/refman/5.5/en/date-and-time-functions.html#function_date-add
            
    Shorthand for above (+/-): 
            
            SELECT birthdate + INTERVAL UNITS FROM people;
            
            Ex:
            SELECT birthdate + INTERVAL 1 YEAR + INTERVAL 10 HOUR FROM people;
  
  
##### TIMESTAMP
    
    TIMESTAMP: stores both date and time information.
    
    Diff between DATETIME and TIMESTAMP:
    
    DATETIME -  Ranges 1000-01-01 to 9999-12-31
                Storage space 8 bytes
    
    TIMESTAMP - 1970-01-01 to 2038-01-19        
                4 bytes
                
    ex:
        CREATE TABLE comment (
            content VARCHAR(100),
            created_at TIMESTAMP DEFAULT NOW() ON UPDATE CURRENT_TIMESTAMP
        );
        
 
 ## Logical operators
 
 ##### Not equal
        
        =!
        
        SELECT * FROM books WHERE author_lname != "Harris";
        
 ##### NOT LIKE
        
        SELECT title FROM books WHERE title NOT LIKE 'W%';
 
 ##### Greater than
        >
        SELECT * FROM books WHERE released_by > 2000;
        
##### Greater than equal to
        >=
        SELECT * FROM books WHERE released_by >= 2000;

   SIDENOTE: 
   
    SELECT 99 > 1; // output : 1

    SELECT 99 > 567; // output : 0

    100 > 5
    -- true

    -15 > 15
    -- false

    9 > -10
    -- true

    1 > 1
    -- false

    'a' > 'b'
    -- false

    'A' > 'a'
    -- false

    'A' >=  'a'
    -- true


