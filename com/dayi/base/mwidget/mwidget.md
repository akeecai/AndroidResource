# 控件内容说明

##  1.TitleBar 界面标题栏组合控件
    ### 1.样式资源设置：
        * widget_leftdrawble: 设置左侧按钮资源
        * widget_lefttext: 设置左侧文字
        * widget_lefttextcolor: 设置左侧文字颜色
        * widget_centertitle: 设置中间文字
        * widget_centertextcolor: 设置中间文字颜色
        * widget_rightdrawable: 设置右侧按钮资源
        * widget_righttext: 设置右侧文字
        * widget_righttextcolor: 设置右侧文字颜色
        * widget_bgcolor: 设置titlebar的背景颜色，默认为透明颜色
        * 在xml中示例：
               <com.dayi.mwidget.componts.TitleBar
                    android:layout_width="match_parent"
                    android:layout_height="60dp"
                    app:widget_centertitle="主title"/>

    ### 2.提供方法：
        * 1.setClickListener(OnViewClick mClick) 方法设置titlebar的点击事件
        * 2.对应提供设置样式资源的方法。

    ### 3.说明：
        *当未设置点击事件时，默认左返回按钮调用onBackPressed()方法

## CircleImageView 圆形图片控件

    ### 使用说明：
    * xml 中定义
    <com.dayi.mwidget.componts.CircleImageView
                    android:layout_width="@dimen/widget_dp_34"
                    android:layout_height="@dimen/widget_dp_34"
                    app:widget_civ_border_width="dimen 边框线宽度"
                    app:widget_civ_border_overlay="boolean 是否显示边框"
                    app:widget_civ_border_color="color 边框线颜色"
                    app:widget_civ_fill_color="圆形填充颜色"/>
    * 提供的方法：
    setImageBitmap(Bitmap bm)   设置bitmap
    setImageDrawable(Drawable drawable)     设置drawable
    setImageResource(@DrawableRes int resId)    设置资源
    setImageURI(Uri uri)        设置uri图片


## CircularCornerImageView 圆角图片控件

    ### 使用说明：
    * xml 中定义
    <com.dayi.mwidget.componts.CircularCornerImageView
            android:layout_width="match_parent"
            android:layout_height="@dimen/widget_dp_90"
            app:widget_topleft1_radius="@dimen/widget_dp_12"
            app:widget_topright1_radius="@dimen/widget_dp_12"
            app:widget_bottomleft1_radius="@dimen/widget_dp_12"
            app:widget_bottomright1_radius="@dimen/widget_dp_12"
            android:scaleType="fitXY"
            app:widget_topleft2_radius="@dimen/widget_dp_12"
            app:widget_topright2_radius="@dimen/widget_dp_12"
            app:widget_bottomleft2_radius="@dimen/widget_dp_12"
            app:widget_bottomright2_radius="@dimen/widget_dp_12"
            />

## 界面状态管理（包state.manager）

    ### 1.功能与说明：
    * 可以自由切换内容，空数据，异常错误，加载，网络错误等5种状态
    * 父类BaseActivity直接暴露5中状态，方便子类统一管理状态切换
    * 倘若有些页面想定制状态布局，也可以自由实现，既可以用在单独的页面，也可以放在父类中统一管理状态切换
    * 虽然存在空数据，异常数据，没有网络等异常页面，但是加载布局不会影响性能问题，因为都是用ViewStub控件，只有在显示的时候才inflate出来……
    * 也可以用在list页面局部动态管理，比如加载瀑布流图片，每个图片会有加载loading，加载失败，加载成功等状态
    * StateFrameLayout是继承FrameLayout自定义布局，主要是存放不同的视图，以及隐藏和展示视图操作
    * StateLayoutManager是状态管理器，主要是让开发者设置不同状态视图的view，以及切换视图状态操作
    * 几种异常状态要用ViewStub，因为在界面状态切换中loading和内容View都是一直需要加载显示的，但是其他的3个只有在没数据或者网络异常的情况下才会加载显示，所以用ViewStub来加载他们可以提高性能
    * OnRetryListener，为接口，主要是重试作用。比如加载失败了，点击视图需要重新刷新接口，则可以用到这个，也可以自己设置点击事件

    ### 2.字段（方法）说明：
    * wrapContent   StateFrameLayout布局创建时，是否包裹内容，默认是false，即MATCH_PARENT
    * loadingLayoutResId loading资源ID
    * contentLayoutResId content资源ID
    * netWorkErrorRetryViewId 自定义网络异常布局
    * emptyDataRetryViewId 自定义空数据异常布局
    * errorRetryViewId 自定义错误重新刷新布局
    * retryViewId  自定义重新刷新布局
    * emptyDataIconImageId 空数据图片
    * emptyDataTextTipId 空数据提示文案
    * errorIconImageId 错误提示图片
    * errorTextTipId 错误提示文案
    * errorLayout 自定义异常布局
    * emptyDataLayout 自定义空布局
    * onShowHideViewListener 状态View显示隐藏监听事件
    * onRetryListener 重试加载按钮的监听事件
    * onNetworkListener 重试加载按钮的监听事件
    * 注意：对应的参数字段通过Builder模式配置

    ### 3.使用：
    * 初始化statusLayoutManager，并设置个状态的view
        statusLayoutManager = StateLayoutManager.newBuilder(this)
                .contentView(R.layout.activity_content_data)
                .emptyDataView(R.layout.activity_empty_data)
                .errorView(R.layout.activity_error_data)
                .loadingView(R.layout.activity_loading_data)
                .netWorkErrorView(R.layout.activity_networkerror)
                .onRetryListener(new OnRetryListener() {
                    @Override
                    public void onRetry() {
                        //点击重试
                        showContent();
                    }
                })
                .onNetworkListener(new OnNetworkListener() {
                    @Override
                    public void onNetwork() {
                        //网络异常，点击重试
                        showLoading();
                    }
                })
                .build();
    * 将rootLayout添加到视图里：
    LinearLayout ll_main = (LinearLayout) findViewById(R.id.ll_main);
    ll_main.addView(statusLayoutManager.getRootLayout());
    * 调用statusLayoutManager的各种状态切换的方法：
    showLoading() 显示loading
    goneLoading() 隐藏loading
    showContent() 显示content
    showEmptyData(int iconImage, String textTip) 显示带自定义图片文案的空数据视图
    showEmptyData() 显示空数据
    showLayoutEmptyData(Object... objects) 显示空界面
    showNetWorkError() 显示网络异常
    showError(int iconImage, String textTip) 显示带自定义图片文案的异常视图
    showError() 显示异常
    showLayoutError(Object... objects) 显示异常界面
    getRootLayout() 获取根布局


## BasePopView  BasePop 弹窗封装与管理工具

    ### 1.功能与使用说明：
    * BasePopView 封装管理 BasePop的方法，具体方法参阅方法说明；

    ### 2.方法说明
    #### 1.BasePopView方法说明：
          * 传递对应参数进行窗体创建和显示  _anchor为参照的控件 其他参考参数名英译，其他几个show方法，也只是参数的默认值设定
          show(Context _context, View _anchor, int _layoutResId, int _popW, int _popH,
          boolean bOutsideTouchable, int _backColor, ANIMATION _animation,
          OnEventListenner.OnBaseClickListenner _onClickListenner, SIMPLE_GRAVITY _gravity)

    #### 2. BottomColumnPopupWindow 默认的底部弹窗，数据类型为字符串集合（其他方法根据方法名的含义去理解配置）:
            new BottomColumnPopupWindow.Builder(WidgetActivity.this)
                                        .data(mList)
                                        .targetView(mBtnBottomPop)
                                        .onClickListener((value, pos) -> Toast.makeText(WidgetActivity.this, "value:" + value + "position:" + pos, Toast.LENGTH_LONG).show())
                                        .build()
                                        .show();

    #### 3.CommonPopupWindow 通用自定义弹窗，通过popAdapterListenner方法获取到视图，然后通过获取到的视图去做数据的适配（其他方法根据方法名的含义去理解配置）：
            CommonPopupWindow commonPopupWindow = new CommonPopupWindow.Builder(WidgetActivity.this, R.layout.demo_pop_common)
                                    .targetView(mBtnBottomPop)
                                    .touchAble(true)
                                    .simpleGravity(BasePopView.SIMPLE_GRAVITY.CENTER_IN_PARENT)
                                    .popAdapterListenner((popView, pop_builder) -> {
                                        TextView mTv1 = popView.findViewById(R.id.demo_tv_pop_1);
                                        TextView mTv2 = popView.findViewById(R.id.demo_tv_pop_2);
                                        Button mBtnCancel = popView.findViewById(R.id.demo_btn_pop_cancel);
                                        mTv1.setText("这是设置的第一条数据");
                                        mTv2.setText("这是设置的第二条数据");
                                        mBtnCancel.setOnClickListener(v1 -> pop_builder.dissmiss());
                                    })
                                    .build();
                            commonPopupWindow.show();



## Dialog 弹窗工具 CommonAlertDialog

    ### 功能说明：
    * 通用风格的dialog弹窗；
    * 可根据设置的弹窗类型（CommonAlertDialog中定义的Type类型，来指定现实的弹窗的类型，有：NORMAL_TYPE(默认类型)，ERROR_TYPE，SUCCESS_TYPE等）
    * 提供动态设置弹窗内容的方法
    * 可设置弹窗进度的风格

    ### 使用说明：
    * 1.获取CommonAlertDialog对象，并设置需要的dialog类型（默认是NORMAL_TYPE）
        CommonAlertDialog dialog = new CommonAlertDialog(MainActivity.this, CommonAlertDialog.SUCCESS_TYPE);
    * 2.设置需要的参数
        dialog.setTitleText("title")
              .setContentText("content")
              .setConfirmText("确定")
              .setCancelText("取消")
              .setConfirmClickListener(OnCommonDialogClickListener对象)
              .ssetCancelClickListener(OnCommonDialogClickListener对象);
    * 3. 显示dialog
        dialog.show();
    * 4. 隐藏dialog
        dialog.dismissWithAnimation();
        dialog.cancel();
        dialog.dissmiss();
    * dissmiss方法是Dialog原生的方法，取消diaolog的显示，无动画，其他两种会有动画
    * 4.其他说明
     * 可以通过调用dialog的getProgressHelper()获取进度对象，从而设置进度的样式
     * 可以在回调里获取到dialog对象然后更新dialog的类型以及相关参数，从而达到联动交互的效果
     * 图片类型时调用setCustomImage设置头像

## BannerLayout Banner轮播控件

    ### 1.功能说明：
    * 加载展示banner信息
    * 设置指示器样式，目前支持rect, oval（矩形与圆形）两种
    * 设置指示器选择时颜色
    * 设置view的title
    * 设置是否可以自动轮播

    ### 2.字段（方法）说明：
    * widget_selected_indicator_color 选中后指示器的颜色
    * widget_unselected_indicator_color 未选中时指示器的颜色
    * widget_title_bg_color 标题背景颜色
    * widget_title_color 标题文字颜色
    * widget_indicator_shape 指示器形状 0 矩形 1 圆形
    * widget_selected_indicator_height 选中时指示器高度
    * widget_selected_indicator_width 选中时指示器宽度
    * widget_unselected_indicator_height 未选中时指示器高度
    * widget_unselected_indicator_width 未选中时指示器宽度
    * widget_indicator_space 指示器间距
    * widget_indicator_margin 指示器与底部的距离
    * widget_autoplay_duration 切换间隔时间
    * widget_scroll_duration 切换动作的时间（过程）
    * widget_default_image 默认图片
    * widget_isautoplay 自动切换

    ### 3.使用：
    * 在xml中定义控件
          <com.dayi.mwidget.banner.BannerLayout
                android:layout_width="match_parent"
                android:layout_height="130dp"/>
    * 在xml中根据2（字段说明）中的字段去设置相应的样式
    * 在界面中中得到定义的bannerlayout，设置其图片加载方法
          mBanner.addImageLoader(BannerImageLoadCallback实现对象);
    * 设置要轮播的数据（图片url的集合或者资源中的地址集合）
          mBanner.setViewUrls(图片url集合, 对应的图片名称集合);
          mBanner.setViewRes(图片地址集合, 对应的图片名称的集合)
          注意：在设置图片数据前，一定要先设置好ImageLoader图片加载器
    * 设置banner的点击事件
          mBanner.setOnBannerItemClickListener(OnBannerItemClickListener实现对象);
    * 启动轮播
          mBanner.startAutoPlay();

## 指示器

    ### 说明：
    * 1.CircleIndicator圆形指示器，绑定viewpager
    * 2.CircleIndicator2圆形指示器，绑定recycleview
    * 3.CircleIndicator3圆形指示器，绑定viewpager2

    ### 使用方法（以CircleIndicator为例）：
    * xml中定义指示器以及其位置
    <com.dayi.mwidget.indictor.CircleIndicator
                android:layout_width="match_parent"
                android:layout_height="48dp"/>
    * 界面中得到指示器对象
    CircleIndicator indicator = (CircleIndicator) view.findViewById(R.id.indicator);
    * 调用setViewPager(viewPager)方法绑定跟随的view pager
    indicator.setViewPager(viewPager);
    * 其他两个使用是相同的，只是CircleIndicator2绑定的是recycleview，调用的方法为attachToRecyclerView(RecyclerView recyclerView,SnapHelper snapHelper)，CircleIndicator3绑定的是viewpager2，传的对象是viewpager2

## 广告弹窗AdvertisementDialog

    ### 使用说明：
            AdvertisementDialog
                      .getInstance()
                      .setPaths(mList)
                      .setImageLoader(new AdvertiseImageLoader() {
                           @Override
                           public void loadImag(ImageView view, String path) {

                           }
                       })
                       .setImages(new int[]{})
                       .setCanceledOnTouchOutside(true)
                       .setPageTransformer(new ZoomOutPageTransformer())
                       .show(getSupportFragmentManager());

    ### 方法说明：
    * setImages(int[] images) 设置res资源图片
    * setPaths(List<String> mListPath) 设置图片url
    * setImageLoader(AdvertiseImageLoader loader) 图片加载设置
    * setPageTransformer(ViewPager.PageTransformer pageTransformer) 设置view pager切换动画，目前默认提供两个DepthPageTransformer和ZoomOutPageTransformer
    * show(FragmentManager fragmentManager) 展示
    * setCanceledOnTouchOutside(boolean isCancel) 设置外部是否点击消失，默认取消
    * setOutsideIsTransparent(boolean isTransparent) 设置背景四周是否透明,调用时需要放到show方法后面
    * dissmiss() 消失

























