 # 2017 06 09
[文档地址](http://pan.baidu.com/disk/home?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&#list/vmode=list&path=%2F%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6%E5%A4%B9%2F%E5%AE%89%E5%8D%93%E9%A1%B9%E7%9B%AE%E4%BB%A3%E7%A0%81%E4%BB%93%E5%BA%93%2FMarkDown%E5%BC%80%E5%8F%91%E6%96%87%E6%A1%A3 "查看") —— [源文件相关](http://pan.baidu.com/disk/home?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&#list/vmode=list&path=%2F%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6%E5%A4%B9%2F%E9%A1%B9%E7%9B%AE%E6%A8%A1%E5%9D%97%2F%E6%A8%A1%E5%9D%97%E7%B3%BB%E5%88%97%2FTanYinQingAar "查看")——  [个人首页](https://tanyinqing.github.io/)

<h1 id="1">目录1</h1> 
网络→[1. 待定](#101)

<h1 id="2">目录2</h1> 
其他→[说明](#201)→[如何创建](#202)
global→[3. MyApplication](#203)→[4. Constant](#204)

 <h1 id="3">目录3</h1> 
[1. 资源的引用](#301)→[2. AndroidManifest.xml](#302)→[3. styles.xml](#303)→[4. themes.xml](#304)→[5. colors.xml](#305)→[6. dimens.xml](#306)→[7. strings.xml](#307)

参考文档
[Aar地址git](https://github.com/tanyinqing/TanYinQingAar)

1. 简介  

<h1 id="201">1. 说明</h1>

[返回目录](#2)

包含的Jar有andbase.jar→universal-image-loader-1.9.3.jar→xUtils-2.6.14.jar

源代码的名字叫 TanYinQingJar  这个文件的作用就是一些资源文件，记住包里不加入依赖，都是源代码，不和别的项目绑定。

<h1 id="202">2. 如何创建</h1>

[返回目录](#2)

使用Aar文件时要进行配置
 compile(name: 'tanyinqingmyaar-release', ext: 'aar')

使用AAr包时 这个是app的module中的配置

```java
  buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
       			 }
   			 }
      repositories {
              flatDir {
                    dirs 'libs'
                    	}
       			 }

```
本地电脑地址
D:\studiospace\MyCode

```

建立子模块时一定要选中Android Library


但是必须apk要加入对module的依赖才可以生成jar


在android studio 提供的Terminal中（目录默认伟当前工程的）键入 gradlew makeJar 回车看到如下所示就OK了


//Copy类型  这个的子module中配置 放到最后的位置
task makeJar(type: Copy) {
    //删除存在的
    delete 'build/libs/mysdk.jar'
    //设置拷贝的文件
    from('build/intermediates/bundles/release/')
    //打进jar包后的文件目录
    into('build/libs/')
    //将classes.jar放入build/libs/目录下
    //include ,exclude参数来设置过滤
    //（我们只关心classes.jar这个文件）
    include('classes.jar')
    //重命名
    rename ('classes.jar', 'mysdk.jar')
}

makeJar.dependsOn(build)
//在终端执行生成JAR包
// gradlew makeJar
```
<h1 id="301">1. 资源的引用</h1>

[返回目录](#3)

```
android:theme="@style/myTheme"

```
<h1 id="302">2. AndroidManifest.xml</h1>

[返回目录](#3)

四大组件的声明
```
 <activity
            android:name=".aar_Activity.MainActivity"
            android:label="@string/app_name"
            android:configChanges="keyboardHidden|orientation">
        </activity>
```
application
```
 <application        			android:name=".andbase.global.MyApplication"
        android:allowBackup="true"
        android:label="@string/app_name"
        android:theme="@style/myTheme">
```
权限
```
<!--bar-->
    <uses-permission android:name="android.permission.EXPAND_STATUS_BAR" />
    <!--读写内存-->
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <!--flashlight-->
    <uses-permission android:name="android.permission.CAMERA" />
    <uses-feature android:name="android.hardware.camera" />
    <uses-feature android:name="android.hardware.camera.autofocus" />
    <uses-feature android:name="android.hardware.camera.flash" />
    <uses-permission android:name="android.permission.FLASHLIGHT" />
    <!--位置-->
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <!--<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />-->
    <!--网络-->
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <!--<uses-permission android:name="android.permission.MODIFY_PHONE_STATE" />-->
    <uses-permission android:name="android.permission.INTERNET" />
    <!--打电话-->
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    <!--拨打电话-->
    <uses-permission android:name="android.permission.CALL_PHONE" />
    <!--发送短信-->
    <uses-permission android:name="android.permission.SEND_SMS" />
    <!--获取手机联系人-->
    <!--<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>-->
    <uses-permission android:name="android.permission.READ_CONTACTS" />
    <!--获取短信-->
    <!--<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>-->
    <uses-permission android:name="android.permission.READ_SMS" />
    <!--进程-->
    <uses-permission android:name="android.permission.KILL_BACKGROUND_PROCESSES" />
    <!-- 其他 -->
    <uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
    <uses-permission android:name="android.permission.WAKE_LOCK" />
    <uses-permission android:name="android.permission.VIBRATE" /> //振动
    <uses-permission android:name="android.permission.RECORD_AUDIO" />
    <!-- -->
    <uses-permission android:name="com.android.launcher.permission.INSTALL_SHORTCUT" />
    <uses-permission android:name="com.android.browser.permission.READ_HISTORY_BOOKMARKS" />
    <uses-permission android:name="com.android.browser.permission.WRITE_HISTORY_BOOKMARKS" />

```
<h1 id="303">3. styles.xml</h1>

[返回目录](#3)

```
<resources>

    <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
        <!-- Customize your theme here. -->
    </style>


    <style name="Widget" parent="android:Widget"></style>

    <style name="mCustomWindowTitleBackground" parent="@style/Widget">
        <item name="android:background">@color/transparent</item>
    </style>
    <!--这个对可扩展列表的修改-->
    <style name="mExpandableListView" parent="@style/Widget">
        <item name="android:groupIndicator">@drawable/expander_group</item>
        <item name="android:indicatorLeft">10dip</item>
        <item name="android:indicatorRight">
            ?android:attr/expandableListPreferredItemIndicatorRight
        </item>
        <item name="android:childDivider">@drawable/list_divider</item>

    </style>
    <!--这个对条形进度条的修改-->
    <style name="mProgressBarHorizontal" parent="@style/Widget">
        <item name="android:indeterminateOnly">false</item>
        <item name="android:progressDrawable">@drawable/progress_horizontal</item>
        <item name="android:indeterminateDrawable">@drawable/progress_indeterminate_horizontal
        </item>
        <item name="android:minHeight">5dip</item>
        <item name="android:maxHeight">5dip</item>
    </style>
    <!--这个圆形进度条的修改-->
    <style name="mProgressBarCircular" parent="@style/Widget">
        <item name="android:indeterminateOnly">true</item>
        <item name="android:indeterminateDrawable">@drawable/progress_circular</item>
        <item name="android:minHeight">5dip</item>
        <item name="android:maxHeight">5dip</item>
    </style>
    <!--这个对白按钮的修改-->
    <style name="mButtonWhite" parent="@style/Widget">
        <item name="android:background">@drawable/button_selector_white</item>
        <item name="android:focusable">true</item>
        <item name="android:clickable">true</item>
        <item name="android:textAppearance">?android:attr/textAppearanceSmallInverse</item>
        <item name="android:gravity">center_vertical|center_horizontal</item>
        <item name="android:textColor">@android:color/primary_text_light</item>
    </style>
    <!--这个对列表样式的修改-->
    <style name="mListView" parent="@style/Widget">
        <item name="android:listSelector">@drawable/list_selector_background</item>
        <item name="android:cacheColorHint">?android:attr/colorBackgroundCacheHint</item>
        <item name="android:divider">@drawable/list_divider</item>
    </style>
    <!--这个对输入框的修改-->
    <style name="mEditText" parent="@style/Widget">
        <item name="android:focusable">true</item>
        <item name="android:focusableInTouchMode">true</item>
        <item name="android:clickable">true</item>
        <item name="android:background">@drawable/input_bg</item>
        <item name="android:textAppearance">?android:attr/textAppearanceMediumInverse</item>
        <item name="android:textColor">@color/gray</item>
        <item name="android:gravity">center_vertical</item>
    </style>

    <!--这个是后来自己添加的 对文本的修改-->
    <style name="mTextView" parent="@style/Widget">
        <!--<item name="android:textColor">@color/red</item>-->
    </style>
    <!--这个对选项框的修改-->
    <style name="mCheckBox" parent="@android:style/Widget.CompoundButton.CheckBox">
        <item name="android:textSize">18sp</item>
        <item name="android:textColor">@color/gray</item>
        <item name="android:paddingLeft">10dip</item>
        <item name="android:button">@drawable/check_box</item>
    </style>


</resources>


```
<h1 id="304">4. themes.xml</h1>

[返回目录](#3)

```
<?xml version="1.0" encoding="utf-8"?>
<resources xmlns:android="http://schemas.android.com/apk/res/android">
	<style name="myTheme" parent="android:Theme">
        <!-- <item name="android:windowBackground">@drawable/start</item> -->
	    <item name="android:windowFullscreen">false</item>  //是否全屏
        <item name="android:windowContentOverlay">@null</item>  <!--定义ActionBar窗体的背景-->
	    <item name="android:windowNoTitle">false</item>  //没有标题
	    <item name="android:windowTitleSize">55dip</item>
	    <item name="android:windowTitleBackgroundStyle">@style/mCustomWindowTitleBackground</item>
		<!--这个的各种常用控件的样式-->
	    <item name="android:expandableListViewStyle">@style/mExpandableListView</item>
	    <item name="android:listViewStyle">@style/mListView</item>
	    <item name="android:buttonStyle">@style/mButtonWhite</item>
	    <item name="android:editTextStyle">@style/mEditText</item>
	    <item name="android:checkboxStyle">@style/mCheckBox</item>
	  <!-- 这个是后来自己添加的-->
	     <item name="android:textViewStyle">@style/mTextView</item>

	    <item name="android:progressBarStyleHorizontal">@style/mProgressBarHorizontal</item>
	    
	    <item name="android:scrollbarSize">15dip</item>
        <item name="android:scrollbarThumbVertical">@drawable/scrollbar_handle_vertical</item>
        <item name="android:scrollbarTrackVertical">@drawable/scrollbar_vertical</item>
	</style>

</resources>

```
<h1 id="305">5. colors.xml</h1>

[返回目录](#3)

```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="red">#FF0000</color>
    <color name="green">#00FF00</color>
    <color name="green_dark">#9CDC6A</color>
    <color name="blue">#33B5E5</color>
    <color name="white">#FFFFFFFF</color>
    <color name="black">#000000</color>
    <color name="gray">#7c7c7c</color>
    <color name="gray_white">#ebebeb</color>
    <color name="gray_light">#887c7c7c</color>
    <color name="gray_dark">#2e2e2e</color>
    <color name="yellow">#FFFC00</color>
    <color name="pink">#FF87EF</color>
    <color name="orange">#ff6200</color>
    <color name="list_divider">#D3D3D3</color>
    <!--这个是透明色-->
    <color name="transparent">#00000000</color>
    <color name="transparent_bg">#88838B8B</color>

</resources>

```
<h1 id="306">6. dimens.xml</h1>

[返回目录](#3)

```
<resources>
    <!-- Default screen margins, per the Android Design guidelines. -->
    <dimen name="activity_horizontal_margin">16dp</dimen>
    <dimen name="activity_vertical_margin">16dp</dimen>

    <!-- slidingmenu配置 -->
    <dimen name="slidingmenu_offset">60dp</dimen>
    <dimen name="shadow_width">16dp</dimen>
</resources>

```
<h1 id="307">7. strings.xml</h1>

[返回目录](#3)

```
<resources>
    <string name="app_name">TanYinQingMyAar</string>

    <string name="hello_world">Hello world!</string>
    <string name="action_settings">Settings</string>
    <string name="copyright">© 2012 amsoft.cn</string>

    <!--登录页面-->
    <string name="rem_pwd">记住密码</string>
    <string name="register">注册</string>
    <string name="login">登录</string>
    <string name="find_pwd">找回密码</string>
    <string name="userPwd">密码</string>
    <string name="userName">用户名</string>
    <string name="im_login">登录</string>
    <string name="error_name_expr">用户名只能是字母和数字</string>
    <string name="error_pwd_expr">密码只能是字母和数字</string>
    <string name="error_name">请输入用户名！</string>
    <string name="error_name_length1">用户名长度不能少于3个字符</string>
    <string name="error_name_length2">用户名长度不能超过20个字符</string>
    <string name="error_pwd">请输入密码！</string>
    <string name="error_pwd_length1">密码长度不能少于6个字符</string>
    <string name="error_pwd_length2">密码长度不能超过20个字符</string>


    <string name="agreement_name">用户注册协议</string>
    <string name="read_desc">请仔细阅读如下条款</string>
    <string name="agreement_desc">\t提醒：本程序是一款Android学习产品，使用本程序即同意如下条款。
        \n1、服务修订
		\n本程序所有者保留随时修改或中断服务而不需通知用户的权利。
		\n2、用户隐私制度
		\n尊重用户个人隐私是本公司的一项基本政策。本公司一定不会在用户不允许的情况下公开、或透露用户的注册资料。
		\n3、用户的帐号、密码和安全性
		\n如果您未保管好自己的帐号和密码而对您或第三方造成的损害，责任由用户个人承担。
		\n4、拒绝提供担保和免责声明
		\n用户明确同意使用本项服务的风险由用户个人承担。服务提供是建立在免费的基础上。本公司不提供任何类型的担保。
		\n5、用户管理
		\n用户单独承担发布内容的责任。用户对服务的使用是根据所有适用于服务的地方法律、国家法律和国际法律标准的。
		\n6、通告
		\n所有发给用户的通告都可通过电子邮件或常规的信件传送。
    </string>

    <string name="user_email">邮箱</string>
    <string name="register_name">新用户注册</string>
    <string name="error_email_expr">邮箱格式不正确!</string>
    <string name="error_email_expr2">邮箱不能输入中文!</string>
    <string name="error_email">请输入邮箱！</string>
    <string name="okBtn">确定</string>
    <string name="about">关于</string>
    <string name="version_lable">程序版本：</string>
    // n是换行符 t是空格
    <string name="about_desc">
      \t\tAndroid开发宝
      \n\t\t又“andBase开发框架”
      andbase是为Android开发者量身打造的一款开源类库产品，
                 您可以在amsoft.cn中获取到最新的代码，示例以及开发文档。
      \n\t\tandbase中包含了大量的开发常用手段，如网络下载，Http请求,线程与线程池的管理，
	      图片缓存管理，图片文件下载上传，数据库ORM框架，并封装了大量常用工具类入如字符串，日期，文件处理，图片处理等，
	      能够使您的应用在团队开发中减少冗余代码，很大的提高了代码的维护性与开发高效性，
	      能很好的规避由于开发疏忽而导致常犯的错误。
	  \n\t\t同时andbase也包含一些常用的控件，如侧边栏，下拉刷新，Tab滑动等，
	      不会使你的程序包变大，却能大幅度缩小您的程序。
	      而这一切都是免费的。
	   \n
       \n\t\t官方主页：www.amsoft.cn
       \n\t\t交流QQ群：38535812
    </string>
    <string name="firm_pwd">确认密码</string>
    <string name="agreement">同意注册协议</string>
    <string name="email">邮箱,用于找回密码</string>
    <string name="error_pwd_match">两次密码输入不一致！</string>
    <string name="error_agreement">请阅读用户协议条款并同意!</string>
    <string name="clear_cache">清空缓存</string>
    <string name="share_desc">分享什么呢</string>
</resources>


```
<h1 id="203">3. MyApplication</h1>

[返回目录](#2)

```
package codewarehouse.yzkj.com.tanyinqingmyaar.andbase.global;

import android.app.Application;
import android.content.Context;
import android.content.SharedPreferences;
import android.content.SharedPreferences.Editor;

import com.ab.global.AbAppConfig;
import com.ab.global.AbConstant;

import codewarehouse.yzkj.com.tanyinqingmyaar.Exception.CrashHandler;
import codewarehouse.yzkj.com.tanyinqingmyaar.andbase.User;


public class MyApplication extends Application {

	// 登录用户
	public User mUser = null;
//默认的城市id和名字
	public String cityid = Constant.DEFAULTCITYID;
	public String cityName = Constant.DEFAULTCITYNAME;
	public boolean userPasswordRemember = false;
	public boolean ad = false;
	public boolean isFirstStart = true;
	public SharedPreferences mSharedPreferences = null;

	@Override
	public void onCreate() {
		super.onCreate();
		//临时数据 初始化
		mSharedPreferences = getSharedPreferences(AbAppConfig.SHARED_PATH,
				Context.MODE_PRIVATE);
		//对登录信息进行初始化
		initLoginParams();
		//这个是对长连接的信息进行初始化
		initIMConfig();

		//将捕捉未知异常的类初始化
		CrashHandler crashHandler = CrashHandler.getInstance();
		crashHandler.init(getApplicationContext());

	}

	/**
	 * 上次登录参数
	 */
	private void initLoginParams() {
		SharedPreferences preferences = getSharedPreferences(
				AbAppConfig.SHARED_PATH, Context.MODE_PRIVATE);
		String userName = preferences.getString(Constant.USERNAMECOOKIE, null);
		String userPwd = preferences.getString(Constant.USERPASSWORDCOOKIE,
				null);
		Boolean userPwdRemember = preferences.getBoolean(
				Constant.USERPASSWORDREMEMBERCOOKIE, false);
		if (userName != null) {
			mUser = new User();
			mUser.setUserName(userName);
			mUser.setPassword(userPwd);
			userPasswordRemember = userPwdRemember;
		}
	}

	//记忆常规登录参数
	public void updateLoginParams(User user) {
		mUser = user;
		if (userPasswordRemember) {
			Editor editor = mSharedPreferences.edit();
			editor.putString(Constant.USERNAMECOOKIE, user.getUserName());
			editor.putString(Constant.USERPASSWORDCOOKIE, user.getPassword());
			editor.putBoolean(Constant.ISFIRSTSTART, false);
			editor.commit();
		} else {
			Editor editor = mSharedPreferences.edit();
			editor.putBoolean(Constant.ISFIRSTSTART, false);
			editor.commit();
		}
		isFirstStart = false;
	}

	/**
	 * 清空上次登录参数
	 */
	public void clearLoginParams() {
		Editor editor = mSharedPreferences.edit();
		editor.clear();
		editor.commit();
		mUser = null;
	}

	/**
	 * IM配置  这个是对长连接的信息进行初始化
	 */
	public void initIMConfig() {
	 /*   IMConfig mIMConfig = new IMConfig();

	    mIMConfig.setXmppHost(mSharedPreferences.getString(
				IMConstant.XMPP_HOST,
				getResources().getString(R.string.xmpp_host)));

	    mIMConfig.setXmppPort(mSharedPreferences.getInt(
				IMConstant.XMPP_PORT,
				getResources().getInteger(R.integer.xmpp_port)));

	    mIMConfig.setXmppServiceName(mSharedPreferences.getString(
				IMConstant.XMPP_SEIVICE_NAME,
				getResources().getString(R.string.xmpp_service_name)));

	    mIMConfig.setNovisible(mSharedPreferences.getBoolean(
				IMConstant.IS_NOVISIBLE,
				getResources().getBoolean(R.bool.is_novisible)));
		
		IMUtil.setIMConfig(this.getApplicationContext(),mIMConfig);*/
		
	}
	
	@Override
	public void onTerminate() {
		super.onTerminate();
	}

}


```
<h1 id="204">4. Constant</h1>

[返回目录](#2)

```
package codewarehouse.yzkj.com.tanyinqingmyaar.andbase.global;



public class Constant {

	public static final Boolean CeShiBanKai =true;//正式版为 false   测试版为 true
	
	public static final boolean DEBUG = true;
	public static final String sharePath = "andbase_share";
    public static final String USERSID = "user";
    //页面默认显示南京，登陆后显示注册用户的城市
    public static final String CITYID = "cityId";
    public static final String CITYNAME = "cityName";
    public static final String DEFAULTCITYID = "1001";//默认城市id
    public static final String DEFAULTCITYNAME = "南京";//默认城市名字
    
    //cookies
    public static final String USERNAMECOOKIE = "cookieName";
    public static final String USERPASSWORDCOOKIE = "cookiePassword";
    public static final String USERPASSWORDREMEMBERCOOKIE = "cookieRemember";
    public static final String ISFIRSTSTART = "isfirstStart";
    
    // 连接超时
 	public static final int timeOut = 12000;
 	// 建立连接
 	public static final int connectOut = 12000;
 	// 获取数据
 	public static final int getOut = 60000;
 	
 	//1表示已下载完成
 	public static final int downloadComplete = 1;
 	//1表示未开始下载
 	public static final int undownLoad = 0;
 	//2表示已开始下载
 	public static final int downInProgress = 2;
 	//3表示下载暂停
 	public static final int downLoadPause = 3;
 	
 	public static final String BASEURL = "http://www.amsoft.cn/";

 	//应用的key
 	//1512528
 	public final static String APPID = "1512528";
 		
 	//jfa97P4HIhjxrAgfUdq1NoKC
 	public final static String APIKEY = "jfa97P4HIhjxrAgfUdq1NoKC";
 	
    
}


```
<h1 id="301">1. 资源的引用</h1>

[返回目录](#3)

```
android:theme="@style/myTheme"

```
<h1 id="301">1. 资源的引用</h1>

[返回目录](#3)

```
android:theme="@style/myTheme"

```
<h1 id="301">1. 资源的引用</h1>

[返回目录](#3)

```
android:theme="@style/myTheme"

```