# EEPROM.write()

## 说明

本示例演示如何通过EEPROM.write() 函数向EEPROM中写入信息。

## 示例程序

```c++
/*
 * EEPROM Write 示例程序
 * 
 * 储存于EEPROM的数值即使在断开Arduino开发板电源后仍会保存
 * 在EEPROM中。当我们将新程序上传Arduino开发板后，这些储存
 * 于EEPROM中的数值仍然可以被新的程序调用或者修改。
 * 
 * 本实例程序注释中文翻译：太极创客（WWW.TAICHI-MAKER.COM ）
 * 如需要获得EEPROM的使用中文说明以及Arduino开发板开发的更多资料和
 * 视频教程，请参见太极创客网站:
 * 
 * 2017-11-22
 * 
 */
 
#include <EEPROM.h>
 
/** 被写入数据的EEPROM地址编号 (即哪一个存储地址将要被写入数据) **/
int addr = 0;
 
void setup() {
  /** setup内无内容 **/
}
 
 
 
void loop() {
  /***
    如使用EEPROM存储模拟输入引脚所读取到的数值（即使用analogRead函数
    读取Arduino开发板的模拟输入引脚并且将读取到的数值存储于EEPROM），
    则需要将该数值除以4。原因是用analogRead函数所读取到的数值为0-1023
    而EEPROM只能储存0-255的数值。（EEPROM每一个存储地址可以储存一个字节，
    因此只能存储0-255的数值。）
  ***/
 
  int val = 123;  // 将要存储于EEPROM的整数数值
  
  /***
    将数值写入相应EEPROM地址。该数值即使在断开
    Arduino开发板电源后，仍将保持在开发板的EEPROM中不变。
  ***/
  EEPROM.write(addr, val);
 
  /***
 
    转入下一存储地址。当存储地址序列号达到EEPROM的存储空间结尾，
    返回到EEPROM开始地址。
    
    不同型号Arduino开发板具有不同大小的EEPROM存储空间，即:
    - Arduno Duemilanove: 512b EEPROM 存储空间.
    - Arduino Uno:        1kb EEPROM 存储空间 （允许使用的EEPROM地址序列号为 0-1023 ）.
    - Arduino Mega:       4kb EEPROM 存储空间.
  ***/
  addr = addr + 1;
  if (addr == EEPROM.length()) {
    addr = 0;
  }
 
  delay(10);
}
```

