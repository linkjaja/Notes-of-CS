装箱与拆箱

## 概括

* Java提供了两个类型系统，基本类型与引用类型。

  * 基本类型效率高，但很多情况，会创建对象使用，因为对象有更多的功能

  * Java核心库为每种基本类型都提供了对应的包装类型：

    | 基本类型 | 对应的引用类型      |
    | :------- | ------------------- |
    | boolean  | java.lang.Boolean   |
    | byte     | java.lang.Byte      |
    | short    | java.lang.Short     |
    | int      | java.lang.Integer   |
    | long     | java.lang.Long      |
    | float    | java.lang.Float     |
    | double   | java.lang.Double    |
    | char     | java.lang.Character |

    

## 装箱

* 把基本类型转换为对应的引用类型

  * 因为Java核心库为每种基本类型都提供了对应的包装类型，所以可以直接调用，无需自己定义。

* 基本类型-->包装对象

  ```java
  int i = 100;
  // 调用构造方法，通过new操作符创造Integer实例(不推荐，会有编译警告)
  Integer n1 = new Integer(i);
  // 使用包装类中的静态方法valueOf(int)创建Integer实例
  Integer n2 = Integer.valueOf(i);
  // 通过静态方法valueOf(String)创建Integer实例
  Integer n3 = Integer.valueOf("100");
  System.out.println(n3.intValue()); // 100
  ```

  

## 拆箱

* 包装对象-->基本类型

  ```java
  int n3 = n2.intValue();
  ```

  

## Auto Boxing

* 从Java 5（JDK 1.5）开始，基本类型与包装类的装箱、拆箱动作可以自动完成。

  * 比如，Java编译器可以帮助我们自动在`int`和`Integer`之间转型：

    ```java
    Integer n = 100; // 编译器自动使用Integer.valueOf(int)
    int x = n; // 编译器自动使用Integer.intValue()
    ```

  

  * 这种直接把`int`变为`Integer`的赋值写法，称为自动装箱（Auto Boxing），反过来，把`Integer`变为`int`的赋值写法，称为自动拆箱（Auto Unboxing）。

    

    

