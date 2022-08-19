# EEPROM.put()

## 说明

EEPROM.write()函数每次只能写入一个字节的数据到EEPROM。而大部分数据类型占用的字节数量都是超过1个字节的。如浮点型数据，整形数据等。

EEPROM.put()函数允许我们向EEPROM写入多字节的数据。这就允许我们向EEPROM[存储带有小数点的浮点型数据](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/eeprom-put/#code)或[存储EEPROM整数型数据](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/eeprom-put/#code2)以及其它数据类型。

## 语法

EEPROM.put(address, var)

## 参数

address: 存储信息的EEPROM地址值
var: 被存储的变量

## 示例程序1 – 存储浮点型数据到EEPROM

此示例程序旨在演示如何利用eeprom_put()函数向EEPROM存储带有小数点的浮点型数据。

假如您想要[存储的数据是整数型数据](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/eeprom-put/#code2)，那么您只需要把此示例程序的浮点型变量更换为整数型变量就可以了。Arduino IDE会根据您所需要存储的数据类型自动做出相应调整的。

**注意**：此示例程序需要与[eeprom_get_float示例程序](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/eeprom-get/#code)配合使用，从而确定此示例程序中的浮点数据确实写入了EEPROM中。eeprom_get_float示例程序的作用是从EEPROM读取此示例程序所写入EEPROM的浮点数并将其显示于串行监视器中。以供用户查验。

```c++
/*
 * eeprom_put_float
 * 太极创客（WWW.TAICHI-MAKER.COM ）
 * 
 * 此示例程序旨在演示如何利用eeprom_put()函数
 * 向EEPROM存储带有小数点的浮点型数据。
 * 
 * 如需要获得EEPROM的使用中文说明以及Arduino开发板开发的更多资料和
 * 视频教程，请参见太极创客网站:
 * 
 * WWW.TAICHI-MAKER.COM
 */
 
#include <EEPROM.h>
 
void setup() {
 
  Serial.begin(9600);
 
  float floatVar1 = 123.456;         // 将要存储入EEPROM的浮点型数据1
  float floatVar2 = 234.567;         // 将要存储入EEPROM的浮点型数据2
  
  int fVar1Addr = 0;                  // 存储floatVar1的EEPROM地址
  int fVar2Addr = 4;                  // 存储floatVar2的EEPROM地址
 
  /*
   * 每一个浮点型变量所占的内存大小是4个字节
   * 假如我们选择EEPROM地址序号0来存储floatVar1变量。
   * 那么实际上Arduino将会用EEPROM地址序号为0-3这4个存储单元
   * 来存储floatVar1。
   * 
   * 因此存储第二个浮点型变量floatVar2的EEPROM地址序号就要从
   * 序号4或者4以后的序号选。这也就是为什么我们将fVar2Addr的数值设置为4。
  */
 
  EEPROM.put(fVar1Addr, floatVar1);  // 将floatVar1存入EEPROM地址1
  delay(10);
  EEPROM.put(fVar2Addr, floatVar2);  // 将floatVar2存入EEPROM地址2
  delay(10);   
/*
 * 此示例程序需要与eeprom_get_float示例程序配合使用，
 * 从而确定此示例程序中的浮点数据确实写入了EEPROM中。
 * 
 * eeprom_get_float示例程序的作用是从EEPROM读取此示例程序
 * 所写入EEPROM的浮点数并将其显示于串行监视器中。以供用户查验。
*/
 
  Serial.println("Finished writing float data!");
}
 
void loop() {
  /* 无内容 */
}
```

## 示例程序2 – 存储整数型数据到EEPROM

```c++
/*
 * eeprom_put_int
 * 太极创客（WWW.TAICHI-MAKER.COM ）
 * 
 * 此示例程序旨在演示如何利用eeprom_put()函数
 * 向EEPROM存储整数型数据。
 * 
 * 此示例程序需要与eeprom_get_int示例程序配合使用，
 * 从而确定此示例程序中的整数数据确实写入了EEPROM中。
 * 
 * eeprom_get_int示例程序的作用是从EEPROM读取此示例程序
 * 所写入EEPROM的整数数并将其显示于串行监视器中。以供用户查验。
 * 
 * 
 * 如需要获得EEPROM的使用中文说明以及Arduino开发板开发的更多资料和
 * 视频教程，请参见太极创客网站:
 * 
 * WWW.TAICHI-MAKER.COM
 */
 
#include <EEPROM.h>
 
void setup() {
 
  Serial.begin(9600);
 
  int i = 9999;               // 将要存储入EEPROM的整数型数据
  int address = 1;            // EEPROM存储地址
 
  EEPROM.put(address, i);    // 将整数型变量i存入EEPROM
  
/*
 * 此示例程序需要与eeprom_get_int示例程序配合使用，
 * 从而确定此示例程序中的整数数据确实写入了EEPROM中。
 * 
 * eeprom_get_int示例程序的作用是从EEPROM读取此示例程序
 * 所写入EEPROM的整数数并将其显示于串行监视器中。以供用户查验。
*/
 
  Serial.println("Finished writing int data type!");
}
 
void loop() {
  /* Empty loop */
}
```

