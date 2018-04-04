# Docker ELK Example

### 简介

快速创建ELK metricbeat x-pack学习环境

> 目标

- build-compose快速部署
- 支持[DaoCloud Stack](http://guide.daocloud.io/dcs/%E9%83%A8%E7%BD%B2%E5%A4%8D%E6%9D%82%E7%9A%84%E5%A4%9A%E8%8A%82%E7%82%B9%E5%BE%AE%E6%9C%8D%E5%8A%A1%E5%BA%94%E7%94%A8-9153682.html)自动化部署
- Metricbeat System 监听
- Metricbeat Docker 监听
- Metricbeat Nginx 监听
- Metricbeat Mysql 监听
- Metricbeat Redis 监听
- Metricbeat NodeJs 监听
- Metricbeat Golang 监听
- Metricbeat Kubernetes 监听
- X-pack 权限解析
- ELK 集群

### 准备工具

 - [docker-compose](https://docs.docker.com/compose/install/#install-compose)

### 本地编译安装

```
$ git clone "https://github.com/wilfordw/docker-elk-example.git"
$ cd docker-elk-example
$ docker-compose up -d
```

### ~~DaoCloud Stack 自动化部署~~

> 开发测试阶段暂不提供 stack 脚本更新，包装完会整体更新

```
$ git clone "https://github.com/wilfordw/docker-elk-example.git"
$ cd docker-elk-example
$ pwd
```

~~把 dao-docker-compose.yml 内容复制进 Stack 的 YAML, 把上面克隆项目的 `pwd` 替换里面的 `/root/app/docker-elk/`, 点击部署就可以~~

> ~~想要自己创建镜像也可以，把你创建好的镜像地址替换 `yml` 里的 `image`~~

### 注意事项

#### Metricbeat

> Metricbeat System 监听 无法在 MacOS 或者 Win 上使用， 请关闭(进入 `./metricbeat/modules.d`， 修改 `system.yml` 为 `system.yml.disabled`)

#### Logstash

>  ~~Logstash 默认使用 x-pack 监听特性，在 kibana 编辑已注册 pipeline ID 的 pipeline。 ( 编辑位置 Kibana > Management > Pipelines )，初始化后必须先添加一个 pipeline 要不 Logstash 无法正常工作~~

>  ~~Logstash 要恢复默认配置，请修改~~

./logstash/conf/pipeline

```
- pipeline.id: main
   path.config: "/usr/share/logstash/pipeline"
```

./logstash/conf/logstash.yml

```
#xpack.management.enabled: true
#xpack.management.elasticsearch.url: "http://elasticsearch:9200/"
#xpack.management.elasticsearch.username: elastic
#xpack.management.elasticsearch.password: "123456"
#xpack.management.logstash.poll_interval: 5s
#xpack.management.pipeline.id: ["var.log.system","main"]
```

> 可以在 `./logstash/pipeline` 目录下新增自己的管道

#### 初始账户

> 初始账号 elastic 密码 123456 修改密码在 `docker-compose.yml` 里修改 `ELASTIC_PASSWORD: 123456`， 其他账号密码可在 kibana 里修改
> **初始密码修改后请同步修改 `./metricbeat/metricbeat.yml`*
```
output.elasticsearch:

  ...

  username: "elastic"
  password: "<your password>"
```



### Change List

- v1.1.1
  - 修复 redis 崩溃 bug

- v1.1.0
  - 暂时去除 DaoCloud Stack 脚本更新，专注 docker-compose
  - 新增 mariadb 监控支持
  - 新增 redis 监控支持
  - 新增 mariadb 慢查询日志分析
  - 恢复 logstash 默认设置，不再使用 x-pack management。

- v1.0.3
  - 去除 DaoCloud Stack 脚本 image 版本依赖 (默认 latest)

- v1.0.2
  - 新增 DaoCloud Stack 集成部署支持
  - nginx 监控

- v1.0.1

  - Kibana + Logstash + ElasticSearch + X-pack + Metricbeat docker-compose 构建 
  - metricbeat 实现系统监控


### TODO


- Metricbeat NodeJs 监听
- Metricbeat Golang 监听
- Metricbeat Kubernetes 监听
- X-pack 权限解析
- ELK 集群
- 新增 filebeat 支持