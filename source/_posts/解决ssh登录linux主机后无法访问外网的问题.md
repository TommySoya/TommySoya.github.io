---
title: 解决ssh登录linux主机后无法访问外网的问题
date: 2023-04-08 15:20:47
tags: 技术总结
---
**简言之：我忘了export代理环境变量了**
```shell
vim /etc/profile

# http_proxy
export http_proxy=http://127.0.0.1:7890
export https_proxy=http://127.0.0.1:7890

# 保存后
source /etc/profile
```