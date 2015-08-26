# lims2-deploy-doc

该文档用于说明如何部署 lims2 依赖的 docker 服务.

## 服务列表和版本

| 服务列表 | 版本 |
| --------------------------------------- | ---------------------------: |
| docker.genee.in/genee/reserv-server | v0.2.1-d2015082101 |
| docker.genee.in/genee/lims2-backup-server | v0.1-d2015082001 |
| docker.genee.in/genee/debade-courier | v0.2.2-d2015082001 |
| docker.genee.in/genee/debade-trigger | v0.1.7-d20150820101 **注意, 此版本未正确按照 [docker-convention](https://github.com/genee-tools/docker-convention) 限定** |
| docker.genee.in/genee/haikan-nvs | v1.2.1-d2015081901 |
| docker.genee.in/genee/tiandy-nvs | v1.2.1-d2015081901 |
| docker.genee.in/genee/lims2-guard | v1.0.0-d2015081701 |
| docker.genee.in/genee/crtmp-server | v0.716-d2015081701 |
| docker.genee.in/genee/node-lims2 | v1.0.2-d2015081701 |
| docker.genee.in/genee/icco-server | v0.3.9-d3015081401 |
| docker.genee.in/genee/cacs-server | v0.2.1-d2015081401 |
| docker.genee.in/genee/gdoor-server | v0.1.8-d2015081401 |
| docker.genee.in/genee/glogon-server |  v0.4.4-d2015081401 |
| docker.genee.in/genee/env-server | v0.1.4-d2015081401 |
| docker.genee.in/genee/vidmon-server | v0.3.2-d2015081401 |
| docker.genee.in/genee/dc-cacs-server | v0.1.8-d2015081401 |
| docker.genee.in/genee/tszz-server | v0.1.2-d2015081401 |
| docker.genee.in/genee/epc-server | v0.3.4-d2015081401 |
| docker.genee.in/genee/genee-updater-server | v0.2.12-d2015081401 |
| docker.genee.in/genee/mariadb | v10.0.21-d2015081001 |
| docker.genee.in/genee/redis | v2.8.17-d2015080301 |
| docker.genee.in/genee/beanstalkd | v1.10.0-d2015080301 |
| docker.genee.in/genee/sphinxsearch | v2.2.9-d2015080301 |

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
	│   └── default.js
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
	docker.genee.in/genee/node-lims2:v1.0.2-d2015081701
	```
	
### 注意事项

* ~ 目录下, 部分服务中源码未删除, 只进行了目录挂载
* nodejs 的所有的服务, 使用 `docker exec` 进入容器中时, 请使用 `/bin/sh`, 不要使用 `/bin/bash` (alpine:3.2 没有 bash)
* mariadb 的服务初次部署需要按照如下方法部署
	* 1. 挂载临时目录 `/tmp/mysql` 到 `/target` 下
	* 2. `docker run --rm -it -v /tmp/mysql:/target docker.genee.in/genee/mariadb:xxxx /bin/bash` 进入到容器中
	* 3. `mysql_db_install` 初始化数据库数据
	* 4. `tar -zcvf /target/mysql.tar.gz /var/lib/mysql` 打包基础 mysql 数据库
	* 5. 宿主机上进行 mysql.tar.gz 解压到 /var/lib/
	* 6. 重新部署即可

* 所有非公网暴露的端口, 如需内部使用, 需绑定到 **docker0** 网卡
* 所有非文件 Log, 一定要挂载 /dev/log 到容器中

### 服务部署


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
	docker.genee.in/genee/beanstalkd:v1.10.0-d2015080301
```


#### vidmon-server

```
docker run \
	-d \
	--name vidmon-server \
	-v /home/genee/vidmon-server/config:/usr/src/app/config \
	-v /home/genee/vidmon-server/logs:/usr/src/app/logs \
	-v /tmp/genee-nodejs-ipc:/tmp/genee-nodejs-ipc \
	-p 5824:5824  \
	--restart=always \
	docker.genee.in/genee/vidmon-server:v0.3.2-d2015081401
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
	-v /tmp/genee-nodejs-ipc:/tmp/genee-nodejs-ipc \
	-p 2430:2430 \
	--restart=always \
	docker.genee.in/genee/glogon-server:v0.4.4-d2015081401
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
	-v /home/genee/gdoor-server/config:/usr/src/app/config \
	-v /home/genee/gdoor-server/logs:/usr/src/app/logs \
	-v /tmp/genee-nodejs-ipc:/tmp/genee-nodejs-ipc \
	-p 2930:2930 \
	--restart=always \
	docker.genee.in/genee/gdoor-server:v0.1.8-d2015081401
```

#### epc-server:

```
docker run \
	-d \
	--name=epc-server \
	-v /tmp/genee-nodejs-ipc:/tmp/genee-nodejs-ipc \
	-v /home/genee/epc-server/config:/usr/src/app/config \
	-v /home/genee/epc-server/logs:/usr/src/app/logs \
	-p 3041:3041 \
	--restart=always \
	docker.genee.in/genee/epc-server:v0.3.4-d2015081401
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
	-v /tmp/genee-nodejs-ipc:/tmp/genee-nodejs-ipc \
	-p 2730:2730 \
	-p 2830:2830 \
	--restart=always \
	docker.genee.in/genee/dc-cacs-server:v0.1.8-d2015081401
```

#### cacs-server

```
docker run \
	-d \
	--name=cacs-server \
	-v /home/genee/cacs-server/config:/usr/src/app/config \
	-v /home/genee/cacs-server/logs:/usr/src/app/logs \
	-v /tmp/genee-nodejs-ipc:/tmp/genee-nodejs-ipc \
	-p 2530:2530 \
	--restart=always \
	docker.genee.in/genee/cacs-server:v0.2.1-d2015081401 
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
	docker.genee.in/genee/debade-courier:v0.2.2-d2015082001
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
	-v /home/genee/node-lims2/config:/usr/src/app/ \
	-v /home/genee/node-lims2/logs:/var/log/node-lims2 \
	-v /tmp/lims2-msg:/tmp/lims2-msg \
	-p 172.17.42.1:8041:8041 \
	--restart=always \
	docker.genee.in/genee/node-lims2:v1.0.2-d2015081701
```

#### mariadb

```
docker run \
	--name=mariadb \
	-d \
	-v /var/lib/mysql:/var/lib/mysql \
	-p 172.17.42.1:3306:3306 \
	--restart=always \
	docker.genee.in/genee/mariadb:v10.0.21-d2015081001
```

#### reserv-server

```
docker run \
	--name=reserv-server \
	-d \
	-v /home/genee/reserv-server/config:/usr/src/app/config \
	-v /home/genee/reserv-server/logs:/usr/src/app/logs \
	-p 172.17.42.1:9898:9898 \
	--restart=always \
	docker.genee.in/genee/reserv-server:v0.2.1-d2015082101
```

#### icco-server

```
docker run \
	--name=icco-server 
	-d \
	-v /home/genee/icco-server/config:/usr/src/app/config \
	-v /home/genee/icco-server/logs:/usr/src/app/logs \
	-v /tmp/genee-node-ipc:/tmp/genee-node-ipc \
	-p 2333:2333 \
	-p 2332:2332 \
	-p 2730:2730 \
	--restart=always \
	docker.genee.in/genee/icco-server:v0.3.9-d2015081401
```

#### lims2-backup-server

```
docker run \
	--name=lims2-backup-server \
	-d \
	-v /backups/remote:/backup/backups/remote \
	-p 1738:1738 \
   --restart=always \
   docker.genee.in/genee/lims2-backup-server:v0.1-d2015082001
```

#### haikan-nvs

TODO 

#### tiandy-nvs

TODO

#### crtmp-server

TODO
