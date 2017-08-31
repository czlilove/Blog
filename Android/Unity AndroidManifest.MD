# Unity如何生成Android Manifest ?
Unity打包app时，会按照以下步骤自动生成Android Manifest：
## 一.确定Main Android Manifest。如果没有Assets/Plugins/Android/AndroidManifest.xml，那么就是Unity默认的一个Manifest.
## 二.找到所有插件（必须是安卓库工程或者Android Studio的ARR)的AndroidManifest.xml
## 三.使用谷歌的Google’s manifmerger类，将插件中的AndroidManifest.xml被合并到Main Android Manifest。
## 四.Unity修改Manifest，根据PlayerSettings,更改包名，版本号，自动添加权限，配置选项。。。


# 自定义Android Manifest:
把自定义的Android Manifest放在Assets/Plugins/Android/AndroidManifest.xml，从而覆盖Unity生成的原始Manifest.这个Manifest就是Main Manifest。
这时，Android库工程的Manifest仍会被合并到Main Manifest中。

# 何为Android Library Projects
Android Library projects should be added as a subdirectory in Assets/Plugins/Android, for example Assets/Plugins/Android/myandroidlibrary. It must contain project.properties file with android.library set to true, and AndroidManifest.xml - in that case it is recognized as an Android Library.
必须有一个project.properties文件，并且其中的android.library设置为true，还要有一个AndroidManifest.xml文件，这样一个文件夹就被视为Android Library，其中的AndroidManifest.xml才会被自动合并到主Manifest中。


检查最终生成的Android Manifest:
Unity为APP最终生成的Android Manifest，可以在Temp/StagingArea/AndroidManifest.xml中看到。这是个二进制文件，需要使用Android Studio APK Analyzer或者第三方工具 (比如Apktool)打开.


After building, please check that Temp/StagingArea/android-libraries dir contains your plugin. If it does not - then you are probably missing something, just post a simple project and I'll take a look.


Well, we support the following plugin types for Android:


- native .so files (you have to check the correct architecture for them in Plugin inspector)
- compiled .jar files
- Android library projects (preferred over jars, especially if you have resources or want to merge your manifest with Unity manifest)
- AARs (same as Android library, but easier as this is a single file)（5.x才支持AAR）




Then goes the manifest merging logic.
If you have your own manifest here: Assets/Plugins/Android/AndroidManifest.xml, it is taken as the base one, otherwise Unity default manifest is used as the base one.


Next, it gets merged with all Android Libraries' manifests.


Last step - properties, uses-features and permissions are set.








Permissions


Unity automatically adds the necessary permissions to the Manifest based on the Player Settings and Unity APIs that your app calls from the script. For example:


Network classes add the INTERNET permission
Using vibration (such as Handheld.Vibrate) adds VIBRATE
The InternetReachability property adds ACCESS_NETWORK_STATE
Location APIs (such as LocationService) adds ACCESS_FINE_LOCATION
WebCamTexture APIs add CAMERA permission
The Microphone class adds RECORD_AUDIO
For more information about permissions, see the Android Manifest Permissions page of the Android Developer documentation.


Note that if your plug-ins require a permission by declaring it in their Manifests, the permission is automatically be added to the resulting Android Manifest during the merge stage. Any Unity APIs called by the plug-ins also contribute to the permission list.








