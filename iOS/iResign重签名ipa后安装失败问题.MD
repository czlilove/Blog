问题描述：
用iResign重签名ipa，注意entitlements.plist那个不用选，软件会自动帮我们生成一个。
签名完成之后，用XCode Devices窗口安装ipa，有时会报以下错误：
"Can't install application
The Info.plist for application at <path_to_ipa> specifies a CFBundleExecutable of <app_name>, which is not executable
解决方法：
1.Rename yourapp_resigned.ipa to yourapp_resigned.zip
2.Unzip yourapp_resigned.zip to yourapp_resigned folder
3.Launch Terminal, type command: $ cd yourapp_resigned folder
4. Type command: $ chmod -R +x Payload/yourapp (here yourapp is executable file)
5.Type command $ zip -r -T -y yourapp_resigned_fixed.ipa Payload
6.Try to install yourapp_resigned_fixed.ipa to your phone.

前两步可归结为解压重签名后的ipa到一个新的目录
然后在这个目录下执行4,5命令。注意4中，chmod -R +x Payload/yourapp.app

参考：https://github.com/maciekish/iReSign/issues/45
