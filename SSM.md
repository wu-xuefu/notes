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

### scope 指定对象范围

|取值范围|说明|创建时机|生命周期:对象创建-对象运行-对象销毁|
|-|-|-|-|
|singleton|默认、单例的|spring核心文件被加载时|对象创建：应用加载容器，创建容器时，对象就被创造了<br>对象运行：只要容器存在就一直存在 <br> 对象销毁：应用卸载，销毁容器时，对象就被销毁了|
|prototype|多例的|调用getBean()实例化Bean|对象创建：当使用对象时，创造新的实例<br>对象运行：只要只要使用就一直存在<br>对象销毁：长时间不用，被java的垃圾回收|
|request|WEB项目中，spring创建一个Bean对象，将对象存入request域|||
|session|WEB项目中，spring创建一个Bean对象，将对象存入session域|||
|global session|WEB项目中，应用在Portlet环境，如果没有PortLet环境，globalSession相当于session|||

### 生命周期配置

`init-method` 指定初始化方法
`destyroy-method` 指定销毁方法

### Bean实例化三种方式

1. 无参构造方法实例化
2. 工厂静态方法实例化

```xml
<bean id="" class=""  factory-method=""></bean>
```

3. 工厂实例方法实例化

```xml
<bean id="" factory-bean=""  factory-method=""></bean>
```

### 依赖注入

IOC解耦只是降低他们的依赖关系，但不会消除，依赖关系由spring维护

方式

1. 构造方法
2. set方法

注入的数据类型

1. 普通数据类型 `value=`
2. 引用数据类型
3. 集合数据类型

```xml
 <property name="strList" >
            <list>
                <value>aa</value>
            </list>
        </property>
        <property name="userMap">
            <map>
                <entry key="user1" value-ref="user"></entry>
            </map>
        </property>
            <property name="properties">
                <props>
                    <prop key="p1">pppp1</prop>
                    <prop key="p2">2</prop>
                </props>
            </property>
    </bean>
```

TODO property

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

### 引入其他配置文件

```xml
<import resource=""/>
```

## 3.spring相关api

1. ClassPathXmlApplicationContext
2. FileSystemXmlApplicationContext
3. AnnotationConfigApplicationContext

getBean()

1. id 
2. Class<T> 

## 4.spring配置数据源

