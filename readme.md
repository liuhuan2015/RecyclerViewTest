>RecyclerView源码分析——绘制流程 [【进阶】RecyclerView源码解析(一)——绘制流程](https://www.jianshu.com/p/c52b947fe064)

三个方法：

dispatchLayoutStep1:<br>
    1. 处理Adapter更新
    2. 决定是否执行 ItemAnimation
    3. 保存 ItemView 的动画信息

dispatchLayoutStep2:<br>
    1. 进行 children 的测量和布局

dispatchLayoutStep3:<br>
    1. 执行在 dispatchLayoutStep1 里面保存的动画信息


layoutChunk(...)


总结

1. RecyclerView是将绘制流程交给LayoutManager处理，如果没有设置不会测量子View。
2. 绘制流程是区分正向绘制和倒置绘制。
3. 绘制是先确定锚点，然后向上绘制，向下绘制，fill()至少会执行两次，如果绘制完还有剩余空间，则会再执行一次fill()方法。
4. LayoutManager获得View是从RecyclerView中的Recycler.next()方法获得，涉及到RecyclerView的缓存策略，如果缓存没有拿到，则走我们自己重写的onCreateView方法。
5. 如果RecyclerView宽高没有写死，onMeasure就会执行完子View的measure和Layout方法，onLayout仅仅是重置一些参数，如果写死，子View的measure和layout会延后到onLayout中执行。

