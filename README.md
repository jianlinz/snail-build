snail-build
=====
脚手架工具

- 编译工具[gradle-6.7.1](https://docs.gradle.org/current/userguide/userguide.html)
- 技术栈
    - gradle
        - plugin
        - bom
    - springboot

目录结构
=====

包名  |  作用
---- |-----
application | springBoot应用 application
bom | 本项目所有第三方jar包引用均强制要求在bom声明版本
build-conf | configuration.gradle 包含脚手架配置信息和模块依赖信息  dependencies.gradle简化依赖 统一声明依赖变量
gradle  | gradle-wrapper.properties 配置gradle版本信息
plugin | 引用的插件
plugin-source | 定义的插件
subprojects | 项目内容
gradle.properties | 基础配置信息
build.gradle | 全局构建脚手架
settings.gradle | 全局引用项目

如何使用
====
- 1.配置gradle.properties nexus参数
    - nexusUrl
    - nexusUsername
    - nexusPassword
    
- 2.其它配置
    - build-conf/configuration.gradle 中包含了 代码生成器配置 根据提示自行配置后执行gradlew :plugin:generator-tool:generate可代码生成
    - build-conf/configuration.gradle dependent_models配置依赖的模块
    
- 3.构建，发布到私服
    - gradlew clean
    - 不走单元测试 gradlew build -x test
    - gradlew upload
    
命令
====

- clean gradlew clean
- 发布bom gradlew :bom:{projectName}-dependencies:publish
- 发布plugin-source gradlew :plugin-source:{pluginName}:upload
- 打包
    - 走单元测试 gradlew build
    - 不走单元测试 gradlew build -x test
- 发布到私服 gradlew upload
- 代码生成 gradlew :plugin:generator-tool:generate