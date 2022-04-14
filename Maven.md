# Maven

## 是什么

Maven的本质是一个项目管理工具，将项目开发和管理过程抽象成一个项目对象模型（POM）

## 作用

1. 项目构建
2. 依赖管理
3. 统一开发结构

## 基本概念

### 仓库

用于存储资源，包含各种jar包

1. 远程仓库
   1. 中央仓库
   2. 私服
2. 本地仓库

### 坐标

|组成|说明|
|-|-|
|groupId|当前Maven项目隶属组织名称|
|artifactId|当前maven项目名称|
|version|当前项目版本号|
|packaging(*不属于坐标*)|打包方式|

mvn仓库 <https://mvnrepository.com/>

配置

## 构建

### 目录结构

### 命令

```mvn
mvn compile #编译
mvn clean #清理
mvn test #测试
mvn package #打包
mvn install #安装到本地仓库
```

项目模板  `mvn archetype:generate`

## 依赖管理

### 依赖有传递性

1. 直接依赖
2. 间接依赖

### 冲突问题

- 路径优先 层级浅优先
- 声明优先 配置顺序考前优先
- 特殊优先 同级后配置优先

### 可选依赖

隐藏当前依赖——不透明

```xml
<optional>true</optional>
```

### 排除依赖

主动断开依赖资源，被排除的资源无需指定版本——不需要

```xml
<exclusions>
    <exclusion>
        <groupId></groupId>
        <artifactId></artifactId>
    </exclusion>
</exclusions>
```

### 依赖范围

依赖的jar默认情况可以在任何地方使用，使用`<scope>`标签

#### 范围

|scope|mian|test|package|
|-|-|-|-|
|compile|Y|Y|Y|
|test||Y||
|provided|Y|Y||
|runtime|||Y|

依赖范围传递性

|间接依赖\直接依赖|compile|test|provided|runtime|
|-|-|-|-|-|
|compile|compile|test|provided|runtime|
|test|||||
|provided|||||
|runtime|runtime|test|provided|runtime|
