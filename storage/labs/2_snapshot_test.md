hadoop fs -mkdir /user/brownunes/precious

[brownunes@bootcamp01 ~]$ hadoop fs -ls /user/brownunes
Found 4 items
drwx------   - brownunes hadoop          0 2017-04-04 14:57 /user/brownunes/.staging
drwxr-xr-x   - brownunes hadoop          0 2017-04-04 15:23 /user/brownunes/precious

[brownunes@bootcamp01 ~]$ hadoop fs -put SEBC-master.zip /user/brownunes/precious
[brownunes@bootcamp01 ~]$ hadoop fs -ls /user/brownunes/precious
Found 1 items
-rw-r--r--   3 brownunes hadoop     473950 2017-04-04 15:53 /user/brownunes/precious/SEBC-master.zip


•	Delete the directory
•	Delete the ZIP file
[root@bootcamp01 brownunes]# hadoop fs -ls /user/brownunes/precious
Found 1 items
-rw-r--r--   3 brownunes hadoop     473950 2017-04-04 15:53 /user/brownunes/precious/SEBC-master.zip

[brownunes@bootcamp01 ~]$ hadoop fs -rm /user/brownunes/precious/SEBC-master.zip

17/04/04 20:59:56 INFO fs.TrashPolicyDefault: Moved: 'hdfs://bootcamp01.ec2.internal:8020/user/brownunes/precious/SEBC-master.zip' to trash at: hdfs://bootcamp01.ec2.internal:8020/user/brownunes/.Trash/Current/user/brownunes/precious/SEBC-master.zip

[brownunes@bootcamp01 ~]$ hadoop fs -ls /user/brownunes/precious
[brownunes@bootcamp01 ~]$

AFTER SNAPSHOT:
[brownunes@bootcamp01 ~]$ hadoop fs -ls /user/brownunes/precious
Found 1 items
-rw-r--r--   3 hdfs hadoop     473950 2017-04-04 21:04 /user/brownunes/precious/SEBC-master.zip
