# 4_Lua 数据类型

Lua 是动态类型语言，变量不要类型定义,只需要为变量赋值。 值可以存储在变量中，作为参数传递或结果返回。

Lua 中有 8 个基本类型分别为：nil、boolean、number、string、userdata、function、thread 和 table。

| **数据类型** | **描述**                                                     |
| ------------ | ------------------------------------------------------------ |
| nil          | 这个最简单，只有值nil属于该类，表示一个无效值（在条件表达式中相当于false）。 |
| boolean      | 包含两个值：false和true。                                    |
| number       | 表示双精度类型的实浮点数                                     |
| string       | 字符串由一对双引号或单引号来表示                             |
| function     | 由 C 或 Lua 编写的函数                                       |
| userdata     | 表示任意存储在变量中的C数据结构                              |
| thread       | 表示执行的独立线路，用于执行协同程序                         |
| table        | Lua 中的表（table）其实是一个"关联数组"（associative arrays），数组的索引可以是数字、字符串或表类型。在 Lua 里，table 的创建是通过"构造表达式"来完成，最简单构造表达式是{}，用来创建一个空表。 |

我们可以使用 type 函数测试给定变量或者值的类型：

```lua
print(type("Hello world"))      --> string
print(type(10.4*3))             --> number
print(type(print))              --> function
print(type(type))               --> function
print(type(true))               --> boolean
print(type(nil))                --> nil
print(type(type(X)))            --> string
```

## nil（空）

nil 类型表示一种没有任何有效值，它只有一个值 -- nil，例如打印一个没有赋值的变量，便会输出一个 nil 值：

```lua
> print(type(a))
nil
>
```

对于全局变量和 table，nil 还有一个"删除"作用，给全局变量或者 table 表里的变量赋一个 nil 值，等同于把它们删掉，执行下面代码就知：

```lua
tab1 = { key1 = "val1", key2 = "val2", "val3" }
for k, v in pairs(tab1) do
    print(k .. " - " .. v)
end
 
tab1.key1 = nil
for k, v in pairs(tab1) do
    print(k .. " - " .. v)
end
```

### nil 作比较时应该加上双引号 **"**：

```lua
> type(X)
nil
> type(X)==nil
false
> type(X)=="nil"
true
>
```

**type(X)==nil** 结果为 **false** 的原因是 type(X) 实质是返回的 **"nil"** 字符串，是一个 string 类型：

```lua
type(type(X))==string
```

## boolean（布尔）

boolean 类型只有两个可选值：true（真） 和 false（假），Lua 把 false 和 nil 看作是 false，其他的都为 true，数字 0 也是 true:

```lua
print(type(true))
print(type(false))
print(type(nil))
 
if false or nil then
    print("至少有一个是 true")
else
    print("false 和 nil 都为 false")
end

if 0 then
    print("数字 0 是 true")
else
    print("数字 0 为 false")
end
```

以上代码执行结果如下：

![image-20220725145530317](C:\Users\陈小贵儿\AppData\Roaming\Typora\typora-user-images\image-20220725145530317.png)

## number（数字）

Lua 默认只有一种 number 类型 -- double（双精度）类型（默认类型可以修改 luaconf.h 里的定义），以下几种写法都被看作是 number 类型：

```lua
print(type(2))
print(type(2.2))
print(type(0.2))
print(type(2e+1))
print(type(0.2e-1))
print(type(7.8263692594256e-06))
```

以上代码执行结果：

```lua
number
number
number
number
number
number
```

## string（字符串）

字符串由一对双引号或单引号来表示。

```lua
string1 = "this is string1"
string2 = 'this is string2'
```

也可以用 2 个方括号 "[[]]" 来表示"一块"字符串。

```lua
html = [[
<html>
<head></head>
<body>
    <a href="http://www.runoob.com/">菜鸟教程</a>
</body>
</html>
]]
print(html)
```

以下代码执行结果为：

<img src="data:image/png;base64,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">

在对一个数字字符串上进行算术操作时，Lua 会尝试将这个数字字符串转成一个数字:

```lua
> print("2" + 6)
8.0
> print("2" + "6")
8.0
> print("2 + 6")
2 + 6
> print("-2e2" * "6")
-1200.0
> print("error" + 1)
stdin:1: attempt to perform arithmetic on a string value
stack traceback:
        stdin:1: in main chunk
        [C]: in ?
>
```

以上代码中"error" + 1执行报错了，字符串连接使用的是 **.. **，如：

```lua
> print("a" .. 'b')
ab
> print(157 .. 428)
157428
> 
```

使用 # 来计算字符串的长度，放在字符串前面，如下实例：

```lua
> len = "www.runoob.com"
> print(#len)
14
> print(#"www.runoob.com")
14
>
```

## table（表）

在 Lua 里，table 的创建是通过"构造表达式"来完成，最简单构造表达式是{}，用来创建一个空表。也可以在表里添加一些数据，直接初始化表:

```lua
-- 创建一个空的 table
local tbl1 = {}
 
-- 直接初始表
local tbl2 = {"apple", "pear", "orange", "grape"}
```

Lua 中的表（table）其实是一个"关联数组"（associative arrays），数组的索引可以是数字或者是字符串。

```lua
-- table_test.lua 脚本文件
a = {}
a["key"] = "value"
key = 10
a[key] = 22
a[key] = a[key] + 11
for k, v in pairs(a) do
    print(k .. " : " .. v)
end
```

脚本执行结果为：

```lua
$ lua table_test.lua 
key : value
10 : 33
```

不同于其他语言的数组把 0 作为数组的初始索引，在 Lua 里表的默认初始索引一般以 1 开始。

```lua
-- table_test2.lua 脚本文件
local tbl = {"apple", "pear", "orange", "grape"}
for key, val in pairs(tbl) do
    print("Key", key)
end
```

脚本执行结果为：

```lua
$ lua table_test2.lua 
Key    1
Key    2
Key    3
Key    4
```

table 不会固定长度大小，有新数据添加时 table 长度会自动增长，没初始的 table 都是 nil。

```lua
-- table_test3.lua 脚本文件
a3 = {}
for i = 1, 10 do
    a3[i] = i
end
a3["key"] = "val"
print(a3["key"])
print(a3["none"])
```

脚本执行结果为：

```
$ lua table_test3.lua 
val
nil
```

## function（函数）

在 Lua 中，函数是被看作是"第一类值（First-Class Value）"，函数可以存在变量里:

```lua
-- function_test.lua 脚本文件
function factorial1(n)
    if n == 0 then
        return 1
    else
        return n * factorial1(n - 1)
    end
end
print(factorial1(5))
factorial2 = factorial1
print(factorial2(5))
```

脚本执行结果为：

```lua
$ lua function_test.lua 
120
120
```

function 可以以匿名函数（anonymous function）的方式通过参数传递:

```lua
-- function_test2.lua 脚本文件
function testFun(tab,fun)
        for k ,v in pairs(tab) do
                print(fun(k,v));
        end
end


tab={key1="val1",key2="val2"};
testFun(tab,
function(key,val)--匿名函数
        return key.."="..val;
end
);
```

脚本执行结果为：

```lua
$ lua function_test2.lua 
key1 = val1
key2 = val2
```



## thread（线程）

在 Lua 里，最主要的线程是协同程序（coroutine）。它跟线程（thread）差不多，拥有自己独立的栈、局部变量和指令指针，可以跟其他协同程序共享全局变量和其他大部分东西。

线程跟协程的区别：线程可以同时多个运行，而协程任意时刻只能运行一个，并且处于运行状态的协程只有被挂起（suspend）时才会暂停。

## userdata（自定义类型）

userdata 是一种用户自定义数据，用于表示一种由应用程序或 C/C++ 语言库所创建的类型，可以将任意 C/C++ 的任意数据类型的数据（通常是 struct 和 指针）存储到 Lua 变量中调用。