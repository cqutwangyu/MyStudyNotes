# Java中8种基本数据类型

boolean -> byte,short,char-> int -> long -> float -> double

## 一、8种基本数据类型表格

| 序号 | 数据类型        | 字节 | 位数 | 默认值 | 取值范围       | 举例              |
| ---- | --------------- | ---- | ---- | ------ | -------------- | ----------------- |
| 1    | boolean(布尔值) | 1    | 8    | false  | true、false    | boolean b = true; |
| 2    | byte(字节)      | 1    | 8    | 0      | -2^7 - 2^7-1   | byte b = 10;      |
| 3    | short(短整数)   | 2    | 16   | 0      | -2^15 - 2^15-1 | short s = 10;     |
| 4    | char(字符)      | 2    | 16   | 空     | 0 - 2^16-1     | char c = 'c';     |
| 5    | int(整数)       | 4    | 32   | 0      | -2^31 - 2^31-1 | int i = 10;       |
| 6    | long(长整数)    | 4    | 64   | 0      | -2^63 - 2^63-1 | long l = 10l;     |
| 7    | float(单精度)   | 8    | 32   | 0.0    | -2^31 - 2^31-1 | float f = 10.0f;  |
| 8    | double(双精度)  | 8    | 64   | 0.0    | -2^63 - 2^63-1 | double d = 10.0d; |

## 二、byte（字节）

- `byte` 类型的数据是8位有符号整数
- `byte` 类型的取值范围**-128~127**
- 1 `byte`（字节）等于 8 `bits`（位）
- `Byte`是`byte`的封装类，继承于抽象类`Number`，实现`Comparable<Byte>`接口
- 在`socket`开发过程中，通常需要将各种类型的值转为 byte 类型
- 可与 `int` 数据做比较


```Java
		byte a=127；//a+1=-127
		byte b=-128；//b-1=126
```
## 三、short（短整型）

- `short` 数据类型是**16位有符号**的二进制数（0000 0000 0000 0000）
- `short` 类型的取值范围-**-32768~32767**
- 在C语言中 `unsigned short i；`　i可以表示无符号0~65535的整数
- `Short`是`short`的封装类，继承于抽象类`Number`，实现`Comparable<Short>`接口
```Java
        short s = 1;
        short c = 1;
        s += 1;//编译通过
        s = s+1;//编译不通过
		s = s+c;//编译不通过
```
**为什么编译通过？**

`s+=1`等价于`short s=(short)(s+1)`，复合赋值表达式会自动将计算结果转为存储值的变量类型。编译顺序：加法运算、强制类型转换、赋值运算，编译通过。

**为什么编译不通过？**

`s=s+1`，加法运算的优先级高于赋值运算，因此会先编译加法运算，`s`为`short`类型，常量`1`为`int`类型，这时会隐式转换`s`为`int`类型，在加法运算后，将`int`类型的结果赋值给 `short` 类型的 `s`， `short`类型的数据长度为16位，而`int`类型的数据长度为32位，在赋值过程中会发生数据丢失，因此编译不通过。

`s=s+c`同上，加法运算表达式会自动把数据长度小于`int`的数据值转换为`int`型，而`int`型的结果无法赋值给`short`，所以编译不通过。改为`s=(short)(s+c)`可编译通过。

注：加法运算表达式会自动把数据长度小于`int`的数据值转换为`int`型，不会把数据长度大于`int`的类型转为`int`，如`long a=1`，`a=a+a`编译通过。且`final`关键字声明的变量不会被转换类型。

## 四、int（整型）

- `int`类型的数据是**32位有符号**
- `Integer`是`int`的封装类，继承于抽象类`Number`，实现`Comparable<Integer>`接口

```Java
        int a = 1;
        Integer b = 1;
        Integer c = new Integer(1);
        System.out.println(a == b);//1、true
        System.out.println(a == c);//2、true
        System.out.println(b == c);//3、false
        System.out.println(b.equals(c));//4、true
        Integer a1 = 127;
        Integer b2 = 127;
        System.out.println(a1 == b2);//5、true
        Integer integer1 = 128;
        Integer integer2 = 128;
        System.out.println(integer1==integer2);//6、false
```

**分析**

1. `a==b`：当`Integer`与`int`比较时会自动将`Integer`拆装为`int`。
2. `a==c`：当`Integer`与`int`比较时会自动将`Integer`拆装为`int`，与`new Integer(1)`声明方式无关。
3. `b==c`：`b`为**缓存池**中的对象，而`c`是`new`的对象，是两个不同的对象，不会进行拆箱比较，对象是唯一的所以不等。
4. `b.equals(c)`，通过`equals`比较时，会判断是否为`Integer`类，如果是则取拆装之后比较值。
5. `a1==b2`：`Integer`作为常量时（非new对象），**-128~127**之间的数会存在于**缓存池**中，所以`a1`与`a2`都是使用的**缓存池**中的**同一个**值为**127**的`Integer`对象。
6. `integer1==integer2`：由于**128**不在**缓存池**中，会自动`new`一个对象，等同于两个**对象**做比较。

## 五、long（长整型）

- `long`类型的数据是64位有符号整数
- 当数值超出`int`数据长度即32位时可使用`long`
- 