# 面向对象基础

Object-Oriented Programming，区别于面向过程，强调的是通过调用对象的行为来实现功能，而不是自己一步一步去操作实现。



## 特点

* 将复杂的事情简单化，将我们从操作者变成了指挥者。面向对象对象的语言中，包含了三大基本特征：封装、继承、多态。

### 封装

封装就是将一些细节信息隐藏起来，对于外界不可见。

1. 方法就是一种封装。
2. 关键字private也是一种封装。
   * [private keyword](./java-plugins/private-keyword.md)



## this关键字

* 当方法的局部变量和类的成员变量重名的时候，根据“就近原则”，优先使用局部变量。
* 如果需要访问本类中的成员变量，需要使用格式`this.成员变量名`



## 对象

通常情况下，一个类不能直接使用，需要根据类创建一个对象，才能使用。

### 类的定义

* 类（class）相当于蓝图，由`成员变量`和`成员方法`组成。

  * 成员变量是引用变量，与局部变量不同，它有默认值。

  ```java
  // 定义一个类，模拟一个“学生”事物
  class Student {
      
      // 成员变量（属性）
      // 注意：此时的变量不是局部变量，它直接写在类当中，在方法外，而不是方法中。
      String name; // 姓名
      int grade; // 年级
      
      // 成员方法（行为）
      // 注意：成员方法不要写static关键字。
      public void study(){
          System.out.println("学习");
      }
  
  }
  ```

  * [JavaBean](./java-plugins/JavaBean.md)
  
  

### 对象的创建及其使用

1. 导包

   * 也就是指出需要使用的类在什么位置
* 注意：对于和当前类属于同一个包的情况，可以省略不写
  
   ```java
   // 格式
   import 包名称.类名称；
   ```

2. 创建对象

   ```java
   // 格式
   类名称 对象名 = new 类名称();
   City bj = new City();
   ```

3. 使用

   1. 使用成员变量：

      ```java
      // 格式
      对象名.成员变量名
      ```

   2. 使用成员方法：

      ```java
      // 格式
      对象名.成员方法名()
      ```



## 方法

* 方法可以让外部代码安全地访问实例字段；
* 方法是一组执行语句，并且可以执行任意逻辑；
* 方法内部遇到return时返回，void表示不返回任何值（注意和返回null不同）；
* 外部代码通过public方法操作实例，内部代码可以调用private方法；
* 理解方法的参数绑定。

[定义方法的格式](./java-plugins/Method-format.md)




## 构造方法

* 构造方法是专门用来创建对象的方法，当我们用关键字new来创建对象时，其实就是在调用构造方法。

  ```java
  // 格式
  pubic 类名称 (参数类型 参数名称){
      方法体
  }
  // 注意：
  // 1.构造方法的名称必须和所在类名称完全一样；2.构造方法不要写返回值类型，连void都不写。
  ```

  * 实例在创建时通过`new`操作符会调用其对应的构造方法，构造方法用于初始化实例；

* 和普通方法相比，构造方法没有返回值（也没有`void`）;

* 没有定义构造方法时，编译器会自动创建一个默认的无参数构造方法；

* 可以定义多个构造方法，编译器根据参数自动判断；

* 可以在一个构造方法内部调用另一个构造方法，便于代码复用。



## 方法重载

* 方法重载(Overload)是指多个方法的方法名相同，但各自的参数不同；
  * 只需要记一个方法名，就可以实现类似的多个功能，调用更简单。
* 重载方法应该完成类似的功能，参考`String`的`indexOf()`；
* 重载方法返回值类型应该相同。



## 继承

* 继承是面向对象编程的一种强大的代码复用方式；
* Java只允许单继承，所有类最终的根类是`Object`；
* `protected`允许子类访问父类的字段和方法；
* 子类的构造方法可以通过`super()`调用父类的构造方法；
* 可以安全地向上转型为更抽象的类型；
  * 把一个子类类型安全地变为父类类型的赋值，被称为向上转型（upcasting）。
* 可以强制向下转型，最好借助`instanceof`判断；
* 子类和父类的关系是is，has关系不能用继承。



## 多态/final

* 子类可以覆写父类的方法（Override），覆写在子类中改变了父类方法的行为；
  * 在继承关系中，子类如果定义了一个与父类方法签名完全相同的方法，被称为覆写。
  * 加上`@Override`可以让编译器帮助检查是否进行了正确的覆写。
  
* Java的方法调用总是作用于运行期对象的实际类型，这种行为称为多态；
  
  * 多态具有一个非常强大的功能，就是允许添加更多类型的子类实现功能扩展，却不需要修改基于父类的代码。
  
* `final`修饰符有多种作用：

  - `final`修饰的方法可以阻止被覆写；

    ```java
    public class Hello {
        // 无法被覆写:
        protected final void hi() {
        }
    }
    ```

    

  - `final`修饰的class可以阻止被继承；

    ```java
    // 无法被继承:
    public final class Hello {
        private int n = 0;
        protected void hi(int t) {
            long i = t;
        }
    }
    ```

    

  - `final`修饰的`field`必须在创建对象时初始化，随后不可修改。

    - `final`修饰的`field`可以阻止被重新赋值；

      ```java
      public class Hello {
          private final int n = 0;
          protected void hi() {
              this.n = 1; // error!
          }
      }
      ```

      

    - `final`修饰的局部变量可以阻止被重新赋值。

      ```java
      public class Hello {
          protected void hi(final int t) {
              t = 1; // error!
          }
      }
      ```

      



## 抽象类

* 通过`abstract`定义的方法是抽象方法，它只有定义，没有实现。抽象方法定义了子类必须实现的接口规范；
  * [抽象方法的定义格式](./java-plugins/Method-format.md)
* 定义了抽象方法的class必须被定义为抽象类，从抽象类继承的子类必须实现（即覆写）抽象方法；
* 如果不实现抽象方法，则该子类仍是一个抽象类；
* 面向抽象编程使得调用者只关心抽象方法的定义，不关心子类的具体实现



## 接口

* Java的接口（interface）定义了纯抽象规范，一个类可以实现多个接口；
  * [接口的格式](./java-plugins/Interface-format.md)
* 接口也是数据类型，适用于向上转型和向下转型；
* 接口的所有方法都是抽象方法，接口不能定义实例字段；
* 接口可以定义`default`方法（JDK>=1.8）。



## static 关键字

* static 关键字可以用来修饰成员变量和成员方法，被修饰的成员是属于==类==的，而不是单单是属于某个对象的。
* 调用静态方法不需要实例，无法访问`this`，但可以访问静态字段和其他静态方法；
* 推荐用类名来访问静态字段。
* 静态方法常用于工具类和辅助方法。



## package

* Java内建的`package`机制是为了避免`class`命名冲突；
* JDK的核心类使用`java.lang`包，编译器会自动导入；
* JDK的其它常用类定义在`java.util.*`，`java.math.*`，`java.text.*`，……；
  * `import`的时候，使用`*`，表示把这个包下面的所有`class`都导入进来（但不包括子包的`class`）：
* 包名推荐使用倒置的域名，例如`org.apache`。



## 作用域

### public

* 定义为`public`的`class`、`interface`可以被其他任何类访问；
* 定义为`public`的`field`、`method`可以被其他类访问，前提是首先有访问`class`的权限。

### protected

* `protected`作用于继承关系。定义为`protected`的字段和方法可以被子类访问，以及子类的子类；

### private

* 定义为`private`的`field`、`method`无法被其他类访问；
* `private`访问权限被限定在`class`的内部，而且与方法声明顺序*无关*。
* 推荐把`private`方法放到后面，因为`public`方法定义了类对外提供的功能，阅读代码的时候，应该先关注`public`方法。
* 由于Java支持嵌套类，如果一个类内部还定义了嵌套类，那么，嵌套类拥有访问`private`的权限。

### package

* 包作用域是指一个类允许访问同一个`package`的没有`public`、`private`修饰的`class`，以及没有`public`、`protected`、`private`修饰的字段和方法。



## classpath/jar

* JVM通过环境变量`classpath`决定搜索`class`的路径和顺序；
  * `classpath`就是一组目录的集合，它设置的搜索路径与操作系统相关。
* 不推荐设置系统环境变量`classpath`，始终建议通过`-cp`命令传入；
  * 在系统环境变量中设置`classpath`环境变量，不推荐；
  * 在启动JVM时设置`classpath`变量，推荐。
* jar包相当于目录，可以包含很多`.class`文件，方便下载和使用；
  * 注意：打包时不要把bin也包进去了。
* `MANIFEST.MF`文件可以提供jar包的信息，如`Main-Class`，这样可以直接运行jar包。



## Module

* Java 9引入的模块目的是为了管理依赖；
* 使用模块可以按需打包JRE；
* 使用模块对类的访问权限有了进一步限制。



# Java核心类

## String

* Java字符串`String`是不可变对象；
* 字符串操作不改变原字符串内容，而是返回新字符串；
* 常用的字符串操作：提取子串、查找、替换、大小写转换等；
* Java使用Unicode编码表示`String`和`char`；
* 转换编码就是将`String`和`byte[]`转换，需要指定编码；
* 转换为`byte[]`时，始终优先考虑`UTF-8`编码。



## StringBuilder

* `StringBuilder`是可变对象，用来高效拼接字符串；
  * 是一个字符串的缓冲区，即它是一个容器，容器中可以装很多字符串。
  * `append`方法：添加任意类型数据的字符串形式，并返回当前对象自身。
  * `toString`方法：将当前StringBuilder对象转换为String对象。
* `StringBuilder`可以支持链式操作，实现链式操作的关键是返回实例本身；
* `StringBuffer`是`StringBuilder`的线程安全版本，现在很少使用。



## StringJoiner

* 用指定分隔符拼接字符串数组时，使用`StringJoiner`或者`String.join()`更方便；
* 用`StringJoiner`拼接字符串时，还可以额外附加一个“开头”和“结尾”。



## 包装类型

* Java核心库提供的包装类型可以把基本类型包装为`class`；

  * [装箱与拆箱](./java-plugins/BoxingAndUnboxing.md)

* 自动装箱和自动拆箱都是在编译期完成的（JDK>=1.5）；

* 装箱和拆箱会影响执行效率，且拆箱时可能发生`NullPointerException`；

* 包装类型的比较必须使用`equals()`；

* 整数和浮点数的包装类型都继承自`Number`；

* 包装类型提供了大量实用方法。

  * 以`Integer`类为例，最常用的静态方法`parseInt()`可以把字符串解析成一个整数，并进行进制转换

    ```java
    int x1 = Integer.parseInt("100"); // 100
    int x2 = Integer.parseInt("100", 16); // 256,因为按16进制解析
    ```

    

  * `Integer`还可以把整数格式化为指定进制的字符串

    ```java
    System.out.println(Integer.toString(100)); // "100",表示为10进制
    System.out.println(Integer.toString(100, 36)); // "2s",表示为36进制
    System.out.println(Integer.toHexString(100)); // "64",表示为16进制
    ```

    

  * 处理无符号整型

    * 在Java中，并没有无符号整型（Unsigned）的基本数据类型。`byte`、`short`、`int`和`long`都是带符号整型，最高位是符号位。
    * 无符号整型和有符号整型的转换在Java中就需要借助包装类型的静态方法完成。
    * 例如，byte是有符号整型，范围是`-128`~`+127`，但如果把`byte`看作无符号整型，它的范围就是`0`~`255`。我们把一个负的`byte`按无符号整型转换为`int`：

    ```java
    byte x = -1;
    byte y = 127;
    System.out.println(Byte.toUnsignedInt(x)); // 255
    System.out.println(Byte.toUnsignedInt(y)); // 127
    ```

    

## JavaBean

[JavaBean](./java-plugins/JavaBean.md)

* JavaBean是一种符合命名规范的`class`，它通过`getter`和`setter`来定义属性；
  * 例如，`name`属性：
    * 对应的读方法是`String getName()`--只读属性（read-only）
    * 对应的写方法是`setName(String)`--只写属性（write-only）
* 属性是一种通用的叫法，并非Java语法规定；
* 可以利用IDE快速生成`getter`和`setter`；
* 使用`Introspector.getBeanInfo()`可以获取属性列表。



## 枚举类

* Java使用`enum`定义枚举类型，它被编译器编译为`final class Xxx extends Enum { … }`

* 通过`name()`获取常量定义的字符串，注意不要使用`toString()`；

* 通过`ordinal()`返回常量定义的顺序（无实质意义）；

* 可以为`enum`编写构造方法、字段和方法

* `enum`的构造方法要声明为`private`，字段强烈建议声明为`final`；

  * ```java
    // 构造方法
    private Color() {}
    ```

  * ```java
    // 字段
    public final int dayValue;
    ```

    

* `enum`适合用在`switch`语句中

  * 因为枚举类天生具有类型信息和有限个枚举常量，所以比`int`、`String`类型更适合用在`switch`语句中。



## 记录类

* 从Java 14开始，提供新的`record`关键字，可以非常方便地定义Data Class：
  - 使用`record`定义的是不变类；
    - 不变类
      - 定义class时使用`final`，无法派生子类；
      - 每个字段使用`final`，保证创建实例后无法修改任何字段。
  - 可以编写Compact Constructor对参数进行检查验证；
  - 可以定义静态方法。



## BigInteger

在Java中，由CPU原生提供的整型最大范围是64位`long`型整数。使用`long`型整数可以直接通过CPU指令进行计算，速度非常快。但是如果我们使用的整数范围超过了`long`型，只能用软件来模拟一个大整数。

* `java.math.BigInteger`就是用来表示任意大小的整数；
  * 对`BigInteger`做运算的时候，只能使用实例方法。
* `BigInteger`是不变类，并且继承自`Number`；
* 将`BigInteger`转换成基本类型时可使用`longValueExact()`等方法保证结果准确。
  * 在转换时如果超出基本类型的范围，将直接抛出`ArithmeticException`异常。



## BigDecimal

* `BigDecimal`用于表示精确的小数，常用于财务计算；
* 比较`BigDecimal`的值是否相等，必须使用`compareTo()`而不能使用`equals()`。
  * 因为使用`equals()`方法不但要求两个`BigDecimal`的值相等，还要求它们的`scale()`相等
  * 使用`compareTo()`方法来比较，它根据两个值的大小分别返回负数、正数和`0`，分别表示小于、大于和等于。
* 如果查看`BigDecimal`的源码，可以发现，实际上一个`BigDecimal`是通过一个`BigInteger`和一个`scale`来表示的，即`BigInteger`表示一个完整的整数，而`scale`表示小数位数。
* `BigDecimal`也是从`Number`继承的，也是不可变对象。



## 常用工具类

Java提供的常用工具类有：

- Math：数学计算；
  - [Math类](./java-plugins/Class-Math.md)
- Random：生成伪随机数；
  - 所谓伪随机数，是指只要给定一个初始的种子，产生的随机数序列是完全一样的。
  - 使用的`Math.random()`实际上内部调用了`Random`类，所以它也是伪随机数，只是我们无法指定种子。
- SecureRandom：生成安全的随机数。