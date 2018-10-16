# 3. Maven入门

## 3.1 编写POM

POM: Project Object Model

定义项目基本信息，描述项目如何构建，声明项目依赖

```XML	
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
 
    <groupId>com.sequoiadb</groupId>
    <artifactId>hello-world</artifactId>
    <version>1.0-SNAPSHOT</version>
    <name>Maven Hello World Project</name>
</project>
```
 
## 3.2 编写主代码

src/main/java/com/sequoiadb/helloworld/HelloWorld.java

```Java
package com.sequoiadb.helloworld;
 
public class HelloWorld {
    public String sayHello() {
        return "Hello Maven";
    }
 
    public static void main(String[] args) {
        System.out.println(new HelloWorld().sayHello());
    }
}
```

```bash
mvn clean compile
```

设置源文件编码格式

```XML
<build>
    <plugins>
        <plugin> 
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.6.0</version>
            <configuration>
                <source>1.7</source>
                <target>1.7</target>
                <encoding>UTF-8</encoding>
            </configuration>
        </plugin>
    </plugins>
</build>
```
 

执行

```XML
<build>
    <plugin> 
        <groupId>org.codehaus.mojo</groupId> 
        <artifactId>exec-maven-plugin</artifactId> 
        <version>1.5.0</version> 
        <executions> 
            <execution> 
                <goals> 
                    <goal>java</goal> 
                </goals> 
            </execution> 
        </executions> 
        <configuration> 
            <mainClass>com.sequoiadb.helloworld.HelloWorld</mainClass> 
        </configuration> 
    </plugin>
</build>
```

```
mvn exec:java
```

## 3.3 编写测试代码

添加JUnit依赖

```XML
<dependencies>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

src/test/java/com/sequoiadb/helloworld/HelloWorldTest.java

```XML
package com.sequoiadb.helloworld;
 
import static org.junit.Assert.assertEquals;
import org.junit.Test;
 
public class HelloWorldTest {
    @Test
    public void testSayHello() {
        HelloWorld helloworld = new HelloWorld();
        String result = helloworld.sayHello();
        assertEquals("Hello Maven", result);
    }
}
```

```bash
mvn clean test
```

## 3.4 打包和运行

打包：

```
mvn clean package
```

target/hello-world-1.0-SNAPSHOT.jar

默认生成的jar不能直接运行，添加Main-Class到manifest中

```
<build>
    <plugins>
        <plugin> 
            <groupId>org.apache.maven.plugins</groupId> 
            <artifactId>maven-jar-plugin</artifactId>
            <version>3.0.2</version>
            <configuration> 
                <archive> 
                    <manifest> 
                        <mainClass>com.sequoiadb.helloworld.HelloWorld</mainClass> 
                    </manifest> 
                </archive> 
            </configuration> 
        </plugin>
    </plugins>
</build>
```

安装到本地仓库：

```
mvn clean install
```