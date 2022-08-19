# EEPROM.get()

## 说明

EEPROM.read()函数每次只能读取一个字节的数据。而大部分数据类型占用的字节数量都是超过1个字节的，如[浮点型](http://www.taichi-maker.com/homepage/reference-index/arduino-code-reference/float/)数据，[整形](http://www.taichi-maker.com/homepage/reference-index/arduino-code-reference/int/)数据等。

EEPROM.get()函数允许用户一次获取多个字节的数据。这就允许我们向EEPROM存储带有小数点的浮点型数据或整数型数据以及其它数据类型。

## 语法

EEPROM.get(address, var)

## 参数

address: 读取信息的EEPROM地址值
var: 此变量用于存储读取到的EEPROM数据

## 示例程序1 – 从EEPROM中读取浮点型数据

此示例程序旨在演示如何利用eeprom_get()函数向EEPROM读取带有小数点的浮点型数据。

假如您想要[读取的数据是整数型变量](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/eeprom-get/#code2)，那么您只需要把此示例程序的浮点型变量更换为整数型变量就可以了。Arduino IDE会根据您所需要读取的数据类型自动做出相应调整的。

**注意**：此示例程序需要与[eeprom_put_float示例程序](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/eeprom-put/#code)配合使用。在运行本示例程序前请先运行eeprom_put_float示例程序，从而确保EEPROM中已经写入可以获取的浮点型数据了。如果没有进行以上操作，此示例程序仍然可以运行，但是输出信息可能是毫无意义的乱码。

```c++
/*
 * eeprom_get_float 示例
 * 太极创客（WWW.TAICHI-MAKER.COM ）
 * 
 * 此示例程序旨在演示如何利用eeprom_get()函数
 * 向EEPROM读取带有小数点的浮点型数据。
 * 
 * 如需要获得EEPROM的使用中文说明以及Arduino开发板开发的更多资料和
 * 视频教程，请参见太极创客网站:
 * WWW.TAICHI-MAKER.COM
 * 2018-01-12    
*/
  
#include <EEPROM.h>
  
void setup() {
  
  float floatVar1;   //此变量用于存储获取到的EEPROM浮点型数据1
  float floatVar2;   //此变量用于存储获取到的EEPROM浮点型数据2
  
  int fVar1Addr = 0;                  // 存储floatVar1的EEPROM地址
  int fVar2Addr = 4;                  // 存储floatVar2的EEPROM地址
  
  Serial.begin(9600);
  
  Serial.println("Get float from EEPROM: ");
  
  //从EEPROM获取浮点型数据
  EEPROM.get(fVar1Addr, floatVar1);
  delay(10);
  EEPROM.get(fVar2Addr, floatVar2);
  delay(10);
  /*
   * 此示例程序需要与eeprom_put_float示例程序配合使用。
   * 在运行本示例程序前，请先运行eeprom_put_float示例程序，
   * 从而确保EEPROM中已经写入可以获取的浮点型数据了。
   * 如果没有进行以上操作，此示例程序仍然可以运行，但是输出信息
   * 可能是毫无意义的乱码。  
   */
   
  Serial.print("floatVar1 = ");   
  Serial.println(floatVar1, 3);  
  Serial.print("floatVar2 = ");     
  Serial.println(floatVar2, 3);  
 
}
  
void loop() {
  /* Empty loop */
}
```

## 示例程序2 – 从EEPROM中读取整数型数据

```c++
/*
 * eeprom_get_int 示例
 * 太极创客（WWW.TAICHI-MAKER.COM ）
 * 
 * 此示例程序旨在演示如何利用eeprom_get()函数
 * 向EEPROM读取整数型数据。
 * 
 * 如需要获得EEPROM的使用中文说明以及Arduino开发板开发的更多资料和
 * 视频教程，请参见太极创客网站:
 * WWW.TAICHI-MAKER.COM
 * 2018-01-12    
*/
  
#include <EEPROM.h>
  
void setup() {
  
  int i;             //此变量用于存储获取到的EEPROM整数型数据
  int eeAddress = 1; //起始获取信息的EEPROM地址
  
  Serial.begin(9600);
  
  Serial.print("Get int from EEPROM: ");
  
  //从'eeAddress'地址获取整数型数据
  EEPROM.get(eeAddress, i);
  Serial.println(i);    
/*
 * 此示例程序需要与eeprom_put_int示例程序配合使用。
 * 在运行本示例程序前，请先运行eeprom_put_int示例程序，
 * 从而确保EEPROM中已经写入可以获取的整数型数据了。
 * 如果没有进行以上操作，此示例程序仍然可以运行，但是输出信息
 * 可能是毫无意义的乱码。  
 */
}
  
void loop() {
  /* Empty loop */
}
```

