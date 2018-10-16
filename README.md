# Maven Practice Notes

## **ATTENTION**

This document is only for self-learning, **DO NOT USE** for any commercial purpose!!! 

请勿用于商业目的！！！

## Reference
  - [Maven实战](https://book.douban.com/subject/5345682/)

## Contents

- [1 Maven简介](01-Maven简介.md)
  - 1.1 Maven是什么？
  - 1.2 为什么需要Maven？
- [2 Maven的安装配置](02-Maven的安装配置.md)
  - 2.1 安装目录分析
  - 2.2 配置用户范围settings.xml
  - 2.3 设置HTTP代理
- 3 [Maven入门](03-Maven入门.md)
  - 3.1 编写POM
  - 3.2 编写主代码
  - 3.3 编写测试代码
  - 3.4 打包和运行
- 4 [坐标和依赖](04-坐标和依赖.md)
  - 4.1 坐标
  - 4.2 依赖配置
  - 4.3 依赖范围
  - 4.4 传递性依赖
  - 4.5 依赖调解
  - 4.6 可选依赖
  - 4.7 优化依赖
- 5 [仓库](05-仓库.md)
  - 5.1 仓库的布局
  - 5.2 仓库的分类
  - 5.3 配置远程仓库
  - 5.4 快照版本
  - 5.5 从仓库解析依赖的机制
  - 5.6 镜像
  - 5.7 仓库搜索服务
- 6 [生命周期和插件](06-生命周期和插件.md)
  - 6.1 生命周期详解
  - 6.2 插件目标
  - 6.3 插件绑定
  - 6.4 插件配置
  - 6.5 从命令行调用插件
  - 6.6 插件解析机制
- 7 [聚合与继承](07-聚合与继承.md)
  - 7.1 聚合
  - 7.2 继承
  - 7.3 聚合与继承的关系
  - 7.4 预定优于配置
  - 7.5 反应堆
- 8 [使用Maven进行测试](08-使用Maven进行测试.md)
  - 8.1 maven-surefire-plugin
  - 8.2 跳过测试
  - 8.3 动态指定要执行的测试用例
  - 8.4 包含与排除测试用例
  - 8.5 测试报告
- 9 [版本管理](09-版本管理.md)
  - 9.1 Maven的版本号定义约定
- 10 [灵活的构建](10-灵活的构建.md)
  - 10.1 Maven属性
  - 10.2 资源过滤
  - 10.3 Maven Profile
- 11 [向中央仓库发布软件包](11-向中央仓库发布软件包.md)
  - [GPG key generation: Not enough random bytes available.](11-01-GPG没有足够的随机字节生成key.md)
- 12 [Maven常用插件](12-Maven常用插件.md)
  - exec-maven-plugin
  - maven-dependency-plugin
  - maven-enforcer-plugin
