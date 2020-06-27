# 反射

## class类

* JVM为每个加载的`class`及`interface`创建了对应的`Class`实例来保存`class`及`interface`的所有信息；
* 获取一个`class`对应的`Class`实例后，就可以获取该`class`的所有信息；
* 通过Class实例获取`class`信息的方法称为反射（Reflection）；
* JVM总是动态加载`class`，可以在运行期根据条件来控制加载class。