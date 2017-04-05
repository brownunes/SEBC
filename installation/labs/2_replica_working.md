[ec2-user@bootcamp01 ~]$ service mysqld status
Redirecting to /bin/systemctl status  mysqld.service
Unit mysqld.service could not be found.
[ec2-user@bootcamp01 ~]$ service mariadb status
Redirecting to /bin/systemctl status  mariadb.service
? mariadb.service - MariaDB database server
   Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled; vendor preset: disabled)
   Active: active (running) since Tue 2017-04-04 23:09:19 EDT; 41min ago

MariaDB [(none)]> create database amon DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> create database rman DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> create database metastore DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> create database sentry DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> create database nav DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> create database navms DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> create database oozie DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

Hue criado...
grant all privileges on hive.* to 'hive'@'localhost' identified by 'hive';
grant all privileges on oozie.* to 'oozie'@'%' identified by 'oozie';

grant all privileges on hue.* to 'hue'@'localhost' identified by 'hue';

grant all privileges on rman.* to 'rman'@'%' identified by 'rman';

grant all privileges on hive.* to 'hive'@'%' identified by 'hive';
MariaDB [(none)]> grant all privileges on oozie.* to 'oozie'@'localhost' identified by 'oozie';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> grant all privileges on oozie.* to 'oozie'@'%' identified by 'oozie';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> grant all privileges on amon.* to 'amon'@'localhost' identified by 'amon';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> grant all privileges on rman.* to 'rman'@'localhost' identified by 'rman';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> grant all privileges on metastore.* to 'metastore'@'localhost' identified by 'metastore';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> grant all privileges on sentry.* to 'sentry'@'localhost' identified by 'sentry';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> grant all privileges on nav.* to 'nav'@'localhost' identified by 'nav';  Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> grant all privileges on navms.* to 'navms'@'localhost' identified by 'navms';
Query OK, 0 rows affected (0.00 sec)
