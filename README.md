# 读写分离配置

```
docker pull mysql:5.7

docker run -d -e MYSQL_ROOT_PASSWORD=123456 --name mysql-master  -v d:/documents/project/mysql-docker/mysql-master:/var/lib/mysql -v d:/documents/project/mysql-docker/my-master.cnf:/etc/mysql/my.cnf -p 3306:3306 mysql:5.7

docker run -d -e MYSQL_ROOT_PASSWORD=123456 --name mysql-slave1  -v d:/documents/project/mysql-docker/mysql-slave1:/var/lib/mysql -v d:/documents/project/mysql-docker/my-slave1.cnf:/etc/mysql/my.cnf -p 3307:3306 mysql:5.7
```

cat /etc/hosts

master:
```sql
	grant replication slave on *.* to 'slave'@'%' identified by 'slave';
	flush privileges;
	show master status;
```
slave:
```sql
	change master to master_host='172.17.0.2',master_user='slave',master_password='slave',
master_log_file='mysql-bin.000004',master_log_pos=1160,master_port=3306;
	start slave;
	show slave status\G
```