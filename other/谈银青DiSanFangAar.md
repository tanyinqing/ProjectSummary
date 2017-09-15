 # 2017 06 09
[文档地址](http://pan.baidu.com/disk/home?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&#list/vmode=list&path=%2F%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6%E5%A4%B9%2F%E5%AE%89%E5%8D%93%E9%A1%B9%E7%9B%AE%E4%BB%A3%E7%A0%81%E4%BB%93%E5%BA%93%2FMarkDown%E5%BC%80%E5%8F%91%E6%96%87%E6%A1%A3 "查看") —— [源文件相关](http://pan.baidu.com/disk/home?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&#list/vmode=list&path=%2F%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6%E5%A4%B9%2F%E9%A1%B9%E7%9B%AE%E6%A8%A1%E5%9D%97%2F%E7%AC%AC%E4%B8%89%E6%96%B9%E7%9A%84demo "查看") ——  [个人首页](https://tanyinqing.github.io/)

* ### 创建  <h1 id="1"></h1> 
* ### 高德地图→[高德定位说明与链接](#101)→[高德定位demo说明](#102)
* ### 第三方的demo →[3. ](#103)→[4. ](#104)

参考文档
[订单](5%9D%97 "查看")

<h1 id="101">1. 说明与链接</h1>

[返回目录](#1)

[高德demo的源码地址](http://pan.baidu.com/disk/home?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&#list/vmode=list&path=%2F%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6%E5%A4%B9%2F%E9%A1%B9%E7%9B%AE%E6%A8%A1%E5%9D%97%2F%E7%AC%AC%E4%B8%89%E6%96%B9%E7%9A%84demo%2F%E9%AB%98%E5%BE%B7%E5%9C%B0%E5%9B%BE)
这个软件不要加载任何的图片类的信息，占位置太大，这个只包括最基本的信息。
[开发指南](http://lbs.amap.com/api)→[控制台](http://lbs.amap.com/dev/key/app)

获取SHA1值
通过Android Studio编译器获取SHA1
第一步、打开Android Studio的Terminal工具
第二步、输入命令：keytool -v -list -keystore keystore文件路径
本文件：keytool -v -list -keystore C:\android-sdk\.android\debug.keystore
第三步、输入Keystore密码
默认密码为：android
别名: androiddebugkey   
这个是studio绑定的

  SHA1: F9:A3:38:79:A7:F4:1A:59:9B:FA:C9:FF:24:08:5B:95:BD:39:45:04

通过exlipse获取SHA1
Windows：依次在 eclipse 中打开 Window -> Preferances -> Android -> Build。
在用studio的编译器获得
keytool -v -list -keystore D:\workspace\wechat_sdk_sample_android\debug.keystore

     SHA1: 81:77:2C:60:0F:16:8D:6F:9C:B3:9B:C3:2C:83:74:18:F3:7E:35:13

定位失败：key错误。引用key绑定的debug.keystore错误，exlipse绑定的是自定义的debug.keystore。而不是默认的


获得key
首先，绝大多数App在调试时使用的签名文件（debug keystore）和最终App发布使用的签名文件（自定义的keystore）是不同的，不同签名文件的SHA1值也是不同的。下面提供几种获取SHA1值的方式：

输入发布版安全码  SHA1、调试版安全码 SHA1、以及 Package，

项目的 “AndroidManifest.xml” 文件中，添加如下代码：
XML
```
<application
         android:icon="@drawable/icon"
         android:label="@string/app_name" >        
 		<!--集成地图的账号-->
        <meta-data
            android:name="com.amap.api.v2.apikey"
            android:value="21cd04c0996abbd371a0e45f332c0c" />         
</application>

```
[图解如何获得key](http://lbs.amap.com/faq/top/hot-questions/249)

请在application标签中声明service组件,每个app拥有自己单独的定位service。

集成高德包含的库文件 14.1M
AMap_Location_V3.5.0_20170731.jar
Android_Map3D_SDK_V5.2.1_20170630.jar
arm64-v8a文件夹下
libGNaviData.so 
libGNaviMap.so
libGNaviMapex.so
libGNaviSearch.so
libGNaviUtils.so
libRoadLineRebuildAPI.so
armeabi文件夹
libGNaviData.so
libGNaviMap.so
libGNaviMapex.so
libGNaviSearch.so
libGNaviUtils.so
libRoadLineRebuildAPI.so
armeabi-v7a 文件夹
libGNaviData.so
libGNaviMap.so
libGNaviMapex.so
libGNaviSearch.so
libGNaviUtils.so
libRoadLineRebuildAPI.so
x86文件夹
libGNaviData.so
libGNaviMap.so
libGNaviMapex.so
libGNaviSearch.so
libGNaviUtils.so
libRoadLineRebuildAPI.so
x86_64 文件夹
libGNaviData.so
libGNaviMap.so
libGNaviMapex.so
libGNaviSearch.so
libGNaviUtils.so
libRoadLineRebuildAPI.so

<h1 id="102">2. 高德定位demo说明</h1>

[返回目录](#1)

D:\workspace\AMapLocationDemo

<h1 id="102.00">内部各页面的写法</h1>

[定位功能展示首页面](#102.01)
[获取定位数据页面](#102.02)
[H5辅助定位页面](#102.03)
[错误码说明页面](#102.04)
[定时唤起CPU页面](#102_05)

设置key和服务和Activity
```
 <!-- 设置key -->
        <meta-data
            android:name="com.amap.api.v2.apikey"
            android:value="3e63408136607f6e4e8053b2844e9403" />
		<!-- 定位需要的服务 -->
        <service android:name="com.amap.api.location.APSService" >
        </service>
        
        <activity
            android:name="com.amap.location.demo.StartActivity"
            android:label="@string/app_name"
            android:configChanges="keyboardHidden|orientation|screenSize"
             >
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <activity
            android:name="com.amap.location.demo.Location_Activity"
            android:windowSoftInputMode="adjustResize|stateHidden"
            android:configChanges="keyboardHidden|orientation|screenSize"
            >
        </activity>
```
需要的权限
```
<!-- Normal Permissions 不需要运行时注册 -->
    <!--获取运营商信息，用于支持提供运营商信息相关的接口-->
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <!--用于访问wifi网络信息，wifi信息会用于进行网络定位-->
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <!--这个权限用于获取wifi的获取权限，wifi信息会用来进行网络定位-->
    <uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
    <uses-permission android:name="android.permission.CHANGE_CONFIGURATION" />
    
    <!-- 请求网络 -->
    <uses-permission android:name="android.permission.INTERNET" />
    
    <!-- 不是SDK需要的权限，是示例中的后台唤醒定位需要的权限 -->
    <uses-permission android:name="android.permission.WAKE_LOCK" />
    
   
    
    <!-- 需要运行时注册的权限 -->
    <!--用于进行网络定位-->
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <!--用于访问GPS定位-->
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <!--用于提高GPS定位速度-->
    <uses-permission android:name="android.permission.ACCESS_LOCATION_EXTRA_COMMANDS" />
    <!--写入扩展存储，向扩展卡写入数据，用于写入缓存定位数据-->
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
     <!--读取缓存数据-->
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    
    <!--用于读取手机当前的状态-->
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    
    <!-- 更改设置 -->
    <uses-permission android:name="android.permission.WRITE_SETTINGS" />
    
    <!-- 3.2.0版本增加 -->
    <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
    <!-- 3.2.0版本增加-->
    <uses-permission android:name="android.permission.BLUETOOTH" />
```
<h1 id="102.01">1. 定位功能展示首页面</h1>

[返回目录](#102.00)

![](http://i.imgur.com/UNMMhhm.png)

xml布局
```
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/container"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    >
    <ListView
        android:id="@android:id/list"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1" />
</LinearLayout>
```
适配的布局
```
<?xml version="1.0" encoding="utf-8"?>

<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
  android:layout_width="match_parent"
  android:layout_height="wrap_content"
  android:layout_margin="5dp"
  android:layout_weight="1"
  android:orientation="vertical">
  <TextView
    android:id="@+id/title"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:textSize="20sp"/>
  <TextView
    android:id="@+id/description"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:textSize="16sp"/>
</LinearLayout>

```
代码实现
```
package com.amap.location.demo;

import com.amap.location.demo.view.FeatureView;

import android.app.ListActivity;
import android.content.Context;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ArrayAdapter;
import android.widget.ListAdapter;
import android.widget.ListView;

/**
 * 高德定位SDK功能接口实例 更多SDK请进入官网“http://lbs.amap.com/api/”查看
 * 官方论坛：http://lbsbbs.amap.com/portal.php
 *
 * @项目名称： AMapLocationDemo2.x
 * 
 * @author hongming.wang
 * @文件名称: StartActivity.java
 * @类型名称: StartActivity
 */
public class StartActivity extends ListActivity {
	//这个是内部类
	private static class DemoDetails {
		private final int titleId;
		private final int descriptionId;
		private final Class<? extends android.app.Activity> activityClass;
		public DemoDetails(int titleId, int descriptionId,
				Class<? extends android.app.Activity> activityClass) {
			super();
			this.titleId = titleId;
			this.descriptionId = descriptionId;
			this.activityClass = activityClass;
		}
	}
//这个是内部适配器
	private static class CustomArrayAdapter extends ArrayAdapter<DemoDetails> {
		public CustomArrayAdapter(Context context, DemoDetails[] demos) {
			super(context, R.layout.feature, R.id.title, demos);
		}

		@Override
		public View getView(int position, View convertView, ViewGroup parent) {
			FeatureView featureView;
			if (convertView instanceof FeatureView) {
				featureView = (FeatureView) convertView;
			} else {
				featureView = new FeatureView(getContext());
			}
			DemoDetails demo = getItem(position);
			featureView.setTitleId(demo.titleId);
			featureView.setDescriptionId(demo.descriptionId);
			return featureView;
		}
	}
//这个是内部类对应的数组 是声明的变量
	private static final DemoDetails[] demos = {
			new DemoDetails(R.string.location,
					R.string.location_dec, Location_Activity.class),
			new DemoDetails(R.string.geoFence, R.string.geoFence_dec,
					GeoFence_Activity.class),
			new DemoDetails(R.string.assistantLocation,
					R.string.assistantLocation_dec,
					Assistant_Location_Activity.class),
			new DemoDetails(R.string.tools, R.string.tools_dec,
					Tools_Activity.class),
			new DemoDetails(R.string.lastLocation, R.string.lastLocation_dec,
					LastLocation_Activity.class),
			new DemoDetails(R.string.alarmCPU, R.string.alarmCPU_dec,
					Alarm_Location_Activity.class),
			new DemoDetails(R.string.errorCode, R.string.errorCode_dec,
					ErrorCode_Activity.class),
			};

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_start);
		/**
		 * setApiKey必须在启动Activity或者Application的onCreate里进行， 在其他地方使用有可能无效,
		 * 如果使用setApiKey设置key，则AndroidManifest.xml里的key会失效
		 */
		// AMapLocationClient.setApiKey("需要更换的key");

		setTitle(R.string.title_main);
		ListAdapter adapter = new CustomArrayAdapter(
				this.getApplicationContext(), demos);
		setListAdapter(adapter);
//		permChecker = new PermissionsChecker(this);
	}

	@Override
	public void onBackPressed() {
		super.onBackPressed();
		System.exit(0);
	}

	@Override
	protected void onListItemClick(ListView l, View v, int position, long id) {
		DemoDetails demo = (DemoDetails) getListAdapter().getItem(position);
		startActivity(
				new Intent(this.getApplicationContext(), demo.activityClass));
	}

}

```

<h1 id="102.02">2. 获取定位数据页面</h1>

[返回目录](#102.00)

![](http://i.imgur.com/c5JiZfG.png)

xml页面
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical" >
	<!-- 单选项 -->
    <RadioGroup
        android:id="@+id/rg_locationMode"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal" >

        <RadioButton
            android:id="@+id/rb_batterySaving"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="@string/battery_saving" />

        <RadioButton
            android:id="@+id/rb_deviceSensors"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="@string/device_sensors" />

        <RadioButton
            android:id="@+id/rb_hightAccuracy"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:checked="true"
            android:text="@string/hight_accuracy" />
    </RadioGroup>
<!-- 两个输入框 -->
    <LinearLayout
        android:id="@+id/layout_interval"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="@dimen/normal_margin" >

        <TextView
            android:id="@+id/tv_info"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/interval" />

        <EditText
            android:id="@+id/et_interval"
            android:layout_width="130dp"
            android:layout_height="wrap_content"
            android:layout_marginLeft="@dimen/margin_middle"
            android:ems="10"
            android:hint="@string/defaultInteval"
            android:inputType="number" >

            <requestFocus />
        </EditText>
    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content" >

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/httpTimeout" />

        <EditText
            android:id="@+id/et_httpTimeout"
            android:layout_width="130dp"
            android:layout_height="wrap_content"
            android:layout_marginLeft="@dimen/margin_middle"
            android:ems="10"
            android:hint="@string/defaultHttpTimeout"
            android:inputType="number" >

            <requestFocus />
        </EditText>
    </LinearLayout>
<!-- 三个选择框 -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center_vertical"
        android:orientation="horizontal" >

        <CheckBox
            android:id="@+id/cb_onceLocation"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/location_once" />

        <CheckBox
            android:id="@+id/cb_gpsFirst"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/gpsFirst" />
    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center_vertical"
        android:orientation="horizontal" >

        <CheckBox
            android:id="@+id/cb_needAddress"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:checked="true"
            android:text="@string/needAddress" />

        <CheckBox
            android:id="@+id/cb_cacheAble"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:checked="true"
            android:text="@string/cacheAble" />
    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center_vertical"
        android:orientation="horizontal" >

        <CheckBox
            android:id="@+id/cb_onceLastest"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/onceLastest" />
        <CheckBox
            android:id="@+id/cb_sensorAble"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/useSensor" />
    </LinearLayout>

</LinearLayout>
```
以上是引用的xml 以下是下半部分
```
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="@dimen/normal_margin" >
<!-- 这个是上面的部分 -->
    <include layout="@layout/plugin_location_option"/>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center" >

        <Button
            android:id="@+id/bt_location"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/startLocation" />
    </LinearLayout>
<!-- 这个是用来显示详细的信息 -->
    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent" >

        <TextView
            android:id="@+id/tv_result"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="@dimen/normal_margin" />
    </ScrollView>

</LinearLayout>
```

定位类型对照表

定位成功，定位回调将按照定位结果返回如下几种响应码，用于区分本次定位的来源：
响应码
说明
介绍
0
定位失败
请通过AMapLocation.getErrorCode()方法获取错误码，并参考错误码对照表进行问题排查。
1
GPS定位结果
通过设备GPS定位模块返回的定位结果，精度较高，在10米－100米左右
2
前次定位结果
网络定位请求低于1秒、或两次定位之间设备位置变化非常小时返回，设备位移通过传感器感知。
4
缓存定位结果
返回一段时间前设备在同样的位置缓存下来的网络定位结果
5
Wifi定位结果
属于网络定位，定位精度相对基站定位会更好，定位精度较高，在5米－200米之间。
6
基站定位结果
纯粹依赖移动、联通、电信等移动网络定位，定位精度在500米-5000米之间。
8
离线定位结果

实现的代码
```
package com.amap.location.demo;

import com.amap.api.location.AMapLocation;
import com.amap.api.location.AMapLocationClient;
import com.amap.api.location.AMapLocationClientOption;
import com.amap.api.location.AMapLocationClientOption.AMapLocationMode;
import com.amap.api.location.AMapLocationClientOption.AMapLocationProtocol;
import com.amap.api.location.AMapLocationListener;

import android.os.Bundle;
import android.text.TextUtils;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.CompoundButton;
import android.widget.EditText;
import android.widget.RadioGroup;
import android.widget.RadioGroup.OnCheckedChangeListener;
import android.widget.TextView;

/**
 * 高精度定位模式功能演示
 *
 * @创建时间： 2015年11月24日 下午5:22:42
 * @项目名称： AMapLocationDemo2.x
 * @author hongming.wang
 * @文件名称: Hight_Accuracy_Activity.java
 * @类型名称: Hight_Accuracy_Activity
 */
public class Location_Activity extends CheckPermissionsActivity
		implements
			OnCheckedChangeListener,
			OnClickListener{
	private RadioGroup rgLocationMode;
	private EditText etInterval;
	private EditText etHttpTimeout;
	private CheckBox cbOnceLocation;
	private CheckBox cbAddress;
	private CheckBox cbGpsFirst;
	private CheckBox cbCacheAble;
	private CheckBox cbOnceLastest;
	private CheckBox cbSensorAble;
	private TextView tvResult;
	private Button btLocation;
//定位服务类。此类提供单次定位、持续定位、最后位置相关功能。
	private AMapLocationClient locationClient = null;
	//定位参数设置，通过这个类可以对定位的相关参数进行设置 
	private AMapLocationClientOption locationOption = null;

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_location);
		setTitle(R.string.title_location);
//		初始化布局和监听器
		initView();
		
//		初始化定位
		initLocation();
	}
	
	//初始化控件
	private void initView(){
		rgLocationMode = (RadioGroup) findViewById(R.id.rg_locationMode);
		
		etInterval = (EditText) findViewById(R.id.et_interval);
		etHttpTimeout = (EditText) findViewById(R.id.et_httpTimeout);
		
		cbOnceLocation = (CheckBox)findViewById(R.id.cb_onceLocation);
		cbGpsFirst = (CheckBox) findViewById(R.id.cb_gpsFirst);
		cbAddress = (CheckBox) findViewById(R.id.cb_needAddress);
		cbCacheAble = (CheckBox) findViewById(R.id.cb_cacheAble);
		cbOnceLastest = (CheckBox) findViewById(R.id.cb_onceLastest);
		cbSensorAble = (CheckBox)findViewById(R.id.cb_sensorAble);

		tvResult = (TextView) findViewById(R.id.tv_result);
		btLocation = (Button) findViewById(R.id.bt_location);
		
		rgLocationMode.setOnCheckedChangeListener(this);
		btLocation.setOnClickListener(this);
	}
	
	@Override
	protected void onDestroy() {
		super.onDestroy();
		destroyLocation();//销毁定位
	}

	@Override
	public void onCheckedChanged(RadioGroup group, int checkedId) {
		if (null == locationOption) {
			locationOption = new AMapLocationClientOption();
		}
//		这个是第一轮单选框
		switch (checkedId) {
			case R.id.rb_batterySaving :
				locationOption.setLocationMode(AMapLocationMode.Battery_Saving);
				break;
			case R.id.rb_deviceSensors :
				locationOption.setLocationMode(AMapLocationMode.Device_Sensors);
				break;
			case R.id.rb_hightAccuracy :
				locationOption.setLocationMode(AMapLocationMode.Hight_Accuracy);
				break;
			default :
				break;
		}

	}

	/**
	 * 设置控件的可用状态
	 * 当开启定位后，所有的状态是不可用的
	 */
	private void setViewEnable(boolean isEnable) {
		for(int i=0; i<rgLocationMode.getChildCount(); i++){
			rgLocationMode.getChildAt(i).setEnabled(isEnable);
		}
		etInterval.setEnabled(isEnable);
		etHttpTimeout.setEnabled(isEnable);
		cbOnceLocation.setEnabled(isEnable);
		cbGpsFirst.setEnabled(isEnable);
		cbAddress.setEnabled(isEnable);
		cbCacheAble.setEnabled(isEnable);
		cbOnceLastest.setEnabled(isEnable);
		cbSensorAble.setEnabled(isEnable);
	}

	@Override //但点击按钮后，对是否正在定位进行判断
	public void onClick(View v) {
		if (v.getId() == R.id.bt_location) {
			if (btLocation.getText().equals(
					getResources().getString(R.string.startLocation))) {
				setViewEnable(false);
				btLocation.setText(getResources().getString(
						R.string.stopLocation));
				tvResult.setText("正在定位...");
				startLocation();
			} else {
				setViewEnable(true);
				btLocation.setText(getResources().getString(
						R.string.startLocation));
				stopLocation();
				tvResult.setText("定位停止");
			}
		}
	}
	
	/**
	 * 初始化定位
	 * 
	 * @since 2.8.0
	 * @author hongming.wang
	 *
	 */
	private void initLocation(){
		//初始化client
		locationClient = new AMapLocationClient(this.getApplicationContext());
		//这个是在初始化时设置定位参数
		locationOption = getDefaultOption();
		//设置定位参数
		locationClient.setLocationOption(locationOption);
		// 设置定位监听
		locationClient.setLocationListener(locationListener);
	}
	
	/**
	 * 默认的定位参数
	 * @since 2.8.0
	 * @author hongming.wang
	 *
	 */
	private AMapLocationClientOption getDefaultOption(){
		AMapLocationClientOption mOption = new AMapLocationClientOption();
		mOption.setLocationMode(AMapLocationMode.Hight_Accuracy);//可选，设置定位模式，可选的模式有高精度、仅设备、仅网络。默认为高精度模式
		mOption.setGpsFirst(false);//可选，设置是否gps优先，只在高精度模式下有效。默认关闭
		mOption.setHttpTimeOut(30000);//可选，设置网络请求超时时间。默认为30秒。在仅设备模式下无效
		mOption.setInterval(2000);//可选，设置定位间隔。默认为2秒
		mOption.setNeedAddress(true);//可选，设置是否返回逆地理地址信息。默认是true
		mOption.setOnceLocation(false);//可选，设置是否单次定位。默认是false
		mOption.setOnceLocationLatest(false);//可选，设置是否等待wifi刷新，默认为false.如果设置为true,会自动变为单次定位，持续定位时不要使用
		AMapLocationClientOption.setLocationProtocol(AMapLocationProtocol.HTTP);//可选， 设置网络请求的协议。可选HTTP或者HTTPS。默认为HTTP
		mOption.setSensorEnable(false);//可选，设置是否使用传感器。默认是false
		mOption.setWifiScan(true); //可选，设置是否开启wifi扫描。默认为true，如果设置为false会同时停止主动刷新，停止以后完全依赖于系统刷新，定位位置可能存在误差
		mOption.setLocationCacheEnable(true); //可选，设置是否使用缓存定位，默认为true
		return mOption;
	}
	
	/**
	 * 定位监听
	 */
	AMapLocationListener locationListener = new AMapLocationListener() {
		@Override
		public void onLocationChanged(AMapLocation location) {
			if (null != location) {

				StringBuffer sb = new StringBuffer();
				//errCode等于0代表定位成功，其他的为定位失败，具体的可以参照官网定位错误码说明
				if(location.getErrorCode() == 0){
					sb.append("定位成功" + "\n");
					sb.append("定位类型: " + location.getLocationType() + "\n");
					sb.append("经    度    : " + location.getLongitude() + "\n");
					sb.append("纬    度    : " + location.getLatitude() + "\n");
					sb.append("精    度    : " + location.getAccuracy() + "米" + "\n");
					sb.append("提供者    : " + location.getProvider() + "\n");

					sb.append("速    度    : " + location.getSpeed() + "米/秒" + "\n");
					sb.append("角    度    : " + location.getBearing() + "\n");
					// 获取当前提供定位服务的卫星个数
					sb.append("星    数    : " + location.getSatellites() + "\n");
					sb.append("国    家    : " + location.getCountry() + "\n");
					sb.append("省            : " + location.getProvince() + "\n");
					sb.append("市            : " + location.getCity() + "\n");
					sb.append("城市编码 : " + location.getCityCode() + "\n");
					sb.append("区            : " + location.getDistrict() + "\n");
					sb.append("区域 码   : " + location.getAdCode() + "\n");
					sb.append("地    址    : " + location.getAddress() + "\n");
					sb.append("兴趣点    : " + location.getPoiName() + "\n");
					//定位完成的时间
					sb.append("定位时间: " + Utils.formatUTC(location.getTime(), "yyyy-MM-dd HH:mm:ss") + "\n");
				} else {
					//定位失败
					sb.append("定位失败" + "\n");
					sb.append("错误码:" + location.getErrorCode() + "\n");
					sb.append("错误信息:" + location.getErrorInfo() + "\n");
					sb.append("错误描述:" + location.getLocationDetail() + "\n");
				}
				//定位之后的回调时间
				sb.append("回调时间: " + Utils.formatUTC(System.currentTimeMillis(), "yyyy-MM-dd HH:mm:ss") + "\n");

				//解析定位结果，
				String result = sb.toString();
				tvResult.setText(result);
			} else {
				tvResult.setText("定位失败，loc is null");
			}
		}
	};
	
	// 根据控件的选择，重新设置定位参数
	private void resetOption() {
		// 设置是否需要显示地址信息
		locationOption.setNeedAddress(cbAddress.isChecked());
		/**
		 * 设置是否优先返回GPS定位结果，如果30秒内GPS没有返回定位结果则进行网络定位
		 * 注意：只有在高精度模式下的单次定位有效，其他方式无效
		 */
		locationOption.setGpsFirst(cbGpsFirst.isChecked());
		// 设置是否开启缓存
		locationOption.setLocationCacheEnable(cbCacheAble.isChecked());
		// 设置是否单次定位
		locationOption.setOnceLocation(cbOnceLocation.isChecked());
		//设置是否等待设备wifi刷新，如果设置为true,会自动变为单次定位，持续定位时不要使用
		locationOption.setOnceLocationLatest(cbOnceLastest.isChecked());
		//设置是否使用传感器
		locationOption.setSensorEnable(cbSensorAble.isChecked());
		//设置是否开启wifi扫描，如果设置为false时同时会停止主动刷新，停止以后完全依赖于系统刷新，定位位置可能存在误差
		//这个是第一个输入框
		String strInterval = etInterval.getText().toString();
		if (!TextUtils.isEmpty(strInterval)) {
			try{
				// 设置发送定位请求的时间间隔,最小值为1000，如果小于1000，按照1000算
				locationOption.setInterval(Long.valueOf(strInterval));
			}catch(Throwable e){
				e.printStackTrace();
			}
		}
		//这个是第二个输入框
		String strTimeout = etHttpTimeout.getText().toString();
		if(!TextUtils.isEmpty(strTimeout)){
			try{
				// 设置网络请求超时时间
			     locationOption.setHttpTimeOut(Long.valueOf(strTimeout));
			}catch(Throwable e){
				e.printStackTrace();
			}
		}
	}

	/**
	 * 开始定位
	 * 
	 * @since 2.8.0
	 * @author hongming.wang
	 *
	 */
	private void startLocation(){
		//根据控件的选择，重新设置定位参数
		resetOption();
		// 设置定位参数
		locationClient.setLocationOption(locationOption);
		// 启动定位
		locationClient.startLocation();
	}
	
	/**
	 * 停止定位
	 * 
	 * @since 2.8.0
	 * @author hongming.wang
	 *
	 */
	private void stopLocation(){
		// 停止定位
		locationClient.stopLocation();
	}
	
	/**
	 * 销毁定位
	 * 
	 * @since 2.8.0
	 * @author hongming.wang
	 *
	 */
	private void destroyLocation(){
		if (null != locationClient) {
			/**
			 * 如果AMapLocationClient是在当前Activity实例化的，
			 * 在Activity的onDestroy中一定要执行AMapLocationClient的onDestroy
			 */
			locationClient.onDestroy();
			locationClient = null;
			locationOption = null;
		}
	}
}

```
<h1 id="102.03">3. H5辅助定位页面</h1>

[返回目录](#102.00)

![](http://i.imgur.com/CXuIJAd.png)

location.html 页面的写法

```
<!doctype html>
<html>
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="initial-scale=1.0, user-scalable=no, width=device-width">
    <title>浏览器定位</title>
    <link rel="stylesheet" href="http://cache.amap.com/lbs/static/main1119.css"/>
    <script type="text/javascript" src="http://webapi.amap.com/maps?v=1.3&key=b5713c7bcc8fe27fad9a40e32a29768d"></script>
    <script type="text/javascript" src="http://cache.amap.com/lbs/static/addToolbar.js"></script>
<body>
<div id='container'></div>
<div id="tip"></div>
<script type="text/javascript">
    var map, geolocation;
    //加载地图，调用浏览器定位服务
    map = new AMap.Map('container', {
        resizeEnable: true
    });
    map.plugin('AMap.Geolocation', function() {
        geolocation = new AMap.Geolocation({
            enableHighAccuracy: true,//是否使用高精度定位，默认:true
            timeout: 10000,          //超过10秒后停止定位，默认：无穷大
            buttonOffset: new AMap.Pixel(10, 20),//定位按钮与设置的停靠位置的偏移量，默认：Pixel(10, 20)
            zoomToAccuracy: true,      //定位成功后调整地图视野范围使定位位置及精度范围视野内可见，默认：false
            buttonPosition:'RB',
            useNative:true
        });
        map.addControl(geolocation);
        geolocation.getCurrentPosition();
        AMap.event.addListener(geolocation, 'complete', onComplete);//返回定位信息
        AMap.event.addListener(geolocation, 'error', onError);      //返回定位出错信息
    });
    //解析定位结果
    function onComplete(data) {
        var str=['定位成功'];
        str.push('经度：' + data.position.getLng());
        str.push('纬度：' + data.position.getLat());
        str.push('精度：' + data.accuracy + ' 米');
        str.push('是否经过偏移：' + (data.isConverted ? '是' : '否'));
        document.getElementById('tip').innerHTML = str.join('<br>');
    }
    //解析定位错误信息
    function onError(data) {
        document.getElementById('tip').innerHTML = '定位失败';
    }
</script>
</body>
</html>
```
定义的xml布局
```
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="@dimen/normal_margin" >

    <LinearLayout
        android:id="@+id/layout_interval"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="@dimen/normal_margin"
        android:orientation="vertical" 
        android:gravity="center">
<!-- 为的是让一个控件集中显示 -->
        <Button
            android:id="@+id/bt_assistant"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/startAssistantLocation" />

    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="@dimen/normal_margin"
        android:gravity="center" >

        <Button
            android:id="@+id/bt_location"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/urlLocation"
            android:enabled="false" />

    </LinearLayout>
     <WebView
        android:id="@+id/webView"
        android:visibility="gone"
        android:layout_marginTop="@dimen/normal_margin"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
       /> 
</LinearLayout>
```
代码实现的过程
```
package com.amap.location.demo;

import com.amap.api.location.AMapLocationClient;

import android.app.Activity;
import android.graphics.Bitmap;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.view.Window;
import android.webkit.GeolocationPermissions.Callback;
import android.webkit.JsResult;
import android.webkit.WebChromeClient;
import android.webkit.WebSettings;
import android.webkit.WebView;
import android.webkit.WebViewClient;
import android.widget.Button;

/**
 * H5辅助定位模式功能演示
 *
 * @创建时间： 2015年11月24日 下午4:24:07 
 * @项目名称： AMapLocationDemo2.x
 * 
 * @author hongming.wang
 * @文件名称: Battery_Saving_Activity.java
 * @类型名称: Battery_Saving_Activity
 */
public class Assistant_Location_Activity extends CheckPermissionsActivity implements OnClickListener {
	private Button btAssistant;
	private Button btLocation;

	private AMapLocationClient locationClient = null;

	private WebView webView;
	
	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_assistant_location);
		setTitle(R.string.title_assistantLocation);

		btAssistant = (Button) findViewById(R.id.bt_assistant);
		btLocation = (Button) findViewById(R.id.bt_location);

		locationClient = new AMapLocationClient(getApplicationContext());
		btAssistant.setOnClickListener(this);
		btLocation.setOnClickListener(this);

		initWebView();
	}

	private void initWebView(){
		webView = (WebView) findViewById(R.id.webView);
		
		WebSettings webSettings = webView.getSettings();
		// 允许webview执行javaScript脚本
		webSettings.setJavaScriptEnabled(true);
		// 设置是否允许定位，这里为了使用H5辅助定位，设置为false。
	    //设置为true不一定会进行H5辅助定位，设置为true时只有H5定位失败后才会进行辅助定位
		webSettings.setGeolocationEnabled(false);
		
		
		webView.setWebViewClient(new WebViewClient() {
			
			public void onPageFinished(WebView view, String url) {
				super.onPageFinished(view, url);
			}

			public void onPageStarted(WebView view, String url, Bitmap favicon) {
				super.onPageStarted(view, url, favicon);
			}
		});

		webView.setWebChromeClient(new WebChromeClient() {
			// 处理javascript中的alert
			public boolean onJsAlert(WebView view, String url, String message,
					final JsResult result) {
				return true;
			};

			// 处理javascript中的confirm
			public boolean onJsConfirm(WebView view, String url,
					String message, final JsResult result) {
				return true;
			};

			// 处理定位权限请求
			@Override
			public void onGeolocationPermissionsShowPrompt(String origin,
					Callback callback) {
				callback.invoke(origin, true, false); 
				super.onGeolocationPermissionsShowPrompt(origin, callback);
			}
			@Override
			// 设置网页加载的进度条
			public void onProgressChanged(WebView view, int newProgress) {
				Assistant_Location_Activity.this.getWindow().setFeatureInt(
						Window.FEATURE_PROGRESS, newProgress * 100);
				super.onProgressChanged(view, newProgress);
			}

			// 设置应用程序的标题title
			public void onReceivedTitle(WebView view, String title) {
				super.onReceivedTitle(view, title);
			}
		});
	}
	
	@Override
	protected void onDestroy() {
		super.onDestroy();
		if (null != locationClient) {
			locationClient.stopAssistantLocation();
			locationClient.onDestroy();
		}
		if(null != webView){
			webView.destroy();
		}
	}
	
	@Override
	public void onClick(View v) {
		if (v.getId() == R.id.bt_assistant) {
			if (btAssistant.getText().equals(getResources().getString(R.string.startAssistantLocation))) {
				btAssistant.setText(getResources().getString(R.string.stopAssistantLocation));
				locationClient.startAssistantLocation();
				btLocation.setEnabled(true);
			} else {
				btAssistant.setText(getResources().getString(R.string.startAssistantLocation));
				locationClient.stopAssistantLocation();
				btLocation.setEnabled(false);
				webView.setVisibility(View.GONE);
			}
		} else if (v.getId() == R.id.bt_location) {
			webView.setVisibility(View.VISIBLE);
			//浏览器定位，加载预置的H5定位页面
//			public final static String URL_H5LOCATION = "file:///android_asset/location.html";
			webView.loadUrl(Utils.URL_H5LOCATION);
		}
	}
}

```
<h1 id="102.04">4. 错误码说明页面</h1>

[返回目录](#102.00)

xml和页面文字的格式
```
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="@dimen/normal_margin" >
    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent" 
        android:layout_marginTop="5dp">

        <TextView
            android:id="@+id/tv_errinfo"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="@string/errorCodeInfo"
            android:textSize="@dimen/font_34"
            android:layout_marginTop="@dimen/normal_margin" />
    </ScrollView>

</LinearLayout>


<string name="errorCodeInfo">
	    0	定位成功。	可以在定位回调里判断定位返回成功后再进行业务逻辑运算\n
	    1	一些重要参数为空，如context；	请对定位传递的参数进行非空判断\n
	    2	定位失败，由于仅扫描到单个wifi，且没有基站信息。	请重新尝试\n
	    3	获取到的请求参数为空，可能获取过程中出现异常。	请对所连接网络进行全面检查，请求可能被篡改\n
	    4	请求服务器过程中的异常，多为网络情况差，链路不通导致	请检查设备网络是否通畅\n
	    5	返回的XML格式错误，解析失败。	请稍后再试\n
	    6	定位服务返回定位失败。	请将errorDetail（通过getLocationDetail()方法获取）信息通过工单系统反馈给我们\n
	    7	KEY鉴权失败。	请仔细检查key绑定的sha1值与apk签名sha1值是否对应，或通过高频问题查找相关解决办法\n
	    8	Android exception常规错误	请将errordetail（通过getLocationDetail()方法获取）信息通过工单系统反馈给我们\n
	    9	定位初始化时出现异常。	请重新启动定位\n
	    10	定位客户端启动失败。	请检查AndroidManifest.xml文件是否配置了APSService定位服务\n
	    11	定位时的基站信息错误。	请检查是否安装SIM卡，设备很有可能连入了伪基站网络\n
	    12	缺少定位权限。	请在设备的设置中开启app的定位权限\n
	    13	定位失败，由于设备未开启WIFI模块或未插入SIM卡，且GPS当前不可用。 建议开启设备的WIFI模块，并将设备中插入一张可以正常工作的SIM卡，或者检查GPS是否开启；如果以上都内容都确认无误，请您检查App是否被授予定位权限\n
	    14  GPS 定位失败，由于设备当前 GPS 状态差。 建议持设备到相对开阔的露天场所再次尝试\n
	    15	定位结果被模拟导致定位失败。 如果您希望位置被模拟，请通过setMockEnable(true);方法开启允许位置模拟\n
	    16 	当前POI检索条件、行政区划检索条件下，无可用地理围栏。 建议调整检索条件后重新尝试，例如调整POI关键字，调整POI类型，调整周边搜区域，调整行政区关键字等\n
	    17 	相同的地理围栏已经存在，无需重复添加\n
	    18	飞行模式下关闭了WIFI开关，请关闭飞行模式或者打开WIFI开关\n
	    19	没有检查到SIM卡，并且关闭了WIFI开关，请打开WIFI开关或者插入SIM卡\n
	</string>
```
<h1 id="102_05">5. 定时唤起CPU页面</h1>

[返回目录](#102.00)

![](http://i.imgur.com/DXggscn.png)
#知识要点
1 利用 Handler Message进行消息的传递
```
Handler mHandler = new Handler() {
		public void dispatchMessage(android.os.Message msg) {
			switch (msg.what) {
			//开始定位
			case Utils.MSG_LOCATION_START:
				tvReult.setText("正在定位...");
				break;
			// 定位完成
			case Utils.MSG_LOCATION_FINISH:
				AMapLocation loc = (AMapLocation) msg.obj;
				//对地址的信息进行分解
				String result = Utils.getLocationStr(loc);
				tvReult.setText(result);
				break;
			//停止定位
			case Utils.MSG_LOCATION_STOP:
				tvReult.setText("定位停止");
				break;
			default:
				break;
			}
		};
	};

// 定位监听回调的函数中发信息
	@Override
	public void onLocationChanged(AMapLocation loc) {
		if (null != loc) {
			//消息携带一个内部对象
			Message msg = mHandler.obtainMessage();
			msg.obj = loc;
			msg.what = Utils.MSG_LOCATION_FINISH;
			mHandler.sendMessage(msg);
		}
	}
```
2 利用内部的广播进行监听
```
//内部自定义的广播接收器
	private BroadcastReceiver alarmReceiver = new BroadcastReceiver(){
		@Override
		public void onReceive(Context context, Intent intent) {
			if(intent.getAction().equals("LOCATION")){
				if(null != locationClient){
					locationClient.startLocation();
				}
			}
		}
	};

//		注销广播接收器
		if(null != alarmReceiver){
			unregisterReceiver(alarmReceiver);
			alarmReceiver = null;
		}

//动态注册一个广播
		IntentFilter filter = new IntentFilter();
		filter.addAction("LOCATION");
		registerReceiver(alarmReceiver, filter);
```
3 周期性启动事件
```
//这个中包含一个意图，携带一个动作LOCATION  专门有广播会接受这个动作
private Intent alarmIntent = null;
//对意图进行包装 意味着将来去做什么事
	private PendingIntent alarmPi = null;
//系统级的定时器 意味着将来去发送这个意图
	private AlarmManager alarm = null;

// 创建Intent对象，action为LOCATION
		alarmIntent = new Intent();
		alarmIntent.setAction("LOCATION");
// 定义一个PendingIntent对象，PendingIntent.getBroadcast包含了sendBroadcast的动作。
		// 也就是发送了action 为"LOCATION"的intent
		alarmPi = PendingIntent.getBroadcast(this, 0, alarmIntent, 0);
		// AlarmManager对象,注意这里并不是new一个对象，Alarmmanager为系统级服务
		alarm = (AlarmManager) getSystemService(ALARM_SERVICE);


if(null != alarm){
					//设置一个闹钟，2秒之后每隔一段时间执行启动一次定位程序
					alarm.setRepeating(AlarmManager.ELAPSED_REALTIME_WAKEUP, SystemClock.elapsedRealtime() + 2*1000,
							alarmInterval * 1000, alarmPi);
				}
```
把定位返回的对象解析成字符串
```
/**
	 * 根据定位结果返回定位信息的字符串
	 * @param location
	 * @return
	 */
	public synchronized static String getLocationStr(AMapLocation location){
		if(null == location){
			return null;
		}
		StringBuffer sb = new StringBuffer();
		//errCode等于0代表定位成功，其他的为定位失败，具体的可以参照官网定位错误码说明
		if(location.getErrorCode() == 0){
			sb.append("定位成功" + "\n");
			sb.append("定位类型: " + location.getLocationType() + "\n");
			sb.append("经    度    : " + location.getLongitude() + "\n");
			sb.append("纬    度    : " + location.getLatitude() + "\n");
			sb.append("精    度    : " + location.getAccuracy() + "米" + "\n");
			sb.append("提供者    : " + location.getProvider() + "\n");

			sb.append("速    度    : " + location.getSpeed() + "米/秒" + "\n");
			sb.append("角    度    : " + location.getBearing() + "\n");
			// 获取当前提供定位服务的卫星个数
			sb.append("星    数    : " + location.getSatellites() + "\n");
			sb.append("国    家    : " + location.getCountry() + "\n");
			sb.append("省            : " + location.getProvince() + "\n");
			sb.append("市            : " + location.getCity() + "\n");
			sb.append("城市编码 : " + location.getCityCode() + "\n");
			sb.append("区            : " + location.getDistrict() + "\n");
			sb.append("区域 码   : " + location.getAdCode() + "\n");
			sb.append("地    址    : " + location.getAddress() + "\n");
			sb.append("兴趣点    : " + location.getPoiName() + "\n");
			//定位完成的时间
			sb.append("定位时间: " + formatUTC(location.getTime(), "yyyy-MM-dd HH:mm:ss") + "\n");
		} else {
			//定位失败
			sb.append("定位失败" + "\n");
			sb.append("错误码:" + location.getErrorCode() + "\n");
			sb.append("错误信息:" + location.getErrorInfo() + "\n");
			sb.append("错误描述:" + location.getLocationDetail() + "\n");
		}
		//定位之后的回调时间
		sb.append("回调时间: " + formatUTC(System.currentTimeMillis(), "yyyy-MM-dd HH:mm:ss") + "\n");
		return sb.toString();
	}

```
xml布局
```
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="@dimen/normal_margin" >
<!-- 两个输入框 -->
    <LinearLayout
        android:id="@+id/layout_interval"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="@dimen/normal_margin" >

        <TextView
            android:id="@+id/tv_info"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/interval" />

        <EditText
            android:id="@+id/et_interval"
            android:layout_width="130dp"
            android:layout_height="wrap_content"
            android:layout_marginLeft="@dimen/margin_middle"
            android:ems="10"
            android:hint="@string/defaultInteval"
            android:inputType="number" >

            <requestFocus />
        </EditText>

    </LinearLayout>
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="@dimen/normal_margin" >

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/alarmInterval" />

        <EditText
            android:id="@+id/et_alarm"
            android:layout_width="130dp"
            android:layout_height="wrap_content"
            android:layout_marginLeft="@dimen/margin_middle"
            android:ems="10"
            android:hint="5"
            android:inputType="number" >
            <requestFocus />
        </EditText>
    </LinearLayout>
<!-- 一个选项框 -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="@dimen/normal_margin" >

        <CheckBox
            android:id="@+id/cb_needAddress"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:checked="true"
            android:text="@string/needAddress" />

        <CheckBox
            android:id="@+id/cb_gpsFirst"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/gpsFirst"
            android:visibility="gone" />
    </LinearLayout>
<!-- 开始定位 -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center" >

        <Button
            android:id="@+id/bt_location"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/startLocation" />
    </LinearLayout>

    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent" >

        <TextView
            android:id="@+id/tv_result"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="@dimen/normal_margin" />
    </ScrollView>

</LinearLayout>
```
代码进行实现
```
package com.amap.location.demo;

import com.amap.api.location.AMapLocation;
import com.amap.api.location.AMapLocationClient;
import com.amap.api.location.AMapLocationClientOption;
import com.amap.api.location.AMapLocationClientOption.AMapLocationMode;
import com.amap.api.location.AMapLocationListener;

import android.app.Activity;
import android.app.AlarmManager;
import android.app.PendingIntent;
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.content.IntentFilter;
import android.os.Bundle;
import android.os.Handler;
import android.os.Message;
import android.os.SystemClock;
import android.text.TextUtils;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

/**
 * 后台唤醒定位
 * @创建时间：2016年1月8日 上午11:25:01
 * @项目名称： AMapLocationDemo2.x 
 * @author hongming.wang
 * @文件名称：Alarm_Location_Activity.java
 * @类型名称：Alarm_Location_Activity
 * @since 2.3.0
 */
public class Alarm_Location_Activity extends CheckPermissionsActivity implements
		 OnClickListener, AMapLocationListener {
	private EditText etInterval;
	private EditText etAlarm;
	private CheckBox cbAddress;
	private CheckBox cbGpsFirst;
	private TextView tvReult;
	private Button btLocation;
	//定位服务类。此类提供单次定位、持续定位、最后位置相关功能。
	private AMapLocationClient locationClient = null;
	//定位参数设置，通过这个类可以对定位的相关参数进行设置 
	private AMapLocationClientOption locationOption = null;
	
	private Intent alarmIntent = null;
	private PendingIntent alarmPi = null;
	private AlarmManager alarm = null;

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_alarm_location);
		setTitle(R.string.title_alarmCPU);

		etInterval = (EditText) findViewById(R.id.et_interval);
		etAlarm = (EditText) findViewById(R.id.et_alarm);
		cbAddress = (CheckBox) findViewById(R.id.cb_needAddress);
		cbGpsFirst = (CheckBox) findViewById(R.id.cb_gpsFirst);
		tvReult = (TextView) findViewById(R.id.tv_result);
		btLocation = (Button) findViewById(R.id.bt_location);

		btLocation.setOnClickListener(this);

		locationClient = new AMapLocationClient(this.getApplicationContext());
		locationOption = new AMapLocationClientOption();
		// 设置定位模式为高精度模式
		locationOption.setLocationMode(AMapLocationMode.Hight_Accuracy);
		// 设置定位监听
		locationClient.setLocationListener(this);
		
		// 创建Intent对象，action为LOCATION
		alarmIntent = new Intent();
		alarmIntent.setAction("LOCATION");
		/*意图过滤器*/
		IntentFilter ift = new IntentFilter();

		// 定义一个PendingIntent对象，PendingIntent.getBroadcast包含了sendBroadcast的动作。
		// 也就是发送了action 为"LOCATION"的intent
		alarmPi = PendingIntent.getBroadcast(this, 0, alarmIntent, 0);
		// AlarmManager对象,注意这里并不是new一个对象，Alarmmanager为系统级服务
		alarm = (AlarmManager) getSystemService(ALARM_SERVICE);
		
		//动态注册一个广播
		IntentFilter filter = new IntentFilter();
		filter.addAction("LOCATION");
		registerReceiver(alarmReceiver, filter);
	}

	@Override
	protected void onDestroy() {
		super.onDestroy();
		if (null != locationClient) {
			/**
			 * 如果AMapLocationClient是在当前Activity实例化的，
			 * 在Activity的onDestroy中一定要执行AMapLocationClient的onDestroy
			 */
			locationClient.onDestroy();
			locationClient = null;
			locationOption = null;
		}
//		注销广播接收器
		if(null != alarmReceiver){
			unregisterReceiver(alarmReceiver);
			alarmReceiver = null;
		}
	}

	/**
	 * 设置控件的可用状态
	 */
	private void setViewEnable(boolean isEnable) {
		etInterval.setEnabled(isEnable);
		etAlarm.setEnabled(isEnable);
		cbAddress.setEnabled(isEnable);
		cbGpsFirst.setEnabled(isEnable);
	}

	@Override
	public void onClick(View v) {
		if (v.getId() == R.id.bt_location) {
			if (btLocation.getText().equals(
					getResources().getString(R.string.startLocation))) {
				setViewEnable(false);//设置控件的可用状态
				initOption();// 根据控件的选择，重新设置定位参数
				//这个是唤醒周期
				int alarmInterval = 5;
				String str = etAlarm.getText().toString();
				if(!TextUtils.isEmpty(str)){
					alarmInterval = Integer.parseInt(str);
				}
//				按钮显示的文字发生变化
				btLocation.setText(getResources().getString(
						R.string.stopLocation));
				// 设置定位参数
				locationClient.setLocationOption(locationOption);
				// 启动定位
				locationClient.startLocation();
//				public final static int MSG_LOCATION_START = 0;
				mHandler.sendEmptyMessage(Utils.MSG_LOCATION_START);
				
				if(null != alarm){
					//设置一个闹钟，2秒之后每隔一段时间执行启动一次定位程序
					alarm.setRepeating(AlarmManager.ELAPSED_REALTIME_WAKEUP, SystemClock.elapsedRealtime() + 2*1000,
							alarmInterval * 1000, alarmPi);
				}
			} else {
				setViewEnable(true);
				btLocation.setText(getResources().getString(
						R.string.startLocation));
				// 停止定位
				locationClient.stopLocation();
				mHandler.sendEmptyMessage(Utils.MSG_LOCATION_STOP);
				
				//停止定位的时候取消闹钟
				if(null != alarm){
					alarm.cancel(alarmPi);
				}
			}
		}
	}

	// 根据控件的选择，重新设置定位参数
	private void initOption() {
		// 设置是否需要显示地址信息
		locationOption.setNeedAddress(cbAddress.isChecked());
		/**
		 * 设置是否优先返回GPS定位结果，如果30秒内GPS没有返回定位结果则进行网络定位
		 * 注意：只有在高精度模式下的单次定位有效，其他方式无效
		 */
		locationOption.setGpsFirst(cbGpsFirst.isChecked());
		String strInterval = etInterval.getText().toString();
		if (!TextUtils.isEmpty(strInterval)) {
			// 设置发送定位请求的时间间隔,最小值为1000，如果小于1000，按照1000算
			locationOption.setInterval(Long.valueOf(strInterval));
		}

	}

	Handler mHandler = new Handler() {
		public void dispatchMessage(android.os.Message msg) {
			switch (msg.what) {
			//开始定位
			case Utils.MSG_LOCATION_START:
				tvReult.setText("正在定位...");
				break;
			// 定位完成
			case Utils.MSG_LOCATION_FINISH:
				AMapLocation loc = (AMapLocation) msg.obj;
				//对地址的信息进行分解
				String result = Utils.getLocationStr(loc);
				tvReult.setText(result);
				break;
			//停止定位
			case Utils.MSG_LOCATION_STOP:
				tvReult.setText("定位停止");
				break;
			default:
				break;
			}
		};
	};
	
	// 定位监听
	@Override
	public void onLocationChanged(AMapLocation loc) {
		if (null != loc) {
			//消息携带一个内部对象
			Message msg = mHandler.obtainMessage();
			msg.obj = loc;
			msg.what = Utils.MSG_LOCATION_FINISH;
			mHandler.sendMessage(msg);
		}
	}
	
	//内部自定义的广播接收器
	private BroadcastReceiver alarmReceiver = new BroadcastReceiver(){
		@Override
		public void onReceive(Context context, Intent intent) {
			if(intent.getAction().equals("LOCATION")){
				if(null != locationClient){
					locationClient.startLocation();
				}
			}
		}
	};
	
}

```
<h1 id="101">1. 说明</h1>

[返回目录](#1)

```
android:theme="@style/myTheme"
```
<h1 id="101">1. 说明</h1>

[返回目录](#1)

```
android:theme="@style/myTheme"
```