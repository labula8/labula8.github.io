
# redis集群调研

## 调研对比表

| Feature       | Redis Cluster                    | TwemProxy              | Codis                             | CacheCloud    |
|---|---|---|---|---|
| 厂商          | 官方                             | Twitter                | 豌豆荚                            | 搜狐     |
| 存储引擎      | 原生Redis                        | 原生Redis              | 基于原生Redis扩展增加迁移相关指令 | 原生Redis     |
| 数据分布算法  | 哈希槽crc16(key) % 16384         | ketama/modula/random   | 哈希槽crc16(key) % 1024           | 同Redis Cluster     |
| 平滑扩缩容    | 支持                             | 不支持                 | 支持                              | 同Redis Cluster     |
| Value大小限制 | 无                               | 无                     | 无                                | 同Redis Cluster     |
| 开发语言(Proxy)| 采用无中心节点设计,无Proxy      | C                      | Go                                | Java     |
| Client        | 需要支持cluster语义              | 任意                   | 任意                              | 同Redis Cluster     |
| Pipeline      | 不支持                           | 支持                   | 支持                              | 同Redis Cluster     |
| 运维成本      | 高                               | 高                     | 低                                | 低     |
| 定制开发成本  | 高                               | 高                     | 低                                | 高     |
| 优点          | 官方出品，持续维护，无中心设计，数据自动同步 | 线上使用，架构成熟，运维熟悉，数据同步   | 大厂使用多，有很多成功案例，go开发，匹配技术栈，数据同步扩容，运维方便，可高度定制 | 有很多成功案例，界面友好，数据同步扩容，运维最方便，java技术栈，定制化排错可能有坑     |
| 缺点          | 需要支持cluster语义，运维需要了解相关架构，迁移成本  | 缩扩容麻烦，手工运维           | 不是原生redis，很多指令不支持，依赖项目持续更新          | 高     |

    官方：redis-cluster
    最火：TwemProxy, codis
    界面最友好: CacheCloud

## 初步结论

    当前生产环境使用 TwemProxy

    综合对比，结合部门技术栈，候选方案排序：
    1. Codis
    2. Redis Cluster
    3. CacheCloud


## 参考

    twemproxy
    https://github.com/twitter/twemproxy
    
    Codis
    https://github.com/CodisLabs/codis
    
    cachecloud
    https://github.com/sohutv/cachecloud
    
    X-pipe
    https://github.com/ctripcorp/x-pipe

    codis不支持指令
    https://github.com/CodisLabs/codis/blob/release3.2/doc/unsupported_cmds.md
    
    大规模 codis 集群的治理与实践
    https://cloud.tencent.com/developer/article/1006262
    
    为什么大厂都喜欢用 Codis 来管理分布式集群？
    https://juejin.im/post/5c132b076fb9a04a08218eef
    
    美团在Redis上踩过的一些坑-5.redis cluster遇到的一些问题
    https://blog.51cto.com/lee90/2057976
    

