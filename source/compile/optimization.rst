代码优化
========================================

简介
----------------------------------------
代码优化对程序实施各种等价变化，使得变换后程序能生成高效率的目标代码。好的编译器需要生成目标代码占用的存储空间少，且运行时间短。另外，编译器的编译时间、资源消耗也是需要考虑的指标。

优化方式
----------------------------------------
代码优化可以分为与机器有关的优化和与机器无关的优化。

机器无关的优化主要有下面几种方式：

- 局部优化
     - 合并已知量
     - 删除公共子表达式 （删除多余的运算）
     - 删除无用赋值
- 循环优化
     - 代码外提
     - 删除归纳变量
     - 强度削弱
- 全局优化
     - 在整个程序范围内进行优化，需要进行数据流分析，代价很高

优化原则
----------------------------------------
在当前，优化越来越重要，一个是因为现代处理器越来越复杂，有更多的机制来提供优化的机会。

另一个原因是多核并行越来越普遍，编译器需要适应，但是在硬件条件多变的情况下，很难知道一个解是不是最优解，那么就遵循以下的原则：

+ 优化必须保证正确
+ 优化要保证大部分程序都能提升表现
+ 优化带来的编译时间消耗需要是可以接受的
+ 工程量要能接受
