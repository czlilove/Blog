首先要区分 AndroidManifest.xml中的package属性 与 源代码所在的java package

R.java的包名始终与package属性保持一致。

比如说创建新的Android工程时，Src Java包名为com.x,AndroidManifest.xml中的package属性名也为com.x，因此R.java的包名也为com.x

这时MainActivity.java中第一行必定是package com.x
MainActivity可以直接使用R类，因为他们在同一个package。

如果修改了xml中的package属性名或者修改了源代码的package名，必然导致R.java与MainActivity的包名不一致。MainActivity就无法识别R类。

比如修改xml中的package属性名为com.y,R.java的包名也自动换成了com.y,那么MainActivity就无法识别R类了，除非import com.y.R
