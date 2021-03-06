# 模型量化学习

## 1.量化基本思路&原理

### 1.1浮点数直接相乘：
以两个16位的浮点数相乘为例，
2.918 * 3.1415926 = 9.1671672068

### 1.2浮点数--->定点数相乘--->浮点数
（1）将此浮点数定点化，定点要求为Qn=12（这里Qn=12表示小数位数占12bit），取符号位为1bit，则整数部分为3bit。

2.918 * 2^12 = 11952.168  定点化后取整为： 11952;
3.1415926 * 2^12 = 12867.8632896 定点化后取整为： 12868;
以上做舍入误差后取整数。

（2）定点数相乘

11952 * 12868 = 153798336.

（3）定点数还原为小数

153798336 / (2^24) = 9.167095184326171875
两个12bit的数相乘，结果为24bit，因此除以2^24可以还原原数据，由于存在舍入误差


### 1.3量化误差与量化精度

小数点量化误差的不同带来的量化误差不同。

以上定点转换的过程中对小数进行了四舍五入。2.918的小数部分转为二进制以后，无法用12bit完全表示。小数位数越多，量化精度越高。最大量化精度为 1/(2^n) .

### 1.4无损定点化

量化误差小于量化精度的一半，就可以认为是无损，在实际做题中，只要在转为定点数时，转换后的小数小于0.5就认为是无损量化。
```


## 2.定点数、浮点数转化

2.1定点数转换浮点数的步骤
```
Step1：计算 b=a*2^F， F 表示小数的字长。
Step2：将 b 转换成最近的整数，例如 round(3.56) = 4，round(-1.9) = -2。
Step3： 将 b 用二进制表示成 c。
Step4：假定 c 用 n 位表示 b。w 表示最终的定点数的字长，f 表示最终的定点数的小数长度。w 应当不小于 n，最终的数最左边 （w-n）位补零，小数部分选取 c 的最低 f 位。
```
2.2浮点数转换定点数的步骤
```
补充
```
2.3均量化
2.4非均量化

## 3.评估衡量量化优劣？

## 4.模型量化3种

3.1Post training Dynamic Quantization
3.2Post training Static Quantization
3.3QAT(Quantization Aware Training)


## reference
Quantizing deep convolutional networks for efficient inference: A whitepaper : https://arxiv.org/abs/1806.08342
A White Paper on Neural Network Quantization : https://arxiv.org/abs/2106.08295
