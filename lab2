part2
1.

use problem1;

select a.id, a.type, a.status, a.amount, 
(b.average - a.amount) as difference
from account a
join
(select type, avg(amount) as average from account
where status = "Active"
group by type) b
on (a.type = b.type)
where status = "Active";




hive -f solution.sql



2.

create database problem2;

use problem2;

CREATE EXTERNAL TABLE employee(
 id 		int,
 fname 		string,
 lname		string,
 address 	string,
 city 		string,
 state 		string,
 zip		string,
 birthday	string,
 hireday	string
)  
row format delimited 
fields terminated by ','
location 'hdfs://localhost:8020/user/training/problem2/data/employee';


3.

CREATE EXTERNAL TABLE solution(
custid              	string,
fname               	string,              	                    
lname               	string,              	                    
hphone              	string  
)  
row format delimited 
fields terminated by ','
location 'hdfs://localhost:8020/user/training/problem3/data/solution';


insert into table solution
select a.custid, c.fname , c.lname, c.hphone
from account a 
    ,customer c
where a.amount < 0.0 
and a.custid = c.id;


4.

create problem4;

use problem4;


CREATE EXTERNAL TABLE employee1 (
id string,
fname string,
lname string,
address string,
city string,
state string,
zip string
) 
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '\t;'
LOCATION 'hdfs://localhost:8020/user/training/problem4/data/employee1';

select * from employee1 limit 10;



CREATE EXTERNAL TABLE employee2 (
id string,
num string,
lname string,
fname string,
address string,
city string,
state string,
zip string
) 
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
LOCATION 'hdfs://localhost:8020/user/training/problem4/data/employee2';



CREATE EXTERNAL TABLE solution (
id string,
fname string,
lname string,
address string,
city string,
state string,
zip string
) 
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '\t;'
LOCATION 'hdfs://localhost:8020/user/training/problem4/solution';

INSERT OVERWRITE TABLE solution
select * from (
select id, initcap(fname), initcap(lname), address, city, state, substr(zip, 1, 5) as zip
from employee1 a where a.state = 'CA'
union all
select id, initcap(fname), initcap(lname), address, city, state, substr(zip, 1, 5) as zip
from employee2 b where b.state = 'CA'
) ab ;

select * from solution limit 10;


5.

CREATE EXTERNAL TABLE solution (
fname string,
lname string,
city string,
state string
) 
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '\t;'
LOCATION 'hdfs://localhost:8020/user/training/problem5/solution'
;

INSERT OVERWRITE TABLE solution
Select fname,lname, city, state 
from customer 
where  city = 'Palo Alto'
and state = 'CA'
union all
select fname,lname, city, state
from employee
where  city = 'Palo Alto'
and state = 'CA'
;

select * from solution limit 10;


6.

CREATE EXTERNAL TABLE solution (
	  id 		int, 	  
	  fname string, 
	  lname string, 
	  address string, 
	  city string, 
	  state string, 
	  zip string, 
	  birthday string)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '\t;'
LOCATION	  'hdfs://localhost:8020/user/training/problem6/solution';

INSERT OVERWRITE TABLE solution 
select id,
    fname,
    lname,
    address,
    city,
    state,
    zip,
    substr(birthday, 1,5)
from employee;

select * from solution limit 10;


7.

select concat(fname," ", lname) as name 
from employee 
where city = 'Seattle' 
order by name asc;


8.

8-1. data export

[training@localhost problem1]$ sqoop export --connect jdbc:mysql://localhost/problem8 --username cloudera --password cloudera --table solution --export-dir hdfs://localhost:8020/user/training/problem8/data/customer --input-fields-terminated-by '\t'
19/07/19 00:46:29 INFO sqoop.Sqoop: Running Sqoop version: 1.4.6-cdh5.8.0
19/07/19 00:46:29 WARN tool.BaseSqoopTool: Setting your password on the command-line is insecure. Consider using -P instead.
19/07/19 00:46:29 INFO manager.MySQLManager: Preparing to use a MySQL streaming resultset.
19/07/19 00:46:29 INFO tool.CodeGenTool: Beginning code generation
19/07/19 00:46:29 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `solution` AS t LIMIT 1
19/07/19 00:46:29 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `solution` AS t LIMIT 1
19/07/19 00:46:29 INFO orm.CompilationManager: HADOOP_MAPRED_HOME is /usr/lib/hadoop-mapreduce
Note: /tmp/sqoop-training/compile/1a6d753099e0dbcd32e888d63ea6a059/solution.java uses or overrides a deprecated API.
Note: Recompile with -Xlint:deprecation for details.
19/07/19 00:46:32 INFO orm.CompilationManager: Writing jar file: /tmp/sqoop-training/compile/1a6d753099e0dbcd32e888d63ea6a059/solution.jar
19/07/19 00:46:32 INFO mapreduce.ExportJobBase: Beginning export of solution
19/07/19 00:46:32 INFO Configuration.deprecation: mapred.job.tracker is deprecated. Instead, use mapreduce.jobtracker.address
19/07/19 00:46:32 INFO Configuration.deprecation: mapred.jar is deprecated. Instead, use mapreduce.job.jar
19/07/19 00:46:32 INFO Configuration.deprecation: mapred.map.max.attempts is deprecated. Instead, use mapreduce.map.maxattempts
19/07/19 00:46:33 INFO Configuration.deprecation: mapred.reduce.tasks.speculative.execution is deprecated. Instead, use mapreduce.reduce.speculative
19/07/19 00:46:33 INFO Configuration.deprecation: mapred.map.tasks.speculative.execution is deprecated. Instead, use mapreduce.map.speculative
19/07/19 00:46:33 INFO Configuration.deprecation: mapred.map.tasks is deprecated. Instead, use mapreduce.job.maps
19/07/19 00:46:34 INFO client.RMProxy: Connecting to ResourceManager at /0.0.0.0:8032
19/07/19 00:46:35 WARN hdfs.DFSClient: Caught exception 
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeInternal(DFSOutputStream.java:830)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:826)
19/07/19 00:46:35 WARN hdfs.DFSClient: Caught exception 
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.endBlock(DFSOutputStream.java:600)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:789)
19/07/19 00:46:35 WARN hdfs.DFSClient: Caught exception 
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.endBlock(DFSOutputStream.java:600)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:789)
19/07/19 00:46:35 WARN hdfs.DFSClient: Caught exception 
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.endBlock(DFSOutputStream.java:600)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:789)
19/07/19 00:46:35 WARN hdfs.DFSClient: Caught exception 
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.endBlock(DFSOutputStream.java:600)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:789)
19/07/19 00:46:35 WARN hdfs.DFSClient: Caught exception 
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.endBlock(DFSOutputStream.java:600)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:789)
19/07/19 00:46:35 WARN hdfs.DFSClient: Caught exception 
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeInternal(DFSOutputStream.java:830)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:826)
19/07/19 00:46:35 WARN hdfs.DFSClient: Caught exception 
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.endBlock(DFSOutputStream.java:600)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:789)
19/07/19 00:46:35 WARN hdfs.DFSClient: Caught exception 
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.endBlock(DFSOutputStream.java:600)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:789)
19/07/19 00:46:35 WARN hdfs.DFSClient: Caught exception 
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.endBlock(DFSOutputStream.java:600)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:789)
19/07/19 00:46:35 WARN hdfs.DFSClient: Caught exception 
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeInternal(DFSOutputStream.java:830)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:826)
19/07/19 00:46:35 WARN hdfs.DFSClient: Caught exception 
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.endBlock(DFSOutputStream.java:600)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:789)
19/07/19 00:46:35 WARN hdfs.DFSClient: Caught exception 
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.endBlock(DFSOutputStream.java:600)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:789)
19/07/19 00:46:35 WARN hdfs.DFSClient: Caught exception 
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.endBlock(DFSOutputStream.java:600)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:789)
19/07/19 00:46:36 WARN hdfs.DFSClient: Caught exception 
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeInternal(DFSOutputStream.java:830)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:826)
19/07/19 00:46:36 WARN hdfs.DFSClient: Caught exception 
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeInternal(DFSOutputStream.java:830)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:826)
19/07/19 00:46:36 WARN hdfs.DFSClient: Caught exception 
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeInternal(DFSOutputStream.java:830)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:826)
19/07/19 00:46:36 WARN hdfs.DFSClient: Caught exception 
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1245)
	at java.lang.Thread.join(Thread.java:1319)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:862)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeInternal(DFSOutputStream.java:830)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:826)
19/07/19 00:46:36 INFO input.FileInputFormat: Total input paths to process : 1
19/07/19 00:46:36 INFO input.FileInputFormat: Total input paths to process : 1
19/07/19 00:46:36 INFO mapreduce.JobSubmitter: number of splits:4
19/07/19 00:46:36 INFO Configuration.deprecation: mapred.map.tasks.speculative.execution is deprecated. Instead, use mapreduce.map.speculative
19/07/19 00:46:36 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1563509164339_0013
19/07/19 00:46:36 INFO impl.YarnClientImpl: Submitted application application_1563509164339_0013
19/07/19 00:46:37 INFO mapreduce.Job: The url to track the job: http://localhost:8088/proxy/application_1563509164339_0013/
19/07/19 00:46:37 INFO mapreduce.Job: Running job: job_1563509164339_0013
19/07/19 00:46:45 INFO mapreduce.Job: Job job_1563509164339_0013 running in uber mode : false
19/07/19 00:46:45 INFO mapreduce.Job:  map 0% reduce 0%
19/07/19 00:47:03 INFO mapreduce.Job:  map 100% reduce 0%
19/07/19 00:47:04 INFO mapreduce.Job: Job job_1563509164339_0013 completed successfully
19/07/19 00:47:04 INFO mapreduce.Job: Counters: 30
	File System Counters
		FILE: Number of bytes read=0
		FILE: Number of bytes written=571200
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=18887
		HDFS: Number of bytes written=0
		HDFS: Number of read operations=19
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=0
	Job Counters 
		Launched map tasks=4
		Data-local map tasks=4
		Total time spent by all maps in occupied slots (ms)=132908
		Total time spent by all reduces in occupied slots (ms)=0
		Total time spent by all map tasks (ms)=66454
		Total vcore-seconds taken by all map tasks=66454
		Total megabyte-seconds taken by all map tasks=34024448
	Map-Reduce Framework
		Map input records=100
		Map output records=100
		Input split bytes=676
		Spilled Records=0
		Failed Shuffles=0
		Merged Map outputs=0
		GC time elapsed (ms)=889
		CPU time spent (ms)=2120
		Physical memory (bytes) snapshot=477360128
		Virtual memory (bytes) snapshot=9048907776
		Total committed heap usage (bytes)=251920384
	File Input Format Counters 
		Bytes Read=0
	File Output Format Counters 
		Bytes Written=0
19/07/19 00:47:04 INFO mapreduce.ExportJobBase: Transferred 18.4443 KB in 30.9412 seconds (610.4152 bytes/sec)
19/07/19 00:47:04 INFO mapreduce.ExportJobBase: Exported 100 records.


8-2. show mysql table data
[training@localhost problem1]$ mysql -u training -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 703
Server version: 5.1.73 Source distribution

Copyright (c) 2000, 2013, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> use problem8;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> show tables;
+--------------------+
| Tables_in_problem8 |
+--------------------+
| solution           |
+--------------------+
1 row in set (0.00 sec)

mysql> select * from solution limit 10;
+----------+--------+----------+--------------------------------+-------------+-------+-------+------------+
| id       | fname  | lname    | address                        | city        | state | zip   | birthday   |
+----------+--------+----------+--------------------------------+-------------+-------+-------+------------+
| 10000000 | Deanna | Lane     | 900-1514 Vitae, Rd.            | Lafayette   | LA    | 97827 | 08/31/2016 |
| 10000001 | Hall   | Garrett  | 9656 Urna Avenue               | Tucson      | AZ    | 86511 | 08/24/2016 |
| 10000002 | Lucian | Dotson   | P.O. Box 277, 4808 Fusce St.   | Seattle     | WA    | 57731 | 08/12/2016 |
| 10000003 | Yuri   | Sherman  | Ap #399-8275 Molestie Road     | Kapolei     | HI    | 16943 | 08/26/2016 |
| 10000004 | Jaime  | Griffin  | Ap #647-2123 Quis Rd.          | Madison     | WI    | 51394 | 08/13/2016 |
| 10000005 | Zorita | Weber    | 747-9424 Orci, Av.             | Hattiesburg | MS    | 90262 | 08/09/2016 |
| 10000006 | Mara   | Meadows  | 517-4594 Ac, Rd.               | Huntsville  | AL    | 35374 | 08/11/2016 |
| 10000007 | Evan   | Richard  | P.O. Box 223, 8182 Non, Av.    | College     | AK    | 99682 | 08/25/2016 |
| 10000008 | Briar  | Anderson | Ap #548-6452 Nunc Road         | Cleveland   | OH    | 90704 | 08/18/2016 |
| 10000009 | Cole   | Odom     | P.O. Box 962, 2496 Sodales St. | Boston      | MA    | 27282 | 08/21/2016 |
+----------+--------+----------+--------------------------------+-------------+-------+-------+------------+
10 rows in set (0.00 sec)

mysql> 







9.

CREATE EXTERNAL TABLE solution (
	id 		    string,
    fname 		string,
    lname		string,
    address 	string,
    city 		string,
    state 		string,
    zip		string,
    birthday	string )
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '\t;'
LOCATION 'hdfs://localhost:8020/user/training/problem9/solution';

INSERT OVERWRITE TABLE solution
select concat("A",id) as id
       , fname
       , lname
       ,address
       ,city
       ,state
       ,zip
       ,birthday
from customer;

select * from solution limit 10;



10.

CREATE EXTERNAL TABLE solution(
id int, 
fname string, 
lname string, 
city string, 
state string, 
charge double, 
billdate string
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '\t;'
LOCATION 'hdfs://localhost:8020/user/training/problem10/solution'
;

INSERT OVERWRITE TABLE solution
select c.id
     , c.fname
     , c.lname
     , c.city
     , c.state
     , b.charge
     , substr(b.tstamp, 1, 10) as billdata
from customer c
    ,billing b
where c.id = b.id;

select * from solution limit 10;
