redisCluster-monitor
---------

Base [redis-monitor](https://github.com/LittlePeng/redis-monitor)

说明：项目只支持RedisCluster,且RedisCluster没有设置密码。
     redis-monitor项目在我们项目的集群环境上部署不成功。
     该项目加入了RedisCluster API的支持
     该项目是调试成功后的初版

## Features:
*  cluster: support thousands of redis instances
*  light: redis info base
*  metrics: memory, comands, Key HitRate, keyspace, master-slave change, expire keys
*  notification API: crash, master-slave stats changed notify

## Configuration
vim src/redis_live.conf

config：

- RedisStatsServer: stats storage backend(redis)
- others: config on dashboard settings tab

samples:
```
{"master_slave_sms": "1,1",
 "RedisStatsServer": {"port": 6379, "server": "127.0.0.1"},
 "sms_alert": "192.168.110.207:9999", //改配置项暂时没有使用到，可以先随意配置
 "DataStoreType": "redis",
  "RedisServers": [
  {"instance": "Master1", "group": "Test1", "port": 6379, "server": "127.0.0.1"},
  {"instance": "Slave1", "group": "Test1", "port": 6380, "server": "127.0.0.1"}
]}

```

## Install Deps
    pip install -r requirements.txt

## Run
    # 1. start redisCluster instance for stat stroage
    redis-server --port 6379

    # 2. start web portal
    cd src/
    python redis_live.py
    
    # 3. start stats collector daemon process
    cd src/
    python redis_monitor.py 

    # 4. dashboard: http://127.0.0.1:8888/index.html

 

