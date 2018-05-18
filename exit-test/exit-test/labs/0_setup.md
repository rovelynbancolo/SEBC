AWs

ec2-52-207-232-214.compute-1.amazonaws.com
ec2-35-173-245-239.compute-1.amazonaws.com
ec2-52-87-164-34.compute-1.amazonaws.com
ec2-52-201-216-87.compute-1.amazonaws.com
ec2-54-209-223-57.compute-1.amazonaws.com

03:07:58 up 28 min,  1 user,  load average: 0.00, 0.01, 0.04
03:08:49 up 29 min,  1 user,  load average: 0.00, 0.01, 0.05
 03:09:54 up 30 min,  1 user,  load average: 0.00, 0.01, 0.04
 03:10:22 up 30 min,  1 user,  load average: 0.00, 0.01, 0.04
 03:11:02 up 31 min,  1 user,  load average: 0.00, 0.01, 0.04
 
 CENTOS 7
 
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda1       50G  895M   50G   2% /
devtmpfs        7.8G     0  7.8G   0% /dev
tmpfs           7.8G     0  7.8G   0% /dev/shm
tmpfs           7.8G   17M  7.8G   1% /run
tmpfs           7.8G     0  7.8G   0% /sys/fs/cgroup
tmpfs           1.6G     0  1.6G   0% /run/user/1000
tmpfs           1.6G     0  1.6G   0% /run/user/0


yum repolist enabled
Loaded plugins: fastestmirror
Determining fastest mirrors
 * base: mirror.atlanticmetro.net
 * extras: centos.mirror.constant.com
 * updates: mirror.cs.pitt.edu
base                                                     | 3.6 kB     00:00
extras                                                   | 3.4 kB     00:00
updates                                                  | 3.4 kB     00:00
(1/4): extras/7/x86_64/primary_db                          | 125 kB   00:00
(2/4): updates/7/x86_64/primary_db                         | 1.0 MB   00:00
(3/4): base/7/x86_64/group_gz                              | 166 kB   00:00
(4/4): base/7/x86_64/primary_db                            | 5.9 MB   00:00
repo id                             repo name                             status
base/7/x86_64                       CentOS-7 - Base                       9,911
extras/7/x86_64                     CentOS-7 - Extras                       258
updates/7/x86_64                    CentOS-7 - Updates                      151
repolist: 10,320


yum repolist enabled
Loaded plugins: fastestmirror
Determining fastest mirrors
base: mirror.atlanticmetro.net
extras: centos.mirror.constant.com
updates: mirror.cs.pitt.edu
base | 3.6 kB 00:00
extras | 3.4 kB 00:00
updates | 3.4 kB 00:00
(1/4): extras/7/x86_64/primary_db | 125 kB 00:00
(2/4): updates/7/x86_64/primary_db | 1.0 MB 00:00
(3/4): base/7/x86_64/group_gz | 166 kB 00:00
(4/4): base/7/x86_64/primary_db | 5.9 MB 00:00
repo id repo name status
base/7/x86_64 CentOS-7 - Base 9,911
extras/7/x86_64 CentOS-7 - Extras 258
updates/7/x86_64 CentOS-7 - Updates 151
repolist: 10,320

31 groupadd blackorder
32 groupadd avengers
33 sudo useradd -u 2500 -g blackorder thanos
34 sudo useradd -u 2600 -g avengers hulk
35 sudo useradd -u 2700 -g avengers groot


thanos❌2500:1001::/home/thanos:/bin/bash
hulk❌2600:1002::/home/hulk:/bin/bash
groot❌2700:1002::/home/groot:/bin/bash
blackorder❌1001:
avengers❌1002: