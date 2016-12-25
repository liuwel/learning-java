#Learning Java
------
##java数据类型
|   类型    |   长度(字节)    |   默认值  |   默认封箱类  |
| :--------:|:---------:|:---------:|:---------:|:---------:| 
|   byte    |   1   |   0   |java.lang.Byte|
|   short   |   2   |   0   |java.lang.Short|
|   int     |   4   |   0   |java.lang.Integer|
|   long    |   8   |   0   |java.lang.Long|
|   float   |   4   |   0.0   |java.lang.Float|
|   double   |   8   |   0.0   |java.lang.Double|
|   char   |   8   |   0.0   |java.lang.Character|
|   boolean   |   1/8   |   false   |java.lang.Boolean|

#### 整型默认类型是int 浮点默认类型是 double
```java
// 给long类型数据赋值格式 
long l = 33342L;

// 给float类型赋值格式
float f = 2.3F;
```

#### int类型自动装箱 byte值范围之内的对象 是被jdk缓存起来的 所以 byte范围内打封装对象是同一个


##java 访问修饰符



##正则表达式
package java.util.regex
字符串匹配
String.matches(regex)
```java
String regex = "1\\d{10}";
String emailRegex = "\\w+@\\w+(\\.([a-zA-Z])+)+";

System.out.println("13300001111".matches(regex));
System.out.println("d@c.coma.d".matches(emailRegex));
// true
// true
```
字符串分割
String.split(regex)
```java
String regex = "\\$";
String s = "dasfasfasf$sdafas$fsdfasd$fasd$asfasd$asdaaas$d$daasfa$";
System.out.println(Arrays.toString(s.split(regex)));
// [dasfasfasf, sdafas, fsdfasd, fasd, asfasd, asdaaas, d, daasfa]
```
字符串替换
String.replaceAll(regex,replacement)
```java
String regex = "\\d";
String s = "helloqq123456worldkh897897897897java";
System.out.println(s.replaceAll(regex, "*"));
// helloqq******worldkh************java
```
正则
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

## System
package java.lang

### System.gc()
```java
// 强行唤醒java垃圾回收机制(浪费资源不建议使用)
System.gc();
```

### System.exit()
```java
// 退出当前运行java虚拟机
System.exit();
```

### System.currentTimeMillis();
```java
System.out.println(System.currentTimeMillis());
// 输出时间戳(包含毫秒) 1481813610134
```

### System.arraycopy()
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

------
##BigInteger
package java.math
大整型运算
```java
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

##BigDecimal
package java.math
精确运算 一般金融项目会用到

```java
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
## Date
package java.util
```java
Date d = new Date();
System.out.println(d);
System.out.println(d.getTime());
System.out.println(System.currentTimeMillis());
// Fri Dec 16 20:03:14 CST 2016
// 1481889794220
// 1481889794230
```
## SimpleDateFormat
package java.text
日期格式化
```java
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
##Calendar
日历类
package java.util.Calendar
```java 
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



