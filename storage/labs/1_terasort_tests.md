1 - create an end-user Linux account named with your GitHub handle 
useradd brownunes
[brownunes@bootcamp01 ~]$ whoami
brownunes

2 - Create a home HDFS directory for this user as well
sudo -u hdfs <command>
[brownunes@bootcamp01 ~]$ sudo -u hdfs hadoop fs -mkdir /user/brownunes
[brownunes@bootcamp01 ~]$ 

3 - Create a 10 GB file using teragen
VAI PARA - cd /opt/cloudera/parcels/CDH/jars
hadoop jar hadoop-examples.jar teragen -D dfs.block.size=33554432 100000000 /user/brownunes/terasort-input

time = 96,13s

[brownunes@bootcamp01 /]$ hadoop fs -ls /user/brownunes
Found 2 items
drwx------   - brownunes hadoop          0 2017-04-04 14:37 /user/brownunes/.staging
drwxr-xr-x   - brownunes hadoop          0 2017-04-04 14:37 /user/brownunes/terasort-input

4 - Run the terasort command on this file 

cd /opt/cloudera/parcels/CDH/jars
hadoop jar hadoop-examples.jar terasort /user/brownunes/terasort-input /user/brownunes/terasort-output

Time = 5.3m

[brownunes@bootcamp01 jars]$ hadoop fs -ls /user/brownunes
Found 3 items
drwx------   - brownunes hadoop          0 2017-04-04 14:57 /user/brownunes/.staging
drwxr-xr-x   - brownunes hadoop          0 2017-04-04 14:37 /user/brownunes/terasort-input
drwxr-xr-x   - brownunes hadoop          0 2017-04-04 14:57 /user/brownunes/terasort-output
