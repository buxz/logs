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

## 3. 特点
1. 速度快
    - c语言实现
    - 完全基于内存
    - 单线程，避免线程切换开销以及线程的竞争问题
    - 网络层使用epoll解决高并发问题，非阻塞I/O,不在网络上浪费时间
2. 支持多种数据类型
    - 常用的String、Hash、List、Set、SortSet
    - 都是基于键值对
3. 功能丰富
    - 可设置建过期
    - Pipeline功能，减小网络开销
    - 通过Lua创建新命令，具有原子性
    - 基于发布订阅可实现简单的消息队列
4. 服务器简单
    - 采用单线程模型，减少竞争，规避并发问题
    - 不依赖操作系统类库（多路复用Redis自己实现了）
5. 支持持久化
    - RDB
    - AOF
6. 主从复制，高可用/分布式


## 4.使用场景
1. 缓存
2. 排行榜
    - 利用redis的SortSet数据结构
3. 计算器/限速器
    - 利用Redis中的原子性的自增操作，我们可以统计类似用户点赞数/用户访问数
    - 限制某个用户访问某个api的频率，常用的抢购，防止用户疯狂点击带来不必要的压力
4. 好友关系
    - 利用集合的交集、并集、差集等
5. session共享

## 5.不适用场景
>Redis的持久化方案并不能保证数据的绝对的落地，还可能带来性能下降，因为 持久化太过频繁会增大服务的压力
1. 数据量太大
2. 数据访问频率非常低的业务

# Redis一些典型问题
## 缓存穿透
>是指查询一个数据库一定不存在的数据。
1. 正常使用缓存流程大致是，数据查询先对缓存查询，如果

## 缓存雪崩
## 缓存击穿

