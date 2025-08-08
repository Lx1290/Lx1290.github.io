### 查询每个key的占用情况脚本

```
for key in $(redis-cli --scan); do
  size=$(redis-cli MEMORY USAGE "$key")
  echo "$key => ${size} bytes"
done
```

### 登录redis

```
redis-cli -h <hot_node_ip> -p <hot_node_port> -a <密码>
```

### 查询redis的key

```
DBSIZE(快速获取当前数据库的键总数)

keys * (列出所有key)
```