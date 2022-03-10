# 使用说明

## WXController：
    使用步骤：
    1.在入口初配置申请的appid：WXController.init(Context context, String appid);
    2.在配置文件清单中注册回调路径（详情看注册回调activity的说明）;
    3.调用相应的需要使用的方法.

### 1.微信授权
    说明：WXAuthResultCallback为授权结果的回调，在次处理授权的回调结果

    WXController.getInstance().authByParam(WXAuthParameterBean payBuilder, WXAuthResultCallback callBack);

### 2.微信分享
    说明：WXShareResultCallback为分享结果的回调，在此处理分享结果的回调

    1.分享图片海报，需要在WXShareParameterBean设置好sharePoster
    WXController.getInstance().shareBitmap(WXShareParameterBean payBuilder, WXShareResultCallback callback);

    2.分享文字url，需要在WXShareParameterBean设置好shareTitle,shareUrl,shareDes,shareThumb,shareSence(分享到好友或者朋友圈)
    WXController.getInstance().shareDes(WXShareParameterBean payBuilder, WXShareResultCallback callback);

### 3.微信支付
    说明：WXPayResultCallback为支付结果的回调，可在此处理微信支付结果的回调

    1.引用支付实体去支付
    WXController.getInstance().payByEntity(WXPayOrderBean payBuilder, int extData, WXPayResultCallback callBack);

    2.逐个参数设置去支付
    WXController.getInstance().payByParam(WXPayParameterBean payBuilder, WXPayResultCallback callBack);

### 注册回调activity：
    <!--微信授权,分享回调activity-->
            <activity-alias
                android:name=".wxapi.WXEntryActivity"
                android:exported="true"
                android:targetActivity="com.dayi.mpay.wx.WXEntryActivity" />

    <!--微信支付回调activity-->
                <activity-alias
                    android:name=".wxapi.WXPayEntryActivity"
                    android:exported="true"
                    android:targetActivity="com.dayi.mpay.wx.WXPayCallbackActivity" />

## AliPayController:
    使用步骤：
    1.初始化工具：AliPayController aliPayController = new AliPayController(Context context);
    2.配置相关参数：
    aliPayController.setmPayInfo(String orderInfo);                     //配置支付参数
    aliPayController.setmLoading(boolean loading);                      //跳转过程是否需要过渡效果
    aliPayController.setmPayCallBack(AliPayResultCallback callback);    //支付回调

## PayExceptionUtils 错误统一解析工具
    说明：可在此类添加全局的统一处理动作，但是正常的业务类回调需在界面操作，暂时在支付动作处绑定回调操作
    使用：在入口调用setCallback(PayExceptionCallback callback)方法，在定义的方法中处理动作