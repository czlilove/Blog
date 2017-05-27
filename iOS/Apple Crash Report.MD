# 两种方法 ：
# 1 .
打包时选中Include app symbols for your application…，用户安装完应用后，同意向开发者分享数据。那么开发者就可以在XCode的Organizer的Crashes中看到Crash Report
## 2.
连接设备，在XCode的Devics窗口中的View Device Log后，拖入crashlog，XCode会自动分享crashlog.

**注意crashlog的后缀必须是.crash,Archive中必须要包含对应版本的dSYM文件**

https://developer.apple.com/library/content/technotes/tn2151/_index.html

https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppDistributionGuide/AnalyzingCrashReports/AnalyzingCrashReports.html

https://developer.apple.com/library/content/qa/qa1747/_index.html
