# Linux 安装 Redis
## 1.先安装gcc 环境
```
yum -y install gcc gcc-c++
# 安装完毕之后 输入 gcc --version 验证是否安装成功
```

## 2.安装Redis
>可参见官网 https://redis.io/download

```
# 以最新版为例
# 下载
wget http://download.redis.io/releases/redis-5.0.4.tar.gz
# 解压
tar xzf redis-5.0.4.tar.gz
# 编译
cd redis-5.0.4
make 
# 启动redis
src/redis-server

# 启动redis-cli
src/redis-cli

# 测试
set foo bar
get foo
```



