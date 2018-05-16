Terasort Command
#sudo -u hdfs hdfs dfs -mkdir /user/rovy

##time sudo -u  hdfs hadoop jar  /opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce/hadoop-examples.jar teragen -Dmapred.map.tasks=4 -Ddfs.block.size=33554432 100000000 /user/Dzndrx/teragen

real    1m55.879s
user    0m7.912s
sys     0m0.448s

drwxr-xr-x   - hdfs supergroup          0 2018-05-16 03:27 /user/rovy/teragen
[root@ip-172-31-0-136 mysql]# hdfs dfs -ls /user/rovy/teragen
Found 5 items
-rw-r--r--   3 hdfs supergroup          0 2018-05-16 03:27 /user/rovy/teragen/_SUCCESS
-rw-r--r--   3 hdfs supergroup 2500000000 2018-05-16 03:27 /user/rovy/teragen/part-m-00000
-rw-r--r--   3 hdfs supergroup 2500000000 2018-05-16 03:27 /user/rovy/teragen/part-m-00001
-rw-r--r--   3 hdfs supergroup 2500000000 2018-05-16 03:27 /user/rovy/teragen/part-m-00002
-rw-r--r--   3 hdfs supergroup 2500000000 2018-05-16 03:27 /user/rovy/teragen/part-m-00003

Run the Terasort Command:
# time sudo -u hdfs hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar terasort /home/centos /home/centos/

real    4m25.312s
user    0m10.457s
sys     0m0.562s

[root@ip-172-31-0-136 mysql]# hdfs dfs -ls /user/rovy
Found 2 items
drwxr-xr-x   - hdfs supergroup          0 2018-05-16 03:27 /user/rovy/teragen
drwxr-xr-x   - hdfs supergroup          0 2018-05-16 03:35 /user/rovy/terasort

-rw-r--r--   1 hdfs supergroup          0 2018-05-16 03:35 /user/rovy/terasort/_SUCCESS
-rw-r--r--  10 hdfs supergroup         55 2018-05-16 03:31 /user/rovy/terasort/_partition.lst
-rw-r--r--   1 hdfs supergroup 1666405600 2018-05-16 03:35 /user/rovy/terasort/part-r-00000
-rw-r--r--   1 hdfs supergroup 1675282100 2018-05-16 03:35 /user/rovy/terasort/part-r-00001
-rw-r--r--   1 hdfs supergroup 1652233700 2018-05-16 03:35 /user/rovy/terasort/part-r-00002
-rw-r--r--   1 hdfs supergroup 1656208800 2018-05-16 03:35 /user/rovy/terasort/part-r-00003
-rw-r--r--   1 hdfs supergroup 1672771000 2018-05-16 03:35 /user/rovy/terasort/part-r-00004
-rw-r--r--   1 hdfs supergroup 1677098800 2018-05-16 03:35 /user/rovy/terasort/part-r-00005