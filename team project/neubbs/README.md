# Neubbs 项目

## 待完成目标
+ 重构代码（功能代码 + 单元测试）
+ 环境脚搭建，尝试 Docker 部署应用程序
+ 消息通知功能开发
+ 日志系统
+ 用户回复列表,喜欢话题列表，关注列表，需做分页
+ 缓存模块构建
+ Mybatis sql 语句优化，mapping 文件减少，尝试通用 mapping
+ 安全优化，加密优化


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
+ 2018.01.22 【重构】
  - 删除 'page display service' 业务接口和实现类
  - 修改 'random service' 接口，添加部分注释
  - 优化 'redis service' redis 服务，删除无用函数，修改部分函数名与注释，删除 service 测试包（包含 Redis 测试类），直接对 api 测试，暂时不进行 service 测试，‘redis service’ 重命名为 'cache service', 修改相关调用和代码
+ 2018.01.23 【重构】
  - 优化 'secret service'  加密服务，修改函数名和注释，‘getUserInfoByAuthentication()’ 通过 authentication 获取用户信息，删除 key 传递参数（直接在函数内写入），修复各个接口相关代码调用
+ 2018.01.24 【重构】
  - 优化 'topic service'  话题服务，删除无用函数，修改部分函数名，添加注释
+ 2018.01.26 【修改代码格式】
  - 修改 'ITopicService.java' 添加类注释，展示话题服务函数列表
+ 2018.01.27 【重构】
  - 优化 'user service' 用户服务，修改函数名，整理函数，提取重复代码放置函数中，添加类注释（展示用户服务函数列表）
+ 2018.01.28 【重构】
  - 优化 'validation service' 校验服务，优化函数代码，修改部分函数名，添加类注释（展示校验服务函数列表）
+ 2018.01.29【修改代码格式 + 重构】
  - 修改 'AnnotationUtil.java' 注解工具类注释
   - 修改 'CookieUtil.java' Cookie工具类注释，删除 'isExistCookie()',添加类注释（展示 Cookie 工具类函数列表） 
+ 2018.01.30【修改代码格式 + 修复】
  - 修改 'FtpUtil.java' FTP工具类，static 静态块中删除 'connect()' 操作，修复 'delete()' 函数 ，若删除目录（第二参数为空），无法释放 ftp 连接 的 bug
+ 2018.01.31 【重构】
  - 优化 'json util class' JSON格式处理工具类，函数名优化，代码格式整理，删除不必要引用，完善注释，修复相关服务类的代码调用
  - 修改项目根目录 'README.md' 文档，重新定义 [后端 API 交互协议] 链接地址（原本已失效）
+ 2018.02.01【重构】
  - 优化 'jwt token util class' 口令工具类，改名为 'token util class'，删除只引用一次的对象，合并代码行，简化函数调用，修改函数名，解密函数不再需要输入密钥，修复相关的代码调用
+ 2018.02.02 【重构】
  - 优化 'map filter util class' 键值对过滤工具类，优化注释，修改 'filterTopicInfo()' 函数，删除最后回复时间替换功能代码（若查询 lastRelyTime 为 null， 则替换为话题发布时间）（已经由 sql 脚本在，初始化数据表时，forum_topic 的 'ft_lastreplytime' 设置好 Default Value）
  - 优化 'pattern util class' 正则匹配工具类，提取重复代码至单一函数，正则变量名优化，优化注释
+ 2018.02.03 【修改数据脚本 + 说明书】
  - 修改数据库脚本，实现"建库，建表，重复执行则清空"，优化注释，重命名 'initBuildForumDataTables.sql' -> 'InitNeubbsForumDatabase.sql' 和 initInsertTestDataScipt.sql'  -> 'InsertTestData.sql' 
  - 修改 java 后端开发说明书，'src\main\java\README.md'，重新规范说明和规划目录机构
  - 修改根目录 'README.md'，重新整理
+ 2018.02.04 【修改代码格式 + 重构】
  - 优化 'public params util class' 公共参数工具类，修改注释，添加函数列表说明
  - 重构 'random util class' 生成随机数工具类，删除无用函数，重命名函数，优化 `generateRandomNumbers()` 和 `generateRandomString()`
+ 2018.02.05【修改代码格式 + 重构 + 测试相关】
  - 优化 'setConst.java' 设置常量类，优化注释，删除无意义常量（例：public static final int ONE = 1），分隔不同类型常量，添加类说明
  - 优化 'request params check util class' 请求参数检查工具类，重命名为 'ParamValidate.java'，删除 'check(Map)' 检查器（重载类型 2），优化代码结构（静态变量-静态代码块-私有静态内部类-公共函数-私有函数），优化注释（删除不清晰语义注释，修正错别字，补充部分注释，每个代码层添加分隔注释）
  - 修复部分测试类错误命名
+ 2018.02.06 【重构】
  - 删除 'ResponsePrintWriterUtil.java' 响应输入工具类，因为只有 'ApiExceptionHandler.java' 用到，所以唯一的函数 outFailJSONMessage()'' 直接移植过去，删除不必要注释，构造有序哈希 Map 直接初始面积 = 3，内置 "model" 字段  HashMap 构造长度修改位0（空对象即可）
+ 2018.02.07 【重构】
  - 优化 'SecretUtil.java' 工具类
    - 删除暂时无用的 AES 加解密函数，二进制转十六进制函数
    - 修改函数名与注释，修改相关代码调用
    - 优化 MD5 加密函数
    - 'encryptUserPassword()' 函数移动至 'UserServiceImpl.java'，成为私有函数，相关其余的代码调用修复（服务之间不进行相关调用，降低耦合）
    - 新增 'SecretFailException.java' 标记加密失败异常（若工具类加密和解码失败，重新包装成此异常然后向上抛出）
    - 'LogWarnEnum' 日志提醒枚举类添加 UC（Util Class) 类型，是哟管工具类的异常
    - 修改 'SeecretUtilTest.java' 工具测试类，每个函数单独测试，删除无用函数测试，优化注释，修复相关代码
  - 优化 'SendEmailUtil.java' 工具类，
    - 部分静态常量移动到 'SetConst.java' 设置常量类
    - 修改函数名 'sendEmail()' -> 'send()'，优化注释
    - 新增 'UtilClassException.java' 工具类异常，读取配置文件若出现 IO 异常包装后抛出
  - 优化 'StringUtil.java' 字符串工具类
    - 静态块修改为读取  neubbs.properties 函数（原本是通过配置类 NeubbsConfigDO.java）
    - 修改部分函数名，修改注释
    - 优化 'spliceUserAvatorUrl()' 函数代码，if 判断用三目运算符改写，不使用 StringBuilder 拼接字符串，删除相关的私有函数，合并到唯一函数，重命名为 'generateUserAvatarUrl()'
+ 2018.02.08 【重构 + 修复 + 删除】
  - 删除 'AnnotationUtil.java' 和 'AnnotationUtilTest.java' ，修复相关调用
  - 修复 'FtpUtil.java'  bug
    - 无法连接服务器异常（读取配置文件时加入 Base64 解码操作）
    - 操作 ftp 服务器异常（连接时需调用 'FtpClient.enterLocalPassiveMode()' 开通端口传输数据
    - 部分操作若失败抛出自定义异常，'FileUploadFailException.java' 重命名为 'FtpException' 
  - 重构 'FtpUtilTest.java' 重构 ftp 测试代码
  - 删除部分异常类，整合成 'service exception' 和 'util class exception'
    - 删除 SecretException.java' 加密失败异常，修复相关代码，变为 'UtilClassException.java'
    - 'AccountErrorException.java' 重命名为 'ServiceException.java' 业务异常
    - 删除 'TokenErrorException' 口令失败异常，修复相关代码，变为 'UtilClassException.java' 或者 'ServiceException.java'
    - 删除 'FtpServiceErrorException.java' ftp服务异常，修复修复相关代码，变为 'ServiceException.java
    - 删除 'DatabaseOperationFailException.java' 数据操作异常，修复相关代码调用为 'ServiceException.java'
    - 删除 'TopicErrorException.java' 话题错误异常，修复相关代码调用为 'ServiceException'  
  - 重构工具类测试用例
    - 优化 'JsonUtilTest.java'  
    - 新建 'MapFilterUtilTest.java'，测试键值对过滤工具类
+ 2018.02.09 【文档】
  - 更新项目说明，添加项目 logo，图片放置(./src/main/webapp/resources/images/neubbs.jpg) 
  - 重构 'ParamValidateUtil.java' 参数校验工具测试类
+ 2018.02.10 【重构】
  - 重构 'PatternUtilTest.java' 正则工具测试代码
+ 2018.02.11 【重构】
  - 重构 'RandomUtilTest.java' 随机数工具测试代码
  - 重构 'SecretUtilTest.java' 加密工具测试代码
+ 2018.02.12 【重构 + 修复 Bug】
  - 重构 'SendEmailUtilTest.java' 发送邮件工具测试代码'
  - 修复不能注销 Bug，修改 'ApiJsonDTO' 
    - 构造函数 mode 字段默认不要设置为 new Object，修改为设置 new HashMap<>(0)
    - 'CookUtil.java' Cookie 工具类，获取 Cookie 值，加入异常判断，若在 HTTP Request Headers 中未获取到 Cookie ，抛出异常
- 2018.02.13 【测试】
  - 'StringUtil.java' 字符串工具类，添加测试类 'StringUtilTest.java'，每个函数进行单元测试，完善注释说明
- 2018.02.14 【重构】
  - 将 'TokenUtil.java' 功能复制到 'SecretUtil.java'
     - 修改 'SecretUtilTest.java'，添加新的测试方法，测试加解密用户信息 Token (JWT)  
     - 重写 UserDO 的 equals() 和 hashCode() 函数
     - SecretUtil.java' 的解密用户信息 Token 函数 `decryptUserInfoToken()` 若解密异常，不返回 null，直接向上抛出 'UntilClassException' 工具类异常
  - 删除 'TokenUtil.java'，修复相关代码调用，改为 'SecretUtil.java'，同时删除 'JwtUtilTest.java'
- 2018.02.15 【修复 + 重构】
  - 修复 'ValidationServiceImpl.java' 的 `checkUsername()` 参数为空，不超过那你vhbhkbhlbk.jll.bj.kklbk,        你，bk/sasaasassssssssssssssssssssssssssssssssssssssssssssssssssssss抛出 'NullPointerException' 空指针异常 Bug，加入判断，提前处理异常
  - 修复 'ApiExceptionHandler.java' API 异常处理器内，打印日志函函数 `printApiExceptionToLocalLog()` ，若抛出异常时，并未链式调用 `.log(LogWarnEnum)`，则枚举类为空，获取枚举类的错误信息字符串时，抛出控制针异常 Bug
    - 主要针对在异常跑出前直接使用 `log.warn(...)`，并不链式调用的情况
    - 加入 null 判断，预防控制针异常情况
  - 重构 'AccountControllerTest.java' 账户接口测试类
    - 私有函数优化，移动到类的最下方，并添加分隔符
    - 优化 @Before 标识的 `setup()` 函数，初始化 MockMvc 实例，添加过滤器，上下文内的`LOGIN_USER` 属性
    - 优化 `/api/account`，`/api/account/state` 和 `/api/account/login` 接口的测试函数
    - 删除已优化接口测试函数类变量，接口定义，定义至函数内，保证测试用例之间的隔离性
    - 新增 `/api/account/following` 和 `/api/account/followed` 接口测试函数，先定义，未实现