---
title: 清理docker容器日志
date: 2023-03-06 21:23:13
tags: 技术总结
---
## 查看docker容器日志
```shell
#!/bin/sh

echo "======== docker containers logs file size ========"  

logs=$(find /var/lib/docker/containers/ -name *-json.log)  

for log in $logs  
        do  
             ls -lh $log   
        done  

```

给权限
```shell
# chmod +x docker_log_size.sh

# ./docker_log_size.sh

```
## 清理日志

```shell
#!/bin/sh 
  
echo "======== start clean docker containers logs ========"  
  
logs=$(find /var/lib/docker/containers/ -name *-json.log)  
  
for log in $logs  
        do  
                echo "clean logs : $log"  
                cat /dev/null > $log  
        done  

echo "======== end clean docker containers logs ========"  

```

赋予权限
```shell
# chmod +x clean_docker_log.sh

# ./clean_docker_log.sh
```


参考：
https://blog.csdn.net/yjk13703623757/article/details/80283729

