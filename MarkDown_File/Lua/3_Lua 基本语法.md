# 3_Lua 基本语法

## 第一个 Lua 程序

### 交互式编程

Lua 提供了交互式编程模式。我们可以在命令行中输入程序并立即查看效果。

Lua 交互式编程模式可以通过命令 lua -i 或 lua 来启用：

```lua
$ lua -i 
$ Lua 5.3.0  Copyright (C) 1994-2015 Lua.org, PUC-Rio
> 
```

在命令行中，输入以下命令:

```lua
> print("Hello World！")
```

接着我们按下回车键，输出结果如下：

```lua
> print("Hello World！")
Hello World！
>
```

### 脚本式编程

我们可以将 Lua 程序代码保存到一个以 lua 结尾的文件，并执行，该模式称为脚本式编程，如我们将如下代码存储在名为 hello.lua 的脚本文件中：

```lua
print("Hello World！")
print("www.runoob.com")
```

使用 lua 名执行以上脚本，输出结果为：

```lua
$ lua hello.lua
Hello World！
www.runoob.com
```

我们也可以将代码修改为如下形式来执行脚本（在开头添加：#!/usr/local/bin/lua）：

```lua
#!/usr/local/bin/lua

print("Hello World！")
print("www.runoob.com")
```

以上代码中，我们指定了 Lua 的解释器 /usr/local/bin directory。加上 # 号标记解释器会忽略它。接下来我们为脚本添加可执行权限，并执行：

```lua
./hello.lua 
Hello World！
www.runoob.com
```

## 注释

### 单行注释

`--`

### 多行注释

``

```
--[[
 多行注释
 多行注释
 --]]
```

## 标示符

Lua 标示符用于定义一个变量，函数获取其他用户定义的项。标示符以一个字母 A 到 Z 或 a 到 z 或下划线 **_** 开头后加上 0 个或多个字母，下划线，数字（0 到 9）。

最好不要使用下划线加大写字母的标示符，因为Lua的保留字也是这样的。

Lua 不允许使用特殊字符如 **@**, **$**, 和 **%** 来定义标示符。 Lua 是一个区分大小写的编程语言。因此在 Lua 中 Runoob 与 runoob 是两个不同的标示符。以下列出了一些正确的标示符：

<img src="data:image/png;base64,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" >

## 关键词

以下列出了 Lua 的保留关键词。保留关键字不能作为常量或变量或其他用户自定义标示符：

| and      | break | do    | else   |
| -------- | ----- | ----- | ------ |
| elseif   | end   | false | for    |
| function | if    | in    | local  |
| nil      | not   | or    | repeat |
| return   | then  | true  | until  |
| while    | goto  |       |        |

一般约定，以下划线开头连接一串大写字母的名字（比如 _VERSION）被保留用于 Lua 内部全局变量。

## 全局变量

在默认情况下，变量总是认为是全局的。

全局变量不需要声明，给一个变量赋值后即创建了这个全局变量，访问一个没有初始化的全局变量也不会出错，只不过得到的结果是：nil。

```lua
> print(b)
nil
> b=10
> print(b)
10
>
```

如果你想删除一个全局变量，只需要将变量赋值为nil。

```lua
b = nil
print(b)      --> nil
```

这样变量b就好像从没被使用过一样。换句话说, 当且仅当一个变量不等于nil时，这个变量即存在。