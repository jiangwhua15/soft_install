
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

#### 使用配置logstash

```bash
 # logstash 默认命令行目录
 /usr/share/logstash/bin/logstash
```
##### logstash 例子

```
# 创建 heartbeat.conf

[root@localhost elastic]# vim heartbeat.conf

input {
  heartbeat {
    interval => 10
    type => "heartbeat"
  }
}

output {
  stdout {
    codec => rubydebug
  }
}

[root@localhost elastic]# /usr/share/logstash/bin/logstash -f /home/elastic/heartbeat.conf

Using bundled JDK: /usr/share/logstash/jdk
OpenJDK 64-Bit Server VM warning: Option UseConcMarkSweepGC was deprecated in version 9.0 and will likely be removed in a future release.
WARNING: Could not find logstash.yml which is typically located in $LS_HOME/config or /etc/logstash. You can specify the path using --path.settings. Continuing using the defaults
Could not find log4j2 configuration at path /usr/share/logstash/config/log4j2.properties. Using default config which logs errors to the console
[INFO ] 2022-04-22 18:22:47.318 [main] runner - Starting Logstash {"logstash.version"=>"8.1.3", "jruby.version"=>"jruby 9.2.20.1 (2.5.8) 2021-11-30 2a2962fbd1 OpenJDK 64-Bit Server VM 11.0.14.1+1 on 11.0.14.1+1 +indy +jit [linux-x86_64]"}
[INFO ] 2022-04-22 18:22:47.324 [main] runner - JVM bootstrap flags: [-Xms1g, -Xmx1g, -XX:+UseConcMarkSweepGC, -XX:CMSInitiatingOccupancyFraction=75, -XX:+UseCMSInitiatingOccupancyOnly, -Djava.awt.headless=true, -Dfile.encoding=UTF-8, -Djruby.compile.invokedynamic=true, -Djruby.jit.threshold=0, -Djruby.regexp.interruptible=true, -XX:+HeapDumpOnOutOfMemoryError, -Djava.security.egd=file:/dev/urandom, -Dlog4j2.isThreadContextMapInheritable=true, --add-opens=java.base/java.security=ALL-UNNAMED, --add-opens=java.base/java.io=ALL-UNNAMED, --add-opens=java.base/java.nio.channels=ALL-UNNAMED, --add-opens=java.base/sun.nio.ch=ALL-UNNAMED, --add-opens=java.management/sun.management=ALL-UNNAMED]
[WARN ] 2022-04-22 18:22:47.848 [LogStash::Runner] multilocal - Ignoring the 'pipelines.yml' file because modules or command line options are specified
[INFO ] 2022-04-22 18:22:50.105 [Api Webserver] agent - Successfully started Logstash API endpoint {:port=>9600, :ssl_enabled=>false}
[INFO ] 2022-04-22 18:22:51.255 [Converge PipelineAction::Create<main>] Reflections - Reflections took 149 ms to scan 1 urls, producing 120 keys and 419 values 
[INFO ] 2022-04-22 18:22:52.111 [Converge PipelineAction::Create<main>] javapipeline - Pipeline `main` is configured with `pipeline.ecs_compatibility: v8` setting. All plugins in this pipeline will default to `ecs_compatibility => v8` unless explicitly configured otherwise.
[INFO ] 2022-04-22 18:22:52.389 [[main]-pipeline-manager] javapipeline - Starting pipeline {:pipeline_id=>"main", "pipeline.workers"=>1, "pipeline.batch.size"=>125, "pipeline.batch.delay"=>50, "pipeline.max_inflight"=>125, "pipeline.sources"=>["/home/elastic/heartbeat.conf"], :thread=>"#<Thread:0x5ed43d0a run>"}
[INFO ] 2022-04-22 18:22:53.536 [[main]-pipeline-manager] javapipeline - Pipeline Java execution initialization time {"seconds"=>1.14}
[INFO ] 2022-04-22 18:22:53.673 [[main]-pipeline-manager] javapipeline - Pipeline started {"pipeline.id"=>"main"}
[INFO ] 2022-04-22 18:22:53.758 [Agent thread] agent - Pipelines running {:count=>1, :running_pipelines=>[:main], :non_running_pipelines=>[]}
{
          "host" => {
        "name" => "localhost.localdomain"
    },
      "@version" => "1",
    "@timestamp" => 2022-04-22T10:22:53.814617Z,
          "type" => "heartbeat",
       "message" => "ok"
}




```
