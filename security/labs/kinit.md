#kadmin -p admin/admin
#listprincs
kadmin.local:  listprins
kadmin.local: Unknown request "listprins".  Type "?" for a request list.
kadmin.local:  listprincs
HTTP/ip-172-31-0-136.ap-southeast-1.compute.internal@CLOUDERA.COM
HTTP/ip-172-31-11-104.ap-southeast-1.compute.internal@CLOUDERA.COM
HTTP/ip-172-31-12-166.ap-southeast-1.compute.internal@CLOUDERA.COM
HTTP/ip-172-31-15-3.ap-southeast-1.compute.internal@CLOUDERA.COM
HTTP/ip-172-31-3-221.ap-southeast-1.compute.internal@CLOUDERA.COM
K/M@CLOUDERA.COM
admin/admin@CLOUDERA.COM
ferdinand@CLOUDERA.COM
george@CLOUDERA.COM
hdfs/ip-172-31-0-136.ap-southeast-1.compute.internal@CLOUDERA.COM
hdfs/ip-172-31-11-104.ap-southeast-1.compute.internal@CLOUDERA.COM
hdfs/ip-172-31-12-166.ap-southeast-1.compute.internal@CLOUDERA.COM
hdfs/ip-172-31-15-3.ap-southeast-1.compute.internal@CLOUDERA.COM
hdfs/ip-172-31-3-221.ap-southeast-1.compute.internal@CLOUDERA.COM
hdfs@CLOUDERA.COM
hive/ip-172-31-0-136.ap-southeast-1.compute.internal@CLOUDERA.COM
hive/ip-172-31-3-221.ap-southeast-1.compute.internal@CLOUDERA.COM
hue/ip-172-31-0-136.ap-southeast-1.compute.internal@CLOUDERA.COM
hue/ip-172-31-3-221.ap-southeast-1.compute.internal@CLOUDERA.COM
kadmin/admin@CLOUDERA.COM

 # addprinc george@CLOUDERA.COM
 # addprinc ferdinand@CLOUDERA.COM
 # addprinc rovy@CLOUDERA.COM
 # addprinc root@CLOUDERA.COM
 # addprinc hdfs@CLOUDERA.COM
 
[rovy@ip-172-31-0-136 ~]kinit rovy@CLOUDERA.COM 

[root@ip-172-31-0-136 krb5kdc]# kinit rovy@CLOUDERA.COM
Password for rovy@CLOUDERA.COM:
[root@ip-172-31-0-136 krb5kdc]# klist
Ticket cache: FILE:/tmp/krb5cc_0
Default principal: rovy@CLOUDERA.COM

Valid starting       Expires              Service principal
05/16/2018 18:03:27  05/17/2018 18:03:27  krbtgt/CLOUDERA.COM@CLOUDERA.COM
[root@ip-172-31-0-136 krb5kdc]#
 