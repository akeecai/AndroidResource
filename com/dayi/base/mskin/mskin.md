# 工具说明

## 引用说明
    1.在项目的build中申明远程Maven的地址：
              maven {
                  url "https://raw.githubusercontent.com/akeecai/AndroidResource/master"
              }

    2.在app的build中正常引用对应工具包：
    implementation 'com.dayi.base:mskin:1.0.0'

## 使用说明
    1.在项目入口初始化相关资源，在配置文件配置好权限：
    SkinManager.getInstance().init(this);
    <uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS" /> 在SDCard中创建与删除文件权限
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" /> 往SDCard写入数据权限
    2.在需要使用的界面注册与反注册：
    注册方法：SkinManager.getInstance().register(this);
    反注册方法：SkinManager.getInstance().unregister(this);
    3.资源切换方法：
        3.1 内部资源切换：
        SkinManager.getInstance().changeSkin(sub); sub为新资源名的后缀，
        注意:全新的资源名必须为 原资源名+_sub的拼接，例如原icon资源名为ic_main_a,
        调用该方法后工具会寻找ic_main_a_sub的资源进行替换，同理颜色值也是一样。
        3.2 插件资源切换：
        SkinManager.getInstance().changeSkin(skinPluginPath, skinPluginPkg, callback);
        skinPluginPath:资源包的路径（存储路径）；
        skinPluginPkg：资源包的包名；
        callback：切换回调，包含三个状态onStart(),onError(Exception e),onComplete()。
     4.控件中申明：
        4.1 tag中skin:资源名:资源类型(目前定义了src图片资源,textColor文字颜色,divider分割线,background背景)，如文本颜色：
                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="资源说明"
                    android:tag="skin:demo_test_color:textColor"
                    android:textColor="@color/demo_test_color"/>
        4.2 在要切换资源的控件中，一定要按规则声明tag，否则无法正常切换。