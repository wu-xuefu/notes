#

## HikariCP

### 为什么快

1. 字节码级别优化（JavaAssist生成）
2. 大量小改动
   1. fastStatemenList替代 ArrayList
   2. 无锁集合ConcurrentBag
   3. 代理类的优化