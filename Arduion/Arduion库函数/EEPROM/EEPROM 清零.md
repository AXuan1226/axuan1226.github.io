# EEPROM 清零

## 说明

本示例演示如何通过EEPROM.write() 函数将所有EEPROM的存储信息清零

## 示例程序

```c++
/*
 * EEPROM 清零
 *
 * 本示例演示如何通过EEPROM.write() 函数将所有EEPROM的存储信息清零
 * 
 * 本实例程序注释中文翻译：太极创客（WWW.TAICHI-MAKER.COM ）
 * 如需要获得EEPROM的使用中文说明以及Arduino开发板开发的更多资料和
 * 视频教程，请参见太极创客网站:
 * 
 * WWW.TAICHI-MAKER.COM
 * 
 * 2018-01-12
 * 
 */
#include <EEPROM.h>
 
void setup() {
  // 设置内置LED引脚为输出模式
  pinMode(LED_BUILTIN, OUTPUT);
   
  /***
      转入下一存储单元。当存储序列号达到EEPROM的结尾，
      返回到EEPROM开始。
       
      不同型号Arduino开发板具有不同大小的EEPROM存储空间，即:
      - Arduno Duemilanove: 512b EEPROM 存储空间.
      - Arduino Uno:        1kb EEPROM 存储空间 （允许使用的EEPROM地址序列号为 0-1023 ）.
      - Arduino Mega:       4kb EEPROM 存储空间.
    ***/
 
  for (int i = 0 ; i < EEPROM.length() ; i++) {
    EEPROM.write(i, 0);
  }
 
  // EEPROM清零完成后点亮内置LED
  digitalWrite(LED_BUILTIN, HIGH);
}
 
void loop() {
  /** 无内容. **/
}

```

