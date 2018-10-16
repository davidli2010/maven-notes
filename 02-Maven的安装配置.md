# 2. Maven的安装配置

## 2.1 安装目录分析

bin：mvn运行脚本

boot：自带类加载器

conf：settings.xml

lib：运行时类库

~/.m2

本地仓库：~/.m2/repository

## 2.2 配置用户范围settings.xml

$MAVEN_HOME/conf/settings.xml 全局范围

~/.m2/settings.xml 用户范围

## 2.3 设置HTTP代理

~/.m2/settings.xml

```XML
<proxies>
    <proxy>
        <id>my-proxy</id>
        <active>true</active>
        <protocol>http</protocol>
        <host>192.168.1.10</host>
        <port>3128</port>
        <!--
        <username>***</username>
        <password>***</password>
        -->
    </proxy>
</proxies>
```