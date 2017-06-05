用ILSpy反编译Dll，可以看到任何一个foreach语句的实现都是这样的

    IEnumerator enumerator = this.xx.GetEnumerator();
    try
    {
        while(enumerator.MoveNext())
        {
            xxx xxxx = (xxx)enumerator.Current;
            ....
        }
    }
    finally
    {
        IDisposable disposable;
        if((disposable = (enumerator as IDisposable)) !=null)
        {
            disposable.Dispose();
        }
    }

所以，foreach里面的类必须有一个GetEnumerator方法返回一个IEnumerator（或者是自定义的类实现了MoveNext和Current即可）实例。

enumerator.Current的类型是object，所以这里有一个强制转换
