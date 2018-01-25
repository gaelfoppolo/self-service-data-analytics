## Hive basic command line

The following operation are basic command line  such as create database, drop database, ...

### Create Database

Create Database is a statement used to create a database in Hive. A database in Hive is a namespace or a collection of tables.

`CREATE DATABASE|SCHEMA [IF NOT EXISTS] <database name>   `

Here, IF NOT EXISTS is an optional clause, which notifies the user that a database with the same name already exists. We can use SCHEMA in place of DATABASE in this command.

**<u>Example:</u>**

```powershell
hive> CREATE SCHEMA myDB;
hive> SHOW DATABASES;
default
myDB
```

### Drop DataBase :

Drop Database is a statement that drops all the tables and deletes the database.

`DROP DATABASE StatementDROP (DATABASE|SCHEMA) [IF EXISTS] database_name [RESTRICT|CASCADE];`

**<u>Example:</u>**

```powershell
hive> DROP DATABASE IF EXISTS myDB;
```

### Create Table:

Create Table is a statement used to create a table in Hive. 

```powershell
CREATE [TEMPORARY] [EXTERNAL] TABLE [IF NOT EXISTS] [db_name.] table_name

[(col_name data_type [COMMENT col_comment], ...)]
[COMMENT table_comment]
[ROW FORMAT row_format]
[STORED AS file_format]
```

**<u>Example:</u>**

Let's assume that you went to create a table employee from a a following table list:

| Sr.No | Field Name  | Data Type |
| ----- | ----------- | --------- |
| 1     | Eid         | int       |
| 2     | Name        | String    |
| 3     | Salary      | Float     |
| 4     | Designation | string    |

The following data is a Comment, Row formatted fields such as Field terminator, Lines terminator, and Stored File type and the following query creates a table named **employee** using the above data.

```
hive> CREATE TABLE IF NOT EXISTS employee ( eid int, name String,
salary String, destination String)
COMMENT ‘Employee details’
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ‘\t’
LINES TERMINATED BY ‘\n’
STORED AS TEXTFILE;
OK
Time taken: 5.905 seconds
```

### Drop Table :

This chapter describes how to drop a table in Hive. When you drop a table from Hive Metastore, it removes the table/column data and their metadata.

```
DROP TABLE [IF EXISTS] table_name;
```

**<u>Example:</u>**

```
hive> DROP TABLE IF EXISTS employee;
```

### Load from file :

Generally, after creating a table in SQL, we can insert data using the Insert statement. But in Hive, we can insert data using the LOAD DATA statement.

```powershell
LOAD DATA [LOCAL] INPATH 'filepath' [OVERWRITE] INTO TABLE tablename 
[PARTITION (partcol1=val1, partcol2=val2 ...)]
```

**<u>Example:</u>**

```
hive> LOAD DATA LOCAL INPATH '/home/user/sample.txt'
OVERWRITE INTO TABLE employee;
```

the example file is a txt file containing the following value:

1201  Gopal       45000    Technical manager
1202  Manisha     45000    Proof reader
1203  Masthanvali 40000    Technical writer
1204  Kiran       40000    Hr Admin
1205  Kranthi     30000    Op Admin

### Alter Table :

The following query alter the structure of a table. it's  possible to change the name of the table, add column, drop column, replace column and change the type of a column. the syntax is as follow :

```powershell
ALTER TABLE name RENAME TO new_name
ALTER TABLE name ADD COLUMNS (col_spec[, col_spec ...])
ALTER TABLE name DROP [COLUMN] column_name
ALTER TABLE name CHANGE column_name new_name new_type
ALTER TABLE name REPLACE COLUMNS (col_spec[, col_spec ...])
```

**<u>Example:</u>**

Bellow are shown different example of the alteration.

The query is based on the table created previously.

```powershell
#Rename table name employee to emp
hive> ALTER TABLE employee RENAME TO emp;
```

```powershell
#change the column name "name" to "ename"
#change the column salary type from float to double
hive> ALTER TABLE employee CHANGE name ename String;
hive> ALTER TABLE employee CHANGE salary salary Double;
```

```powershell
#add the column "dept" with string type
hive> ALTER TABLE employee ADD COLUMNS ( 
dept STRING COMMENT 'Department name');
```

```powershell
#replace the column eid with a colum empid and the column ename with a column name
hive> ALTER TABLE employee REPLACE COLUMNS ( 
eid INT empid Int, 
ename STRING name String);
```

### Partitioning :

Hive organizes tables into partitions. It is a way of dividing a table into related parts based on the values of partitioned columns such as date, name, ... . Tables or partitions are sub-divided into **buckets,** to provide extra structure to the data that may be used for more efficient querying.

```
ALTER TABLE table_name ADD [IF NOT EXISTS] PARTITION partition_spec
[LOCATION 'location1'] partition_spec [LOCATION 'location2'] ...;

partition_spec:
: (p_column = p_col_value, p_column = p_col_value, ...)
```

**<u>Example:</u>**

We will take for example a table containing the following data

| id   | name     | dept | years |
| ---- | -------- | ---- | ----- |
| 1    | gopal    | TP   | 2012  |
| 2    | kiran    | HR   | 2012  |
| 3    | kaleel   | SC   | 2012  |
| 4    | Prasanth | SC   | 2013  |

By using the following query, we will partition the table by year:

```powershell
hive> ALTER TABLE employee
> ADD PARTITION (year=’2013’)
> location '/2012/part2012';
```

We will obtain then this to partition

| id   | name   | dept | years |
| ---- | ------ | ---- | ----- |
| 1    | gopal  | TP   | 2012  |
| 2    | kiran  | HR   | 2012  |
| 3    | kaleel | SC   | 2012  |

| id   | name     | dept | years |
| ---- | -------- | ---- | ----- |
| 4    | Prasanth | SC   | 2013  |



## 