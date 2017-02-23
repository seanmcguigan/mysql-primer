## mysql-primer

### create table
```
mysql> create table tbFootBallScores (home varchar(15),away varchar(15));
```
### select from table
```
mysql> select custInfoName from tbCustomerInfoBkup where custInfoCityName like 'Belfast';
```
### add column
```
mysql> alter table tbCustomerInfoBkup add custInfoDOB varchar(10);
```
### update data for column
```
update tbEmpInfo set custNumFingers = '41' where empID=10;
```
### add data
```
mysql> insert into tbCustomerInfoBkup (custInfoName,custInfoLastName,custInfoAddr1,custInfoAddr2,custInfoCityName,custInfoCounty,custInfoPostcode,custInfoPhone) values ('Gwen','Matlock','33 Ball Row','','Leeds','CD','LE12 2BF','07734876497');
```
### update data for column
```
update ssh_keys set ssh_key='new_value' where username='warp'; 
```

### delete row identify by data value
```
mysql> delete from tbCustomerInfoBkup where custInfoDOB='7/9/1987';
```
### change column type from varchar to year
```
mysql> alter table tbCustomerInfoBkup modify custInfoDOB year;
```
### create index on the table primary key (it's unique) column for better searching.
 <!---Indexes are used to find rows with specific column values quickly. Without an index, MySQL must begin with the first row and then read through the entire table to find the relevant rows. The larger the table, the more this costs. If the table has an index for the columns in question, MySQL can quickly determine the position to seek to in the middle of the data file without having to look at all the data. This is much faster than reading every row sequentially.
-->
```
mysql> create index indexCustInfoID on tbCustomerDBInfo (custID);
```
### remove data but leave schema
```
truncate table tbCustomerInfoBkup;
```
### auto increment
```
create table tbEmpInfo(empID int PRIMARY KEY AUTO_INCREMENT,empLastName varchar(20),empSSN varchar(11));

mysql> show fields from tbEmpInfo;
+-------------+-------------+------+-----+---------+----------------+
| Field       | Type        | Null | Key | Default | Extra          |
+-------------+-------------+------+-----+---------+----------------+
| empID       | int(11)     | NO   | PRI | NULL    | auto_increment |
| empLastName | varchar(20) | YES  |     | NULL    |                |
| empSSN      | varchar(11) | YES  |     | NULL    |                |
+-------------+-------------+------+-----+---------+----------------+
3 rows in set (0.00 sec)

insert into tbEmpInfo(empLastName,empSSN) values ('McGuigan','A89736534N');

mysql> select * from tbEmpInfo;
+-------+-------------+------------+
| empID | empLastName | empSSN     |
+-------+-------------+------------+
|     1 | McGuigan    | A89736534N |
+-------+-------------+------------+
1 row in set (0.00 sec)

mysql> insert into tbEmpInfo(empLastName,empSSN) values ('May','K83736534V');
Query OK, 1 row affected (0.00 sec)

mysql> select * from tbEmpInfo;
+-------+-------------+------------+
| empID | empLastName | empSSN     |
+-------+-------------+------------+
|     1 | McGuigan    | A89736534N |
|     2 | May         | K83736534V |
+-------+-------------+------------+
2 rows in set (0.00 sec)
```
### on the table tbCustomerDBInfo change Field custID from varchar to integer and use the consraint AUTO_INCREMENT
```
mysql> show fields from tbCustomerDBInfo;
+------------------+-------------+------+-----+---------+-------+
| Field            | Type        | Null | Key | Default | Extra |
+------------------+-------------+------+-----+---------+-------+
| custID           | varchar(10) | NO   | PRI | NULL    |       |
| custInfoName     | varchar(50) | YES  |     | NULL    |       |
| custInfoLastName | varchar(50) | YES  |     | NULL    |       |
| custInfoAddr1    | varchar(50) | YES  |     | NULL    |       |
| custInfoAddr2    | varchar(50) | YES  |     | NULL    |       |
| custInfoCityName | varchar(50) | YES  |     | NULL    |       |
| custInfoCounty   | varchar(10) | YES  |     | NULL    |       |
| custInfoPostcode | varchar(50) | YES  |     | NULL    |       |
| custInfoPhone    | varchar(12) | YES  |     | NULL    |       |
+------------------+-------------+------+-----+---------+-------+
9 rows in set (0.00 sec)

mysql> alter table tbCustomerDBInfo modify custID int AUTO_INCREMENT;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> show fields from tbCustomerDBInfo;
+------------------+-------------+------+-----+---------+----------------+
| Field            | Type        | Null | Key | Default | Extra          |
+------------------+-------------+------+-----+---------+----------------+
| custID           | int(11)     | NO   | PRI | NULL    | auto_increment |
| custInfoName     | varchar(50) | YES  |     | NULL    |                |
| custInfoLastName | varchar(50) | YES  |     | NULL    |                |
| custInfoAddr1    | varchar(50) | YES  |     | NULL    |                |
| custInfoAddr2    | varchar(50) | YES  |     | NULL    |                |
| custInfoCityName | varchar(50) | YES  |     | NULL    |                |
| custInfoCounty   | varchar(10) | YES  |     | NULL    |                |
| custInfoPostcode | varchar(50) | YES  |     | NULL    |                |
| custInfoPhone    | varchar(12) | YES  |     | NULL    |                |
+------------------+-------------+------+-----+---------+----------------+
9 rows in set (0.01 sec)
```
### functions, Count, how many records do I have?
```
mysql> select count(*) from tbCustomerInfo;
+----------+
| count(*) |
+----------+
|        2 |
+----------+
1 row in set (0.00 sec)
```
### show me how many users have the same last name
```
mysql> select * from tbCustomerInfo;
+--------------+------------------+---------------+---------------+------------------+----------------+------------------+---------------+
| custInfoName | custInfoLastName | custInfoAddr1 | custInfoAddr2 | custInfoCityName | custInfoCounty | custInfoPostcode | custInfoPhone |
+--------------+------------------+---------------+---------------+------------------+----------------+------------------+---------------+
| Gwen         | Matlock          | 33 Ball Row   |               | Leeds            | CD             | LE12 2BF         | 07734876497   |
| Steve        | Austin           | 5 nut row     |               | Lincon           | LN             | LN52 2BF         | 07730746497   |
| Mary         | Austin           | 5 nut row     |               | Lincon           | LN             | LN52 2BF         | 07730746497   |
+--------------+------------------+---------------+---------------+------------------+----------------+------------------+---------------+
3 rows in set (0.00 sec)

mysql> select count(distinct custInfoLastName) from tbCustomerInfo;
+----------------------------------+
| count(distinct custInfoLastName) |
+----------------------------------+
|                                2 |
+----------------------------------+
1 row in set (0.00 sec)
```
### select like
```
mysql> select * from tbCustomerInfo where custInfoLastName='Austin';
+--------------+------------------+---------------+---------------+------------------+----------------+------------------+---------------+
| custInfoName | custInfoLastName | custInfoAddr1 | custInfoAddr2 | custInfoCityName | custInfoCounty | custInfoPostcode | custInfoPhone |
+--------------+------------------+---------------+---------------+------------------+----------------+------------------+---------------+
| Steve        | Austin           | 5 nut row     |               | Lincon           | LN             | LN52 2BF         | 07730746497   |
| Mary         | Austin           | 5 nut row     |               | Lincon           | LN             | LN52 2BF         | 07730746497   |
+--------------+------------------+---------------+---------------+------------------+----------------+------------------+---------------+
2 rows in set (0.00 sec)
```
### find customer last names that begin with A (% == wildcard, _ == any single charachter)
```
mysql> select * from tbCustomerInfo where custInfoLastName like 'A%';
+--------------+------------------+---------------+---------------+------------------+----------------+------------------+---------------+
| custInfoName | custInfoLastName | custInfoAddr1 | custInfoAddr2 | custInfoCityName | custInfoCounty | custInfoPostcode | custInfoPhone |
+--------------+------------------+---------------+---------------+------------------+----------------+------------------+---------------+
| Steve        | Austin           | 5 nut row     |               | Lincon           | LN             | LN52 2BF         | 07730746497   |
| Mary         | Austin           | 5 nut row     |               | Lincon           | LN             | LN52 2BF         | 07730746497   |
+--------------+------------------+---------------+---------------+------------------+----------------+------------------+---------------+
2 rows in set (0.00 sec)
```
### combine with count HOW MANY records exist where the last name begins with A
```
mysql> select count(*) from tbCustomerInfo where custInfoLastName like 'A%';~
+----------+
| count(*) |
+----------+
|        2 |
+----------+
1 row in set (0.00 sec)

mysql> select * from tbEmpInfo;
+-------+-------------+-------------+----------------+
| empID | empLastName | empSSN      | custNumFingers |
+-------+-------------+-------------+----------------+
|     1 | McGuigan    | A89736534N  |             32 |
|     2 | May         | K83736534V  |             73 |
|     3 | Mercury     | K83736534V  |             11 |
|     4 | Decon       | K83736534V  |            141 |
|     5 | Taylor      | K83736534V  |           2141 |
|     6 | Watson      | K83736534V  |             19 |
|     7 | Crick       | K83736534V  |             98 |
|     8 | Bush        | K83736534V  |              3 |
|     9 | Gore        | K83736534V  |            112 |
|    10 | Bush        | GT645342K2O |             41 |
+-------+-------------+-------------+----------------+
10 rows in set (0.00 sec)


mysql> show fields from tbEmpInfo;
+-------------+-------------+------+-----+---------+----------------+
| Field       | Type        | Null | Key | Default | Extra          |
+-------------+-------------+------+-----+---------+----------------+
| empID       | int(11)     | NO   | PRI | NULL    | auto_increment |
| empLastName | varchar(20) | YES  |     | NULL    |                |
| empSSN      | varchar(11) | YES  |     | NULL    |                |
+-------------+-------------+------+-----+---------+----------------+
3 rows in set (0.00 sec)
```
### count how many custumers are called Bush
```
mysql> select count(*) from tbEmpInfo where empLastName like '%bush%';
+----------+
| count(*) |
+----------+
|        2 |name like
+----------+
1 row in set (0.00 sec)
```
### get me the aveage number of fingers, and sum total of fingers, and count the occurence of, anyone in tbEmpInfo that has # the last name Bush. 
```
mysql> select AVG(custNumFingers),SUM(custNumFingers),COUNT(*) FROM tbEmpInfo WHERE empLastName LIKE '%bush%';
+---------------------+---------------------+----------+
| AVG(custNumFingers) | SUM(custNumFingers) | COUNT(*) |
+---------------------+---------------------+----------+
|             22.0000 |                  44 |        2 |
+---------------------+---------------------+----------+
1 row in set (0.00 sec)
```
### and for people whose name begins with m
```
mysql> select AVG(custNumFingers),SUM(custNumFingers),COUNT(*) FROM tbEmpInfo WHERE empLastName LIKE 'm%';
+---------------------+---------------------+----------+
| AVG(custNumFingers) | SUM(custNumFingers) | COUNT(*) |
+---------------------+---------------------+----------+
|             38.6667 |                 116 |        3 |
+---------------------+---------------------+----------+
1 row in set (0.00 sec)
```
### With their name 
### Disable ONLY_FULL_GROUP_BY, mysql> set sql_mode = ''
```
mysql> select empLastName,AVG(custNumFingers),SUM(custNumFingers),COUNT(*) FROM tbEmpInfo WHERE empLastName LIKE '%bush%';
+-------------+---------------------+---------------------+----------+
| empLastName | AVG(custNumFingers) | SUM(custNumFingers) | COUNT(*) |
+-------------+---------------------+---------------------+----------+
| Bush        |             22.0000 |                  44 |        2 |
+-------------+---------------------+---------------------+----------+
1 row in set (0.00 sec)
```
### stored proceedure
```
 DELIMITER //
 CREATE PROCEDURE GetAllProducts()
   BEGIN
   SELECT *  FROM products;
   END //
 DELIMITER ;
```
### call the procedure
```
CALL STORED_PROCEDURE_NAME();
```
### view, run only when data changes, as opposed to running in a loop(poll v push)
### lets create a view, which effectivly creates a table
```
mysql> select * from tbEmpInfo;
+-------+-------------+-------------+----------------+-------------+------------------------+
| empID | empLastName | empSSN      | custNumFingers | custInfoSex | custInfoCriminalRecord |
+-------+-------------+-------------+----------------+-------------+------------------------+
|     1 | McGuigan    | A89736534P  |             32 | Male        | yes                    |
|     2 | May         | K83736534V  |             73 | Male        | yes                    |
|     3 | Mercury     | K83736534V  |             11 | Female      | no                     |
|     4 | Decon       | K83736534V  |            141 | Male        | yes                    |
|     5 | Taylor      | K83736534V  |           2141 | Male        | no                     |
|     6 | Watson      | K83736534V  |             19 | Male        | yes                    |
|     7 | Cricks      | K83736534V  |             98 | Male        | yes                    |
|     8 | Bush        | K83736534V  |              3 | Male        | no                     |
|     9 | Gore        | K83736534V  |            112 | Male        | yes                    |
|    10 | Bush        | GT645342K2O |             41 | Male        | yes                    |
+-------+-------------+-------------+----------------+-------------+------------------------+
10 rows in set (0.00 sec)

mysql> CREATE VIEW myView AS SELECT COUNT(*),AVG(custNumFingers),SUM(custNumFingers) FROM tbEmpInfo WHERE custNumFingers > 50;
Query OK, 0 rows affected (0.00 sec

mysql> show tables;
+--------------------------+
| Tables_in_dbCustomerInfo |
+--------------------------+
| myView                   |
| tbCustomerDBInfo         |
| tbCustomerInfo           |
| tbCustomerInfoBkup       |
| tbEmpInfo                |
| tbFootBallScores         |
+--------------------------+
6 rows in set (0.00 sec)

mysql> select * from myView;
+----------+---------------------+---------------------+
| COUNT(*) | AVG(custNumFingers) | SUM(custNumFingers) |
+----------+---------------------+---------------------+
|        5 |            513.0000 |                2565 |
+----------+---------------------+---------------------+
1 row in set (0.00 sec)

mysql> 
```
### joins, selecting two or more rows from different tables based on some common field.
### lets do a join(INNER) from two tables
```
mysql> select * from tbCustomerDBInfo;
+--------+--------------+------------------+---------------+---------------+------------------+----------------+------------------+---------------+
| custID | custInfoName | custInfoLastName | custInfoAddr1 | custInfoAddr2 | custInfoCityName | custInfoCounty | custInfoPostcode | custInfoPhone |
+--------+--------------+------------------+---------------+---------------+------------------+----------------+------------------+---------------+
|      1 | Sean         | McGuigan         | NULL          | NULL          | London           | NULL           | NULL             | NULL          |
|      2 | James        | Cook             | NULL          | NULL          | London           | NULL           | NULL             | NULL          |
|      3 | Janice       | Gandolfino       | NULL          | NULL          | London           | NULL           | NULL             | NULL          |
+--------+--------------+------------------+---------------+---------------+------------------+----------------+------------------+---------------
mysql> select * from tbEmpInfo;
+-------+-------------+-------------+----------------+-------------+------------------------+
| empID | empLastName | empSSN      | custNumFingers | custInfoSex | custInfoCriminalRecord |
+-------+-------------+-------------+----------------+-------------+------------------------+
|     1 | McGuigan    | A89736534P  |             32 | Male        | yes                    |
|     2 | May         | K83736534V  |             73 | Male        | yes                    |
|     3 | Mercury     | K83736534V  |             11 | Female      | no                     |
|     4 | Decon       | K83736534V  |            141 | Male        | yes                    |
|     5 | Taylor      | K83736534V  |           2141 | Male        | no                     |
|     6 | Watson      | K83736534V  |             19 | Male        | yes                    |
|     7 | Cricks      | K83736534V  |             98 | Male        | yes                    |
|     8 | Bush        | K83736534V  |              3 | Male        | no                     |
|     9 | Gore        | K83736534V  |            112 | Male        | yes                    |
|    10 | Bush        | GT645342K2O |             41 | Male        | yes                    |
+-------+-------------+-------------+----------------+-------------+------------------------+

mysql> SELECT tbEmpInfo.custInfoCriminalRecord, tbCustomerDBInfo.custInfoName, tbEmpInfo.custInfoSex FROM tbEmpInfo INNER JOIN tbCustomerDBInfo on tbEmpInfo.empID=tbCustomerDBInfo.custID;
+------------------------+--------------+-------------+
| custInfoCriminalRecord | custInfoName | custInfoSex |
+------------------------+--------------+-------------+
| yes                    | Sean         | Male        |
| yes                    | James        | Male        |
| no                     | Janice       | Female      |
+------------------------+--------------+-------------+
```
### this snippet matches the ID's in both tables up. tbEmpInfo.empID=tbCustomerDBInfo.custID; where the empID matches the custID
```
FROM tbEmpInfo(LEFT TABLE) INNER JOIN tbCustomerDBInfo(RIGT TABLE)
```
#### WHAT TO JOIN --- SELECT TABLES TO JOIN ---- JOIN ON THE FIELD THAT I INDICATE

### Union
```
mysql> select * from tbCustomerDBInfo order by custInfoName ASC limit 3;
+--------+--------------+------------------+---------------+---------------+------------------+----------------+------------------+---------------+
| custID | custInfoName | custInfoLastName | custInfoAddr1 | custInfoAddr2 | custInfoCityName | custInfoCounty | custInfoPostcode | custInfoPhone |
+--------+--------------+------------------+---------------+---------------+------------------+----------------+------------------+---------------+
|      2 | James        | Cook             | NULL          | NULL          | London           | NULL           | NULL             | NULL          |
|      3 | Janice       | Gandolfino       | NULL          | NULL          | London           | NULL           | NULL             | NULL          |
|      1 | Sean         | McGuigan         | NULL          | NULL          | London           | NULL           | NULL             | NULL          |
+--------+--------------+------------------+---------------+---------------+------------------+----------------+------------------+---------------+

mysql> select * from tbCustomerDBInfo order by custInfoName DESC limit 3;
+--------+--------------+------------------+---------------+---------------+------------------+----------------+------------------+---------------+
| custID | custInfoName | custInfoLastName | custInfoAddr1 | custInfoAddr2 | custInfoCityName | custInfoCounty | custInfoPostcode | custInfoPhone |
+--------+--------------+------------------+---------------+---------------+------------------+----------------+------------------+---------------+
|      1 | Sean         | McGuigan         | NULL          | NULL          | London           | NULL           | NULL             | NULL          |
|      3 | Janice       | Gandolfino       | NULL          | NULL          | London           | NULL           | NULL             | NULL          |
|      2 | James        | Cook             | NULL          | NULL          | London           | NULL           | NULL             | NULL          |

```
