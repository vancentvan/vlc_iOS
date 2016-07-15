# vlc_iOS
Steps to compile vlc for iOS on OS X

1. Preparation
Download these packages from official site http://www.videolan.org/vlc/download-ios.html : VLC for iOS 2.7.0 source code, MediaLibraryKit 2.6.0 source code and MobileVLCKit 3.0.0-pre1 source code, put them into a folder such as vlc_iOS and rename as vlc, MediaLibraryKit and MobileVLCKit,  and besides some tools should be installed on the platform as git, gcc, g++, ant, autoconf, automake, autopoint, cmake, gawk, libtool, m4, patch, pkg-config and so on just according to the installation tips with command 'brew install';

2. Compiling
Open terminal, 'cd' to directory /vlc_iOS/MobileVLCKit/ and enter command sh buildMobileVLCKit.sh or ./buildMobileVLCKit.sh()(Compile for mobile devices without options, for emulator use command sh buildMobileVLCKit.sh -s, when directory /MobileVLCKit/ImportedSources/vlc/ download is completed (may take a long time just continue compiling), followed compilation will launch automatically. Various errors will emerge during this process and some of them should be solved to continue, such as the one below: 

mv: rename gas-preprocessor-72887b9 to gas: No such file or directory, 
This may be caused by the incomplete download package, just delete it and recompile or find the package and copy to the folder;

Actually, most of the errors are caused by the poor network state, just search for related resources and copy to folder /MobileVLCKit/ImportedSources/vlc/contrib/tarballs/. For most of the time, it works well. Some errors with package fribidi, libmatroska, libssh and taglib;

3、Compilation success
[info] Building MobileVLCKit (Aggregate static plugins, Release)
[info] Building MobileVLCKit (MobileVLCKit, Release)
[info] Build for iphoneos completed
When information above shows on the terminal window (similar for both device and simulator), use command to combine them 
lipo -create /Users/apple/Desktop/vlc_iOS/MobileVLCKit/build/Release-iphoneos/libMobileVLCKit.a /Users/apple/Desktop/vlc_iOS/MobileVLCKit/build/Release-iphonesimulator/libMobileVLCKit.a -output /Users/apple/Desktop/vlc_iOS/MobileVLCKit.a
And when you test the supported types you will find armv7 and i386 are both supported
appletekiiMac:~ apple$ lipo -info /Users/apple/Desktop/vlc_iOS/MobileVLCKit.a
Architectures in the fat file: /Users/apple/Desktop/vlc_iOS/MobileVLCKit.a are: armv7 i386 x86_64 arm64 

You can also use command sh buildMobileVLCKit.sh -f directly to deliver dyni=amic library framework MobileVLCKit.framework during compiling and it can be used after bing imported to your project.
