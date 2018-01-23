# 从动态共享(dyld shared cache)缓存中抽取动态库

**在iOS/os** 系统中程序编译以后我们都可以找到对应路径下的可执行（executable）文件，然而我们在查找系统动态类似于 `UIKit` `MapKit` `AVKit` `CFNetwork` 等一些系统库的可执行文件时候到其默认输出路径`/System/Library/Frameworks/UIKit.framework`中无法找到对应的executable文件，这是由于苹果官方为了提高性能，不再将动态库单独存放，而是将绝大多数系统动态库都打包存放在一个缓存文件中(dyld shared cache)，默认缓存路径为`/System/Library/Cache/com.app.dyld`,在这个文件夹下，我们可以在下图看到两种架构的动态库缓存文件

<img src="https://github.com/markdashi/dsc_extractor/blob/master/images/1.png" width="400" height="592" align="center">

这个动态共享库中就包含着我们常用的调用系统库，类似`UIKit`等常用系统库，我们需要做的就是将这个库中的动态库一个个抽取出来，抽取后，我们会得到以下系统库文件

<img src="https://github.com/markdashi/dsc_extractor/blob/master/images/2.png" width="400" height="744" align="center">

这样我们就可以单独拿到一个系统动态 (dynamically linked shared library)库的,这样我们就可以去分析单一的库了。
