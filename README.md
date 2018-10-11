# example-nepxion-discovery-springcloud
example-nepxion-discovery-springcloud

# 环境说明
consul 服务注册中心

apollo 远程配置中心

Nepxion Discovery

# 第一步 拉去镜像，生成容器

https://github.com/foxiswho/docker-nginx-redis-mysql-rocketmq-rabbitmq-zookeeper

# 第二步 本地文件编译

克隆 https://github.com/Nepxion/Discovery

克隆完成后进入 `Discovery`目录，执行编译安装命令
> 这里主要 把包安装到本地库
```SHELL
mvn install
```

# 第三步 导入数据库

账号/密码: apollo/admin

Apollo（阿波罗）是携程框架部门研发的分布式配置中心，能够集中化管理应用不同环境、不同集群的配置，配置修改后能够实时推送到应用端，并且具备规范的权限、流程治理等特性，适用于微服务配置管理场景。

https://github.com/ctripcorp/apollo

如果要使用，请先 创建几个数据库 ，打开如下链接 创建数据库

https://github.com/ctripcorp/apollo/tree/master/scripts/sql

数据库库指导

https://github.com/ctripcorp/apollo/wiki/分布式部署指南#21-创建数据库


> 注意:
> 案例 使用的是dev 所以要创建库`ApolloConfigDBDev`，

把 SQL文件 
https://github.com/ctripcorp/apollo/blob/master/scripts/sql/apolloconfigdb.sql 
保存下来，
另存为 `apolloconfigdbDev.sql`文件，
修改`apolloconfigdbDev.sql`文件，内容部分修改
```SQL
CREATE DATABASE IF NOT EXISTS ApolloConfigDB DEFAULT CHARACTER SET = utf8mb4;

Use ApolloConfigDB;
```
修改为
```SQL
CREATE DATABASE IF NOT EXISTS ApolloConfigDBDev DEFAULT CHARACTER SET = utf8mb4;

Use ApolloConfigDBDev;
```

最后把这个文件导入 `ApolloConfigDBDev` 库 中，

# 第四步 克隆本案例


启动 

DiscoveryApplicationA1

DiscoveryApplicationB1

DiscoveryApplicationC1

其他Application启动，请自行启动

执行测试
```测试结果
curl -i -H Accept:application/json -X POST http://localhost:1100/invoke -H Content-Type: application/json -d '{"xxx":"xxxxx"}'
```
输出
```SHELL
{"xxx":"xxxxx"} -> discovery-springcloud-example-a[192.168.0.100:1100][V1.0][Region=dev] -> discovery-springcloud-example-b[192.168.0.100:1200][V1.0][Region=dev] -> discovery-springcloud-example-c[192.168.0.100:1300][V1.0][Region=dev]
```

# 第五步 请看官方说明

https://github.com/Nepxion/Discovery