
### Docker-composer 安装 Elasticsearch

#### Step 1：docker启动elasticsearch

```
 docker run --name es01 --net elastic -p 9200:9200 -p 9300:9300 -it elasticsearch:8.1.2
```
##### Setp2： 打开另外一个终端，进入Elasticsearch容器
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


