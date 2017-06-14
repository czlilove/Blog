在Animator窗口中添加一个新的transition时，这个新的transition默认Has Exit Time是勾选的。
如果取消勾选，Unity会提示
>Transition needs at least one condition or an Exit Time to be valid.other it will be ignored.

意思是Transition需要至少一个condition或者Exit Time才是有效的。
因此可以看出，Exit Time相当于一个condition，在当前state运行到exit time时并且满足其他condition时才能向下一个state转移。

>If you have Has Exit Time selected for the transition and have one or more conditions, note that the Unity Editor considers whether the conditions are true after the Exit Time. This allows you to ensure that your transition occurs during a certain portion of the animation.

>If Has Exit Time is enabled for the transition and has one or more conditions, these conditions are only checked after the exit time of the state. This allows you to ensure that your transition only occurs during a certain portion of the animation.

上述两段文字引用自[Unity官方文档](https://docs.unity3d.com/Manual/class-Transition.html)，意思大体相同：
如果Has Exit Time启用了，且transition还有其他condition，那么只有在exit time之后，才会判断其他condition是否成立，也就是说，在当前state运行到exit time之后才会向下一个state转移。

与此相反，如果没有勾选Has Exit Time，那么在condition满足后，会立即向下一个state转移，而不会等到exit time后再转移。

不管什么时候向下一个state转移，trannsition duration都是固定的。

举例来说，从idle->dead，condition为death=true,exit time=0.8,trannsition duration=0.2，fixed duration = false，idle时长3秒
在idle播放到50%的时候，death改变为true，

如果Has Exit Time为true,那么在idle 播放到80%的时候开始向dead过渡,历时3秒*0.2=0.6秒完全过渡到dead状态

如果Has Exit Time为false，那么在idle播放到50%的时候就立刻向dead过渡，仍然历时3秒*0.2=0.6秒完全过渡到dead状态。

在3秒*0.2=0.6秒这段过渡时间内，是idle向dead过渡的阶段，也是idle与dead的融合阶段。
上述两种情况下，前者是idle动画的80%至100%阶段与dead动画融合；
              后者是idle动画的50%至70%阶段与dead动画融合。
