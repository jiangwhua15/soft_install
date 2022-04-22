
#### Docker-composer 安装 Elasticsearch

##### Step 1：docker启动elasticsearch

```
 [root@localhost elastic]# docker run -d --name es01 --net elastic -p 9200:9200 -p 9300:9300 -it elasticsearch:8.1.2
3e4bb6f3ae0ce1d771ab6c15e1cf3416c543f9635b2efea094bc15b3894b8d98

```
###### Setp2： 打开另外一个终端，进入Elasticsearch容器,并生成证书
```
# 进入容器
[root@localhost ~]# docker exec -it es01 /bin/bash

# 查看当前目录
elasticsearch@5c76f60793a1:~$ ls
LICENSE.txt  NOTICE.txt  README.asciidoc  bin  config  data  jdk  lib  logs  modules  plugins
elasticsearch@5c76f60793a1:~$ 


# 生成证书
elasticsearch@5c76f60793a1:~$ elasticsearch-certutil ca
This tool assists you in the generation of X.509 certificates and certificate
signing requests for use with SSL/TLS in the Elastic stack.

The 'ca' mode generates a new 'certificate authority'
This will create a new X.509 certificate and private key that can be used
to sign certificate when running in 'cert' mode.

Use the 'ca-dn' option if you wish to configure the 'distinguished name'
of the certificate authority

By default the 'ca' mode produces a single PKCS#12 output file which holds:
    * The CA certificate
    * The CA's private key

If you elect to generate PEM format certificates (the -pem option), then the output will
be a zip file containing individual files for the CA certificate and private key

Please enter the desired output file [elastic-stack-ca.p12]: 
Enter password for elastic-stack-ca.p12 : 
elasticsearch@5c76f60793a1:~$ ls
LICENSE.txt  NOTICE.txt  README.asciidoc  bin  config  data  elastic-stack-ca.p12  jdk  lib  logs  modules  plugins

```

##### Step3:退出容器
```
# 复制证书到 docker-composer.yml 所在目录
[root@localhost elastic]# docker cp es01:/usr/share/elasticsearch/elastic-stack-ca.p12 .
[root@localhost elastic]# ls
config  data  docker-compose.yml  elastic-stack-ca.p12  logs  plugins

# 停止并且销毁容器
[root@localhost elastic]# docker stop es01
es01
[root@localhost elastic]# docker rm es01
es01

```


