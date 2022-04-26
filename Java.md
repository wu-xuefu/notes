# Java核心技术卷

## 泛型数组列表

ArrayList类

## 异常

### 异常层次结构

![java异常](/img/Java/Java%E5%BC%82%E5%B8%B8%E7%BB%A7%E6%89%BF.png)

### Throwable

- Throwable()
- Throwable(String message)
- Throwable(Throwable cause)
- Throwable(String message, Throwable cause)
- Throwable initCause(Throwable cause)
- Throwable getCause()
- String getMessage()

try/catch/finally

### 捕获多个异常

可以合并catch语句

捕获多个异常不仅会让你的代码看起来更简单，还会更高效。生成的字节码只包一个对应公共catch子句的代码块。

```java
catch (FileNotFoundException | UnknownHostException e) { . . . }
```

### 再次抛出异常与异常链

1. 在 catch 子句中可以抛出一个异常，这样做的目的是改变异常的类型，

```java
try{...}
catch(SQLException e)
{
    Throwable se = new ServletException("database error");
    se.initCause(e);
    throw se;
}


Throwable e = se.getCause();
```

使用包装技术。这样可以让用户抛出子系统中的高级异常，而不会丢失原始异常的细节。

2. 有时你可能只想记录一个异常， 再将它重新抛出， 而不做任何改变：

```java
try
{
    access the database
}
catch (Exception e)
{
    logger.logOevel, message, e);
    throw e;
}
```

### 带资源的 try 语句

```java
try (Scanner in = new Scanne「(new FileInputStream('7usr/share/dict/words"). "UTF-8"):
    PrintWriter out = new Pri ntWriter("out.txt"))
{
    while (in.hasNextO)
    out.pri ntl n(i n.next().toUpperCaseO);
}
```

不论这个块如何退出， in 和 out 都会关闭。如果你用常规方式手动编程，就需要两个嵌
套的 try/finally语句。

### 分析堆栈轨迹元素

堆栈轨迹（ stack trace ) 是一个方法调用过程的列表， 它包含了程序执行过程中方法调用的特定位置

```java
Throwable t = new ThrowableO ;
StackTraceElement[] frames = t.getStackTrace();
for (StackTraceElement frame : frames)
    analyze frame

```
TODO 线程 静态的 Thread.getAllStackTrace 方法， 它可以产生所有线程的堆栈轨迹
