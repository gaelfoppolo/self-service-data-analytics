## Pig Latin query (relational operators)

In this part we will describe in Pig Latin the query that can be used in Pig script such as load, store, filter, ... .

### Load Operator

It's possible to load data into Apache Pig from the file system (HDFS/ Local) using LOAD operator of Pig Latin. 

```powershell
Relation_name = LOAD 'Input file path' USING function as schema;
```

Where,

- **relation_name** : We have to mention the relation in which we want to store the data
- **Input file path** : We have to mention the HDFS directory where the file is stored. 
- **function** : We have to choose a function from the set of load functions provided by Apache Pig (**BinStorage, JsonLoader, PigStorage, TextLoader**)
- **Schema** : We have to define the schema of the data. We can define the required schema as follows

```powershell
(column1 : data type, column2 : data type, column3 : data type);
```

**<u>Example :</u>**

We will try to load the following table that is stored in HDFS.

| Student ID | First Name | Last Name   | Phone      | City         |
| ---------- | ---------- | ----------- | ---------- | ------------ |
| 001        | Rajiv      | Reddy       | 9848022337 | Hyderabad    |
| 002        | siddarth   | Battacharya | 9848022338 | Kolkata      |
| 003        | Rajesh     | Khanna      | 9848022339 | Delhi        |
| 004        | Preethi    | Agarwal     | 9848022330 | Pune         |
| 005        | Trupthi    | Mohanthy    | 9848022336 | Bhuwaneshwar |
| 006        | Archana    | Mishra      | 9848022335 | Chennai      |

The file is located in pig_data/student_data.txt . The query to load this file is :

```powershell
grunt> student = LOAD 'hdfs://localhost:9000/pig_data/student_data.txt' 
   USING PigStorage(',')
   as ( id:int, firstname:chararray, lastname:chararray, phone:chararray, 
   city:chararray );
```

The loaded data are stored in the relation **student**. The loaded data used this schema :

| column   | id   | firstname  | lastname   | phone      | city       |
| -------- | ---- | ---------- | ---------- | ---------- | ---------- |
| datatype | int  | char array | char array | char array | char array |

### Store Operator

The loaded data can be stored in the file system using the STORE operator.

```powershell
STORE Relation_name INTO ' required_directory_path ' [USING function];
```

Where,

- **relation_name** : We have to mention the relation in which the data is contained
- **required_directory_path** : We have to mention the HDFS directory where the file will be stored. 
- **function** : We have to choose a function from the set of load functions provided by Apache Pig (**BinStorage, JsonLoader, PigStorage, TextLoader**)

**<u>Example :</u>**

We will now try to store the previously loaded data in the student relation.

The query to store in the directory pig_Output is :

```powershell
grunt> STORE student INTO ' hdfs://localhost:9000/pig_Output/ ' USING PigStorage (',');
```

if the query is correctly executed, the displayed result should be :

```powershell
2015-10-05 13:05:05,429 [main] INFO  org.apache.pig.backend.hadoop.executionengine.mapReduceLayer.
MapReduceLau ncher - 100% complete
2015-10-05 13:05:05,429 [main] INFO  org.apache.pig.tools.pigstats.mapreduce.SimplePigStats - 
Script Statistics:
   
HadoopVersion    PigVersion    UserId    StartedAt             FinishedAt             Features 
2.6.0            0.15.0        Hadoop    2015-10-0 13:03:03    2015-10-05 13:05:05    UNKNOWN  
Success!  
Job Stats (time in seconds): 
JobId          Maps    Reduces    MaxMapTime    MinMapTime    AvgMapTime    MedianMapTime    
job_14459_06    1        0           n/a           n/a           n/a           n/a
MaxReduceTime    MinReduceTime    AvgReduceTime    MedianReducetime    Alias    Feature   
     0                 0                0                0             student  MAP_ONLY 
OutPut folder
hdfs://localhost:9000/pig_Output/ 
 
Input(s): Successfully read 0 records from: "hdfs://localhost:9000/pig_data/student_data.txt"  
Output(s): Successfully stored 0 records in: "hdfs://localhost:9000/pig_Output"  
Counters:
Total records written : 0
Total bytes written : 0
Spillable Memory Manager spill count : 0 
Total bags proactively spilled: 0
Total records proactively spilled: 0
  
Job DAG: job_1443519499159_0006
  
2015-10-05 13:06:06,192 [main] INFO  org.apache.pig.backend.hadoop.executionengine
.mapReduceLayer.MapReduceLau ncher - Success!
```

### Diagnostic Operators

Pig Latin provides four different types of diagnostic operators to display results during a script.

#### Dump Operator

The DUMP operator is used to run the Pig Latin statements and display the results on the screen. It display the data in a relation.

```powershell
grunt> Dump Relation_Name
```

**<u>Example :</u>**

We will try to display the result in the student relation loaded before hand.

```powershell
grunt> Dump student
```

and the output is :

```powershell
2015-10-01 15:05:27,642 [main]
INFO  org.apache.pig.backend.hadoop.executionengine.mapReduceLayer.MapReduceLauncher - 
100% complete
2015-10-01 15:05:27,652 [main]
INFO  org.apache.pig.tools.pigstats.mapreduce.SimplePigStats - Script Statistics:   
HadoopVersion  PigVersion  UserId    StartedAt             FinishedAt       Features             
2.6.0          0.15.0      Hadoop  2015-10-01 15:03:11  2015-10-01 05:27     UNKNOWN
                                                
Success!  
Job Stats (time in seconds):
  
JobId           job_14459_0004
Maps                 1  
Reduces              0  
MaxMapTime          n/a    
MinMapTime          n/a
AvgMapTime          n/a 
MedianMapTime       n/a
MaxReduceTime        0
MinReduceTime        0  
AvgReduceTime        0
MedianReducetime     0
Alias             student 
Feature           MAP_ONLY        
Outputs           hdfs://localhost:9000/tmp/temp580182027/tmp757878456,

Input(s): Successfully read 0 records from: "hdfs://localhost:9000/pig_data/
student_data.txt"
  
Output(s): Successfully stored 0 records in: "hdfs://localhost:9000/tmp/temp580182027/
tmp757878456"  

Counters: Total records written : 0 Total bytes written : 0 Spillable Memory Manager 
spill count : 0Total bags proactively spilled: 0 Total records proactively spilled: 0  

Job DAG: job_1443519499159_0004
  
2015-10-01 15:06:28,403 [main]
INFO  org.apache.pig.backend.hadoop.executionengine.mapReduceLayer.MapReduceLau ncher - Success!
2015-10-01 15:06:28,441 [main] INFO  org.apache.pig.data.SchemaTupleBackend - 
Key [pig.schematuple] was not set... will not generate code.
2015-10-01 15:06:28,485 [main]
INFO  org.apache.hadoop.mapreduce.lib.input.FileInputFormat - Total input paths 
to process : 1
2015-10-01 15:06:28,485 [main]
INFO  org.apache.pig.backend.hadoop.executionengine.util.MapRedUtil - Total input paths
to process : 1

(1,Rajiv,Reddy,9848022337,Hyderabad)
(2,siddarth,Battacharya,9848022338,Kolkata)
(3,Rajesh,Khanna,9848022339,Delhi)
(4,Preethi,Agarwal,9848022330,Pune)
(5,Trupthi,Mohanthy,9848022336,Bhuwaneshwar)
(6,Archana,Mishra,9848022335,Chennai)
```

#### Describe Operator

The DESCRIBE operator is used to view the schema of a relation.

```powershell
grunt> Describe Relation_name
```

**<u>Example :</u>**

We will try to display the result in the student relation loaded before hand.

```powershell
grunt> Describe student
```

and the output is :

```powershell
grunt> student: { id: int,firstname: chararray,lastname: chararray,phone: chararray,city: chararray }
```

#### Explain Operator

The **explain** operator is used to display the logical, physical, and execution plans of a relation.

**<u>Example :</u>**

We will try to display the result in the student relation loaded before hand.

```powershell
grunt> Explain student
```

and the output is :

```powershell
2015-10-05 11:32:43,660 [main]
2015-10-05 11:32:43,660 [main] INFO  org.apache.pig.newplan.logical.optimizer
.LogicalPlanOptimizer -
{RULES_ENABLED=[AddForEach, ColumnMapKeyPrune, ConstantCalculator,
GroupByConstParallelSetter, LimitOptimizer, LoadTypeCastInserter, MergeFilter, 
MergeForEach, PartitionFilterOptimizer, PredicatePushdownOptimizer,
PushDownForEachFlatten, PushUpFilter, SplitFilter, StreamTypeCastInserter]}  
#-----------------------------------------------
# New Logical Plan: 
#-----------------------------------------------
student: (Name: LOStore Schema:
id#31:int,firstname#32:chararray,lastname#33:chararray,phone#34:chararray,city#
35:chararray)
| 
|---student: (Name: LOForEach Schema:
id#31:int,firstname#32:chararray,lastname#33:chararray,phone#34:chararray,city#
35:chararray)
    |   |
    |   (Name: LOGenerate[false,false,false,false,false] Schema:
id#31:int,firstname#32:chararray,lastname#33:chararray,phone#34:chararray,city#
35:chararray)ColumnPrune:InputUids=[34, 35, 32, 33,
31]ColumnPrune:OutputUids=[34, 35, 32, 33, 31]
    |   |   | 
    |   |   (Name: Cast Type: int Uid: 31) 
    |   |   |     |   |   |---id:(Name: Project Type: bytearray Uid: 31 Input: 0 Column: (*))
    |   |   |     
    |   |   (Name: Cast Type: chararray Uid: 32)
    |   |   | 
    |   |   |---firstname:(Name: Project Type: bytearray Uid: 32 Input: 1
Column: (*))
    |   |   |
    |   |   (Name: Cast Type: chararray Uid: 33)
    |   |   |
    |   |   |---lastname:(Name: Project Type: bytearray Uid: 33 Input: 2
	 Column: (*))
    |   |   | 
    |   |   (Name: Cast Type: chararray Uid: 34)
    |   |   |  
    |   |   |---phone:(Name: Project Type: bytearray Uid: 34 Input: 3 Column:
(*))
    |   |   | 
    |   |   (Name: Cast Type: chararray Uid: 35)
    |   |   |  
    |   |   |---city:(Name: Project Type: bytearray Uid: 35 Input: 4 Column:
(*))
    |   | 
    |   |---(Name: LOInnerLoad[0] Schema: id#31:bytearray)
    |   |  
    |   |---(Name: LOInnerLoad[1] Schema: firstname#32:bytearray)
    |   |
    |   |---(Name: LOInnerLoad[2] Schema: lastname#33:bytearray)
    |   |
    |   |---(Name: LOInnerLoad[3] Schema: phone#34:bytearray)
    |   | 
    |   |---(Name: LOInnerLoad[4] Schema: city#35:bytearray)
    |
    |---student: (Name: LOLoad Schema: 
id#31:bytearray,firstname#32:bytearray,lastname#33:bytearray,phone#34:bytearray
,city#35:bytearray)RequiredFields:null 
#-----------------------------------------------
# Physical Plan: #-----------------------------------------------
student: Store(fakefile:org.apache.pig.builtin.PigStorage) - scope-36
| 
|---student: New For Each(false,false,false,false,false)[bag] - scope-35
    |   |
    |   Cast[int] - scope-21
    |   |
    |   |---Project[bytearray][0] - scope-20
    |   |  
    |   Cast[chararray] - scope-24
    |   |
    |   |---Project[bytearray][1] - scope-23
    |   | 
    |   Cast[chararray] - scope-27
    |   |  
    |   |---Project[bytearray][2] - scope-26 
    |   |  
    |   Cast[chararray] - scope-30 
    |   |  
    |   |---Project[bytearray][3] - scope-29
    |   |
    |   Cast[chararray] - scope-33
    |   | 
    |   |---Project[bytearray][4] - scope-32
    | 
    |---student: Load(hdfs://localhost:9000/pig_data/student_data.txt:PigStorage(',')) - scope19
2015-10-05 11:32:43,682 [main]
INFO  org.apache.pig.backend.hadoop.executionengine.mapReduceLayer.MRCompiler - 
File concatenation threshold: 100 optimistic? false
2015-10-05 11:32:43,684 [main]
INFO  org.apache.pig.backend.hadoop.executionengine.mapReduceLayer.MultiQueryOp timizer - 
MR plan size before optimization: 1 2015-10-05 11:32:43,685 [main]
INFO  org.apache.pig.backend.hadoop.executionengine.mapReduceLayer.
MultiQueryOp timizer - MR plan size after optimization: 1 
#--------------------------------------------------
# Map Reduce Plan                                   
#--------------------------------------------------
MapReduce node scope-37
Map Plan
student: Store(fakefile:org.apache.pig.builtin.PigStorage) - scope-36
|
|---student: New For Each(false,false,false,false,false)[bag] - scope-35
    |   |
    |   Cast[int] - scope-21 
    |   |
    |   |---Project[bytearray][0] - scope-20
    |   |
    |   Cast[chararray] - scope-24
    |   |
    |   |---Project[bytearray][1] - scope-23
    |   |
    |   Cast[chararray] - scope-27
    |   | 
    |   |---Project[bytearray][2] - scope-26 
    |   | 
    |   Cast[chararray] - scope-30 
    |   |  
    |   |---Project[bytearray][3] - scope-29 
    |   | 
    |   Cast[chararray] - scope-33
    |   | 
    |   |---Project[bytearray][4] - scope-32 
    |  
    |---student:
Load(hdfs://localhost:9000/pig_data/student_data.txt:PigStorage(',')) - scope
19-------- Global sort: false
 ---------------- 
```

#### Illustrate  Operator

The **illustrate** operator gives you the step-by-step execution of a sequence of statements.

```powershell
grunt> illustrate Relation_name;
```

**<u>Example :</u>**

We will try to display the result in the student relation loaded before hand.

```powershell
grunt> Illustrate student
```

and the output is :

```powershell
INFO  org.apache.pig.backend.hadoop.executionengine.mapReduceLayer.PigMapOnly$M ap - Aliases
being processed per job phase (AliasName[line,offset]): M: student[1,10] C:  R:
---------------------------------------------------------------------------------------------
|student | id:int | firstname:chararray | lastname:chararray | phone:chararray | city:chararray |
--------------------------------------------------------------------------------------------- 
|        | 002    | siddarth            | Battacharya        | 9848022338      | Kolkata        |
---------------------------------------------------------------------------------------------
```

### Group Operators

The GROUP operator is used to group the data in one or more relations. It collects the data having the same key.

```powershell
grunt> Group_data = GROUP Relation_name BY data_key;
```

#### Simple Group Operator

**<u>Example :</u>**

We will try to group the student shown in the table bellow by age.

| ID   | First name | Last Name   | age  | phone      | city         |
| ---- | ---------- | ----------- | ---- | ---------- | ------------ |
| 001  | Rajiv      | Reddy       | 21   | 9848022337 | Hyderabad    |
| 002  | siddarth   | Battacharya | 22   | 9848022338 | Kolkata      |
| 003  | Rajesh     | Khanna      | 22   | 9848022339 | Delhi        |
| 004  | Preethi    | Agarwal     | 21   | 9848022330 | Pune         |
| 005  | Trupthi    | Mohanthy    | 23   | 9848022336 | Bhuwaneshwar |
| 006  | Archana    | Mishra      | 23   | 9848022335 | Chennai      |
| 007  | Komal      | Nayak       | 24   | 9848022334 | Trivendram   |
| 008  | Bharathi   | Nambiayar   | 24   | 9848022333 | Chennai      |

First we will loaded the data in a relation named student_details with the right schema.

```powershell
grunt> student_details = LOAD 'hdfs://localhost:9000/pig_data/student_details.txt' USING PigStorage(',')
   as (id:int, firstname:chararray, lastname:chararray, age:int, phone:chararray, city:chararray);
```

Now we will group the relation by age :

```powershell
grunt> group_data = GROUP student_details by age;
```

To verify the result dump the relation group_data :

```powershell
(21,{(4,Preethi,Agarwal,21,9848022330,Pune),(1,Rajiv,Reddy,21,9848022337,Hydera bad)})
(22,{(3,Rajesh,Khanna,22,9848022339,Delhi),(2,siddarth,Battacharya,22,984802233 8,Kolkata)})
(23,{(6,Archana,Mishra,23,9848022335,Chennai),(5,Trupthi,Mohanthy,23,9848022336 ,Bhuwaneshwar)})
(24,{(8,Bharathi,Nambiayar,24,9848022333,Chennai),(7,Komal,Nayak,24,9848022334, trivendram)})
```

#### Group by multiple column Operator

**<u>Example :</u>**

We will try to group now the student_details relation by age and city.

```powershell
grunt> group_multiple = GROUP student_details by (age, city);
```

To verify the result dump the relation group_multiple :

```powershell
grunt> Dump group_multiple; 
  
((21,Pune),{(4,Preethi,Agarwal,21,9848022330,Pune)})
((21,Hyderabad),{(1,Rajiv,Reddy,21,9848022337,Hyderabad)})
((22,Delhi),{(3,Rajesh,Khanna,22,9848022339,Delhi)})
((22,Kolkata),{(2,siddarth,Battacharya,22,9848022338,Kolkata)})
((23,Chennai),{(6,Archana,Mishra,23,9848022335,Chennai)})
((23,Bhuwaneshwar),{(5,Trupthi,Mohanthy,23,9848022336,Bhuwaneshwar)})
((24,Chennai),{(8,Bharathi,Nambiayar,24,9848022333,Chennai)})
(24,trivendram),{(7,Komal,Nayak,24,9848022334,trivendram)})
```

#### Group by all column Operator

**<u>Example :</u>**

We will try to group now the student_details relation by all the column in the schema.

```powershell
grunt> group_all = GROUP student_details All;
```

To verify the result dump the relation group_all :

```powershell
grunt> Dump group_all;  
  
(all,{(8,Bharathi,Nambiayar,24,9848022333,Chennai),(7,Komal,Nayak,24,9848022334 ,trivendram), 
(6,Archana,Mishra,23,9848022335,Chennai),(5,Trupthi,Mohanthy,23,9848022336,Bhuw aneshwar), 
(4,Preethi,Agarwal,21,9848022330,Pune),(3,Rajesh,Khanna,22,9848022339,Delhi), 
(2,siddarth,Battacharya,22,9848022338,Kolkata),(1,Rajiv,Reddy,21,9848022337,Hyd erabad)})
```

### CoGroup Operator

The COGROUP operator works more or less in the same way as the GROUP operator. The only difference between the two operators is that the GROUP operator is normally used with one relation, while the COGROUP operator is used in statements involving two or more relations.

```
grunt> Cogroup_data = COGROUP Relation_name BY data_key, Relation_name BY data_key, ... ;
```

**<u>Example :</u>**

We will try to group now the data loaded in two relation by age.

The first relation is the student_details previously used and the employee_details containing the data shown bellow

| ID   | name  | age  | city         |
| ---- | ----- | ---- | ------------ |
| 001  | Robin | 22   | New York     |
| 002  | Bob   | 23   | Kolkata      |
| 003  | Maya  | 23   | Tokyo        |
| 004  | Sara  | 25   | London       |
| 005  | David | 23   | Bhuwaneshwar |
| 006  | Maggy | 22   | Chennai      |

  Now, let's group the two relation by age :

```powershell
grunt> cogroup_data = COGROUP student_details by age, employee_details by age;
```

To verify the result dump the relation cogroup_data :

```powershell
grunt> Dump cogroup_data;
(21,{(4,Preethi,Agarwal,21,9848022330,Pune), (1,Rajiv,Reddy,21,9848022337,Hyderabad)}, 
   {    })  
(22,{ (3,Rajesh,Khanna,22,9848022339,Delhi), (2,siddarth,Battacharya,22,9848022338,Kolkata) },  
   { (6,Maggy,22,Chennai),(1,Robin,22,newyork) })  
(23,{(6,Archana,Mishra,23,9848022335,Chennai),(5,Trupthi,Mohanthy,23,9848022336 ,Bhuwaneshwar)}, 
   {(5,David,23,Bhuwaneshwar),(3,Maya,23,Tokyo),(2,BOB,23,Kolkata)}) 
(24,{(8,Bharathi,Nambiayar,24,9848022333,Chennai),(7,Komal,Nayak,24,9848022334, trivendram)}, 
   { })  
(25,{   }, 
   {(4,Sara,25,London)})
```

The COGROUP operator groups the tuples from each relation according to age where each group depicts a particular age value.

In case a relation doesn’t have tuples having the age value 21, it returns an empty bag.

### Join Operators :

The JOIN operator is used to combine records from two or more relations. While performing a join operation, we declare one (or a group of) tuple(s) from each relation, as keys. Joins can be of the following types:

- Self-join
- Inner-join
- Outer-join − left join, right join, and full join

**<u>Preparation :</u>**

We will prepare before hand to relation containing the data bellow

**Customer :**

```json
1,Ramesh,32,Ahmedabad,2000.00
2,Khilan,25,Delhi,1500.00
3,kaushik,23,Kota,2000.00
4,Chaitali,25,Mumbai,6500.00 
5,Hardik,27,Bhopal,8500.00
6,Komal,22,MP,4500.00
7,Muffy,24,Indore,10000.00
```

**Order :**

```powershell
102,2009-10-08 00:00:00,3,3000
100,2009-10-08 00:00:00,3,1500
101,2009-11-20 00:00:00,2,1560
103,2008-05-20 00:00:00,4,2060
```

we load this two data set in two relation named customers et orders respectively :

```powershell
grunt> customers = LOAD 'hdfs://localhost:9000/pig_data/customers.txt' USING PigStorage(',')
   as (id:int, name:chararray, age:int, address:chararray, salary:int);
  
grunt> orders = LOAD 'hdfs://localhost:9000/pig_data/orders.txt' USING PigStorage(',')
   as (oid:int, date:chararray, customer_id:int, amount:int);
```

now we will see the different join on these data set.

#### Self-Join

Self-join is used to join a table with itself as if the table were two relations, temporarily renaming at least one relation

```powershell
grunt> Relation3_name = JOIN Relation1_name BY key, Relation2_name BY key ;

```

**<u>Example :</u>**

Let's perform self-join on the customer relation :

```powershell
grunt> customers2 = JOIN customers BY id, customers BY id;
```

we dump the result to verify :

```powershell
grunt> Dump customers2;
(1,Ramesh,32,Ahmedabad,2000,1,Ramesh,32,Ahmedabad,2000)
(2,Khilan,25,Delhi,1500,2,Khilan,25,Delhi,1500)
(3,kaushik,23,Kota,2000,3,kaushik,23,Kota,2000)
(4,Chaitali,25,Mumbai,6500,4,Chaitali,25,Mumbai,6500)
(5,Hardik,27,Bhopal,8500,5,Hardik,27,Bhopal,8500)
(6,Komal,22,MP,4500,6,Komal,22,MP,4500)
(7,Muffy,24,Indore,10000,7,Muffy,24,Indore,10000)
```

#### Inner Join

Inner Join is used quite frequently. An inner join returns rows when there is a match in both tables. The query compares each row of A with each row of B to find all pairs of rows which satisfy the join-predicate.

```
grunt> result = JOIN relation1 BY columnname, relation2 BY columnname;

```

**<u>Example :</u>**

Let's perform inner join on the customers and orders relation :

```powershell
grunt> customer_orders = JOIN customers BY id, orders BY customer_id;
```

We verify the results with a dump :

```powershell
grunt> Dump customer_orders;
(2,Khilan,25,Delhi,1500,101,2009-11-20 00:00:00,2,1560)
(3,kaushik,23,Kota,2000,100,2009-10-08 00:00:00,3,1500)
(3,kaushik,23,Kota,2000,102,2009-10-08 00:00:00,3,3000)
(4,Chaitali,25,Mumbai,6500,103,2008-05-20 00:00:00,4,2060)
```

#### Left-outer Join

The left-outer Join operation returns all rows from the left table, even if there are no matches in the right relation. 

```powershell
grunt> Relation3_name = JOIN Relation1_name BY id LEFT OUTER, Relation2_name BY customer_id;
```

**<u>Example :</u>**

Let's perform left-outer join on the customers and orders relation :

```powershell
grunt> outer_left = JOIN customers BY id LEFT OUTER, orders BY customer_id;
```

We verify the results with a dump :

```powershell
grunt> Dump outer_left;
(1,Ramesh,32,Ahmedabad,2000,,,,)
(2,Khilan,25,Delhi,1500,101,2009-11-20 00:00:00,2,1560)
(3,kaushik,23,Kota,2000,100,2009-10-08 00:00:00,3,1500)
(3,kaushik,23,Kota,2000,102,2009-10-08 00:00:00,3,3000)
(4,Chaitali,25,Mumbai,6500,103,2008-05-20 00:00:00,4,2060)
(5,Hardik,27,Bhopal,8500,,,,)
(6,Komal,22,MP,4500,,,,)
(7,Muffy,24,Indore,10000,,,,) 
```

#### Right-outer Join

The right-outer join operation returns all rows from the right table, even if there are no matches in the left table.

```powershell
grunt> outer_right = JOIN customers BY id RIGHT OUTER, orders BY customer_id;
```

**<u>Example :</u>**

Let's perform right-outer join on the customers and orders relation :

```powershell
grunt> outer_left = JOIN customers BY id RIGHT OUTER, orders BY customer_id;
```

We verify the results with a dump :

```powershell
grunt> Dump outer_right
(2,Khilan,25,Delhi,1500,101,2009-11-20 00:00:00,2,1560)
(3,kaushik,23,Kota,2000,100,2009-10-08 00:00:00,3,1500)
(3,kaushik,23,Kota,2000,102,2009-10-08 00:00:00,3,3000)
(4,Chaitali,25,Mumbai,6500,103,2008-05-20 00:00:00,4,2060)
```

#### Full-outer Join

The full-outer join operation returns rows when there is a match in one of the relations.

```
grunt> outer_full = JOIN customers BY id FULL OUTER, orders BY customer_id;

```

**<u>Example :</u>**

Let's perform full-outer join on the customers and orders relation :

```powershell
grunt> outer_full = JOIN customers BY id FULL OUTER, orders BY customer_id;
```

We verify the results with a dump :

```powershell
grunt> Dump outer_full; 
(1,Ramesh,32,Ahmedabad,2000,,,,)
(2,Khilan,25,Delhi,1500,101,2009-11-20 00:00:00,2,1560)
(3,kaushik,23,Kota,2000,100,2009-10-08 00:00:00,3,1500)
(3,kaushik,23,Kota,2000,102,2009-10-08 00:00:00,3,3000)
(4,Chaitali,25,Mumbai,6500,103,2008-05-20 00:00:00,4,2060)
(5,Hardik,27,Bhopal,8500,,,,)
(6,Komal,22,MP,4500,,,,)
(7,Muffy,24,Indore,10000,,,,)
```

#### Join with multiple key

It's possible to perform each of the previous join with multiple keys.

```powershell
grunt> Relation3_name = JOIN Relation2_name BY (key1, key2), Relation3_name BY (key1, key2);
```

**<u>Example :</u>**

we will first load a two new relation employee and employee_contact containing the data bellow :

**Employee**

```powershell
001,Rajiv,Reddy,21,programmer,003
002,siddarth,Battacharya,22,programmer,003
003,Rajesh,Khanna,22,programmer,003
004,Preethi,Agarwal,21,programmer,003
005,Trupthi,Mohanthy,23,programmer,003
006,Archana,Mishra,23,programmer,003
007,Komal,Nayak,24,teamlead,002
008,Bharathi,Nambiayar,24,manager,001
```

**Employee_contact**

```powershell
001,9848022337,Rajiv@gmail.com,Hyderabad,003
002,9848022338,siddarth@gmail.com,Kolkata,003
003,9848022339,Rajesh@gmail.com,Delhi,003
004,9848022330,Preethi@gmail.com,Pune,003
005,9848022336,Trupthi@gmail.com,Bhuwaneshwar,003
006,9848022335,Archana@gmail.com,Chennai,003
007,9848022334,Komal@gmail.com,trivendram,002
008,9848022333,Bharathi@gmail.com,Chennai,001
```

Let's make a join on the id and the jobId :

```powershell
grunt> emp = JOIN employee BY (id,jobid), employee_contact BY (id,jobid);
```

we display the result :

```powershell
grunt> Dump emp;
(1,Rajiv,Reddy,21,programmer,113,1,9848022337,Rajiv@gmail.com,Hyderabad,113)
(2,siddarth,Battacharya,22,programmer,113,2,9848022338,siddarth@gmail.com,Kolka ta,113)  
(3,Rajesh,Khanna,22,programmer,113,3,9848022339,Rajesh@gmail.com,Delhi,113)  
(4,Preethi,Agarwal,21,programmer,113,4,9848022330,Preethi@gmail.com,Pune,113)  
(5,Trupthi,Mohanthy,23,programmer,113,5,9848022336,Trupthi@gmail.com,Bhuwaneshw ar,113)  
(6,Archana,Mishra,23,programmer,113,6,9848022335,Archana@gmail.com,Chennai,113)  
(7,Komal,Nayak,24,teamlead,112,7,9848022334,Komal@gmail.com,trivendram,112)  
(8,Bharathi,Nambiayar,24,manager,111,8,9848022333,Bharathi@gmail.com,Chennai,111)
```

### Cross Operator

The Cross operator compute the product of crossing two or more relation.

```powershell
grunt> Relation3_name = CROSS Relation1_name, Relation2_name;
```

**<u>Example :</u>**

In this example we will cross the relations customers and orders used in the previous join example.

```powershell
grunt> cross_data = CROSS customers, orders;
```

And the the result of this cross is :

```powershell
(7,Muffy,24,Indore,10000,103,2008-05-20 00:00:00,4,2060) 
(7,Muffy,24,Indore,10000,101,2009-11-20 00:00:00,2,1560) 
(7,Muffy,24,Indore,10000,100,2009-10-08 00:00:00,3,1500) 
(7,Muffy,24,Indore,10000,102,2009-10-08 00:00:00,3,3000) 
(6,Komal,22,MP,4500,103,2008-05-20 00:00:00,4,2060) 
(6,Komal,22,MP,4500,101,2009-11-20 00:00:00,2,1560) 
(6,Komal,22,MP,4500,100,2009-10-08 00:00:00,3,1500) 
(6,Komal,22,MP,4500,102,2009-10-08 00:00:00,3,3000) 
(5,Hardik,27,Bhopal,8500,103,2008-05-20 00:00:00,4,2060) 
(5,Hardik,27,Bhopal,8500,101,2009-11-20 00:00:00,2,1560) 
(5,Hardik,27,Bhopal,8500,100,2009-10-08 00:00:00,3,1500) 
(5,Hardik,27,Bhopal,8500,102,2009-10-08 00:00:00,3,3000) 
(4,Chaitali,25,Mumbai,6500,103,2008-05-20 00:00:00,4,2060) 
(4,Chaitali,25,Mumbai,6500,101,2009-20 00:00:00,4,2060) 
(2,Khilan,25,Delhi,1500,101,2009-11-20 00:00:00,2,1560) 
(2,Khilan,25,Delhi,1500,100,2009-10-08 00:00:00,3,1500) 
(2,Khilan,25,Delhi,1500,102,2009-10-08 00:00:00,3,3000) 
(1,Ramesh,32,Ahmedabad,2000,103,2008-05-20 00:00:00,4,2060) 
(1,Ramesh,32,Ahmedabad,2000,101,2009-11-20 00:00:00,2,1560) 
(1,Ramesh,32,Ahmedabad,2000,100,2009-10-08 00:00:00,3,1500) 
(1,Ramesh,32,Ahmedabad,2000,102,2009-10-08 00:00:00,3,3000)-11-20 00:00:00,2,1560) 
(4,Chaitali,25,Mumbai,6500,100,2009-10-08 00:00:00,3,1500) 
(4,Chaitali,25,Mumbai,6500,102,2009-10-08 00:00:00,3,3000) 
(3,kaushik,23,Kota,2000,103,2008-05-20 00:00:00,4,2060) 
(3,kaushik,23,Kota,2000,101,2009-11-20 00:00:00,2,1560) 
(3,kaushik,23,Kota,2000,100,2009-10-08 00:00:00,3,1500) 
(3,kaushik,23,Kota,2000,102,2009-10-08 00:00:00,3,3000) 
(2,Khilan,25,Delhi,1500,103,2008-05-20 00:00:00,4,2060) 
(2,Khilan,25,Delhi,1500,101,2009-11-20 00:00:00,2,1560) 
(2,Khilan,25,Delhi,1500,100,2009-10-08 00:00:00,3,1500)
(2,Khilan,25,Delhi,1500,102,2009-10-08 00:00:00,3,3000) 
(1,Ramesh,32,Ahmedabad,2000,103,2008-05-20 00:00:00,4,2060) 
(1,Ramesh,32,Ahmedabad,2000,101,2009-11-20 00:00:00,2,1560) 
(1,Ramesh,32,Ahmedabad,2000,100,2009-10-08 00:00:00,3,1500) 
(1,Ramesh,32,Ahmedabad,2000,102,2009-10-08 00:00:00,3,3000)  
```

### Union Operator

The UNION operator merges the content of two relations. To perform UNION operation on two relations, their columns and types must be identical.

```powershell
grunt> Relation_name3 = UNION Relation_name1, Relation_name2;
```

**<u>Example :</u>**

We will cross two relations : student_data1 and student_data2. The data loaded in the relations are shown in the table below :

**student_data1 :**

| id   | first name | last name   | phone number | city         |
| ---- | ---------- | ----------- | ------------ | ------------ |
| 001  | Rajiv      | Reddy       | 9848022337   | Hyderabad    |
| 002  | siddarth   | Battacharya | 9848022338   | Kolkata      |
| 003  | Rajesh     | Khanna      | 9848022339   | Delhi        |
| 004  | Preethi    | Agarwal     | 9848022330   | Pune         |
| 005  | Trupthi    | Mohanthy    | 9848022336   | Bhuwaneshwar |
| 006  | Archana    | Mishra      | 9848022335   | Chennai      |

**student_data2 :**

| id   | first name | last name | phone number | city       |
| ---- | ---------- | --------- | ------------ | ---------- |
| 007  | Komal      | Nayak     | 9848022334   | Trivendram |
| 008  | Bharathi   | Nambiayar | 9848022333   | Chennai    |

Let us now merge the two relation using the query :

```powershell
grunt> student = UNION student1, student2;
```

We verify the results :

```powershell
grunt> Dump student; 
(1,Rajiv,Reddy,9848022337,Hyderabad) (2,siddarth,Battacharya,9848022338,Kolkata)
(3,Rajesh,Khanna,9848022339,Delhi)
(4,Preethi,Agarwal,9848022330,Pune) 
(5,Trupthi,Mohanthy,9848022336,Bhuwaneshwar)
(6,Archana,Mishra,9848022335,Chennai) 
(7,Komal,Nayak,9848022334,trivendram) 
(8,Bharathi,Nambiayar,9848022333,Chennai)
```

### Split Operator

The SPLIT operator split a relation in multiple relation.

```powershell
grunt> SPLIT Relation1_name INTO Relation2_name IF (condition1), Relation2_name (condition2),
```

**<u>Example :</u>**

In this example, we will split the following data stored in the relation student in two new relation by the age:

| ID   | First name | Last Name   | age  | phone      | city         |
| ---- | ---------- | ----------- | ---- | ---------- | ------------ |
| 001  | Rajiv      | Reddy       | 21   | 9848022337 | Hyderabad    |
| 002  | siddarth   | Battacharya | 22   | 9848022338 | Kolkata      |
| 003  | Rajesh     | Khanna      | 22   | 9848022339 | Delhi        |
| 004  | Preethi    | Agarwal     | 21   | 9848022330 | Pune         |
| 005  | Trupthi    | Mohanthy    | 23   | 9848022336 | Bhuwaneshwar |
| 006  | Archana    | Mishra      | 23   | 9848022335 | Chennai      |
| 007  | Komal      | Nayak       | 24   | 9848022334 | Trivendram   |
| 008  | Bharathi   | Nambiayar   | 24   | 9848022333 | Chennai      |

We split the relation in two new relation : student_details1 and student_details2.

```powershell
SPLIT student into student_details1 if age<23, student_details2 if (22<age and age>25);
```

We verify the two new relation :

```powershell
grunt> Dump student_details1;  
(1,Rajiv,Reddy,21,9848022337,Hyderabad) 
(2,siddarth,Battacharya,22,9848022338,Kolkata)
(3,Rajesh,Khanna,22,9848022339,Delhi) 
(4,Preethi,Agarwal,21,9848022330,Pune)
grunt> Dump student_details2; 
(5,Trupthi,Mohanthy,23,9848022336,Bhuwaneshwar) 
(6,Archana,Mishra,23,9848022335,Chennai) 
(7,Komal,Nayak,24,9848022334,trivendram) 
(8,Bharathi,Nambiayar,24,9848022333,Chennai)
```

### Filter Operator

The FILTER operator is used to select some tuples from a relation based on a condition. It's equivalent to a SQL SELECT.

```powershell
grunt> Relation2_name = FILTER Relation1_name BY (condition);
```

**<u>Example :</u>**

In this example we will try to select the student living in "Chennai" from the student relation used in the example of the SPLIT operator.

```powershell
filter_data = FILTER student_details BY city == 'Chennai';
```

We now display the content of filter_data :

```powershell
grunt> Dump filter_data;
(6,Archana,Mishra,23,9848022335,Chennai)
(8,Bharathi,Nambiayar,24,9848022333,Chennai)
```

### Distinct Operator

The DISTINCT operator remove the redundant tuples from a relation.

```powershell
grunt> Relation_name2 = DISTINCT Relatin_name1;
```

**<u>Example :</u>**

In this example we will remove the duplicate from the table below loaded in the relation student_details :

| ID   | First name | Last Name   | age  | phone      | city         |
| ---- | ---------- | ----------- | ---- | ---------- | ------------ |
| 001  | Rajiv      | Reddy       | 21   | 9848022337 | Hyderabad    |
| 002  | siddarth   | Battacharya | 22   | 9848022338 | Kolkata      |
| 002  | siddarth   | Battacharya | 22   | 9848022338 | Kolkata      |
| 003  | Rajesh     | Khanna      | 22   | 9848022339 | Delhi        |
| 003  | Rajesh     | Khanna      | 22   | 9848022339 | Delhi        |
| 004  | Preethi    | Agarwal     | 21   | 9848022330 | Pune         |
| 005  | Trupthi    | Mohanthy    | 23   | 9848022336 | Bhuwaneshwar |
| 006  | Archana    | Mishra      | 23   | 9848022335 | Chennai      |
| 006  | Archana    | Mishra      | 23   | 9848022335 | Chennai      |

The query to remove the duplicate is :

```powershell
grunt> distinct_data = DISTINCT student_details;
```

We verify the results :

```powershell
grunt> Dump distinct_data;
(1,Rajiv,Reddy,9848022337,Hyderabad)
(2,siddarth,Battacharya,9848022338,Kolkata) 
(3,Rajesh,Khanna,9848022339,Delhi) 
(4,Preethi,Agarwal,9848022330,Pune) 
(5,Trupthi,Mohanthy,9848022336,Bhuwaneshwar)
(6,Archana,Mishra,9848022335,Chennai)
```

### Foreach Operator

The FOREACH operator is used to generate data transformations on the column data.

```powershell
grunt> Relation_name2 = FOREACH Relatin_name1 GENERATE (required data);
```

**<u>Example :</u>**

We will get the id , the age and city values of each student from the relation student_details containing the following data :

| ID   | First name | Last Name   | age  | phone      | city         |
| ---- | ---------- | ----------- | ---- | ---------- | ------------ |
| 001  | Rajiv      | Reddy       | 21   | 9848022337 | Hyderabad    |
| 002  | siddarth   | Battacharya | 22   | 9848022338 | Kolkata      |
| 003  | Rajesh     | Khanna      | 22   | 9848022339 | Delhi        |
| 004  | Preethi    | Agarwal     | 21   | 9848022330 | Pune         |
| 005  | Trupthi    | Mohanthy    | 23   | 9848022336 | Bhuwaneshwar |
| 006  | Archana    | Mishra      | 23   | 9848022335 | Chennai      |
| 007  | Komal      | Nayak       | 24   | 9848022334 | Trivendram   |
| 008  | Bharathi   | Nambiayar   | 24   | 9848022333 | Chennai      |

The query to get the column is :

```powershell
grunt> foreach_data = FOREACH student_details GENERATE id,age,city;
```

We dump the results in foreach_data :

```powershell
grunt> Dump foreach_data;
(1,21,Hyderabad)
(2,22,Kolkata)
(3,22,Delhi)
(4,21,Pune) 
(5,23,Bhuwaneshwar)
(6,23,Chennai) 
(7,24,trivendram)
(8,24,Chennai) 
```

### Order By Operator

The ORDER BY operator is used to display the contents of a relation in a sorted order based on one or more fields.

```powershell
grunt> Relation_name2 = ORDER Relatin_name1 BY (ASC|DESC);
```

**<u>Example :</u>**

We will sort the student_details relation in a descending order based on the student age. The student_details relation contains the following data :

| ID   | First name | Last Name   | age  | phone      | city         |
| ---- | ---------- | ----------- | ---- | ---------- | ------------ |
| 001  | Rajiv      | Reddy       | 21   | 9848022337 | Hyderabad    |
| 002  | siddarth   | Battacharya | 22   | 9848022338 | Kolkata      |
| 003  | Rajesh     | Khanna      | 22   | 9848022339 | Delhi        |
| 004  | Preethi    | Agarwal     | 21   | 9848022330 | Pune         |
| 005  | Trupthi    | Mohanthy    | 23   | 9848022336 | Bhuwaneshwar |
| 006  | Archana    | Mishra      | 23   | 9848022335 | Chennai      |
| 007  | Komal      | Nayak       | 24   | 9848022334 | Trivendram   |
| 008  | Bharathi   | Nambiayar   | 24   | 9848022333 | Chennai      |

The query to order the relation is :

```powershell
grunt> order_by_data = ORDER student_details BY age DESC;
```

We verify the results :

```powershell
grunt> Dump order_by_data; 
(8,Bharathi,Nambiayar,24,9848022333,Chennai)
(7,Komal,Nayak,24,9848022334,trivendram)
(6,Archana,Mishra,23,9848022335,Chennai) 
(5,Trupthi,Mohanthy,23,9848022336,Bhuwaneshwar)
(3,Rajesh,Khanna,22,9848022339,Delhi) 
(2,siddarth,Battacharya,22,9848022338,Kolkata)
(4,Preethi,Agarwal,21,9848022330,Pune) 
(1,Rajiv,Reddy,21,9848022337,Hyderabad)
```

### Limit Operator

The LIMIT operator is used to get a limited number of tuples from a relation.

```powershell
grunt> Result = LIMIT Relation_name required number of tuples;
```

**<u>Example :</u>**

We will extract from the student_details relation the 4 first entry. The student_details relation contains the following data :

| ID   | First name | Last Name   | age  | phone      | city         |
| ---- | ---------- | ----------- | ---- | ---------- | ------------ |
| 001  | Rajiv      | Reddy       | 21   | 9848022337 | Hyderabad    |
| 002  | siddarth   | Battacharya | 22   | 9848022338 | Kolkata      |
| 003  | Rajesh     | Khanna      | 22   | 9848022339 | Delhi        |
| 004  | Preethi    | Agarwal     | 21   | 9848022330 | Pune         |
| 005  | Trupthi    | Mohanthy    | 23   | 9848022336 | Bhuwaneshwar |
| 006  | Archana    | Mishra      | 23   | 9848022335 | Chennai      |
| 007  | Komal      | Nayak       | 24   | 9848022334 | Trivendram   |
| 008  | Bharathi   | Nambiayar   | 24   | 9848022333 | Chennai      |

The following query extract the 4 first tuples :

```powershell
grunt> limit_data = LIMIT student_details 4; 
```

We verify the results :

```powershell
grunt> Dump limit_data; 
(1,Rajiv,Reddy,21,9848022337,Hyderabad) 
(2,siddarth,Battacharya,22,9848022338,Kolkata) 
(3,Rajesh,Khanna,22,9848022339,Delhi) 
(4,Preethi,Agarwal,21,9848022330,Pune) 
```

