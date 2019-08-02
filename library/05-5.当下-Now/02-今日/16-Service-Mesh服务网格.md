# Service-Mesh

## 服务网格

开源框架

Istio
Linkerd

Service Mesh

几个比较火的Service Mesh实现

Nginx出品—nginmesh

https://github.com/nginmesh/nginmesh

Linkerd制造商Kubernetes出品—conduit

https://github.com/runconduit/conduit

谷歌&IBM出品—istio

https://github.com/istio/istio


## Istio

简介：
    Google联合IBM、Lyft推出的Istio，一经问世就受到了人们的普遍关注，其热度迅速攀升，成为Service Mesh（服务网格）方案的代表项目。
    《深入浅出Istio：Service Mesh快速入门与实践》整理了Istio中的部分概念和案例，
    以快速入门的形式，对Istio的基础用法一一进行讲解，并在书末给出一些试用方面的建议。
    在《深入浅出Istio：Service Mesh快速入门与实践》中，前3章从微服务和服务网格的简短历史开始，
    讲述了服务网格的诞生过程、基本特性及Istio的核心功能，若对这些内容已经有所了解，则可以直接从第4章开始阅读；
    第4、5章分别讲解了Istio的配置和部署过程；
    第6章至第9章，通过多个场景来讲解Istio的常用功能；
    第10章结合了笔者的实践经验，为读者提供了Istio的一系列试用建议。
    《深入浅出Istio：Service Mesh快速入门与实践》没有采用官方复杂的Book Info应用案例，
    而是采用客户端+简单HTTP服务端的案例，读者随时都能在短时间内启动一个小的测试。
    《深入浅出Istio：Service Mesh快速入门与实践》面向对服务网格技术感兴趣，
    并希望进一步了解和学习Istio的中高级技术人员，假设读者已经了解Kubernetes的相关概念
    并能够在Kubernetes上熟练部署和管理微服务。

第1章 服务网格的历史 1
1.1 Spring Cloud 3
1.2 Linkerd 4
1.3 Istio 6
1.4 国内服务网格的兴起 6
第2章 服务网格的基本特性 8
2.1 连接 9
2.2 安全 12
2.3 策略 13
2.4 观察 13
第3章 Istio基本介绍 15
3.1 Istio的核心组件及其功能 16
3.1.1 Pilot 16
3.1.2 Mixer 18
3.1.3 Citadel 20
3.1.4 Sidecar（Envoy） 20
3.2 核心配置对象 21
3.2.1 networking.istio.io 22
3.2.2 config.istio.io 24
3.2.3 authentication.istio.io 27
3.2.4 rbac.istio.io 28
3.3 小结 28
第4章 Istio快速入门 29
4.1 环境介绍 30
4.2 快速部署Istio 31
4.3 部署两个版本的服务 33
4.4 部署客户端服务 37
4.5 验证服务 39
4.6 创建目标规则和默认路由 39
4.7 小结 42
第5章 用Helm部署Istio 43
5.1 Istio Chart概述 44
5.1.1 Chart.yaml 44
5.1.2 values-*.yaml 45
5.1.3 requirements.yaml 46
5.1.4 templates/_affinity.tpl 47
5.1.5 templates/sidecar-injector-configmap.yaml 47
5.1.6 templates/configmap.yaml 48
5.1.7 templates/crds.yaml 48
5.1.8 charts 48
5.2 全局变量介绍 49
5.2.1 hub和tag 49
5.2.2 ingress.enabled 50
5.2.3 Proxy相关的参数 51
5.2.4 proxy_init.image 53
5.2.5 imagePullPolicy 53
5.2.6 controlPlaneSecurityEnabled 53
5.2.7 disablePolicyChecks 53
5.2.8 enableTracing 53
5.2.9 mtls.enabled 53
5.2.10 imagePullSecrets 54
5.2.11 arch 54
5.2.12 oneNamespace 54
5.2.13 configValidation 54
5.2.14 meshExpansion 55
5.2.15 meshExpansionILB 55
5.2.16 defaultResources 55
5.2.17 hyperkube 55
5.2.18 priorityClassName 55
5.2.19 crds 56
5.2.20 小结 56
5.3 Istio安装清单的生成和部署 56
5.3.1 编辑values.yaml 56
5.3.2 生成部署清单 58
5.3.3 部署Istio 58
5.4 小结 59
第6章 Istio的常用功能 60
6.1 在网格中部署应用 61
6.1.1 对工作负载的要求 63
6.1.2 使用自动注入 64
6.1.3 准备测试应用 69
6.2 修改Istio配置 69
6.3 使用Istio Dashboard 70
6.3.1 启用Grafana 70
6.3.2 访问Grafana 71
6.3.3 开放Grafana服务 73
6.3.4 学习和定制 74
6.4 使用Prometheus 76
6.4.1 访问Prometheus 76
6.4.2 开放Prometheus服务 77
6.4.3 学习和定制 77
6.5 使用Jaeger 77
6.5.1 启用Jaeger 78
6.5.2 访问Jaeger 78
6.5.3 跟踪参数的传递 81
6.5.4 开放Jaeger服务 86
6.6 使用Kiali 87
6.6.1 启用Kiali 87
6.6.2 访问Kiali 88
6.6.3 开放Kiali服务 92
6.7 小结 92
第7章 HTTP流量管理 93
7.1 定义目标规则 94
7.2 定义默认路由 98
7.3 流量的拆分和迁移 101
7.4 金丝雀部署 105
7.5 根据来源服务进行路由 108
7.6 对URI进行重定向 110
7.7 通信超时控制 115
7.8 故障重试控制 116
7.9 入口流量管理 120
7.9.1 使用Gateway开放服务 121
7.9.2 为Gateway添加证书支持 123
7.9.3 为Gateway添加多个证书支持 124
7.9.4 配置入口流量的路由 126
7.10 出口流量管理 127
7.10.1 设置Sidecar的流量劫持范围 128
7.10.2 设置ServiceEntry 129
7.11 新建Gateway控制器 131
7.12 设置服务熔断 134
7.13 故障注入测试 136
7.13.1 注入延迟 137
7.13.2 注入中断 138
7.14 流量复制 139
第8章 Mixer适配器的应用 142
8.1 Mixer适配器简介 143
8.2 基于Denier适配器的访问控制 144
8.3 基于Listchecker适配器的访问控制 146
8.4 使用MemQuota适配器进行服务限流 150
8.4.1 Mixer对象的定义 150
8.4.2 客户端对象定义 152
8.4.3 测试限流功能 153
8.4.4 注意事项 154
8.5 使用RedisQuota适配器进行服务限流 155
8.5.1 启动Redis服务 155
8.5.2 定义限流相关对象 156
8.5.3 测试限流功能 158
8.6 为Prometheus定义监控指标 158
8.6.1 默认监控指标 159
8.6.2 自定义监控指标 162
8.7 使用stdio输出自定义日志 165
8.7.1 默认的访问日志 167
8.7.2 定义日志对象 169
8.7.3 测试输出 170
8.8 使用Fluentd输出日志 171
8.8.1 部署Fluentd 171
8.8.2 定义日志对象 173
8.8.3 测试输出 174
8.9 小结 175
第9章 Istio的安全加固 176
9.1 Istio安全加固概述 177
9.2 启用mTLS 179
9.3 设置RBAC 183
9.4 RBAC的除错过程 189
第10章 Istio的试用建议 192
10.1 Istio自身的突出问题 193
10.2 确定功能范围 194
10.3 选择试用业务 196
10.4 试用过程 197
10.4.1 制定目标 197
10.4.2 方案部署 198
10.4.3 测试验证 200
10.4.4 切换演练 201
10.4.5 试点上线 201

## Linkerd

## Envoy


## 参考

https://baike.baidu.com/item/%E6%B7%B1%E5%85%A5%E6%B5%85%E5%87%BAIstio%3AService%20Mesh%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8%E4%B8%8E%E5%AE%9E%E8%B7%B5

https://www.jianshu.com/p/e23e3e74538e

http://baijiahao.baidu.com/s?id=1604614219077165559&wfr=spider&for=pc

https://gitbook.cn/books/5a1e7dca387c5b4ee351790b/index.html

https://time.geekbang.org/article/2362

https://www.servicemesher.com/istio-handbook/

https://www.cnblogs.com/rinack/p/10792336.html

https://www.kubernetes.org.cn/istio

https://www.kubernetes.org.cn/5470.html

https://istio.cn/t/topic/169

https://istio.io/zh/docs/

https://github.com/apache/servicecomb-service-center

https://www.cnblogs.com/xishuai/p/microservices-and-service-mesh.html

https://jimmysong.io/posts/what-is-a-service-mesh/

https://skyao.io/learning-istio/

https://skyao.io/talk/201710-service-mesh-next-generation-microservice/

活动

https://www.lfasiallc.com/events/kubecon-cloudnativecon-china-2019/schedule-chinese/

blog

https://skyao.io/

linkerd

https://gitbook.cn/gitchat/column/5a3740d7d7fd1364997391bf/topic/5a3757cfd7fd136499739b8e

https://jimmysong.io/posts/future-architecture-from-soa-to-cloud-native/