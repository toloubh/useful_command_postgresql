# Top psql commands and flags you need to know | PostgreSQL
psql is an interface you can access through the terminal to interact with Postgres databases. You can use it to connect to a database, add & read & modify data, check the available databases & fields, run commands from a file, and so on.

## 1. Connect to a database - psql -d

Same host database
If the database is on the same host as your machine, you can use the following command:
```
psql -d <db-name> -U <username> -W

```
// example
```
psql -d tutorials_db -U admin -W
    • -d - specifies the name of the database to connect to 
    • -U - specifies the name of the user to connect as 
    • -W - forces psql to ask for the user password before connecting to the database

```
Different host database
```
psql -h <db-address> -d <db-name> -U <username> -W
```
//example
```
psql -h my-psql-db.cloud.neon.tech -d tutorials_db -U admin -W
```
SSL mode
There might be cases where you want to use SSL for the connection.

```
psql "sslmode=require host=<db-address> dbname=<db-name> user=<username>"
```
//example
```
psql "sslmode=require host=my-psql-db.cloud.neon.tech dbname=tutorials_db user=admin"
```

## 2. List all databases - \l

In many cases, you will work with more than one database. You can list all the available databases with the following command:
```
\l
```

## 3. Switch to another database - \c
```
\c <db-name>
```
// example
```
\c tutorials_db
```
## 4. List database tables - \dt

The \dt psql command returns the tables alongside:
```
    • the schema they belong to 
    • their type 
    • their owner
```
Showing tables using pg_catalog schema
```
SELECT *
FROM pg_catalog.pg_tables
WHERE schemaname != 'pg_catalog' AND 
    schemaname != 'information_schema';
```

## 5. Describe a table - \d

```
\d <table-name>
```
// example
```
\d tutorials
```
The \d command returns all the columns, their types, collection, whether they are nullable or not, and their configured default value.

If you want more information about a table, you can use the command:
```
\d+ <table-name>
```
Now, you get extra information such as storage, compression, stats target, and a description.

## 6. List all schemas - \dn
The \dn psql command lists all the database schemas.

## 7. List users and their roles - \du

Sometimes, you might need to change the user. Postgres has a command that lists all the users and their roles.
```
\du
```
## 8. Retrieve a specific user - \du

```
\du <username>
```	
//example
```
/du postgres
```
Now, you can see the roles of the specified user, and whether the user is a member of a group or not.

## 9. List all functions - \df

The command returns all functions and the:
```
    • schema they belong to 
    • names 
    • result data type 
    • argument data types 
    • type 
```

## 10. List all views - \dv

The psql interface enables you to list all the database views with the \dv command.

## 11. Save query results to a file - \o

There might be cases where you want to analyze the result of a query at a later time. Or two compare two query results. The psql interface allows you to do that.
You can save query results in a file as follows:
```
\o <file-name>
```
// example
```
\o query_results
```
...run the psql commands...
```
\o - stop the process and output the results to the terminal again
```
Let's save the following query results in a file:
```
    • the available database tables 
    • the result of describing a database table 
    • the list of all users 
    • the details of the user "postgres" 
```
Note: To stop saving results to the file, you need to run the \o command again without the file name.

## 12. Run commands from a file - \i 

It's also possible to run commands from a file. For simple commands, it might not be the best solution. But when you want to run multiple commands and complex SQL statements, it helps a lot.
Create a txt file with the following content:
```
\l
\dt
\du
```
When you run the file, it should return a list of all:
```
    • databases 
    • database tables 
    • users 
```
You can run commands from a file with the following psql command:
```
\i <file-name>
```
// example
```
\i psql_commands.txt
```

## 13. Quit psql - \q
