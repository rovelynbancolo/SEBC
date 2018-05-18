hostname -f
ip-172-31-14-52.ap-southeast-1.compute.internal



[root@ip-172-31-14-52 /]# mysql -u root -padmin -e "status"
--------------
mysql  Ver 15.1 Distrib 5.5.56-MariaDB, for Linux (x86_64) using readline 5.1

Connection id:          11
Current database:
Current user:           root@localhost
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
Uptime:                 23 min 21 sec

Threads: 1  Questions: 34  Slow queries: 0  Opens: 1  Flush tables: 2  Open tables: 2               7  Queries per second avg: 0.024


mysql -u root -padmin -e "show databases"
+--------------------+
| Database           |
+--------------------+
| information_schema |
| hive               |
| hue                |
| mysql              |
| oozie              |
| performance_schema |
| rman               |
| scm                |
| sentry             |
+--------------------+