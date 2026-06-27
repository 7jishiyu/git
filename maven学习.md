# Maven

> 一款用于管理和构建Java项目的工具，是apache旗下的一个开源项目
> 
> 作用：
> 
>     -- 依赖管理：方便快捷的管理项目依赖的资源（jar包）
> 
>     -- 项目构建：标准化的跨平台（Linux、Windows、Mac0S）的自动化项目构建方式
> 
>     -- 统一项目结构：提供标准、统一的项目结构    

## 依赖管理

![4225f66a-3846-47f6-a9b2-23b89fbd669d](file:///C:/Users/Jsy/Desktop/Pictures/Typedown/4225f66a-3846-47f6-a9b2-23b89fbd669d.png)

## 项目构建

![198cfdde-9b58-47c6-8232-a9f8022ab73d](file:///C:/Users/Jsy/Desktop/Pictures/Typedown/198cfdde-9b58-47c6-8232-a9f8022ab73d.png)

## 统一项目结构

![66f10e70-47c1-4565-85f8-6858e22f80fe](file:///C:/Users/Jsy/Desktop/Pictures/Typedown/66f10e70-47c1-4565-85f8-6858e22f80fe.png)







# 概述

## 介绍

> Apache Maven 是一个项目管理和构建工具，它基于项目对象模型（POM）的概念，通过一小段描述信息来管理项目的构建。
> 
> 作用：
> 
>     -- 方便的依赖管理
> 
>     -- 标准的项目构建流程
> 
>     -- 统一的项目结构



注：POM -- project object model

## 仓库

> ：用于存储资源，管理各种jar包
> 
> 中央仓库：由Maven团队维护的全球唯一的。仓库地址：https://repo1.maven.org/maven2/
> 
> 远程仓库（私服）：一般由公司团队搭建的私有仓库

![d03c8714-ad99-4971-b105-c99016fdc8ad](file:///C:/Users/Jsy/Desktop/Pictures/Typedown/d03c8714-ad99-4971-b105-c99016fdc8ad.png)

## 安装

> 安装步骤
> 
>     -- 解压 安装包
> 
>     -- 配置本地仓库：修改 conf / settings.xml 中的 <localReposiroty> 为一个指定目录。
> 
> ```java
> <localRepository> C:\develop\apache-maven-3.9.4\mvn_repo</localRepository>
> ```
> 
>     -- 配置阿里云私服：修改 conf / settings.xml 中的 <mirrors>标签，为其添加如下子标签
> 
> ```java
> <mirror>
>     <id>alimaven</id>
>     <name>aliyu maven</name>
>     <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
>     <mirrorOf>central</mirrorOf>
> </mirror>
> ```
> 
>     -- 配置环境变量：MAVEN_HOME 为maven的解压目录，并将其bin目录加入PATH环境变量





# IDEA集成Maven

## 创建Maven项目

未补充......



## Maven坐标

> Maven中的坐标是资源（jar）的唯一标识，通过该坐标可以唯一定位资源位置。
> 
> 使用坐标来定义项目或引入项目中需要的依赖。

### 组成

> groupId：组织名称（通常为域名反写）
> 
> artifactId：模块名称
> 
> version：版本号

### Maven项目的版本分类

> SNAPSHOT：功能不稳定、尚处于开发中的版本，即快照版本
> 
> RELEASE：功能趋于稳定、当前更新停止，可以用于发行的版本

 

## 导入Maven项目

> 方式一：File --> Project Structure --> Modules --> Import Module --> 选择maven项目的pom.xml
> 
> 方式二：Maven面板 --> +（Add Maven Projects）--> 选择maven项目的pom.xml





# 依赖管理

> 依赖：指当前项目运行所需要的jar包，一个项目中可以引入多个依赖。
> 
> 配置：
> 
>     -- 1.在pom.xml中编写<dependencies>标签
> 
>     -- 2.在<dependencies>标签中，使用<dependency>引入坐标
> 
>     -- 3.定义坐标的 groupId,artifactId,version
> 
>     -- 4.点击刷新按钮，引入最新加入的坐标



## 依赖传递



## 排除依赖

> 指主动断开依赖的资源，被排除的资源无需指定版本
> 
> <exclusion></exclusion>

```java
<dependency>
    <groupId>com.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>6.1.4</version>

    <exclusions>
            <exclusion>
                <artifactId>io.micrometer</artifactId>
                <groupId>micrometer-observation</groupId>
            </exclusion>   
    </exclusions>
    
</dependency>
```

## 注意事项：

> 一旦依赖配置变更了，记得重新加载
> 
> 引入的依赖本地仓库不存在，记得联网    





# 生命周期

> Maven的生命周期就是为了对所有的maven项目构建工程进行抽象和统一

Maven中有3套相互独立的生命周期：

> clean：清理工作。
> 
> default：核心工作，如：编译、测试、打包、安装、部署等。
> 
> site：生成报告、发布站点等。

![7cef7d5e-a922-446c-8284-072e7bbafb83](file:///C:/Users/Jsy/Desktop/Pictures/Typedown/7cef7d5e-a922-446c-8284-072e7bbafb83.png)

## 五个阶段

> clean：移除上一次构建生成的文件
> 
> compile：编译项目源代码
> 
> test：使用合适的单元测试框架运行测试（junit）
> 
> package：将编译后的文件打包，如：jar、war等
> 
> install：安装项目到本地仓库
> 
> 注意：在 同一套 生命周期中，当运行后面的阶段时，前面的阶段都会运行







# 测试

> 测试：是一种用来促进鉴定软件的正确性、完整性、安全性和质量的过程。
> 
> 阶段划分：单元测试、集成测试、系统测试、验收测试。 
> 
> 测试方法：白盒测试、黑盒测试 及 灰盒测试。 

## 阶段划分

### 单元测试（白）

> 介绍：对软件的基本组成单位进行测试，最小测试单位。
> 
> 目的：检验软件基本组成单位的正确性。
> 
> 测试人员：开发人员

### 集成测试（灰）

> 介绍：将已分别通过测试的单元，按设计要求组合成系统或子系统，再进行的测试。
> 
> 目的：检查单元之间的协作是否正确。
> 
> 测试人员：开发人员

### 系统测试（黑）

> 介绍：对已经集成好的软件系统进行彻底的测试
> 
> 目的：验证软件系统的正确性、性能是否满足指定的要求。
> 
> 测试人员：测试人员

### 验收测试（黑）

> 介绍：交付测试，是针对用户需求、业务流程进行的正式的测试。
> 
> 目的：验证软件系统是否满足验收标准。
> 
> 测试人员：客户/需求方

## 测试方法

### 白盒测试

> 清楚软件内部结构、代码逻辑
> 
> 用于验证代码、逻辑正确性

### 黑盒测试

> 不清楚软件内部结构、代码逻辑
> 
> 用于验证软件的功能、兼容性等方面

### 灰盒测试

> 结合了白盒测试和黑盒测试的特带你，既关注软件的内部结构有考虑外部表现（功能）。





# 单元测试

> 针对最小的功能单元（方法），编写测试代码对其正确性进行测试。
> 
> JUnit：最流行的Java测试框架之一，提供了一些功能，方便程序进行单元测试（第三方公司提供）。

### main方法测试

> 测试代码与源代码为分开，难维护
> 
> 一个方法测试失败，影响后面方法
> 
> 无法自动化测试，得到测试报告        

## JUnit单元测试

> 测试代码与源代码分开，便于维护
> 
> 可根据需要进行自动化测试
> 
> 可自动分析测试结构，产出测试报告




























