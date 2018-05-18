ip-172-31-85-79.ec2.internal


[root@ip-172-31-85-79 centos]# mysql -u dbadmin -pdbpass -e "status;"
--------------
mysql  Ver 15.1 Distrib 5.5.56-MariaDB, for Linux (x86_64) using readline 5.1

Connection id:          10
Current database:
Current user:           dbadmin@localhost
SSL:                    Not in use
Current pager:          stdout
Using outfile:          ''
Using delimiter:        ;
Server:                 MariaDB
Server version:         5.5.56-MariaDB MariaDB Server
Protocol version:       10
Connection:             Localhost via UNIX socket
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    utf8
Conn.  characterset:    utf8
UNIX socket:            /var/lib/mysql/mysql.sock
Uptime:                 6 min 30 sec

Threads: 1  Questions: 39  Slow queries: 0  Opens: 1  Flush tables: 2  Open tables: 27  Queries per          second avg: 0.100



[root@ip-172-31-85-79 centos]# mysql -u dbadmin -pdbpass -e "show databases;"
+--------------------+
| Database           |
+--------------------+
| information_schema |
| hive               |
| hue                |
| oozie              |
| rman               |
| scm                |
| sentry             |
+--------------------+
