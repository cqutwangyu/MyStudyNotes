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
`true`<br>
`equalsIgnoreCase`可以无视大小写匹配字符串

```Java
        String str="";
        System.out.println(str==null);
        System.out.println(str.length());
```
`false`
`0`<br>
`String`可以为空串，长度为`0`，但不为`null`
```
        String str=null;
        if(str!=null&&str.length()!=0)
```
当`String`为`null`时`str.length()`会报错，所以先判断是否为空，可以避免这个`BUG`
