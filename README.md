# 从动态共享(dyld shared cache)缓存中抽取动态库

在iOS/os 系统中程序编译以后我们都可以找到对应路径下的可执行（executable）文件，然而我们在查找系统动态类似于 `UIKit` `MapKit` 等一些系统库的可执行文件时候到其默认输出路径`/System/Library/Frameworks/UIKit.framework`中无法找到对应的executable文件，这是由于苹果官方为了提高性能，不再将动态库单独存放，而是将绝大多数系统动态库都打包存放在一个缓存文件中(dyld shared cache)，默认缓存路径为`/System/Library/Cache/com.app.dyld`,在这个文件夹下，我们可以看到两种架构的动态库缓存文件
()[]

