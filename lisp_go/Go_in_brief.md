# Go语言简明教程

```
2016年12月05日 10:44:32 HinaKaze 阅读数 3700
版权声明：本文为HinaKaze原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。
本文链接：https://blog.csdn.net/muxxpkq/article/details/53463071 (转载时略有删节)
```

## 简介
### 创立时间
- 2007年 google作为20%项目开始研发
- 2009年11月10日 开源，获得TIOBE年度语言
- 2012年3月28日 发布Go1.0版本
- 2016年8月18日 发布Go1.7版本

### 创始人
- Robert Griesemer (V8,Chubby,HotSpot JVM)
- Rob Pike(Unix,UTF-8,plan9)
- Ken Tompson(B语言、C语言、Unix之父，图灵奖)
- lan Lance Taylor(GCC)
- Brad Fitzpatrick(Memcache,HTTP2)

### 吉祥物
[gopher：囊地鼠（产自北美的一种地鼠）](https://github.com/golang/go/blob/master/doc/gopher/favicon.svg)

### 设计初衷
- 设计Go语言是为了解决当时Google内部开发的一些痛点

#### 所处的环境：
-    大量的C++代码，同时又引入了Java和Python
-    成千上万的工程师（C系为主）
-    分布式的编译系统
-    数以百万记行的代码
-    数以万记的服务器

#### 遇到的问题是：
-    新的C-like语言需求
-    语法繁杂、代码难以维护
-    失控的依赖
-    编译速度慢
-    交叉编译困难、难以部署

所以Go语言是一门工程上的实用主义语言

### 特点
-    C-like 语法风格
-    强一致类型（静态语言）
-    struct组合复杂类型
-    function和Method
-    没有异常处理（Error is value）
-    基于首字母的访问控制
-    多余的import和变量会引起编译错误
-    内置GC
-    完备的标准库包（网络编程、系统编程、互联网应用）
-    支持各种编程范式：过程式编程、面向对象编程、函数式编程

## 语言要素
### 标识符
-    代表一个变更或者一个类型，可以被看作是变量或者类型的代号或者名称
-    若干字母、下划线（_）和数字组成的字符序列，第一个字符必须为字母
-    在一个代码块中，不允许重复声明同一个标识
-    预定义标识符
     +   所有基本数据类型的名称
     +   接口类型 error
     +   常量 true、false 以及 iota
     +   所有内置函数的名称，即 append、cap、close、complex、copy、delete、imag、len、make、new、panic、print、println、real和 recover

### 关键字
-    又称保留字，不允许被使用为标识符
-    25个关键字：
```				
break 	default 	func 	interface 	select
case 	defer 	go 	map 	struct
chan 	else 	goto 	package 	switch
const 	fallthrough 	if 	range 	type
continue 	for 	import 	return 	var
```
- 程序声明：import、package
- 程序实体声明和定义：chan、const、func、interface、map、struct、type、var
- 程序流程控制：go、select、break、case、continue、default、defer、else、fallthrough、for、goto、if、range、return、switch

### 字面量
-    表示值的一种标记法
-    用于表示基础数据类型值的各种字面量
     +   数字 2016,1e9,1+2i
     +   字符串 “iota”
     +   布尔值 true,false
-    用户构造各种自定义的复合数据类型的类型字面量

```
type Person struct {
    Name string
    Age uint8
    Address string
}
```

-    用于表示复合数据类型的值的复合字面量
     +   struct,array,slice,map构造的值
     `   Person{Name: “Eric Pan”, Age: 28, Address: “Beijing China”}`

### 操作符和分隔符
```
+ 	& 	+= 	&= 	&& 	== 	!= 	( 	)
- 	| 	-= 	|= 	|| 	< 	<= 	[ 	]
* 	^ 	*= 	^= 	<- 	> 	>= 	{ 	}
// 	<< 	/= 	<<= 	++ 	= 	:= 	, 	;
% 	>> 	%= 	>>= 	– 	! 	… 	. 	:
&^ 	&^= 							
```

### 优先级
```
优先级 	操作符
5 	* / % << >> & &^
4 	+ - | ^
3 	== != < <= > >=
2 	&&
1 	||
```

### 类型
-    基本类型
     +   bool
     +   int/uint
     +   int8/uint8/byte
     +   int16/uint16
     +   int32/uint32/rune
     +   int64/uint64
     +   float32/float64
     +   complex64/complex128
     +   string
     
-    复杂类型
     +   Array
     +   Slice
     +   Map
     +   Struct
     +   Interface
     +   Function
     +   Channel
     +   Pointer
     
-    潜在类型
     +   type MyString string //MyString是实际类型，string是潜在类型

-    静态类型和动态类型
    + 除了interface都为静态类型，interface的动态性体现在运行时与该interface变量绑定在一起的值的实际类型

## 语法
### 变量/常量定义
```
    var v Type
    var v Type = value
    var v = value
    var v1,v2,v3 Type
    var v1,v2,v3 Type = value1,value2,value3
    var v1,v2,v3= value1,value2,value3
    v1,v2,v3:= value1,value2,value3
    i,j = j,i
//Tips：:=为简短声明，编译器根据初始化的值自动推断相应的类型，但是不能定义在函数外部使用。
    const cname = value
    const cname type  = value
//Tips：声明但未使用的变量会在编译阶段报错。
    //声明分组
    import（
    “fmt”
    “os”
）
const(
    s = “string”
    pi = 3.1415
    pi2
)
var(
    i int
    pi float32 = 3.1415
)

iota枚举：为分组中iota++
const(
a = 1+iota*2
b
c = “iota”
d
)
```

### array & slice
#### array定义
```
    var a [2]int = [2]int{1,2}  
    a := [2]int{1,2}    
    a := [...]int{1,2,3,4}
    a2 := [2][3]int{[3]int{1,2,3},[3]int{3,2,1}}    
    a2 := [2][3]int{{1,2,3},{3,2,1}}
```

#### slice定义
slice 是引用类型
```
    var s []int  = make([]int,n)
    s := []int{v1,v2,v3}

// slice操作
    copy(dst,src []Type)int //dst必须初始化完成，长度根据需要初始化
    append(slice []Type,elems ...Type)[]Type
    len(slice []Type)int
    cap(slice []Type)int

// slice切片
    s[:j] == s[0:j]
    s[i:] == s[i:len(s)]
    s[i:j]:包含index区间为[i,j)s的元素
    //不能代替array和slice的copy操作，切片后是原数据的引用
```

### map
引用类型，无序，长度不定，非线程安全
```
var m map[keyType]valueType //keyType可以是string及完全定义了==/!=操作的类型
m := make(map[keyType]valueType)
m:=map[keyType]valueType{k1:v1,k2:v2,k3:v3}
len(m map[keyType]valueType)int
delete(m map[Type]Type1,key Type)
```

### channel
引用类型，goroutine之间通信的通道
```
    c := make(chan Type,n)//不初始化为nil
    c 

// 单向channel
    var c chan

// channel操作
    close(ch)
    /*
关闭一个已关闭的channel会导致panic
向已关闭的channel中写数据会导致panic
从已关闭的channel中读数据不会导致panic   
```

### 流程控制
#### if/else
```
    if x := getX();x > 0{
    //...
}else if x == 0{
    //...
}else{
    //...
}//依次逐条匹配，若匹配则进入逻辑块
```

#### switch/case
```
case e1:
    //...
case e2，e3:
    //...
    fallthrough
default:
    //...
}
//sExpr需要和case的expr类型一致，如果sExpr不存在，则比较类型为bool，只有true可以被匹配
```

#### for
```
for e1;e2;e3{
}
for expression{
}
//for + range 遍历slice和map数据
```

- break：跳出当前循环，可以配合标签使用
- continue：跳过本次循环，可以配合标签使用
- for+range 遍历array/slice/map/string，循环接收channel中的数据

Range expression 1st value 2nd value
array or slice a [n]E, *[n]E, or []E index i int a[i] E
string s string type index i int see below rune
map m map[K]V key k K m[k] V
channel c chan E, <-chan E element e E

#### select
多channel的场景中，使用select机制，监听各个channel上的数据流动，默认阻塞，当监听的channel中有发送或可接收时才会工作，所有channel都准备好时，随机选择一个执行

#### goto
```
func myFunc(){
    i := 0
Here:
    i++
    goto Here
}
```

### 函数
#### 声明
```
    func funcName(input1 Type,input2 Type)([output1] Type,[output2] Type){
    return value1,value2
}
```

- 只有一个返回值且不声明返回变量，返回值的括号可以省略
- 没有返回值可以省略包括返回值的括号，且可以不需要return
- 如果有复数个相同Type的参数或返回值，可以省略重复Type声明，比如(a int,b int) =>(a,b int)
- 如果函数是导出的，建议命名返回值，提高可读性

#### 变参
```
func funcName(arg ...Type){}
//arg为[]Type
```

- 支持多值返回
- 传值和传指针
    + 使用指针类型传参
    + 可以共同操作同一对象
    + 传指针很轻量级，8B（64位机），对一些大的struct，在copy上会花费较多的系统开销

#### 匿名函数和闭包
First-class value:可以作为别的函数的参数、返回值，可以赋值给变量，或者成为类型，函数式编程范式
```
func adder() func(int) int {
     sum := 0
     return func(x int) int {
          sum += x
          return sum
     }
}
```

#### 特殊函数
- defer函数
```
//在函数返回之前，先进后出执行defer语句，一般在需要资源回收的时候使用
```

- main函数
```
func main(){
    //...
}
//package main中必须包含一个main函数，是程序的入口函数
```

- init函数
```
func init(){
 //some init logic...
}
/*一个package中最好只写一个init
    1.如果package中需要import其他包，则先导入其他包
    2.所有包import完毕后，依次初始化cons->var->init()
*/
```

### 错误处理
- panic

中断控制流程，之前入栈的defer函数依然会执行，然后返回到被调用的地方，调用方也认为触发了panic行为。依次向上，直到发生panic的goroutine上所有调用函数返回，导致程序退出
来源：调用panice，runtime error（数组越界，0值除数）

恢复panic，存在于defer函数中才有效

### 面向对象

#### struct
一种自定义用户类型
: 初始化
```
P := person{“iota”,22} //顺序初始化
P := person{age:22,name:”iota”} //field:value初始化
P := new(person) //new初始化
```

: 匿名字段
匿名字段可以是任意内置类型、struct、自定义类型
匿名字段命名冲突问题：最外层访问优先

#### method
-    声明与函数的声明语法几乎一致，但是多了一个receiver部分，表示method依赖的主体
-    “A method is a function with an implicit first argument, called a receiver.”
-    receiver的值传递和引用传递，引用传递相当于OO语言中的this
-    可以定义在包括struct在内的任何自定义类型（c中的typedef）、内置类型
-    无论receiver是指针还是值，go都会自动相互转换
-    继承method后可以重写method
-    通过声明开头的大小来表明是否可以导出

#### interface
-    一组method签名的组合
-    如果某个struct实现了某个接口的所有方法，则- 此对象就实现了此接口
-    Any类型：interface{} like void*
-    interface{}的类型转换：
-    断言：value,ok = element.(T)
-    switch:T := element.(type),这种语法只能在switch代码块中使用，default表示的意义
-    embedded interface
```
     type ReadWriter interface{
     Reader
     Writer
     }
```

#### package
-    package相当于python中的module
-    大写字母开头的变量和函数是可导出的，是public的
-    小写字母开头的变量和函数是不可导出的，是private的
-    import：导入package的方式
-    类似树结构的深度优先遍历
-    若包已加载，则跳过
-    包的初始化顺序：const、var、init()
-    依次从GOROOT、GOPATH（可能有多个）寻找目标package
-    点import：使用包的导出资源时，可以省略包名
-    别名import
-    预加载import：不引入包，只是调用该包的init()，比如数据库驱动的加载
-    禁止循环导入，禁止导入包未使用

#### 面向对象特性
-    封装、继承、多态
-    类的定义
-    interface：动态绑定
-    Any类型：interface{}
-    包管理：public、private、import

### reflect
-    检查程序在runtime的状态
-    reflect.Type 类型定义: reflect.TypeOf(v)
-    t.Elem().Field(0).Tag
-    reflect.Value 存储的值: reflect.ValueOf(v)
-    v.Elem().Field(0).String()
-    Kind()：潜在类型的实际类型
-    若要改变原始变量的值，需要反射变量的指针
```
     var x float64 = 3.4
     p := reflect.ValueOf(&x)
     v := p.Elem()
     v.SetFloat(7.1)
```

### 并发模型
-    Goroutine：协程、轻量级、底层混合使用nonblockingIO和线程、极小栈内存
-    Channel：功能（传值&同步）读写阻塞
-    Select：同时监听多个channel
-    CSP（Communicating sequential processes）通信顺序进程
-    通过通信来共享、而不是通过共享来通信

### runtime
-    Goexit:退出当前goroutine，但是defer正常执行
-    Gosched：让出当前goroutine的执行权限，调度器安排其他goroutine执行，并在下次某个时候从该位置恢复执行
-    NumCPU：返回CPU数量
-    NumGoroutine：返回正在执行和排队的任务总数
-    GOMAXPROCS：设置并行计算的最大CPU核数，并返回之前设置的值-

### go命令
```
    go build
    go clean
    go run
    go install
    go get
    go tool
    go doc
    go env
    go version
```

### 常用类库
```
    运行时：runtime,runtime/debug,runtime/pprof,runtime/cgo
    系统库：os
    网络库：net,net/http,net/rpc
    io操作：io、io/ioutil,
    编码库：json,base64,xml
    压缩库：gzip
    加密库：MD5,SHA-1,SHA-256,aes,des,rsa
    同步：sync，sync/atomic
    数据库：database/sql
```

## 语言对比
```
C/C++
    上限高：速度更快、内存利用率高
    下限低：内存泄漏、core dump
    语言层级没有对并发支持、调用os的并发机制（线程、进程）

Java
    语言繁琐
    语言层级的线程并发支持
    开发效率低

PHP/PYTHON/RUBY
    开发效率快，但是差距不大
    运行速度慢
    语言层级裸用os的并发机制
```


### 优势
```
    学习曲线平滑
    容易写出健壮、稳定、高性能的程序
    开发效率高（近PHP的开发效率）
    运行性能好（近C的运行效率）
    语言层级多核并发支持，且简单易用
    二进制文件、Copy部署
    运行快、开发快、部署快
```
