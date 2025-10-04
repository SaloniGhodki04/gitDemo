

**clauses:**



**where clause**

**order by clause**

**group by clause**

**having clause**



**-----------------**

**order by clause:**

used for sorting data into the table

--->asc/dec



select * from student

order by name asc;



**--------------------------------------**



**distinct:**

used for avoiding duplications.



select distinct(city) from student_details;

**---------------------------------------**



**limit:**

select * from student limit 2;



bottom 2 records:



select * from student

order by id desc limit 2;



select * from student limit 2,2;



**-------------------------------------------**

**group by:**



select count(name) from student

group by city;

**--------------------------------------------**

**having clause:**

used to pass additional condtion on my records.



select city,count (*) from student

group by city

having count(*)>1;



**----------------------------------**



**1)match module:**



create table course(id int,name varchar(20),des varchar(300));



insert into course(id,name,des)values(1,DBMS','Database management system'),(2,'Java','App development');



alter table course

add fulltext(des);



select name,des from course where match(des) against('development');



**--------------------------------------------------**

**load file into normal cmd:**

When local_infile is ON (or =1), a client may execute LOAD DATA LOCAL INFILE 'file.csv' INTO TABLE ... and the server will accept the client-sent file contents and import them into a table. If local\_infile is OFF, LOAD DATA LOCAL INFILE will fail




Temporary (runtime) enable on server:

SET GLOBAL local_infile = 1;

---

**steps:**

copy that file

goto c drive-->programdata-->mysql-->mysqlserver-->uploads-->paste that file



Go to normal cmd:


1)MySQL -u root -p --local_infile=1

2)MySQL password:

3)set global local_infile=1;

4)use db;

5)create table batsman();


load data local infile " paste that file location from c drive / batsman.csv" 

  into table batsman

  fields terminated by ','

  lines terminated by '\n'

  ignore 1 rows;



select * from batsman;

---

User Creation:

Steps:

1)create database

2)use db

3)create table s_info(id int,name varchar(20),marks int);

insert

---

Create Users:

create user 'yashasvi1'@'localhost' identified by 'y1';
create user 'yashasvi2'
create user 'yashasvi3'
create user 'yashasvi4'



select user from MySQL.user

---

mysql> create user 'yashasvi1'@'localhost' identified by 'y1';

Query OK, 0 rows affected (0.229 sec)


mysql> create user 'namita'@'localhost' identified by 'n1';

Query OK, 0 rows affected (0.122 sec)


mysql> create user 'lata'@'localhost' identified by 'l1';

Query OK, 0 rows affected (0.060 sec)


mysql> create user 'tina'@'localhost' identified by 't1';

Query OK, 0 rows affected (0.129 sec)

mysql> -- create user 'user_name'@'localhost' identified by 'password'


select user from MySQL.user
---

Grant privileges:

grant insert on createdata.student to 'namita'@locahost;

grant update on createdata.student to 'lata'@localhost;

grant delete on createdata.student to 'tina'@localhost;

grant select on createdata.student to 'tinea'@localhost;

grant select on createdata.student to 'lata'@localhost;

grant select on createdata.student to 'namita'@localhost;

grant select on createdata.student to 'yashasvi1'@localhost;


---
To view all grants:
show grants;

show grants for 'username'@'localhost';

---

To remove permission:

revoke select on dbname.tablename  from 'yash1'@'localhost';



---

To change password:

alter user 'yash1'@'localhost' identified by 'y1';



---

To delete:

drop user 'yash1'@'localhost';

---

To grant all privileges:

Grant all privileges *.* to 'yash'@'localhost';


---


WINDOW FUNCTION:



used to perform calculations across set of table rows.

over()- clause:

defines the window/set of rows over which the function operates.



It include:

1)partition: divides the set into parts (groups)

along with order by.


employee table:

eid     ename     dname     salary


q)find the max salary earn by an employee:

select max(salary) from emp;


for each dept:

select max(salary) from emp group by dname;


Also with all details:
SELECT *,

       MAX(salary) OVER() AS max_salary

FROM emp e;


corresponding to each dept:

over(partition by dname);
---

row_number:

assign unique identifier/unique value:


select * , row_number() over() as uni_value  from emp;


q)Number based on diff dept:

select *,row_number() over(partition by dname) from emp;


Rank()

Assigns the **same rank** to rows **with equal values.**

**Skips the next rank(s) after a tie.**



q)fetch top 3 emp in each dept earning max salary:



select *,rank() over(order by salary desc) as rnk from emp;

 select *,rank() over(partition by deptname order by sal desc) as rnk from emp;

