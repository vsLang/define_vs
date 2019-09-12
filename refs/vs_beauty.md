# `Lisp之美`代码的`vs`重现

- 清单 1. 简单原子
```
1
a
```

- 清单 2. 延迟求值和引用
```
`a`
`Append@{tigers bears}(lions)`
```

- 清单 3. 键入一个简单列表
```
{1 2 3}  # 并不自动求值
```

- 清单 4. 基本 Lisp 函数
```
{lions tigers bears}[0]
lions
 
{lions tigers bears}[1:]
{tigers bears}
```

- 清单 5. 使用构造函数
```
Append@{tigers bears}(lions)
{tigers bears lions}
 
Append@{lions}(tigers bears)
{lions tigers bears}
```

- 清单 6. 构建第二个元素、第三个元素，然后模拟 list 和 append
```
{1 2 3}[1] # 2
 
{1 2 3}[2] # 3
```

- 清单 7. 构建第二个函数
```
Wrap~lst@my_2nd( lst[1] )

my_2nd( {1 2.0 "3" 4 5} )  # 2.0
```

- 清单 8. 计算两个整数中的最大值
```
Wrap~x y@my_max (
    Case (
      {>(x y) x}
      {True   y} # all other cases
    )
)

my_max(2 5) # 5 
my_max(6 1) # 6
```

- 清单 9. 使用递归计算列表的总和
```
Wrap~x@total (
    Case(
      {IsNull(x) 0}
      {True  +(x[0] total(x[1:]))}
    )
)
 
total({1 5 1}) # 7
```

- 清单 10. Lambda 表达式 // 匿名函数
```
Wrap ~ p1 p2 @ _ (...)
```