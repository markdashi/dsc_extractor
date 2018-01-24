# 从动态共享(dyld shared cache)缓存中抽取动态库

**在iOS/os** 系统中程序编译以后我们都可以找到对应路径下的可执行（executable）文件，然而我们在查找系统动态类似于 `UIKit` `MapKit` `AVKit` `CFNetwork` 等一些系统库的可执行文件时候到其默认输出路径`/System/Library/Frameworks/UIKit.framework`中无法找到对应的executable文件，这是由于苹果官方为了提高性能，不再将动态库单独存放，而是将绝大多数系统动态库都打包存放在一个缓存文件中(dyld shared cache)，默认缓存路径为`/System/Library/Cache/com.app.dyld`,在这个文件夹下，我们可以在下图看到两种架构的动态库缓存文件

<img src="https://github.com/markdashi/dsc_extractor/blob/master/images/1.png" width="400" height="592">

这个动态共享库中就包含着我们常用的调用系统库，类似`UIKit`等常用系统库，我们需要做的就是将这个库中的动态库一个个抽取出来，抽取后，我们会得到以下系统库文件

<img src="https://github.com/markdashi/dsc_extractor/blob/master/images/2.png" width="400" height="744">

这样我们就可以单独拿到一个系统动态 (dynamically linked shared library)库的,这样我们就可以去分析单一的库了。

# How To Use 如何使用

```
cd dsc_extractor // cd到dsc_extractor文件夹下
./dsc_extractor  xx  oo // xx 是指待抽取的共享缓存库文件名  oo 是指待输出的文件夹

```
或者你输入 ./dsc_extractor 会打印出你需要拼接的参数
```
usage: dsc_extractor <path-to-cache-file> <path-to-device-dir>
```

上述文件如果需要在不指定路径下执行，可以 `cp dsc_extractor /usr/bin or /usr/local/bin  `

如果上述方法不好使，可以编辑 .bash_profile 指定路径export $PATH。


# Installation
```
git clone https://github.com/markdashi/dsc_extractor.git

```


### License

> Copyright (c) 2017 俊斐 王

> Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

> The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE. 


