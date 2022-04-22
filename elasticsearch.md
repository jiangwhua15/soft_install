
#### Docker-composer 安装 Elasticsearch

```
# 使用docker-compose.yml 安装

docker-compose up -d

```


#### 安装Logstash

 ```
 # 安装 mysql 连接器
 
 [root@localhost elastic]# wget https://repo1.maven.org/maven2/mysql/mysql-connector-java/8.0.28/mysql-connector-java-8.0.28.jar
 
 
 # 安装Yum 源
 [root@localhost elastic]# sudo rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch

# Add the following in your /etc/yum.repos.d/ directory in a file with a .repo suffix, for example logstash.repo

[logstash-8.x]
name=Elastic repository for 8.x packages
baseurl=https://artifacts.elastic.co/packages/8.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md


# 安装
[root@localhost elastic]# yum install logstash


 
 
 ```
