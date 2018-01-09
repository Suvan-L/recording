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
+ 2018.01.08 【重构】修改 @ResponseBody 注解的使用范围，声明函数修改为声明类
+ 2018.01.09 【重构 + 新增】
    - 使用 @RestController 注解，取代 @Controller 和 @ResponseBody
    - 参数检查服务重命名(ParamCheckService -> ValidationService)
    - 优化 account，topic，count，file 的 api，修改注释与函数名，更加清晰直观
    - 使用 ThreadLocal，将公共参数提取出来（例如: request，response），在 api 过滤器中进行注入，优化 http 服务，全面修改相关类与接口