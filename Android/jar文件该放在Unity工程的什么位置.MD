http://answers.unity3d.com/questions/837762/where-can-jar-files-be-placed-under-assetspluginsa.html

We support the following Android plugin types:

plain compiled .jar files - can be placed in Assets/Plugins/Android, Assets/Plugins/Android/bin and Assets/Plugins/Android/libs. They are copied to StagingArea and compiled into resulting .dex. No resource or manifest merging available here (only complete overriding the manifest by placing it into Assets/Plugins/Android/AndroidManifest.xml)

Android library projects - this is a subdir in Assets/Plugins/Android with its own project structure (just as you described in the original post). The compiled .jar file can be placed in libs/ or bin/, resources and manifests are merged. Please refer to Android Library Project section in http://docs.unity3d.com/Manual/PluginsForAndroid.html for more details.

My wild guess is that your subdirs are not being identified as Android Library projects because the project.properties file does not contain

 android.library=true 
line. Try adding it... Though you would probably also need some magic with the manifests, but the classes should be present now.

评论 ·  隐藏 2 · 分享
avatar imageswquinn · 2014年11月21日 21:05 0
Ah! I think you're right! Let me try the android.library property. I forgot completely about that! I actually think I may have made a change to that property haphazardly before. Do you happen to know where (if at all) that property is documented? I couldn't find it.

 avatar imageswquinn · 2014年11月22日 00:42 0
Thanks Yury, that was exactly the issue that I was experiencing. Both in the case that one of my subfolders had a project.properties with android.library=false and another didn't have one at all.

Also, in case anyone is interested it appears .jar files in the root of Plugins/Android will be staged under the StagingArea/plugins directory, whereas subfolders identified by android.library=true in the project.properties files will be staged under StagingArea/android-libraries.
