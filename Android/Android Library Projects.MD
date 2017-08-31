Android Library projects are similar to AAR plug-ins: they contain native and Java code, resources, and an Android Manifest.
However, an Android Library is not a single archive file, but a directory with a special structure which contains all of the Assets.

Import pre-compiled Android library projects into the Assets/Plugins/Android folder.  
Pre-compiled means that all .java files must have been compiled into .jar files and placed in either the bin/ or the libs/ folder of the Android Studio project before being imported into Unity.  
From these folders, AndroidManifest.xml gets automatically merged with the main manifest file when the project is built.

Unity视Assets/Plugins/Android的任一子文件夹为潜在的Android Library，并且禁用了这些子文件夹的资源导入。
如果这些子文件夹含有AndroidManifest.xml文件和project.properties文件，并且project.properties中包含android.library=true这一行字符串，那么这个子文件夹就被Untiy视为Android Library Project

Unity treats any subfolder of Assets/Plugins/Android as a potential Android Library, and disables Asset importing from within these subfolders. The subfolder is recognized as an Android Library if it contains the AndroidManifest.xml file, and the project.properties file contains the string android.library=true.

