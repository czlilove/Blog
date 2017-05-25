
打包完ipa提交到appstore时无法构建版本，后来收到了苹果的邮件，提示如下：
>Missing Info.plist key - This app attempts to access privacy-sensitive data without a usage description. The app's Info.plist must contain an NSCameraUsageDescription key with a string value explaining to the user how the app uses this data.

意思是，如果app中要使用手机摄像头，需要在plist中添加NSCameraUsageDescription这一key，并且在value中描述app如何使用这些数据，plist文件中是NSCameraUsageDescription，在XCode中添加的话对应的是Privacy - Camera Usage Description

苹果文档如下：
https://developer.apple.com/library/content/qa/qa1937/_index.html

实际上，如果不添加描述的话，不仅提交时无法构建版本，使用app中需要使用相机等敏感信息的功能时，app会crash的。

