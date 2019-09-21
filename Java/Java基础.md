Java基础笔记
====
运算符
----

运算符的两边都为整数，则为整数除法，否则表示浮点除法。

枚举类型
----
```Java
        enum Size={SMALL,MEDIUM,LARGE};
        Size s=Size.MEDIUM;
```
枚举类型的变量只能存储这个类型声明中给定的某个枚举值。

字符串
----
```Java
       "Hello".equalsIgnoreCase("hello");
```
结果为：<br>
`true`<br>
`equalsIgnoreCase`可以忽略大小写匹配字符串

```Java
        String str="";
        System.out.println(str==null);
        System.out.println(str.length());
```
结果为：<br>
`false`<br>
`0`<br>
`String`可以为空串，长度为`0`，但不为`null`

```
        String str=null;
        if(str!=null&&str.length()!=0)
```
当`String`为`null`时`str.length()`会报错，所以先判断是否为空，可以避免这个`BUG`

StringBuilder的作用
----------
有些时候，需要由较短的字符串构建字符串，例如，按键或来自文件中的单词。采用字符串连接的方式达到此目的效率比较低。每次连接字符串，都会构建一个新的`String`对象，既`耗时`，又`浪费空间`。使用`StringBuilder`类就可以`避免`这个问题的发生。如果需要用许多小段的字符串构建一个字符串，那么应该按照下列步骤进行。首先，构建一个空的字符串构建器：
```Java
        StringBuilder builder=new StringBuilderO；
        builder.append("hello");
        builder.append("world");
        System.out.println(builder.toString());
```
结果为：<br>
`helloworld`<br>

## StringBuffer的线程安全

在StringBuilder的基础上，对线程不安全的一些方法加上了synchronized关键字，确保StringBuffer在多线程中能够保证线程安全。

格式化输出
------
沿用了C语言库函数中的printf方法。例如:
```Java

        double x=10000.0/3.0;
        System.out.println(x);
        System.out.printf("%8.2f",x);
```
`3333.3333333333335`
` 3333.33`<br>
并且在`printf`中，可以使用多个参数，例如：
```Java
System.out.printf（"Hel1o，%s.Next year，you'11 be %d"，name，age）;
```
命令行参数`main`函数中`String[] args`参数的作用
-------
```Java
        public class Main {

            public static void main(String[] args)
            {
                for(String a:args){
                    System.out.println(a);
                }
            }
        }
        
        控制台中执行Main
        java Main a b c d
```
结果为：<br>
`a`<br>
`b`<br>
`c`<br>
`d`<br>

`String[] args`参数用于接收控制台传入的参数

不规则数组
--------
利用不规则数组轻而易举的用`*`号输出一个三角形
```Java
         public static void main(String[] args)
            {
                int NMAX=3;
                String[][] odds=new String[NMAX+1][];
                for (int n=0;n<=NMAX;n++)
                {
                    odds[n]=new String[n+1];
                    for (int i = 0; i <n+1 ; i++) {
                        odds[n][i]="*";
                    }
                }
                for (String[] odd:odds)
                {
                    for (String od:odd)
                    {
                        System.out.printf(String.valueOf(od));
                    }
                    System.out.println();
                }
            }
```
结果为：<br>
```Java
*
**
***
****
```
## 封装

封装是把数据和操作数据的方法绑定起来，对数据的访问只能通过已定义的接口。面向对象的本质就是将现实世界描绘成一系列完全自治、封闭的对象。例如一个人的姓名和年龄不会写在脸上，你想知道就需要询问（调用相应的接口）。

继承
----

Boss包含Manager和Employee的属性和方法，Manager包含Employee的属性和方法，Boss和Manager和Employee都属于公司的一员（这里假设都属于员工），    Employee=>Manager=>Boss从左到右看，是一种包含的关系Employee的数组可以存放Manager和Boss，而反过来则不行，Boss的数组不能存放Manager或Employee。
```Java
         public class Employee{
                public void name(){}
         }
         public class Manager extends Employee{
                public void bonus(){}
         }
         public class Boss extends Manager{
                public void PromoteEmployees()
         }

         Employee e=new Employee();
         e.name()✔

         Manager m=new Manager();
         m.name();✔
         m.bonus();✔

         Boss b=new Boss();
         b.name();✔
         b.bonus();✔
         b.PromoteEmployees()✔
```
 多态
------

多态性是指允许不同子类型的对象对同一消息作出不同的响应。通过声明基类可以实例化一个派生类，而派生类可也重写父类的方法，也就是说一个类或接口可以有不同的实例化，而每一个实例又可以对相同方法的调用做出不同的响应。

  ```Java
         //基类包含所有派生类
         Employee e=new Manager();✔
         Employee e=new Boss();✔
         //派生类不包含超类（Employee）
         Manager m=new Employee();✖
         Manager m=new Boss();✔

         Boss b=new Employee();✖
         Boss b=newManager();✖
  ```
## 重写与重载

**重写**：在父类与子类之间，方法名、方法参数、返回值全部相同。

重写指一个方法的方法体被重新定义，旧的方法体会被新的方法体覆盖。

一般用于子类对父类方法的重写，重写时需与父类方法同名、同参、返回类型相同，且不能重写父类的私有(private)方法。

**重载**：在一个类中，方法名相同，方法参数的类型或个数或顺序不同。

重载指一个类中有多个同名方法，且每个方法拥有不同的方法体，同名方法之间需参数类型或个数或顺序不同。

## 构造方法

**概述**：构造方法存在于类中，用于类被实例化时给对象属性初始化；
**特点**：构造方法名与类名必须一样，且没有返回值，也不能以void为返回值;
**默认构造方法**：当没有构造方法时，默认提供一个无参构造方法；当存在一个构造方法时，不再提供默认的无参构造方法。

**构造方法可以重载**：在一个类中，可以有多个构造方法（方法参数不同） ，来实现对象属性不同的初始化；

**构造方法不能重写**：重写需要方法名、方法参数、返回值全部相同。而构造方法没有返回值，所以不能重写。

**子类无法继承构造方法**：子类无法继承构造方法，但子类的构造方法中可以调用父类的构造方法。

动态绑定
-----

同一个方法名，根据传入的参数类型不同，绑定不同的方法体，达到不一样的效果。
```Java
        String.valueOf(1);✔
        String.valueOf(1.5);✔
        String.valueOf(true);✔
        String.valueOf(new Object());✔
```
抽象类
----
```Java
        public abstract class Person {
            public abstract String getDescription();
        }
        public class Student extends Person{
            public String getDescription() {
                return "学习使我快乐！";
            }
        }
        public class Employee extends Person {
            public String getDescription() {
                return "劳动最光荣！";
            }
        }

            public static void main(String[] args) {
                Person[] people=new Person[2];
                people[0]=new Student();
                people[1]=new Employee();
                for (Person p : people) {
                    System.out.println(p.getDescription());
                }
            } 
```
输出结果：
```
    学习使我快乐！
    劳动最光荣！
```
protected受保护的
----
`protected`修饰的类、对象、方法、变量，仅允许在同一个`package`目录下访问，如果在上一级或者下一集`package`中都会显示`编译错误`。

接口与抽象类
-----
接口与抽象类的功能类似，为什么要引入接口呢？使用抽象类表示通用属性存在问题：因为类只能继承于一个类，不能继承多个类。而接口则不同，每个类可以实现多个接口。<br>
### 如何选择接口和抽象类呢？<br>
#### 使用接口：
* 需要让不相关的类都实现一个方法，例如不相关的类都可以实现 Compareable 接口中的 compareTo() 方法；<br>
* 需要使用多重继承。<br>
#### 使用抽象类：
* 需要在几个相关的类中共享代码。<br>
* 需要能控制继承来的成员的访问权限，而不是都为 public。<br>
* 需要继承非静态和非常量字段。<br>
```Java
        class Employee extends Person,Comparable{}✖
        class Employee extends Person implements Comparable{}✔
```
对象克隆
-----
```Java
        Employee original=new Enployee("John Public"，50000);
        Employee copy =original;//copy和original引用同一个对象（copy和original所指向的地址空间相同）
        copy.raiseSalary(10);//copy和original的值同时被改变了
```
如果创建一个对象的新的copy，它的最初状态与original一样，但以后将可以各自改变各自的状态，那就需要使用clone方法。
```Java
        Eaployee copy =original.clone();//得到一个初始值和original相同，但地址空间不同的新对象
        copy.raiseSalary(10);//original没有改变，而copy改变
```
参数传递
----
将`e`对象传入方法，方法体中`e=new Employee(...)`，`new`的新对象仅在方法体内有效，方法体外，原对象不变。
```Java
        Employee e=new Employee("张三",2000);
        System.out.println(e.toString()+e.getName()+e.getSalary());//polymorphic.Employee@1b6d3586张三2000.0
        changeSalary(e);
        System.out.println(e.toString()+e.getName()+e.getSalary());//polymorphic.Employee@1b6d3586张三2000.0

    private static void changeSalary(Employee e){
        e=new Employee("李四",1500);
        System.out.println(e.toString()+e.getName()+e.getSalary());//polymorphic.Employee@4554617c李四1500.0
    }
```
在方法体中`e=new Employee(...)`并`return e`，并在调用方法时`e=changeSalary(e)`将返回值赋给e，可使原对象被改变，若在方法体外不将返回值赋给e，原对象依旧不变。
```Java
        Employee e=new Employee("张三",2000);
        System.out.println(e.toString()+e.getName()+e.getSalary());//polymorphic.Employee@1b6d3586张三2000.0
        e=changeSalary(e);
        System.out.println(e.toString()+e.getName()+e.getSalary());//polymorphic.Employee@4554617c李四1500.0

    private static Employee changeSalary(Employee e){
        e=new Employee("李四",1500);
        System.out.println(e.toString()+e.getName()+e.getSalary());//polymorphic.Employee@4554617c李四1500.0
        return e;
    }
```
等价与相等
----
* 对于基本类型，== 判断两个值是否相等，基本类型没有 equals() 方法。
* 对于引用类型，== 判断两个变量是否引用同一个对象，而 equals() 判断引用的对象是否等价。
```Java
        Integer x = new Integer(1);
        Integer y = new Integer(1);
        System.out.println(x.equals(y)); // true
        System.out.println(x == y);      // false
```
方法
----
* 声明方法不能被子类重写。
private 方法隐式地被指定为 final，如果在子类中定义的方法和基类中的一个 private 方法签名相同，此时子类的方法不是重写基类方法，而是在子类中定义了一个新的方法。

## **访问修饰符**

- 类的成员不写访问修饰时默认为default。
- 默认(default)对于同一个包中的其他类相当于公开（public），对于不是同一个包中的其他类相当于私有（private）。
- 受保护（protected）对子类相当于公开，对不是同一包中的没有父子关系的类相当于私有。
- Java中，外部类的修饰符只能是public或默认，类的成员（包括内部类）的修饰符可以是以上四种。

|  修饰符   | 当前类 | 同 包 | 子 类 | 其他包 |
| :-------: | :----: | :---: | :---: | :----: |
|  public   |   √    |   √   |   √   |   √    |
| protected |   √    |   √   |   √   |   ×    |
|  default  |   √    |   √   |   ×   |   ×    |
|  private  |   √    |   ×   |   ×   |   ×    |

