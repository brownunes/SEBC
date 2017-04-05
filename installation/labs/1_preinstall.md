SYSTEM CONFIGURATION CHECKS
A – CHECK SWAPPINESS
sudo bash -c "echo 'vm.swappiness = 1' >> /etc/sysctl.conf"
[root@bootcamp01 brownunes]# sudo sysctl -p
net.ipv6.conf.all.disable_ipv6 = 1
vm.swappiness = 1
fs.file-max = 6544018
vm.swappiness = 15
vm.swappiness = 1

B – SHOW MOUNT ATTRIBUTES – ALL NODES HAVE THE SAME SET (XFS)

[root@bootcamp05 discos]# mount
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
devtmpfs on /dev type devtmpfs (rw,nosuid,size=7593092k,nr_inodes=1898273,mode=755)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,mode=755)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,mode=755)
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,xattr,release_agent=/usr/lib/systemd/systemd-cgroups-agent,name=systemd)
pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)
cgroup on /sys/fs/cgroup/pids type cgroup (rw,nosuid,nodev,noexec,relatime,pids)
cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,cpuacct,cpu)
cgroup on /sys/fs/cgroup/net_cls,net_prio type cgroup (rw,nosuid,nodev,noexec,relatime,net_prio,net_cls)
cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,perf_event)
cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,cpuset)
cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,freezer)
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,memory)
cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,blkio)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)
cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,hugetlb)
configfs on /sys/kernel/config type configfs (rw,relatime)
/dev/xvda2 on / type xfs (rw,relatime,attr2,inode64,noquota)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=26,pgrp=1,timeout=300,minproto=5,maxproto=5,direct)
debugfs on /sys/kernel/debug type debugfs (rw,relatime)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime)
mqueue on /dev/mqueue type mqueue (rw,relatime)
tmpfs on /run/user/1000 type tmpfs (rw,nosuid,nodev,relatime,size=1497260k,mode=700,uid=1000,gid=1000)
/dev/xvdb1 on /discos/disco1 type xfs (rw,noatime,attr2,inode64,noquota)

C – DISABLE TRANSPARENT HUGEPAGE SUPPORT
nano /etc/rc.local
echo never > /sys/kernel/mm/transparent_hugepage/defrag
chmod +x /etc/rc.local
reboot

# nano /boot/grub/grub.conf
...
03-bf61-2ee88aa54dbf console=hvc0 LANG=en_US.UTF-8
        initrd /boot/initramfs-3.10.0-514.el7.x86_64.img

transparent_hugepage=never

D - LIST YOUR NETWORK INTERFACE CONFIGURATION

Define o caminho dos clusters 
sudo su
nano /etc/hosts
#SEBC Cluster
172.31.42.126	bootcamp01.ec2.internal bootcamp01
172.31.37.238	bootcamp02.ec2.internal bootcamp02
172.31.46.112	bootcamp03.ec2.internal bootcamp03
172.31.37.170	bootcamp04.ec2.internal bootcamp04
172.31.43.214	bootcamp05.ec2.internal bootcamp05

Desabilita o IPV6
nano /etc/sysctl.conf
net.ipv6.conf.all.disable_ipv6 = 1
vm.swappiness = 1


E - SHOW CORRECT FORWARD AND REVERSE HOST LOOKUPS

•	FOR /ETC/HOSTS, USE GETENT

[ec2-user@bootcamp01 ~]$ getent hosts
127.0.0.1       localhost localhost.localdomain localhost4 localhost4.localdomain4
127.0.0.1       localhost localhost.localdomain localhost6 localhost6.localdomain6
172.31.42.126   bootcamp01.ec2.internal bootcamp01
172.31.37.238   bootcamp02.ec2.internal bootcamp02
172.31.46.112   bootcamp03.ec2.internal bootcamp03
172.31.37.170   bootcamp04.ec2.internal bootcamp04
172.31.43.214   bootcamp05.ec2.internal bootcamp05

•	FOR DNS, USE NSLOOKUP
[ec2-user@bootcamp01 ~]$ nslookup
> ^C[ec2-user@bootcamp01 ~]$ nslookup 54.175.1.180
Server:         172.31.0.2
Address:        172.31.0.2#53

Non-authoritative answer:
180.1.175.54.in-addr.arpa       name = ec2-54-175-1-180.compute-1.amazonaws.com.

[ec2-user@bootcamp01 ~]$ nslookup 52.91.64.232
Server:         172.31.0.2
Address:        172.31.0.2#53

Non-authoritative answer:
232.64.91.52.in-addr.arpa       name = ec2-52-91-64-232.compute-1.amazonaws.com.

[ec2-user@bootcamp01 ~]$ nslookup 52.91.207.254
Server:         172.31.0.2
Address:        172.31.0.2#53

Non-authoritative answer:
254.207.91.52.in-addr.arpa      name = ec2-52-91-207-254.compute-1.amazonaws.com.

[ec2-user@bootcamp01 ~]$ nslookup 54.164.21.230
Server:         172.31.0.2
Address:        172.31.0.2#53

Non-authoritative answer:
230.21.164.54.in-addr.arpa      name = ec2-54-164-21-230.compute-1.amazonaws.com

[ec2-user@bootcamp01 ~]$ nslookup 54.164.163.7
Server:         172.31.0.2
Address:        172.31.0.2#53

Non-authoritative answer:
7.163.164.54.in-addr.arpa       name = ec2-54-164-163-7.compute-1.amazonaws.com.

F - SHOW THE NSCD SERVICE IS RUNNING
[ec2-user@bootcamp01 ~]$ service nscd status
Redirecting to /bin/systemctl status  nscd.service
? nscd.service - Name Service Cache Daemon
   Loaded: loaded (/usr/lib/systemd/system/nscd.service; enabled; vendor preset: disabled)
   Active: active (running) since Tue 2017-04-04 23:09:09 EDT; 21min ago

G - SHOW THE NTPD SERVICE IS RUNNING (RUNNING CHRONYD INSTEAD)
[ec2-user@bootcamp01 ~]$ service chronyd status
Redirecting to /bin/systemctl status  chronyd.service
? chronyd.service - NTP client/server
   Loaded: loaded (/usr/lib/systemd/system/chronyd.service; enabled; vendor preset: enabled)
   Active: active (running) since Tue 2017-04-04 23:09:09 EDT; 30min ago
