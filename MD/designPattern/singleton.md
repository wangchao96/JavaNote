# Singleton 单例设计模式
## 什么是单例模式？
### 概念
> 单例模式是一种常见的设计模式，可以使得某个类只有一个实例，自己创建该类实例并向外界提供该实例。
### 单例的三要素：
- 私有构造器（防止客户端实例化）
- 静态属性
- 静态方法（同于获取单例实例）
### 单例模式优缺点
####	优点
- 数据共享
- 项目安全（配合同步实现）
#### 缺点
- 并发性降低
- 增加耦合
## 为什么使用单例模式？
在某些条件下，使用单例模式可以控制类实例的数量，达到节约资源的目的，同时由于只有一个实例，可以实现通信的功能以及资源共享，不仅如此，单例模式配合线程的同步可解决并发访问中的安全问题。

在一些优先考虑安全性的程序中可以尝试使用单例。

>单例模式的缺点是非常明显的，降低程序的并发性，增加模块之间的耦合，所以单例的使用需要谨慎。

## 几种实现方式
>根据实例创建的时机可以分为两类：lazy-load、非lazy-load。
### 非lazy-load

```java
/**
 * 单例模式
 * 当类加载时创建单例实例
 *
 * 优点：不需要考虑并发
 * 缺点：类加载后不获取单例对象会造成内存浪费
 */
public final class IvoryTower {

  /**
   * 私有构造器
   */
  private IvoryTower() {}

  /**
   * 静态属性
   */
  private static final IvoryTower INSTANCE = new IvoryTower();

  /**
   * 静态方法
   *
   * @return 单例实例
   */
  public static IvoryTower getInstance() {
    return INSTANCE;
  }
}
```
### 非lazy-load

#### 线程安全的单例类

```java
/**
 * 线程安全的单例类
 * 实例是惰性初始化的，因此需要同步
 *
 * 注意：如果通过反射创建，那么在同一个类加载器中不会创建单例对象，而是多个实例
 */
public final class ThreadSafeLazyLoadedIvoryTower {

  private static ThreadSafeLazyLoadedIvoryTower instance;

  private ThreadSafeLazyLoadedIvoryTower() {
    // 防止通过反射实例化
    if (instance == null) {
      instance = this;
    } else {
      throw new IllegalStateException("Already initialized.");
    }
  }

  /**
   * 只有在第一次调用实例时才会创建实例。延迟加载
   */
  public static synchronized ThreadSafeLazyLoadedIvoryTower getInstance() {
    if (instance == null) {
      instance = new ThreadSafeLazyLoadedIvoryTower();
    }

    return instance;
  }
}
```

#### 静态内部类

```java
/**
 * 利用静态内部类实现lazy-load的单例模式
 */
public final class InitializingOnDemandHolderIdiom {

  /**
   * 私有构造器
   */
  private InitializingOnDemandHolderIdiom() {}

  /**
   * 静态方法
   *
   * @return 单例实例
   */
  public static InitializingOnDemandHolderIdiom getInstance() {
    return HelperHolder.INSTANCE;
  }

  /**
   * 静态内部类
   */
  private static class HelperHolder {
    private static final InitializingOnDemandHolderIdiom INSTANCE =
        new InitializingOnDemandHolderIdiom();
  }
}
```

#### Double check locking

```java
/**
 * Double check locking
 */
public final class ThreadSafeDoubleCheckLocking {

  private static volatile ThreadSafeDoubleCheckLocking instance;

  /**
   * 私有构造器
   */
  private ThreadSafeDoubleCheckLocking() {
    // 防止通过反射实例化
    if (instance != null) {
      throw new IllegalStateException("Already initialized.");
    }
  }

  /**
   * 静态方法
   *
   * @return 单例实例
   */
  public static ThreadSafeDoubleCheckLocking getInstance() {
    // 局部变量可以提高25%的性能
    // Joshua Bloch，《Effective Java，第二版》，第283-284页
    ThreadSafeDoubleCheckLocking result = instance;
    if (result == null) {
      synchronized (ThreadSafeDoubleCheckLocking.class) {
        result = instance;
        if (result == null) {
          instance = result = new ThreadSafeDoubleCheckLocking();
        }
      }
    }
    return result;
  }
}
```

