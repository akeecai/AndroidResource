# 数据层 mhttp说明

## 引用说明：
    ### 1.复制mHttp.aar到项目的libs下；
    ### 2.使用的模块的build的android里面说明flatDir 即:
     repositories {
               flatDir {
                     dirs 'libs'
                       }
                }
    ### 3.dependencies 里面：
     implementation(name: 'mhttp', ext: 'aar')

## 使用说明：
    ### 1.在入口配置好ParameterConfig相应的参数（具体参数值看类说明）：
    ParameterConfig.instance().mContext(this).openProxy(true);
    ### 2.业务层可继承BaseDataConvertImp，也可以直接获取对象，调用其中的方法:
    MyPresenter extends BaseDataConvertImp
    ### 3.正常编写业务层的方法，数据操作入口调用BaseDataConvertImp封装的方法。

## 重要类说明：
    ### 1.ParameterConfig.class，参数配置管理类，单例，在请求数据前配置：
    #### timeCache(int mTimeCache)方法设置网络缓存保存时间 默认60 * 1000s
    #### readTimeout(int mReadTimeout)方法设置 读 操作超时时间 默认20 * 1000s
    #### connectTimeout(int mConnectTimeout)方法设置 连接 操作超时时间 默认10 * 1000s
    #### writeTimeout(int mWriteTimeout)方法设置 写 操作超时时间 默认20 * 1000s
    #### retryConnect(boolean mRetryConnect)方法设置是否错误重连 默认重连
    #### openProxy(boolean mProxy)方法设置是否允许代理访问  默认不开启
    #### successCode(int mSuccessCode)方法设置接口返回成功值   默认为1
    #### exceptionCallback(ExceptionCallback mExceptionCallback)设置统一网络请求错误异常回调，如果不设置，默认土司
    #### maxCacheSize(int mMaxCacheSize)方法设置本地缓存的大小，单位是M，默认100M

    ### 2.BaseDataConvertImp.class，数据请求入口：
    #### convert(Observable<T> observable , RequestCallback<T> callBack) 请求网络数据
    #### convert(String key, CommonDYCacheCallback<T> callback) 查询缓存的数据
    #### convert(DataType type, String key, CommonDYCacheCallback<T> callback) 根据DataType类型去查询对应存在本地的数据
    #### commit(String key, T data, CommonDYCacheCallback<T> callback) 缓存数据到DiskCache，注意data需实现Serializable
    #### commit(DataType type, String key, T data, CommonDYCacheCallback<T> callback) 根据DataType类型去缓存数据到本地
    #### remove(String key, CommonDYCacheCallback<String> callback) 根据key删除DiskCache对应的数据
    #### remove(DataType type, String key, CommonDYCacheCallback<String> callback) 根据Key去删除对应DataType类型的缓存数据

    ### 3.RequestCallback.class 请求回调类，对应相应的返回状态的回调方法

    ### 4.CommonDYRequestCallback.class 实现了RequestCallback的请求回调类，内部方法统一将数据解析成BaseDefaultBean基础数据类型，如果接口返回为BaseDefaultBean类的结构，可直接使用该回调

    ### 5.CommonDYCacheCallback.class 实现了RequestCallback的缓存请求回调类，用于缓存操作的回调


