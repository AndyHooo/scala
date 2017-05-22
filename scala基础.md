# scala学习笔记
## 一.基础  
1. 变量  
val标识符：声明常亮;如：val answer = 1  
var标识符:声明变量;  
- 类型推断:变量的类型由scala根据初始化变量的表达式推断而来;  
  鼓励使用val;  
  注:声明变量时不做初始化会报错.  
- 明确类型:scala的变量或函数的类型总是写在变量或函数的后面。  
``` scala
val a:Int = 1
val str:String = 2
```
2. 常用类型  
scala支持7种数值类型和1种Boolean类型。  
	- Byte/Char/Short/Int/Long/Float/Double
	- Boolean  
	
注：所有这些类型都是类，Scala并未区分基本类型与引用类型。如，可以调用1.toString方法。    

3. 数值类型转换：   
scala中使用方法，而非强制类型转换来做数值类型之间的转换。如，  
>scala\>99.44.toInt
>res2:Int = 99
>
>scala\>99.44.toChar
>res3:Char = c
>
>scala\>99.44.toLong
>res4:Long = 99
>
>scala\>"99.445".toDouble
>res5:Double = 99.445

4. 操作符  
scala支持Java中的绝大多数的操作符，不过所有的操作符都是方法。如：  
a+b是a.+(b)的缩写  
即：a方法b是a.方法(b)的缩写，两种写法可以互换。  
【注：scala中不支持++和--操作符】
5. 函数调用和方法  
常用的数学函数包括在scala.math包中，可以通过如下的语句引入包。  
``` scala
import scala.math._   //scala中，字符_是通配符，类似java中的*
```
另外，以scala开头的包，在引入时可以省略scala.
``` java
import math._
math.sqrt(2)
```
【注：scala中没有静态方法。】  
不带参数的方法在调用时可以省略括号，如：
`"helloworld.toString"`
6. apply方法  
在scala中通常使用类似函数调用的形式来访问数组，链表等的元素。如：
>scala\>"hello"(0)
>res0:Char = h         

上述调用中，"hello"(0)是"hello".apply(0)的调用。其中apply方法是StringOps类中的方法。
## 二.控制结构和函数  
1. if语句也有返回值  
if语句称为条件表达式，如：  
>scala\>val x = 3
>x:Int = 3
>scala\>val y = if(x>1)1 else -1
>y:Int =1

条件表达式的结构为：`if(判断条件)值1 else 值2`  
该条件表达式可以用来初始化常量。   
注：scala中每个表达式都会返回值，如
>scala\>if(x>4)1
>res0:AnyVal = ()

条件表达式返回了(),其中()表示Unit类，表示没有值。可以看作java中的void类型。

未完待续：[scala学习基础](http://www.cnblogs.com/-crazysnail/p/3980024.html)
