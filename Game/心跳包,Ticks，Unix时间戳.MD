玩家进入游戏以后，客户端定时（比如每十秒）向服务器发送心跳包，服务器收到心跳包后，立即向客户端发送响应消息。
**心跳包及其服务端响应包中的内容通常是服务器的时间**。

对于C#来说，System.DateTime.Ticks表示自公元0001年1月1日凌晨0点0时0分所经历的以100毫微秒为单位的整数。
一秒是10的7次方个tick。也就是1千万个tick.
所以一个tick是10的-7次方秒，MSDN上说一个tick是100毫微秒，那么可以推算出1毫微秒是10的-9次方秒。1秒=10亿毫微秒。
实际上一毫微秒就是一纳秒
1秒=1000豪秒
1毫秒=1000微秒
1微秒=1000毫微秒
1毫微秒＝1纳秒

公元0001年1月1日凌晨0时0分1秒这个时间的Ticks就是10000000
DateTime.Ticks的值也与Kind属性无关，只是计算当前时间距离公元元年的时间差

Unix时间戳：表示从UTC时间1970年1月1日0时0分0秒到现在所经历的秒数。
UTC时间比北京时间慢8小时。比如现在北京时间是24号晚上8点，那么UTC时间还是24号中午十二点。

Unix时间戳的计算方法：
       public static long GetTimeStamp()
       {
           TimeSpan ts = DateTime.UtcNow - new DateTime(1970, 1, 1, 0, 0, 0, 0);
           return Convert.ToInt64(ts.TotalSeconds * 1000);
       }

**DateTime这个结构体，除了年月日时分秒这些属性外，还有一个kind属性。表示当前时间所在的时区，有三种，Utc,Local，Unspecified，**
分别表示Utc时间，计算机本地时间（也就是北京时间），未指定（一般也是本地时间）
时间（2017,1,1,8,0,0,Local）和时间（2017,1,1,8,0,0,Utc）是不一样的。前者比后者晚8小时。
Kind属性可以在DateTime构造函数中指定。DateTime.UtcNow和DateTime.ToUniversalTime()返回的DateTime的Kind属性都是Utc

上面 TimeSpan ts = DateTime.UtcNow - new DateTime(1970, 1, 1, 0, 0, 0, 0);
**DateTime的减法运算实际上是不考虑时区的。也就是说不管时区，是拿两个时间的年月日时分秒去互减得到一个时间差**。

>***The members of the DateTimeKind enumeration are used in conversion operations between local time and Coordinated Universal Time (UTC), but not in comparison or arithmetic operations. For more information about time conversions, see[ Converting Times Between Time Zones](https://msdn.microsoft.com/zh-cn/library/bb397769(v=vs.110).aspx).***

**上面这段描述引用自MSDN，意思是DateTimeKind这一属性只用于本地时间与UTC时间的转换，不用于比较和数学运算。**


