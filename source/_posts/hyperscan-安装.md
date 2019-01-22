title: hyperscan 安装
author: MiracleQi-温柔魔君
tags:
  - hyperscan
categories:
  - Linux
date: 2018-11-24 18:49:00
cover: /img/post-cover/53.jpg
---
# 1. 前言
本文在 Debian8 中安装 hyperscan 5.0.0  
内存至少 2 G，不然编译慢而且失败

# 2. 依赖
## 2.1 C/C++编译器
hyperscan使用C++开发，且需要C99和C++11支持，目前支持的编译器有

* GCC, v4.8.1 or higher
* Clang, v3.4 or higher (with libstdc++ or libc++)
* Intel C++ Compiler v15 or higher

## 2.2 第三方依赖库
```
    依赖项       版本         说明
    -------------------------------------------------
    CMake       >=2.8.11     
    Ragel       6.9  
    Python      2.7  
    Boost       >=1.57      仅需要头文件，无需编译
    Pcap        >=0.8       Optional: 仅用于示例程序
```

注1: Ragel 最好用 6.9 版本，7.0 版本可能会报错

```
wget -c http://www.colm.net/files/ragel/ragel-6.9.tar.gz
```

注2：boost不需要编译安装，如果通过系统包管理工具(yum/apt-get)安装的版本无法满足版本需要，只需要解压源码包

```
wget -c https://sourceforge.net/projects/boost/files/boost/1.68.0/boost_1_68_0.tar.gz/download
```
注3：pcap库会依赖flex和bison

# 3. 编译 hyperscan

```
ln -s /soft/boost_1_68_0/boost /soft/hyperscan-5.0.0/include/boost
cd /soft/hyperscan-5.0.0
mkdir build
cd build
cmake ../
cmake --build .  (别忘了最后有个点，编译时间较长)     
make install
```
hyperscan 还通过 cmake 支持一些编译选项，如 debug/release, static/shared 等，如  
* -DCMAKE_BUILD_TYPE=Release 编译为Release版本，不带调试信息，默认是RelWithDebInfo
* -DBUILD_SHARED_LIBS=on 编译为动态库，默认是静态库

等。

# 4. BUG
安装过程中，提示如下错误

```
hyperscan-5.0.0/src/nfa/limex_compile.cpp:983:54: error: call of overloaded ‘distance(std::vector<boost::dynamic_bitset<> >::iterator, __gnu_cxx::__normal_iterator<boost::dynamic_bitset<>, std::vector<boost::dynamic_bitset<> > >&)’ is ambiguous
return verify_u32(distance(squash.begin(), it));
^
```
可在 github 的 issues 中找到解决方案 https://github.com/intel/hyperscan/issues/104

作者给出的解释和解决方案如下：

![upload successful](/images/pasted-36.png)

只需将这两行的，distance 改为 std::distance 即可