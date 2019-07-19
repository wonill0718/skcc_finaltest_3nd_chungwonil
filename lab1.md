# 1. Create a CDH Cluster on AWS

## Create a password for user 'centos'
sudo passwd centos

```
[centos@ip-172-31-39-204 ~]$ sudo passwd centos
Changing password for user centos.
New password:
BAD PASSWORD: The password is shorter than 8 characters
Retype new password:
passwd: all authentication tokens updated successfully.
[centos@ip-172-31-39-204 ~]$
```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/1.passwd_centos.PNG"></img>

## Modify sshd_config to allow password login
sudo vi /etc/ssh/sshd_config
패스워드 인증 허용

```
.....
sudo vi /etc/ssh/sshd_config
	change ->
PasswordAuthentication yes
sudo systemctl restart sshd.service
....
```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/2.use_passwd_for_centos.PNG"></img>

## a. Linux setup
### i. Add the following linux accounts to all nodes
#### 1. User training with a UID of 3800
```
sudo useradd training -u 3800
```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/6.create_user_training.PNG"></img>

#### 2. Set the password for user “training” to “training”
```
sudo passwd training
```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/5.set_passwd_for_training.PNG"></img>

#### 3. Create the group skcc and add training to it
```
sudo groupadd skcc
sudo usermod -a -G skcc training
```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/7.create_group_and_add_training.PNG"></img>

#### 4. Give training sudo capabilities
```
sudo gpasswd -a training wheel
```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/8.%20give_training_sudo_capabilities.PNG"></img>

### ii. List the your instances by IP address and DNS name
```
sudo vi /etc/hosts
```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/3.%20etc_hosts_setup.PNG"></img>

```
sudo hostnamectl set-hostname m1.skcc.com
```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/4.change_hostname.PNG"></img>

### iii. List the Linux release you are using
```
hostname -f
```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/11.%20hostname_check.PNG"></img>

### iv. List the file system capacity for the first node
### v. List the command and output for yum repolist enabled
```
yum list installed
```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/10.%20yum_list.PNG"></img>

### vi. List the /etc/passwd entries for training
```
ii. 참고
```

### vii. List the /etc/group entries for skcc
```
viii. 참고
```

### viii. List output of the flowing commands
```
getent group skcc
getent passwd training
```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/9.%20getent_group_skcc_and_passwd_training.PNG"></img>

## b. Install a MySQl server
### i. Use MariaDB as the database for all the services
```
sudo yum install -y wget
```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/12.yul_install_wget.PNG"></img>

```
sudo yum install -y java-1.8.0-openjdk-devel.x86_64
```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/13.%20install_openjdk1.8.PNG"></img>

```
sudo yum install -y mariadb-server
sudo systemctl enable mariadb
sudo systemctl start mariadb
sudo /usr/bin/mysql_secure_installation
```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/14.install_mariadb_and_secure_installation.PNG"></img>

### ii. List the following in your GitHub
#### 1. A command and output that shows the hostname of your database server
```
hostname -f
mysql --version
```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/17.%20show_hostname_and_database_server.PNG"></img>

#### 2. A command and output that reports the database server version
```
mysql --version
```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/15.mysql_version.PNG"></img>

#### A command and output that lists all the databases in the server
```
show databases;
```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/16.show_databases.PNG"></img>

## c. Install Cloudera Manager
```
sudo wget https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/cloudera-manager.repo \
-P /etc/yum.repos.d/
```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/18.PNG"></img>

### i. Specifically, you MUST install CDH version 5.15.2
```
cd /etc/yum.repos.d/
sudo vi cloudera-manager.repo
    -> baseurl=https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5.15.2/
```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/19.PNG"></img>

```
sudo rpm --import https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera
sudo yum install -y cloudera-manager-daemons cloudera-manager-server
```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/20.PNG"></img>

### iii. Make sure that the following services
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/22.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/23.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/24.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/25.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/26.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/27.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/29.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/30.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/31.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/32.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/33.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/34.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/35.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/36.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/37.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/38.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/39.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/40.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/41.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/42.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/43.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/44.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/45.PNG"></img>

# 2. In MySQL create the sample tables that will be used for the rest of the test
## a. In MySQL, create a database and name it “test”
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/28.PNG"></img>

## b. Create 2 tables in the test databases: authors and posts
```
DROP TABLE IF EXISTS `authors`;
CREATE TABLE `authors` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `first_name` varchar(50) COLLATE utf8_unicode_ci NOT NULL,
  `last_name` varchar(50) COLLATE utf8_unicode_ci NOT NULL,
  `email` varchar(100) COLLATE utf8_unicode_ci NOT NULL,
  `birthdate` date NOT NULL,
  `added` timestamp NOT NULL DEFAULT current_timestamp(),
  PRIMARY KEY (`id`),
  UNIQUE KEY `email` (`email`)
) ENGINE=InnoDB AUTO_INCREMENT=10001 DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;


DROP TABLE IF EXISTS `posts`;
CREATE TABLE `posts` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `author_id` int(11) NOT NULL,
  `title` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `description` varchar(500) COLLATE utf8_unicode_ci NOT NULL,
  `content` text COLLATE utf8_unicode_ci NOT NULL,
  `date` date NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=110001 DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/46.mysql_use_test_show_tables.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/47.insert_authors_table.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/48.insert_post_table.PNG"></img>

## c. Create and grant user “training” with password “training” full access to the test database.
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/21.mysql_training_user_create.PNG"></img>

# 3. Extract tables authors and posts from the database and create Hive tables.
```
[centos@ip-172-31-41-17 ~]$ su - training
Password:
[training@cm ~]$ pwd
/home/training
[training@cm ~]$ sqoop import --connect jdbc:mysql://cm:3306/test \
--username training \
-P \
--split-by id \
--columns id,first_name,last_name,email,birthdate,added \
--table authors \
--fields-terminated-by "\t" \
--hive-import \
--create-hive-table \
--hive-table test.authors

sqoop import --connect jdbc:mysql://cm:3306/test \
--username training \
-P \
--split-by id \
--columns id,author_id,title,description,content,date \
--table posts \
--fields-terminated-by "\t" \
--hive-import \
--create-hive-table \
--hive-table test.posts
```
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/49.%20sqoop%20import%20mysql%20to%20hive.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/50.hive%20select.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/51.%20hive_create_table_select_insert_result.PNG"></img>
<img src="https://github.com/wonill0718/skcc_finaltest_3nd_chungwonil/blob/master/png/52.%20hive_select_result.PNG"></img>

# 4. Create and run a Hive/Impala query. From the query, generate the results dataset that
```
CREATE EXTERNAL TABLE results (
	  id 		int, 	  
	  fname string, 
	  lname string, 
	  num_posts int)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '\t;';

INSERT OVERWRITE TABLE results 
select b.author_id as id,
    a.first_name fname,
    a.last_name lname,
    count(*) num_posts
from authors a, posts b
where a.id = b.id
group by b.author_id, a.first_name, a.last_name;

select * from results limit 10;
```

# 5. Export the data from above query to MySQL
```
sqoop export --connect jdbc:mysql://cm:3306/test \
--username training \
-P \
--split-by id \
--columns id,fname,lname,num_posts \
--table results \
--fields-terminated-by "\t" \
--hive-import \
--create-hive-table \
--hive-table test.posts
```
