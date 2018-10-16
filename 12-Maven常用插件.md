# 12 Maven常用插件

## exec-maven-plugin

```XML
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>1.5.0</version>
    <configuration>
        <mainClass>com.sequoiadb.datascheduler.Launcher</mainClass>
    </configuration>
</plugin>
```

执行：

```bash
mvn exec:java
```

## maven-dependency-plugin

http://maven.apache.org/plugins/maven-dependency-plugin/index.html

maven-dependency-plugin最大的用途是帮助分析项目依赖，dependency:list能够列出项目最终解析到的依赖列表，dependency:tree能进一步的描绘项目依赖树，dependency:analyze可以告诉你项目依赖潜在的问题，如果你有直接使用到的却未声明的依赖，该目标就会发出警告。

maven-dependency-plugin还有很多目标帮助你操作依赖文件，例如dependency:copy-dependencies能将项目依赖从本地Maven仓库复制到某个特定的文件夹下面。

```XML
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-dependency-plugin</artifactId>
    <executions>
        <execution>
            <id>copy-dependencies</id>
            <phase>prepare-package</phase>
            <goals>
                <goal>copy-dependencies</goal>
            </goals>
            <configuration>
                <outputDirectory>${project.build.directory}/lib</outputDirectory>
                <includeTypes>jar</includeTypes>
                <includeScope>runtime</includeScope>
                <type>jar</type>
                <excludeTransitive>false</excludeTransitive>
            </configuration>
        </execution>
    </executions>
</plugin>
```

## maven-enforcer-plugin

http://maven.apache.org/enforcer/maven-enforcer-plugin/index.html

在一个稍大一点的组织或团队中，你无法保证所有成员都熟悉Maven，那他们做一些比较愚蠢的事情就会变得很正常，例如给项目引入了外部的SNAPSHOT依赖而导致构建不稳定，使用了一个与大家不一致的Maven版本而经常抱怨构建出现诡异问题。maven-enforcer-plugin能够帮助你避免之类问题，它允许你创建一系列规则强制大家遵守，包括设定Java版本、设定Maven版本、禁止某些依赖、禁止SNAPSHOT依赖。只要在一个父POM配置规则，然后让大家继承，当规则遭到破坏的时候，Maven就会报错。除了标准的规则之外，你还可以扩展该插件，编写自己的规则。maven-enforcer-plugin的enforce目标负责检查规则，它默认绑定到生命周期的validate阶段。

```XML
<plugins>
    <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-enforcer-plugin</artifactId>
        <version>1.4.1</version>
        <executions>
            <execution>
                <id>enforce-version</id>
                <goals>
                    <goal>enforce</goal>
                </goals>
                <configuration>
                    <rules>
                        <requireJavaVersion>
                            <version>1.7</version>
                        </requireJavaVersion>
                    </rules>
                </configuration>
            </execution>
        </executions>
    </plugin>
</plugins>
```

这个插件默认提供的规则有:
```
alwaysPass - Always passes... used to test plugin configuration. 
alwaysFail - Always fail... used to test plugin configuration. 
bannedDependencies - enforces that excluded dependencies aren't included. 
bannedPlugins - enforces that excluded plugins aren't included. 
dependencyConvergence - ensure all dependencies converge to the same version. 
evaluateBeanshell - evaluates a beanshell script. 
requireReleaseDeps - enforces that no snapshots are included as dependencies. 
requireReleaseVersion - enforces that the artifact is not a snapshot. 
requireMavenVersion - enforces the Maven version. 
requireJavaVersion - enforces the JDK version. 
requireOS - enforces the OS / CPU Archictecture. 
requirePluginVersions - enforces that all plugins have a specified version. 
requireProperty - enforces the existence and values of properties. 
requireFilesDontExist - enforces that the list of files do not exist. 
requireFilesExist - enforces that the list of files do exist. 
requireFilesSize - enforces that the list of files exist and are within a certain size range.
```