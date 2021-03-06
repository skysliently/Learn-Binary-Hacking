语法分析
========================================

简介
----------------------------------------
语法分析以词法分析生成的单词符号序列作为输入，根据语法规则识别出语法成分。

分析方法
----------------------------------------

自上而下
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
自上而下的分析法从文法开始符号开始，正向推导。

自下而上
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
自下而上的分析法从给定的输入串开始，逐步归约。

语法
----------------------------------------

上下文无关语法
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
上下文无关语法（context-free grammar）有四个模块

+ 一组终结符（terminal symbols），有时候又叫token
+ 一组非终结符（nonterminal）syntactic variables.
+ 一组产生式（productions）
+ 一个非终结符作为起始符号

二义性文法
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
ambiguous grammars

错误处理
----------------------------------------
错误发生时，有一些可选的方法，最简单一种处理方式是 遇到第一个错误就退出，但是当错误很多的时候，最好能够容忍，并报出之后的错误。

Panic-Mode Recovery
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
当遇到错误的时候，就开始丢弃遇到的符号，直到遇到一个终结符，例如分号等。

Phrase-Level Recovery
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
这个方式是遇到错误的时候，替换一个能让当前parse执行下去的符号。

Error Productions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
把错误的产生式加到语法解析里面。

Global Corrections
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
还有一种做法是找到一个最近的能正常parse的源程序然后往下，但是这种做法太过消耗时间和空间资源，实际情况下使用的情况较少。
