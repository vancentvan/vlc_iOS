# vlc_iOS
Course of compiling for iOS on OS X

1、编译准备：
首先下载三个包（地址：http://www.videolan.org/vlc/download-ios.html），VLC for iOS 2.7.0 source code、MediaLibraryKit 2.6.0 source code和MobileVLCKit 3.0.0-pre1 source code，放入文件夹如vlc_iOS中并分别命令为vlc、MediaLibraryKit和MobileVLCKit(文件夹名称随意修改)，其他的要安装的准备工具，如：git，gcc，g++，ant，autoconf，automake，autopoint，cmake，gawk，libtool，m4，patch，pkg-config等等，按照提示安装即可（brew install命令）；

2、开始编译
	打开终端，进入vlc_iOS/MobileVLCKit/目录，输入命令sh buildMobileVLCKit.sh或者./buildMobileVLCKit.sh（真机编译，模拟器编译命令：sh buildMobileVLCKit.sh -s），等待MobileVLCKit/ImportedSources/目录下下载vlc相关编译文件（这块可能下载比较慢，也很有可能会下到一半直接挂掉，这步与网络状况有直接联系），git上下好之后编译就会自行自动，中间会出现各种各样的错误，没关系，一个一个解决即可，如错误：
mv: rename gas-preprocessor-72887b9 to gas: No such file or directory，可能就是因为下载包不完整导致，可以将其删除重新编译，或者找到相关的包下载好拷贝进去即可；
其实大部分的错误差不多都是下载出错，这可以在网上搜索相关资源下载拷贝入MobileVLCKit/ImportedSources/vlc/contrib/tarballs文件夹中一般都可以轻松解决，如：我就遇到fribidi、libmatroska、libssh和taglib文件的下载失败问题，都是在网上下载解决的；

3、编译成功
[info] Building MobileVLCKit (Aggregate static plugins, Release)
[info] Building MobileVLCKit (MobileVLCKit, Release)
[info] Build for iphoneos completed
当看到上面所示说明时表明编译成功（真机和模拟器类似），然后将两者合并：
lipo -create /Users/apple/Desktop/vlc_iOS/MobileVLCKit/build/Release-iphoneos/libMobileVLCKit.a /Users/apple/Desktop/vlc_iOS/MobileVLCKit/build/Release-iphonesimulator/libMobileVLCKit.a -output /Users/apple/Desktop/vlc_iOS/MobileVLCKit.a
检测支持类型会发现armv7和i386都是支持的
appletekiiMac:~ apple$ lipo -info /Users/apple/Desktop/vlc_iOS/MobileVLCKit.a
Architectures in the fat file: /Users/apple/Desktop/vlc_iOS/MobileVLCKit.a are: armv7 i386 x86_64 arm64 

也可以直接在编译的时候使用命令 sh buildMobileVLCKit.sh -f直接得到动态库文件MobileVLCKit.framework，导入项目即可使用。
