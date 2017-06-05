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
