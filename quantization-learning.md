# 模型量化学习

## 1.量化基本思路&原理

1.1浮点数转定点数

Step1：计算 [公式] ， F 表示小数的字长。
Step2：将 b 转换成最近的整数，例如 round(3.56) = 4，round(-1.9) = -2。
Step3： 将 b 用二进制表示成 c。
Step4：假定 c 用 n 位表示 b。w 表示最终的定点数的字长，f 表示最终的定点数的小数长度。w 应当不小于 n，最终的数最左边 （w-n）位补零，小数部分选取 c 的最低 f 位。

1.2定点数计算快
1.3定点数计算结果，转回浮点数

## 2.定点数、浮点数转化

2.1定点数转换浮点数的步骤
2.2浮点数转换定点数的步骤

2.3均量化
2.4非均量化

## 3.模型量化3种

3.1Post training Dynamic Quantization
3.2Post training Static Quantization
3.3QAT(Quantization Aware Training)
