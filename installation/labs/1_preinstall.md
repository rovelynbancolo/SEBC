nano /etc/sysctl.conf
   vm.swappiness=1
   service network restart
   verification : cat /proc/sys/vm/swappiness
   **verify this***


Show the mount attributes of your volume(s)
# lsblk
	NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
	xvda    202:0    0  30G  0 disk
	└─xvda1 202:1    0  30G  0 part /


3. List the reserve space
	If you have ext-based volumes, list the reserve space setting
	XFS volumes do not support reserve space

	[root@cmserver centos]# df -h
		Filesystem      Size  Used Avail Use% Mounted on
		/dev/xvda1       30G  1.5G   29G   5% /
		devtmpfs        7.8G     0  7.8G   0% /dev
		tmpfs           7.8G     0  7.8G   0% /dev/shm
		tmpfs           7.8G   17M  7.8G   1% /run
		tmpfs           7.8G     0  7.8G   0% /sys/fs/cgroup
		tmpfs           1.6G     0  1.6G   0% /run/user/1000
		
	[root@cmserver centos]# mount | grep /dev/xvda1
		/dev/xvda1 on / type xfs (rw,relatime,seclabel,attr2,inode64,noquota)

    **Not applicable xfs file system**
	
4. Disable transparent hugepage support

Disable Transparent hugepage:
    #echo never > /sys/kernel/mm/transparent_hugepage/enabled
    #echo never > /sys/kernel/mm/transparent_hugepage/defrag

Verification:
	#cat /sys/kernel/mm/transparent_hugepage/defrag
		always madvise [never]	
	#cat /sys/kernel/mm/transparent_hugepage/enabled
		always madvise [never]


5. List your network interface configuration
	
[root@cmserver centos]# ifconfig
ens3: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 172.31.0.136  netmask 255.255.240.0  broadcast 172.31.15.255
        inet6 fe80::47:10ff:fecb:af5e  prefixlen 64  scopeid 0x20<link>
        ether 02:47:10:cb:af:5e  txqueuelen 1000  (Ethernet)
        RX packets 2811  bytes 269005 (262.7 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 2342  bytes 278475 (271.9 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 6  bytes 416 (416.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 6  bytes 416 (416.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

[root@cmserver centos]# cat /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6


6. Show that forward and reverse host lookups are correctly resolved
For /etc/hosts, use getent
For DNS, use nslookup

	# nslookup master
		Server:         172.31.0.2
		Address:        172.31.0.2#53
		
	# nslookup cloudera.com
	    Server:         172.31.0.2
		Address:        172.31.0.2#53

		Non-authoritative answer:
		Name:   cloudera.com
		Address: 13.56.96.0
		Name:   cloudera.com
		Address: 52.8.3.138	
		
6. Show the nscd service is running
     # yum -y install nscd
     # systemctl enable nscd
     # systemctl start nscd
     # systemctl status nscd
	    ● nscd.service - Name Service Cache Daemon
		   Loaded: loaded (/usr/lib/systemd/system/nscd.service; enabled; vendor preset: disabled)
		   Active: active (running) since Mon 2018-05-14 17:27:32 UTC; 6s ago
		  Process: 13639 ExecStart=/usr/sbin/nscd $NSCD_OPTIONS (code=exited, status=0/SUCCESS)
		 Main PID: 13640 (nscd)
		   CGroup: /system.slice/nscd.service
		           └─13640 /usr/sbin/nscd

		May 14 17:27:32 master.cloudera.com nscd[13640]: 13640 monitoring directory `/e...)
		May 14 17:27:32 master.cloudera.com nscd[13640]: 13640 monitoring file `/etc/ho...)
		May 14 17:27:32 master.cloudera.com nscd[13640]: 13640 monitoring directory `/e...)
		May 14 17:27:32 master.cloudera.com nscd[13640]: 13640 monitoring file `/etc/re...)
		May 14 17:27:32 master.cloudera.com nscd[13640]: 13640 monitoring directory `/e...)
		May 14 17:27:32 master.cloudera.com nscd[13640]: 13640 monitoring file `/etc/se...)
		May 14 17:27:32 master.cloudera.com nscd[13640]: 13640 monitoring directory `/e...)
		May 14 17:27:32 master.cloudera.com nscd[13640]: 13640 disabled inotify-based m...y
		May 14 17:27:32 master.cloudera.com nscd[13640]: 13640 stat failed for file `/e...y
		May 14 17:27:32 master.cloudera.com systemd[1]: Started Name Service Cache Daemon.
		Hint: Some lines were ellipsized, use -l to show in full.

	 
7. Show the ntpd service is running