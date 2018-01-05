# Neubbs 项目

## 待完成目标
+ resources/redis.properties 文件多余内容
+ 用户回复列表,喜欢话题列表，关注列表，需做分页
+ 环境脚本搭建，尝试 dockie 
+ 消息通知功能开发
+ 重构代码
+ 日志系统
+ 异常体系
+ 邮箱 HTML 传入值
+ 单元测试补齐
+ Mybatis sql 语句优化，mapping 文件减少，尝试通用 mapping


## 开发记录
+ 2018.01.03 开始记录，之前已经 400 次 commit（未记录）
+ 2018.01.03 【重构】ParamCheckService.check() 修改为链式调用，修改位于 api 包内，相关的调用代码
+ 2018.01.05 【新增】
	- 针对 jdbc.properties 和 neubbs.properties 配置文件的'password'字段进行加密（目前 Base64），
	- 定义处理器，继承 Spring 的 PropertyPlaceholderConfigurer，重写 convertProperty() 函数 读取配置文件的时进行转码解密