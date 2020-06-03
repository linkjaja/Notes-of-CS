一个标准的类：通常要拥有下面四个组成部分

Java Bean

## 定义

1. 所有的成员变量都要使用private关键字修饰

2. 为每个成员变量写一对Getter/Setter方法

   ```java
   // 读方法:
   public Type getXyz()
   // 写方法:
   public void setXyz(Type value)
   ```

   * `boolean`字段比较特殊，它的读方法一般命名为`isXyz()`：

   ```java
   // 读方法:
   public boolean isChild()
   // 写方法:
   public void setChild(boolean value)
   ```

   

3. 编写一个无参数的构造方法

4. 编写一个全参数的构造方法

```java
// 定义一个标准的“学生”类
public class Student{
    private String name;
    private int age;
    
    // 无参数的构造方法
    public Student(){
        
    }
    // 全参数的构造方法
    public Student(String name, int age){
        this.name = name;
        this.age = age;
    }
    
    // Getter/Setter
    public String getName(){return name;} // 读方法
    public void setName(String name){this.name = name;} // 写方法
    // Getter/Setter
    public int getAge(){return age;}
    public void setAge(int age){this.age = age;}
}
```



## 调用

```java
// 调用该类
public class Demo01Student {
    public static void main(String[] args) {
        Student stu1 = new Student();
        stu1.setName("李华");
        stu1.setAge(20);
        System.out.println("姓名："+ stu1.getName()+"，年龄："+stu1.getAge());
        System.out.println("==========");

        // 调用全参构造方法
        Student stu2 = new Student("赵雷",20);
        System.out.println("姓名："+ stu2.getName()+"，年龄："+stu2.getAge());
    }
}
```

