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
+ 2018.02.13 【测试】
  - 'StringUtil.java' 字符串工具类，添加测试类 'StringUtilTest.java'，每个函数进行单元测试，完善注释说明
+ 2018.02.14 【重构】
  - 将 'TokenUtil.java' 功能复制到 'SecretUtil.java'
     - 修改 'SecretUtilTest.java'，添加新的测试方法，测试加解密用户信息 Token (JWT)  
     - 重写 UserDO 的 equals() 和 hashCode() 函数
     - SecretUtil.java' 的解密用户信息 Token 函数 `decryptUserInfoToken()` 若解密异常，不返回 null，直接向上抛出 'UntilClassException' 工具类异常
  - 删除 'TokenUtil.java'，修复相关代码调用，改为 'SecretUtil.java'，同时删除 'JwtUtilTest.java'
+ 2018.02.15 【修复 + 重构】
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
+ 2018.02.16 【修复 + 重构 + 测试】
  - 修复 `/api/account/state` 获取用户激活状态接口，model 返回数据异常，返回的不是期望类型`model:true`，应返回`model: {}`
    - 且重命名 'ApiJsonDTO.java' 的 `map() -> model()`，修复相关代码调用
  - 修复 `/api/account` 获取用户信息接口，model 内 state 字段属性值类型，表示用户激活状态（0-false，1-true）
  - 删除  'ApiJsonDTO.java' 的 `list()` 函数，修复相关代码，改为使用 `model()`
  - 修复 `/api/account/following` 和 `/api/account/followed` 两个接口的参数校验，参数校验时，传递 `check(ParamConst.USER_ID)` 修改为 `check(ParamConst.ID)`,直接检查 id 类型
  - 实现 `/api/account/following` 和 `/api/account/followed` 接口测试类函数，成功性测试，异常测试
+ 2018.02.17 【重构】
  - 重构 `/api/account/logout` 接口 mock 成功性和异常测试
+ 2018.02.18 【修复 + 重构】
  - 修复注册用户 BUG
    - 自动插入 'forum_user_action' 记录时，需输入用户id，Mybatis 在 输入 UserDO 实例，插入 'forum_user' 记录，会重写往对象中注入用户 id，所以应该把插入用户基本信息数据后，准备自动插入用户行为记录前，设置 UserActionDO 对象的 id
  - 修复 'FtpUtil.java' 完全删除目录，递归异常，删除中途突然断开连接 BUG，重写提炼删除函数，私有递归，单次连接执行删除文件及目录
  - 重构 `/api/account/register` 接口 mock 成功性和异常测试
    - 【补充修复】'FtpUtil.java' ftp 工具类，完全删除函数，删除初始目录
+ 2018.02.19 【修复 + 重构 + 新增】
  - 修复 'SecretUtil.class' 加密工具类的 `generateUserInfoToken()` 生成用户信息 Token 函数，加入空判断，若加密所需 UserDO 的某些属性为 null，则抛出 'UtilClassException' 工具类异常
  - 创建 'PermissionException.java' 权限异常，api 拦截器中，所有检查权限，若失败，抛出 'ServiceException' 修改为抛出此异常
  - 修复 'UserServiceImpl.java' 用户服务的 `alterUserProfile()` 修改用户个人信息函数，如果输入参数（birthday，position，description）为空，则注入 "" 空字符串，取消 null
  - 添加功能 'PatternUtil.java' 正则工具类，添加日期格式正则匹配检测（yyyy-MM-dd），并在 'ParamValidateUtil.java' 的正则检查集合策略中(typePatternMap) 添加 ParamConst.BIRTHDAY，用户出生年月日判断
    - 修复检测 'ParamValidateUtil.java' 参数校验 bug，若 allowEmptyTypeSet 中允许为空，则不在 `check()` 执行检查，直接跳过（不必对value = null 元素执行范围检查和正则检查）
  - 重构 `/api/account/update-profile` 修改用户基本信息接口，优化成功性测试，添加异常测试
+ 2018.02.21 【测试】
  - 优化 `/api/account/update-password` 修改密码接口测试
    - 优化成功性测试，异常测试
    - 补充注释，提取函数`getNoActivatedUserDO()` 和 `getOtherAlreadyLoginUserCookie()`
  - 修复 'AccountControllerTest.java'， 符号 bug（前一次提交问题）
+ 2018.02.22 【测试】
  - 优化 `/api/account/update-email` 修改邮箱接口测试
    - 优化成功性测试，异常测试
    - 'AccountControllerTest.java' 优化注释，异常测试函数，加入 [✔]
    - 删除不必要变量声明例如 `Throwable throwable = ne.getRootCause();`
+ 2018.02.23 【测试】
  - 优化 `/api/account/activate` 激活账户接口测试
    - 优化成功性测试，异常测试
    - 激活邮件内容修复
    - 成功性测试发送邮件，增加阻塞主线程最大限制时间 60 s，保证测试成功率
+ 2018.02.24【重构 + 测试 + 修复】
  - 优化 'SecretUtil.java' 加密工具类，加入参数空检测，若参数为空，则抛出指定异常
  - 优化 `/api/account/validate` 激活 token 验证接口测试
    - 优化成功性测试，异常测试
  - 修复 'HttpServiceImpl.java' 的 `saveCaptchaText()` 作用域保存验证码 BUG （request -> session）
  - 优化 `/api/account/captcha` 生成图片验证码接口测试
    - 优化成功性测试
    - 优化注释 
+ 2018.02.25 【测试 + 重构】
  - 优化 `/api/account/check-captcha`
    - 接口重命名为 `/api/account/validate-captcha`
    - 优化成功性测试，异常测试 
  - 优化 `/api/account/forget-password`
    - 优化成功性测试，异常测试
  - 重构 'IEmailService.java' 重构邮箱服务接口类
    - 修改 'EmailServiceImpl.java' 实现类，合并函数，只提供出发送激活邮件和充值临时密码邮件函数
    - 修改 'AccountController.java' 激活用户和忘记密码接口，修复相关代码调用
+ 2018.02.26 【重构 + 修复 +  测试】
  - 优化 'UserActionMapper.xml' 用户行为映射文件中
    - 修改查询用户喜欢，收场，关注话题，主动关注人，被动关注人的 SQL 语句 `resultMap(UserAction) -> resultType(java.lang.String)`，查询结果删除 'fu_id' 字段，并改相应的 'IUserActionDAO' 接口函数返回值，各个服务中的调用，以及 'UserActionDAOTest.java' 的 测试代码
  - 修复 'ApiExceptionHandler.java' 接口异常处理器，
    - 加入判断 'ClassCastException.java' 异常，当参数转换失败时（传入不符合类型参数），接口 message 字段返回 'incorrect input parameter' 提示信息，并删除异常栈的打印代码
  - 添加 `/api/account/following` 关注用户接口的单元测试
    - 成功性测试，异常测试
+ 2018.02.27 【修改格式 + 测试 + 重构】
  - 优化项目内函数注释，
    - 部分函数中 javaDoc 的参数注释后，中英文之间加入空格
  - 接口测试包中，将自定义工具函数分离，仅当前包使用
    - 重命名 'AccountCollectorTest.java' -> 'AccountControllerTest.java'
    - 从 'AccountControllerTest.java' 将私有函数抽离至 'ApiTestUtil.java'，功能复用
    - 修复 bug
      - 执行整个 'AccountControllerTest.java' 时，当执行到 `testFollowingUserSuccess()` 测试关注用户成功函数时，出现问题，数据源不可预料的切换到了云数据库，导致出现异常
      - 因为测试函数都是针对本地数据源的，所以若切换到云数据库则会出现不可预料异常，单个函数测试的时候无问题，但整个类测试时，出现问题
      - 【解决方法】 在初始化的 '@Before' 声明的 `setup()` 函数（每个测试函数执行前都会执行一次）中，加入动态切换数据源代码 `DynamicSwitchDataSourceHandler.setDataSource(SetConst.LOCALHOST_DATA_SOURCE_MYSQL);设置为本地 MySQL; 
      - 原本是只在 '@BeforeClass' 声明的 `init()` 函数中，进行指定当前线程的数据源
  - 优化 'CountControllerTest.java' 统计测试接口类函数
    - 优化 `/api/count` 论坛基数统计接口测试函数
    - 优化 `/api/count/online` 在线统计接口测试函数
    - 优化 `/api/count/user` 用户统计接口测试函数
  - 重构 'FileControllerTest.java' 文件接口测试类函数
    - 修改 `/api/file/avator` 上传用户头像接口
      - 重命名为 `...../avatar` ，
      - 请求参数名 `avatorImage` -> `avatarImageFile`
      - 加入限制 `consumes = "multipart/form-data"`
    - 删除 'IFileTreatService.java' 和 'FileTreatServiceImpl.java' 
      - 唯一的函数 `checkUserUploadAvatarNorm()` 检测上传文件规范，移动到 'IValidationService.java' 和 'ValidationServiceImpl.java'，修复相关代码调用，补充注释
      - 将 'LogWarnEnum.java' 中的 FS 常量删除，修改为 VS
    - 修改 'FtpServiceImpl.java' ftp 服务实现类，删除无用函数（功能重复了）
    - 修改 'FtpUtil.java' ftp 工具类，上传文件函数，加入不存在目录检测
    - 优化 `/api/file/avatar` 上传用户头像接口测试函数
      - 成功性测试，异常测试
    - 删除文件接口测试类中私有函数，改为调用公共函数工具类
+ 2018.02.28 【重构】
  - 优化 '/api/topic' 获取话题信息接口函数
    - 'TopicControllerTest.java' 话题接口测试类，函数私有函数移动到 'ApiTestUtil.java' 接口测试工具类
    - 'ApiTest.Util.java' 添加 ` confirmMapShouldHavaKeyItems()` 确认 Map 具备指定选项函数
    - 'IUserService.java' 的 `isUserLikeTopic()` 函数取消验证用户存在性，修复其接口实现类
    - 修改'TopicController.java' 的 `getTopicInfo()` 函数，优化注释，修改部分变量名，调整代码顺序
    - 优化 '/api/topic' 接口的单元测试，仅保留三种测试，二种成功性（阅读数增加，阅读数不变），异常测试