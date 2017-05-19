问题描述：同步失败，因为这台电脑不再被授权使用在此iphone上购买的项目
遇到这个问题想了很多办法，
1.首先既然说未授权，那么就去给这台电脑授权：登录apple id，给这台电脑授权，依然没有卵用，还是一样的错误提示
2.查看手机的udid是不是在ipa里的pp文件里，确实在的（这里，udid在不在pp文件里，其实是不影响安装的，只是安装后不能启动，打开后立马闪退而已）

上面两遍都检查了，实在没有解决办法，只好去问谷哥，找到了这篇文章：
http://stackoverflow.com/questions/20353250/the-iphone-could-not-be-synced-because-this-computer-is-no-longer-authorized-fo
看到下面这个回答
This phone contains apps that were purchased with different Apple ID than the one that the computer is authorized for. So you need to delete those apps to authorize this computer.
意思是手机上安装有使用其他Apple id下载的app，而这台电脑并没有被授权使用这个apple id。所以我们需要把手机上用其他apple id下载的app删除了。
看到这立马醒悟，自己之前使用第三方手机助手（苹果助手，pp助手）在手机上安装了一个app。
把这个app删除，再同步，就把ipa顺利的同步到手机行了。

注意：上面，既不需要iTunes登录apple id，更不需要向电脑授权，就能同步安装ipa到手机上。
