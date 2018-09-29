# lims2-deploy-doc

该文档用于说明如何部署 lims2 依赖的 docker 服务.

## 服务列表和版本

| 服务列表 | 版本 | dockerfile 地址 | 项目地址 | 七牛云镜像 |
| --------------------------------------- | ---------------------------: | ----------------------------------- | ----------------------------------- | ----------------------- |
| docker.genee.in/genee/lims2-env | v0.1.0-d2016051101 | https://bitbucket.org/genee-yiqikong/lims2-dockerimage-builder | https://bitbucket.org/genee-yiqikong/lims2-dockerimage-builder | http://od4jrri6r.bkt.clouddn.com/lims2-env.v0.1.0-d2016051101.tar.gz |
| docker.genee.in/genee/lims2 | v1.1.1-d2018011101 | https://github.com/HuangStomach/lims2-necessity	| https://github.com/HuangStomach/lims2-necessity | http://od4jrri6r.bkt.clouddn.com/lims2.v1.1.1-d2018011101.tar.gz |
| docker.genee.in/genee/cron-server | v1.2.0-d2018032801 | https://bitbucket.org/genee-yiqikong/cron-server | https://bitbucket.org/genee-yiqikong/cron-server | http://od4jrri6r.bkt.clouddn.com/cron-server.v1.2.0-d2018032801.tar.gz |
| docker.genee.in/genee/reserv-server | v0.4.3-d2017060101 | https://github.com/17kong/lims2-reserv-server | https://github.com/17kong/lims2-reserv-server | http://od4jrri6r.bkt.clouddn.com/reserv-server.v0.5.0-d2018011101.tar.gz |
| docker.genee.in/genee/lims2-backup-server | v0.1.1-d2015082701 | https://bitbucket.org/genee/lims2-backup | https://bitbucket.org/genee/lims2-backup |
| docker.genee.in/genee/debade-courier | v0.3.0-d2015122301 | https://github.com/iamfat/dockerfile-debade-courier | https://github.com/iamfat/debade-courier | http://od4jrri6r.bkt.clouddn.com/debade-courier.v0.3.0-d2015122301.tar.gz |
| docker.genee.in/genee/debade-trigger | v0.1.7-d20150820101 **注意, 此版本未正确按照 [docker-convention](https://github.com/genee-projects/docker-convention) 限定** | https://github.com/iamfat/dockerfile-debade-trigger | https://github.com/iamfat/debade-trigger | http://od4jrri6r.bkt.clouddn.com/debade-trigger.v0.1.7-d20150820101.tar.gz |
| docker.genee.in/genee/haikan-nvs | v1.2.3-d2018041801 | https://bitbucket.org/genee/genee-nvs | https://bitbucket.org/genee/genee-nvs | http://od4jrri6r.bkt.clouddn.com/haikan-nvs.v1.2.3-d2018041801.tar.gz |
| docker.genee.in/genee/tiandy-nvs | v1.2.1-d2015082701 | https://bitbucket.org/genee/genee-nvs | https://bitbucket.org/genee/genee-nvs | http://od4jrri6r.bkt.clouddn.com/tiandy-nvs.v1.2.1-d2015082701.tar.gz |
| docker.genee.in/genee/lims2-guard | v1.0.0-d2015081701 | https://bitbucket.org/genee/lims2-guard | https://bitbucket.org/genee/lims2-guard | 
| docker.genee.in/genee/crtmp-server | v0.716-d2015081701 | https://bitbucket.org/genee/dockerfile-crtmp | https://bitbucket.org/genee/dockerfile-crtmp | 
| docker.genee.in/genee/node-lims2 | v1.0.2-d2015081701 | https://bitbucket.org/genee/node-lims2 | https://bitbucket.org/genee/node-lims2 | http://od4jrri6r.bkt.clouddn.com/node-lims2.v2.0.1-d2017120801.tar.gz |
| docker.genee.in/genee/icco-server | v0.3.12-d2017042501 | https://bitbucket.org/genee/icco-server | https://bitbucket.org/genee/icco-server | http://od4jrri6r.bkt.clouddn.com/icco-server.v0.3.12-d2017042501.tar.gz |
| docker.genee.in/genee/cacs-server | v0.2.2-d2016081001 | https://bitbucket.org/genee/cacs-server | https://bitbucket.org/genee/cacs-server | http://od4jrri6r.bkt.clouddn.com/cacs-server.v0.2.2-d2016081001.tar.gz |
| docker.genee.in/genee/gdoor-server | v0.2.0-d2018042301 | https://bitbucket.org/genee/gdoor-server | https://bitbucket.org/genee/gdoor-server | http://od4jrri6r.bkt.clouddn.com/gdoor-server.v0.2.0-d2018030501.tar.gz |
| docker.genee.in/genee/glogon-server | v0.5.2-d2017093001 | https://bitbucket.org/genee/glogon-server | https://bitbucket.org/genee/glogon-server | http://od4jrri6r.bkt.clouddn.com/glogon-server.v1.0.0-d2018020701.tar.gz |
| docker.genee.in/genee/env-server | v0.1.4-d2015081401 | https://bitbucket.org/genee/env-server | https://bitbucket.org/genee/env-server | http://od4jrri6r.bkt.clouddn.com/env-server.v0.1.4-d2015081401.tar.gz |
| docker.genee.in/genee/vidmon-server | v0.3.3-d2016081101 | https://bitbucket.org/genee/vidmon-server | https://bitbucket.org/genee/vidmon-server | http://od4jrri6r.bkt.clouddn.com/vidmon-server.v0.3.3-d2016081101.tar.gz |
| docker.genee.in/genee/dc-cacs-server | v0.1.9-d2016081001 | https://bitbucket.org/genee-yiqikong/dc-cacs-server | https://bitbucket.org/genee-yiqikong/dc-cacs-server | http://od4jrri6r.bkt.clouddn.com/dc-cacs-serve.v0.1.9-d2016081001.tar.gz |
| docker.genee.in/genee/tszz-server | v0.1.2-d2015081401 | https://bitbucket.org/genee/tszz-server | https://bitbucket.org/genee/tszz-server | http://od4jrri6r.bkt.clouddn.com/tszz-server.v0.1.2-d2015081401.tar.gz |
| docker.genee.in/genee/epc-server | v0.5.1-d2018052801 | https://bitbucket.org/genee-latrine/epc-server | https://bitbucket.org/genee-latrine/epc-server | http://od4jrri6r.bkt.clouddn.com/epc-server.v0.5.1-d2018052801.tar.gz |
| docker.genee.in/genee/genee-updater-server | v0.2.12-d2015081401 | https://bitbucket.org/genee/genee-updater-server | https://bitbucket.org/genee/genee-updater-server | http://od4jrri6r.bkt.clouddn.com/update.v0.2.12-d2015081401.tar.gz |
| docker.genee.in/genee/mariadb | v10.1.10-d2015122701 | https://github.com/iamfat/dockerfile-mariadb | https://github.com/iamfat/dockerfile-mariadb | http://od4jrri6r.bkt.clouddn.com/mariadb.v10.1.10-d2015122701.tar.gz |
| docker.genee.in/genee/redis | v2.8.17-d2015080301 | https://github.com/iamfat/dockerfile-redis | https://github.com/iamfat/dockerfile-redis | http://od4jrri6r.bkt.clouddn.com/redis.v2.8.17-d2015080301.tar.gz |
| docker.genee.in/genee/beanstalkd | v1.10.0-d2017112401 | https://github.com/genee-projects/dockerfile-beanstalkd | https://github.com/genee-projects/dockerfile-beanstalkd | http://od4jrri6r.bkt.clouddn.com/beanstalkd.v1.10.0-d2017112401.tar.gz |
| docker.genee.in/genee/sphinxsearch | v2.2.9-d2015080301 | https://github.com/iamfat/dockerfile-sphinxsearch | https://github.com/iamfat/dockerfile-sphinxsearch | http://od4jrri6r.bkt.clouddn.com/sphinxsearch.v2.2.9-d2015080301.tar.gz |

## 服务说明

### 构建说明

* 有个 nodejs 的服务的镜像是用 genee/node:0.12 构建的, genee/node:0.12 是使用 alpine:3.2 构建的
* 非 nodejs 的服务的镜像是使用 debian:8 进行构建的

### 服务目录规划说明

* 目前大多数服务均在 genee 用户的 ~ 目录下进行配置、管理。例如:

    genee-updater-server 配置路径、结构如下:
    
    ```
    genee@less:~/genee-updater-server$ pwd
    /home/genee/genee-updater-server
    
    genee@less:~/genee-updater-server$ tree .
    .
    ├── config
    │   └── default.js
    ├── files
    └── logs
        └── genee-updater-server.log

    3 directories, 2 files
    ```
* 服务通常需要如下几个目录
    * config *配置*
    * logs *日志*
    * lib *依赖*
    * 其他非必要的目录配置

### 服务部署方式

服务部署, 需要挂载配置目录、日志目录、依赖目录、其他需要的目录到容器对应目录中.
例如:

debade-trigger 的部署, 命令如下:

```
docker run -d \
    --name=debade-trigger \
    --restart=always \
    -v /home/genee/debade-trigger/config:/etc/debade/ \
    docker.genee.in/genee/debade-trigger:v0.1.7-d20150820101
```

挂载了 config 配置目录进入

node-lims2 的部署, 命令如下:

```
docker run -d \
    --name=node-lims2 \
    --restart=always \
    -v /home/genee/node-lims2/config:/usr/src/app/config \
    -v /home/genee/node-lims2/logs:/var/log/node-lims2 \
    -v /tmp/lims2-msg:/tmp/lims2-msg \
    -p 172.17.42.1:8041:8041 \
    docker.genee.in/genee/node-lims2:v1.0.2-d2015081701
```
    
### 注意事项

* ~ 目录下, 部分服务中源码未删除, 只进行了目录挂载
* nodejs 的所有的服务, 使用 `docker exec` 进入容器中时, 请使用 `/bin/sh`, 不要使用 `/bin/bash` (alpine:3.2 没有 bash)
* mariadb 的服务初次部署需要按照如下方法部署
    * 1. 挂载临时目录 `/tmp/mysql` 到 `/target` 下
    * 2. `docker run --rm -it -v /tmp/mysql:/target docker.genee.in/genee/mariadb:xxxx /bin/bash` 进入到容器中
    * 3. `mysql_install_db` 初始化数据库数据
    * 4. `cp -r /var/lib/mysql /target` 复制 mysql 数据库至宿主机
    * 5. 宿主机上将 /target/mysql 目录放置到指定目录 (通常为 `/var/lib/mysql`)
    * 6. 重新部署即可

* 所有非公网暴露的端口, 如需内部使用, 需绑定到 **docker0** 网卡
* 所有非文件 Log, 一定要挂载 /dev/log 到容器中
* 所有服务的配置文件, 请参照上述的项目地址, 确定配置文件.
* sphinxsearch 在第一次部署后无法正常启动, 需要通过 lims2 获取 sphinxsearch 配置后才能启动

### 服务部署

#### lims2-env

> php7

```
docker run \
    --name=lims2 \
    -d \
    -v /opt/lims2/volumes:/volumes \
    -v /etc/sphinxsearch/conf.d:/etc/sphinxsearch/conf.d \
    -v /etc/lims2:/etc/lims2 \
    -v /etc/msmtprc:/etc/msmtprc \
    -v /var/run/genee-nodejs-ipc:/var/run/genee-nodejs-ipc \
    -v /var/lib/lims2:/var/lib/lims2 \
    -v /var/lib/lims2_vidcam:/var/lib/lims2_vidcam \
    -v /home/disk:/home/disk \
    -p 3007:9000/tcp \
    --restart=always \
    --privileged \
    docker.genee.in/genee/lims2:v1.0.1-d2017022103
```

```
docker run \
    --name=lims2 \
    -d \
    -v /opt/lims2/volumes:/volumes \
    -v /etc/sphinxsearch/conf.d:/etc/sphinxsearch/conf.d \
    -v /etc/lims2:/etc/lims2 \
    -v /etc/msmtprc:/etc/msmtprc \
    -v /var/run/genee-nodejs-ipc:/var/run/genee-nodejs-ipc \
    -v /var/lib/lims2:/var/lib/lims2 \
    -v /var/lib/lims2_vidcam:/var/lib/lims2_vidcam \
    -v /home/disk:/home/disk \
    -p 3007:9000/tcp \
    --restart=always \
    --privileged \
    docker.genee.in/genee/lims2:v1.1.1-d2018011101
```


#### eq-stat

```
docker run \
    --name eq-stat \
    -d \
    -p 3008:9000/tcp \
    -v /data/gini-modules:/data/gini-modules:rw \
    --restart=always \
    genee/gini:latest \
    /start
```

### nginx

```
docker run \
	--name nginx \
	-d \
	-v /home/genee/nginx/nginx.conf:/etc/nginx/nginx.conf \
        -v /home/genee/nginx/fastcgi_params:/etc/nginx/fastcgi_params \
	-v /home/genee/nginx/sites-enabled:/etc/nginx/sites-enabled \
	-v /home/genee/nginx/sites-available:/etc/nginx/sites-available \
	-v /home/genee/nginx/conf.d:/etc/nginx/conf.d \
	-v /var/log/nginx:/var/log/nginx \
	-v /var/lib/lims2:/var/lib/lims2:rw \
	-v /data/gini-modules:/data/gini-modules:rw \
	-v /var/www:/var/www \
	-v /var/run:/var/run \
	-p 80:80/tcp \
	--restart=always \
	--privileged \
	nginx:1.11-alpine
```

#### redis

```
docker run \
    --name redis \
    -d \
    -v /home/genee/redis/config/:/etc/redis \
    -v /home/genee/redis/lib/:/var/lib/redis \
    -v /dev/log/:/dev/log \
    -p 172.17.42.1:6379:6379 \
    --restart=always \
    docker.genee.in/genee/redis:v2.8.17-d2015080301
```

#### beanstalkd

```
docker run \
    --name beanstalkd \
    -d \
    -v /home/genee/beanstalkd/data:/data \
    --restart=always \
    -p 172.17.42.1:11300:11300 \
    docker.genee.in/genee/beanstalkd:v1.10.0-d2017112401
```

#### cron-server

```
docker run \
    --name cron-server \
    -d \
    -v /home/genee/cron-server/config:/usr/src/app/config \
    -v /home/genee/cron-server/logs:/usr/src/app/logs \
    --restart=always \
    docker.genee.in/genee/cron-server:v1.2.0-d2018032801
```

#### vidmon-server

```
docker run \
    -d \
    --name vidmon-server \
    -v /home/genee/vidmon-server/config:/usr/src/app/config \
    -v /home/genee/vidmon-server/logs:/usr/src/app/logs \
    -v /var/run/genee-nodejs-ipc:/var/run/genee-nodejs-ipc \
    -p 172.17.42.1:5824:5824  \
    --restart=always \
    docker.genee.in/genee/vidmon-server:v0.3.3-d2016081101
```


#### tszz-server

```
docker run \
    -d \
    --name=tszz-server \
    -v /home/genee/tszz-server/logs:/usr/src/app/logs \
    -v /home/genee/tszz-server/config:/usr/src/app/config \
    -p 8237:8237 \
    -p 8236:8236 \
    -p 8235:8235 \
    -p 8234:8234 \
    -p 8238:8238 \
    --restart=always \
    docker.genee.in/genee/tszz-server:v0.1.2-d2015081401
```

#### glogon-server

```
docker run \
    -d \
    --name=glogon-server \
    -v /home/genee/glogon-server/config:/usr/src/app/config \
    -v /home/genee/glogon-server/logs:/usr/src/app/logs \
    -p 2430:2430 \
    -p 172.17.42.1:2450:2450 \
    --restart=always \
    docker.genee.in/genee/glogon-server:v1.0.0-d2018020701
```

#### genee-updater-server:

```
docker run \
    --name genee-updater-server \
    -d \
    -v /home/genee/genee-updater-server/config/:/usr/src/app/config \
    -v /home/genee/genee-updater-server/logs/:/usr/src/app/logs \
    -v /home/genee/genee-updater-server/files/:/usr/src/app/files \
    -p 3000:3000 \
    --restart=always \
    docker.genee.in/genee/genee-updater-server:v0.2.12-d2015081401
```

#### gdoor-server:

```
docker run \
    -d \
    --name=gdoor-server \
    -v ~/gdoor-server/config:/usr/src/app/config \
    -v ~/gdoor-server/logs:/usr/src/app/logs \
    -p 2930:2930 \
    -p 2950:2950 \
    --restart=always \
    docker.genee.in/genee/gdoor-server:v0.2.0-d2018042301
```

#### epc-server:

```
docker run \
    -d \
    --name=epc-server \
    -v /home/genee/epc-server/config:/usr/src/app/config \
    -v /home/genee/epc-server/logs:/usr/src/app/logs \
    -p 3041:3041 \
    -p 3061:3061 \
    --restart=always \
    docker.genee.in/genee/epc-server:v0.5.0-d2018030201
```

#### env-server

```
docker run \
    -d \
    --name=env-server \
    -v /home/genee/env-server/config/:/usr/src/app/config \
    -p 3741:3741 \
    --restart=always \
    docker.genee.in/genee/env-server:v0.1.4-d2015081401
```

#### dc-cacs-server

```
docker run \
    -d \
    --name=dc-cacs-server \
    -v /home/genee/dc-cacs-server/config:/usr/src/app/config \
    -v /home/genee/dc-cacs-server/logs:/usr/src/app/logs \
    -v /var/run/genee-nodejs-ipc:/var/run/genee-nodejs-ipc \
    -p 2730:2730 \
    -p 2830:2830 \
    --restart=always \
    docker.genee.in/genee/dc-cacs-server:v0.1.9-d2016081001
```

#### cacs-server

```
docker run \
    -d \
    --name=cacs-server \
    -v /home/genee/cacs-server/config:/usr/src/app/config \
    -v /home/genee/cacs-server/logs:/usr/src/app/logs \
    -v /var/run/genee-nodejs-ipc:/var/run/genee-nodejs-ipc \
    -p 2530:2530 \
    --restart=always \
    docker.genee.in/genee/cacs-server:v0.2.2-d2016081001 
```

#### sphinxsearch

```
docker run \
    --name=sphinxsearch \
    -d \
    -v /home/genee/sphinxsearch/lib/:/var/lib/sphinxsearch \
    -v /home/genee/sphinxsearch/logs/:/var/log/sphinxsearch \
    -v /dev/log/:/dev/log \
    -v /home/genee/sphinxsearch/config/:/etc/sphinxsearch \
    -p 172.17.42.1:9306:9306 \
    --restart=always \
    docker.genee.in/genee/sphinxsearch:v2.2.9-d2015080301
```

#### debade-trigger

```
docker run \
    --name=debade-trigger \
    -d \
    -v /home/genee/debade-trigger/config:/etc/debade \
    --restart=always \
    docker.genee.in/genee/debade-trigger:v0.1.7-d20150820101
```

#### debade-courier

```
docker run \
    --name=debade-courier \
    -d \
    -v /home/genee/debade-courier/config:/etc/debade \
    --restart=always \
    -p 172.17.42.1:3333:3333 \
    docker.genee.in/genee/debade-courier:v0.3.0-d2015122301
```

#### lims2-guard

```
docker run \
     --name=lims2-guard 
     -d \
     -v /var/run/docker.sock:/var/run/docker.sock \
    --restart=always \
    docker.genee.in/genee/lims2-guard:v1.0.0-d2015081701
```

#### node-lims2

```
docker run \
    --name=node-lims2 \
    -d \
    -v /home/genee/node-lims2/config:/usr/src/app/config/ \
    -v /home/genee/node-lims2/logs:/var/log/node-lims2 \
    -v /tmp/lims2-msg:/tmp/lims2-msg \
    -p 172.17.42.1:8041:8041 \
    --restart=always \
    docker.genee.in/genee/node-lims2:v2.0.1-d2017120801
```

#### mariadb

```
docker run \
    --name=mariadb \
    -d \
    -v /var/lib/mysql:/var/lib/mysql \
    -v /var/log/mysql:/var/log/mysql \
    -v /home/genee/mariadb/my.cnf:/etc/mysql/my.cnf \
    -v /home/genee/mariadb/conf.d/binlog.cnf:/etc/mysql/conf.d/binlog.cnf \
    -v /home/genee/mariadb/conf.d/mysqld_safe_syslog.cnf:/etc/mysql/conf.d/mysqld_safe_syslog.cnf \
    -v /dev/log:/dev/log \
    -p 172.17.42.1:3306:3306 \
    --restart=always \
    docker.genee.in/genee/mariadb:v10.1.10-d2015122701
```

#### mongo

```
docker run \
	--name=mongo \
	-d \
	-v /home/genee/mongo/data/db:/data/db \
	-p 172.17.42.1:27017:27017/tcp \
	--cpu-period=10000 \
	--cpu-quota=1000 \
	--privileged \
	mongo:3.4.4
```

> 注意在kernal版本为4.0以下的时候 必须要加--cpu-period --cpu-quota来限制cpu使用

> 并且可以一直尝试去使用官方的最新版本

#### reserv-server

```
docker run \
    --name=reserv-server \
    -d \
    -v /home/genee/reserv-server/config:/usr/src/app/config \
    -v /home/genee/reserv-server/logs:/usr/src/app/logs \
    -p 172.17.42.1:9898:9898 \
    -p 172.17.42.1:9509:9509 \
    --restart=always \
    docker.genee.in/genee/reserv-server:v0.5.0-d2018011101
```

#### icco-server

```
docker run \
    --name=icco-server \
    -d \
    -v /home/genee/icco-server/config:/usr/src/app/config \
    -v /home/genee/icco-server/logs:/usr/src/app/logs \
    -v /var/run/genee-nodejs-ipc:/var/run/genee-nodejs-ipc \
    -p 2333:2333 \
    -p 2332:2332 \
    -p 2730:2730 \
    --restart=always \
    docker.genee.in/genee/icco-server:v0.3.12-d2017042501
```

#### lims2-backup-server

```
docker run \
    --name=lims2-backup-server \
    -d \
    -v /backups/remote:/backup/backups/remote \
    -p 1738:1738 \
    --restart=always \
    docker.genee.in/genee/lims2-backup-server:v0.1.1-d2015082701
```

#### haikan-nvs

```
docker run \
    --name=haikan-nvs \
    -d \
    -v /home/genee/haikan-nvs/config/haikan_nvs.conf:/etc/haikan_nvs.conf \
    --restart=always \
    --log-driver=none \
    docker.genee.in/genee/haikan-nvs:v1.2.3-d2018041801
```

> --log-driver 需要在 1.6 (及)以上的 docker 中使用, 1.6 以下请不要使用 --log-driver


#### tiandy-nvs

```
docker run \
    --name=tiandy-nvs \
    -d \
    -v /home/genee/tiandy-nvs/config/tiandy_nvs.conf:/etc/tiandy_nvs.conf \
    --restart=always \
    --log-driver=none \
    docker.genee.in/genee/tiandy-nvs:v1.2.1-d2015082701
```

> --log-driver 需要在 1.6 (及)以上的 docker 中使用, 1.6 以下请不要使用 --log-driver

> 目前所有需要 tiandy-nvs 和 haikan-nvs 的站点 docker daemon 均在 1.6 版本以上

#### crtmp-server

```
docker run \
    --name=crtmp-server \
    -d \
    -p 1935:1935 \
    -v /home/genee/crtmp-server/config/:/etc/lims2/crtmp-server/ \
    --restart=always \
    docker.genee.in/genee/crtmp-server:v0.716-d2015081701
```
