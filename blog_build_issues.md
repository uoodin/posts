---
title: "搭建Blog以及持续集成遇到的一些问题"
date: 2021-03-14
publishdate: 2021-03-14
lastmod: 2021-03-14
draft: false
tags: ["website"]
---

### Nginx
   - 403 Forbidden
      - static文件权限如何处理?
   - 404 Page not found
      - root,location是怎样匹配的?
   - HTTPS配置
      - 私钥pem,key文件配置
      - 80跳转443
      
### Docker
   - DockerFile,DockerCompose的使用
   - 不同实例间为什么ping不通?
   	- DockerService的使用
   	
### 持续集成
   - 编写Deploy脚本
      - golang execute command 路径如何写? 
      - 怎么让指定目录git pull
      - shell脚本权限,如何处理 exit status 255
    - webhook
      - 如何用jobs,bg,nohup等命令执行后台任务
      ```
      nohup webhook -hooks hooks.json -verbose > webhook.log &
      ```
      - webhook如何指定SSL私钥访问，防止被刷接口
      - shell脚本权限 chmod a+x sync.sh
      
### Git
   - 如何管理多个ssh key?



