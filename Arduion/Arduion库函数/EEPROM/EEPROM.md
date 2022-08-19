

# 1.[EEPROM](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/) 

> 读写开发板内置EEPROM，“永久”保存数据。

<iframe src="//player.bilibili.com/player.html?aid=18314857&bvid=BV1tW411q7Hn&cid=29896859&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>

## EEPROM库简介

[Arduino开发板](http://www.taichi-maker.com/homepage/reference-index/arduino-hardware-refrence/)上的微控制器带有EEPROM（电可擦除可编程只读存储器）。存储于EEPROM中的信息不会因为Arduino断电而丢失（这就好像 一个小U盘一样）。通过EEPROM，我们可以存储需要长久保存的变量数值或其它数据信息。EEPROM库可以让用户轻松的读取和写入Arduino开发板的EEPROM。

对于不同的Arduino 开发板微控制器，他们的EEPROM大小是不同的。[ Arduino Uno](http://www.taichi-maker.com/homepage/reference-index/arduino-hardware-refrence/arduino-uno/) 以及 [Arduino Nano](http://www.taichi-maker.com/homepage/reference-index/arduino-hardware-refrence/arduino-nano/) 开发板的 EEPROM大小是1 KB (1024字节) 。而[Arduino Mega](http://www.taichi-maker.com/homepage/reference-index/arduino-hardware-refrence/arduino-mega/)开发板的 EEPROM大小是 4 KB (4096 字节)。

## EEPROM库读写操作

EEPROM的主要操作为读取和写入。对于最基本的读写操作，可以通过[EEPROM.read()](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/eeprom-read/)以及[EEPROM.write()](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/eeprom-write/)来完成。但是这两个函数具有局限性，EEPROM的 每一个地址可以存储的信息为1字节。这就限制了EEPROM的 每一个地址内所能单独存储的整数数值为0~255区间。由于EEPROM.read()以及EEPROM.write()每一次只能读或写一个字节的数据, 假如我们需要存储超出0~255范围的[整数](http://www.taichi-maker.com/homepage/reference-index/arduino-code-reference/int/)数值或者带有小数点的[浮点数](http://www.taichi-maker.com/homepage/reference-index/arduino-code-reference/float/)，就需要用多个EEPROM协作存储来完成。好在Arduino库还配有[EEPROM.put()](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/eeprom-put/)和[EEPROM.get()](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/eeprom-get/)这两个函数。利用这两个函数您可以轻松地完成以下操作：

- [向 EEPROM 存储浮点型数据](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/eeprom-put/#code)
- [从 EEPROM 读取浮点型数据](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/eeprom-get/#code)
- [向 EEPROM 存储整数型数据](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/eeprom-put/#code2)
- [从 EEPROM 读取整数型数据](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/eeprom-get/#code2)

## EEPROM库函数

| – [EEPROM 清零](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/eeprom-clear/)：EEPROM信息清零 |
| ------------------------------------------------------------ |
| – [EEPROM.read()](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/eeprom-read/)：读取EEPROM中存储的信息 |
| – [EEPROM.write()](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/eeprom-write/):向EEPROM中写入信息 |
| – [EEPROM CRC检查](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/eeprom-crc/):计算CRC 信息以判定EEPROM储存内容是否被更改 |
| – [EEPROM.put()](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/eeprom-put/): 向EEPROM储存数据 |
| – [EEPROM.get()](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/eeprom-get/):获取EEPROM储存的数据 |
| – [EEPROM.update()](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/eeprom-library/eeprom-update/): 更新EEPROM存储内容。 |