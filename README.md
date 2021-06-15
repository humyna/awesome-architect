# 后端架构师知识能力图谱

## 架构原则
### 软件设计原则
#### 1. GRASP 通用职责分配软件模式
> 来自 Craig Larman 的软件设计书《 UML 和模式应用》，Larman 在书中提出软件设计的关键任务是职责分配，并提炼总结出 9 种 (5 种核心 +4 种扩展) 软件职责分配模式，这些模式是比 GoF 设计模式更抽象的元模式。

1. 信息专家 (Information Expert)
2. 创建者 (Creator)
3. 低耦合 (Low Coupling)
4. 高内聚 (High Cohesion)
5. 控制器 (Controller)
6. 多态 (Polymorphism)
7. 纯虚构 (Pure Fabrication)
8. 间接 (Indirection)
9. 受保护的变化 (Protected Variation)


#### 2. SOLID 面向对象设计原则
> S.O.L.I.D 是面向对象设计和编程 (OOD&OOP) 中几个重要原则的首字母缩写

1. 单一职责原则 (The Single Responsibility Principle)
2. 开放封闭原则 (The Open Closed Principle)
3. 里氏替代原则 (The Liskov Substitution Principle)
4. 依赖倒置原则 (The Dependency Inversion Principle)
5. 接口分离原则 (The Interface Segregation Principle)


### 分布式系统架构设计原则

#### 1. AKF 架构原则
> 共15 个架构原则，来自《架构即未来 (The Art of Scalability)》一书，作者马丁 L. 阿伯特和迈克尔 T. 费舍尔分别是 eBay 和 PayPal 的前 CTO，他们经历过 eBay 和 PayPal 大规模分布式电商平台的架构演进，在一线实战经验的基础上总结并提炼出 15 条架构原则。

1. N + 1 设计
2. 回滚设计
3. 禁用设计
4. 监控设计
5. 设计多活数据中心
6. 使用成熟的技术
7. 异步设计
8. 无状态系统
9. 水平扩展而非垂直升级
10. 设计时至少要有两步前瞻性
11. 非核心则购买
12. 使用商品化硬件
13. 小构建、小发布和快试错
14. 隔离故障
15. 自动化

*消化吸收这 15 条原则，基本可保系统架构不会有原则性问题；这 15 条原则同样适用于现在的微服务架构。*

#### 2. 12 要素应用
> Heroku 是国外知名的云应用平台。基于上百万应用的托管和运营经验，创始人 Adam Wiggins 提出了 12 要素应用宣言。简单讲，满足这 12 个要素的应用是比较容易云化并居住在 Heroku 平台上的。

1. 基准代码——一份基准代码，多份部署
2. 依赖——显式声明依赖。
3. 配置——在环境中存储配置。现在采用集中式配置中心也是一种流行方式。
4. 后端服务——把后端服务 (例如缓存，数据库，MQ 等) 当作附加资源，相关配置和连接字符串通过环境变量注入，或者采用配置中心。
5. 构建、发布和运行——严格分离构建和运行。
6. 进程——一个或者多个无状态的进程运行应用。
7. 端口绑定——通过端口绑定提供服务。
8. 并发——通过进程模型进行扩展。
9. 易处理——快速启动和优雅终止可最大化健壮性。
10. 开发环境和线上环境等价——尽可能保持开发、测试、预发和线上环境相同。
11. 日志——把日志当作数据流。
12. 管理进程——后台管理任务当作一次性的进程

*12 要素应用也是当前云原生应用 (Cloud Native App) 的参考标准。满足这 12 个要素的应用，可以比较顺利迁移到各种云平台 (Kubernetes, Marathon, Cloud Foundry 等) 上; Docker 容器技术可以认为是为云迁移量身定制的技术。容器化是后续云迁移的捷径，所以遗留应用改造可以先想办法做到容器化*


#### 3. CAP 定理
> 2000 年 7 月，加州大学伯克利分校的 Eric Brewer 教授在 ACM PODC 会议上提出 CAP 猜想。2 年后，麻省理工学院的 Seth Gilbert 和 Nancy Lynch 从理论上证明了 CAP。之后，CAP 理论正式成为分布式计算领域的公认定理。
>
> CAP 认为：一个分布式系统最多同时满足一致性 (Consistency)，可用性 (Availability) 和分区容忍性 (Partition Tolerance) 这三项中的两项。

1. 一致性 (Consistency)
2. 可用性 (Availability)
3. 分区容忍性 (Partition tolerance)

![](./images/cap-theorem.jpeg)

#### 4. BASE 理论
> eBay 架构师 Dan Pritchett 基于对大规模分布式系统的实践总结，在 ACM 上发表文章提出了 BASE 理论，BASE 理论是对于 CAP 理论的延伸，核心思想是即使无法做到强一致性 (Strong Consistency，CAP 中的一致性指强一致性)，但是可以采用适当的方式达到最终一致性 (Eventual Consistency)。
>
> BASE 指基本可用 (Basically Available)、软状态 (Soft State) 和最终一致性 (Eventual Consistency)。

1. 基本可用 (Basically Available)
2. 软状态 (Soft State)
3. 最终一致性 (Eventual Consistency)

*选择使用分布式产品时，比如 NoSQL 数据库，你需要了解它在 CAP 环中所在的位置，确保它满足你的场景需要。*


### 组织和系统改进原则
#### 1. 康威法则
> Melvin Conway 在 1967 年提出所谓康威法则，指出组织架构和系统架构之间有一种隐含的映射关系：Organization which design system […] are constrained to produce designs which are copies of the communication structures of these organization. 
> 康威法则也可以倒过来阐述：Conway’s law reversed：You won’t be able to successfully establish an efficient organization structure that is not supported by your system design(architecture)

*康威法则是微服务架构背后的组织原则*

#### 2. 系统改进三原则
> IT 运维管理畅销书《凤凰项目》的作者 Gene Kim 在调研了众多高效能 IT 组织后总结出支撑 DevOps 运作的三个原理 (The Three Ways: The Principles Underpinning DevOps)

![](./images/devops-design-principle.jpeg)

1. 系统思考 (System Thinking)
2. 强化反馈环 (Amplify Feedback Loops)
3. 持续试验和学习的文化 (Culture of Continual Experimentation And Learning)


## 架构方法论

## 架构设计能力
### 微服务

### 分布式

## 架构工具

## 解决方案
### 性能调优

### 高可用

### 如何评估新技术

## 软件工程
### DevOps

### CI/CD

### 工程师文化

## 注意事项

## 参考资料
1. [架构师必须知道的架构设计原则](https://mp.weixin.qq.com/s/03wnIHoAe6VyiMur0UvZHA)

