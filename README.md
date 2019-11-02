```created God the heaven... ...בָּרָא אֱלֹהִים אֵת הַשָּׁמַיִם```

# `vs`
试着做个玩具(计算机用)语言, 它应该 `极为简单`, `极为自然`, `极易处理`.

在参考了人类自然语言和现有计算机语言的特点之后, 这里决定采用 `谓状主宾结构`(类似圣经希伯来语, 古典阿拉伯语和许多玛雅语族语言).
每条语句, 
- 必须有且只有一个`谓语`
- 必须有若干个`宾语` (个数为0时, 需用`()`占位)
- 可以有零到若干个`主语`(个数为0时, 直接省略, 无需占位)
- 存在主语时可以加若干个`修饰词`(个数为0时, 直接省略, 无需占位)

即, `vs`的合法语句只有如下三种句式:
- `Verb ( O1 O2 ... )`
- `Verb @ S1 S2 ... ( O1 O2 ... )`
- `Verb ~ M1 M2 ... @ S1 S2 ... (O1 O2 ...)`

应用场景: 通用过程描述, 日常问题求解

## 内置数据类型
- 布尔型(Bool, 8bit), 整型(Int, 64bit), 实型(Real, 64bit), 复型(Complex, 128bit), 字符串(String), 句柄(Handle)
- 列表(List, 用`{}`定义), 自定义数据类型

## 内置操作类型
- 内置数据类型相关操作(访问列表元素用: `[]`, 撇号可括起表达式而不求值)
- 函数(Wrap), 函数列表

## 语法结构
### 顺序
```
Var~Int@x() # x是整型变量, 初始值为0
Var@x(15) # x是整型变量, 初始值为15
Var@x1({15, 50}) # x1 is a List # 逗号可以省略
Var@y(real(0)) # Var~Real@y(0) 0.0 
Var@z(`Real(1 2 3)`) # 将列表`{{Real} {} {} {1 2 3}}`赋值给z, 在这里不会对表达式求值
Var@a, b, c(1 '3' 5.0) # 逗号可以省略
Var@x(Scan@Con("Please input a number:"))

Val@y(5) # x是整型常量, 初始值为5

Print@Con("Hello, world!")
Print@Con(z[-1] z[0]) # {1 2 3} {real}
Print@File1("Hello, world!")
=@x(9) # assign Value 9 to x

Map @ FunctionA ({a b c e d f g h i j k l}) # map
Reduce @ FunctionB ({a b c e d f g h i j k l}) # reduce
Pipeline @ {FuncA FuncB FuncC FuncD}(xxx) # FuncD(FuncC(FuncB(FuncA(xxx))))
Times 3 @ Func(xxx) # Func(Func(Func(xxx)))

Math('3 + $a$ * (5 - $c$)') # easy reading eqs. # a c are Vars
Print@Con(' $06I:a$ $\t$ && $\t$ (5 > $b$ + $6.3R:c$) $\n$$$') # 字符串转义与打印
Eval( `...` ) # Eval `vs` expr (yet another list)
Exec( "..." ) # Exec `vs` source codes in string
```

### 分支
```
Case(
      {==(varX      "DNBE") Print@Con("Do NOT Be Evil!\n")} # 双引号串不转义
      {==(varX[-4:] "TING") Print@Con("That is not good!")}
      {True                 Print@Con("Listen Well Google!")} # 所有其他情况
      )
```

### 循环
```
Loop~index value@ListY(
    Print@Con(index value) # index is loop cursor index of the list, value is assigned the list items
    Print@Con("Hello, world!")
    )


Loop~value@ListY(
    Print@Con(value)
    )
```

### 函数
```
Wrap~p1 p2 p3@funZ ObjZ( # ...
     # fields in ObjZ can be accessed and updated by funZ
     # no side effect
     )

funZ@O1(1 2 3) # o1 can be updated


Wrap~q1 q2 q3@ mac (
     # can return something
     # no side effect
     )

mac(12.3 23 45.6)

Var ~ Int @ fn ( # 指定返回值类型
    Wrap ~ x y z @ _ ( # 匿名函数
        # ------
    ))
```

### 库
```
Package("main")

Import("Linear" "../PlotLib")
Import("ML/Trees/RF")
Import( {"Math/Plotlib" Plt} ) # import plotlib as plt; no sub lib
=@x(Linear.Matrix.Transpose( {{1 3} {5 9}} )) # is not this complex?
```
