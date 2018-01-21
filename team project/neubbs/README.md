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
+ 2018.01.10【修改 + 重构】
  - 优化 controller/annotation 注包内，注解接口的 javadoc
  - 删除 'SwitchDataSourceHandler.java‘ 类，将其动态切数据源功能，移植到'DynamicDataSource'，SetConst 常量类谁知数据源名（云 + 本地）; 重命名 'DynamicDataSource'  -> 'DynamicSwitchDataSource'
+ 2018.01.11【重构】
  - 删除 controller/data 目录，移动文件至 controller/handler 目录重命名''DynamicSwitchDataSource' -> 'DynamicSwitchDataSourceHandler'
  - 重命名 'DecryptPropertyPlaceholderConfiguerHandler'-> 'DecryptConfigurationFileHandler'
  - 优化 'ApiInterceptor.java' ，调整代码结构与注释
  - 重命名 ‘ClientOnlineAccessListenert.java’ -> 'ClientListener.java', 重构代码，- 删除统计访问人数（vistUser）以及相关类的相关字段与函数调用，类变量 HashMap 修改为 ConcurrentHashMap（维护在线登陆用户 Session），新的客户端若请求 api，新建 Session，并加入 ConcurrentHashMap（哈希表）
+ 2018.01.13【重构】
  - 删除 ' PageJsonDTO.java' 和'PageJsonListDTO.java' ，整合成 'ApiJsonDTO.java' ，重新设计
  - 修改 'ApiJsonDTO.java’  的接口的 error( ) -> fail(), 修改 Account api 内相关代码
+ 2018.01.18【修改格式 + 重构】
  - 修改 utils 包下工具类  ‘PictureProcessingUtil.java'  的代码结构，使其通过 ’Neubbs Java CheckStyle‘ 代码规范检查
  - 优化 constant/log  包，新增 'LogWarnEnum.java'，尝试枚举类型定义日志常量，同时删除原 ’LogWarn.java‘，并修改相关的代码引用
  - 修改 ’RequestParamCheckUtil.java‘ 工具类，修改类变量名，见名知意 
+ 2018.01.19 【重构】
  - 优化 validation service，校验服务（参数验证），修改函数名和注释，合并部分函数，修改 controller/api 包下相关代码调用
+ 2018.01.20【重构】
  - 优化 'captcha service', 验证码服务，修改函数名和添加注释
  - 优化 ’email service‘ 邮件服务，修改相应函数名，部分行内注释转为 javadoc 注释
  - 优化 'file treat service' 文件处理服务，删除 'transferToServer()' 和 'compressFile()' 暂时无用到，后续需要使用时再加，修改部分函数与变量名
+ 2018.01.21 【重构】
  - 优化 ‘ftp service’，FTP  服务，删除 'getServerPersonalUserAvatorDirectoryPath()' 整合进''uploadUserAvatorImage()' , 修改其他函数名和注释，优化 'FtpUtil.java' ，FTP 工具类，删除 ‘keepConnect()’ 和 'getFTPClientInstance()'，修改相关函数调用，类变量 'FTPClient' 声明 volatile ，保证多线程可见性
  - 优化 'http service' http 请求服务，修改函数与注释，类 javadoc 加入函数名列表，在 ‘captcha, email, file treat, ftp service' 的类 javadoc 都加入函数名列表，'file treat service' 的 'checkUploadAvatarNorm()' 函数名修改为 'checkUserUploadAvatarNorm()'