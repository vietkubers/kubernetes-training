# Linux Control Groups

### Contents

<!-- MarkdownTOC -->
[1. What's cgroups?](#-what-is-cgroups)  
[2. How to use cgroups?](#-how-to-use-cgroups)  
[3. Manual approach](#-manual-approach)  
[4. References](#-references)   
<!-- /MarkdownTOC -->

<a name="-what-is-cgroups"><a/>
### 1. What's cgroups?

`cgroups` stands for **Control Groups**, it's a feature of Linux kernel that allocates and isolates resources: CPU, memory, disk I/O and networking of one or more processes.  
The below figure shows the configurations of `cgroups` in Linux kernel:
![cgroups](images/cgroups-kernel.PNG)

The design of `cgroup` aims to provide a unified interface to manage processes or OS-level virtualization, including `Linux Containers` (LXC):
* **Resource limiting:** a group can be configured not to exceed a specified memory limit or use more than the desired amount of processors or be limited to specific peripheral devices. 
* **Prioritization:**  one or more groups may be configured to utilize fewer or more CPUs or disk I/O throughput. 
* **Accounting:** a group's resource usage is monitored and measured.
* **Control:** groups of processes can be frozen or stopped and restarted.

<a name="-how-to-use-cgroups"><a/>
### 2. How to use cgroups?

The user can access and manage cgroups directly and indirectly (with `LXC`, `libvirt` or `Docker`).  
Install the necessary packages:
```sh
$ sudo apt-get install libcgroup1 cgroup-tools
```
Now, the enabled `cgroups` can be seen via `proc filesystem` or `sysfs`:
```sh
$ cat /proc/cgroups

#subsys_name    hierarchy       num_cgroups     enabled
cpuset  9       2       1
cpu     4       134     1
cpuacct 4       134     1
blkio   7       134     1
memory  5       163     1
devices 11      134     1
freezer 2       2       1
net_cls 3       2       1
perf_event      10      2       1
net_prio        3       2       1
hugetlb 8       2       1
pids    6       136     1

$ ls -l /sys/fs/cgroup/

total 0
dr-xr-xr-x 6 root root  0 Nov 13 00:55 blkio
drwxr-xr-x 2 root root 60 Nov 13 01:00 cgmanager
lrwxrwxrwx 1 root root 11 Nov 13 00:55 cpu -> cpu,cpuacct
lrwxrwxrwx 1 root root 11 Nov 13 00:55 cpuacct -> cpu,cpuacct
dr-xr-xr-x 6 root root  0 Nov 13 00:55 cpu,cpuacct
dr-xr-xr-x 3 root root  0 Nov 13 00:55 cpuset
dr-xr-xr-x 6 root root  0 Nov 13 00:55 devices
dr-xr-xr-x 3 root root  0 Nov 13 00:55 freezer
dr-xr-xr-x 3 root root  0 Nov 13 00:55 hugetlb
dr-xr-xr-x 6 root root  0 Nov 13 00:55 memory
lrwxrwxrwx 1 root root 16 Nov 13 00:55 net_cls -> net_cls,net_prio
dr-xr-xr-x 3 root root  0 Nov 13 00:55 net_cls,net_prio
lrwxrwxrwx 1 root root 16 Nov 13 00:55 net_prio -> net_cls,net_prio
dr-xr-xr-x 3 root root  0 Nov 13 00:55 perf_event
dr-xr-xr-x 6 root root  0 Nov 13 00:55 pids
dr-xr-xr-x 6 root root  0 Nov 13 00:55 systemd
```
`cgroups` can be configured directly via the `sysfs`. For example, let's create a small bash script named **test_cgroups.sh** for demostration:
```sh
#!/bin/bash

while :
do
    echo "Print line" > /dev/tty
    sleep 5
done
```
Run above script:
```sh
$ sh test_cgroups.sh
Print line
Print line
Print line
...
...
```
Change directory to `/sys/fs/cgroup/devices` where `devices` represents kind of resources that allows or denies access to devices by tasks in a `cgroup`:
```sh
$ cd sys/fs/cgroup/devices
```
Then, create a directory `cgroups_test_group`:
```sh
# mkdir cgroups_test_group
```
After creation of the `cgroups_test_group` directory, the following files will be generated:
```sh
$ ls -l /sys/fs/cgroup/devices/cgroups_test_group

total 0
-rw-r--r-- 1 root root 0 Nov 16 02:05 cgroup.clone_children
-rw-r--r-- 1 root root 0 Nov 16 02:05 cgroup.procs
--w------- 1 root root 0 Nov 16 02:05 devices.allow
--w------- 1 root root 0 Nov 16 02:05 devices.deny
-r--r--r-- 1 root root 0 Nov 16 02:05 devices.list
-rw-r--r-- 1 root root 0 Nov 16 02:05 notify_on_release
-rw-r--r-- 1 root root 0 Nov 16 02:05 tasks
```
The `tasks` file contains PIDs (Process ID) of processes which will be attached to the `cgroups_test_group`, the 


<a name="-manual-approach"><a/>
### 3. Manual approach


<a name="-references"><a/>
### 4. References