# 01.ASP.NET MVC 教程

MVC 是三种 ASP.NET 编程模式中的一种。

MVC 是一种使用 MVC（Model View Controller 模型-视图-控制器）设计创建 Web 应用程序的模式：

- Model（模型）表示应用程序核心（比如数据库记录列表）。
- View（视图）显示数据（数据库记录）。
- Controller（控制器）处理输入（写入数据库记录）。

MVC 模式同时提供了对 HTML、CSS 和 JavaScript 的完全控制。

<img src="\MVC\img\01.jpg">

**Model（模型）**是应用程序中用于处理应用程序数据逻辑的部分。
通常模型对象负责在数据库中存取数据。

**View（视图）**是应用程序中处理数据显示的部分。
通常视图是依据模型数据创建的。

**Controller（控制器）**是应用程序中处理用户交互的部分。
通常控制器负责从视图读取数据，控制用户输入，并向模型发送数据。

MVC 分层有助于管理复杂的应用程序，因为您可以在一个时间内专门关注一个方面。例如，您可以在不依赖业务逻辑的情况下专注于视图设计。同时也让应用程序的测试更加容易。

MVC 分层同时也简化了分组开发。不同的开发人员可同时开发视图、控制器逻辑和业务逻辑。

## Web Forms 对比 MVC

MVC 编程模式是对传统 ASP.NET（Web Forms）的一种轻量级的替代方案。它是轻量级的、可测试性高的框架，同时整合了所有已有的 ASP.NET 特性，比如母版页、安全性和认证。

## Visual Studio Express 2012/2010

Visual Studio Express 是 Microsoft Visual Studio 的免费版本。

Visual Studio Express 是为 MVC（和 Web Forms）量身定制的开发工具。

Visual Studio Express 包含：

- MVC 和 Web Forms
- 拖拽 Web 控件和 Web 组件
- Web 服务器语言（Razor 使用 VB 或者 C#）
- Web 服务器（IIS Express）
- 数据库服务器（SQL Server Compact）
- 完整的 Web 开发框架（ASP.NET）

如果您已经安装了 Visual Studio Express，您将从本教程中学到更多。

如果您想安装 Visual Studio Express，请点击下列链接中的一个：

[Visual Web Developer 2012](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=VWDOrVs11AzurePack)（Windows 7 或者 Windows 8）

[Visual Web Developer 2010](http://www.microsoft.com/web/gallery/install.aspx?appid=VWDorVS2010SP1Pack)（Windows Vista 或者 XP）



| ![lamp](https://www.runoob.com/images/lamp.jpg) | 在您首次安装完 Visual Studio Express 之后，您可以通过再次运行安装程序来安装补丁和服务包，只需要再次点击链接即可。 |
| ----------------------------------------------- | ------------------------------------------------------------ |



------

## ASP.NET MVC 参考手册

在本教程的最后，我们提供了完整的 ASP.NET MVC 参考手册供您查阅。