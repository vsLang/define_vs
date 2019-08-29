```
... בָּרָא אֱלֹהִים אֵת הַשָּׁמַיִם
created God the heaven
```

# vs
试着做个玩具(计算机用)语言, 它应该 `极为简单`, `极为自然`, `极易处理`.

在参考了人类自然语言和现有计算机语言的特点之后,
这里决定采用 `谓主宾结构`(如古希伯来语), 基本句式只有两种(宏与函数):
- `verb(o1 o2 ...)`
- `verb@sub(o1 o2 ...)`

与绝大多数计算机语言一样, 这里不引入对vso各部分的修饰语(定补状).

应用场景:  通用过程描述, 日常问题求解

- 看起来像是`Lisp`的一个方言呢
- 好吧, 根本就是一个`Lisp`方言
- 我也全然不知道为什么会这样...

## 内置数据类型
- 布尔型(bool, 8bit), 整型(int, 64bit), 实型(real, 64bit), 复型(complex, 128bit), 字符串(string), 句柄(handle)
- 列表(list, 定义时用: `{}`), 自定义数据类型

## 内置操作类型
- 内置数据类型相关操作(访问列表元素用: `[]`; 改变运行次序用: `()`)
- 函数(wrap), 函数列表

## 语法结构
### 顺序
```
let@x(15)
let@y(real(0))
let@z({real(123)}) # 将列表{...}赋值给z, 在这里不会对表达式求值

print@con("Hello, world!")
print@con(z[1] z[0])
print@file1("Hello, world!")
=@x(9) # assign value 9 to x
```

### 分支
```
case@varX(
      ('NG' print@con('not good'))
      ('DNBE' print@con('do NOT be evil! listen well, Google!'))
      )
```

### 循环
```
loop(value index)@ListY(
    print@con(index) # index means loop cursor index on the list
    print@con(value) # value is assigned the list item value now
    )


loop(value)@ListY(
    print@con(value)
    )
```

### 函数
- no really funcs here. Just marcos

```
wrap(funZ ObjZ)@(p1 p2 p3)( # ...
     # fields in ObjZ can be accessed and updated by funZ
     # no side effect
     )

# call:
funZ@O1(1 2 3)


wrap(mac)@(q1 q2 q3)(
     # can return something
     # no side effect
     )

# call:
mac(12.3 23 45.6)
```
