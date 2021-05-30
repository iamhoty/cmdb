# open-falcon

## 架构详解

![Snipaste_2020-12-06_17-40-29](/Users/yutang/Documents/运维开发/asset/Snipaste_2020-12-06_17-40-29.png)

绿色部分：

​	数据的采集、传输、存储

​	**collector（agent）**部署到目标机器上去，采集目标机器的cpu、内存、磁盘io、网络等信息

​		collector采集到数据会推送到server端也就是transfer来接收数据，中间是tcp的长连接。

​		**plugin** 扩展机制，采集插件，可以根据自己的需求采集指定的目标机器信息

​		**log** 根据log采集日志中根据正则匹配的日志指标

​		**sdk**

​	**transfer** 可以水平扩展，collector中可以配置多个transfer的地址。将数据推给tsdb和judge。

​	**tsdb** 存储transfer传来的数据

​	**index** 索引模块	

红色部分：

​	告警引擎

​	**judge** transfer将用来做告警判断的数据推送给judge。接收的数据偏小。可以部署多个，处理告警策略。judge会判断报警，如果出发阈值之后会生成一条event数据，然后推送pull给redis。

​	**redis** 可以部署多个，其中一个redis挂掉后，judge会推送给另一个redis。将alarm传来的alert告警信息发送给配置的短信、微信、邮箱中。

​	**monitor_api（alarm）** 从redis中pop拉取event数据，将redis当成一个队列来处理。将event存入数据库中，并补充告警信息，再回推给redis一条alert信息。

紫色部分：

​	用户接口的api

​	**monitor_api（portal）** 用户可以配置告警策略，查询获取告警信息等。