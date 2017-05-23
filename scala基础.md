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

2.  常用类型  
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
7.  if语句也有返回值  
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
超类型：Any  
if..else语句有返回值：  
>if(x>0) 1等价于
>if(x>0) 1 else ()在scala中每一个表达式都有值，这个时候scala引入一个Unit类,写作()

8. 块表达式和赋值：在scala中{}包含一系列表达式，其结果也是一个表达式，块中最后一个表达式的值就是块的值。    
赋值动作本身是没有值的，严格的说它的值是Unit类型的。   

9. scala中循环：  
>for(i 1 to 10){}
> for(i 0 util s.length){}
> var sum = 0
> for(ch <- "hello")sum +=ch

	scala中没有break和continue，退出循环可以使用以下方法：   
    - 使用Boolean类型的控制变量
    - 使用嵌套函数，从函数中return
    - 使用Breaks对象中的break方法

	scala中的高级for循环和for推导式
``` scala
    import scala.math._
    import scala.util._
    object Hello {
      def main(args: Array[String]): Unit = {
        println(sqrt(4))
        var name: String = readLine("请输入你的姓名：")
        printf("你的名字%s\n",name)
        var sum: Int = 0
        for(i <- 1 to 10){
          sum += i
        }
        println("sum:"+sum)
        var s: String = "hello"

        //高级for循环
        for(i <- 1 to 10; j <- 2 to 16 if i!=j){
          println(i*j)
        }

        var lower: String = ""
        //大写变小写
        for(ch <- "ABCDEFGHIJKLMN";upper = ch + 32){
          lower += upper
        }
        println(lower)
        println(cal(2,3))
      }
      //非递归函数不需要指定返回类型，函数本身可以根据最后一个表达式来推测返回类型
      def cal(x: Int,y: Int) = {
        x+y
      }

      //变长参数
      def calculate(args: Int*)={
        var sum = 0
        for(i<-args){
          sum += i
        }
        sum
      }
      //没有返回值的函数成为过程
      def printHello(): Unit = {
        println("hello")
      }
    }
```
`lazy val words = scala.io.source.fromFile("/usr/java/words").mkString`   

10. 异常处理:scala中没有受检异常

## 三.数组相关操作
``` scala

    import scala.collection.mutable.ArrayBuffer  
    import sun.font.TrueTypeFont
    import com.sun.beans.decoder.FalseElementHandler

    /**
     * @author admin
     * 数组相关操作
     */
    object ArrayTest {
      def main(args: Array[String]): Unit = {
        /*
         * 定长数组Array
         */
        //10个整数的数组，所有元素的初始化值为0
        var num = new Array[Int](10)
        //10个字符串，初始化值为null
        var strArr = new Array[String](10)
        //对于直接初始化的数组不需要使用new
        var nameArr = Array("andy","tom")
        //数组元素的访问使用(下标),不是[]
        nameArr(0) = "hoo"

        /*
         * 变长数组,数组缓冲ArrayBuffer
         */
        var b: ArrayBuffer[Int] = new ArrayBuffer[Int]() //或者 var b: ArrayBuffer[Int] = new ArrayBuffer[Int]
        //+=在尾端添加元素
        b+=1
        //添加多个元素时用()
        b+=(1,2,3,4)
        //使用++=添加任何集合
        b++=Array(4,5,6)
        //尾端移除最后几个元素
        b.trimEnd(5)
        //插入和移除操作
        b.insert(2,6) //在下标为2的位置插入6
        b.insert(2,7,8,9) //在下标为2的位置插入7,8,9
        b.remove(2) //移除下标为2的元素
        b.remove(2,3) //移除下标为2和3的元素

        //ArrayBuffer转换Array
        var bArr = b.toArray
        //Array转换为ArrayBuffer
        var bBuffer = bArr.toBuffer

        /*
         * 遍历数组和数组缓冲,遍历方法一样
         */
        for(i <- 0 until bBuffer.length){
          println(bBuffer(i))
        }

        //每隔两个元素访问下
        for(i <- 0 until (bBuffer.length,2)){
          println(bBuffer(i))
        }
        //倒序访问
        for(i <- (0 until bBuffer.length).reverse){
          println(bBuffer(i))
        }

        //数组转换for(....)yield ...创建一个与原始类型相同的集合,原始集合不受影响
        var bBuffer2 = for(num <- bBuffer) yield num*2
        
        //多维数组1.Array.ofDim[Double](3,4)
        var matrix = Array.ofDim[Double](3,4)
        
        //不规则的二维数组
        var matrixs =new Array[Array[Int]](3)
        for(i <- 0 until matrixs.length){
          matrixs(i) = new Array[Int](i+1)
        }
      }
      //移除一个数组中第一个负数之外的所有负数
      def removeNagative(buffer: ArrayBuffer[Int]) = {
        var first = true
        val indexes = for(i <- 0 until buffer.length if buffer(i)>0 || first) yield {
          if(buffer(i)<0) first = false
          i
        }
        for(j <- 0 until indexes.length)buffer(j) = buffer(indexes(j))
        buffer.trimEnd(buffer.length-indexes.length)
      }
    }
```

## 四.常用算法
``` scala
	
import scala.collection.mutable.ArrayBuffer
/**
 * @author admin
 * 常用的算法
 */
object AlgorithmTest {
  def main(args: Array[String]): Unit = {
    //1.求和,求和的元素必须是数值类型
    var sum = Array(10,20,40.0,45).sum
    
    //2.最值
    var max = ArrayBuffer(1,45,67).max
    var min = ArrayBuffer("hello","nihao","sawadika").min
    
    //排序
    var b = ArrayBuffer(23,34,23,45,67)
    //val sort = b.sorted(_ < _)
    
    //对数组进行排序
    var arr = Array(23,13,4,54)
    scala.util.Sorting.quickSort(arr)
    
    //mkString方法,可以指定分割符
    println(arr.mkString(" and "))
    println(arr.mkString("<",",",">"))
  }
}
```

## 五.映射和元组
映射:
``` scala
	import java.util.HashMap
    import scala.collection.JavaConversions.mapAsScalaMap
    import scala.collection.JavaConversions.mapAsJavaMap


    /**
     * @author admin
     * 映射相关操作(映射是对偶的集合,对偶就是两个值构成的组,使用操作符->构建对偶，如："andy"->100,可以写成("andy",100))
     */
    object MapTest {
      def main(args: Array[String]): Unit = {

        //构造一个不可变的映射,等价于 val scores = Map(("andy",100),("tom",60),("lucy",40))
        val scores = Map("andy"->100,"tom"->60,"lucy"->40)
        //构造一个可变的映射
        var mutableScores = scala.collection.mutable.Map("karen"->23,"rubin"->245)
        //构造一个空的映射
        var newScores = new scala.collection.mutable.HashMap[String,Int]

        //获取映射中的值,如果映射中不包含请求的键值则会报错，可以使用contains()方法检查
        var andyScore = if (scores.contains("andy")) scores("andy") else 0
        //上面表达式的简写方法
        var andySco = scores.getOrElse("andy", 0)

        //更新映射中的值
        mutableScores("karen") = 120

        //映射中添加元素
        mutableScores+=("andy"->150,"jeery"->130)

        //删除映射中的元素
        mutableScores -= "jeery"

        /*
         * 映射的迭代
         */
        for((k,v)<-mutableScores){
          println(k+":"+v)
        }
        //获取所有的键
        var keys = mutableScores.keySet
        for(key <- keys){
          println(key)
        }

        //获取所有的值
        var values = mutableScores.values
        for(value <- values){
          println(value)
        }

        //反转映射：映射的键值互换
        var reverseMap = for((k,v)<-mutableScores)yield (v,k)

        //已排序映射，树形映射
        //var sortedMap = scala.collections.Immutable.SortedMap("andy"->100)

        //java中的映射转换为scala映射
        var sm: scala.collection.mutable.Map[String,Int] = new java.util.TreeMap[String,Int]

      }
}
```

元组：
``` scala

    /**
     * @author admin
     * 元组相关操作 (元组：一组不同类型值的聚集)
     */
    object TupleTest {
      def main(args: Array[String]): Unit = {
        var t0 = Tuple3[Int,String,Double](1,"andy",45.7)
        var t = (1,"andy",45.7)
        //访问元组中的每个组元,元组中的下标从1开始,t._1 可以写成t _1
        val no = t0._1
        val name = t0._2
        val weight = t0._3

        println("编号:"+no+",姓名:"+name+",体重:"+weight)

        //通常会采用匹配模式来获取元组的值,在不需要的值的位置上加上_即可
        val (first,second,third) = t

        //拉链操作
        val symbols = Array("<","-",">")
        val count = Array(2,10,2)
        val pairs = symbols.zip(count)

        for((s,c)<-pairs)Console.print(s*c)
        pairs.toMap

      }
}	
```

