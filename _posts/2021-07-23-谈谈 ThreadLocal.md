---
layout: mypost
title: 浅谈 ThreadLocal
categories: [Java]
---



### 浅谈 ThreadLocal

ThreadLocal 作用是提供线程内的局部变量，这种变量在线程的生命周期内起作用，减少一个线程内多个函数或者组件之间一些公共变量的传递的复杂性。ThreadLoacl 有一个静态内部类 ThreadLocalMap，其 Key 是 ThreadLocal 对象，值是 Entry 对象，ThreadLocalMap是每个线程私有的

+ set 给ThreadLocalMap设置值。 
+ get 获取ThreadLocalMap。
+ remove 删除ThreadLocalMap类型的对象

问题：

1. 对于线程池，由于线程池会重用 Thread 对象，因此与 Thread 绑定的 ThreadLocal 也会被重用， 造成一系列问题。所有在 finally 阶段一定要 remove 清除。
2. 内存泄漏。由于 ThreadLocal 是弱引用，但 Entry 的 value 是强引用，因此当 ThreadLocal 被垃圾回收后，value 依旧不会被释放，产生内存泄漏。

```java
// 典型使用
static ThreadLocal<User> threadLocalUser = new ThreadLocal<User>();
void processUser(User) {
    try {
        threadLocalUser.set(user);
        step1();
        step2();
    } finally {
        threadLocalUser.remove();
    }
}

// 使用 ThreadLocal 解决数据库连接、Session 管理等
// ThreadLocal 实例总是以静态字段初始化
private static final ThreadLocal threadSession = new ThreadLocal();
public static Session getSession() {
	Session s = (Session) threadSession.get();
    if (s == null) {
        s = getSessionFactory().openSession();
        threadSession.set(s);
    }
    return s;
}
```

