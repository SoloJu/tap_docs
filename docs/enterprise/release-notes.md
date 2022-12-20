# 更新日志

## V2.11

### 新增功能

- 用户可以根据需要调整目标节点建表时字段的类型、长度和精度
- 在创建数据源时，支持设置黑名单将不需要的表过滤掉
- 新增Beta数据源BigQuery支持作为目标进行数据写入
- 新增支持CSV文件作为源进行数据同步
- 新增支持XML文件作为源进行数据同步
- 新增支持JSON文件作为源进行数据同步
- MySQL作为源时支持指定增量时间点进行同步

### 功能优化

- 任务列表展示优化，新增展示任务的增量时间点，并支持排序
- 任务创建逻辑优化，Agent不可用时，无法创建新的开发任务
- 用户体验优化，用户选择分类后，会记住用户的分类选择
- 可观测日志展示方式优化，支持折叠和展开时自动格式化
- 源节点增量时间点推进逻辑优化，任务使用的表的增量时间点，应随着所在库的增量时间点进行持续推进
- 版本升级优化，支持不停服平滑升级，不会中断正在运行的任务

### 问题修复

- 修复了MySQL作为源，增量同步时报模型不存在导致解析失败的问题
- 修复了RDS MySQL作为源时，增量数据不同步的问题
- 修复了MongoDB分片集作为目标时，出现：Bulk write operation error, not find host matching read preference 报错导致无法正常写入的问题
- 修复了MySQL的gtid模式下，存在非监听表变更时不推进offset的问题
- 修复了其它的一些已知问题

## V2.10

### 新增功能

- 新增支持Custom Connection作为源和目标
- 在复制和开发可观测页面增加关联任务查看（目前仅能查看挖掘任务）
- 新增TiDB作为目标，并支持在TIDB上支持直接发布API
- 新增任务重置日志，重置超时可以基于日志查看超时原因。
- 新增任务告警功能，支持任务异常时进行通知

### 功能优化

- 数据源连接断开时支持自动重试
- ClickHouse作为目标时支持批量写入
- 可观测指标计算逻辑和展示方式优化，指标准确性提升
- 纯增量任务的增量时间点设置优化，无需指定计划开始时间也可以设置增量时间点

### 问题修复

- 已修复MySQL作为源的增量同步，时间类型字段同步到目标会多8个小时的问题
- 已修复Oracle作为源时，DDL同步到目标的字段长度不对的问题



## V2.9

### 已知问题

- 无主键的表在同步过程中会以全部字段作为主键在目标创建主键索引，可能会导致目标索引长度超过限制
- DDL同步功能目前仅支持MySQL，Oracle，DB2和PG，其中PG仅支持DDL应用不支持DDL输出。
- 数据校验功能，目前仅支持1:1复制，暂不支持添加处理节点，不支持动态新增表和DDL

### 新增功能

- 新增数据服务-服务管理功能
- 新增支持DM数据源，支持作为源和目标，支持全量和增量
- 新增数据发现功能，支持默认数据目录分类
- 新增支持mongo作为源和目标时，连接断开后的重试功能
- 新增支持Hive数据源作为目标
- 新增支持Kingbase数据源，支持作为源和目标，支持全量和增量
- 新增数据开发可观测能力，支持在运行监控页面查看任务运行关键指标和运行日志

### 功能优化

- 推演逻辑优化，推演完成后任务才可以进入运行中
- JS模型推演，改为异步推演方式

### 问题修复

- 修复了JS 推演结果丢字段的问题
- 修复了TM出现NPE的问题
- 修复了创建共享缓存后，缓存任务运行报错的问题
- 修复了创建共享挖掘任务后，挖掘任务运行报错的问题
- 修复了其他一些已知的缺陷



## V2.8

### 新增功能

* **复制任务校验**：用户可在创建复制任务时开启数据校验功能，系统会自动对原表和目标表的数据进行比对并反馈异常数据，任务正常运行后点击右上角校验按钮打开校验信息 。

  ![](images/release_notes_1.png)

* 动态新增表：用户可以在源节点的配置界面开启动态新增表功能，开启后系统会将源端新增加的表直接写到目标端

* 新数据源DB2：新增了DB2作为数据源，用户可以将其作为目标。

* 数据源MariaDB：新增了MariaDB作为数据源，用户可以将其作为目标

* 数据源RocketMQ：新增了RocketMQ作为数据源，用户可以将其作为目标 

* 新数据源Redis：新增了Redis作为数据源，用户可以将其作为目标 

### 功能优化

- 开发任务去掉子任务优化 
- 逻辑表与物理表拆分优化 
- 目标节点表映射关系优化 
- 目标节点默认值展示优化 
- Oracle裸日志功能优化 



### 问题修复

- 解决了共享挖掘任务报错的问题 
- 解决了主从合并节点无法选择关联条件，目标表字段为空的问题 
- 解决了oracle 测试连接，修改参数不生效的问题 
- 解决了MySQL到MySQL复制全量+增量，任务报错的问题 
- 解决了字段编辑节点中屏蔽的字段还是同步到了目标的问题 
- 解决了复制任务pg为源的增量时间点的时间显示有误的问题 
- 解决了RabbitMQ，数据源加载schema报错的问题 
- 解决了oceanbase作为目标update事件报错的问题



## V2.7

### 新增功能

* 表编辑节点：用户可在创建复制任务时可以添加表编辑节点对表名进行修改 
* 新数据源 SQLServer：新增了 SQLServer作为数据源，用户可以将其作为源或者目标
* 新数据源 Elasticsearch：新增了ES作为数据源，用户可以将其作为目标 
* 新数据源 OceanBase：新增了OceanBase作为数据源，用户可以将其作为目标

### 功能优化

- 共享缓存交互逻辑及配置优化 
- 连接信息说明内容优化 
- 创建任务字段类型选择优化 

### 问题修复

- 解决了Kafka数据源schema加载完成，数据模型与表不一致的问题 
- 解决了创建共享缓存任务报错的问题 
- 解决了oracle连接测试失败的问题 
- 解决了创建MySQL时连接会报错的问题 
- 解决了选择主从合并节点，属性设置中点击从表名，页面报错的问题 
- 解决了mysql-oracle全量+增量任务，启动后任务报错的问题