在Animator窗口中添加一个新的transition时，这个新的transition默认Has Exit Time是勾选的。
如果取消勾选，Unity会提示
>Transition needs at least one condition or an Exit Time to be valid.other it will be ignored.

意思是Transition需要至少一个condition或者Exit Time才是有效的。
因此可以看出，Exit Time相当于一个condition，在当前state运行到exit time时并且满足其他condition时才能向下一个state转移。
