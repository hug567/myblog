## 1、常见变量：

### 1.1、系统变量：

```C
$@											//目标文件
$^											//所有依赖文件
$<											//第一个依赖文件
```

### 1.2、make参数：

```c
-C dir, --directory=dir						//执行前先进入 dir 目录
```

### 1.3、赋值符号：

```c
=											//基本赋值
:=											//覆盖赋值
?=											//若未赋值则赋新值
+=											//添加赋值
```

## 2、常用函数

```c
$(wildcard *.c)								//获取当前目录下所有.c文件，空格分割
```
