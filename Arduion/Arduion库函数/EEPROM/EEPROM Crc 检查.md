# EEPROM Crc 检查

## 说明

CRC可用于检查EEPROM中的数据是否发生改变。每当我们改变EEPROM储存的信息内容，CRC也会随之发生变化。

CRC（[循环冗余检查](https://baike.baidu.com/item/循环冗余检查/10168241?fr=aladdin&fromid=11335030&fromtitle=Cyclic+Redundancy+Check)? Cyclical Redundancy Check）:
循环冗余检查（CRC）是一种数据传输检错功能，对数据进行多项式计算，并将得到的结果附在帧的后面，接收设备也执行类似的算法，以保证数据传输的正确性和完整性。

## 示例程序

```c++
/***
    EEPROM CRC 示例程序
    代码原作者：Christopher Andrews.
    CRC 算法生成：pycrc  MIT licence ( https://github.com/tpircher/pycrc ).
 
    CRC可用于检查数据是否发生改变或损坏。本实例程序用于计算EEPROM存储数据的CRC值。
    本示例程序的目的是为展示如何像数组一样使用EEPROM对象。
     
    本实例程序注释中文翻译：太极创客（WWW.TAICHI-MAKER.COM ）
    如需要获得EEPROM的使用中文说明以及Arduino开发板开发的更多资料和
    视频教程，请参见太极创客网站:  http://www.taichi-maker.com
 
***/
 
#include <Arduino.h>
#include <EEPROM.h>
 
void setup() {
 
  //Start serial
  Serial.begin(9600);
  while (!Serial) {
  }
 
  //输出进行CRC的数据长度
  Serial.print("EEPROM length: ");
  Serial.println(EEPROM.length());
 
  //输出调用 eeprom_crc() 函数的结果
  Serial.print("CRC32 of EEPROM data: 0x");
  Serial.println(eeprom_crc(), HEX);
  Serial.print("\n\nDone!");
}
 
void loop() {
  /* Empty loop */
}
 
unsigned long eeprom_crc(void) {
 
  const unsigned long crc_table[16] = {
    0x00000000, 0x1db71064, 0x3b6e20c8, 0x26d930ac,
    0x76dc4190, 0x6b6b51f4, 0x4db26158, 0x5005713c,
    0xedb88320, 0xf00f9344, 0xd6d6a3e8, 0xcb61b38c,
    0x9b64c2b0, 0x86d3d2d4, 0xa00ae278, 0xbdbdf21c
  };
 
  unsigned long crc = ~0L;
 
  for (int index = 0 ; index < EEPROM.length()  ; ++index) {
    crc = crc_table[(crc ^ EEPROM[index]) & 0x0f] ^ (crc >> 4);
    crc = crc_table[(crc ^ (EEPROM[index] >> 4)) & 0x0f] ^ (crc >> 4);
    crc = ~crc;
  }
  return crc;
}

```

