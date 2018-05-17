Cloud Provider : Amazon AWS

REDhat 7.4

172.31.14.52 ip-172-31-14-52.ap-southeast-1.compute.internal
172.31.9.52 ip-172-31-9-52.ap-southeast-1.compute.internal
172.31.10.42 ip-172-31-10-42.ap-southeast-1.compute.internal
172.31.9.235 ip-172-31-9-235.ap-southeast-1.compute.internal
172.31.3.76 ip-172-31-3-76.ap-southeast-1.compute.internal

[root@ip-172-31-14-52 yum.repos.d]# df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2       50G  1.8G   49G   4% /
devtmpfs        7.8G     0  7.8G   0% /dev
tmpfs           7.8G     0  7.8G   0% /dev/shm
tmpfs           7.8G   17M  7.8G   1% /run
tmpfs           7.8G     0  7.8G   0% /sys/fs/cgroup
tmpfs           1.6G     0  1.6G   0% /run/user/1000



[root@ip-172-31-14-52 yum.repos.d]# yum repolist enabled
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
cloudera-director                                                         |  951 B  00:00:00
cloudera-manager                                                          |  951 B  00:00:00
rhui-REGION-client-config-server-7                                        | 2.9 kB  00:00:00
rhui-REGION-rhel-server-releases                                          | 3.5 kB  00:00:00
rhui-REGION-rhel-server-rh-common                                         | 3.8 kB  00:00:00
(1/2): cloudera-director/primary                                          | 2.5 kB  00:00:00
(2/2): cloudera-manager/primary                                           | 4.3 kB  00:00:00
cloudera-director                                                                            5/5
cloudera-manager                                                                             7/7
repo id                                          repo name                                 status
cloudera-director                                Cloudera Director                              5
cloudera-manager                                 Cloudera Manager                               7
rhui-REGION-client-config-server-7/x86_64        Red Hat Update Infrastructure 2.0 Client       1
rhui-REGION-rhel-server-releases/7Server/x86_64  Red Hat Enterprise Linux Server 7 (RPMs)  20,399
rhui-REGION-rhel-server-rh-common/7Server/x86_64 Red Hat Enterprise Linux Server 7 RH Comm    231
repolist: 20,643


	
	

	 	
	   