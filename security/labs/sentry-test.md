Verify user privileges
#beeline   
# !connect 'jdbc:hive2://ip-172-31-0-136.ap-southeast-1.compute.internal:10000/;principal=hive/ip-172-31-0-136.ap-southeast-1.compute.internal@CLOUDERA.COM'
0: jdbc:hive2://ip-172-31-0-136.ap-southeast-> show databases;

kinit as george, then login to beeline
[rovy@ip-172-31-0-136 logs]$ kinit george@CLOUDERA.COM
Password for george@CLOUDERA.COM:
[rovy@ip-172-31-0-136 logs]$ klist
Ticket cache: FILE:/tmp/krb5cc_1002
Default principal: george@CLOUDERA.COM

Valid starting Expires Service principal
05/17/2018 04:34:45 05/18/2018 04:34:45 krbtgt/CLOUDERA.COM@CLOUDERA.COM

#beeline

!connect 'jdbc:hive2://ip-172-31-0-136.ap-southeast-1.compute.internal:10000/default;principal=hive/ip-172-31-0-136.ap-southeast-1.compute.internal@CLOUDERA.COM'

0: jdbc:hive2://ip-172-31-0-136.ap-southeast-> show tables;
INFO : Compiling command(queryId=hive_20180517043939_fa110382-da27-474f-ac90-95960923d267): show tables
INFO : Semantic Analysis Completed
INFO : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO : Completed compiling command(queryId=hive_20180517043939_fa110382-da27-474f-ac90-95960923d267); Time taken: 0.049 seconds
INFO : Executing command(queryId=hive_20180517043939_fa110382-da27-474f-ac90-95960923d267): show tables
INFO : Starting task [Stage-0:DDL] in serial mode
INFO : Completed executing command(queryId=hive_20180517043939_fa110382-da27-474f-ac90-95960923d267); Time taken: 0.115 seconds
INFO : OK
+------------+--+
| tab_name |
+------------+--+
| sample_07 |
| sample_08 |
+------------+--+
2 rows selected (0.207 seconds)
0: jdbc:hive2://ip-172-31-0-136.ap-southeast->

[rovy@ip-172-31-0-136 logs]$ kinit ferdinand@CLOUDERA.COM
Password for ferdinand@CLOUDERA.COM:
[rovy@ip-172-31-0-136 logs]$ klist
Ticket cache: FILE:/tmp/krb5cc_1002
Default principal: ferdinand@CLOUDERA.COM

Valid starting Expires Service principal
05/17/2018 04:41:17 05/18/2018 04:41:17 krbtgt/CLOUDERA.COM@CLOUDERA.COM
[rovy@ip-172-31-0-136 logs]$ beeline

show tables;

+------------+--+
| tab_name |
+------------+--+
| sample_07 |
+------------+--+



