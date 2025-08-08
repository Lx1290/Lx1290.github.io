## POST请求

```
curl -H "Content-Type: application/json" -X POST -d '{"key":"value"}' http://api.cloud.sci99.com/infoitem-es/es/info/separateSearch
```

## GET请求

```
curl "http://api.cloud.sci99.com/infoitem-es/es/info/separateSearch"
```

## restart脚本

```
#!/bin/bash

JAR_NAME="your-application.jar"  # 修改为你的JAR文件名

# 停止服务
kill $(ps -ef | grep "$JAR_NAME" | grep -v grep | awk '{print $2}') 2>/dev/null

# 等待2秒确保进程释放资源
sleep 2

# 启动服务
nohup j/path/to/java -jar "$JAR_NAME" > run.log 2>&1 &

echo "Restarted $JAR_NAME"
```