# 仓库管理系统


## 开发日志
- 2018.03.26 凌晨 00:37 开始记录，基于分布式 zheng 框架进行架构，构建项目基础模块，上传 GitHub
- 2018.03.26 晚 ~ 2018.03.27 凌晨
  - 修改配置文件，连接本地：Reids 和 MySQL ，修改相应密码（密文）
  - 將 "张恕征" 修改为“刘淑玮”， zheng-master 更名为 zheng-introduce，存放框架介绍
- 2018.03.28 凌晨
  - 修改前端 index.html 页面，删除部分信息，主要 “通用”  -> "仓库"
- 2018.03.29 凌晨
  - 删除 zheng-oss，zheng-pay，zheng-wechat，zheng-shop 模块
    - 修改部分前端页面，加入 “仓库”
- 2018.04.01
  - 全面修改 zheng -> wms ，删除无用模块（pay, show, wechat，ucenter），提取 sql 语句，分为构建表，和插入测试数据，删除无用表，修改项目，并进行运行测试（成功）
- 2018.04.07
  - 重新设计数据库表（用户权限与仓库库存）与设计测试数据，并重新构建 sql 构建脚本
  - 修改 upms 和 cms 系统的 mybatis 逆向生成工具类（zheng -> wms），修复路径中有中文名就无法生成 generatorConfig.xml 的 bug
  - 修改 commen 包下关于 Controller，Service 的 vm 模板（路径：D:\java\Intellij IDEA\project\wms\wms-common\src\main\resources\template\\*.vm）
  - 对 cms 模块执行逆向操作，生成 Service，并修改部分日期注释为 `suvan on 2018/04/06`
  - 修改测试数据，加入不同角色用户，修改相关的 *.sql 脚本
  - 添加自设计项目的  'wms’ logo
  - 修改 wms-upms 后台管理页面 `index.jsp` 页面
  - 删除项目后端代码内部分注释 
- 2018.04.08 
  - 【凌晨】添加仓库库存管理框架（模块构建好，功能未完全实现）
- 2018.04.09
  - 修改项目文档说明，新增  'wms-resources' 目录，存放设计图
- 2018.05.29
  - 尝试开启邮件阀值监控，单线程邮件发送成功，wms 项目 maven 重新 install 成功（解决 ClassNoException 问题） 
- 2018.05.30
  - 修改发送邮件工具类（SendEmailUtil.java），增加线程池，异步发送
  - 修改  'CmsWarehouseCapacityController' 仓库容量接口，仅当当容量达到预设阀值 90% 时，才发送提醒邮件至 liushuiwei0925@gmail.com
  - 修改项目根目录 README.md ，邮件提醒功能 ，完成库存阀值提醒
