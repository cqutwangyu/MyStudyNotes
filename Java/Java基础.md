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

#StringBuilder的作用
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

