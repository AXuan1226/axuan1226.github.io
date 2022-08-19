# EEPROM.read()

## 说明

本示例演示如何通过EEPROM.read() 函数将EEPROM中存储的信息读取并且显示出来。

## 示例程序

```c++
/*
 * EEPROM Read
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
 
//从EEPROM的第一个字节（地址序号0）开始读取
int address = 0;
byte value;
 
void setup() {
  //初始化串口通讯并等待初始化完成
  Serial.begin(9600);
  while (!Serial) {
    ; // 等待初始化串口通讯初始化完成
  }
}
 
void loop() {
  //从当前EEPROM存储地址中读取数据
  value = EEPROM.read(address);
 
  Serial.print(address);
  Serial.print("\t");
  Serial.print(value, DEC);
  Serial.println();
 
  /***
    转入下一存储单元。当存储序列号达到EEPROM的结尾，
    返回到EEPROM开始。
     
    不同型号Arduino开发板具有不同大小的EEPROM存储空间，即:
    - Arduno Duemilanove: 512b EEPROM 存储空间.
    - Arduino Uno:        1kb EEPROM 存储空间 （允许使用的EEPROM地址序列号为 0-1023 ）.
    - Arduino Mega:       4kb EEPROM 存储空间.
  ***/
  address = address + 1;
  if (address == EEPROM.length()) {
    address = 0;
  }
 
  delay(500);
}

```

