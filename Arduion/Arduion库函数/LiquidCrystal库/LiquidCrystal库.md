# LiquidCrystal库

- [LiquidCrystal库简介](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/#LiquidCrystal库简介)
- 硬件需求
  - [LCD1602液晶屏](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/#LCD1602液晶屏)
  - [技术参数](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/#技术参数)
  - [引脚说明](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/#引脚说明)
- Arduino控制LCD液晶屏
  - [电路连接](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/#Arduino控制LCD液晶屏电路)
  - [示例1 文字显示](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/#示例1文字显示)
  - [示例2 滚动显示](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/#示例2滚动显示)
  - [示例3 串口输入到LCD](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/#示例3串口输入到LCD)
  - [示例4 左右流动](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/#示例4左右流动)
- [LiquidCrystal库函数](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/#LiquidCrystal库函数)

## LiquidCrystal库简介

通过使用LiquidCrystal库，您可以使用Arduino开发板控制基于Hitachi HD44780芯片组或兼容LiquidCrystald库的液晶显示器（LCD），如1602液晶显示器。该库可以以4线或8线模式工作（即除了rs，enable和rw控制线之外还可以使用4或8条数据线连接运行）

## 硬件需求

LiquidCrystal库支持多款LCD屏幕模块。我们将以最常见的`LCD1602`作为示例讲解如何使用`LiquidCrystal`标准库LCD1602液晶屏

LCD1602液晶显示器是广泛使用的一种字符型液晶显示模块。它是由字符型液晶显示屏（LCD）、控制驱动主电路HD44780及其扩展驱动电路HD44100，以及少量电阻、电容元件和结构件等装配在PCB板上而组成。不同厂家生产的LCD1602芯片可能有所不同，但使用方法都是一样的。为了降低成本，绝大多数制造商都直接将裸片做到板子上。太极创客(www.taichi-maker.com)

<img src="http://www.taichi-maker.com/wp-content/uploads/2020/07/lcd1602%E5%9B%BE%E6%A0%B7.png">

### 技术参数

1. 显示容量：16×2个字符。
2. 芯片工作电压：4.5~5.5V。太极创客(www.taichi-maker.com)
3. 工作电流：2.0mA（5.0V）。
4. 模块最佳的工作电压：5.0V。太极创客(www.taichi-maker.com)
5. 字符尺寸：2.95mm×4.35mm（宽×高）

### 引脚说明

第1脚：VSS为地电源太极创客(www.taichi-maker.com)

第2脚：VDD接5V正电源

第3脚：V0为液晶显示器对比度调整端，接正电源时对比度最弱，接地电源时对比度最高，对比度过高时会产生“鬼影”，使用时可以通过一个10K的电位器调整对比度太极创客(www.taichi-maker.com)

第4脚：RS为寄存器选择，高电平时选择数据寄存器、低电平时选择指令寄存器。

第5脚：R/W为读写信号线，高电平时进行读操作，低电平时进行写操作。当RS和RW共同为低电平时可以写入指令或者显示地址，当RS为低电平RW为高电平时可以读忙信号，当RS为高电平RW为低电平时可以写入数据。

第6脚：E端为使能端，当E端由高电平跳变成低电平时，液晶模块执行命令。

第7～14脚：D0～D7为8位双向数据线。太极创客(www.taichi-maker.com)

第15脚：A背光电源正极

第16脚：K背光电源负极太极创客(www.taichi-maker.com)

## Arduino控制LCD液晶屏

为了方便大家搭建LCD调试环境, 以下示例程序均采用此电路连接的方法:

##### **电路连接**

<img src="http://www.taichi-maker.com/wp-content/uploads/2020/07/LCD602-UNO%E8%BF%9E%E7%BA%BF%E5%9B%BE-1024x387.png">

```
Arduino
* VSS GND
* VDD 5V
* V0  GND  (接正电源时对比度最弱，接地电源时对比度最高，可以通过一个10K的电位器调整对比度)
* RS  12
* RW  GND
* E   11
* D4  5
* D5  4
* D6  3
* D7  2
* A  5v
* K  GND

1
2
3
4
5
6
7
8
9
10
11
12
13
* VSS GND
* VDD 5V
* V0  GND  (接正电源时对比度最弱，接地电源时对比度最高，可以通过一个10K的电位器调整对比度)
* RS  12
* RW  GND
* E   11
* D4  5
* D5  4
* D6  3
* D7  2
* A  5v
* K  GND
```

### 示例1 文字显示

使用print函数在LCD屏幕打印字符串信息以及当前设备运行的时间(秒)

**示例程序**

```c++
/**********************************************************************
程序名称/Program name     : LiquidCrystal_demo_1
团队/Team                 : 太极创客团队 / Taichi-Maker (www.taichi-maker.com)
作者/Author               : Dapenson
日期/Date（YYYYMMDD）     : 2020/06/20
程序目的/Purpose          :  
演示如何使用LCD1602显示文字
-----------------------------------------------------------------------
修订历史/Revision History  
日期/Date    作者/Author      参考号/Ref    修订说明/Revision Description
-----------------------------------------------------------------------
***********************************************************************/
 
#include<LiquidCrystal.h>
 
// 创建lcd控制对象,并指定其引脚与Arduino控制板对应关系
const int rs=12,en=11,d4=5,d5=4,d6=3,d7=2;
LiquidCrystal lcd(rs,en,d4,d5,d6,d7);
 
void setup()
{
  lcd.begin(16,2);
  lcd.print("TaichiMaker!");
}
 
void loop() {
  // 设置光标位置在第0列,第1行
  // 注意,行和列都是从0开始的
  lcd.setCursor(0, 1);
  //打印自开发板重置以来的秒数：
  lcd.print(millis()/1000);
}
```

**效果演示**

<img sec="http://www.taichi-maker.com/wp-content/uploads/2020/07/LCD%E6%95%88%E6%9E%9C%E6%BC%94%E7%A4%BA%E6%98%BE%E7%A4%BA%E6%96%87%E5%AD%97.jpg">

### 示例2 滚动显示

本示例将告诉您如何使用`autoscroll()`和`noAutoscroll()`函数向左或向右滚动显示的所有字符。

每次添加字母时，通过调用`autoscroll()`函数会将所有文本向左移动一格

如果使用`noAutoscroll()`函数则会停止自动滚动

本示例在自动滚动关闭的条件下下打印字符0到9，然后将光标移到右下角，打开自动滚动，然后再次打印。

```c++
/**********************************************************************
程序名称/Program name     : LiquidCrystalAutoscroll
团队/Team                 : 太极创客团队 / Taichi-Maker (www.taichi-maker.com)
作者/Author               : Dapenson
日期/Date（YYYYMMDD）     : 2020/06/16
程序目的/Purpose          :  
本示例将告诉您如何使用`autoscroll()`和`noAutoscroll()`函数向左或向右
滚动显示的所有字符。
-----------------------------------------------------------------------
修订历史/Revision History  
日期/Date    作者/Author      参考号/Ref    修订说明/Revision Description
-----------------------------------------------------------------------
***********************************************************************/
 
#include <LiquidCrystal.h>
 
// 创建lcd控制对象,并指定其引脚与Arduino控制板对应关系
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);
 
void setup() {
  // lcd初始化,同时设置lcd屏幕的列数和行数(宽和高)
  lcd.begin(16, 2);
}
 
void loop() {
  // 设置光标在(0,0)位置处
  lcd.setCursor(0, 0);
  // 使用for循环打印数字0~9
  for (int thisChar = 0; thisChar < 10; thisChar++) {
    lcd.print(thisChar);
    delay(500);
  }
//<span style="color: #ffffff;">太极创客(www.taichi-maker.com)</span>
  // 设置光标处于(16,1)位置处
  lcd.setCursor(16, 1);
  // 设置lcd屏幕自动滚动
  lcd.autoscroll();
  // 打印数字0~9
  for (int thisChar = 0; thisChar < 10; thisChar++) {
    lcd.print(thisChar);
    delay(500);
  }
  // 关闭自动滚动功能
  lcd.noAutoscroll();
 
  // 清屏并继续下一个循环
  lcd.clear();
}
```

**效果演示**

<img src="http://www.taichi-maker.com/wp-content/uploads/2020/07/LCD%E6%95%88%E6%9E%9C%E6%BC%94%E7%A4%BA%E6%BB%9A%E5%8A%A8%E6%98%BE%E7%A4%BA.gif">

### 示例3 串口输入到LCD

本示例将向您演示如何将串口的数据实时显示到LCD屏幕中,在此过程中,您可以在烧录程序后通过串口监视器发送数据并在LCD屏幕进行查看

(电路连接见上)

您可以使用本示例进行LCD屏幕调试

```c++
/**********************************************************************
程序名称/Program name     : LiquidCrystalSerialDisplay
团队/Team                 : 太极创客团队 / Taichi-Maker (www.taichi-maker.com)
作者/Author               : Dapenson
日期/Date（YYYYMMDD）     : 2020/06/16
程序目的/Purpose          :  
本示例将向您演示如何将串口的数据实时显示到LCD屏幕中,
在此过程中,您可以在烧录程序后通过串口监视器发送数据并在LCD屏幕进行查看
-----------------------------------------------------------------------
修订历史/Revision History  
日期/Date    作者/Author      参考号/Ref    修订说明/Revision Description
-----------------------------------------------------------------------
***********************************************************************/
 
#include <LiquidCrystal.h>
 
// 创建lcd控制对象,并指定其引脚与Arduino控制板对应关系
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);
 
void setup()
{
  // lcd初始化,同时设置lcd屏幕的列数和行数(宽和高)
  lcd.begin(16, 2);
  // 初始化串口并设置波特率为9600
  Serial.begin(9600);
}
//<span style="color: #ffffff;">太极创客(www.taichi-maker.com)</span>
void loop()
{
  // 当串口收到数据时将数据写入到屏幕
  if (Serial.available())
  {
    // 延时100毫秒以等待消息接收完整
    delay(100);
    // 清屏
    lcd.clear();
    // 读取串口缓冲区所以数据
    while (Serial.available() > 0)
    {
      // 显示每一个字符到LCD显示屏
      lcd.write(Serial.read());
    }
  }
}
```

**效果演示**

当我们通过串口监视器输入`taichimaker test`并发送时, LCD屏幕就会显示我们键入的内容,注意,串口监视器参数应该选择`没有结束符`和波特率为`9600`

<img src="http://www.taichi-maker.com/wp-content/uploads/2020/07/image-20200702120425738.png">

### 示例4 左右流动

本示例演示如何使用`leftToRight()`和`rightToLeft()`函数。这些函数控制文本从LCD流出的方式。

`rightToLeft()` 使文本从光标向左流动，就像显示是右对齐的一样。

`leftToRight()` 使文本从光标向右流动，就像显示是左对齐的一样。

本示例将打印字符`'a'`通过`l`从右到左，然后`m`通过`r`左到右，然后`s`通过`z`从右到左再次运行。

(电路连接见上)

```c++
/**********************************************************************
程序名称/Program name     : LiquidCrystalTextDirection
团队/Team                 : 太极创客团队 / Taichi-Maker (www.taichi-maker.com)
作者/Author               : Dapenson
日期/Date（YYYYMMDD）     : 2020/06/16
程序目的/Purpose          :  
本示例将打印字符'a'通过`l`从右到左，然后`m`通过`r`左到右，然后`s`通过`z`从右到左再次运行。
-----------------------------------------------------------------------
修订历史/Revision History  
日期/Date    作者/Author      参考号/Ref    修订说明/Revision Description
-----------------------------------------------------------------------
***********************************************************************/
 
#include <LiquidCrystal.h>
 
// 创建lcd控制对象,并指定其引脚与Arduino控制板对应关系
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);
 
// 定义一个'a'变量
int thisChar = 'a';
 
void setup()
{
  // lcd初始化,同时设置lcd屏幕的列数和行数(宽和高)
  lcd.begin(16, 2);
  // 打开光标
  lcd.cursor();
}
 
void loop()
{
  //在'm'处转向
  if (thisChar == 'm')
  {
    // go right for the next letter
    lcd.rightToLeft();
  }
  // 在's'处再次反转
  if (thisChar == 's')
  {
    // 向左走到下一个字母
    lcd.leftToRight();
  }
  // 大于'z'则重置
  if (thisChar > 'z')
  {
    // 回到(0,0)位置:
    lcd.home();
    //再次从a开始
    thisChar = 'a';
  }
  // 打印字符
  lcd.write(thisChar);
  // 延时等待一秒
  delay(1000);
  // thisChar自增
  thisChar++;
}
 
 
```

<img src="http://www.taichi-maker.com/wp-content/uploads/2020/07/062DF777AB1A86AF893FF13EEDCC605F.gif">

## LiquidCrystal库函数

– [LiquidCrystal](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/arduino-liquidcrystal-liquidcrystal/)
– [begin](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/arduino-liquidcrystal-begin/)
– [clear](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/arduino-liquidcrystal-clear/)太极创客(www.taichi-maker.com)
– [home](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/arduino-liquidcrystal-home/)
– [setCursor](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/arduino-liquidcrystal-setcursor/)
– [write](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/arduino-liquidcrystal-write/)
– [print](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/arduino-liquidcrystal-print/)
– [cursor](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/arduino-liquidcrystal-cursor/)
– [noCursor](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/arduino-liquidcrystal-nocursor/)
– [blink](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/arduino-liquidcrystal-blink/)
– [noBlink](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/arduino-liquidcrystal-noblink/)
– [display](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/arduino-liquidcrystal-display/)
– [noDisplay](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/arduino-liquidcrystal-nodisplay/)
– [scrollDisplayLeft](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/arduino-liquidcrystal-scrolldisplayleft/)
– [scrollDisplayRight](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/arduino-liquidcrystal库-scrolldisplayright/)
– [autoscroll](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/arduino-liquidcrystal-autoscroll/)
– [noAutoscroll](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/arduino-liquidcrystal-noautoscroll/)
– [leftToRight](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/arduino-liquidcrystal-lefttoright/)
– [rightToLeft](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/arduino-liquidcrystal-righttoleft/)
– [createChar](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/arduino-liquidcrystal-createchar/)