# SSM

## 1.spring

full-stack 代表各层都有解决方案

1. IoC (Inverse Of Control)反转控制
2. AOP (Aspect Oriented Programming)面向切面编程

![spring framework runtime](img/SSM/SpringFrameworkRuntime.png)

TODO  lombok var 

## 开发步骤

1. 导入坐标
2. 创建Bean
3. 创建applicationContext.xml
4. 配置配置文件
5. 船舰applicationContext对象getBean

## 2.spring配置文件

scope 指定对象范围

|取值范围|说明|创建时机|生命周期:对象创建-对象运行-对象销毁|
|-|-|-|-|
|singleton|默认、单例的|spring核心文件被加载时|对象创建：应用加载容器，创建容器时，对象就被创造了|
|prototype|多例的|调用getBean()实例化Bean||
|request|WEB项目中，spring创建一个Bean对象，将对象存入request域|||
|session|WEB项目中，spring创建一个Bean对象，将对象存入session域|||
|global session|WEB项目中，应用在Portlet环境，如果没有PortLet环境，globalSession相当于session|||

### 依赖注入

IOC解耦只是降低他们的依赖关系，但不会消除，依赖关系由spring维护

方式

1. 构造方法
2. set方法

注入的数据类型

1. 普通数据类型
2. 引用数据类型
3. 集合数据类型

#### set方法注入

```xml
<property name="userDao" ref="userDao"></property>
```

`name`标签是首字母小写的seter

引入p命名空间

```xml
xmlns:p="http://www.springframework.org/schema/p"

<bean id="userService" class="org.example.service.impl.UserServiceImpl" p:userDao-ref="userDao"/>
```

#### 构造方法

```xml
<bean>
<constructor-arg name="userDao1" ref="userDao"></constructor-arg>
</bean>
```

