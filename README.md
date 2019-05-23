![image.png](http://ata2-img.cn-hangzhou.img-pub.aliyun-inc.com/9e7048ef11db23b0579a439676dec4c9.png)

# COLA架构
<strong>COLA是Clean Object-Oriented and Layered Architecture的缩写，代表“整洁面向对象分层架构”，也叫“可乐”架构。</strong>
>注意本架构曾用名SOFA、COPA，以后统一使用COLA这个新名称，带来不便，表示抱歉

更多关于COLA架构的信息：
- COLA架构的设计思想和原理：[请点击](https://blog.csdn.net/significantfrank/article/details/85785565)
- 领域建模的方法论：[请点击](http://blog.csdn.net/significantfrank/article/details/79614915)

需要进一步交流的，可以微信咨询： josico-nie

# 项目说明
COLA框架包括两个Project，一个是cola-framework里面是框架的核心代码，另一个是cola-archetype是用来生成新应用的Maven Archetype源码。
## cola-framework Project
该Project包含3个Module，cola-core, cola-common, cola-test
### cola-core
该Module是整个框架的核心，里面的主要功能和Package如下：
```
com
└── alibaba
    └── cola
        ├── assembler  \\提供Assembler标准
        ├── boot \\这是框架的核心启动包，负责框架组件的注册、发现
        ├── command  \\提供Command标准
        ├── common
        ├── context  \\提供框架执行所需要的上下文
        ├── convertor  \\提供Convertor标准
        ├── domain  \\提供Domain Entity标准
        ├── event
        ├── exception \\提供Exception标准
        ├── extension  \\负责扩展机制中的重要概念-扩展(Extension)的定义和执行
        ├── extensionpoint  \\负责扩展机制中的重要概念-扩展点(Extension Point)的定义
        ├── logger  \\提供DIP的日志接口
        ├── repository  \\提供仓储（Repository）的标准
        ├── rule  \\提供业务规则或者叫策略（Rule）的标准和执行
        │   └── ruleengine
        └── validator  \\提供Validator标准和执行
```
### cola-common
该Module提供了框架中Client Object, Entity Object和Data Object的定义，二方库会依赖该Module。
### cola-test  
该Module主要是提供一些开发测试的工具，可以使用TDD来进行开发。

## cola-archetype Project
为了提升应用创建的效率，以及保证架构风格和规范被准守。我们开发了创建应用的Maven Archetype，这样只要执行一行命令就可以生成一个基于COLA框架的应用骨架来。

可以按照以下步骤使用COLA Archetype：

1. 下载Archetype

2. 安装Archetype到本地：运行 mvn install

3. 生成应用，比如，要生成一个名为demo应用，只要执行下面的maven 命令：
```
mvn archetype:generate  -DgroupId=com.alibaba.sample -DartifactId=demo -Dversion=1.0.0-SNAPSHOT -Dpackage=com.alibaba.sample -DarchetypeArtifactId=cola-framework-archetype -DarchetypeGroupId=com.alibaba.cola -DarchetypeVersion=1.0.0-SNAPSHOT
```

4. 启动SpringBoot，首先在demo目录下运行mvn install（如果不想运行测试，可以加上-DskipTests参数）。然后进入start目录，执行mvn spring-boot:run。
运行成功的话，可以看到SpringBoot启动成功的界面

5. 执行测试，生成的应用中，已经实现了一个简单的Rest请求，可以在浏览器中输入 http://localhost:8080/customer?name=World 进行测试。

6. 请求执行成功的话，可以在浏览器中的返回值中看到："customerName":"Hello, World"。同时观察启动SpringBoot的控制台，可以看到LoggerInterceptor打印出来的日志。

查看生成的demo应用，我们可以看到生成了5个module，分别是demo-controller、demo-client、demo-app、demo-domain、demo-infrastructure。其中demo-client是用来存放RPC调用中的DTO（Data Transfer Object）类，其它四个module分别对应控制层、应用层、领域层和基础实施层。。
