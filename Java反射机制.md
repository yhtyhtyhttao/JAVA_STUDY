# Java 反射机制 #

 一.反射的概念：

* 主要是指程序可以访问，检测和修改它本身状态或行为的一种能力，并能根据自身行为的状态和结果，调整或修改应用所描述行为的状态和相关的语义。

* 反射是Java中一种强大的工具，能够使我们很方便的创建灵活的代码，这些代码可以再运行时装配，无需在组件之间进行源代码链接。但是反射使用不当会成本很高！
看概念很晕的，继续往下看。

二，反射机制的作用：

* 反编译：.class-->.java

* 通过反射机制访问java对象的属性，方法，构造方法等；

三.反射机制中的类：

* ava.lang.Class;

* java.lang.reflect.Constructor;

* java.lang.reflect.Field;

* java.lang.reflect.Method;

* java.lang.reflect.Modifier;

四.具体功能实现：

1.反射机制获取类有三种方法，我们来获取Employee类型
```java
//第一种方式：
Classc1 = Class.forName("Employee");
//第二种方式：
//java中每个类型都有class 属性.
Classc2 = Employee.class;

//第三种方式：
//java语言中任何一个java对象都有getClass 方法
Employeee = new Employee();
Classc3 = e.getClass(); //c3是运行时类 (e的运行时类是Employee)
```
2.创建对象：获取类以后我们来创建它的对象，利用newInstance：
```java
Class c =Class.forName("Employee");

//创建此Class 对象所表示的类的一个新实例
Objecto = c.newInstance(); //调用了Employee的无参数构造方法.

```
3.获取属性：分为所有的属性和指定的属性：

(1)获取所有的属性的写法：
```java
//获取整个类
            Class c = Class.forName("java.lang.Integer");
              //获取所有的属性?
            Field[] fs = c.getDeclaredFields();

                   //定义可变长的字符串，用来存储属性
            StringBuffer sb = new StringBuffer();
            //通过追加的方法，将每个属性拼接到此字符串中
            //最外边的public定义
            sb.append(Modifier.toString(c.getModifiers()) + " class " + c.getSimpleName() +"{\n");
            //里边的每一个属性
            for(Field field:fs){
                sb.append("\t");//空格
                sb.append(Modifier.toString(field.getModifiers())+" ");//获得属性的修饰符，例如public，static等等
                sb.append(field.getType().getSimpleName() + " ");//属性的类型的名字
                sb.append(field.getName()+";\n");//属性的名字+回车
            }

            sb.append("}");

            System.out.println(sb);

```
 (2)获取特定的属性：
 ````java
 public static void main(String[] args) throws Exception{

 <span style="white-space:pre">  </span>//以前的方式：
     /*
     User u = new User();
     u.age = 12; //set
     System.out.println(u.age); //get
     */

     //获取类
     Class c = Class.forName("User");
     //获取id属性
     Field idF = c.getDeclaredField("id");
     //实例化这个类赋给o
     Object o = c.newInstance();
     //打破封装
     idF.setAccessible(true); //使用反射机制可以打破封装性，导致了java对象的属性不安全。
     //给o对象的id属性赋值"110"
     idF.set(o, "110"); //set
     //get
     System.out.println(idF.get(o));
 }
 ````
