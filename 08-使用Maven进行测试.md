# 8. 使用Maven进行测试

## 8.1 maven-surefire-plugin

Maven的测试执行器，兼容JUnit和TestNG。

在默认情况下，maven-surefire-plugin的test目标会自动执行测试源码路径（默认为src/test/java/）下所有符合一组命名模式的测试类。

这组模式为：
- `**/Test*.java`：任何子目录下所有以Test开头的Java类。
- `**/*Test.java`：任何子目录下所有命名以Test结尾的Java类。
- `**/*TestCase.java`：任何子目录下所有命名以TestCase结尾的Java类。

## 8.2 跳过测试

```bash
mvn package -DskipTests
```

不仅跳过测试运行，还想跳过测试代码的编译

```bash
mvn package -Dmaven.test.skip=true
```

## 8.3 动态指定要执行的测试用例

maven-surefire-plugin提供了一个test参数让Maven用户能够在命令行指定要运行的测试用例。

执行执行RandomGeneratorTest测试类：

```bash
mvn test -Dtest=RandomGeneratorTest
```

执行所有以Random开头、Test结尾的测试类：

```bash
mvn test -Dtest=Random*Test
```

还可以使用逗号指定多个测试用例：

```bash
mvn test -Dtest=RandomGeneratorTest,AccountCaptchaServiceTest
```

也可以结合使用星号和逗号：

```bash
mvn test -Dtest=Random*Test,AccountCaptchaServiceTest
```
test参数的值必须匹配一个或者多个测试类，如果找不到任何匹配的测试类，就会报错并导致构建失败。

```bash
mvn test -Dtest
```

加上-DfailIfNoTests=false，告诉maven-surefire-plugin即使没有任何测试也不要报错：

```bash
mvn test -Dtest -DfailIfNoTests=false
```

## 8.4 包含与排除测试用例

```XML
<plugin>
    <groupId>org.apache.maven.plugins</groupId> 
    <artifactId>maven-surefire-plugin</artifactId>
    <version>2.19.1</version>
    <configuration>
        <includes>
            <include>**/*Tests.java</include>
        </includes>
        <excludes>
            <exclude>**/*ServiceTest.java</exclude>
        </excludes>
    </configuration>
</plugin>
```

## 8.5 测试报告

默认情况下，maven-surefire-plugin会在项目的target/surefire-reports目录下生成两种格式的错误报告：

简单文本格式

与JUnit兼容的XML格式
