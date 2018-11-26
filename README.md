# parallel_docker

## 服务开启

**docker-compose的命令执行都是在parallel_docker根目录下执行的**

+ 开启所有服务
> docker-compose up -d

+ 关闭所有服务
> docker-compose down

+ 单独开启服务
  + 只开启mysql
  > docker-compose up -d mysql
  + 只开启redis
  > docker-compose up -d redis
  + 只开启elasticsearch
  > docker-compose up -d elasticsearch
  + 只开启mongo
  > docker-compose up -d mongo
  + 开启php后台服务器
  > docker-compose up -d mysql redis php-fpm nginx workspace
  + 开启会员中心和门户网站
  > docker-compose up -d nginx mysql redis php-fpm workspace member portal
  + 开启咨询机构控制台
  > docker-compose up -d nginx mysql redis mongo php-fpm workspace api member portal consult

(单独开启容器的某一个服务，其他的服务连接外部)

## 服务维护

<pre>
//查看服务状态
docker-compose ps

//停止某个服务(stop跟上容器名称, 如mysql)
docker-compose stop mysql

//启动被停止的服务
docker-compose start mysql

//删除被停止的服务
docker-compose rm mysql

//查看服务的输出
docker-compose logs mysql

//在一个服务上执行一个命令
docker-compose run mysql ls

//进入服务器bash命令行
docker-compose exec mysql bash

</pre>


## 使用前

使用前需要你在系统上安装好docker以及docker-compose <br/>
适用多系统 (windows, linux, MAC os等)

下面是在linux环境下安装docker-compose的命令
<pre>
// 安装docker-compose
curl -L https://get.daocloud.io/docker/compose/releases/download/1.13.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
// 开启国内镜像加速
curl -sSL https://get.daocloud.io/daotools/set_mirror.sh | sh -s http://1f637783.m.daocloud.io
</pre>


## 环境配置

### .env文件

+ 应用代码路径指定
<pre>
APP_CODE_PATH_HOST    ParallelForPhp_new代码在本机路径
API_CODE_PATH_HOST    ParallelApiForSails代码在本机路径
MEMBER_CODE_PATH_HOST    MemberCenterForSails代码在本机路径
PORTAL_CODE_PATH_HOST    ParallelPortalForSails代码在本机路径
CONSULT_CODE_PATH_HOST    ParallelConsultationForVue代码在本机路径
</pre>

+ windows系统的特殊配置
> COMPOSE_PATH_SEPARATOR=;

+ 具体容器的参数配置 (主要是端口指定)

### 其他个性化配置(如果需要的话)

1. 将nginx的conf配置文件放置于./nginx/sites/目录下

2. mysql中导入数据
有两种方式, 一种是直接用sql管理工具(如navicat)连接后直接导入  
第二种是进入容器bash命令行执行命令  
<pre>
// 将sql文件放置于./mysql/docker-entrypoint-initdb.d/目录下  
// (这里放置的是parallel.sql文件)  
// 然后执行命令:
docker-compose exec mysql bash  
mysql -u root -p < /docker-entrypoint-initdb.d/parallel.sql  
</pre>

### 项目中服务连接配置

1. 容器内部间连接，在配置文件配置相关服务时，使用主机名，如redis的配置
<pre>
redis:{
    host: 'redis',
    port: 6379,
    db: 3,
    prefix: 'portal:'
    }   
</pre>

2. 前端服务器打开过程中有交互以及切换的情况，这里对前端服务网络访问也做了域名指向  
需要适当配置hosts文件
只使用php服务时，只需要配置api.parallel.test, web.parallel.test两个域名和ip对应即可  
使用前端服务时，需要再配置portal.parallel.test, member.parallel.test，consult.parallel.test和ip对应

