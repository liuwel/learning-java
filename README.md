#Learning Java
------

##基础语法
###关键字
java中所有关键字都是小写的 注意 main不是关键字
> abstract    assert  boolean break   byte    case
catch   char    class   const   continue    default
do  double	else    enum	extends final	finally	float
for	goto	if	implements	import
instanceof	int	interface	long	native
new	package	private	protected	public
return	strictfp	short	static	super
switch	synchronized	this	throw	throws
transient	try	void	volatile	while

###命名规则
* 由英文字母数字下划线 $符号组成
* 不能以数字开头，也不能是关键字

###命名规范
* 包 全小写 . 分割
* 类和接口 大驼峰
* 成员方法成员变量 小驼峰
* 常量 全大写 单词之间 _ 分割如 MAX_LENGTH

###数据进制的标识方式
* 2进制 0b开头
* 8进制 0开头
* 10进制 0-9 默认
* 16进制 0x开头 0-9 a-f 组成

###进制转换
*  n进制转10进制：n进制从左到右的每一位数分别乘以n的0次，1次，2次~n次方。如：2进制1001 – 10进制的1+0+0+8 = 9
*  10进制转换n进制：10进制数除以n进制的n，一直到商0，然后把余数倒过来。

##java数据类型
###基础数据类型
|   类型    |   长度(字节)    |   默认值  |   默认封箱类  |
| :--------:|:---------:|:---------:|:---------:|:---------:| 
|   byte    |   1   |   0   |java.lang.Byte|
|   short   |   2   |   0   |java.lang.Short|
|   int     |   4   |   0   |java.lang.Integer|
|   long    |   8   |   0   |java.lang.Long|
|   float   |   4   |   0.0   |java.lang.Float|
|   double   |   8   |   0.0   |java.lang.Double|
|   char   |   2   |   \u0000   |java.lang.Character|
|   boolean   |   1/8   |   false   |java.lang.Boolean|
###引用数据类型
* 类 使用class 定义的类实例化对象 
```java
ClassName xxx = new ClassName();
```
* 接口 实现了interface定义的接口子类实例化对象
```java
InterfaceName inter = new ClassImpl();
```
* 数组 
```java
int[] i = new int[]{1,2,3};
```
###类型转换
* 默认转换(数据从小到大做类型转换)
    1. byte,short,char -> int -> long -> float -> double 
    2. 如果参与运算的有大的数据类型，结果必定是大的数据类型 如：int和double 进行运算 结果一定是double类型
    3. byte, short,char相互之间不转换。它们参与运算首先转换为int类型。char类型会根据asc码表来转换成int值。
    > 案例分析 byte a = 3; byte b = 5; byte c; c = a + b; 错误，因为byte类型做运算时，会转换成int类型（类型提升），用byte类型去保存int类型，所以会报错。丢失精度
    > byte c = 3 + 5; 正确。因为3个5是常量值。常量运算时首先看结果是否在数据类型的范围内，如果在则不报错。3 + 5的结果在byte范围内，所以不报错。

    4.  强制类型转换（从大的数据类型到小的数据类型的转换）：
    格式：目标数据类型 变量名 = (目标数据类型) (被转换的数据类型); 
    >  如：int a = 10; byte b = 3; byte c = (byte) (a + b);
    (不要随意的使用强制类型转换，会导致精度丢失。)

整型默认类型是int 浮点默认类型是 double
```java
// 给long类型数据赋值格式 
long l = 33342L;

// 给float类型赋值格式
float f = 2.3F;
```
> int类型自动装箱 byte值范围之内的对象 是被jvm缓存起来的 所以 byte范围内打封装对象是同一个

###数组
> 数组是引用类型的，当参数传递时，传入方法的是地址。
数组可以存储任何类型的数据，包括对象类型，基础类型和引用类型都可以通过数组存储，但是数组内存储的元素类型必须一致。
数组的最大的缺点是，一旦定义，元素固定。

定义和初始化
```java
// 动态初始化 
int[] a = new int[4]; // 定义一个长度是4 类型是int的数组(推荐使用的写法)
int b[] = new int[3]; // 定义一个长度是3 类型是int的数组
// 静态初始化
int[] c = new int[]{1, 2, 3, 4, 5};
int[] d = {1, 2, 3}; //(推荐使用的写法)
```
访问
数组是通过索引访问的 (索引只可以是整型)
通过length属性可以获取到数组的长度
```java
int[] arr = {4,5,6};
System.out.println(arr[0]);
// 输出 4

// 循环数组
for(int i=0;i<arr.length;i++){
	System.out.println(arr[i]);
}
// 4
// 5
// 6
```

####二维数组和多维数组
* 二维数组的每个元素都是一个一维数组。
	1. 如：int[][] arr = new int[3][2];  表示这个二维数组有3个一维数组组成，每个一维数组都有2个元素。
	2. 上例中，打印arr，arr[0] ~ arr[2]的值，都是地址值。只有arr[0][0] ~ arr[2][1] 才是真正的值。
* 二维数组的动态初始化：
	1. int[][] arr = new int[2][3];  初始化时确定了元素的个数。这是一个由2个一维数组组成的二维数组，每个一维数组都有固定的3个元素。
	2. int[][] arr = new int[2][];  arr[0] = new int[3]; arr[1] = new int[8]; 初始化时不确定一维数组的元素个数，然后动态给定长度，每个一维数组的元素个数可以不一样。
		> 注： arr[0] = {1,2,3,4,5};  arr[1] = {1, 2}; 这样是错误的。只能如上例一样赋值。
* 二维数组的静态初始化：
	1. int[][] arr = {{1,2,3}, {5,6,7}, {9,10,11}}; 元素数量固定的静态初始化。
	2. int[][] arr = {{1, 3, 5}, {1, 2}, {8}}; 元素数量不固定的静态初始化。
```java
// 二维数组的定义
int[][] testInt = new int[2][];
// 二维数组的赋值
testInt[0] = new int[] { 1, 2, 3 };
testInt[1] = new int[] { 4, 5 };
// 二维数组的遍历
for (int i = 0; i < testInt.length; i++) {
	for (int j = 0; j < testInt[i].length; j++) {
		System.out.println(testInt[i][j]);
	}
}
```
####数组操作的几个案例
```java
// 数组反序
int[] a = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
int temp = 0;
for (int i = 0; i < a.length / 2; i++) {
	temp = a[i];
	a[i] = a[a.length - 1 - i];
	a[a.length - 1 - i] = temp;
}
System.out.println(Arrays.toString(a));
// [9, 8, 7, 6, 5, 4, 3, 2, 1]

// bubble冒泡排序
int[] b = { 1, 22, 63, 43, 6, 12, 4, 56 };
int swap = 0;
for (int i = 0; i < b.length - 1; i++) {
	for (int j = 0; j < b.length - 1 - i; j++) {
		if (b[j] > b[j + 1]) {
			swap = b[j];
			b[j] = b[j + 1];
			b[j + 1] = swap;
		}
	}
}
System.out.println(Arrays.toString(b));
// [1, 4, 6, 12, 22, 43, 56, 63]

// select选择排序
int[] c = { 999, 22, 63, 43, 6, 12, 4, 56, 125 };
int swapInt = 0;
for (int i = 0; i < c.length - 1; i++) {
	for (int j = i + 1; j < c.length; j++) {
		if (c[i] > c[j]) {
			swapInt = c[j];
			c[j] = c[i];
			c[i] = swapInt;
		}
	}
}
System.out.println(Arrays.toString(c));
// [4, 6, 12, 22, 43, 56, 63, 125, 999]
```
------
##包
> 包就是文件夹，一个文件夹，就是一个包。
> 定义在一个文件夹中的n个文件，都是不需要引入直接使用的，因为他们都在同一个包中。
作用：对类进行管理。

####包管理方案
* 按照功能分。如：增加，删除，修改，查询分成包来管理。如：cn.itcast.add, cn.itcast.delete…
* 按照模板分(推荐)。如：老师的功能放一个包，学生的功能放一个包。如：cn.itcast.teacher, cn.itcast.stdunt
* 以上两种方案结合使用。先按模块分，再按功能分。

####包的定义
* 使用package关键字。多级包用“.”来分开。如：cn.itcast.teacher => cn/itcast/teacher

####包的注意事项
* package语句必须放在可执行代码的第一行。
* 一个类中只能定义一个包名。也就是说。一个类中，只能使用一次package语句。同php的namespace一样。
* 如果类不用package声明，则表示无包名。

####导入包
* 使用import关键字。格式：import 包名。
        1. 例子1(推荐)：import cn.itcast.student.StdentDemo
            ** 以上是类级别的导包。StdentDemo是一个具体的类名。
        2. 例子2（不推荐）: import cn.itcast.student.
* 所有的包中的类，都加上public修饰符。如：public class A {}
包的访问权限，可以查看权限修饰符相关内容。
------

##常用API
###Object
* java中所有类的父类。包括数组在内，所有对象都继承了Object类的方法和属性。由于Object中默认是无参构造，所以所有的子类不定义构造函数时，默认都使用它的无参构造。
* 该类的大多数方法，都可以使用编辑器来重写。
* 常用的方法：hashCode()，getClass()，toString()，equals()，clone()。
> 注：克隆出的2个对象的引用完全无关，都是独立的对象，互相不会影响。和a对象赋值给b对象，引用指向一个地址是2个概念。

###Scanner
* 作用：是个键盘输入类。
* 构造时的参数：一般是System.in，一个InputStream输入流对象。
* 常用方法：hasXxx() 和 nextXxx()方法。一个是判断，一个是获取。先判断，后获取。
>  注：该方法经常配合循环一起实用。如while (true), 可以一直处于等待输入状态，可以通过break退出输入。

###System
* 该类和系统运行相关，其中包含很多有用的方法和属性。所有成员都是静态的。
* 常用方法和属性：in,out,exit(),currentTimeMillis()等等。
package java.lang

#### System.gc()
```java
// 强行唤醒java垃圾回收机制(浪费资源不建议使用)
System.gc();
```

#### System.exit()
```java
// 退出当前运行java虚拟机
System.exit();
```

#### System.currentTimeMillis()
```java
System.out.println(System.currentTimeMillis());
// 输出时间戳(包含毫秒) 1481813610134
```

#### System.arraycopy()
```java
int[] a = {1,2,3,4};		
int[] b = {5,6,7,8};
System.arraycopy(a, 2, b, 2, 2);
System.out.println("a:"+Arrays.toString(a));
System.out.println("b:"+Arrays.toString(b));
// 输出
// a:[1, 2, 3, 4]
// b:[5, 6, 3, 4]
```

###String
* 概念：字符串就是由多个字符组成的一串数据，可以看成一个字符数组。
* 特点：
        所有的字面量的字符串，如："abc" 都是一个字符串对象。
        字符串是常量，一旦被赋值，就不能被改变。
* 理解字符串是常量：String str = "abc"; str += "def"; 
        字符串是在常量池里面分配的，以上操作一共产生了3个字符串，abc,def,abcdef
        不能改变指的是定义后就在常量池中存在，但是字符串str的指向是可以改变的，最终指向了abcdef。
* 字节和字符的说明：
        byte类型表示字节（-127~127之间的数字），字符串可以用字节或字节数组表示，比如：97 => a。{97，98}  => ab
        char表示字符，一个字符数组，就表示一个字符串。如：{'a', 'b'} => ab
* 字符串类型和其他类型的转换：
    > 其他类型数据 -> String：
    1. valueOf() : 把任意类型的数据（包括对象），转换为字符串。如：一个字节数字，字符数组，字节数组等。字符串类型转换成其他类型，推荐使用valueOf方法。
    2. toString() : 把任意类型数据，转换为字符串。
    3. 构造方法的不同参数，把数据转换成字符串。如：字节数组，字符数组等等。
String -> 其他类型数据：
    4. getBytes() : 把字符串，转换为字节数组。和String(byte[] bytes)构造方法相互对应。
    5. 使用基本包装类型的方法，把String转换为基本类型。
* 常用方法：查看api文档。
* String类不仅仅有字符串的基本操作功能，还有正则的功能，如：匹配，替换，分割等。

###StringBuffer
* 长度和内容可变的，线程安全的带缓冲区的字符串类，效率高于String类。
* 它自带了一个可扩充的缓冲区。
* String对象和StringBuffer对象的转换：
    转换的意义：前者转成后者的目的是，使用后者的功能。后者转为前者的目的是，希望返回的是前者的类型，直接可以使用。
    String => StringBuffer : 
        ** 通过构造方法转换：new StringBuffer(xx);
        ** 使用append()方法来转换。sb.append(xx);
    StringBuffer => String : 
        ** 通过构造方法转换：new String(yy)
        ** 通过toString()方法来转换。

###StringBuilder
* 它是一个非线程安全的字符串缓冲区类。在单线程中使用。效率更高。推荐在大多数应用场景中使用它。
* 常用API： 和 StringBuffer一模一样。

> 以上3个字符串处理类的差异：
        String，StringBuffer，StringBuilder对象，作为方法参数时的不同：
        String类型：它是特殊的引用类型，当成参数传入方法中，并且进行操作时，和基本类型一样，不会一改全改。
        StringBuffer和StringBuilder类型：当成参数传入方法中，并进行操作时，和其他引用类型一样，一改全改。

###Arrays
* 它是一个数组操作类，封装了数组的常用操作，如：排序，查找等。
```java
int[] a = { 2, 3, 45, 56, 6, 1 };
		
// 快速排序法排序数组
Arrays.sort(a);

// 友好打印的数组格式 数组看上去更加直观
System.out.println(Arrays.toString(a));
// [1, 2, 3, 6, 45, 56]

// 二分查找法查找元素在数组中的索引位置 没有找到则返回负数
System.out.println(Arrays.binarySearch(a, 45));
// 4
```

###Math
* 该类用于数学运算，提供一些数学中的常用操作。如：四舍五入，绝对值等等。
* 案例：设置一个1~100之间的随机数。(int) (Math.random() * (end - start + 1)) + start;

###Random
* 随机数类。但是在大多数情况下，还是Math.random更方便使用。
```java
Random r = new Random();
System.out.println(r.nextInt(20));
// 生成一个1-20之间的随机数(但不包括20)
```
------
###BigInteger
* 该类用于处理高精度的任意整型数的运算，无论大小。主要用于超出int范围的数值运算。

```java
// package java.math
BigInteger bi = new BigInteger("100");
// 加法
System.out.println(bi.add(new BigInteger(String.valueOf(50))));
// 150

// 减法
System.out
		.println(bi.subtract(new BigInteger(String.valueOf(50))));
// 50

// 乘法
System.out
		.println(bi.multiply(new BigInteger(String.valueOf(50))));
// 5000

// 除法
System.out.println(bi.divide(new BigInteger(String.valueOf(50))));
// 2

System.out.println("=================");
// 除法 保留余数
BigInteger[] res = bi.divideAndRemainder(new BigInteger(String
		.valueOf(50)));
// 商
System.out.println(res[0]);
// 2

// 余数
System.out.println(res[1]);
// 0
```
------
###BigDecimal
*  该类用于处理高精度浮点数，弥补float和double类型的精度缺失问题，解决这些问题。

精确运算 一般金融项目会用到
```java
// package java.math
BigDecimal bd1 = new BigDecimal("0.09");		
BigDecimal bd2 = new BigDecimal("0.01");

// 加法
System.out.println(bd1.add(bd2));
// 0.10

// 减法
System.out.println(bd1.subtract(bd2));
// 0.08

// 乘法
System.out.println(bd1.multiply(bd2));
// 0.0009

// 除法
System.out.println(bd1.divide(bd2));
// 9

// 除法 设置取舍位
System.out.println(bd1.divide(bd2,2,BigDecimal.ROUND_HALF_UP));
// 9.00
```
------
###Date
* 日期处理类。精确到毫秒。推荐使用Calendar类来处理日期时间。
* 关于Date和Sting的互相转换：使用SimpleDateFormate类。如：yy-mm-dd hh:ii:ss 这样的格式和Date对象的互转。
```java
//package java.util

Date d = new Date();
System.out.println(d);
System.out.println(d.getTime());
System.out.println(System.currentTimeMillis());
// Fri Dec 16 20:03:14 CST 2016
// 1481889794220
// 1481889794230
```
------
###SimpleDateFormate
* 日期时间格式化类。它有个父类，是DateFormate类。很多方法都可以参数父类的。
* 主要用于把Date对象转换为指定的字符串格式，或者把指定的字符串格式转换为日期。字符串 - Date，Date - 字符串。
* 注：字符串 - Date时，字符串的格式，必须和SimpleDateFormate的构造参数的格式一致才能使用。
* 案例：
    Date - String：
        ** Date d = new Date(); SimpleDateFormate sdf = new SimpleDateFormate("yyyy-MM-dd HH:mm:ss"); String s = sdf.format(d);
    String - Date：
        ** String str = "2015-12-25 12:25:35"; SimpleDateFormate sdf = new SimpleDateFormate("yyyy-MM-dd HH:mm:ss"); Date dd = sdf.parse(str);

```java
// package java.text
Date d = new Date();
// 格式化输出 Date对象为字符串
SimpleDateFormat sdf1 = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");

System.out.println(sdf1.format(d));
// 2016-12-16 20:21:27

// 格式化字符串为Date对象
String str = "2010-08-08 12:12:12";
SimpleDateFormat sdf2 = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
System.out.println(sdf2.parse(str));
// Sun Aug 08 12:12:12 CST 2010
```
------ 
###Calendar
* 该类表达日历时间。用于替代Date类使用。它是一个抽象类，不可以实例化。所有方法和属性都是静态的。
* 注：月的值是0~11，所以月都要+1。
* 案例1：获取当前的年：
    Calendar nowTime = Calendar.getInstance();
    int year = nowTime.get(Calendar.YEAR);
* 案例2：获取任意一年的2月的天数：
    int year = 2016;
    Calendar c = Calendar.getInstance();
    c.set(year, 2, 1); // 设置时间为2016年3月1日。
    c.add(Calendar.DATE, -1); // 减去1天就是2月的最后一天。
    System.out.println(c.get(Calendar.DATE)); // 打印这个日期就是一共有多少天
```java 
//package java.util.Calendar

// 获取日历类实例
Calendar c = Calendar.getInstance();

// 输出年
System.out.println(c.get(Calendar.YEAR));
// 输出月
System.out.println(c.get(Calendar.MONTH));
// 输出日
System.out.println(c.get(Calendar.DATE));

// 设置 年月日 日期
c.set(2015,2,3);

// 返回日期类 Date
System.out.println(c.getTime());
```
------
###正则表达式
* 字符：
    \\ ： 表示反斜线,2个\表示1个\。特定情况下可以用来转义使用。如：\\d, \\.
    \n : 换行。
    \r : 回车。
* 字符类：
     [abc] ： 匹配a或b或c中的一个。
     [^abc] ： 除了a或b或c之外的任意字符。
     [a-zA-Z0-9] : 表示区间范围中的一个。
* 预定义字符类：
    . 代表任意字符。
    \d，\D : 数字和非数字。
    \s, \S : 空白（空格）和非空白字符。
    \w, \W : 表示[a-zA-Z_0-9] 和 非这些字符。
* 边界匹配器：
    ^ : 匹配行的开头。
    $ ：匹配行的结尾。
    \b ： 单词边界。
* 数量词：
    ? 0次或1次。
    \* 0次或多次。
    \+ 1次或多次。
    {n} 恰好n次。
    {n,} 最少n次。
    {n,m} 最少n次，但不超过m次。
* 分组：
     () : 表示括号内的规则是一个组，一个整体。如：(\\.[\w]{2,3})+ 表示这一组规则，可以出现一次或多次。
* 防贪婪的惰性匹配符：
     *?	重复任意次，但尽可能少重复
     +?	重复1次或更多次，但尽可能少重复
     ??	重复0次或1次，但尽可能少重复
     {n,m}? 重复n到m次，但尽可能少重复
     {n,}?	  重复n次以上，但尽可能少重复
* 反向引用：
    (…)\n


####字符串匹配
String.matches(regex)
```java
String regex = "1\\d{10}";
String emailRegex = "\\w+@\\w+(\\.([a-zA-Z])+)+";

System.out.println("13300001111".matches(regex));
System.out.println("d@c.coma.d".matches(emailRegex));
// true
// true
```
####字符串分割
String.split(regex)
```java
String regex = "\\$";
String s = "dasfasfasf$sdafas$fsdfasd$fasd$asfasd$asdaaas$d$daasfa$";
System.out.println(Arrays.toString(s.split(regex)));
// [dasfasfasf, sdafas, fsdfasd, fasd, asfasd, asdaaas, d, daasfa]
```
####字符串替换
String.replaceAll(regex,replacement)
```java
String regex = "\\d";
String s = "helloqq123456worldkh897897897897java";
System.out.println(s.replaceAll(regex, "*"));
// helloqq******worldkh************java
```
####正则的使用
java.util.regex.Pattern;
java.util.regex.Matcher;
```java
String s = "jin tian xia yu le  da jia gao xin ma ";

Matcher m = Pattern.compile("\\b\\w{3}\\b").matcher(s);

while (m.find()) {
	System.out.println(m.group());
}
// jin
// xia
// jia
// gao
// xin
```
------

##java 访问权限修饰符
|   访问权限    |   类    |   包  |   子类  |   其他包  |
| :--------:|:---------:|:---------:|:---------:|:---------:| 
| public    |   Y   |   Y   |   Y   |   Y   |
| protect   |   Y   |   Y   |   Y   |   X   |
| default   |   Y   |   Y   |   X   |   X   |
| private   |   Y   |   X   |   X   |   X   |

