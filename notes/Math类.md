# Math

顾名思义，`Math`类就是用来进行数学计算的，它提供了大量的静态方法来便于我们实现数学计算。



## 求绝对值

```java
Math.abs(-100); // 100
Math.abs(-7.8); // 7.8
```



## 取最大值或最小值

```java
Math.max(100, 99); // 100
Math.min(1.2, 2.3); // 1.2
```



## 计算 x<sup>y</sup> 次方

```java
Math.pow(2, 10); // 2的10次方=1024
```



## 计算√x

```java
Math.sqrt(2); // 1.414...
```



## 计算e<sup>x</sup>次方

```java
Math.exp(2); // 7.389...
```



## 计算以e为底数的对数

```java
Math.log(4); // 1.386...
```



## 计算以10为底数的对数

```java
Math.log10(100); // 2
```



## 三角函数

```java
Math.sin(3.14); // 0.00159...
Math.cos(3.14); // -0.9999...
Math.tan(3.14); // -0.0015...
Math.asin(1.0); // 1.57079...
Math.acos(1.0); // 0.0
```



## 数学常量

```java
double pi = Math.PI; // 3.14159...
double e = Math.E; // 2.7182818...
Math.sin(Math.PI / 6); // sin(π/6) = 0.5
```



## 随机数

生成一个随机数x，x的范围是`0 <= x < 1`：

```java
Math.random(); // 0.53907... 每次都不一样
```

* 如果我们要生成一个区间在`[MIN, MAX)`的随机数，可以借助`Math.random()`实现

  ```java
  // 区间在[MIN, MAX)的随机数
  public class Main {
      public static void main(String[] args) {
          double x = Math.random(); // x的范围是[0,1)
          double min = 10;
          double max = 50;
          double y = x * (max - min) + min; // y的范围是[10,50)
          long n = (long) y; // n的范围是[10,50)的整数
          System.out.println(y); // 浮点数
          System.out.println(n); // 长整型
      }
  }
  ```

  