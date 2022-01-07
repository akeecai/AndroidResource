# 使用说明

## 主要内容

    工具主要包含两个组合控件：
    1.刷新控件DYRefreshLayout，可自定义刷新头；
    2.列表控件DYRefreshView，可自定义刷新头。

    两个自定义的常用刷新头（注意，所有自定义的刷新头需要继承自DYRefreshLayout.BaseRefreshView）：
    1.菊花型 + 文字说明的刷新头SimplePullModel；
    2.Android官方自带的圆球型刷新头CircleMaterialModel。

    两种类型的适配器：
    1.简单型BaseRecyclerAdapter，快捷做数据适配；
    2.通用型CommonRecyclerAdapter，控制相关状态。

## 调用说明

    刷新控件DYRefreshLayout：
    1.在xml中声明控件（注意：子控件需要可滑动控件，如ScrollView，RecyclerView，ListView等）：
    <com.dayi.mrefresh.layout.DYRefreshLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <androidx.core.widget.NestedScrollView
                android:layout_width="match_parent"
                android:layout_height="match_parent">

            </androidx.core.widget.NestedScrollView>

    </com.dayi.mrefresh.layout.DYRefreshLayout>
    2.在调用的时候配置刷新头：
    通过setRefreshView(T view)方法配置
    3.在完成刷新的时候调用setRefreshing(false)方法取消刷新效果

    列表控件DYRefreshView：
    1.在xml中申明控件：
    <com.dayi.mrefresh.layout.DYRefreshView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:overScrollMode="never"/>
    2.在调用处配置相关样式：
    setCacheSize配置预加载数据条数
    scrollToPosition配置预滚动到第几条数据
    clear清除适配器
    setModel(DYRefreshLayout.BaseRefreshView model)配置自定义刷新头的样式，默认为菊花+文字说明样式；
    setEmptyView配置空数据界面
    showEmpty显示空界面
    setProgressView配置加载中界面
    showProgress显示加载界面
    showRecycler显示数据加载完
    setErrorView配置错误界面
    showError显示错误界面
    setRefreshListener设置下拉刷新监听
    setRefreshing设置是否刷新
    以及其他recyclerview相关的方法

    简单型BaseRecyclerAdapter：
    1.构造方法BaseRecyclerAdapter(Collection<T> collection, @LayoutRes int layoutId, AdapterView.OnItemClickListener listener)，
      collecation为数据源
      layoutId为item的布局文件
      listener为item点击事件
    2.抽象方法onBindViewHolder(SmartViewHolder holder, T model, int position)，
      holder包含布局中申明的所有控件，可通过id去做相应的配置或获取该控件的对象
      model是适配的数据
      position是数据位置
    3.refresh方法刷新数据
      loadMore加载数据

    通用型CommonRecyclerAdapter：
    1.正常的通过构造方法获取到适配器的对象；
    2.配置相关的方法与回调：
    数据部分：
     addAll(Collection<? extends T> collection)或addAll(T[] items) 添加所有数据
     add(T object)添加单条数据
     insert(T object, int index)，insertAll(T[] object, int index) 或insertAll(Collection<? extends T> object, int index)在index处插入数据
     update(T object,int pos)更新pos处的数据
     remove(T object)或remove(int position)移除数据
     setTop(int position)置顶数据
     clear()清除所有数据
     sort(Comparator<? super T> comparator)使用指定的比较器对此适配器的内容进行排序
     setNotifyOnChange(boolean notifyOnChange)设置操作数据[增删改查]后，是否刷新adapter，默认刷新
     状态与样式部分：
     setHeaderAndFooterSpan(boolean isHeaderAndFooterSpan)多列数据时，最后一行（footer）是否占全格
     stopMore()停止加载更多
     pauseMore()暂停加载更多
     resumeMore()恢复加载更多
     setMore(final int res, final OnLoadMoreListener listener)或setMore(final View view,final OnLoadMoreListener listener)设置上拉加载更多的自定义布局和监听（自动触发）
     setMore(final int res, final OnMoreListener listener)或setMore(final View view,OnMoreListener listener) 设置上拉加载更多的自定义布局和监听（手动触发）
     setNoMore(final int res)或setNoMore(final View view)设置上拉加载没有更多数据时的布局
     setNoMore(final View view , OnNoMoreListener listener)或setNoMore(final @LayoutRes int res , OnNoMoreListener listener)设置上拉加载没有更多数据时的布局与监听






