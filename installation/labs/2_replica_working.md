MARIADB INSTALLATION (CMSERVER)

	# yum -y install mariadb-server
	# systemctl start mariadb
	# chkconfig mariadb on
	# mkdir /mysql_backup
	# mv /var/lib/mysql/ib_* /mysql_backup/
	# mysql_secure_installation
	    
		    Enter current password for root (enter for none):
		    Set root password? [Y/n] y
		    New password:
		    Re-enter new password:
		    Remove anonymous users? [Y/n] Y
		    Disallow root login remotely? [Y/n] N
		    Remove test database and access to it [Y/n] Y
		    Reload privilege tables now? [Y/n] Y
		    All done!

	# nano /etc/my.cnf (pasted this setting suggested by the cloudera documentation)

	      	transaction-isolation = READ-COMMITTED
			key_buffer = 16M
			key_buffer_size = 32M
			max_allowed_packet = 32M
			thread_stack = 256K
			thread_cache_size = 64
			query_cache_limit = 8M
			query_cache_size = 64M
			query_cache_type = 1

			max_connections = 550
			#expire_logs_days = 10
			#max_binlog_size = 100M

			#log_bin should be on a disk with enough free space. Replace '/var$
			#and chown the specified folder to the mysql user.
			#added the following except log_bin, change binlog_format=row
			log_bin=/var/lib/mysql/mysql_binary_log


			read_buffer_size = 2M
			read_rnd_buffer_size = 16M
			sort_buffer_size = 8M
			join_buffer_size = 8M    


	        # InnoDB settings
			innodb_file_per_table = 1
			innodb_flush_log_at_trx_commit  = 2
			innodb_log_buffer_size = 64M
			innodb_buffer_pool_size = 4G
			innodb_thread_concurrency = 8
			innodb_flush_method = O_DIRECT
			innodb_log_file_size = 512M


	# systemctl restart mariadb;


<---START OF THE REPLICATION CONFIGURATION(MASTER)--->

	1. Enable Binary Logging and adding the binding address(added to my.cnf of CMSERVER(MASTER))
	        log_bin=/var/lib/mysql/mysql_binary_log
	        binlog_format=row
	        log_base=master1
			bind-address=cmserver.cloudera.com

	2. Setting up a Server_ID (added to my.cnf of CMSERVER(MASTER)		
			server-id=1
			
	3. Restart mariadb
	       # systemctl restart mariadb

	4. Slaves will need to connect and start the replicating from the server. Granting user permission to replicate
	      # mysql -u root -p
	      Password:

	      #GRANT REPLICATION SLAVE ON *.* TO 'root'@'master.cloudera.com' identified by 'admin';
	      
	      #FLUSH PRIVILEGES

	5. Flush and lock all running tables by runnning

	      #FLUSH TABLES WITH READ LOCK;

	6. Check if BINARY LOGGING IS WORKING

	      # show binary logs;

			+--------------------+-----------+
			| Log_name           | File_size |
			+--------------------+-----------+
			| master1-bin.000001 |       423 |
			| master1-bin.000002 |       245 |
			+--------------------+-----------+

	7. DISPLAY THE MASTER STATUS

	      #SHOW MASTER STATUS;
	        
	        +--------------------+----------+--------------+------------------+
			| File               | Position | Binlog_Do_DB | Binlog_Ignore_DB |
			+--------------------+----------+--------------+------------------+
			| master1-bin.000003 |      245 |              |                  |
			+--------------------+----------+--------------+------------------+
	      
	      #exit;

	8. Since I created the SCM first. I need to backup that db and copy it the slave node.
	   Note that i did include the pemfile in order to copy in AWS but i immediatly removed it after
	      
	      #mysqldump -u root -p scm > /mysql_backup/scmdb_backup.sql
	      #scp pemfile /mysql_backup/scmdb_backup.sql centos@ec2-13-229-233-106.ap-southeast-1.compute.amazonaws.com:/home/centos

	9. Login to mysql again and unlock the tables.
	      #mysql -u root -p
	      #UNLOCK TABLES;
	      #EXIT;


MARIADB-INSTALLATION (SLAVE)
 
  1. Followed the same steps on MARIADB INSTALLATION (CMSERVER)
 
<---START OF THE REPLICATION CONFIGURATION(SLAVE)--->
 
  2. Enable Binary Logging and adding the binding address(added to my.cnf of CMSERVER(MASTER))
	        log_bin=/var/lib/mysql/mysql_binary_log
	        binlog_format=row

  3. Setting up a Server_ID (added to my.cnf of SLAVE		
			server-id=2
			
  4. Restart mariadb
	       # systemctl restart mariadb

  5. Load the data scmdb_backup.sql that I copied from CMSERVER/MASTER to this MARIADB Server.
      # mysql -u root -p
	      mysql > CREATE DATABASE scm DEFAULT CHARACTER SET UTF8;
	      mysql > GRANT ALL ON scm.* TO 'scm'@'%' identified by 'scm';
	      mysql > FLUSH PRIVILEGES
	      mysql > exit
      # mysql -u root -p scm < /home/centos/scmdb_backup.sql

  6. Logback-in to mysql
     # mysql -u root -p
	      mysql > CHANGE MASTER TO MASTER_HOST='cmserver.cloudera.com', MASTER_PORT=3306, MASTER_USER='root', MASTER_PASSWORD='admin',  MASTER_LOG_FILE='master1-bin.000003', MASTER_LOG_POS=245;
	      mysql > START SLAVE;
	      mysql > SHOW SLAVE STATUS \G;

                 *************************** 1. row ***************************
					               Slave_IO_State: Waiting for master to send event
					                  Master_Host: cmserver.cloudera.com
					                  Master_User: root
					                  Master_Port: 3306
					                Connect_Retry: 60
					              Master_Log_File: master1-bin.000003
					          Read_Master_Log_Pos: 359
					               Relay_Log_File: mariadb-relay-bin.000004
					                Relay_Log_Pos: 645
					        Relay_Master_Log_File: master1-bin.000003
					             Slave_IO_Running: Yes
					            Slave_SQL_Running: Yes
					              Replicate_Do_DB:
					          Replicate_Ignore_DB:
					           Replicate_Do_Table:
					       Replicate_Ignore_Table:
					      Replicate_Wild_Do_Table:
					  Replicate_Wild_Ignore_Table:
					                   Last_Errno: 0
					                   Last_Error:
					                 Skip_Counter: 0
					          Exec_Master_Log_Pos: 359
					              Relay_Log_Space: 1227
					              Until_Condition: None
					               Until_Log_File:
					                Until_Log_Pos: 0
					           Master_SSL_Allowed: No
					           Master_SSL_CA_File:
					           Master_SSL_CA_Path:
					              Master_SSL_Cert:
					            Master_SSL_Cipher:
					               Master_SSL_Key:
					        Seconds_Behind_Master: 0
					Master_SSL_Verify_Server_Cert: No
					                Last_IO_Errno: 0
					                Last_IO_Error:
					               Last_SQL_Errno: 0
					               Last_SQL_Error:
					  Replicate_Ignore_Server_Ids:
					             Master_Server_Id: 1
					1 row in set (0.00 sec)




<--------------------VEFICATION IF REPLICATION IS WORKING------------------------>
 1. CREATE A PROJDB DATABASE AND MASTER AND IT AUTOMATICALLY REFLECTS IN SLAVE.

 

    
