# 工具库说明

    ## ConvertStringUtil 字符处理工具类
        * rightNum(String strData, int num)：从右开始截取字符串，strData需要截取的资源，num截取多少位
        * leftNum(String strData, int num)：从左开始截取字符串，strData需要截取的字符串资源，num要截取的位数
        * midNum(String strData, int frome, int num)：从字符串的第几位开始截取，strData需要截取的字符串资源，frome从第几位开始截取，num截取多少位
        * subStringBefore(String strData, String sub)：截取字符串指定字符的前段，strData需要截取的资源，sub指定的字符串
        * subStringAfter(String strData, String sub)：截取字符串指定字符的后段，strData需要截取的资源，sub指定的字符串
        * subNumSplitSign(String strData, int from, int num, String sign)：从指定第from位开始截取，截取num位， 并在末尾拼接sign
        * copyStr(String value)：复制文本
        * checkStr2Int(String str)：判断字符串是否可以转成number

    ## ConvertDateUtil 时间转换工具
        * getDateMMDD(): 获取当前日期几月几号
        * getDateYYMMDD(): 获取当前年月日
        * getWeek(String time): 根据当前日期获得是星期几(time为yyyy-mm-dd类型)
        * getDateNextWeekMMDD()：获取今天往后一周的日期（几月几号）
        * getDateBeforeWeekMMDD()：获取今天往前一周的日期（几月几号）
        * getDateBeforeDay(int day)：获取今天往前day天的日期（yyyy-MM-dd）
        * getDateAfterDay(int day)：获取今天往后day天的日期（yyyy-MM-dd）
        * queryData(String startAt, String endAt)：给定开始和结束时间，遍历之间的所有日期
        * queryData(Date startAt, Date endAt)：给定开始和结束时间，遍历之间的所有日期
        * getDateNextWeekYYMMDD()：获取今天往后一周的日期（哪年哪月哪日）
        * getDateNextWeekDD()：获取今天往后一周的日期（几号）
        * getDateNextWeekMMDD_()：获取今天往后一周的日期（几月几号,xx-xx形式）
        * getDateNextWeekDDOfWeek()：获取今天往后一周的集合(周几)
        * getDateNextWeekYYMMDD_()：获取今天往后一周的日期（yyyy-MM-dd  年-月-日）
        * MaxDayFromDay_OF_MONTH(int year, int month)：得到当年当月的最大日期
        * format(Date date)：把当前日期转换格式为yyyy-MM-dd
        * format(Date date, String format)：把当前日期转换为指定格式
        * getTodayYYMMDD_()：获得当前日期（yyyy-MM-dd）
        * getTomorrowYYMMDD_()：获得明天日期（yyyy-MM-dd）
        * getTimeYYMMDDHHMMSS_()：获得当前时间（yyyy-MM-dd HH:mm:ss）
        * dateToStampLong(String time, String format)：时间转时间戳（得到long）
        * dateToStampString(String time, String type)：时间转时间戳（得到String）
        * stampStringToDate(String time, String format)：string类型的时间戳转时间
        * stampLongToDate(Long time, String format)：long类型的时间戳转时间
        * getDateMMDDWeekHHMM(long timeStamp)：long类型时间戳转换成 MM月dd日 周 HH:mm类型
        * getDayOfWeek(long timeStamp)：long 型时间戳转成周几
        * getMonthDays(int year, int month)：根据当前年份 月份 ，获取当前月份的天数
        * getWeekName(int column)：根据列名 获取周
        * isToday(String day)：判断是否为今天(效率比较高)
        * isToday2(String sdate)：判断给定字符串时间是否为今日(效率不是很高，不过也是一种方法)
        * getDateFormat()：获取yyyy-MM-dd hh:mm:ss类型的dateformat
        
    ## AppUtils App工具类
        * 使用前先调用init()方法初始化（可放在application的oncreate方法里去初始化）
            AppUtils.init(this);
        * getApp()：返回该进程的Application
        * runOnUiThread(final Runnable runnable)：在UI线程运行
        * runOnUiThreadDelayed(final Runnable runnable, long delayMillis)：延时多久在UI线程运行
        * getCurrentProcessName()：获取当前进程名

    ## ActivityUtils activity管理工具
        * getActivityByView(@NonNull View view)：根据视图返回activity对象
        * getActivityByContext(Context context)：根据上下文返回activity对象
        * isActivityExists(@NonNull final String pkg,@NonNull final String cls)：根据包名类名判断activity是否还存在
        * startActivity(@NonNull final Class<? extends Activity> clz)：跳转（frome默认为最上面的activity）
        * startActivity(@NonNull final Class<? extends Activity> clz, @Nullable final Bundle options)：带参跳转
        * startActivity(@NonNull final Class<? extends Activity> clz, @AnimRes final int enterAnim, @AnimRes final int exitAnim)：动画跳转
        * startActivity(@NonNull final Activity activity, @NonNull final Class<? extends Activity> clz)：跳转
        * 其他的跳转，forresult跳转，多activity跳转，参考参数的含义
        * startHomeActivity()：跳转到homeActivity
        * startLauncherActivity()：跳转到launcheractivity
        * startLauncherActivity(@NonNull final String pkg)：根据包名跳转到launcheractivity
        * getActivityList()：获取activity列表
        * getLauncherActivity()：获取launcheractivity包名
        * isActivityAlive(final Context context)：判断activity是否活跃
        * isActivityExistsInStack(@NonNull final Activity activity)：activity是否在stack内
        * finishActivity(@NonNull final Activity activity)：结束activity

    ## SPUtils SharedPreferences工具类
        * getInstance():获取默认名称，默认模式的SharedPreferences工具类
        * getInstance(final int mode)：获取默认名称，指定模式的SharedPreferences工具类
        * getInstance(String spName)：获取指定名称，默认模式的SharedPreferences工具类
        * getInstance(String spName, final int mode)：获取指定名称，指定模式的SharedPreferences工具类
        * 其他是对应基本类型的put与get方法
        
    ## StatusBarUtil 状态栏工具类
        * fullScreen(Activity activity)：全屏（隐藏状态栏）
        * transparent(Activity activity)：透明状态栏
        * halfTransparent(Activity activity)：状态栏半透明效果
        * setRootViewFitsSystemWindows(Activity activity,boolean fitsSystemWindows)：代码设置 fitsSystemWindows
        * getStatusBarHeight(Context context)：获取状态栏高度
        * setStatusBarColor(Activity activity,boolean isDarkMode,int color)：设置状态栏背景色以及字体是否深色模式
        * setDarkMode(Activity activity)：设置深色的图标和字体
        * setLightMode(Activity activity)：设置白色的图标和字体
        
    ## ToastUtils 土司工具类
        * setGravity(final int gravity, final int xOffset, final int yOffset)：设置吐司位置
        * setBgColor(@ColorInt final int backgroundColor)：设置背景颜色
        * setBgResource(@DrawableRes final int bgResource)：设置背景资源
        * setMsgColor(@ColorInt final int msgColor)：设置消息颜色
        * showShort(@NonNull final CharSequence text)：安全地显示短时吐司
        * showShort(@StringRes final int resId)：安全地显示短时吐司
        * showLong(@NonNull final CharSequence text)：安全地显示长时吐司
        * showLong(@StringRes final int resId)：安全地显示长时吐司
        * showCustomShort(@LayoutRes final int layoutId)：安全地显示短时自定义吐司
        * showCustomLong(@LayoutRes final int layoutId)：安全地显示长时自定义吐司
        * cancel()：取消吐司显示
        


        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        