# Java 中创建子类对象会创建父类对象么？
## 0.写在前面
- 创建对象指的是在堆区开辟空间
- 编译器在运行子类构造器之前，必须先执行父类构造器；且调用父类构造器的语句必须在子类构造器的第一行。
- 构造方法的作用是为堆区中的对象的属性初始化，不是创建对象。

## 1.开门见山
 `Java` 中创建子类对象`不会`创建父类对象！

## 2.show me the code!

### 示例代码
```java
/**
 * 示例测试类
 *
 * @author chao.wang
 * @date 2018.08.31
 */
public class Test {
    public static void main(String[] args) {
        // 创建子类对象
        Sub sub = new Sub();
        // 通过setter设置父类的私有成员变量str
        sub.setStr("SubString");
        System.out.println(sub.getStr());
    }
}

/**
 * 示例父类
 *
 * @author chao.wang
 * @date 2018.08.31
 */
class Base {
  private String str;

  /**
   * 父类构造器
   */
  public Base() {
    System.out.println("Base():" + this);
  }

  public void setStr(String str) {
    this.str = str;
  }

  public String getStr() {
    return this.str;
  }
}

/**
 * 示例子类
 *
 * @author chao.wang
 * @date 2018.08.31
 */
class Sub extends Base {
  /**
   * 子类构造器
   */
  public Sub() {
    System.out.println("Sub():" + this);
  }

}

```
### 测试结果

```
Base():Sub@2f2c9b19
Sub():Sub@2f2c9b19
SubString
```

## 3.几点疑问
- 是谁在完成创建对象的工作？
 
    `new` 关键字

- 既然没有父类对象，那么父类的私有成员变量 `str` 从何而来？

    虚拟机会在堆区中开辟一块空间来保存这个私有属性（该空间不属于子类对象），并且在运行时该属性的空间会与方法区中 `Base.class` 动态绑定。
    
    子类对象 `sub` 调用继承父类的方法 `setStr()` 时，系统会找到与 `setStr()` 方法 `静态绑定` 的类 `Base`，再找到与 `Base` 类 `动态绑定` 的属性空间 `str`,便可对该属性进行相关操作。
    
    - `静态绑定`：（`final`、`static`、`private`）在程序执行前已经被绑定，也就是说在编译过程中就已经知道这个熟悉或方法是哪个类的方法，此时由编译器获取其他连接程序实现。
    
    - `动态绑定`：在运行根据具体对象的类型进行绑定。
    
    > 类的方法可以被继承，但是类的构造器和 `private` 修饰的属性及方法不能被继承。
    
![内存图](https://user-gold-cdn.xitu.io/2018/8/31/1658f1680df88ba6?w=1340&h=630&f=png&s=301145)

