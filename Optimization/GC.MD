https://unity3d.com/cn/learn/tutorials/topics/performance-optimization/optimizing-garbage-collection-unity-games?playlist=44069

https://docs.unity3d.com/Manual/BestPracticeUnderstandingPerformanceInUnity4-1.html

概述：

Unity对自己的核心引擎代码和我们自己写的脚本代码，采用不同的内存管理方式。前者需要手动管理，后者采用自动管理方式，也就是自动触发GC。

两种内存池：栈和堆。值类型的局部变量分配在栈上，其他所有的都分配在堆上。

1.为什么要优化GC？

GC（garbage collection）次数太频繁或者每次GC都有大量的工作要做，会导致性能恶化

2.如何确定性能问题主要由GC影响？

使用Profiler Window

自动内存管理如此工作：变量创建时，unity给变量分配内存到堆或栈上，当变量超过作用域时，栈上的内存会立即被回收，堆上的无用内存由gc周期性地回收。

堆内存分配过程：

1.先看堆内存池中是否有足够内存

2.没有足够内存就触发gc，这可能会很慢

3.如果gc后仍没有足够内存，就会增大堆内存池的大小，这可能会很慢。至于每次扩展多少内存？根据平台而不同，但大多数Unity平台都会使内存池大小加倍。

因此堆内存分配这个过程可能很慢，尤其是需要运行gc或者扩大堆内存池大小时。
gc为什么会慢？gc要检查堆上的所有对象，并检查所有的对象引用，看对象是否还有对象引用（object reference）在引用它，如果堆上的对象很多，或者我们代码中的对象引用很多，这种检查就很耗时。

何时触发gc？

1.分配堆内存不足时，见上述

2.clr会周期性地（不定时）运行gc，不同平台频率不同

3.手动运行gc

因为分配堆内存时，如果可用的堆内存不足，会触发gc，因此频繁的分配堆内存和回收堆内存会使gc频繁的发生。

gc可能导致的问题

1.gc可能耗时长

2.gc在不合适的时候运行，应尽量在loading时运行？

内存碎片会导致更多的内存占用（大量空闲内存无法使用，从而导致更多gc）

通过profiler里的gc alloc来查看堆内存分配情况。分配的堆内存在没有变量引用它之后就成为垃圾从而被回收。因此减少堆内存的分配可以减少gc。
