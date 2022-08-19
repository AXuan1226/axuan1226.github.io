# EEPROM.update()

## 说明

EEPROM.update()与EEPROM.write()类似，可以用来向EEPROM写入数据。但是与EEPROM.write()不同的是，EEPROM.update()只会更新EEPROM中的数据。也就是说，只有在将要写入EEPROM的数据与EEPROM内现存的数据不同时，EEPROM.update()才会将这一数据写入EEPROM。

这么做有两个目的。首先是可以节约时间，提高程序运行速度。因为每一次Arduino在执行EEPROM的一个地址的数据写入时，都需要耗费3.3毫秒时间。其次是可以节省EEPROM使用寿命。EEPROM的擦写次数是有限的，这个次数大约是100,000次。当然您也不必过分担心这一点，假如您每天向EEPROM写入十次数据那么需要大约27年的时间才能将EEPROM寿命耗尽。同时也请留意，读取EEPROM是不会影响它的寿命的。

## 示例程序

本示例程序旨在演示如何使用EEPROM.update()函数更新EEPROM所存储的信息。

```c++
/*
 * EEPROM update
 *
 * 读取所有EEPROM储存数值并显示于计算机屏幕供用户查看。
 * 
 * 本实例程序注释中文翻译：太极创客（WWW.TAICHI-MAKER.COM ）
 * 如需要获得EEPROM的使用中文说明以及Arduino开发板开发的更多资料和
 * 视频教程，请参见太极创客网站:
 * 
 * WWW.TAICHI-MAKER.COM
 * 
 * 2017-11-22
 * 
 */
 
#include <EEPROM.h>
 
/** 被写入数据的EEPROM地址编号 (即.即哪一个存储地址将要被写入数据) **/
int address = 0;
 
void setup() {
  /** 无内容 **/
}
 
void loop() {
  /***
    如使用EEPROM存储模拟输入引脚所读取到的数值（即使用analogRead函数
    读取Arduino开发板的模拟输入引脚并且将读取到的数值存储于EEPROM），
    则需要将该数值除以4。原因是用analogRead函数所读取到的数值为0-1023
    而EEPROM只能储存0-255的数值。（EEPROM每一个存储地址可以储存一个字节，
    因此只能存储0-255的数值。）
  ***/
  int val = analogRead(0) / 4;
 
  /***
    将数值更新到相应EEPROM地址。该数值即使在断开
    Arduino开发板电源后，仍将保持在开发板的EEPROM中不变。
  ***/
  EEPROM.update(address, val);
 
  /***
     EEPROM.update(address, val)函数与以下代码功能相同:
 
    if( EEPROM.read(address) != val ){
      EEPROM.write(address, val);
    }
  ***/
 
 
  /***
  
    转入下一存储地址。当存储地址序列号达到EEPROM的存储空间结尾，
    返回到EEPROM开始地址。
      
    不同型号Arduino开发板具有不同大小的EEPROM存储空间，即:
    - Arduno Duemilanove: 512b EEPROM 存储空间.
    - Arduino Uno:        1kb EEPROM 存储空间 （允许使用的EEPROM地址序列号为 0-1023 ）.
    - Arduino Mega:       4kb EEPROM 存储空间.
  ***/
  address = address + 1;
  if (address == EEPROM.length()) {
    address = 0;
  }
 
  delay(100);
}
```

