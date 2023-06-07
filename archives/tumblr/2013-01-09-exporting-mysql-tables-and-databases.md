---
layout: post
title: Exporting MySQL tables and databases
date: '2013-01-09T14:24:48+05:30'
tags:
- dump
- export
- mysql
- mysqldump
- sql
tumblr_url: http://www.desinerd.com/post/150535103093/exporting-mysql-tables-and-databases
---
Here are the ways you can export tables and databases, each of them have their advantages and disadvantages depending on the task at hand. We will list out each with examples and discuss them.

We will assume that the database name is D and table name is T.
1.  Going native with SQL and generating an csv from the MySQL console
Assuming that you are already logged into your mysql console using say
mysql -u <user> -p <database>
replace <user> with your username
replace <database> with your database
You can use the following command to generate an csv of pretty much any SQL.

select * from T 
into outfile “
fields enclosed by ’”’
fields terminated by ’,’
lines terminated by ‘n’
where id=1;
One of the limitation is that you cannot get the column names in the csv using this.
2. You can use the mysqldump utility provided, to actually take an output of complete databases/tables or partial tables.
mysqldump -u <user> -p -t -T<location directory> –databases D –tables T –where=“id=1” –fields-enclosed-by=“ –fields-terminated-by=,
The above query will take the output of the Table T from Database D and generate a clean CSV in the location provided with the filename T.csv
The clear limitation as compared to 1 is that you cannot get output of joins and you do not get the column names in the csv.
3. You can now use the mysql commandline to output csv as well
mysql -u root -p D -e "select * from T where id=1” > T.csv

The above query will output the query results with the column names in row 0.
The limitation is that you cannot control the fields enclosed, fields terminated like 1 and 2.

No approach is better than others! For me 3 worked really well as I needed the column names and did not need a lot of control over the column attributes. You may find the other approaches work as well for you.
