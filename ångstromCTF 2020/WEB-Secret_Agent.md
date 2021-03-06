## WEB Secret Agent

Luckily the source code was given in the challenge. By going through the code we can see that the value of `USER-AGENT` Request Header is used in the below SQL query with any Input Verification. By following simple SQL Injection cheats you can verify the Injection.

Moreover we need to keep in mind that the result of sql query contains only one row or else it will print the error messages and will exit.

![code file](https://i.imgur.com/fupTLMs.png?1)

Follow the `UNION Attack` in SQL query you can determine the number of rows in the table `Agents`.

![No of Rows](https://i.imgur.com/HEga6WE.png?1)

Find the version of the SQL Database used by the SQL query `SELECT @@version` 

![version](https://i.imgur.com/9AFuw65.png?1)

From the above picture you can see that MariaDB database is used. Now determine the column names of the table `Agents` by querying in the the table `information_scheme.COLUMNS`. In the above restrict the result to only one row we need to use `LIMIT 1 OFFSET x` x here is the value for number of row the query show exclude.

We know that table Agent has only two columns. So,
x=0 

![col1](https://i.imgur.com/WaejKRF.png?1)

and x=1

![col2](https://i.imgur.com/oc6a9lt.png?1)

So the column names for the table Agent are `UA` and `NAME`

Now print the values of each row in table Agent. Here I used CONCAT method of MariaDB to concate the values of column UA and NAME to print in one row. `And use LIMIT 1 OFFSET x` in the query to return one row at a time.

![flag](https://i.imgur.com/BtJBPor.png?1)

flag is in row 3.
