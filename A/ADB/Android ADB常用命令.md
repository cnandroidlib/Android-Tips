#Android ADB常用命令

下面是一些我搜集的一些Android ADB（Android Debug Bridge）命令，在手动或自动构建和测试过程中它们非常好用。

##查看已连接的设备

使用此命令查看所有的连接设备，并列出它们的ID：

	adb devices

如果存在多个设备连接，可以使用 adb -s DEVICE_ID 来指定特定的设备。

##安装应用

使用 install 命令来安装apk，如果设备上已经安装了应用，可以使用可选参数 -r 重新进行安装并保留所有数据。

	adb install -r APK_FILE

	# example
	adb install -r com.growingwiththeweb.example
##卸载应用

	adb uninstall PACKAGE_NAME

	# example
	adb uninstall com.growingwiththeweb.example
##启动Activity

	adb shell am start PACKAGE_NAME/ACTIVITY_IN_PACKAGE
	adb shell am start PACKAGE_NAME/FULLY_QUALIFIED_ACTIVITY
	
	# example
	adb shell am start -n com.growingwiththeweb.example/.MainActivity
	adb shell am start -n com.growingwiththeweb.example/com.growingwiththeweb.example.MainActivity
##进入设备的命令行

	adb shell
##截取屏幕

Sergei Shvetsov 写出了一行漂亮的PERL代码,它利用 shell screencap截屏并输出到本地目录中，访问他的博客获取详细信息。

	adb shell screencap -p | perl -pe 's/\x0D\x0A/\x0A/g' > screen.png
##解锁屏幕
向设备发送屏幕解锁命令：

	adb shell input keyevent 82
##日志

###用来在命令行中显示日志流：

	adb logcat
###按标签名过滤

	adb logcat -s TAG_NAME
	adb logcat -s TAG_NAME_1 TAG_NAME_2
	
	# example
	adb logcat -s TEST
	adb logcat -s TEST MYAPP
###按优先级过滤

显示指定告警优先级及以上的日志：

	adb logcat "*:PRIORITY"

	# example
	adb logcat "*:W"
	优先级设置如下：
	
	V：Verbose （最低优先级）
	D：Debug
	I：Info
	W：Warning
	E：Error
	F：Fatal
	S：Silent （最高优先级, 在这个级别上不会打印任何信息)）
###按标签名和优先级过滤

	adb logcat -s TAG_NAME:PRIORITY  
	adb logcat -s TAG_NAME_1:PRIORITY TAG_NAME_2:PRIORITY` 
	# example  
	adb logcat -s TEST: W
###使用grep过滤

另外，在支持grep的系统中，logcat输出可以通过管道发送给grep：

	adb logcat | grep "SEARCH_TERM"
	adb logcat | grep "SEARCH_TERM_1\|SEARCH_TERM_2"
	
	# example
	adb logcat | grep "Exception"
	adb logcat | grep "Exception\|Error"
清除logcat的缓冲区
使用这个命令来清除缓冲区，并清除旧的日志数据：

	adb logcat -c
延伸阅读

更多详细信息请参考[adb官方网站](http://developer.android.com/tools/help/adb.html "adb官方网站")。

原文：[Handy adb commands for Android](http://www.growingwiththeweb.com/2014/01/handy-adb-commands-for-android.html)

转载自：[伯乐在线](http://blog.jobbole.com/61592/) - [lum](http://blog.jobbole.com/author/lumeng689/)