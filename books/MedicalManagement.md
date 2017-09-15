 # 2017 06 09

<h1 id="0">目录</h1> 

> ## [简介](#00)
> ## [1. 欢迎页面 WelcomeActivity](#01)
> ## [2. 引导页面 GuideActivity ](#02)
> ## [3. 主页面 MyMainActivity](#03)
> ## [4. ImageDownLoader图片下载](#04)
> ## [5. 智能提醒页面  SetRemindActivity](#05)
> ## [6. 智能提醒调用的广播  RemindReceiver](#05)
> ## [7. 智能提醒调用的提醒页面  RemindSoundActivity](#05)
> ## [8. 测量提醒页面包含日历   SetRemindActivity](#06)
> ## [9. 用药提醒  SetRemindYaoActivity](#07)
> ## [10. 点击药品说明书 出现的详情页面 有语音 收藏 点赞 分享 ZiXunDetailActivity](#10)
> ## [11. 数据库的思路](#11)
> ## [12. 添加用药提醒  YongYaoAddActivity](#12)
> ## [13. 护理任务提醒  SetRemindHuliActivity](#13)
> ## [14. 添加护理任务提醒  SetRemindHuliAddActivity](#14) 
> ## [15. 智能检测  MainCeLingActivity](#15)
>
> ## [16. 病情评估  MainPingGuActivity](#16) 
> ## [17. 更多服务  MainServiceActivity](#17)
> ## [18. 健康商城 MainServiceShopActivity](#18)
> ## [19. 更多应用 MainServiceOtherActivity](#19)
> ## [20. 电话咨询 MainPhoneActivity](#20)
> ## 个人中心板块
>> ## [21. 个人中心 MainSetActivity](#21)
>> ## [22. 其他 MainSetAboutActivity](#22)
>> ## [23. 我的收藏 SetCollectionActivity](#23)
>> ## [24. 数据管理 CeLingDataActivity](#24)
>> ## [25. 生活日志 SetLifeDataActivity](#25)
>> ## [26. 心衰助手 MainHelpActivity](#26)
>> ## [27. 心率记录 HelpHeartActivity](#27)
>> ## [28. 出入水量 HelpWaterActivity](#28)
>> ## [29. 心率详情 HelpHeartInfoActivity](#29)
> ## 病情评估板块
>> ## [30. 病情评估 MainPingGuActivity](#30)
>> ## [31. 心衰评估1 PingGuInfoActivity](#31)
>> ## [32. 历史评估 PingGuHistoryActivity](#32)
>> ## [33. 心衰评估2 PingGuForthwithActivity](#33)
>> ## [34. 心衰评估3 PingGuStageActivity](#34)
> ## 智能咨询板块
>> ## [35. 智能咨询 MainYiShiActivity](#35)
>> ## [36. 咨询会话 YiShiChatActivity](#36)
> ## 心衰百科板块
>> ## [37. 心衰百科 MainZiXunActivity](#37)
>> ## [38. 详情页面(心衰百科) ZiXunDetailActivity](#38)
> ## [39. 日期的运用](#39)

# 参考文档
> # [云端地址](https://github.com/tanyinqing/MarkDown/tree/master/app/src/main/java/codewarehouse/yzkj/com/markdown "查看")
> # [医疗管理.md](https://github.com/tanyinqing/MarkDown/blob/master/app/src/main/java/codewarehouse/yzkj/com/markdown/%E5%8C%BB%E7%96%97%E7%AE%A1%E7%90%86.md#0 "查看")
> # [github](https://github.com/tanyinqing/HeartMark "查看")
> # [百度项目地址](http://pan.baidu.com/disk/home?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&#list/vmode=list&path=%2F%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6%E5%A4%B9%2F%E9%A1%B9%E7%9B%AE%E6%A8%A1%E5%9D%97 "查看")
> # [文档地址](http://pan.baidu.com/disk/home?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&#list/vmode=list&path=%2F%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6%E5%A4%B9%2F%E5%AE%89%E5%8D%93%E9%A1%B9%E7%9B%AE%E4%BB%A3%E7%A0%81%E4%BB%93%E5%BA%93%2FMarkDown%E5%BC%80%E5%8F%91%E6%96%87%E6%A1%A3 "查看")

<h1 id="00">简介</h1> 

## [返回目录](#0)

> ## 1. 这是一个医疗器材类的项目
> ## 2. 用到的第三方有分享，，推送，讯飞语音，扫描，统计。
> ## 3. 硬件有蓝牙，
> ## 4. 页面50多个
> ## 5. 用到的权限如下：

```
 <!-- 分享 -->
    <uses-permission android:name="android.permission.GET_TASKS" />  //获取当前或最近运行的应用
    <uses-permission android:name="android.permission.INTERNET" />	//访问网络
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />	//Wifi状态
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />	//网络状态
    <uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />	//wifi状态改变
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" /> //写入内存卡
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />	//读取电话状态
    <uses-permission android:name="android.permission.MANAGE_ACCOUNTS" /> //允许程序管理AccountsManager中的账号列表
    <uses-permission android:name="android.permission.GET_ACCOUNTS" /> 访问Gmail账号列表

    <!-- 扫描 -->
    <uses-permission android:name="android.permission.VIBRATE" />	//振动
    <uses-permission android:name="android.permission.CAMERA" />	//相机

    <uses-feature android:name="android.hardware.camera" />
    <uses-feature android:name="android.hardware.camera.autofocus" />
    <!-- 蓝牙 -->
    <uses-permission android:name="android.permission.BLUETOOTH" />
    <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />

    <!-- 网络 -->
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />

    <!-- 点亮屏幕  -->
    <uses-permission android:name="android.permission.WAKE_LOCK" />
    <uses-permission android:name="android.permission.DISABLE_KEYGUARD" />

```

> ## 6. 

<h1 id="01">欢迎页面 WelcomeActivity </h1>  

## [返回目录](#0)

> ## 1. 父类中通过Handler来显示和关闭进度条。
> ## 2. [Android 线程通信之Handler -- 一篇文章彻底弄懂Handler](http://www.jianshu.com/p/f4ca6c7918c5 "查看")
> ## 3. 1秒后跳转到引导页面或主页面。
> ## 3. 复制数据库

<h1 id="02">引导页面 WelcomeActivity </h1>  

## [返回目录](#0)

> ## 1. 没写详细。

<h1 id="03">主页面 MyMainActivity </h1>  

## [返回目录](#0)

> ## 1. 整体采用的相对布局，首先是标题，其次是帧布局和viewPager写的图片轮播，下面是4个板块，最下面是3个底部导航栏。
> ## 2. [Android手势监听类GestureDetector](http://www.jianshu.com/p/7b47be38f64a)
> ## 3. 监听viewpager的点击事件，停止滑动
> ## 4. ZiXun 这个类包含了要提供显示的信息。
> ## 5. 从自定义的xml文件中获取字符串数组


```
<?xml version="1.0" encoding="utf-8"?>
<resources>
         <!-- 身体状态 -->
    <string-array name="celing_state">
        <item>多汗</item>
        <item>心悸</item>
        <item>胸疼</item>
        <item>呼吸急促</item>
        <item>烦躁</item>
        <item>咳嗽</item>
    </string-array>
</resources>


private String[] states = null;

states = getResources().getStringArray(R.array.celing_state);

```

> ## 6. 按照比例设置轮播图的宽高

```
private ViewPager mainViewPager;

//按照比例设置轮播图的宽高
		WindowManager wm = (WindowManager) MyMainActivity.this.getSystemService(Context.WINDOW_SERVICE);
		int width = wm.getDefaultDisplay().getWidth();
		LinearLayout.LayoutParams params = new LinearLayout.LayoutParams(LayoutParams.WRAP_CONTENT, LayoutParams.WRAP_CONTENT);
		params.width = width;
		params.height = width * 19 / 32;
		mainViewPager.setLayoutParams(params);
```

> ## 7. 判断当前网络是否已经连接

```
// 判断当前网络是否已经连接 
	public static boolean isConnect(Context context) {
		try {
			ConnectivityManager connectivity = (ConnectivityManager) context
					.getSystemService(Context.CONNECTIVITY_SERVICE);
			if (connectivity != null) {
				// 获取网络连接管理的对象
				NetworkInfo info = connectivity.getActiveNetworkInfo();
				if (info != null && info.isConnected()) {
					if (info.getState() == NetworkInfo.State.CONNECTED) {
						return true;
					}
				}
			}
		} catch (Exception e) {
			return false;
		}
		return false;
	}
```

> ## 8. [使用Gson将Java对象转换为JSON](http://blog.csdn.net/wuseyukui/article/details/13775449)
 
```
//使用Gson将Java对象转换为JSON
	public static String convertObjectToJson(Object obj){
		String result = "";
		Gson gson = new Gson();
		result = gson.toJson(obj);
		return result;
	}

```

> ## 9. 未同步的数据查询 如果存在没有同步的数据，就把这些数据上传到服务器，
  
```
//未同步查询
	public ArrayList<HelpHeart> getListByNoSync(String uid) {
		SQLiteDatabase db = helper.getWritableDatabase();
		ArrayList<HelpHeart> huliLifeArray = new ArrayList<HelpHeart>();
		Cursor cursor = db.query("heart", new String[] { "id", "uid", "sync","date",
				"dateMonth", "day", "time", "timeMill", "heart"}, "sync=? and uid=?", 
				new String[] { String.valueOf(ConstantUtil.SYNC_NO), uid}, null, null, null);
		cursorMethod(huliLifeArray, cursor);
		cursor.close();
		db.close();
		return huliLifeArray;
	}


// 对cursor查询结果方法抽取
	private void cursorMethod(ArrayList<HelpHeart> huliLifeArray, Cursor cursor) {
		while (cursor.moveToNext()) {
			HelpHeart helpHeart = new HelpHeart();
			helpHeart.id = cursor.getInt(cursor.getColumnIndex("id"));
			helpHeart.uid = cursor.getString(cursor.getColumnIndex("uid"));
			helpHeart.sync = cursor.getInt(cursor.getColumnIndex("sync"));
			helpHeart.date = cursor.getString(cursor.getColumnIndex("date"));
			helpHeart.dateMonth = cursor.getString(cursor.getColumnIndex("dateMonth"));
			helpHeart.day = cursor.getString(cursor.getColumnIndex("day"));
			helpHeart.time = cursor.getString(cursor.getColumnIndex("time"));
			helpHeart.timeMill = cursor.getLong(cursor.getColumnIndex("timeMill"));
			helpHeart.heart = cursor.getInt(cursor.getColumnIndex("heart"));
			huliLifeArray.add(helpHeart);
		}
	}
```
> ## 10. 同步数据的方法

 
```
//同步心率  ---6号请求---
		//从数据库查询到的没有同步的数据
		ArrayList<HelpHeart>  heartList = heartDB.getListByNoSync(uid);
		if(heartList.size() > 0){
			//把数据整理成键值对，放到链表中
			List<Map<String, String>> heartUploadList = new ArrayList<Map<String, String>>();
			for(int i=0; i<heartList.size(); i++){
				Map<String,String> heartParam = new HashMap<String,String>();
				heartParam.put("HEART_RATE", String.valueOf(heartList.get(i).heart));
				heartParam.put("NURSE_DATE", heartList.get(i).date+ " " +heartList.get(i).time);
				heartUploadList.add(heartParam);
			}
			// 这个是上传携带的参数
			Map<String, String> weightParams = new HashMap<String, String>();
			String uploadString = JsonUtil.convertObjectToJson(heartUploadList);
			weightParams.put("nurseData", uploadString);
			// heartSucessCallBack 这个是回调方法
			ConnectionManager.getInstance().send("FN11060WD00", "saveNurseInfoByList", weightParams, "heartSucessCallBack", this);
		}
	}


//---6号回调 ---
	@SuppressWarnings("rawtypes")
	public void heartSucessCallBack(Object data) {
		Map resultMap = (Map) data;
		if (resultMap == null) {
			//ShowUtil.showToast(MyMainActivity.this,"体重空");
		} else {
			String result = (String) resultMap.get("head");
			if (result.equals("success")) {
				//ShowUtil.showToast(MyMainActivity.this,"体重yes");
				
				heartDB.updataSyncNoToYes(uid);
			} else if (result.equals("fail")) {
				//ShowUtil.showToast(MyMainActivity.this,"体重no");
				
			}
		}
	}


//将数据库未同步的标志改为同步
	public int updataSyncNoToYes(String uid) {
		SQLiteDatabase db = helper.getWritableDatabase();
		ContentValues values = new ContentValues();
		values.put("sync", ConstantUtil.SYNC_YES);
		int result = db.update("heart", values, "sync=? and uid=?",new String[] { String.valueOf( ConstantUtil.SYNC_NO), uid});
		db.close();
		return result;
	}
```

> ## 11. 对软件判断是否升级。下载新的版本

```
// 下载
	MyDialog m_pDialog;
	public void doawnload() {
		HttpUtils utils = new HttpUtils();
		m_pDialog = new MyDialog(MyMainActivity.this);
		m_pDialog.setTitle("提示");
		m_pDialog.setMessage("心衰版本更新中...");
		//m_pDialog.setIcon(R.drawable.heart_mark_icon);
		//m_pDialog.setIndeterminate(false);
		//m_pDialog.setCancelable(false);
		m_pDialog.setProgressbar();
		m_pDialog.create(null);
		m_pDialog.showMyDialog();
		/**
		 * 判断SD的状态：如果SD不存在就进行友好提示
		 */
		if (!Environment.getExternalStorageState().equals(
				Environment.MEDIA_MOUNTED)) {
			MyToast.show(getApplicationContext(), "手机SD卡不存在",
					Toast.LENGTH_SHORT);
			return;
		}
		/*
		 * 参数： 1 下载url地址 2 下载到哪个位置 3 回调方法
		 */
		utils.download(versionUrl, Environment.getExternalStorageDirectory()
				.getAbsolutePath() + "/HeartMark" + version + ".apk",
				new RequestCallBack<File>() {

					@Override
					public void onFailure(HttpException arg0, String arg1) {// 下载失败
						ShowUtil.showToast(MyMainActivity.this,
								R.string.download_fail);
						m_pDialog.dismiss();
					}

					// 下载成功
					@Override
					public void onSuccess(ResponseInfo<File> arg0) {

						m_pDialog.dismiss();
						// 下载成功，调用系统安装程序进行程序的安装
						installAPk();
					}

					@Override
					public void onLoading(final long total, final long current,
							boolean isUploading) {// 下载进度
						super.onLoading(total, current, isUploading);
						int progress = (int) (current * 100 / total);
						m_pDialog.setProgress(progress);
					}
				});
	}
	
	// 安装
	public void installAPk() {
		Intent intent = new Intent();
		intent.setAction("android.intent.action.VIEW");
		intent.addCategory("android.intent.category.DEFAULT");
		intent.setDataAndType(
				Uri.fromFile(new File(Environment.getExternalStorageDirectory()
						.getAbsolutePath() + "/HeartMark" + version + ".apk")),
				"application/vnd.android.package-archive");
		/**
		 * 安装后进行函数的回调
		 */
		this.startActivityForResult(intent, 100);
	}
```
> ## 12. 图片轮播的实现
 
```
//开启事件传递机制
@SuppressLint("HandlerLeak")
	Handler handler = new Handler() {
		@Override
		public void handleMessage(Message msg) {
			super.handleMessage(msg);
			switch (msg.what) {
			case 1:
				if (mainViewPager.getCurrentItem() == (pagerList.size() - 1)) {
					currentnum = 0;
				} else {
					currentnum = mainViewPager.getCurrentItem() + 1;
				}
				mainViewPager.setCurrentItem(currentnum);
				break;
			case MSG_SHOWUPGRADE:
				showUpgradeDialog();
				SharedPreferenceUtil.setBoolean(MyMainActivity.this, ConstantUtil.SHOW_UPDATE, false);
				break;
				// 进行下载
			case MSG_DOAWNLOAD:
				doawnload();
				break;
			default:
				break;
			}
		}
	};

//定时器 图片开始时开启
private Timer timer; 
	public void TimerStart() {
		TimerTask task = new TimerTask() {
			public void run() {
				Message message = handler.obtainMessage();
				message.what = 1;
				handler.sendMessage(message);
			}
		};
		timer = new Timer(true);
		timer.schedule(task, 0, 4000);
	}

	public void TimerStop() {
		if (timer != null) {
			timer.cancel();
		}
	}


@Override
	public void onDestroy() {
		super.onDestroy();
		TimerStop();
		//如果蓝牙开启,退出时关闭蓝牙
		if(bluetoothAdapter.isEnabled()){
			bluetoothAdapter.disable();
		}
	}


```
> ## 13. 初始化轮播图的指示点

```
//初始化轮播图的指示点
	public void setPoint(int page) {
		pointLayout.removeAllViews();
		page = page % pagerList.size();
		for (int i = 0; i < pagerList.size(); i++) {
			point = new ImageView(this);
			LayoutParams params = new LinearLayout.LayoutParams(
					LayoutParams.WRAP_CONTENT, LayoutParams.WRAP_CONTENT);
			params.leftMargin = 10;
			point.setLayoutParams(params);
			point.setBackgroundResource(R.drawable.point_yes);
			if (page != i) {
				point.setBackgroundResource(R.drawable.point_no);
			}
			pointLayout.addView(point);
		}
	}



mainViewPager = (ViewPager) findViewById(R.id.main_viewpager);
		mainViewPager.setOnPageChangeListener(new MyPageChangeListener());


// viewPager监听器
	class MyPageChangeListener implements OnPageChangeListener {

		@Override
		public void onPageSelected(int arg0) {
			setPoint(arg0);
		}

		@Override
		public void onPageScrolled(int arg0, float arg1, int arg2) {

		}

		@Override
		public void onPageScrollStateChanged(int arg0) {
		}
	}
```

> ## 14. 轮播图的数据是每次都从服务端下载最新的，存入数据库，清除以前的数据。
> ## 15. 药品详情同步的方法，访问服务端，返回最新的数据，清除数据表，把最新的数据插入数据表中。

```
//---2号回调 ---
	@SuppressWarnings("rawtypes")
	public void yaoSucessCallBack(Object data){
		ArrayList<Yao> yaoList = new ArrayList<Yao>();
		List resultMap = (ArrayList) data;
		if (resultMap == null || resultMap.size() == 0) {
		   //ShowUtil.showToast(MyMainActivity.this,R.string.check_network_timeout);
		} else {
		for(int i =0;i<resultMap.size();i++){
			Yao yao =new Yao();
			Map temp = new HashMap();
			temp = (Map) resultMap.get(i);
			yao.uid = uid;
			yao.yaoId = (String) temp.get("UUID");
			yao.name = (String) temp.get("DRUG_NAME");
			yao.type = (String) temp.get("DRUG_TYPE");
		    yao.typeName = (String) temp.get("DRUG_TYPE_NAME");
		    yao.firm = (String) temp.get("DRUG_COMPANY");
		    //yao.content = (String) temp.get("CONTENT");
		    //yao.contentText = (String) temp.get("CONTENT_TEMP");
		    yaoList.add(yao);
		 }
		//清理数据表
		yaoDB.delete();
		//保存到数据库
		for(int i=0; i<yaoList.size(); i++){
			yaoDB.insertYao(yaoList.get(i));
		  }
    	}
	}
```
> ## 16. 多个回调方法的总结：
>> 1. 有些数据只是下载新的数据覆盖老的数据
>> 2. 有些数据是把本地没有同步的数据上传到服务器。
> ## 17 轮播图数据的适配
 
```
if(SharedPreferenceUtil.getBoolean(MyMainActivity.this, ConstantUtil.SHOW_UPDATE)){
			sync();//数据的同步
		}else{
//从数据库读取数据
			pagerList = imageDB.getImageList();
			mainViewPagerAdapter = new NetViewPagerAdapter(MyMainActivity.this,pagerList);
			mainViewPager.setAdapter(mainViewPagerAdapter);
			setPoint(0);//设置指示点
			TimerStart();//图片开始轮播
		}


//ViewPager 的图片适配器

package com.yikang.heartmark.adapter;

import java.util.ArrayList;

import android.content.Context;
import android.content.Intent;
import android.graphics.Bitmap;
import android.os.Bundle;
import android.support.v4.view.PagerAdapter;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ImageView;

import com.example.heartmark.R;
import com.yikang.heartmark.activity.ZiXunDetailGetActivity;
import com.yikang.heartmark.model.ZiXun;
import com.yikang.heartmark.util.ConnectUtil;
import com.yikang.heartmark.util.ImageDownLoader;
import com.yikang.heartmark.util.ImageDownLoader.onImageLoaderListener;

public class NetViewPagerAdapter extends PagerAdapter{
	private LayoutInflater layoutInflater = null;
	private ArrayList<ZiXun> pagers;
	private Context context;
	private ImageDownLoader mImageDownLoader;
	
	public NetViewPagerAdapter(Context context, ArrayList<ZiXun> views) {
		this.pagers = views;
		this.context = context;
		mImageDownLoader = new ImageDownLoader(context);
		this.layoutInflater = LayoutInflater.from(context);
	}

	@Override
	public int getCount() {
		return pagers.size();
	}

	@Override
	public boolean isViewFromObject(View arg0, Object arg1) {
		return arg0 == arg1;
	}

	@Override
	public int getItemPosition(Object object) {
		return super.getItemPosition(object);
	}

	@Override
	public void destroyItem(ViewGroup container, int position, Object object) {
		container.removeView((View) object);
	}

	@Override
	public Object instantiateItem(ViewGroup view, int position) {
		View imageLayout = layoutInflater.inflate(R.layout.item_pager_image, view, false);
		final ImageView imageView = (ImageView) imageLayout.findViewById(R.id.image);
		ZiXun item = pagers.get(position);
		Bitmap bitmap = null;
		bitmap = mImageDownLoader.downloadImage(ConnectUtil.HOST_URL + item.image, new onImageLoaderListener() {
			@Override
			public void onImageLoader(Bitmap bitmap, String url) {
				if(imageView != null && bitmap != null){
					imageView.setImageBitmap(bitmap);
				}
			}
		});
		
		if(bitmap != null){
			imageView.setImageBitmap(bitmap);
		}
	/*	else{
			imageView.setImageDrawable(context.getResources().getDrawable(R.drawable.pinggu_show));
		}*/
		/*BitmapUtils bitmapUtils = new BitmapUtils(context);
		bitmapUtils.display(imageView,ConnectUtil.HOST_URL + item.image);*/
		
		view.addView(imageLayout, 0);
		imageView.setOnClickListener(new MyViewOnclicklistener(pagers.get(position)));
		return imageLayout;
	}
	
	class MyViewOnclicklistener implements View.OnClickListener {
        private ZiXun zixun;
		public MyViewOnclicklistener(ZiXun zixun){
			this.zixun = zixun;
		}
		@Override
		public void onClick(View v) {
			final int rid = v.getId();
			switch (rid) {
			case R.id.image:
				Intent detailIntent = new Intent(context,ZiXunDetailGetActivity.class);
				Bundle bundle = new Bundle();
				bundle.putSerializable("newItem", zixun);
				detailIntent.putExtras(bundle);
				context.startActivity(detailIntent);
				break;

			default:
				break;
			}
		}
	}
}

```

<h1 id="04">ImageDownLoader 图片下载 </h1>  

## [返回目录](#0)

> ## 1. 调用的方法
```
bitmap = mImageDownLoader.downloadImage(ConnectUtil.HOST_URL + item.image, new onImageLoaderListener() {
			@Override
			public void onImageLoader(Bitmap bitmap, String url) {
				if(imageView != null && bitmap != null){
					imageView.setImageBitmap(bitmap);
				}
			}
		});
```
> ## 2. ImageDownLoader

```
package com.yikang.heartmark.util;


import java.io.IOException;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

import android.annotation.SuppressLint;
import android.content.Context;
import android.graphics.Bitmap;
import android.graphics.BitmapFactory;
import android.os.Handler;
import android.os.Message;
import android.support.v4.util.LruCache;

@SuppressLint("HandlerLeak")
public class ImageDownLoader {
	/**
	 * 缓存Image的类，当存储Image的大小大于LruCache设定的值，系统自动释放内存
	 */
	private LruCache<String, Bitmap> mMemoryCache;
	/**
	 * 操作文件相关类对象的引用
	 */
	private FileUtils fileUtils;
	/**
	 * 下载Image的线程池
	 */
	private ExecutorService mImageThreadPool = null;
	
	
	public ImageDownLoader(Context context){
		//获取系统分配给每个应用程序的最大内存，每个应用系统分配32M
		int maxMemory = (int) Runtime.getRuntime().maxMemory();  
        int mCacheSize = maxMemory / 8;
        //给LruCache分配1/8 4M
		mMemoryCache = new LruCache<String, Bitmap>(mCacheSize){

			//必须重写此方法，来测量Bitmap的大小
			@Override
			protected int sizeOf(String key, Bitmap value) {
				return value.getRowBytes() * value.getHeight();
			}
			
		};
		
		fileUtils = new FileUtils(context);
	}
	
	
	/**
	 * 获取线程池的方法，因为涉及到并发的问题，我们加上同步锁
	 * @return
	 */
	public ExecutorService getThreadPool(){
		if(mImageThreadPool == null){
			synchronized(ExecutorService.class){
				if(mImageThreadPool == null){
					//为了下载图片更加的流畅，我们用了2个线程来下载图片
					mImageThreadPool = Executors.newFixedThreadPool(2);
				}
			}
		}
		
		return mImageThreadPool;
		
	}
	
	/**
	 * 添加Bitmap到内存缓存
	 * @param key
	 * @param bitmap
	 */
	public void addBitmapToMemoryCache(String key, Bitmap bitmap) {  
	    if (getBitmapFromMemCache(key) == null && bitmap != null) {  
	        mMemoryCache.put(key, bitmap);  
	    }  
	}  
	 
	/**
	 * 从内存缓存中获取一个Bitmap
	 * @param key
	 * @return
	 */
	public Bitmap getBitmapFromMemCache(String key) {  
	    return mMemoryCache.get(key);  
	} 
	
	/**
	 * 先从内存缓存中获取Bitmap,如果没有就从SD卡或者手机缓存中获取，SD卡或者手机缓存
	 * 没有就去下载
	 * @param url
	 * @param listener
	 * @return
	 */
	public Bitmap downloadImage(final String url, final onImageLoaderListener listener){
		//替换Url中非字母和非数字的字符，这里比较重要，因为我们用Url作为文件名，比如我们的Url
		//是Http://xiaanming/abc.jpg;用这个作为图片名称，系统会认为xiaanming为一个目录，
		//我们没有创建此目录保存文件就会保存
		final String subUrl = url.replaceAll("[^\\w]", "");
		Bitmap bitmap = showCacheBitmap(subUrl);
		if(bitmap != null){
			return bitmap;
		}else{
			
			final Handler handler = new Handler(){
				@Override
				public void handleMessage(Message msg) {
					super.handleMessage(msg);
					listener.onImageLoader((Bitmap)msg.obj, url);
				}
			};
			
			getThreadPool().execute(new Runnable() {
				
				@Override
				public void run() {
					Bitmap bitmap = getBitmapFormUrl(url);
					Message msg = handler.obtainMessage();
					msg.obj = bitmap;
					handler.sendMessage(msg);
					
					try {
						//保存在SD卡或者手机目录
						fileUtils.savaBitmap(subUrl, bitmap);
					} catch (IOException e) {
						e.printStackTrace();
					}
					
					//将Bitmap 加入内存缓存
					addBitmapToMemoryCache(subUrl, bitmap);
				}
			});
		}
		
		return null;
	}
	
	/**
	 * 获取Bitmap, 内存中没有就去手机或者sd卡中获取，这一步在getView中会调用，比较关键的一步
	 * @param url
	 * @return
	 */
	public Bitmap showCacheBitmap(String url){
		if(getBitmapFromMemCache(url) != null){
			return getBitmapFromMemCache(url);
		}else if(fileUtils.isFileExists(url) && fileUtils.getFileSize(url) != 0){
			//从SD卡获取手机里面获取Bitmap
			Bitmap bitmap = fileUtils.getBitmap(url);
			
			//将Bitmap 加入内存缓存
			addBitmapToMemoryCache(url, bitmap);
			return bitmap;
		}
		
		return null;
	}
	
	
	/**
	 * 从Url中获取Bitmap
	 * @param url
	 * @return
	 */
	private Bitmap getBitmapFormUrl(String url) {
		Bitmap bitmap = null;
		HttpURLConnection con = null;
		try {
			URL mImageUrl = new URL(url);
			con = (HttpURLConnection) mImageUrl.openConnection();
			con.setConnectTimeout(10 * 1000);
			con.setReadTimeout(10 * 1000);
			con.setDoInput(true);
			con.setDoOutput(true);
			bitmap = BitmapFactory.decodeStream(con.getInputStream());
		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			if (con != null) {
				con.disconnect();
			}
		}
		return bitmap;
	}
	
	/**
	 * 取消正在下载的任务
	 */
	public synchronized void cancelTask() {
		if(mImageThreadPool != null){
			mImageThreadPool.shutdownNow();
			mImageThreadPool = null;
		}
	}
	
	
	/**
	 * 异步下载图片的回调接口
	 * @author len
	 *
	 */
	public interface onImageLoaderListener{
		void onImageLoader(Bitmap bitmap, String url);
	}
	
}

```
> ## 3. FileUtils文件

```
package com.yikang.heartmark.util;


import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;

import android.content.Context;
import android.graphics.Bitmap;
import android.graphics.Bitmap.CompressFormat;
import android.graphics.BitmapFactory;
import android.os.Environment;

public class FileUtils {
	/**
	 * sd卡的根目录
	 */
	private static String mSdRootPath = Environment.getExternalStorageDirectory().getPath();
	/**
	 * 手机的缓存根目录
	 */
	private static String mDataRootPath = null;
	/**
	 * 保存Image的目录名
	 */
	private final static String FOLDER_NAME = "/AndroidImage";
	
	
	public FileUtils(Context context){
		mDataRootPath = context.getCacheDir().getPath();
	}
	

	/**
	 * 获取储存Image的目录
	 * @return
	 */
	private String getStorageDirectory(){
		return Environment.getExternalStorageState().equals(Environment.MEDIA_MOUNTED) ?
				mSdRootPath + FOLDER_NAME : mDataRootPath + FOLDER_NAME;
	}
	
	/**
	 * 保存Image的方法，有sd卡存储到sd卡，没有就存储到手机目录
	 * @param fileName 
	 * @param bitmap   
	 * @throws IOException
	 */
	public void savaBitmap(String fileName, Bitmap bitmap) throws IOException{
		if(bitmap == null){
			return;
		}
		String path = getStorageDirectory();
		File folderFile = new File(path);
		if(!folderFile.exists()){
			folderFile.mkdir();
		}
		File file = new File(path + File.separator + fileName);
		file.createNewFile();
		FileOutputStream fos = new FileOutputStream(file);
		bitmap.compress(CompressFormat.JPEG, 100, fos);
		fos.flush();
		fos.close();
	}
	
	/**
	 * 从手机或者sd卡获取Bitmap
	 * @param fileName
	 * @return
	 */
	public Bitmap getBitmap(String fileName){
		return BitmapFactory.decodeFile(getStorageDirectory() + File.separator + fileName);
	}
	
	/**
	 * 判断文件是否存在
	 * @param fileName
	 * @return
	 */
	public boolean isFileExists(String fileName){
		return new File(getStorageDirectory() + File.separator + fileName).exists();
	}
	
	/**
	 * 获取文件的大小
	 * @param fileName
	 * @return
	 */
	public long getFileSize(String fileName) {
		return new File(getStorageDirectory() + File.separator + fileName).length();
	}
	
	
	/**
	 * 删除SD卡或者手机的缓存图片和目录
	 */
	public void deleteFile() {
		File dirFile = new File(getStorageDirectory());
		if(! dirFile.exists()){
			return;
		}
		if (dirFile.isDirectory()) {
			String[] children = dirFile.list();
			for (int i = 0; i < children.length; i++) {
				new File(dirFile, children[i]).delete();
			}
		}
		
		dirFile.delete();
	}
}

```
<h1 id="05">智能提醒页面 SetRemindActivity </h1>  

## [返回目录](#0)

> ## 1. 界面和选择器的使用

```
 <RelativeLayout
        android:id="@+id/set_remind_celing_layout"
        android:layout_width="match_parent"
        android:layout_height="40dp"
        android:layout_marginTop="20dp"
        android:background="@drawable/show_item_img" >

        <ImageView
            android:id="@+id/weight_img"
            android:layout_width="25dp"
            android:layout_height="25dp"
            android:layout_centerVertical="true"
            android:layout_marginLeft="20dp"
            android:background="@drawable/remind_celing_img" />

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_centerVertical="true"
            android:layout_marginLeft="10dp"
            android:layout_toRightOf="@+id/weight_img"
            android:text="测量提醒"
            android:textSize="18dp" />

        <Button
            android:id="@+id/set_remind_celing_check"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_centerVertical="true"
            android:layout_alignParentRight="true"
            android:layout_marginRight="20dp"
            android:background="@drawable/alarm_check_selector"
             />
    </RelativeLayout>


if(SharedPreferenceUtil.getBooleanDefaultTrue(SetRemindActivity.this, ConstantUtil.ALARM_YAO)){
			yaoCheck.setSelected(true);
		}else{
			yaoCheck.setSelected(false);
		}
```
> ## 2. 时间API的使用方法

```

//得到现在是周几
	public static int getThisWeek() {
		Calendar cal = Calendar.getInstance();
		return cal.get(Calendar.DAY_OF_WEEK) - 1;
	}


	//获取当前日期   用指定的格式来显示
		yearMonthDay = DateUtil.getNowDate(DateUtil.YEAR_MONTH_DAY);


/**
	 * 获取当前日期   用指定的格式来显示
	 * 
	 * @return
	 */

	public static String getNowDate(String dateFormat) {
		SimpleDateFormat sDateFormat = new SimpleDateFormat(dateFormat);

		return sDateFormat.format(new Date());
	}



//返回现在的时间   格式为Long型
	public static long getNowTimeInMillis() {
		Calendar nowCalendar = Calendar.getInstance();
		nowCalendar.getTimeInMillis();
		
		return System.currentTimeMillis();
	}


  public static final long DAY_MILLIS = 86400000L;  //一天有多少秒
	public static final long WEEK_MILLIS = 604800000L;   //一周有多少秒
  public static final long MONTH_MILLIS = 2592000000L;  //一月有多少秒
```
> ## 3. 不重复闹钟的设置方法

```
//这个是测量提醒
			case R.id.set_remind_celing_check:
                alarmList = alarmDB.getAlarmListByType(Alarm.TYPE_CELING);
				
                //点击的时候，如果被选中
				if (celingCheck.isSelected()) {
					celingCheck.setSelected(false);

					SharedPreferenceUtil.setBoolean(SetRemindActivity.this, ConstantUtil.ALARM_CELING, false);
					for(int i=0; i<alarmList.size(); i++){
						//把这些闹钟逐个关闭
	                	  Alarm.closeRemind(alarmManager, SetRemindActivity.this, alarmList.get(i).alarmId);
	                  }
				
				} else {
					celingCheck.setSelected(true);
					  SharedPreferenceUtil.setBoolean(SetRemindActivity.this, ConstantUtil.ALARM_CELING, true);
	                  for(int i=0; i<alarmList.size(); i++){
	                	  alarmList.get(i).isRepeat = false;
	                	  Alarm.setRemindNoDB(alarmList.get(i), alarmManager, SetRemindActivity.this);
	                  }
				}
				break;
```
> ## 4. 重复闹钟的设置方法

```
//这个是用药提醒  会重复
			case R.id.set_remind_yao_check:
				alarmList = alarmDB.getAlarmListByType(Alarm.TYPE_YAO);

				if (yaoCheck.isSelected()) {
					yaoCheck.setSelected(false);
					
					SharedPreferenceUtil.setBoolean(SetRemindActivity.this, ConstantUtil.ALARM_YAO, false);
					for(int i=0; i<alarmList.size(); i++){
	                	  Alarm.closeRemind(alarmManager, SetRemindActivity.this, alarmList.get(i).alarmId);
	                  }
					
				} else {
					yaoCheck.setSelected(true);

					SharedPreferenceUtil.setBoolean(SetRemindActivity.this, ConstantUtil.ALARM_YAO, true);
					for(int i=0; i<alarmList.size(); i++){
						  for(int k=0; k<weekList.length; k++){
							  if(alarmList.get(i).week.equals(weekList[k])){
								  weekAlarm = k+1;
							  }
						  }
						  
							if(weekAlarm < week){
								day = 7-(week-weekAlarm);
							}
							else if(weekAlarm == week){
								day =0;
							}
							else if(weekAlarm > week){
								day = weekAlarm - week;
							}
						  //日期+时间+天数的毫秒值
						  alarmList.get(i).alarmTime = DateUtil.getLongOfDayTimeAll(yearMonthDay, alarmList.get(i).time) + day*DateUtil.DAY_MILLIS;
	                	  alarmList.get(i).isRepeat = true;
	                	  alarmList.get(i).repeatTime = DateUtil.WEEK_MILLIS;
	                	  Alarm.setRemindNoDB(alarmList.get(i), alarmManager, SetRemindActivity.this);
	                  }
				}
				break;


//关闭闹钟
	public static void closeRemind(AlarmManager alarmManager, Context context, int alarmId) {
		Intent intent = new Intent();
		
		intent.setClass(context, RemindReceiver.class);
		PendingIntent pi = PendingIntent.getBroadcast(context, alarmId, intent, 0);
		
		alarmManager.cancel(pi);
	}


//AlarmManager  闹钟管理器	发送意图   但不存到数据库
	public static void setRemindNoDB(Alarm alarm,AlarmManager alarmManager, Context context){
		Intent intent = new Intent();
		
		Bundle bundle = new Bundle();
		bundle.putSerializable("alarm", alarm);
		intent.putExtras(bundle);
		
		intent.setClass(context, RemindReceiver.class);
		
		PendingIntent pi = PendingIntent.getBroadcast(context, alarm.alarmId,intent, PendingIntent.FLAG_UPDATE_CURRENT);
		if (alarm.isRepeat) {//如果是一个重复的闹钟
			//早于当前时间，到下周开始提醒
			if(alarm.alarmTime < DateUtil.getNowTimeInMillis()){
				alarm.alarmTime = alarm.alarmTime + DateUtil.WEEK_MILLIS;
			}
			alarmManager.setRepeating(AlarmManager.RTC_WAKEUP, alarm.alarmTime,alarm.repeatTime, pi);
		} else {
			if(alarm.alarmTime > DateUtil.getNowTimeInMillis()){
				alarmManager.set(AlarmManager.RTC_WAKEUP, alarm.alarmTime, pi);
			}
		}
	}
```
> ## 5. 闹钟调用的广播页面  RemindReceiver

```
package com.yikang.heartmark.receiver;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.os.Bundle;

import com.yikang.heartmark.activity.RemindSoundActivity;
import com.yikang.heartmark.model.Alarm;

  /*这是一个广播接受器，去启动一个闹钟的功能   启动闹钟的的广播接收器   */
public class RemindReceiver extends BroadcastReceiver {

	@Override
	public void onReceive(Context context, Intent intent) {
		Intent intentSound = new Intent(context, RemindSoundActivity.class);
		
		Alarm alarm = (Alarm) intent.getSerializableExtra("alarm");
		
		Bundle bundle = new Bundle();
		bundle.putSerializable("remindAlarm", alarm);
		intentSound.putExtras(bundle);
		intentSound.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK); //在新的进程中 打开意图
		
		context.startActivity(intentSound);
		
		/**
		
		try {
			MediaPlayer	player = new MediaPlayer();
			//播放完毕监听
			player.setOnCompletionListener(new OnCompletionListener() {

                @Override
                public void onCompletion(MediaPlayer mp) {
//                	playCount--;
//                    if(playCount > 0){
//                    	player.start();
//                    }else{
//                    	player.stop();
//                    	playCount = 3;
//                    }
                }
            });
			Uri alert = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_ALARM);
			player.setDataSource(context, alert);
			final AudioManager audioManager = (AudioManager) context.getSystemService(Context.AUDIO_SERVICE);
			if (audioManager.getStreamVolume(AudioManager.STREAM_NOTIFICATION) != 0) {
				player.setAudioStreamType(AudioManager.STREAM_NOTIFICATION);
				player.setLooping(false);
				player.prepare();
				player.start();
			}
		} catch (Exception e) {
			e.printStackTrace();
		}
		
		 */
	}
	


}
```
> ## 6. 广播显示的页面  RemindSoundActivity

```
package com.yikang.heartmark.activity;

import android.annotation.SuppressLint;
import android.app.KeyguardManager;
import android.app.KeyguardManager.KeyguardLock;
import android.content.Context;
import android.content.Intent;
import android.media.AudioManager;
import android.media.MediaPlayer;
import android.media.MediaPlayer.OnCompletionListener;
import android.media.RingtoneManager;
import android.net.Uri;
import android.os.Bundle;
import android.os.PowerManager;
import android.view.View;
import com.example.heartmark.R;
import com.yikang.heartmark.application.BaseActivity;
import com.yikang.heartmark.model.Alarm;
import com.yikang.heartmark.widget.MyDialog;

@SuppressWarnings("deprecation")
@SuppressLint("Wakelock")
/*作用是播放铃声，弹出对话框，屏幕解锁，屏灯亮*/
public class RemindSoundActivity extends BaseActivity {
	public MediaPlayer player;  //声音相关的类
	public Alarm alarm;
	public String title;
	public String message;

	@Override
	public void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		player = new MediaPlayer();
		Intent intent = this.getIntent();
		alarm = (Alarm) intent.getSerializableExtra("remindAlarm");

		// 获取电源管理器对象
		PowerManager pm = (PowerManager) getSystemService(Context.POWER_SERVICE);
		// 获取PowerManager.WakeLock对象,后面的参数|表示同时传入两个值,最后的是LogCat里用的Tag
		PowerManager.WakeLock wl = pm.newWakeLock(
				PowerManager.ACQUIRE_CAUSES_WAKEUP
						| PowerManager.SCREEN_DIM_WAKE_LOCK, "bright");
		// 点亮屏幕
		wl.acquire();

		// 得到键盘锁管理器对象
		KeyguardManager km = (KeyguardManager) getSystemService(Context.KEYGUARD_SERVICE);
		// 参数是LogCat里用的Tag
		KeyguardLock kl = km.newKeyguardLock("unLock");
		// 解锁
		kl.disableKeyguard();

		
		
		// 播放铃声
		try {
			Uri alert = RingtoneManager
					.getDefaultUri(RingtoneManager.TYPE_ALARM);
			
			player.setDataSource(RemindSoundActivity.this, alert);
			
			final AudioManager audioManager = (AudioManager) RemindSoundActivity.this
					.getSystemService(Context.AUDIO_SERVICE);
			
			if (audioManager.getStreamVolume(AudioManager.STREAM_NOTIFICATION) != 0) {
				player.setAudioStreamType(AudioManager.STREAM_NOTIFICATION);
				player.setLooping(false);
				player.prepare();
				player.start();
			}

			// 播放完毕监听
			player.setOnCompletionListener(new OnCompletionListener() {

				@Override
				public void onCompletion(MediaPlayer mp) {
				}
			});
		} catch (Exception e) {
			e.printStackTrace();
		}

		// 显示dialog
		if (alarm.type.equals(Alarm.TYPE_CELING)) {
			title = "测量提醒";
			message = alarm.time;
		} else if (alarm.type.equals(Alarm.TYPE_YAO)) {
			title = "用药提醒";
			message = alarm.yaoName + "\n" + alarm.time;
		} else if (alarm.type.equals(Alarm.TYPE_HULI)) {
			title = "护理提醒";
			message = alarm.time;
		}
		showDialog(title, message);  //弹出提示框

		
		// 重新启用自动加锁
		//kl.reenableKeyguard();

		wl.release();  //屏灯关闭

	}

	@Override
	public void onDestroy() {
		super.onDestroy();
	}

	private void showDialog(String title, String message) {
		MyDialog dialog = new MyDialog(RemindSoundActivity.this)
				.setTitle(title).setMessage(message)
				.setPositiveButton(R.string.ok, new View.OnClickListener() {

					@Override
					public void onClick(View arg0) {
						player.stop();
						finish();
					}
				})
				.setNegativeButton(R.string.cancel, new View.OnClickListener() {

					@Override
					public void onClick(View arg0) {
						player.stop();
						finish();
					}
				});

		dialog.create(null);
		dialog.showMyDialog();
	}
}

```
<h1 id="06">测量提醒页面 SetRemindCelingActivity </h1>  

## [返回目录](#0)

> ## 1. 日历的xml布局

```
 <!-- 运用相对布局来标定日历的位置 -->
    <RelativeLayout
        android:id="@+id/layout_calendar"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:background="@drawable/show_item_img"
        android:visibility="visible" >

        <TextView
            android:id="@+id/calendarCenter"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_centerHorizontal="true"
            android:layout_margin="8dp"
            android:textColor="@color/app_color"
            android:textSize="18dp" />

        <ImageButton
            android:id="@+id/calendarLeft"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignParentLeft="true"
            android:layout_marginLeft="30dp"
            android:background="@null"
            android:contentDescription="@null"
            android:padding="10dp"
            android:src="@drawable/arrow_remind_left_blue" />

        <ImageButton
            android:id="@+id/calendarRight"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignParentRight="true"
            android:layout_marginRight="30dp"
            android:background="@null"
            android:contentDescription="@null"
            android:padding="10dp"
            android:src="@drawable/arrow_remind_right_blue" />

        <com.yikang.heartmark.view.CalendarView
            android:id="@+id/calendar"
            android:layout_width="fill_parent"
            android:layout_height="match_parent"
            android:layout_alignParentLeft="true"
            android:layout_below="@+id/calendarCenter" />
    </RelativeLayout>
```
> ## 2. 自定义的日历控件  [canvas学习笔记](http://www.jianshu.com/p/f2e92bba4653)

```
package com.yikang.heartmark.view;

import java.util.Calendar;
import java.util.Date;

import android.annotation.SuppressLint;
import android.content.Context;
import android.graphics.Canvas;
import android.graphics.Color;
import android.graphics.Paint;
import android.graphics.Path;
import android.graphics.Typeface;
import android.util.AttributeSet;
import android.util.Log;
import android.view.MotionEvent;
import android.view.View;

/**
 * 日历控件 功能：获得点选的日期区间
 * 
 */
public class CalendarView extends View implements View.OnTouchListener {
	private final static String TAG = "anCalendar";
	private Date selectedStartDate;
	private Date selectedEndDate;
	private Date curDate; // 当前日历显示的月
	private Date today; // 今天的日期文字显示红色
	private Date downDate; // 手指按下状态时临时日期
	private Date showFirstDate, showLastDate; // 日历显示的第一个日期和最后一个日期
	private int downIndex; // 按下的格子索引
	private Calendar calendar;
	private Surface surface;
	private int[] date = new int[42]; // 日历显示数字
	private int curStartIndex, curEndIndex; // 当前显示的日历起始的索引
	private boolean completed = false; // 为false表示只选择了开始日期，true表示结束日期也选择了
	private boolean isSelectMore = false;
	//给控件设置监听事件
	private OnItemClickListener onItemClickListener;
	
	public CalendarView(Context context) {
		super(context);
		init();
	}

	public CalendarView(Context context, AttributeSet attrs) {
		super(context, attrs);
		init();
	}

	@SuppressLint("ClickableViewAccessibility")
	private void init() {
		curDate = selectedStartDate = selectedEndDate = today = new Date();
		calendar = Calendar.getInstance();
		//日历设置成现在的时间
		calendar.setTime(curDate);
		surface = new Surface();
		surface.density = getResources().getDisplayMetrics().density;
		setBackgroundColor(surface.bgColor);
		//对触摸事件进行监听
		setOnTouchListener(this);
	}

	@Override
	protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
		surface.width = getResources().getDisplayMetrics().widthPixels; //和屏幕同宽
		surface.height = (int) (getResources().getDisplayMetrics().heightPixels*2/5); //高是屏幕的40%
//		if (View.MeasureSpec.getMode(widthMeasureSpec) == View.MeasureSpec.EXACTLY) {
//			surface.width = View.MeasureSpec.getSize(widthMeasureSpec);
//		}
//		if (View.MeasureSpec.getMode(heightMeasureSpec) == View.MeasureSpec.EXACTLY) {
//			surface.height = View.MeasureSpec.getSize(heightMeasureSpec);
//		}
		widthMeasureSpec = View.MeasureSpec.makeMeasureSpec(surface.width,
				View.MeasureSpec.EXACTLY);
		heightMeasureSpec = View.MeasureSpec.makeMeasureSpec(surface.height,
				View.MeasureSpec.EXACTLY);
		setMeasuredDimension(widthMeasureSpec, heightMeasureSpec);
		super.onMeasure(widthMeasureSpec, heightMeasureSpec);
	}

	@Override
	protected void onLayout(boolean changed, int left, int top, int right,
			int bottom) {
		Log.d(TAG, "[onLayout] changed:"
				+ (changed ? "new size" : "not change") + " left:" + left
				+ " top:" + top + " right:" + right + " bottom:" + bottom);
		if (changed) {
			surface.init();
		}
		super.onLayout(changed, left, top, right, bottom);
	}

	@Override
	protected void onDraw(Canvas canvas) {
		Log.d(TAG, "onDraw");
		// 画框
		canvas.drawPath(surface.boxPath, surface.borderPaint);
		// 年月
		//String monthText = getYearAndmonth();
		//float textWidth = surface.monthPaint.measureText(monthText);
		//canvas.drawText(monthText, (surface.width - textWidth) / 2f,
		//		surface.monthHeight * 3 / 4f, surface.monthPaint);
		// 上一月/下一月
		//canvas.drawPath(surface.preMonthBtnPath, surface.monthChangeBtnPaint);
		//canvas.drawPath(surface.nextMonthBtnPath, surface.monthChangeBtnPaint);
		// 星期
		float weekTextY = surface.monthHeight + surface.weekHeight * 3 / 4f;
		// 星期背景
//		surface.cellBgPaint.setColor(surface.textColor);
//		canvas.drawRect(surface.weekHeight, surface.width, surface.weekHeight, surface.width, surface.cellBgPaint);
		for (int i = 0; i < surface.weekText.length; i++) {
			float weekTextX = i
					* surface.cellWidth
					+ (surface.cellWidth - surface.weekPaint
							.measureText(surface.weekText[i])) / 2f;
			canvas.drawText(surface.weekText[i], weekTextX, weekTextY,
					surface.weekPaint);
		}
		
		// 计算日期
		calculateDate();
		// 按下状态，选择状态背景色
		drawDownOrSelectedBg(canvas);
		// write date number
		// today index
		int todayIndex = -1;
		calendar.setTime(curDate);
		String curYearAndMonth = calendar.get(Calendar.YEAR) + ""
				+ calendar.get(Calendar.MONTH);
		calendar.setTime(today);
		String todayYearAndMonth = calendar.get(Calendar.YEAR) + ""
				+ calendar.get(Calendar.MONTH);
		if (curYearAndMonth.equals(todayYearAndMonth)) {
			int todayNumber = calendar.get(Calendar.DAY_OF_MONTH);
			todayIndex = curStartIndex + todayNumber - 1;
		}
		for (int i = 0; i < 42; i++) {
			int color = surface.textColor;
			if (isLastMonth(i)) {
				color = surface.borderColor;
			} else if (isNextMonth(i)) {
				color = surface.borderColor;
			}
			if (todayIndex != -1 && i == todayIndex) {
				color = surface.todayNumberColor;
			}
			drawCellText(canvas, i, date[i] + "", color);
		}
		super.onDraw(canvas);
	}

	private void calculateDate() {
		calendar.setTime(curDate);
		calendar.set(Calendar.DAY_OF_MONTH, 1);
		int dayInWeek = calendar.get(Calendar.DAY_OF_WEEK);
		Log.d(TAG, "day in week:" + dayInWeek);
		int monthStart = dayInWeek;
		if (monthStart == 1) {
			monthStart = 8;
		}
		monthStart -= 1;  //以日为开头-1，以星期一为开头-2
		curStartIndex = monthStart;
		date[monthStart] = 1;
		// last month
		if (monthStart > 0) {
			calendar.set(Calendar.DAY_OF_MONTH, 0);
			int dayInmonth = calendar.get(Calendar.DAY_OF_MONTH);
			for (int i = monthStart - 1; i >= 0; i--) {
				date[i] = dayInmonth;
				dayInmonth--;
			}
			calendar.set(Calendar.DAY_OF_MONTH, date[0]);
		}
		showFirstDate = calendar.getTime();
		// this month
		calendar.setTime(curDate);
		calendar.add(Calendar.MONTH, 1);
		calendar.set(Calendar.DAY_OF_MONTH, 0);
		// Log.d(TAG, "m:" + calendar.get(Calendar.MONTH) + " d:" +
		// calendar.get(Calendar.DAY_OF_MONTH));
		int monthDay = calendar.get(Calendar.DAY_OF_MONTH);
		for (int i = 1; i < monthDay; i++) {
			date[monthStart + i] = i + 1;
		}
		curEndIndex = monthStart + monthDay;
		// next month
		for (int i = monthStart + monthDay; i < 42; i++) {
			date[i] = i - (monthStart + monthDay) + 1;
		}
		if (curEndIndex < 42) {
			// 显示了下一月的
			calendar.add(Calendar.DAY_OF_MONTH, 1);
		}
		calendar.set(Calendar.DAY_OF_MONTH, date[41]);
		showLastDate = calendar.getTime();
	}

	/**
	 * 
	 * @param canvas
	 * @param index
	 * @param text
	 */
	private void drawCellText(Canvas canvas, int index, String text, int color) {
		int x = getXByIndex(index);
		int y = getYByIndex(index);
		surface.datePaint.setColor(color);
		float cellY = surface.monthHeight + surface.weekHeight + (y - 1)
				* surface.cellHeight + surface.cellHeight * 3 / 4f;
		float cellX = (surface.cellWidth * (x - 1))
				+ (surface.cellWidth - surface.datePaint.measureText(text))
				/ 2f;
		canvas.drawText(text, cellX, cellY, surface.datePaint);
	}

	/**
	 * 
	 * @param canvas
	 * @param index
	 * @param color
	 */
	private void drawCellBg(Canvas canvas, int index, int color) {
		int x = getXByIndex(index);
		int y = getYByIndex(index);
		surface.cellBgPaint.setColor(color);
		float left = surface.cellWidth * (x - 1) + surface.borderWidth;
		float top = surface.monthHeight + surface.weekHeight + (y - 1)
				* surface.cellHeight + surface.borderWidth;
		canvas.drawRect(left, top, left + surface.cellWidth
				- surface.borderWidth, top + surface.cellHeight
				- surface.borderWidth, surface.cellBgPaint);
	}

	private void drawDownOrSelectedBg(Canvas canvas) {
		// down and not up
		if (downDate != null) {
			drawCellBg(canvas, downIndex, surface.cellDownColor);
		}
		// selected bg color
		if (!selectedEndDate.before(showFirstDate)
				&& !selectedStartDate.after(showLastDate)) {
			int[] section = new int[] { -1, -1 };
			calendar.setTime(curDate);
			calendar.add(Calendar.MONTH, -1);
			findSelectedIndex(0, curStartIndex, calendar, section);
			if (section[1] == -1) {
				calendar.setTime(curDate);
				findSelectedIndex(curStartIndex, curEndIndex, calendar, section);
			}
			if (section[1] == -1) {
				calendar.setTime(curDate);
				calendar.add(Calendar.MONTH, 1);
				findSelectedIndex(curEndIndex, 42, calendar, section);
			}
			if (section[0] == -1) {
				section[0] = 0;
			}
			if (section[1] == -1) {
				section[1] = 41;
			}
			for (int i = section[0]; i <= section[1]; i++) {
				drawCellBg(canvas, i, surface.cellSelectedColor);
			}
		}
	}

	private void findSelectedIndex(int startIndex, int endIndex,
			Calendar calendar, int[] section) {
		for (int i = startIndex; i < endIndex; i++) {
			calendar.set(Calendar.DAY_OF_MONTH, date[i]);
			Date temp = calendar.getTime();
			// Log.d(TAG, "temp:" + temp.toLocaleString());
			if (temp.compareTo(selectedStartDate) == 0) {
				section[0] = i;
			}
			if (temp.compareTo(selectedEndDate) == 0) {
				section[1] = i;
				return;
			}
		}
	}

	public Date getSelectedStartDate() {
		return selectedStartDate;
	}

	public Date getSelectedEndDate() {
		return selectedEndDate;
	}

	private boolean isLastMonth(int i) {
		if (i < curStartIndex) {
			return true;
		}
		return false;
	}

	private boolean isNextMonth(int i) {
		if (i >= curEndIndex) {
			return true;
		}
		return false;
	}

	private int getXByIndex(int i) {
		return i % 7 + 1; // 1 2 3 4 5 6 7
	}

	private int getYByIndex(int i) {
		return i / 7 + 1; // 1 2 3 4 5 6
	}

	// 获得当前应该显示的年月
	public String getYearAndmonth() {
		calendar.setTime(curDate);
		int year = calendar.get(Calendar.YEAR);
		int month = calendar.get(Calendar.MONTH)+1;
		return year + "-" + month;
	}
	
	//上一月
	public String clickLeftMonth(){
		calendar.setTime(curDate);
		calendar.add(Calendar.MONTH, -1);
		curDate = calendar.getTime();
		invalidate();
		return getYearAndmonth();
	}
	//下一月
	public String clickRightMonth(){
		calendar.setTime(curDate);
		calendar.add(Calendar.MONTH, 1);
		curDate = calendar.getTime();
		invalidate();
		return getYearAndmonth();
	}
	
	//设置日历时间
	public void setCalendarData(Date date){
		calendar.setTime(date);
		curDate = selectedStartDate = selectedEndDate = date;
		invalidate();
	}
	
	//获取日历时间
	public void getCalendatData(){
		calendar.getTime();	
	}
	
	//设置是否多选
	public boolean isSelectMore() {
		return isSelectMore;
	}

	public void setSelectMore(boolean isSelectMore) {
		this.isSelectMore = isSelectMore;
	}

	private void setSelectedDateByCoor(float x, float y) {
		// change month
//		if (y < surface.monthHeight) {
//			// pre month
//			if (x < surface.monthChangeWidth) {
//				calendar.setTime(curDate);
//				calendar.add(Calendar.MONTH, -1);
//				curDate = calendar.getTime();
//			}
//			// next month
//			else if (x > surface.width - surface.monthChangeWidth) {
//				calendar.setTime(curDate);
//				calendar.add(Calendar.MONTH, 1);
//				curDate = calendar.getTime();
//			}
//		}
		// cell click down
		if (y > surface.monthHeight + surface.weekHeight) {
			int m = (int) (Math.floor(x / surface.cellWidth) + 1);
			int n = (int) (Math
					.floor((y - (surface.monthHeight + surface.weekHeight))
							/ Float.valueOf(surface.cellHeight)) + 1);
			downIndex = (n - 1) * 7 + m - 1;
			Log.d(TAG, "downIndex:" + downIndex);
			calendar.setTime(curDate);
			if (isLastMonth(downIndex)) {
				calendar.add(Calendar.MONTH, -1);
			} else if (isNextMonth(downIndex)) {
				calendar.add(Calendar.MONTH, 1);
			}
			calendar.set(Calendar.DAY_OF_MONTH, date[downIndex]);
			downDate = calendar.getTime();
		}
		invalidate();
	}

	@SuppressLint("ClickableViewAccessibility")
	@Override
	public boolean onTouch(View v, MotionEvent event) {
		switch (event.getAction()) {
		case MotionEvent.ACTION_DOWN:
			setSelectedDateByCoor(event.getX(), event.getY());
			break;
		case MotionEvent.ACTION_UP:
			if (downDate != null) {
				if(isSelectMore){
					if (!completed) {
						if (downDate.before(selectedStartDate)) {
							selectedEndDate = selectedStartDate;
							selectedStartDate = downDate;
						} else {
							selectedEndDate = downDate;
						}
						completed = true;
						//响应监听事件
						onItemClickListener.OnItemClick(selectedStartDate,selectedEndDate,downDate);
					} else {
						selectedStartDate = selectedEndDate = downDate;
						completed = false;
					}
				}else{
					selectedStartDate = selectedEndDate = downDate;
					//响应监听事件
					onItemClickListener.OnItemClick(selectedStartDate,selectedEndDate,downDate);
				}
				invalidate();
			}
			
			break;
		}
		return true;
	}
	
	//给控件设置监听事件
	public void setOnItemClickListener(OnItemClickListener onItemClickListener){
		this.onItemClickListener =  onItemClickListener;
	}
	//监听接口
	public interface OnItemClickListener {
		void OnItemClick(Date selectedStartDate,Date selectedEndDate, Date downDate);
	}

	/**
	 * 
	 * 1. 布局尺寸 2. 文字颜色，大小 3. 当前日期的颜色，选择的日期颜色
	 */
	private class Surface {
		public float density;
		public int width; // 整个控件的宽度
		public int height; // 整个控件的高度
		public float monthHeight; // 显示月的高度
		//public float monthChangeWidth; // 上一月、下一月按钮宽度
		public float weekHeight; // 显示星期的高度
		public float cellWidth; // 日期方框宽度
		public float cellHeight; // 日期方框高度	
		public float borderWidth;
		public int bgColor = Color.parseColor("#FFFFFF");
		private int textColor = Color.BLACK;
		//private int textColorUnimportant = Color.parseColor("#666666");
		private int btnColor = Color.parseColor("#666666");
		private int borderColor = Color.parseColor("#CCCCCC");
		public int todayNumberColor = Color.RED;
		public int cellDownColor = Color.parseColor("#00000000");
		public int cellSelectedColor = Color.parseColor("#99CCFF");
		public Paint borderPaint;
		public Paint monthPaint;
		public Paint weekPaint;
		public Paint datePaint;
		public Paint monthChangeBtnPaint;
		public Paint cellBgPaint;
		public Path boxPath; // 边框路径
		//public Path preMonthBtnPath; // 上一月按钮三角形
		//public Path nextMonthBtnPath; // 下一月按钮三角形
		public String[] weekText = { "周日","周一", "周二", "周三", "周四", "周五", "周六"};
		//public String[] monthText = {"Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"};
		   
		public void init() {
			float temp = height / 7f;
			monthHeight = 0;//(float) ((temp + temp * 0.3f) * 0.6);
			//monthChangeWidth = monthHeight * 1.5f;
			weekHeight = (float) ((temp + temp * 0.3f) * 0.7);
			cellHeight = (height - monthHeight - weekHeight) / 6f;
			cellWidth = width / 7f;
			borderPaint = new Paint();
			borderPaint.setColor(borderColor);
			borderPaint.setStyle(Paint.Style.STROKE);
			borderWidth = (float) (0.5 * density);
			// Log.d(TAG, "borderwidth:" + borderWidth);
			borderWidth = borderWidth < 1 ? 1 : borderWidth;
			borderPaint.setStrokeWidth(borderWidth);
			monthPaint = new Paint();
			monthPaint.setColor(textColor);
			monthPaint.setAntiAlias(true);
			float textSize = cellHeight * 0.4f;
			Log.d(TAG, "text size:" + textSize);
			monthPaint.setTextSize(textSize);
			monthPaint.setTypeface(Typeface.DEFAULT_BOLD);
			weekPaint = new Paint();
			weekPaint.setColor(textColor);
			weekPaint.setAntiAlias(true);
			float weekTextSize = weekHeight * 0.6f;
			weekPaint.setTextSize(weekTextSize);
			weekPaint.setTypeface(Typeface.DEFAULT_BOLD);
			datePaint = new Paint();
			datePaint.setColor(textColor);
			datePaint.setAntiAlias(true);
			float cellTextSize = cellHeight * 0.5f;
			datePaint.setTextSize(cellTextSize);
			datePaint.setTypeface(Typeface.DEFAULT_BOLD);
			boxPath = new Path();
			//boxPath.addRect(0, 0, width, height, Direction.CW);
			//boxPath.moveTo(0, monthHeight);
			boxPath.rLineTo(width, 0);
			boxPath.moveTo(0, monthHeight + weekHeight);
			boxPath.rLineTo(width, 0);
			for (int i = 1; i < 6; i++) {
				boxPath.moveTo(0, monthHeight + weekHeight + i * cellHeight);
				boxPath.rLineTo(width, 0);
				boxPath.moveTo(i * cellWidth, monthHeight);
				boxPath.rLineTo(0, height - monthHeight);
			}
			boxPath.moveTo(6 * cellWidth, monthHeight);
			boxPath.rLineTo(0, height - monthHeight);
			//preMonthBtnPath = new Path();
			//int btnHeight = (int) (monthHeight * 0.6f);
			//preMonthBtnPath.moveTo(monthChangeWidth / 2f, monthHeight / 2f);
			//preMonthBtnPath.rLineTo(btnHeight / 2f, -btnHeight / 2f);
			//preMonthBtnPath.rLineTo(0, btnHeight);
			//preMonthBtnPath.close();
			//nextMonthBtnPath = new Path();
			//nextMonthBtnPath.moveTo(width - monthChangeWidth / 2f,
			//		monthHeight / 2f);
			//nextMonthBtnPath.rLineTo(-btnHeight / 2f, -btnHeight / 2f);
			//nextMonthBtnPath.rLineTo(0, btnHeight);
			//nextMonthBtnPath.close();
			monthChangeBtnPaint = new Paint();
			monthChangeBtnPaint.setAntiAlias(true);
			monthChangeBtnPaint.setStyle(Paint.Style.FILL_AND_STROKE);
			monthChangeBtnPaint.setColor(btnColor);
			cellBgPaint = new Paint();
			cellBgPaint.setAntiAlias(true);
			cellBgPaint.setStyle(Paint.Style.FILL);
			cellBgPaint.setColor(cellSelectedColor);
		}
	}
}

```
> ## 3. 响应日历的点击事件

```
// 这个是对视图进行刷新
public void refreshView(){
		ArrayList<String> stringList = new ArrayList<String>();
		ArrayList<Alarm> alarmList = alarmDB.getAlarmListByType(Alarm.TYPE_CELING);
		if(alarmList.size()<=0){
			listView.setVisibility(View.GONE);
			imageview.setVisibility(View.VISIBLE);
		}else{
			imageview.setVisibility(View.GONE);
			listView.setVisibility(View.VISIBLE);
		}
		
		for(int i=0; i<alarmList.size(); i++){
			stringList.add(alarmList.get(i).time);
		}
		SetRemindCelingAdapter adapter = new SetRemindCelingAdapter(SetRemindCelingActivity.this, stringList);
		listView.setAdapter(adapter);
	}



//选择提醒的时间
	public void showCheckTime(){
		String	dateStr = DateUtil.getNowDate(DateUtil.DATE_HOUR_MINUTE);
		Date date = DateUtil.dateFromString(dateStr, DateUtil.DATE_HOUR_MINUTE);
		MyDialog dialog = new MyDialog(SetRemindCelingActivity.this).setTitle("请选择时间")
				.setTimePicker(date).setNegativeButton(R.string.cancel, null)
				.setPositiveButton(R.string.ok, new View.OnClickListener() {
					@Override
					public void onClick(View v) {
						WheelView wv_hour = (WheelView) v
								.findViewById(R.id.hour);
						WheelView wv_minute = (WheelView) v
								.findViewById(R.id.minute);
						String parten = "00";
						DecimalFormat decimal = new DecimalFormat(parten);
						String text = decimal.format(wv_hour.getCurrentItem())
								+ ":"
								+ decimal.format(wv_minute.getCurrentItem());
						
						Alarm alarm = new Alarm();
						alarm.type = Alarm.TYPE_CELING;
						long alarmTime = DateUtil.getLongOfDayTimeAll(calendarDate, text);
						if(alarmTime < DateUtil.getNowTimeInMillis()){
							ShowUtil.showToast(SetRemindCelingActivity.this, R.string.time_late);
							return;
						}else{
							alarm.alarmTime = alarmTime;
						}
						alarm.time = calendarDate + "  "+text;
						//查询是否已经设置当前时间
						ArrayList<Alarm> alarmList = alarmDB.getAlarmListByTime(Alarm.TYPE_CELING, alarm.time);
						if(alarmList.size() > 0){
							ShowUtil.showToast(SetRemindCelingActivity.this, R.string.alarm_repeat);
							return;
						}
						alarm.setTime = DateUtil.getNowTimeInMillis();
						alarm.isRepeat = false;
						Alarm.setRemind(alarmDB, alarm, alarmManager, SetRemindCelingActivity.this);
						
						refreshView();
					}
				});
		dialog.create(null).show();
	}


//对点击事件的监听器
	OnItemClickListener itemListener = new OnItemClickListener() {

		@Override
		public void OnItemClick(Date selectedStartDate, Date selectedEndDate,
				Date downDate) {
			if(calendar.isSelectMore()){
				//选择时间段
				//MyToast.show(getApplicationContext(), format.format(selectedStartDate)+"到"+format.format(selectedEndDate), Toast.LENGTH_SHORT);
			}else{
				//MyToast.show(getApplicationContext(), format.format(downDate), Toast.LENGTH_SHORT);
				calendarDate = format.format(downDate);
				showCheckTime();
			}
		}

	};


//注册监听器
		calendarLeft.setOnClickListener(new MyViewOnclicklistener());
		calendarRight.setOnClickListener(new MyViewOnclicklistener());
		calendar.setOnItemClickListener(itemListener);

```
<h1 id="07">用药提醒 SetRemindYaoActivity </h1>  

## [返回目录](#0)

> ## 1. [ExpandableListView--基本使用介绍](http://www.jianshu.com/p/05df9c17a1d8)

采用 ExpandableListView 显示数据，没有数据是显示一个友情提示.
这是具体的界面代码

```
 <ExpandableListView
        android:layout_below="@+id/setRemindYaoTopBar"
        android:id="@+id/set_remind_yao_listview"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:cacheColorHint="#00000000"
        android:divider="@null"
        android:groupIndicator="@null"
        android:listSelector="#00000000" 
        android:visibility="gone"
        >
    </ExpandableListView>
    
   <ImageView
        android:layout_below="@+id/setRemindYaoTopBar"
        android:id="@+id/setRemindYaoimageview"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="100dp"
        android:layout_centerHorizontal="true"
        android:layout_centerVertical="true"
        android:background="@drawable/setremindyaoimageview"
        android:visibility="gone"
         >
    </ImageView>
```
> ## 2. 列表的执行过程

```
@Override
	public void onResume() {
		super.onResume();
		refreshListView();
	}
	
	@Override
	public void onDestroy() {
		super.onDestroy();
		instance = null;
	}


//列表的数据的初始化
titleList = new ArrayList<String>();
//链表嵌套链表
		dataList = new ArrayList<ArrayList<String>>();


//筛选列表的数据
public void refreshListView(){
		titleList.clear();//标题数据
		dataList.clear();//内容数据
		ArrayList<Alarm> alarmList = null;
		//获得提醒数据的类别
		alarmList= alarmDB.getAlarmListByType(Alarm.TYPE_YAO);
		for(int i=0; i<alarmList.size(); i++){
			boolean isHave = false;//标记变量 每一次循环 都要初始化
			if(i == 0){//第一个标题 要加上
				titleList.add(alarmList.get(i).yaoType);
			}
			
			for(int k=0; k<titleList.size(); k++){
				if(alarmList.get(i).yaoType.equals(titleList.get(k))){
					isHave = true;
				}
			}
			
			if(!isHave){//如果标题不重复 就把这个标题加入链表中
				titleList.add(alarmList.get(i).yaoType);
			}
		}
		
		if(titleList.size()<=0){
			listView.setVisibility(View.GONE);
			imageview.setVisibility(View.VISIBLE);
		}else{
			imageview.setVisibility(View.GONE);
			listView.setVisibility(View.VISIBLE);
		}
		
		ArrayList<String> tempArray;
		for (int index = 0; index < titleList.size(); ++index) {
			tempArray = new ArrayList<String>();
			dataList.add(tempArray);
		}
		
		for(int k=0; k<titleList.size(); k++){
			alarmList.clear();
			//获得字列表的数据
			alarmList = alarmDB.getAlarmListByYaoType(Alarm.TYPE_YAO, titleList.get(k));
			// alarmList是提醒的个数
			for(int j=0; j<alarmList.size(); j++){
				boolean isHave = false;
				if(j == 0){//第一个直接加入药名
					dataList.get(k).add(alarmList.get(j).yaoName);
				}
				for(int y=0; y<dataList.get(k).size(); y++){
					if(alarmList.get(j).yaoName.equals(dataList.get(k).get(y))){
						isHave = true;
					}
				}
				if(!isHave){//分类下药名的数量
				dataList.get(k).add(alarmList.get(j).yaoName);
				}
			}
		}
		
		adapter = new SetRemindYaoAdapter(titleList, dataList,SetRemindYaoActivity.this);
		listView.setAdapter(adapter);
	}

```
> ## 3. 列表构造器的写法

```
package com.yikang.heartmark.adapter;

import java.util.ArrayList;

import android.annotation.SuppressLint;
import android.app.AlarmManager;
import android.content.Context;
import android.content.Intent;
import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.view.ViewGroup.LayoutParams;
import android.widget.BaseExpandableListAdapter;
import android.widget.ImageView;
import android.widget.LinearLayout;
import android.widget.TextView;

import com.example.heartmark.R;
import com.yikang.heartmark.activity.SetRemindYaoActivity;
import com.yikang.heartmark.activity.ZiXunDetailActivity;
import com.yikang.heartmark.database.AlarmDB;
import com.yikang.heartmark.database.YaoDB;
import com.yikang.heartmark.model.Alarm;
import com.yikang.heartmark.model.Yao;
import com.yikang.heartmark.model.ZiXun;

public class SetRemindYaoAdapter extends BaseExpandableListAdapter{
	private ArrayList<String> titleList;
	private ArrayList<ArrayList<String>> dataList;
	private Context context;
	private LayoutInflater layoutInflater = null;
	
    public SetRemindYaoAdapter(ArrayList<String> titleList, ArrayList<ArrayList<String>> dataList, Context context){
    	this.titleList = titleList;
    	this.dataList = dataList;
    	this.context = context;
    	layoutInflater = LayoutInflater.from(context);
    }
	@Override
	public int getGroupCount() {
		return titleList.size();
	}

	@Override
	public int getChildrenCount(int groupPosition) {
		int count = dataList.get(groupPosition).size();
		return count;
	}

	@Override
	public Object getGroup(int groupPosition) {
		return titleList.get(groupPosition);
	}

	@Override
	public Object getChild(int groupPosition, int childPosition) {
		return dataList.get(groupPosition).get(childPosition);
	}

	@Override
	public long getGroupId(int groupPosition) {
		return 0;
	}

	@Override
	public long getChildId(int groupPosition, int childPosition) {
		return childPosition;
	}

	@Override
	public boolean hasStableIds() {
		return false;
	}

	@SuppressLint("InflateParams")
	@Override
	public View getGroupView(int groupPosition, boolean isExpanded,
			View convertView, ViewGroup parent) {
		final ViewHolder holder;
		if(convertView == null){
			convertView = layoutInflater.inflate(R.layout.set_remind_yao_title_item, null);
			holder = new ViewHolder();
			
			TextView mateType = (TextView) convertView.findViewById(R.id.mate_type);
			TextView mateCount = (TextView) convertView.findViewById(R.id.mate_count);
			ImageView mateImg = (ImageView) convertView.findViewById(R.id.mate_title_image);
			
			holder.mateType = mateType;
			holder.mateCount = mateCount;
			holder.mateImg = mateImg;
			
			convertView.setTag(holder);
		}else{
			holder = (ViewHolder) convertView.getTag();
		}
		
	
		holder.mateType.setText(titleList.get(groupPosition));
		holder.mateCount.setText(String.valueOf(dataList.get(groupPosition).size()));
		
		if(isExpanded){
			holder.mateImg.setBackgroundResource(R.drawable.arrow_bottom);
		}else{
			holder.mateImg.setBackgroundResource(R.drawable.arrow_right);
		}
		
		return convertView;
	}

	
	@SuppressLint("InflateParams")
	@Override
	public View getChildView(int groupPosition, int childPosition,
			boolean isLastChild, View convertView, ViewGroup parent) {
		final ViewHolderData holder;
		if(convertView == null){
			convertView = layoutInflater.inflate(R.layout.set_remind_yao_data_item, null);
			holder = new ViewHolderData();
			
			TextView textName = (TextView) convertView.findViewById(R.id.set_remind_yao_data_name);
			TextView textExplain = (TextView) convertView.findViewById(R.id.set_remind_yao_data_explain);
			LinearLayout layoutTime = (LinearLayout) convertView.findViewById(R.id.set_remind_yao_data_time);
			LinearLayout textDelete = (LinearLayout) convertView.findViewById(R.id.set_remind_yao_data_delete);
			
			holder.textName = textName;
			holder.textExplain = textExplain;
			holder.layoutTime = layoutTime;
			holder.layoutDelete = textDelete;
			
			convertView.setTag(holder);
		}else{
			holder = (ViewHolderData) convertView.getTag();
		}
		
		holder.textName.setText(dataList.get(groupPosition).get(childPosition));
		ArrayList<Alarm> alarmList= new AlarmDB(context).getAlarmListByYaoTypeName(Alarm.TYPE_YAO,
				titleList.get(groupPosition), dataList.get(groupPosition).get(childPosition));
		ArrayList<String> timeList = new ArrayList<String>();
		holder.layoutTime.removeAllViews();
		//过滤出时间
		for(int i=0; i<alarmList.size(); i++){
			boolean isHave = false;
			LinearLayout.LayoutParams mLayoutParams = new LinearLayout.LayoutParams(  
			        LayoutParams.WRAP_CONTENT, LayoutParams.WRAP_CONTENT);
			if(i == 0){
				timeList.add(alarmList.get(i).time);
				TextView textView =new TextView(context);
				textView.setText(alarmList.get(i).time);
				holder.layoutTime.addView(textView,mLayoutParams);
			}
			
			for(int k=0; k<timeList.size(); k++){
				if(alarmList.get(i).time.equals(timeList.get(k))){
					isHave = true;
				}
			}
			
			if(!isHave){
				timeList.add(alarmList.get(i).time);
				TextView textView =new TextView(context);
				textView.setText(alarmList.get(i).time);
				holder.layoutTime.addView(textView,mLayoutParams);
			}
		}
		
        Yao yao = new YaoDB(context).getYaoListDetail
	              (titleList.get(groupPosition), dataList.get(groupPosition).get(childPosition));
		holder.textExplain.setOnClickListener(new MyViewOnclicklistener(yao.yaoId));
		holder.layoutDelete.setOnClickListener(new MyViewOnclicklistener(titleList.get(groupPosition),
				dataList.get(groupPosition).get(childPosition),null));
		return convertView;
	}

	class MyViewOnclicklistener implements View.OnClickListener {

		String yaoId; 
		String yaoType;
		String yaoName;
		public MyViewOnclicklistener(String yaoId) {
			this.yaoId = yaoId;
		}
		//第三个参数无意义,仅用于区分构造方法
		public MyViewOnclicklistener(String yaoType, String yaoName, String distinguishVoid) {
			this.yaoType = yaoType;
			this.yaoName = yaoName;
		}
		@Override
		public void onClick(View v) {
			final int rid = v.getId();
			switch (rid) {
			case R.id.set_remind_yao_data_explain:
				ZiXun zixun = new ZiXun();
				zixun.newId = yaoId;
				zixun.type = ZiXun.TYPE_EXPLAIN;
				Intent detailIntent = new Intent(context, ZiXunDetailActivity.class);
				Bundle bundle = new Bundle();
				bundle.putSerializable("newItem", zixun);
				detailIntent.putExtras(bundle);
				context.startActivity(detailIntent);
				break;
			case R.id.set_remind_yao_data_delete:
				AlarmDB alarmDB =new AlarmDB(context);
				AlarmManager alarmManager = (AlarmManager) SetRemindYaoActivity.instance.getSystemService(Context.ALARM_SERVICE);
				//关闭闹钟
				ArrayList<Alarm>  alarmList = alarmDB.getAlarmListByYaoTypeName(Alarm.TYPE_YAO,yaoType, yaoName);
				for(int i=0; i<alarmList.size(); i++){
					Alarm.closeRemind(alarmManager, context, alarmList.get(i).alarmId);
				}
				//删除数据库数据
				alarmDB.deleteByYaoTypeName(Alarm.TYPE_YAO ,yaoType, yaoName);
				//更新界面
				SetRemindYaoActivity.instance.refreshListView();
				break;
			default:
				break;
			}
		}
	}
	
	@Override
	public boolean isChildSelectable(int groupPosition, int childPosition) {
//        String content = null;
//        String contentText = null;
//        for(int i=0; i<yaoList.size(); i++){
//        	if(yaoList.get(i).type.equals(titleList.get(groupPosition))
//        			&& yaoList.get(i).name.equals(dataList.get(groupPosition).get(childPosition))){
//        		content = yaoList.get(i).content;
//        		contentText = yaoList.get(i).contentText;
//        	}
//        }
//        
//		Intent detailIntent = new Intent(context, ZiXunDetailActivity.class);
//		detailIntent.putExtra("webxml", content);
//		detailIntent.putExtra("readtext", contentText);
//		context.startActivity(detailIntent);
		return false;
	}

	
	static class ViewHolder {
			TextView mateType;
			TextView mateCount;
			ImageView mateImg;
	 }
	static class ViewHolderData{
		   TextView textName;
		   TextView textExplain; //说明
		   LinearLayout layoutTime;  //time View
		   LinearLayout layoutDelete;
	}
	 
}

```
<h1 id="10">10. 点击药品说明书 出现的详情页面  ZiXunDetailActivity </h1>  

## [返回目录](#0)

> ## 1. 标题的区分 包括点赞和收藏的显示

```
zixun = (ZiXun) intent.getSerializableExtra("newItem");

		refreseData(topbar);


private void refreseData(TopBarView topbar) {
		//如果状态是咨询
		if (zixun.type.equals(ZiXun.TYPE_ZIXUN)) {
			// 如果数据库里已经点赞，在点赞按钮不能点击
			if (goodDB.isHave(zixun.newId)) {
				buttonGood.setSelected(true);
				buttonGood.setClickable(false);
			} else {
				buttonGood.setSelected(false);
				buttonGood.setClickable(true);
			}

			// 查看数据库的状态是否收藏
			if (zixun.house.equals("1")) {
				buttonHouse.setSelected(true);
			} else {
				buttonHouse.setSelected(false);
			}
		} else if (zixun.type.equals(ZiXun.TYPE_EXPLAIN)) {
			topbar.setRightButtonVisible(false);
			buttonGood.setVisibility(View.GONE);
			buttonHouse.setVisibility(View.GONE);
		}
	}
```
> ## 2. 显示药品说明书的流程

```
if (zixun.type.equals(ZiXun.TYPE_ZIXUN)) {
			handlerBase.sendEmptyMessage(ConstantUtil.DIALOG_SHOW);
			Map<String, String> params = new HashMap<String, String>();
			params.put("newsId", zixun.newId);
			ConnectionManager.getInstance().send("FN11050WL00",
					"queryNewsDetailById", params, "detailCallBackHandler",this);
		} else if (zixun.type.equals(ZiXun.TYPE_EXPLAIN)) {
			handlerBase.sendEmptyMessage(ConstantUtil.DIALOG_SHOW);
			Map<String, String> params = new HashMap<String, String>();
			params.put("drugId", zixun.newId);
			ConnectionManager.getInstance().send("CM01090WD00",
					"queryDrugInfoById", params, "yaoDetailCallBack", this);
			// String body = zixun.content;
			// String showBody = null;
			// if(body != null && !body.equals("")){
			// showBody = body.replace("upload",
			// ConnectUtil.HOST_URL+"/upload");
			// }else{
			// showBody = body;
			// }
			//
			// webView.loadDataWithBaseURL(null, showBody, "text/html",
			// "utf-8",null);
		}



// 药品说明书详情
	@SuppressWarnings("rawtypes")
	public void yaoDetailCallBack(Object data) {
		handlerBase.sendEmptyMessage(ConstantUtil.DIALOG_HINT);
		Map resultMap = (Map) data;
		if (resultMap == null) {
			ShowUtil.showToast(ZiXunDetailActivity.this,
					R.string.check_network_timeout);
		} else {
			String body = (String) resultMap.get("CONTENT");
			String showBody = null;
			if (body != null && !body.equals("")) {
				//用一个新的字符串替代老的字符串
				showBody = body.replace("upload", ConnectUtil.HOST_URL+ "/upload");
			} else {
				showBody = body;
			}
			//用webView显示一个字符串
			webView.loadDataWithBaseURL(null, showBody, "text/html", "utf-8",null);
			zixun.contentRead = (String) resultMap.get("CONTENT_TEMP");
		}
	}
```
> ## 3. 有声朗读的实现

```
/**
	 * 语音播报
	 * 
	 * @param context
	 * @param buttonYuYin2
	 */
	private void playSound(Button buttonYuYin) {
		playSound.playSound(zixun.contentRead, buttonYuYin);
	}


//有声朗读的工具类
package com.yikang.heartmark.util;

import android.content.Context;
import android.os.Bundle;
import android.widget.Button;
import android.widget.Toast;

import com.iflytek.cloud.ErrorCode;
import com.iflytek.cloud.InitListener;
import com.iflytek.cloud.SpeechConstant;
import com.iflytek.cloud.SpeechError;
import com.iflytek.cloud.SpeechSynthesizer;
import com.iflytek.cloud.SynthesizerListener;

public class PlaySoundUtil {
	private Context context;
	private SpeechSynthesizer mTts;
	private boolean isFinish = true;   //播完状态
	private boolean isPause = false;   //不在暂停状态

	public PlaySoundUtil(Context context) {
		this.context = context;
		// 初始化合成对象
		mTts = SpeechSynthesizer.createSynthesizer(context, mTtsInitListener);
	}

	// 初始化监听
	private InitListener mTtsInitListener = new InitListener() {
		@Override
		public void onInit(int code) {
			if (code != ErrorCode.SUCCESS) {
				//MyToast.show(context, "初始化失败,错误码：" + code, Toast.LENGTH_SHORT);
			}
		}
	};

	//播放文本
	public void playSound(String text, Button buttonYuYin) {
//如果是播放状态和不在暂停状态
		if(isFinish && !isPause){
			setParam();//参数设置
			int code = mTts.startSpeaking(text, mTtsListener);
			if (code != ErrorCode.SUCCESS) {
				MyToast.show(context, "播放失败,请重试", Toast.LENGTH_SHORT);
				buttonYuYin.setBackgroundResource(com.example.heartmark.R.drawable.yishi_chat_yuyin_no);
			}else{//如果返回码是成功
				isFinish = false;
				buttonYuYin.setBackgroundResource(com.example.heartmark.R.drawable.yishi_chat_yuyin_yes);
			}
		}else if(!isFinish && !isPause){//如果不是播放状态和不在暂停状态
			mTts.pauseSpeaking();
			isPause = true;
			buttonYuYin.setBackgroundResource(com.example.heartmark.R.drawable.yishi_chat_yuyin_no);
			
		}else if(!isFinish && isPause){//如果不是播放状态和在暂停状态
			mTts.resumeSpeaking();
			isPause = false;
			buttonYuYin.setBackgroundResource(com.example.heartmark.R.drawable.yishi_chat_yuyin_yes);
		}
	}
	
	public void stopSound(){
		mTts.stopSpeaking();
		// 退出时释放连接
		mTts.destroy();
		
		isPause = false;
		isFinish = true;
	}
	
	
	/**
	 * 合成回调监听。
	 */
	private SynthesizerListener mTtsListener = new SynthesizerListener() {
		@Override
		public void onSpeakBegin() {
		//	showTip("开始播放");
		}

		@Override
		public void onSpeakPaused() {
		//	showTip("暂停播放");
		}

		@Override
		public void onSpeakResumed() {
		//	showTip("继续播放");
		}

		@Override
		public void onBufferProgress(int percent, int beginPos, int endPos,
				String info) {
			//缓存进度
//			mPercentForBuffering = percent;
//			showTip(String.format(getString(R.string.tts_toast_format),
//					mPercentForBuffering, mPercentForPlaying));
		}

		@Override
		public void onSpeakProgress(int percent, int beginPos, int endPos) {
			//播放进度
//			mPercentForPlaying = percent;
//			showTip(String.format(getString(R.string.tts_toast_format),
//					mPercentForBuffering, mPercentForPlaying));
		}

		@Override
		public void onCompleted(SpeechError error) {
			if(error == null)
			{
			//	showTip("播放完成");
				isFinish = true;
			}
			else if(error != null)
			{
		        showTip(error.getPlainDescription(true));
			}
		}

		@Override
		public void onEvent(int eventType, int arg1, int arg2, Bundle obj) {
			
		}
	};

	private void showTip(String text){
		//MyToast.show(context, text, Toast.LENGTH_LONG);
	}
	

	//参数设置
	private void setParam() {
		// 清空参数
		mTts.setParameter(SpeechConstant.PARAMS, null);
		// 设置合成
		mTts.setParameter(SpeechConstant.ENGINE_TYPE, SpeechConstant.TYPE_CLOUD);
		// 设置发音人
		mTts.setParameter(SpeechConstant.VOICE_NAME, 
				"xiaoyan");

		// 设置语速
		mTts.setParameter(SpeechConstant.SPEED,"50");

		// 设置音调
		mTts.setParameter(SpeechConstant.PITCH,"50");

		// 设置音量
		mTts.setParameter(SpeechConstant.VOLUME,"50");

		// 设置播放器音频流类型
		mTts.setParameter(SpeechConstant.STREAM_TYPE,"3");

	}
}

```
> ## 4. 点赞的实施

```
/**
	 * 点赞
	 */
	private void doGood() {
		//判断网络是否连接
		if (!ConnectUtil.isConnect(ZiXunDetailActivity.this)) {
			ShowUtil.showToast(ZiXunDetailActivity.this, R.string.check_network);
			return;
		}
		Map<String, String> params = new HashMap<String, String>();
		params.put("newsId", zixun.newId);
		ConnectionManager.getInstance().send("FN11050WL00", "updateNewsPraise",
				params, "goodCallBackHandler", this);
	}

	@SuppressWarnings("rawtypes")
	public void goodCallBackHandler(Object data) {
		Map resultMap = (Map) data;
		// 网络连接超时
		if (resultMap == null) {
			ShowUtil.showToast(ZiXunDetailActivity.this,
					R.string.check_network_timeout);
		} else {
			String result = (String) resultMap.get("head");
			if (result.equals("success")) {
				ShowUtil.showToast(ZiXunDetailActivity.this,R.string.good_success);
				buttonGood.setSelected(true);
				buttonGood.setClickable(false);
				//如果点赞成功则点赞表中加入一个id
				new GoodDB(ZiXunDetailActivity.this).insertGood(zixun.newId);
			} else if (result.equals("fail")) {
				ShowUtil.showToast(ZiXunDetailActivity.this, R.string.good_fail);
			}
		}
	}
```
> ## 5. 还有就是收藏和取消收藏，类似
> ## 5. 还有就是分享

```
	@Override
	public void onTopbarRightButtonSelected() {
		showShare("心衰管理", zixun.newId);
	}


/**
	 * 分享客户端
	 * 
	 * @param contextString
	 * @param newId
	 */
	private void showShare(String contextString, String newId) {
		ShareSDK.initSDK(this);

		String url = ConnectUtil.HOST_URL
				+ "FI01080WD00P!querySbtNewsDetailPages.htm?uuid=" + newId;
		OnekeyShare oks = new OnekeyShare();
		// 分享时Notification的图标和文字
		oks.setNotification(R.drawable.heart_mark_icon,
				this.getString(R.string.app_name));
		// oks.setAddress("12345678901");// address是接收人地址，仅在信息和邮件使用
		// oks.setTitle(this.getString(R.string.share)); //
		// title标题，印象笔记、邮箱、信息、微信、人人网和QQ空间使用
		// oks.setTitleUrl("http://sharesdk.cn"); //
		// titleUrl是标题的网络链接，仅在人人网和QQ空间使用
		// text是分享文本，所有平台都需要这个字段
		oks.setText(contextString + url);
		// oks.setImagePath(MainActivity.TEST_IMAGE);//
		// imagePath是图片的本地路径，Linked-In以外的平台都支持此参数
		// imageUrl是图片的网络路径，新浪微博、人人网、QQ空间、
		// 微信的两个平台、Linked-In支持此字段
		// oks.setImageUrl("http://img.appgo.cn/imgs/sharesdk/content/2013/07/25/1374723172663.jpg");
		// url仅在微信（包括好友和朋友圈）中使用
		oks.setUrl(url);
		// appPath是待分享应用程序的本地路劲，仅在微信中使用
		// oks.setAppPath(MainActivity.TEST_IMAGE);
		// comment是我对这条分享的评论，仅在人人网和QQ空间使用
		// oks.setComment(getContext().getString(R.string.share));
		// site是分享此内容的网站名称，仅在QQ空间使用
		oks.setSite(this.getString(R.string.app_name));
		// siteUrl是分享此内容的网站地址，仅在QQ空间使用
		oks.setSiteUrl(url);
		// venueName是分享社区名称，仅在Foursquare使用
		// oks.setVenueName("Southeast in China");
		// venueDescription是分享社区描述，仅在Foursquare使用
		// oks.setVenueDescription("This is a beautiful place!");
		// latitude是维度数据，仅在新浪微博、腾讯微博和Foursquare使用
		// oks.setLatitude(23.122619f);
		// longitude是经度数据，仅在新浪微博、腾讯微博和Foursquare使用
		// oks.setLongitude(113.372338f);
		// 是否直接分享（true则直接分享）
		oks.setSilent(true);
		// 指定分享平台，和slient一起使用可以直接分享到指定的平台
		// if (platform != null) {
		// oks.setPlatform(platform);
		// }
		// 去除注释可通过OneKeyShareCallback来捕获快捷分享的处理结果
		// oks.setCallback(new OneKeyShareCallback());
		// 通过OneKeyShareCallback来修改不同平台分享的内容
		// oks.setShareContentCustomizeCallback(
		// new ShareContentCustomizeDemo());
		oks.show(this);
	}
```

<h1 id="11">数据库的思路 </h1>  

## [返回目录](#0)

> ## 1. 点赞单独放在一个表里，把咨询的id存入表中goodId字段下。 

<h1 id="12">添加用药提醒  YongYaoAddActivity </h1>  

## [返回目录](#0)

> ## 1. 页面的使用技巧

```
//表示加号和减号
 <RelativeLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_below="@+id/yongyao_add_time"
                android:layout_marginTop="10dp" >

                <Button
                    android:id="@+id/yongyao_add_time_min"
                    android:layout_width="40dp"
                    android:layout_height="40dp"
                    android:layout_marginLeft="20dp"
                    android:background="@drawable/yongyao_min_img" />

                <Button
                    android:id="@+id/yongyao_add_time_add"
                    android:layout_width="40dp"
                    android:layout_height="40dp"
                    android:layout_alignParentRight="true"
                    android:layout_marginRight="20dp"
                    android:background="@drawable/yongyao_add_img" />
            </RelativeLayout>



// 这个是星期的表示方法 选中和没选中两种状态
 <LinearLayout
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:gravity="center" >

            <CheckBox
                android:id="@+id/set_remind_yao_check7"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:background="@drawable/zhouri_selector"
                android:button="@null" />
        </LinearLayout>

//选择器
<?xml version="1.0" encoding="utf-8"?>
<selector
  xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:state_checked="true" android:drawable="@drawable/zhouer_yes" />
    <item android:state_checked="false" android:drawable="@drawable/zhouer_no" />
    <item android:drawable="@drawable/zhouer_no" />
</selector>
```
> ## 2. 设置闹钟的过程

```
public void doSave(){
		if(addType.getText().toString() == null || addType.getText().toString().equals("")){
			ShowUtil.showToast(instance, R.string.choose_type);
			return;
		}
		
		if(addName.getText().toString() == null || addName.getText().toString().equals("")){
			ShowUtil.showToast(instance, R.string.choose_name);
			return;
		}
		
		if( !haveTime){
			ShowUtil.showToast(instance, R.string.choose_time);
			return;
		}
		
		boolean isChooseWeek = false;
		for(int i=0; i < checkList.size(); i++){
			if(checkList.get(i).isChecked()){
				isChooseWeek = true;
			}
		}
		
		if(!isChooseWeek){
			ShowUtil.showToast(instance, R.string.choose_week);
			return;
		}
		
		Alarm alarm = new Alarm();
		for(int i=0; i<checkList.size(); i++){
			if(checkList.get(i).isChecked()){//选中了星期几
				for(int k=0; k<timeList.size(); k++){//设置了时间的信息
					if(timeList.get(k) != null && !timeList.get(k).equals("")){
						int day = 0;//这个是时间的差值
						//获取现在的时间信息
						String yearMonthDay = DateUtil.getNowDate(DateUtil.YEAR_MONTH_DAY);
						if(i+1 < week){
							day = 7-(week-(i+1));
						}
						else if(i+1 == week){
							day =0;
						}
						else if(i+1 > week){
							day = i+1 - week;
						}
						
						alarm.type = Alarm.TYPE_YAO;
						// 闹钟响起的时间的毫秒值
						alarm.alarmTime = DateUtil.getLongOfDayTimeAll(yearMonthDay,timeList.get(k)) + day*DateUtil.DAY_MILLIS;
						alarm.setTime = DateUtil.getNowTimeInMillis();
						alarm.time = timeList.get(k);
						alarm.week = weekList[i];
						alarm.isRepeat = true;
						alarm.repeatTime = DateUtil.WEEK_MILLIS;
						alarm.yaoName = addName.getText().toString();
						alarm.yaoType = addType.getText().toString();
						Alarm.setRemind(alarmDB, alarm, alarmManager, instance);
					}
				}
			}
		}
		
		ShowUtil.showToast(instance, R.string.save_success);
		finish();
	}



//AlarmManager  闹钟管理器	 将闹钟存储到数据库  并发送意图
	public static void setRemind(AlarmDB alarmDB, Alarm alarm,AlarmManager alarmManager, Context context) {
		
		String timeStr = String.valueOf(alarm.setTime);
		// 取出时间的最后8位数字
		alarm.alarmId = Integer.valueOf(timeStr.substring(timeStr.length() - 8,timeStr.length()));
		
		alarmDB.insertAlarm(alarm);
		
		//将闹钟对象的信息  放到Intent中  发送给RemindReceiver这个广播接受器
		Intent intent = new Intent();
		
		Bundle bundle = new Bundle();
		bundle.putSerializable("alarm", alarm);
		intent.putExtras(bundle);
		
		intent.setClass(context, RemindReceiver.class);
		
		//这是一个定时的意图     全局定时器
		PendingIntent pi = PendingIntent.getBroadcast(context, alarm.alarmId,intent, PendingIntent.FLAG_UPDATE_CURRENT);
		
		if (alarm.isRepeat) {//如果这是一个循环闹钟
			//早于当前时间，到下周开始提醒
			if(alarm.alarmTime < DateUtil.getNowTimeInMillis()){
				alarm.alarmTime = alarm.alarmTime + DateUtil.WEEK_MILLIS;
			}
			//闹钟管理器  定时去发送一个定时的任务  重复闹钟的设置方法
			alarmManager.setRepeating(AlarmManager.RTC_WAKEUP, alarm.alarmTime,alarm.repeatTime, pi);
		} else {//非重复闹钟
			//晚于当前时间的闹钟，才设置提醒
			if(alarm.alarmTime > DateUtil.getNowTimeInMillis()){
				alarmManager.set(AlarmManager.RTC_WAKEUP, alarm.alarmTime, pi);
			}
		}
	}

```
> ## 3. 提醒的字段的定义

```
public int id;
	public String type; // 区分测量，用药，护理等;不可为空
	public int alarmId; // 闹钟唯一标志    设置闹钟的时间的最后八位
	public long alarmTime; // 闹钟响起的时间的毫秒值
	public String time; // 字符串形式的时间,用于回显
	public String week; // 用于显示重复时间，列：周一||周二...
	public long repeatTime; // 循环周期 ---- 不存数据库 ----
	public int yaoId; // 药的id
	public String yaoName; // 药的名字
	public String yaoType; //药的类型
	public long setTime; // 设置闹钟的时间，用于区分时间相同的俩个闹钟
	public boolean isRepeat; // 是否循环 ---- 不存数据库 ----;不可为空
```
<h1 id="13">护理任务提醒  SetRemindHuliActivity</h1>  

## [返回目录](#0)

> ## 1. 过滤列表显示的数据

```
public void refreshView(){
		ArrayList<String> timeList = new ArrayList<String>();
		ArrayList<String> weekList = new ArrayList<String>();
		ArrayList<Alarm> alarmList = alarmDB.getAlarmListByType(Alarm.TYPE_HULI);
		
		//过滤时间
		for(int i=0; i<alarmList.size(); i++){
			boolean isHave = false;
			if(i == 0){
				timeList.add(alarmList.get(i).time);
			}
			
			for(int k=0; k<timeList.size(); k++){
				if(alarmList.get(i).time.equals(timeList.get(k))){
					isHave = true;
				}
			}
			//重复的数据不在添加
			if(!isHave){
				timeList.add(alarmList.get(i).time);
			}
		}
	 
		if(timeList.size()<=0){
			listView.setVisibility(View.GONE);
			imageview.setVisibility(View.VISIBLE);
		}else{
			imageview.setVisibility(View.GONE);
			listView.setVisibility(View.VISIBLE);
		}
		
		//过滤重复周期
		for(int i=0; i<timeList.size(); i++){
			ArrayList<Alarm> alarms = alarmDB.getAlarmListByTime(Alarm.TYPE_HULI, timeList.get(i));
			String weeks = "";
			for(int k=0; k<alarms.size(); k++){
				weeks += alarms.get(k).week+",";
			}
			//把最后一个逗号去掉
			weekList.add(weeks.substring(0, weeks.length() - 1));
		}
		
		SetRemindHuliAdapter adapter = new SetRemindHuliAdapter(SetRemindHuliActivity.this, timeList, weekList);
		listView.setAdapter(adapter);
	}
```
<h1 id="14">添加护理任务提醒  SetRemindHuliAddActivity</h1>  

## [返回目录](#0)

> ## 1. [Math 以及 DecimalFormat 学习总结](http://www.jianshu.com/p/a506dcc1f917)
[【造轮子系列】转轮选择工具——WheelView](http://www.jianshu.com/p/4b3e2373d0e2)

设置闹钟的操作

```
View.OnClickListener listener = new View.OnClickListener() {
		@Override
		public void onClick(View v) {
			//检查是否全没有选择
			boolean isChooseWeek = false;
			for(int i=0; i < checkList.size(); i++){
				if(checkList.get(i).isChecked()){
					isChooseWeek = true;
				}
			}
			
			if(!isChooseWeek){
				ShowUtil.showToast(instance, R.string.choose_week);
				return;
			}
			
			
			
			String parten = "00";
			DecimalFormat decimal = new DecimalFormat(parten);
			String text = decimal.format(wv_hour.getCurrentItem())
					+ ":"
					+ decimal.format(wv_minutes.getCurrentItem());
			//查询是否已经设置当前时间
			ArrayList<Alarm> alarmList = alarmDB.getAlarmListByTime(Alarm.TYPE_HULI, text);
			if(alarmList.size() > 0){
				ShowUtil.showToast(SetRemindHuliAddActivity.this, R.string.alarm_repeat);
				return;
			}
			
			Alarm alarm = new Alarm();
			for(int i=0; i<checkList.size(); i++){
				if(checkList.get(i).isChecked()){
							int day = 0;   //跟今日对比,多少天后开始提醒
							String yearMonthDay = DateUtil.getNowDate(DateUtil.YEAR_MONTH_DAY);
							if(i+1 < week){
								day = 7-(week-(i+1));
							}
							else if(i+1 == week){
								day =0;
							}
							else if(i+1 > week){
								day = i+1 - week;
							}
							
							alarm.type = Alarm.TYPE_HULI;
							alarm.alarmTime = DateUtil.getLongOfDayTimeAll(yearMonthDay, text) + day*DateUtil.DAY_MILLIS;
							alarm.setTime = DateUtil.getNowTimeInMillis();
							alarm.time = text;
							alarm.week = weekList[i];
							alarm.isRepeat = true;
							alarm.repeatTime = DateUtil.WEEK_MILLIS;
							Alarm.setRemind(alarmDB, alarm, alarmManager, instance);
				}
			}
			
			ShowUtil.showToast(instance, R.string.save_success);
			finish();
		}
	};
```
> ## 2. 设置滚轮显示的数字

```
public void setTimePicker(Date date) {
		int hour = 0;
		int minutes = 0;

		Calendar calendar = Calendar.getInstance();

		if (date != null)
			calendar.setTime(date);

		hour = calendar.get(Calendar.HOUR_OF_DAY);
		minutes = calendar.get(Calendar.MINUTE);

		// 时
		wv_hour = (WheelView) findViewById(R.id.set_remind_huli_add_hour);
		wv_hour.setAdapter(new NumericWheelAdapter(0, 23));
		wv_hour.setCyclic(true);// 可循环滚动
		wv_hour.setLabel("时");// 添加文字
		wv_hour.setCurrentItem(hour);// 初始化时显示的数据

		// 分
		wv_minutes = (WheelView)findViewById(R.id.set_remind_huli_add_minute);
		wv_minutes.setAdapter(new NumericWheelAdapter(0, 59));
		wv_minutes.setCyclic(true);
		wv_minutes.setLabel("分");
		wv_minutes.setCurrentItem(minutes);

		// 根据屏幕密度来指定选择器字体的大小
		int textSize = 40;

		wv_hour.TEXT_SIZE = textSize;
		wv_minutes.TEXT_SIZE = textSize;

	}
```
<h1 id="15">15. 智能检测界面  MainCeLingActivity</h1>  

## [返回目录](#0)

> ## 1. 相关的知识链接

```
```
> ## 2. 参考模式

```
//打印日志
	private static final String TAG = "MainCeLingActivity";
	//单例模式
	public static MainCeLingActivity instance;


	//由于onDestroy耗时,所以我们需要在onDestroy之前执行下面代码。
	public void destroy(){
		instance = null;
		unregisterReceiver(receiverBluetooth);
		SharedPreferenceUtil.setBoolean(MainCeLingActivity.this,ConstantUtil.CELING_DESTORY, true);
	}


public static MainCeLingActivity getInstance(){
		if(instance != null){
			return instance;
		}else{
			return new MainCeLingActivity();
		}
	}

instance = this;
```
> ## 3. 类反射

```
Method createBondMethod = BluetoothDevice.class.getMethod("createBond");
				createBondMethod.invoke(bluetoothDevice); 
```
> ## 4. 常规参数

```
// 蓝牙通讯流
	private OutputStream mOutputStream;
	private InputStream mInInputStream;

/*表示本地蓝牙适配器（蓝牙无线电广播）。
	BluetoothAdapter是所有蓝牙交互的入口点。
	你能够通过它发现其它蓝牙设备，查询一系列已经匹配的设备，
	使用已知的MAC地址实例化一个 BluetoothDevice，
	创建 BluetoothServerSocket 监听来自其他设备的通信。*/
	private BluetoothAdapter bluetoothAdapter;
	/*表示远程蓝牙设备。用这个类通过 BluetoothSocket
	 * 能够请求同远程设备的链接，或者查询设备的名字、
	 * 地址、类和绑定状态。*/
	private BluetoothDevice bluetoothDevice;
	//设备的连接线路
	private BluetoothSocket bluetoothSocket;

	public static final String BLUETOOTH_SPP = "0F:03:14:C2:00:25"; // 蓝牙spp地址
	public static final String BLUETOOTH_BLE = "0F:04:14:C2:00:25"; // 蓝牙ble地址
	// private static final String TEST_OUTER= "SetSerial:'"; // 机外发送设备头
	private static final String TEST_IN = "SetIn:'"; // 机内发送设备头
	
	/*关于UUID   通用唯一标识符（UUID）是为字符串ID而生成的标准化128bit格式，
	 * 用于唯一标示信息。UUID的关键点是它足够大，
	 * 以至于你任意随即选择都不会产生冲突。
	 * 在此情况中，它被用于标识你应用的蓝牙服务。
	 * 为了获得一个你的应用可以使用的UUID，
	 * 你可以从众多的UUID生成器中任意选择一个，
	 * 然后通过fromString(String)实例化一个UUID。*/
	private static final String SPP_UUID = "00001101-0000-1000-8000-00805F9B34FB";

```
> ## 5. 收消息线程

```
// 收消息线程
	private class ReceiveMessageThread extends Thread {
		@Override
		public void run() {
			// synchronized (mLockObj) {

			if (bluetoothSocket != null) {

				try {//从连接中获取输入流
					mInInputStream = bluetoothSocket.getInputStream();

					byte[] buffer = null;
					int len = 0;

					while (isReceiveMessage) {

						buffer = new byte[1024];

						if (mInInputStream != null&& mInInputStream.available() > 0) {
							len = mInInputStream.read(buffer);
						} else {
							len = 0;
						}

						// 发送过程中数据为13字节，（发送过程中，有可能每次不是13个字节，4个字节
						// 9个字节两次发）发生丢包数据
						for (int i = 0; i < len; i++) {
							Log.d(null, (buffer[i]) + "=======>len=" + len);
						}

						if (len > 0) {
							byte[] buf_data = new byte[len];
							for (int i = 0; i < len; i++) {
								buf_data[i] = buffer[i];
							}
							String msg = new String(buf_data);
							//等到消息接受完成，在发送出去
							if (msg.indexOf("READY") != -1|| msg.indexOf("QROK") != -1) {
								//接受到的信息叠加
								sppHandler.obtainMessage(receive_message, len,-1, msg).sendToTarget();
							} else {
								receiveResult = receiveResult + msg;
								if (receiveResult.indexOf("#") != -1) {
									sppHandler.obtainMessage(receive_message,len, -1, receiveResult).sendToTarget();
									receiveResult = "";
								}

							}

						}

						try {
							Thread.sleep(SLEEP_RECEIVE_TIME);
						} catch (InterruptedException e) {
							e.printStackTrace();
						}

					}
				} catch (IOException e) {
					e.printStackTrace();

					// sppHandler.sendEmptyMessage(MSG_MEASURE_EXCEPTION_FAIL);
				}
			} else {
				// sppHandler.sendEmptyMessage(MSG_MEASURE_EXCEPTION_FAIL);
			}
		}
	}

```
> ## 6. 此handler只用于跟蓝牙通讯

```
// 此handler只用于跟蓝牙通讯
	public final Handler sppHandler = new Handler() {
		public void handleMessage(Message msg) {

			switch (msg.what) {
			case connect_success:
				//关闭进度条
				handlerBase.sendEmptyMessage(ConstantUtil.DIALOG_HINT);
				stopConnectTimer();
				startReceiveMessageThread();
				// 告诉设备
				if (isGetResult) {
					// 上次没有测量完成，直接获取结果
					String sendValue = "GetDate\r\n";
					byte[] sendByte = sendValue.getBytes();
					sendMessages(sendByte);
					buttonNext.setText(buttonGet);
				} else {
					// 一次握手代表成功
					String say = "SetCMD:'GetStatus'\r\n";
					byte[] send = say.getBytes();
					sendMessages(send);
				    //Toast.makeText(MainCeLingActivity.this, "建立连接   发送消息 = "+sendResult, Toast.LENGTH_LONG).show();
				}
				break;
			case connect_fail:
				handlerBase.sendEmptyMessage(ConstantUtil.DIALOG_HINT);
				stopConnectTimer();
				//如果蓝牙不能用
				if(!bluetoothAdapter.isEnabled()){
					ShowUtil.showToast(MainCeLingActivity.this, R.string.celing_open_fail);
				}
				if (isGetResult) {
					if (instance != null)
						showConnectDialog(false);
				} else {
					if (instance != null)
						showConnectDialog(false);
					buttonNext.setText(buttonSearchFail);
				}
				break;
			case device_open_fail:
				ShowUtil.showToast(MainCeLingActivity.this, R.string.celing_open_fail);
				stopTest();
				finish();
				break;
			case device_notfind:

				break;
			case device_bond_fail:
				buttonNext.setText(buttonSearchFail);
				break;
			case connect_ing:
				buttonNext.setText(buttonSearch);
				break;
			case receive_message:
			    stopSendTimer();
			    stopConnectTimer();
				handlerBase.sendEmptyMessage(ConstantUtil.DIALOG_HINT);
				String readMessage = msg.obj.toString();
				if (readMessage.indexOf("READY") != -1) {
					buttonNext.setText(buttonChoose);
					textHint.setVisibility(View.VISIBLE);
				}
				// 结果
				else {
					String[] temp = readMessage.split("#");
					if (temp.length > 0) {
						resultJudge(temp[0]);
					}
				}
				break;
			default:
				break;
			}

		}
	};
```
> ## 7. 注册接收蓝牙状态返回的广播

```
// 注册接收蓝牙状态返回的广播
	private void registerBluetooth() {
		IntentFilter intentFilter = new IntentFilter();
		intentFilter.addAction(BluetoothAdapter.ACTION_STATE_CHANGED);
		intentFilter.addAction(BluetoothDevice.ACTION_FOUND);
		intentFilter.addAction(BluetoothDevice.ACTION_BOND_STATE_CHANGED);
		intentFilter.addAction(BluetoothAdapter.ACTION_SCAN_MODE_CHANGED);
		intentFilter.addAction(BluetoothAdapter.ACTION_DISCOVERY_FINISHED);
		registerReceiver(receiverBluetooth, intentFilter);
	}



// 蓝牙状态返回的广播
	private BroadcastReceiver receiverBluetooth = new BroadcastReceiver() {
		@Override
		public void onReceive(Context context, Intent intent) {
			Log.d(TAG, intent.getAction());
			// 搜索到蓝牙
			if (BluetoothDevice.ACTION_FOUND.equals(intent.getAction())) {
				BluetoothDevice device = intent
						.getParcelableExtra(BluetoothDevice.EXTRA_DEVICE);
				Log.d(TAG, "蓝牙名字:" + device.getName() + "   蓝牙mac地址:"
						+ device.getAddress());
				String name = device.getName();
				String mac = device.getAddress();
				if (device != null && name != null&& name.substring(0, 2).equals("LP")&& mac.split(":")[1].equals("03")) {
					bondBluetoothDevice(device, false);
					return;
				}
			}
			// 改变
			if (BluetoothDevice.ACTION_BOND_STATE_CHANGED.equals(intent
					.getAction())) {
				Log.d(TAG, "收到changed广播");
				if (bluetoothDevice != null&& bluetoothDevice.getBondState() == BluetoothDevice.BOND_BONDED) {
					ConnectThread connectThread = new ConnectThread(bluetoothDevice, true);
					//if (!connectThread.isAlive()) {
					connectThread.start();
					startConnectTimer();
					handlerBase.sendEmptyMessage(ConstantUtil.DIALOG_SHOW);
					//}
					
					Log.d(TAG, "连接绑定的设备");
				}
				//绑定失败
				else
				{
					sppHandler.obtainMessage(device_bond_fail).sendToTarget();
				}
			}
			// 搜索完毕
			if (BluetoothAdapter.ACTION_DISCOVERY_FINISHED.equals(intent
					.getAction())) {
                Log.d(TAG, "搜索完毕");
			}

		}
	};


//由于onDestroy耗时,所以我们需要在onDestroy之前执行下面代码。
	public void destroy(){
		instance = null;
		unregisterReceiver(receiverBluetooth);//注销广播
		SharedPreferenceUtil.setBoolean(MainCeLingActivity.this,ConstantUtil.CELING_DESTORY, true);
	}
```
> ## 8. 定义一个连接设备的线程

```
//连接设备线程
	private class ConnectThread extends Thread {

		private BluetoothDevice tempDevice;
		private boolean tempIsOldDevice; //是否搜索

		public ConnectThread(BluetoothDevice device, boolean isOldDevice) {
			tempDevice = device;
			tempIsOldDevice = isOldDevice;
			
			//如果是获取结果的话不需要搜索,获取指定设备
			if(isGetResult){
				tempIsOldDevice = false;
			}
		}

		@SuppressLint("NewApi")
		@Override
		public void run() {

			UUID uuid = UUID.fromString(SPP_UUID);
			Log.d(TAG, "第一次连接");
			// 先试一下createInsecureRfcommSocketToServiceRecord
			try {
				bluetoothSocket = tempDevice
						.createInsecureRfcommSocketToServiceRecord(uuid);
				bluetoothSocket.connect();

				isConnected = true;
			} catch (IOException e) {
				Log.d(TAG, "第一次连接失败"+e);
			}


			if (isConnected && !isTimeOut) {
				// 记录最新的连接设备名称
				SharedPreferenceUtil.setString(MainCeLingActivity.this,ConstantUtil.CELING_DEVICE, tempDevice.getName());

				sppHandler.obtainMessage(connect_success).sendToTarget();
			} else {
				// 再试一下 createRfcommSocketToServiceRecord
				try {
					Log.d(TAG, "第二次连接");
					bluetoothSocket = tempDevice.createRfcommSocketToServiceRecord(uuid);
					bluetoothSocket.connect();

					isConnected = true;
				} catch (IOException e) {
					Log.d(TAG, "第二次连接失败"+e);
					try {
						if (bluetoothSocket != null) {
							bluetoothSocket.close();
						}
					} catch (IOException e1) {
						e1.printStackTrace();
					}
				}

				if (isConnected && !isTimeOut) {
					// 记录最新的连接设备名称
					SharedPreferenceUtil.setString(MainCeLingActivity.this,ConstantUtil.CELING_DEVICE, tempDevice.getName());

					sppHandler.obtainMessage(connect_success).sendToTarget();
				} else {
					if (tempIsOldDevice && !isTimeOut) {
						connectBondBluetooth(true);
					} else {
						// 新搜索出来的，失败
						Log.d(TAG, "发送失败消息");
						//sppHandler.obtainMessage(connect_fail).sendToTarget();
					}
				}
			}
		}
	}
```
> ## 9. 连接已经绑定过得设备

```
// 连接已经绑定过得设备
	private void connectBondBluetooth(boolean startSearch) {

		boolean flag = false;
		// 记录最新的连接设备名称
		String lastDeviceName = SharedPreferenceUtil.getString(MainCeLingActivity.this,ConstantUtil.CELING_DEVICE);
		if (lastDeviceName.length() > 0 && !startSearch) {
//获得绑定的设备的列表
			Set<BluetoothDevice> pairedDevices = bluetoothAdapter.getBondedDevices();
			if (pairedDevices != null && pairedDevices.size() > 0) {
				for (BluetoothDevice device : pairedDevices) {
					String name = device.getName();
					if (name != null && !name.equals("")&& name.equals(lastDeviceName)) {
						Log.d(TAG, "开始连接绑定过得设备"+name);
						bondBluetoothDevice(device, true);
						flag = true;
						break;
					}
				}
			}
		}

		// 没有已经配对的设备,就重新搜索
		if (!flag) {
			bluetoothAdapter.startDiscovery();
		}
	}
```
> ## 10. 从手机向设备发送消息

```
// 从手机向设备发送消息
	public boolean sendMessages(byte[] datas) {

		try {
			Thread.sleep(SLEEP_SEND_TIME);
		} catch (InterruptedException e2) {
			e2.printStackTrace();
		}

		if (bluetoothSocket == null) {
			//ShowUtil.showToast(instance, "尚未连接设备");
			return false;
		}

		boolean flag = false;
		try {
			mOutputStream = bluetoothSocket.getOutputStream();
			if (mOutputStream != null) {
				mOutputStream.flush();
				mOutputStream.write(datas);
				flag = true;
			}
		} catch (Exception e) {
			e.printStackTrace();
			try {
				if (mOutputStream != null) {
					mOutputStream.flush();
					mOutputStream.close();
				}
			} catch (IOException e1) {
				e1.printStackTrace();
			}
		}
		Log.d(TAG, "write success="+flag);
		return flag;
	}
```
> ## 11. 开启接受信息的线程

```
//开启接受信息的线程
	private void startReceiveMessageThread() {
		if (mReceiveMessageThread == null) {
			mReceiveMessageThread = new ReceiveMessageThread();
			mReceiveMessageThread.start();
			isReceiveMessage = true;
		}
	}
```
> ## 12. [从 0 开始开发一款直播 APP】7 倒计时器 CountDownTimer 源码解析](http://www.jianshu.com/p/8fd203f9228c)
##  自定义的倒计时 

```
package com.yikang.heartmark.util;

import android.app.Notification;
import android.app.NotificationManager;
import android.app.PendingIntent;
import android.content.Context;
import android.content.Intent;
import android.os.CountDownTimer;

import com.example.heartmark.R;
import com.yikang.heartmark.activity.MainCeLingActivity;

/**
 * 测量倒计时工具类
 * */
public class MyCount extends CountDownTimer {

	private static MyCount instance;
	private static Context context;
	private static NotificationManager notifi; // 通知栏

	public static MyCount getInstance(Context contxt,long millisInFuture,
			long countDownInterval) {
		context = contxt;
		notifi = (NotificationManager) context.getSystemService(context.NOTIFICATION_SERVICE);
		if (instance == null) {
			instance = new MyCount(millisInFuture, countDownInterval);
		}
		return instance;
	}

	public static void stop() {
		if (instance != null) {
			instance.cancel();
			instance = null;
		}
	}

	public MyCount(long millisInFuture, long countDownInterval) {
		super(millisInFuture, countDownInterval);
	}

	@Override
	public void onTick(long millisUntilFinished) {
		if (MainCeLingActivity.instance != null) {
			MainCeLingActivity.instance.buttonNext.setText("反应倒计时("
					+ millisUntilFinished / 1000 + ")");
		}
	}

	@Override
	public void onFinish() {
		showNotification();
		if (MainCeLingActivity.instance != null) {
			 MainCeLingActivity.instance.buttonNext.setText(MainCeLingActivity.instance.buttonGet);
			 MainCeLingActivity.instance.buttonNext.setClickable(true);
			 
			
			 String sendValue = "GetDate\r\n";
			 byte[] sendByte = sendValue.getBytes();
			 MainCeLingActivity.instance.sendMessages(sendByte);
			 MainCeLingActivity.instance.buttonNext.setText( MainCeLingActivity.instance.buttonGet);
		}
	}
	
	@SuppressWarnings("deprecation")
	public void showNotification() {
		int icon = R.drawable.heart_mark_icon;
		long when = System.currentTimeMillis();

		String appName = context.getResources().getString(R.string.app_name);
		String title = context.getResources().getString(R.string.app_name);
		String info = context.getResources().getString(R.string.celing_notif_info);

		Notification notification = new Notification(icon, title, when);
		notification.flags = Notification.FLAG_ONGOING_EVENT;
		notification.defaults |= Notification.DEFAULT_SOUND; // 添加声音
		notification.flags |= Notification.FLAG_AUTO_CANCEL; // 点击自动清除
		PendingIntent contentIntent = PendingIntent.getActivity(context, 0,new Intent(), 0);

		notification.setLatestEventInfo(context, appName, info, contentIntent);
		notifi.notify(R.string.app_name, notification);
	}

}

```
> ## 13. 蓝牙列表

```
private BluetoothAdapter bluetoothAdapter;

bluetoothAdapter = BluetoothAdapter.getDefaultAdapter();


```
> ## 14. 按返回键的操作

```
//按返回键的操作
	@Override
	public void onBackPressed() {
		destroy();
		stopTest();
		finish();
	}
```
<h1 id="16">16. 病情评估  MainPingGuActivity</h1>  

## [返回目录](#0)

> ## 1. 从服务端取得所有评估次数

```
//从服务端取得所有评估次数  
	@SuppressWarnings({ "rawtypes"})
	public void getCountCallBack(Object data) {
		handlerBase.sendEmptyMessage(ConstantUtil.DIALOG_HINT);
		Map resultMap = (Map) data;
		if (resultMap == null) {
			ShowUtil.showToast(MainPingGuActivity.this,R.string.check_network_timeout);
		} else {
			Map countMap = (Map) resultMap.get("body");
//			intValue()是把Integer对象类型变成int的基础数据类型；
			int count = Double.valueOf(countMap.get("COUNT").toString()).intValue();
			// 已有%d人进行评估  按照这个格式 格式字符串
			textViewCount.setText(String.format(getResources().getString(R.string.pinggu_count),count));
		}
	}
```
<h1 id="17">17. 更多服务  MainServiceActivity</h1>  

## [返回目录](#0)

> ## 1. 可以跳转到两个页面

```
MainServiceShopActivity  健康商城


MainServiceOtherActivity 更多应用
每一个画面，看他的布局是横向的还是竖向的就知道它是如何分布的了。

```
<h1 id="18">18. 健康商城 MainServiceShopActivity</h1>  

## [返回目录](#0)

> ## 1. 主要是跳转到五个界面

```
心衰管理产品  MainServiceShopXinshuaiActivity  跳转到  产品详情
MainServiceShopXinshuaiDetailsActivity


血糖管理产品
远程心电监护
一键式智能呼叫

专家会诊  MainServiceShopHuizhenActivity页面
在跳转到  专家简介MainServiceShopHuizhenDetailsActivity  页面
```
> ## 2. 产品详情 显示png的图片
MainServiceShopXinshuaiDetailsActivity

```
private String url = "file:///android_asset/";
private int intExtra = -1;

intExtra  = getIntent().getIntExtra("main_service_shop_xinshuai", -1);

@Override
	public void onResume() {
		super.onResume();
		WebView webView = (WebView) findViewById(R.id.main_service_shop_xinshuai_details);
		//支持内容重新布局  
		webView.getSettings().setLayoutAlgorithm(LayoutAlgorithm.SINGLE_COLUMN);
		 //将图片调整到适合
		webView.getSettings().setUseWideViewPort(true); 
		// 缩放至屏幕的大小
		webView.getSettings().setLoadWithOverviewMode(true); 		
		switch (intExtra) {
		case 1:		
			webView.loadUrl(url+"main_service_shop_xinshuai_img01.png");
			break;
		case 2:
			webView.loadUrl(url+"main_service_shop_xinshuai_img02.png");
			break;
		case 3:
			webView.loadUrl(url+"main_service_shop_xinshuai_img03.png");
			break;
		case 4:
			webView.loadUrl(url+"main_service_shop_xinshuai_img04.png");
			break;
		case 5:
			webView.loadUrl(url+"main_service_shop_xinshuai_img05.png");
			break;
		case 6:
			webView.loadUrl(url+"main_service_shop_xinshuai_img06.png");
			break;
		default:
			break;
		}
	}
```
<h1 id="19">19. MainServiceOtherActivity 更多应用</h1>  

## [返回目录](#0)

> ## 1. 下载apk

```
String dowmload01 = "http://www.e-care365.com/app/poctor.apk";
			showUpgradeDialog("普博士手机血糖APP下载中...",dowmload01,"poctor");


//提示
	MyDialog dialog;
	private void showUpgradeDialog(final String content, final String dowmload012, final String string2) {
		dialog = new MyDialog(MainServiceOtherActivity.this)
				.setTitle("提示")
				.setMessage("是否下载普博士手机血糖app")
				.setPositiveButton(R.string.ok, new View.OnClickListener() {

					@Override
					public void onClick(View arg0) {
						doawnload(content,dowmload012,string2);
					}
				})
				.setNegativeButton(R.string.cancel, new View.OnClickListener() {
					@Override
					public void onClick(View arg0) {
					}
				});

		dialog.create(null);
		dialog.showMyDialog();
	}
	
	// 下载
	MyDialog m_pDialog;
	public void doawnload(String context, String dowmload, final String name) {
		HttpUtils utils = new HttpUtils();
		m_pDialog = new MyDialog(MainServiceOtherActivity.this);
		m_pDialog.setTitle("提示");
		m_pDialog.setMessage(context);
		m_pDialog.setProgressbar();
		m_pDialog.create(null);
		m_pDialog.showMyDialog();
		/**
		 * 判断SD的状态：如果SD不存在就进行友好提示
		 */
		if (!Environment.getExternalStorageState().equals(
				Environment.MEDIA_MOUNTED)) {
			MyToast.show(getApplicationContext(), "手机SD卡不存在",
					Toast.LENGTH_SHORT);
			return;
		}
		/*
		 * 参数： 1 下载url地址 2 下载到哪个位置 3 回调方法
		 */
		utils.download(dowmload, Environment.getExternalStorageDirectory()
				.getAbsolutePath() + "/"+name+".apk",
				new RequestCallBack<File>() {

					@Override
					public void onFailure(HttpException arg0, String arg1) {// 下载失败
						ShowUtil.showToast(MainServiceOtherActivity.this,R.string.download_fail);
						m_pDialog.dismiss();
					}

					// 下载成功
					@Override
					public void onSuccess(ResponseInfo<File> arg0) {
						m_pDialog.dismiss();
						installAPk(name);
					}

					@Override
					public void onLoading(final long total, final long current,
							boolean isUploading) {// 下载进度
						super.onLoading(total, current, isUploading);
						int progress = (int) (current * 100 / total);
						m_pDialog.setProgress(progress);
					}
				});
	}

	// 安装
	public void installAPk(String name) {
		Intent intent = new Intent();
		intent.setAction("android.intent.action.VIEW");
		intent.addCategory("android.intent.category.DEFAULT");
		intent.setDataAndType(
				Uri.fromFile(new File(Environment.getExternalStorageDirectory()
						.getAbsolutePath() + "/" + name + ".apk")),
				"application/vnd.android.package-archive");
		this.startActivityForResult(intent, 100);
	}
```
<h1 id="20">20. 电话咨询 MainPhoneActivity</h1>  

## [返回目录](#0)

> ## 1. 用盒子的概念来做界面，相对布局里的内容比较方便居中

```
 <!-- 用行对布局做出一个盒子  方便下一级盒子在父类中集中显示-->
		    <RelativeLayout 
		        android:layout_width="match_parent"
		        android:layout_height="wrap_content"
		        android:layout_marginTop="40dp"
		        android:layout_marginBottom="20dp"
		        >
		        <LinearLayout 
		            android:layout_width="match_parent"
		            android:layout_height="wrap_content"
		            android:orientation="vertical"
		            android:layout_centerInParent="true"
		            >
			        <ImageButton
			            android:id="@+id/main_phone_img"
			            android:layout_width="wrap_content"
			            android:layout_height="wrap_content"
			            android:layout_gravity="center_horizontal"
			            android:background="@drawable/main_phone_img"
			            />
			        <!-- 文字的换行 -->
			        <TextView 
			            android:layout_width="wrap_content"
			            android:layout_height="wrap_content"
			            android:text="400-090-6162 \n 拨打咨询电话"
			            android:layout_gravity="center_horizontal"
			            android:textSize="20sp"
			            android:textColor="@color/app_color"
			            android:layout_marginTop="10dp"
			            />            
		        </LinearLayout>
		    </RelativeLayout>
```
> ## 2. 利用intent来拨打电话

```
findViewById(R.id.main_phone_img).setOnClickListener(new OnClickListener() {
			
			@Override
			public void onClick(View v) {
				Intent intent = new Intent(Intent.ACTION_CALL, Uri.parse(getResources().getString(R.string.phone_number_ofzixun)));
                startActivity(intent);
			}
		});
```
<h1 id="21">21. 个人中心 MainSetActivity</h1>  

## [返回目录](#0)

> ## 1. 输入框的排版

```
<!-- 输入框的排版 -->
		   <RelativeLayout
		        android:id="@+id/set_life_data"
		        android:layout_width="match_parent"
		        android:layout_height="40dp"
		        android:layout_marginLeft="15dp"
		        android:layout_marginRight="15dp"
		        android:background="@drawable/edittext_img" >
		
		        <ImageView
		            android:id="@+id/imageView1"
		            android:layout_width="25dp"
		            android:layout_height="25dp"
		            android:layout_centerVertical="true"
		            android:layout_marginLeft="20dp"
		            android:background="@drawable/set_life" />
		
		        <TextView
		            android:layout_width="wrap_content"
		            android:layout_height="wrap_content"
		            android:layout_centerVertical="true"
		            android:layout_marginLeft="10dp"
		            android:layout_toRightOf="@+id/imageView1"
		            android:text="生活日志"
		            android:textSize="18dp" />
		
		        <ImageView
		            android:layout_width="wrap_content"
		            android:layout_height="wrap_content"
		            android:layout_alignParentRight="true"
		            android:layout_centerVertical="true"
		            android:layout_marginRight="20dp"
		            android:background="@drawable/arrow_right_blue" />
		    </RelativeLayout>
```
> ## 2. 判断字符串非空

```
if (!TextUtils.isEmpty(uSER_SEX) && "0001".equals(uSER_SEX)) {
				headIcon.setBackgroundResource(R.drawable.friend_head_man);
			} 
```
> ## 3. 扫描的完成

```
//调用扫描的代码
case R.id.set_scan:
//				if(ConnectUtil.isLogin(MainSetActivity.this)){
				if(true){
				try {
						Intent intent = new Intent(MainSetActivity.this,
								CaptureActivity.class);
						startActivityForResult(intent, SCAN_IMG);
					} catch (Exception e) {
					}
				}else{
					Intent collectIntent = new Intent(MainSetActivity.this, LoginActivity.class);
					startActivity(collectIntent);
				}
				break;




@Override
	public void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		if (resultCode == RESULT_OK) {
			switch (requestCode) {
			case SCAN_IMG:
				Bundle bundle = data.getExtras();
				//这个是扫描到的字符串
				String scanResult = bundle.getString("result");
				Map<String, String> params = new HashMap<String, String>();
				params.put("doctorNo",scanResult);
				ConnectionManager.getInstance().send("FN01070WD00",
						"bindingDoctor", params,"saveScanMessageInfo",this);
				break;



/**
	 * 处理扫描结果（在界面上显示）
	 */
	@SuppressWarnings("rawtypes")
	public void saveScanMessageInfo(Object data) {
		handlerBase.sendEmptyMessage(ConstantUtil.DIALOG_HINT);
		Map resultMap = (Map) data;
		if (resultMap == null) {
			ShowUtil.showToast(MainSetActivity.this,
					R.string.check_network_timeout);
		}else{
			String result = (String) resultMap.get("head");
			String message = (String) resultMap.get("message");
			String DOCTOR_NO = (String) resultMap.get("DOCTOR_NO");
			String flag = (String) resultMap.get("flag");
			if (result.equals("success")) {
				if("01003".equals(message)&&"true".equals(flag)){
					setScan.setClickable(false);
					setScan.setFocusable(false);
					scan_Txt.setText(DOCTOR_NO);
					MyToast.show(MainSetActivity.this,"绑定成功",Toast.LENGTH_LONG);
				}else if("01001".equals(message)){
					setScan.setClickable(false);
					setScan.setFocusable(false);
					scan_Txt.setText(DOCTOR_NO);
					MyToast.show(MainSetActivity.this,"已经绑定过",Toast.LENGTH_LONG);
				}else if("01002".equals(message)){
					MyToast.show(MainSetActivity.this,"医生编号不存在",Toast.LENGTH_LONG);
				}
				SharedPreferenceUtil.setString(MainSetActivity.this,ConstantUtil.USER_NUMBER, DOCTOR_NO);
				SharedPreferenceUtil.setString(MainSetActivity.this,ConstantUtil.USER_NUMBER_CODE, flag);
			}
		}
	}

```
> ## 4. 上传病历

```
//点击后，登录或选择拍照或图库
case R.id.set_image:
				if(ConnectUtil.isLogin(MainSetActivity.this)){
				//if(true){
				showChooseIconDialog();
				}else{
					Intent collectIntent = new Intent(MainSetActivity.this, LoginActivity.class);
					startActivity(collectIntent);
				}
				break;


//拍照上传
	protected void showChooseIconDialog() {
		AlertDialog.Builder builer = new Builder(MainSetActivity.this);
		builer.setTitle("提示");
		builer.setMessage("选择上传图片");
		builer.setPositiveButton("拍照",
				new android.content.DialogInterface.OnClickListener() {
					@SuppressLint("WorldWriteableFiles")
					public void onClick(DialogInterface dialog, int which) {
//
//						Uri imageUri = null;
//						String fileName = null;
//						Intent openCameraIntent = new Intent(
//								MediaStore.ACTION_IMAGE_CAPTURE);
//						// 删除上一次截图的临时文件
//						@SuppressWarnings("deprecation")
//						SharedPreferences sharedPreferences = MainSetActivity.this
//								.getSharedPreferences("temp",Context.MODE_WORLD_WRITEABLE);
//						ImageTools.deletePhotoAtPathAndName(Environment
//								.getExternalStorageDirectory()
//								.getAbsolutePath(), sharedPreferences
//								.getString("tempName", ""));
//
//						// 保存本次截图临时文件名字
//						fileName = String.valueOf(System.currentTimeMillis())+ ".jpg";
//						Editor editor = sharedPreferences.edit();
//						editor.putString("tempName", fileName);
//						editor.commit();
//
//						imageUri = Uri.fromFile(new File(Environment.getExternalStorageDirectory(), fileName));
						// 指定照片保存路径（SD卡），image.jpg为一个临时文件，每次拍照后这个图片都会被替换
						//openCameraIntent.putExtra(MediaStore.EXTRA_OUTPUT,imageUri);
						//startActivityForResult(openCameraIntent, CROP_PHOTO);
						Intent camera = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);
						startActivityForResult(camera,CROP_PHOTO);
					}
				});
		builer.setNegativeButton("图片库",
				new android.content.DialogInterface.OnClickListener() {
					public void onClick(DialogInterface dialog, int which) {
//						Intent openAlbumIntent = new Intent(Intent.ACTION_GET_CONTENT);
//						openAlbumIntent.setDataAndType(MediaStore.Images.Media.EXTERNAL_CONTENT_URI,"image/*");
//						startActivityForResult(openAlbumIntent, ACTION_CROP);
//						
						Intent intent = new Intent(Intent.ACTION_PICK, null);
						intent.setDataAndType(MediaStore.Images.Media.EXTERNAL_CONTENT_URI, "image/*");
						startActivityForResult(intent, CROP_PICTURE);
					}
				});
		AlertDialog dialog = builer.create();
		dialog.show();
	}



/*
	 * 处理大图片 成小点的图片，在把图片放大
	 */
	public static Bitmap dowithBigImage(Bitmap bitmap) {
		Bitmap returnBitmap = null;
		if (bitmap != null) {
			int imageWidth = bitmap.getWidth();
			int imageHeight = bitmap.getHeight();

			if (bitmap.getWidth() >= IMAGE_DOWITH_WIDTH) {
				imageWidth = IMAGE_DOWITH_WIDTH;
			}

			if (bitmap.getHeight() >= IMAGE_DOWITH_HEIGHT) {
				imageHeight = IMAGE_DOWITH_HEIGHT;
			}

			returnBitmap = ImageUtil.zoomImg(bitmap, imageWidth,
					imageHeight);
		}
		return returnBitmap;
	}



/**
	 * 放大缩小了的图片
	 * 
	 * @param bitmap
	 * @param w
	 * @param h
	 * @return
	 */
	public static Bitmap zoomImg(Bitmap bitmap, int w, int h) {
		Bitmap newbmp = null;
		if (bitmap != null) {
			int width = bitmap.getWidth();
			int height = bitmap.getHeight();
			Matrix matrix = new Matrix();
			float scaleWidht = ((float) w / width);
			float scaleHeight = ((float) h / height);
			matrix.postScale(scaleWidht, scaleHeight);
			newbmp = Bitmap.createBitmap(bitmap, 0, 0, width, height, matrix,
					true);
		}
		return newbmp;
	}


//返回图片的路径
	private String getImagePath(Intent data) {
		Uri uri = data.getData();
		if (uri == null)
			return "";

		String[] proj = { MediaStore.Images.Media.DATA };
		Cursor actualimagecursor = managedQuery(uri, proj, null, null, null);

		int actual_image_column_index = actualimagecursor
				.getColumnIndexOrThrow(MediaStore.Images.Media.DATA);
		actualimagecursor.moveToFirst();

		return actualimagecursor.getString(actual_image_column_index);

	}


//把文件保存到内存卡上
	public static void SaveImage(Bitmap bitmap, String fileName) {
		FileOutputStream fout = null;
		try {
			fout = new FileOutputStream(fileName);
			bitmap.compress(Bitmap.CompressFormat.PNG, 100, fout);
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} finally {
			try {
				if (fout != null) {
					fout.flush();
					fout.close();
				}
			} catch (IOException e) {
				e.printStackTrace();
			}
		}

	}


case CROP_PICTURE://图片库
//				Bitmap photo = null;
//				Uri photoUri = data.getData();
//				if (photoUri != null) {
//					photo = BitmapFactory.decodeFile(photoUri.getPath());
//				}
//				if (photo == null) {
//					Bundle extra = data.getExtras();
//					if (extra != null) {
//						photo = (Bitmap) extra.get("data");
//						ByteArrayOutputStream stream = new ByteArrayOutputStream();
//						photo.compress(Bitmap.CompressFormat.JPEG, 100, stream);
//					}
//				}
				Bitmap picture = BitmapFactory.decodeFile(getImagePath(data));
			    
				picture = ImageUtil.dowithBigImage(picture);
				
				File excelFiles = new File(FOLDER_PATH);
				if (!excelFiles.exists()) {
					excelFiles.mkdirs();
				}
				File excelFile = new File(IMAGE_PATH);
				if (excelFile.exists()) {
					excelFile.mkdir();
				}
				if(picture != null){
					ImageUtilBase.SaveImage(picture, IMAGE_PATH);
				}

				File file = new File(IMAGE_PATH);
				if (file != null) {
					new Thread() {
						@SuppressWarnings("rawtypes")
						public void run() {
							Map resultMap = (Map) FileUploadUtil.putImg("FN06070WD00S!uploadPatientImage.action",IMAGE_PATH);
							String result = (String) resultMap.get("head");
							Message msg = new Message();
							if (result.equals("success")) {
								msg.what = UPLOAD_SUCCESS;
								Bundle b=new Bundle();
								b.putString("url", (String) resultMap.get("url"));
								msg.setData(b);
							} else if (result.equals("fail")) {
								msg.what = UPLOAD_FAIL;
								msg.obj = (String) resultMap.get("body");
							}
							handler.sendMessage(msg);
						}
					}.start();
				}
				break;
			case CROP_PHOTO://拍照
				Bundle getBundle = data.getExtras();

				Bitmap bitmap = (Bitmap) getBundle.get("data");
				//处理大图片 成小点的图片，在把图片放大
				bitmap = ImageUtil.dowithBigImage(bitmap);
				
				File folderFile = new File(FOLDER_PATH);
				if (!folderFile.exists()) {
					folderFile.mkdirs();
				}
				File imageFile = new File(IMAGE_PATH);
				if (imageFile.exists()) {
					imageFile.mkdir();
				}
				ImageUtilBase.SaveImage(bitmap, IMAGE_PATH);

				File files = new File(IMAGE_PATH);
				if (files != null) {
					new Thread() {
						@SuppressWarnings("rawtypes")
						public void run() {
							Map resultMap = (Map) FileUploadUtil.putImg("FN06070WD00S!uploadPatientImage.action",IMAGE_PATH);
							String result = (String) resultMap.get("head");
							Message msg = new Message();
							if (result.equals("success")) {
								msg.what = UPLOAD_SUCCESS;
								Bundle b=new Bundle();
								b.putString("url", (String) resultMap.get("url"));
								msg.setData(b);
							} else if (result.equals("fail")) {
								msg.what = UPLOAD_FAIL;
								msg.obj = (String) resultMap.get("body");
							}
							handler.sendMessage(msg);
						}
					}.start();
				}
				break;
```
<h1 id="22">22. 其他 MainSetAboutActivity</h1>  

## [返回目录](#0)

> ## 1. 软件更新

```
case R.id.set_update:
				doUpdate();
				break;


@SuppressLint("HandlerLeak")
	public Handler handler = new Handler() {
		public void handleMessage(Message msg) {
			switch (msg.what) {
			// 弹出升级框
			case MSG_SHOWUPGRADE:
				showUpgradeDialog();
				break;
			// 进行下载
			case MSG_DOAWNLOAD:
				doawnload();
				break;
			}
		};
	};

	// 升级
	private void showUpgradeDialog() {
		MyDialog dialog = new MyDialog(MainSetAboutActivity.this)
				.setTitle(R.string.upgrade_title)
				.setMessage(ConnectUtil.versionNameString + version + "\n更新内容有:\n" + content)
				.setPositiveButton(R.string.ok, new View.OnClickListener() {

					@Override
					public void onClick(View arg0) {
						Message message = Message.obtain();
						message.what = MSG_DOAWNLOAD;
						handler.sendMessage(message);
					}
				})
				.setNegativeButton(R.string.cancel, new View.OnClickListener() {

					@Override
					public void onClick(View arg0) {
					}
				});

		dialog.create(null);
		dialog.showMyDialog();
	}

	// Version请求
	private void doUpdate() {
		Map<String, String> params = new HashMap<String, String>();
		if (ConnectUtil.isConnect(AppContext.context)) {
			ConnectionManager.getInstance().send("CM01080WD00",
					"queryAndroidLastVersion", params,
					"getVersionSucessCallBack", this);
			handlerBase.sendEmptyMessage(ConstantUtil.DIALOG_SHOW);
		} else {
			ShowUtil.showToast(AppContext.context, R.string.check_network);
		}
	}

	// Version返回
	@SuppressWarnings("rawtypes")
	public void getVersionSucessCallBack(Object data) {
		handlerBase.sendEmptyMessage(ConstantUtil.DIALOG_HINT);
		Map resultMap = (Map) data;
		if (resultMap == null) {
			ShowUtil.showToast(MainSetAboutActivity.this,
					R.string.check_network_timeout);
		} else {
			version = (String) resultMap.get("VERSION_NO");
			content = (String) resultMap.get("CONTENT");
			content = content.replace(";", ";\n");
			versionUrl = (String) resultMap.get("DOWN_URL");
			// 无需更新
			String v = getVersionName();
			if (version.equals(v)) {
				ShowUtil.showToast(MainSetAboutActivity.this, R.string.version_new);
			} else {
				Message message = Message.obtain();
				message.what = MSG_SHOWUPGRADE;
				handler.sendMessage(message);
			}
		}

	}

	// 下载
	MyDialog m_pDialog;
	public void doawnload() {
		HttpUtils utils = new HttpUtils();
		m_pDialog = new MyDialog(MainSetAboutActivity.this);
		m_pDialog.setTitle("提示");
		m_pDialog.setMessage("心衰版本更新中...");
		//m_pDialog.setIcon(R.drawable.heart_mark_icon);
		//m_pDialog.setIndeterminate(false);
		//m_pDialog.setCancelable(false);
		m_pDialog.setProgressbar();
		m_pDialog.create(null);
		m_pDialog.showMyDialog();
		/**
		 * 判断SD的状态：如果SD不存在就进行友好提示
		 */
		if (!Environment.getExternalStorageState().equals(
				Environment.MEDIA_MOUNTED)) {
			MyToast.show(getApplicationContext(), "手机SD卡不存在",
					Toast.LENGTH_SHORT);
			return;
		}
		/*
		 * 参数： 1 下载url地址 2 下载到哪个位置 3 回调方法
		 */
		utils.download(versionUrl, Environment.getExternalStorageDirectory()
				.getAbsolutePath() + "/HeartMark" + version + ".apk",
				new RequestCallBack<File>() {

					@Override
					public void onFailure(HttpException arg0, String arg1) {// 下载失败
						ShowUtil.showToast(MainSetAboutActivity.this,
								R.string.download_fail);
						m_pDialog.dismiss();
					}

					// 下载成功
					@Override
					public void onSuccess(ResponseInfo<File> arg0) {

						m_pDialog.dismiss();
						// 下载成功，调用系统安装程序进行程序的安装
						installAPk();
					}

					@Override
					public void onLoading(final long total, final long current,
							boolean isUploading) {// 下载进度
						super.onLoading(total, current, isUploading);
						int progress = (int) (current * 100 / total);
						m_pDialog.setProgress(progress);
					}
				});
	}

	// 安装
	public void installAPk() {
		Intent intent = new Intent();
		intent.setAction("android.intent.action.VIEW");
		intent.addCategory("android.intent.category.DEFAULT");
		intent.setDataAndType(
				Uri.fromFile(new File(Environment.getExternalStorageDirectory()
						.getAbsolutePath() + "/HeartMark" + version + ".apk")),
				"application/vnd.android.package-archive");
		/**
		 * 安装后进行函数的回调
		 */
		this.startActivityForResult(intent, 100);
	}

	// 获取版本号
	public String getVersionName() {
		PackageManager manager = getPackageManager();// packageManager
		try {
			// 获取哪个应用程序的清单文件，getPackageName()指获取当前程序的包名
			PackageInfo packageInfo = manager.getPackageInfo(getPackageName(),
					0);
			return packageInfo.versionName;// 获取清单文件中的版本信息
		} catch (NameNotFoundException e) {
			e.printStackTrace();
			return "";
		}

	}
```
> ## 2. 免责声明 和 关于我们 是一个页面

```
private void init() {
		try {
			TopBarView topbar = (TopBarView) findViewById(R.id.setAboutBarView);
			topbar.setOnTopbarLeftButtonListener(this);
			WebView webView = (WebView) findViewById(R.id.set_about_context);
			if("about".equals(stringExtra)){
				webView.getSettings().setLayoutAlgorithm(LayoutAlgorithm.SINGLE_COLUMN);
				webView.getSettings().setUseWideViewPort(true); 
				webView.getSettings().setLoadWithOverviewMode(true); 
				topbar.setTopbarTitle(R.string.set_about);
				webView.loadUrl("file:///android_asset/about.png"); 
			}else if("limit".equals(stringExtra)){
				webView.getSettings().setJavaScriptEnabled(false);
				webView.getSettings().setSupportZoom(true);
				webView.getSettings().setBuiltInZoomControls(true);
				topbar.setTopbarTitle(R.string.set_limit);
				webView.loadUrl("file:///android_asset/html01.html"); 
			}
		} catch (Exception e) {
		}
	}
```

> ## 3. 个人资料页面 CenterInfoActivity  姓名 性别 年龄体重
> ## 4. 好友数据页面 MainNewsActivity  ViewPager加载页面  NewFriendView这是一个自定义的线性布局页面
里面内置了DynamicListView，动态刷新和加载数据ListView也是自定义的

```
这个是单个的视图
package com.yikang.heartmark.view;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

import android.content.Context;
import android.util.AttributeSet;
import android.view.LayoutInflater;
import android.widget.LinearLayout;

import com.example.heartmark.R;
import com.yikang.heartmark.adapter.NewFriendAdapter;
import com.yikang.heartmark.model.NewFriend;
import com.yikang.heartmark.util.ShowUtil;
import com.yikang.heartmark.view.DynamicListView.DynamicListViewListener;
import com.yuzhi.framework.util.ConnectionManager;

public class NewFriendView extends LinearLayout implements
		DynamicListViewListener {
	private Context context;
	private DynamicListView infoListView;
	private NewFriendAdapter infoAdapter;
	private ArrayList<NewFriend> infoList = new ArrayList<NewFriend>();
	private int page = 1;

	public NewFriendView(Context context) {
		super(context);
		this.context = context;
		LayoutInflater.from(context).inflate(R.layout.new_friend_view, this,
				true);
		init();
	}

	public NewFriendView(Context context, AttributeSet attrs) {
		super(context, attrs);
		this.context = context;
		LayoutInflater.from(context).inflate(R.layout.new_friend_view, this,
				true);
		init();
	}

	private void init() {
		infoListView = (DynamicListView) findViewById(R.id.new_friend_listview);
		infoListView.setOnRefreshListener(this);
		infoListView.setOnMoreListener(this);
		infoListView.setDoMoreWhenBottom(false); // 滚动到低端的时候是否自动加载更多

		Map<String, String> params = new HashMap<String, String>();
		params.put("pageNo", String.valueOf(page));
		ConnectionManager.getInstance().send("FN06090WD00",
				"queryFriendMessageList", params, "newFriendSucessCallBack",this);

	}

	// 首次请求或者刷新回调
	@SuppressWarnings("rawtypes")
	public void newFriendSucessCallBack(Object data) {
		infoListView.doneRefresh();
		Map resultMap = (Map) data;
		if (resultMap == null) {
			ShowUtil.showToast(context,R.string.check_network_timeout);
		} else {
			List list = (List) resultMap.get("body");
			infoList.clear();
			for (int i = 0; i < list.size(); i++) {
				NewFriend newFriend = new NewFriend();
				Map temp = new HashMap();
				temp = (Map) list.get(i);
				newFriend.image = (String) temp.get("FRIEND_SEX");
				newFriend.name = (String) temp.get("FRIEND_NAME");
				newFriend.time = (String) temp.get("CREATE_TIME");
				newFriend.result = (String) temp.get("MONITOR_RESULT");
				newFriend.diag = (String) temp.get("CONTENT");
				infoList.add(newFriend);
			}
			infoAdapter = new NewFriendAdapter(context, infoList);
			infoListView.setAdapter(infoAdapter);
		}
	}

	// 上拉加载的时候的返回
	@SuppressWarnings("rawtypes")
	public void getMoreSucessCallBack(Object data) {
		infoListView.doneMore();
		Map resultMap = (Map) data;
		if(resultMap == null){
			//失败处理
			return;
		}
		List list = (List) resultMap.get("resultSet");
		for (int i = 0; i < list.size(); i++) {
			NewFriend newFriend = new NewFriend();
			Map temp = new HashMap();
			temp = (Map) list.get(i);
			newFriend.image = (String) temp.get("ICON_URL");
			newFriend.name = (String) temp.get("USERNAME");
			newFriend.time = (String) temp.get("USERNAME");
			newFriend.result = (String) temp.get("CONTENT");

			infoList.add(newFriend);
		}
		if (infoAdapter != null) {
			infoAdapter.notifyDataSetChanged();
			page ++;
		}
	}

	@Override
	public boolean onRefreshOrMore(DynamicListView dynamicListView,
			boolean isRefresh) {
		if (isRefresh) {
			// 刷新请求第一页
			page = 1;
			Map<String, String> params = new HashMap<String, String>();
			params.put("pageNo", String.valueOf(page));
			ConnectionManager.getInstance().send("FN06090WD00",
					"queryFriendMessageList", params,
					"newFriendSucessCallBack", this);
		} else {
			if(page == 1){
				page ++;
			}
			Map<String, String> params = new HashMap<String, String>();
			params.put("pageNo", String.valueOf(page));
			ConnectionManager.getInstance().send("FN06090WD00",
					"queryFriendMessageList", params, "getMoreSucessCallBack",
					this);
		}
		return false;
	}
}


只给是自定义的xml布局
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical" >
<!-- android:scrollbars="vertical"这个的意思是显示竖向的滚动条 -->
    <com.yikang.heartmark.view.DynamicListView
        android:id="@+id/new_friend_listview"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:divider="@null"
        android:scrollbars="vertical" />

</LinearLayout>


自定义的刷新布局的ListView
package com.yikang.heartmark.view;

import android.annotation.SuppressLint;
import android.content.Context;
import android.util.AttributeSet;
import android.view.Gravity;
import android.view.MotionEvent;
import android.view.View;
import android.widget.AbsListView;
import android.widget.AbsListView.OnScrollListener;
import android.widget.LinearLayout;
import android.widget.ListView;
import android.widget.ProgressBar;
import android.widget.TextView;

import com.example.heartmark.R;

/**
 * 动态刷新和加载数据ListView
 * 
 * @author RobinTang
 * 
 */
public class DynamicListView extends ListView implements OnScrollListener {

	/**
	 * 监听器 监听控件的刷新或者加载更多事件 所有的条目事件都会有一个偏移量，也就是position应该减1才是你适配器中的条目
	 * 
	 * @author RobinTang
	 * 
	 */
	public interface DynamicListViewListener {
		/**
		 * 
		 * @param dynamicListView
		 * @param isRefresh
		 *            为true的时候代表的是刷新，为false的时候代表的是加载更多
		 * @return true:刷新或者加载更多动作完成，刷新或者加载更多的动画自动消失
		 *         false:刷新或者加载更多为完成，需要在数据加载完成之后去调用控件的doneRefresh
		 *         ()或者doneMore()方法
		 */
		public boolean onRefreshOrMore(DynamicListView dynamicListView,
				boolean isRefresh);
	}

	/**
	 * 状态控件（StatusView，列表头上和底端的）的状态枚举
	 * 
	 * @author RobinTang
	 * 
	 */
	enum RefreshStatus {
		none, normal, willrefresh, refreshing
	}

	/**
	 * 状态控件
	 * 
	 * @author RobinTang
	 * 
	 */
	class StatusView extends LinearLayout {
		public int height;
		public int width;
		private ProgressBar progressBar = null;
		private TextView textView = null;
		private RefreshStatus refreshStatus = RefreshStatus.none;
		private String normalString = "下拉刷新";
		private String willrefreshString = "松开刷新";
		private String refreshingString = "正在刷新";

		public StatusView(Context context, AttributeSet attrs) {
			super(context, attrs);
			initThis(context);
		}

		public StatusView(Context context) {
			super(context);
			initThis(context);
		}

		private void initThis(Context context) {
			this.setOrientation(LinearLayout.HORIZONTAL);
			this.setGravity(Gravity.CENTER_HORIZONTAL | Gravity.CENTER_VERTICAL);

			progressBar = new ProgressBar(context);
			progressBar.setLayoutParams(new LinearLayout.LayoutParams(30, 30));
			textView = new TextView(context);
			textView.setTextSize(18);
			textView.setPadding(5, 0, 0, 0);
			textView.setTextColor(context.getResources().getColor(R.color.typeface));

			setCacheColorHint(0);
			this.setGravity(Gravity.CENTER);
			
			this.addView(progressBar);
			this.addView(textView);

			int w = View.MeasureSpec.makeMeasureSpec(0,
					View.MeasureSpec.UNSPECIFIED);
			int h = View.MeasureSpec.makeMeasureSpec(0,
					View.MeasureSpec.UNSPECIFIED);
			this.measure(w, h);

			height = this.getMeasuredHeight();
			width = this.getMeasuredWidth();

			this.setRefreshStatus(RefreshStatus.normal);
		}

		public RefreshStatus getRefreshStatus() {
			return refreshStatus;
		}

		public void setRefreshStatus(RefreshStatus refreshStatus) {
			if (this.refreshStatus != refreshStatus) {
				this.refreshStatus = refreshStatus;
				if (refreshStatus == RefreshStatus.refreshing) {
					this.progressBar.setVisibility(View.VISIBLE);
				} else {
					this.progressBar.setVisibility(View.GONE);
				}
				refreshStatusString();
				this.invalidate();
			}
		}

		private void refreshStatusString() {
			switch (refreshStatus) {
			case normal:
				textView.setText(normalString);
				progressBar.setProgress(0);
				break;
			case willrefresh:
				textView.setText(willrefreshString);
				break;
			case refreshing:
				textView.setText(refreshingString);
				break;
			default:
				break;
			}
		}

		/**
		 * 设置状态字符串
		 * 
		 * @param normalString
		 *            平时的字符串
		 * @param willrefreshString
		 *            松开后刷新（或加载）的字符串
		 * @param refreshingString
		 *            正在刷新（或加载）的字符串
		 */
		public void setStatusStrings(String normalString,
				String willrefreshString, String refreshingString) {
			this.normalString = normalString;
			this.willrefreshString = willrefreshString;
			this.refreshingString = refreshingString;
			this.refreshStatusString();
		}
	}

	private StatusView refreshView;
	private StatusView moreView;
	private int itemFlag = -1;
	private boolean isRecorded = false;
	private int downY = -1;
	private final float minTimesToRefresh = 1.5f;
	private final static int ITEM_FLAG_FIRST = 1;
	private final static int ITEM_FLAG_NONE = 0;
	private final static int ITEM_FLAG_LAST = -1;
	
	// 两个监听器
	private DynamicListViewListener onRefreshListener;
	private DynamicListViewListener onMoreListener;
	// 滚动到低端的时候是否自动加载更多
	private boolean doMoreWhenBottom = false;

	public DynamicListView(Context context, AttributeSet attrs, int defStyle) {
		super(context, attrs, defStyle);
		initThis(context);
	}

	public DynamicListView(Context context, AttributeSet attrs) {
		super(context, attrs);
		initThis(context);
	}

	public DynamicListView(Context context) {
		super(context);
		initThis(context);
	}

	private void initThis(Context context) {
		refreshView = new StatusView(context);
		moreView = new StatusView(context);
		refreshView.setStatusStrings("继续下拉刷新数据", "松开之后刷新数据", "正在刷新数据");
		moreView.setStatusStrings("继续上拉加载数据", "松开之后加载数据", "正在加载数据");
		//this.addHeaderView(refreshView, null, false);
		//this.addFooterView(moreView, null, false);
		this.setOnScrollListener(this);
		doneRefresh();
		doneMore();
	}
	
	/**
	 * 这个方法不要随便调用
	 */
	public void setRefreshMoreData()
	{
		this.removeHeaderView(refreshView);
		refreshView.setStatusStrings("继续下拉加载数据", "松开之后加载数据", "正在加载数据");
		this.addHeaderView(refreshView, null, false);
	}

	// 监听器操作
	public DynamicListViewListener getOnRefreshListener() {
		return onRefreshListener;
	}

	public void setOnRefreshListener(DynamicListViewListener onRefreshListener) {
		this.onRefreshListener = onRefreshListener;
		
		this.addHeaderView(refreshView, null, false);
	}

	public DynamicListViewListener getOnMoreListener() {
		return onMoreListener;
	}

	public void setOnMoreListener(DynamicListViewListener onMoreListener) {
		this.onMoreListener = onMoreListener;
		
		this.addFooterView(moreView, null, false);
	}

	// 设置
	public boolean isDoMoreWhenBottom() {
		return doMoreWhenBottom;
	}

	public void setDoMoreWhenBottom(boolean doMoreWhenBottom) {
		this.doMoreWhenBottom = doMoreWhenBottom;
	}

	@Override
	public void onScroll(AbsListView l, int t, int oldl, int count) {
		// log("%d %d %d", t, oldl, count);
		if (t == 0)
			itemFlag = ITEM_FLAG_FIRST;
		else if ((t + oldl) == count) {
			itemFlag = ITEM_FLAG_LAST;
			if (doMoreWhenBottom && onMoreListener != null
					&& moreView.getRefreshStatus() != RefreshStatus.refreshing) {
				doMore();
			}
		} else {
			itemFlag = ITEM_FLAG_NONE;
			// isRecorded = false;
		}
	}

	@Override
	public void onScrollStateChanged(AbsListView arg0, int arg1) {

	}

	@SuppressLint("ClickableViewAccessibility")
	@Override
	public boolean onTouchEvent(MotionEvent ev) {
		switch (ev.getAction()) {
		case MotionEvent.ACTION_DOWN:
			if (isRecorded == false
					&& (itemFlag == ITEM_FLAG_FIRST
							&& onRefreshListener != null
							&& refreshView.getRefreshStatus() == RefreshStatus.normal || itemFlag == ITEM_FLAG_LAST
							&& onMoreListener != null
							&& moreView.getRefreshStatus() == RefreshStatus.normal)) {
				downY = (int) ev.getY(0);
				isRecorded = true;
				// log("按下，记录：%d flag:%d", downY, itemFlag);
			}
			break;
		case MotionEvent.ACTION_UP: {
			isRecorded = false;
			if (onRefreshListener != null
					&& refreshView.getRefreshStatus() == RefreshStatus.willrefresh) {
				doRefresh();
			} else if (refreshView.getRefreshStatus() == RefreshStatus.normal) {
				refreshView.setPadding(0, -1 * refreshView.height, 0, 0);
			}

			if (onMoreListener != null
					&& moreView.getRefreshStatus() == RefreshStatus.willrefresh) {
				doMore();
			} else if (moreView.getRefreshStatus() == RefreshStatus.normal) {
				moreView.setPadding(0, 0, 0, -1 * moreView.height);
			}
			break;
		}
		case MotionEvent.ACTION_MOVE: {
			if (isRecorded == false
					&& (itemFlag == ITEM_FLAG_FIRST
							&& onRefreshListener != null
							&& refreshView.getRefreshStatus() == RefreshStatus.normal || itemFlag == ITEM_FLAG_LAST
							&& onMoreListener != null
							&& moreView.getRefreshStatus() == RefreshStatus.normal)) {
				downY = (int) ev.getY(0);
				isRecorded = true;
				// log("按下，记录：%d flag:%d", downY, itemFlag);
			} else if (isRecorded) {
				int nowY = (int) ev.getY(0);
				int offset = nowY - downY;
				if (offset > 0 && itemFlag == ITEM_FLAG_FIRST) {
					// 下拉
					setSelection(0);
					if (offset >= (minTimesToRefresh * refreshView.height)) {
						refreshView.setRefreshStatus(RefreshStatus.willrefresh);
					} else {
						refreshView.setRefreshStatus(RefreshStatus.normal);
					}

					refreshView.setPadding(0, -1
							* (refreshView.height - offset), 0, 0);
				} else if (itemFlag == ITEM_FLAG_LAST) {
					// 上拉
					setSelection(this.getCount());
					if (offset <= -1 * (minTimesToRefresh * moreView.height)) {
						moreView.setRefreshStatus(RefreshStatus.willrefresh);
					} else {
						moreView.setRefreshStatus(RefreshStatus.normal);
					}
					moreView.setPadding(0, 0, 0, -1
							* (moreView.height + offset));
				}
				// log("位移:%d", offset);
			}
			break;
		}
		default:
			break;
		}
		return super.onTouchEvent(ev);
	}

	/**
	 * 开始刷新
	 */
	private void doRefresh() {
		// log("开始刷新");
		refreshView.setRefreshStatus(RefreshStatus.refreshing);
		refreshView.setPadding(0, 0, 0, 0);
		if (onRefreshListener.onRefreshOrMore(this, true))
			doneRefresh();
	}

	/**
	 * 开始加载更多
	 */
	private void doMore() {
		// log("加载更多");
		moreView.setRefreshStatus(RefreshStatus.refreshing);
		moreView.setPadding(0, 0, 0, 0);
		if (onMoreListener.onRefreshOrMore(this, false))
			doneMore();
	}

	/**
	 * 刷新完成之后调用，用于取消刷新的动画
	 */
	public void doneRefresh() {
		// log("刷新完成!");
		refreshView.setRefreshStatus(RefreshStatus.normal);
		refreshView.setPadding(0, -1 * refreshView.height, 0, 0);
	}

	/**
	 * 加载更多完成之后调用，用于取消加载更多的动画
	 */
	public void doneMore() {
		// log("加载完成!");
		moreView.setRefreshStatus(RefreshStatus.normal);
		moreView.setPadding(0, 0, 0, -1 * moreView.height);
	}

	/**
	 * 获取刷新的状态
	 * 
	 * @return 一般 将要刷新 刷新完成
	 */
	public RefreshStatus getRefreshStatus() {
		return refreshView.getRefreshStatus();
	}

	/**
	 * 获取加载更多的状态
	 * 
	 * @return 一般 将要加载 加载完成
	 */
	public RefreshStatus getMoreStatus() {
		return moreView.getRefreshStatus();
	}
}
```

> ## 5. 好友列表  SetFriendActivity

```
@Override
	public void onResume() {
		super.onResume();
		//数据获得
		getFriend();
	}
	@Override
	public void onPause() {
		super.onPause();
		//数据清空
		friendList.clear();
	}



选择器的运用

<Button
            android:id="@+id/set_friend_push_check"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"            android:layout_alignParentRight="true"
            android:layout_centerVertical="true"
            android:layout_marginRight="20dp"
            android:background="@drawable/alarm_check_selector" />


if(SharedPreferenceUtil.getBooleanDefaultTrue(SetFriendActivity.this, ConstantUtil.FRIEND_CHECK)){
			friendPushCheck.setSelected(true);
		}else{
			friendPushCheck.setSelected(false);
		}
		
		friendPushCheck.setOnClickListener(checkListener);
```

> ## 6. 添加好友  SetFriendAddActivity

<h1 id="23">23. 我的收藏 SetCollectionActivity</h1>  

## [返回目录](#0)

> ## 1. 主要是列表显示咨询的信息

<h1 id="24">24. 数据管理 CeLingDataActivity</h1>  

## [返回目录](#0)

> ## 1. 如何刷新本地的数据  只有一个list列表

```
 首先，列表从本地数据库读取数据。
当点击刷新时，访问服务器，获得数据后，删除本地数据，
然后将服务端的数据存到本地，标记为已经同步。
```
<h1 id="25">25. 生活日志 SetLifeDataActivity</h1>  

## [返回目录](#0)

> ## 1. 记录每天的日志  并包括日志的同步和上传

```
// 设置日历日期
			Date date = format.parse(DateUtil.getNowDate(DateUtil.YEAR_MONTH_DAY));

/**
	 * 获取当前日期   用指定的格式来显示
	 * 
	 * @return
	 */

	public static String getNowDate(String dateFormat) {
		SimpleDateFormat sDateFormat = new SimpleDateFormat(dateFormat);

		return sDateFormat.format(new Date());
	}


```
> ## 2. 日历控件的设置

```
//设置监听
		calendarLeft.setOnClickListener(new MyViewOnclicklistener());
		calendarRight.setOnClickListener(new MyViewOnclicklistener());
		calendar.setOnItemClickListener(itemListener);
```

> ## 3. 设置生活日志的数值是，一方面保存到本地，保存到本地时同步状态为0。一方面上传到服务端，上传成功后修改同步状态为1。插入数据时先进行查询判断，按用户和日期从数据查询，没有数据就插入数据库，否则修改数据库的数据。


<h1 id="26">26. 心衰助手 MainHelpActivity</h1>  

## [返回目录](#0)

> ## 1. 没有实际的业务，只是一个跳转和过度。

<h1 id="27">27. 心率记录 HelpHeartActivity</h1>  

## [返回目录](#0)

> ## 1. [ViewFlipper的学习，实现公告轮播条，界面切换动画的效果...](http://www.jianshu.com/p/40f1c8508710)

```
//实现两个界面的切换
<ViewFlipper
        android:id="@+id/help_weight_plipper"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_above="@+id/help_weight_menu"
        android:layout_below="@+id/helpHeartTopBar"
        android:layout_marginLeft="20dp"
        android:layout_marginRight="20dp"
        android:layout_marginTop="20dp" >

        <com.yikang.heartmark.view.HelpHeartWeekView
            android:id="@+id/weekView"
            android:layout_width="match_parent"
            android:layout_height="match_parent" />

        <com.yikang.heartmark.view.HelpHeartMonthView
            android:id="@+id/monthView"
            android:layout_width="match_parent"
            android:layout_height="match_parent" />
    </ViewFlipper>
```
> ## 2. 把一个xml图层，导入另外一个xml中

```
 <LinearLayout
        android:id="@+id/help_weight_menu"
        android:layout_width="match_parent"
        android:layout_height="40dp"
        android:layout_alignParentBottom="true"
        android:layout_marginBottom="30dp"
        android:layout_marginLeft="20dp"
        android:layout_marginRight="20dp"
        android:layout_marginTop="20dp" >

        <include
            android:id="@+id/help_weight_menubar"
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="2"
            layout="@layout/data_curve_menubar" />

        <Button
            android:id="@+id/help_weight_detail"
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:background="@drawable/help_info_selector"
            android:text="详情"
            android:textColor="@color/app_color"
            android:textSize="18dp" />
    </LinearLayout>




<?xml version="1.0" encoding="utf-8"?>
<com.yikang.heartmark.view.MenuBarView 
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="40dp"
    android:layout_margin="10dp"
    android:orientation="horizontal" >

    <LinearLayout
        android:layout_width="wrap_content"
        android:layout_height="match_parent"
        android:layout_weight="1"
        android:background="@drawable/help_week_selector"
        android:gravity="center"
        android:orientation="vertical" >

        <TextView
            android:id="@+id/help_week_text"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="周"
            android:textColor="@color/app_color"
            android:textSize="18dp" >
        </TextView>
    </LinearLayout>

    <LinearLayout
        android:layout_width="wrap_content"
        android:layout_height="match_parent"
        android:layout_weight="1"
        android:background="@drawable/help_month_selector"
        android:gravity="center"
        android:orientation="vertical" >

        <TextView
            android:id="@+id/help_month_text"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="月"
            android:textColor="@color/app_color"
            android:textSize="18dp" >
        </TextView>
    </LinearLayout>

</com.yikang.heartmark.view.MenuBarView>
```
> ## 3. 自定义的线性布局

```
package com.yikang.heartmark.view;

import android.content.Context;
import android.util.AttributeSet;
import android.view.View;
import android.widget.LinearLayout;

public class MenuBarView extends LinearLayout {

	private OnMenuBarListener menuBarListener = null;

	public MenuBarView(Context context) {
		super(context);
	}
	
	/****************** 这是构造器******************************/
	public MenuBarView(Context context, AttributeSet attrs) {
		super(context, attrs);
	}
    /*************************************************************/
	

	//当从XML布局加载文件并用它来构建视图时，回调这个方法
	@Override
	protected void onFinishInflate() {
		super.onFinishInflate();
		init();
	}

	private void init() {
		OnClickListener listener = new OnClickListener() {

			@Override
			public void onClick(View v) {
				setSelectedView(v);
			}
		};
		//判断有多少个子元素
		int count = this.getChildCount();
		for (int i = 0; i < count; i++) {
			//对每一个子元素都加入监听
			View child = this.getChildAt(i);
			child.setOnClickListener(listener);
		}
	}

	public boolean isSelectedByIndex(int index) {
		boolean isSelected = false;
		if (index >= 0) {
			View child = this.getChildAt(index);
			isSelected = child.isSelected(); //这个应用的是View中的方法 TextView是View的子类
		}
		return isSelected;
	}

	public void setSelectedIndex(int index) {
		if (index >= 0 && index < this.getChildCount()) //这个是ViewGroup中的方法  得到子控件的个数
			setSelectedView(this.getChildAt(index));
	}

	private void setSelectedView(View view) {
//在子元素被点击时   判断子元素是否被选中
		if (view.isSelected())
			return;

		int count = this.getChildCount();
		int menuIndex = 0;
		for (int i = 0; i < count; i++) {
			View child = this.getChildAt(i);
			//判断两个视图是同一个视图
			if (child == view) {
				child.setSelected(true);
				menuIndex = i;
			} else
				child.setSelected(false);   //View中的方法  表明该控件未被选中
		}
		if (menuBarListener != null)
			menuBarListener.onMenuBarItemSelected(menuIndex);
	}

	/**
	 * 设置菜单页面的监听事件   外部设置的接口
	 */
	public void setOnMenuBarListener(OnMenuBarListener listener) {
		menuBarListener = listener;//让外部的接口注册进来
	}
	public interface OnMenuBarListener {      //接口
		//这个是接口下的方法，是要被集成和详细写的
		public void onMenuBarItemSelected(int menuIndex);
	}
}

```
> ## 4. 接口的运用

```
/**
	 * 设置菜单页面的监听事件   外部设置的接口注册进来
	 */
	public void setOnMenuBarListener(OnMenuBarListener listener) {
		menuBarListener = listener;//让外部的接口注册进来
	}
	public interface OnMenuBarListener {      //接口
		//这个是接口下的方法，是要被集成和详细写的
		public void onMenuBarItemSelected(int menuIndex);
	}
```
> ## 5. Android游戏开发之旅View类详解自定义View的常用方法:onFinishInflate

```
Android游戏开发之旅 View类详解
　　自定义 View的常用方法:
　　onFinishInflate() 当View中所有的子控件 均被映射成xml后触发
　　onMeasure(int, int) 确定所有子元素的大小
　　onLayout(boolean, int, int, int, int) 当View分配所有的子元素的大小和位置时触发
　　onSizeChanged(int, int, int, int) 当view的大小发生变化时触发
　　onDraw(Canvas) view渲染内容的细节
　　onKeyDown(int, KeyEvent) 有按键按下后触发
　　onKeyUp(int, KeyEvent) 有按键按下后弹起时触发
　　onTrackballEvent(MotionEvent) 轨迹球事件
　　onTouchEvent(MotionEvent) 触屏事件
　　onFocusChanged(boolean, int, Rect) 当View获取 或失去焦点时触发
　　onWindowFocusChanged(boolean) 当窗口包含的view获取或失去焦点时触发
　　onAttachedToWindow() 当view被附着到一个窗口时触发
　　onDetachedFromWindow() 当view离开附着的窗口时触发，Android123提示该方法和 onAttachedToWindow() 是相反的。
　　onWindowVisibilityChanged(int) 当窗口中包含的可见的view发生变化时触发
　　以上是View实现的一些基本接口的回调方法，一般我们需要处理画布的显示时，重写onDraw(Canvas)用的的是最多的：
```
> ## 6. 控件的使用

```
flipperView = (ViewFlipper) findViewById(R.id.help_weight_plipper);
		weekView = (HelpHeartWeekView) findViewById(R.id.weekView);
		monthView = (HelpHeartMonthView) findViewById(R.id.monthView);
		menuBarView = (MenuBarView) findViewById(R.id.help_weight_menubar);
		//把Activity注册进接口
		menuBarView.setOnMenuBarListener(this);
		//默认选中第一个控件
		menuBarView.setSelectedIndex(0); 
```
> ## 7. ViewFlipper

```
一、基本实现
ViewFlipper是一个切换控件，一般用于图片的切换，当然它是可以添加View的，而不限定只用于ImageView，当然我们也可以自定义View，只是我们经常利用ViewFlipper来实现的是ImageView的切换，如果切换自定义的View，倒还不如使用ViewPager来做。


<ViewFlipper  
        android:id="@+id/flipper"  
        android:layout_width="match_parent"  
        android:layout_height="wrap_content"  
        android:layout_alignParentTop="true"  
        android:layout_marginTop="10dp"  
        android:flipInterval="2000" >  
        <ImageView   
            android:layout_width="fill_parent"  
            android:layout_height="300dip"  
            android:scaleType="fitXY"  
            android:src="@drawable/img_1"/>  
        <ImageView   
            android:layout_width="fill_parent"  
            android:layout_height="300dip"  
            android:scaleType="fitXY"  
            android:src="@drawable/img_2"/>  
        <ImageView   
            android:layout_width="fill_parent"  
            android:layout_height="300dip"  
            android:scaleType="fitXY"  
            android:src="@drawable/img_3"/>  
        <ImageView   
            android:layout_width="fill_parent"  
            android:layout_height="300dip"  
            android:scaleType="fitXY"  
            android:src="@drawable/img_4"/>  
    </ViewFlipper>  
  

Java代码
 flipper = (ViewFlipper) findViewById(R.id.flipper);  
        flipper.startFlipping();  

ViewFlipper::showNext();  //显示下一个视图  
ViewFlipper::showPrevious(); //显示上一个视图  



加入手势控制切换图片
public class MainActivity extends Activity implements OnTouchListener {  
  
    private ViewFlipper mFlipper;  
    private GestureDetector mDetector; //手势检测  
    @Override  
    protected void onCreate(Bundle savedInstanceState) {  
        super.onCreate(savedInstanceState);  
        setContentView(R.layout.activity_main);  
          
        mFlipper = (ViewFlipper) findViewById(R.id.flipper);      
        mFlipper.setOnTouchListener(this);  
          
        mDetector = new GestureDetector(new simpleGestureListener());  
    }  
      
    public boolean onTouch(View v, MotionEvent event) {  
        return mDetector.onTouchEvent(event);  
    }  
      
    private class simpleGestureListener extends GestureDetector.SimpleOnGestureListener{  
        final int FLING_MIN_DISTANCE = 100, FLING_MIN_VELOCITY = 200;    
          
        //不知道为什么，不加上onDown函数的话，onFling就不会响应，真是奇怪  
        @Override  
        public boolean onDown(MotionEvent e) {  
            // TODO Auto-generated method stub  
            Toast.makeText(MainActivity.this, "ondown", Toast.LENGTH_SHORT).show();     
            return true;  
        }  
        @Override  
        public boolean onFling(MotionEvent e1, MotionEvent e2, float velocityX,  
                float velocityY) {  
            // Fling left       
            if (e1.getX() - e2.getX() > FLING_MIN_DISTANCE      
                    && Math.abs(velocityX) > FLING_MIN_VELOCITY) {      
  
                mFlipper.showNext();  
  
                Toast.makeText(MainActivity.this, "Fling Left", Toast.LENGTH_SHORT).show();      
            } else if (e2.getX() - e1.getX() > FLING_MIN_DISTANCE      
                    && Math.abs(velocityX) > FLING_MIN_VELOCITY) {      
                // Fling right       
   
                mFlipper.showPrevious();  
                  
                Toast.makeText(MainActivity.this, "Fling Right", Toast.LENGTH_SHORT).show();      
            }        
            return true;    
        }  
    }  
  
}  
```
> ## 8. 自定义的两个显示图表的线性视图

```
Calendar
int month = calendar.get(Calendar.MONTH)+1;//月份从0开始计算，输出要加1


Java正确获取星期Calendar.DAY_OF_WEEK

以下参考：

1. 在获取月份时，Calendar.MONTH + 1 的原因 Java中的月份遵循了罗马历中的规则：当时一年中的月份数量是不固定的，第一个月是JANUARY。而Java中Calendar.MONTH返回的数值其实是当前月距离第一个月有多少个月份的数值，JANUARY在Java中返回“0”，所以我们需要+1。

2. 在获取星期几 Calendar.DAY_OF_WEEK – 1 的原因

Java中Calendar.DAY_OF_WEEK其实表示：一周中的第几天，所以他会受到  第一天是星期几 的影响。

有些地区以星期日作为一周的第一天，而有些地区以星期一作为一周的第一天，这2种情况是需要区分的。

看下表的返回值

星期日为一周的第一天	SUN	MON	TUE	WED	THU	FRI	SAT
DAY_OF_WEEK返回值	1	2	3	4	5	6	7
星期一为一周的第一天	MON	TUE	WED	THU	FRI	SAT	SUN
DAY_OF_WEEK返回值	1	2	3	4	5	6	7
所以Calendar.DAY_OF_WEEK需要根据本地化设置的不同而确定是否需要 “-1” Java中设置不同地区的输出可以使用 Locale.setDefault(Locale.地区名) 来实现。

System.out.println(calendar.get(Calendar.DAY_OF_WEEK));

返回的是周几，而不是一周的第几天

可以这样设置，星期第一天是星期几：

calendar.setFirstDayOfWeek(Calendar.MONDAY);

也可以设置Calendar.SUNDAY

设置好了就决定了当前日期的WEEK_OF_YEAR， 但并不会改变DAY_OF_WEEK !

3. 获取日期时 Calendar.DAY_OF_MONTH 不需要特殊的操作，他直接返回一个月中的第几天





数据库中查询数据
/**新该
	 * 查询  当前时间   所在周 的一周内的数据  时间段
	* <p>Title: getHeartListByTime</p>
	* <p>Description: </p>
	* @param date
	* @param uid
	* @param startTime
	* @param endTime
	* @return
	 */
	public ArrayList<HelpHeart> getHeartListByTime(Date date, String uid, long startTime, long endTime){
		SQLiteDatabase db = helper.getWritableDatabase();
		
		ArrayList<HelpHeart> helpHeartArray = new ArrayList<HelpHeart>();
		
		SimpleDateFormat sdf=new SimpleDateFormat("yyyy-MM:dd");  //格式化时间的类
		
        Calendar cal = Calendar.getInstance();  
        cal.setTime(date);  
        //cal.get(Calendar.DAY_OF_WEEK);
        //----------------从星期天开始计算，如果今天星期二，那么返回3  
        // 1代表是星期天
        int dayWeek = cal.get(Calendar.DAY_OF_WEEK);  
        if(1 == dayWeek) {  
        //代表如果是星期天   就返回一天前的日期
        	cal.add(Calendar.DAY_OF_MONTH, -1);  
        }  
      //将本周的星期一设为日历的时间  星期第一天是星期一：
		cal.setFirstDayOfWeek(Calendar.MONDAY);  
		//一周中的第几天 就不用减1了
		int day = cal.get(Calendar.DAY_OF_WEEK);  
		//让日历中的天数提前几天
		//getFirstDayOfWeek() 获取一星期的第一天；例如，在美国，这一天是 SUNDAY，而在法国，这一天是 MONDAY。
		// 想前推算到星期一的时间
		cal.add(Calendar.DATE, cal.getFirstDayOfWeek()-day);  
		
		//利用循环将现在时间的一周之内的数据抽取出来
		// 通过这个循环取出一周内的数据
		for(int i = 0;i<=6;i++){
			if(i!=0){
				//只有不是第一个数据，日期就不断加1
				cal.add(Calendar.DATE, 1);  
			}
			
			//将月份和日期格式化  yyyy-MM:dd
			String imptimeEnd = sdf.format(cal.getTime());  
			//这个是年和月
			String dateMonth = imptimeEnd.substring(0, imptimeEnd.indexOf(":"));
				//这个是日期
			String dayString = imptimeEnd.substring(imptimeEnd.lastIndexOf(":")+1,imptimeEnd.length());
			
			Cursor cursor = db.query("heart", new String[] { "id", "uid", "sync","date",
					"dateMonth", "day", "time", "timeMill", "heart"}, 
					"uid=? and dateMonth=? and day= ?", new String[] {uid, dateMonth, 
					dayString}, null, null,null);
			if (cursor.moveToNext()) {
				HelpHeart helpHeart = new HelpHeart();
				helpHeart.id = cursor.getInt(cursor.getColumnIndex("id"));
				helpHeart.uid = cursor.getString(cursor.getColumnIndex("uid"));
				helpHeart.sync = cursor.getInt(cursor.getColumnIndex("sync"));
				helpHeart.date = cursor.getString(cursor.getColumnIndex("date"));
				helpHeart.dateMonth = cursor.getString(cursor.getColumnIndex("dateMonth"));
				helpHeart.day = cursor.getString(cursor.getColumnIndex("day"));
				helpHeart.time = cursor.getString(cursor.getColumnIndex("time"));
				helpHeart.timeMill = cursor.getLong(cursor.getColumnIndex("timeMill"));
				helpHeart.heart = cursor.getInt(cursor.getColumnIndex("heart"));
				helpHeartArray.add(helpHeart);
			}
			cursor.close();
		}
		
		
		db.close();
		return helpHeartArray;
	}


```
> ## 9. 心率图表的显示方法

```
package com.yikang.heartmark.view;

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.ArrayList;
import java.util.Calendar;
import java.util.Date;
import java.util.List;

import org.achartengine.ChartFactory;
import org.achartengine.GraphicalView;
import org.achartengine.chart.PointStyle;
import org.achartengine.model.XYMultipleSeriesDataset;
import org.achartengine.model.XYSeries;
import org.achartengine.renderer.XYMultipleSeriesRenderer;
import org.achartengine.renderer.XYSeriesRenderer;

import android.annotation.SuppressLint;
import android.content.Context;
import android.graphics.Color;
import android.graphics.Paint.Align;
import android.util.AttributeSet;
import android.view.LayoutInflater;
import android.widget.LinearLayout;

import com.example.heartmark.R;
import com.yikang.heartmark.database.HelpHeartDB;
import com.yikang.heartmark.model.HelpHeart;
import com.yikang.heartmark.util.ConstantUtil;
import com.yikang.heartmark.util.DateUtil;

@SuppressLint("SimpleDateFormat")
public class HelpHeartWeekView extends LinearLayout {
	private Context context;
	public List<Integer> dayList = new ArrayList<Integer>(); //日期的链表
	public List<Double> valueList = new ArrayList<Double>();  //日期对应的值
	private String uid;
	private HelpHeartDB heartDB = null;

	public HelpHeartWeekView(Context context) {
		super(context);
		this.context = context;
		LayoutInflater.from(context).inflate(R.layout.huli_weight_view, this,
				true);
		init();
	}

	public HelpHeartWeekView(Context context, AttributeSet attrs) {
		super(context, attrs);
		this.context = context;
		LayoutInflater.from(context).inflate(R.layout.huli_weight_view, this,
				true);
		init();
	}

	private void init() {
		uid = ConstantUtil.getUid(context);
		heartDB = new HelpHeartDB(context);
		showCurve();   // 显示表格
	}
	
	SimpleDateFormat df = new SimpleDateFormat("yyyy-MM-dd");
	
	public static Integer getWeekOfDate(Date date) {
		Integer[] weekDaysCode = {6, 0, 1, 2, 3, 4, 5};
		Calendar calendar = Calendar.getInstance();
		calendar.setTime(date);
		//获取星期是周要减1
		int intWeek = calendar.get(Calendar.DAY_OF_WEEK) - 1;
		return weekDaysCode[intWeek];
	}
	
	// 显示表格
	public void showCurve() {
		dayList.clear();   //清空数据
		valueList.clear();   //清空数据
		ArrayList<HelpHeart> heartList = heartDB.getHeartListByTime(new Date(),uid,
				DateUtil.getThisWeekOfMonday(), DateUtil.getThisWeekOfSunday());
		if(heartList.size() == 0){
			dayList.add(0);
			valueList.add(0.0);
		}
		for (int i = 0; i < heartList.size(); i++) {
			try {
				dayList.add(getWeekOfDate(df.parse(heartList.get(i).date)));
				valueList.add(Double.valueOf(heartList.get(i).heart));
			} catch (ParseException e) {
				e.printStackTrace();
			}
		}
		
		String[] weekDaysName = { "周一", "周二", "周三", "周四", "周五", "周六","周日" };
		XYMultipleSeriesRenderer renderer = new XYMultipleSeriesRenderer();
		renderer.setBackgroundColor(Color.parseColor("#ffffff"));// 表格背景颜色
		renderer.setMarginsColor(Color.parseColor("#ffffff"));// 表格四周的颜色
		renderer.setApplyBackgroundColor(true);// 是否显示表格内的颜色

		renderer.setLabelsTextSize(30f);// 坐标轴字体大小
		renderer.setAxisTitleTextSize(30f); // 设置表示x轴，Y轴信息文本的大小
		renderer.setXTitle("时间(天)"); // 设置x轴名字
		renderer.setYTitle("心率(bpm)"); // y轴名字
		renderer.setXAxisMin(1); // x轴坐标最小值
		renderer.setXAxisMax(7); // x轴坐标最大值
		renderer.setXLabelsColor(Color.parseColor("#000000"));
		renderer.setYAxisMin(0); // y轴最小值
		renderer.setYAxisMax(150); // y值最大值
		renderer.setYLabelsColor(0, (Color.parseColor("#000000")));
		renderer.setPointSize(2f); // 点的大小
		renderer.setLabelsColor(Color.parseColor("#000000")); // x,y轴标题颜色（时间。。。）
		renderer.setAxesColor(Color.parseColor("#000000"));// 坐标轴的颜色
		renderer.setLegendTextSize(10f); // 设置下方表示曲线名字的文本字体大小
		renderer.setChartTitleTextSize(20f); // 曲线图说明文字的大小

		renderer.setMargins(new int[] { 80, 80, 40, 40 }); // 数据分别为曲线图离屏幕的上左下右的间距
		renderer.setPanLimits(new double[] { 0, 31, 0.00, 35.00 });
		renderer.setXLabels(weekDaysName.length); // 网格x轴的大概条数
		renderer.setYLabels(10); // 网格Y轴的大概条数
		renderer.setShowGrid(true); // 是否显示网格
		renderer.setGridColor(Color.parseColor("#dfdfdf"));// 分割线的颜色
		renderer.setYLabelsAlign(Align.RIGHT); // 以Y轴的哪个地方对其
		renderer.setZoomButtonsVisible(false); // 是否显示右下角的放大缩小还原按钮
		renderer.setZoomEnabled(false, false);// 设置图表是否缩放
		renderer.setPanEnabled(false, false); // 设置图表是否移动 参数为 x,y轴s

		// 曲线设置
		XYSeriesRenderer xyRenderer = new XYSeriesRenderer();
		xyRenderer.setColor(Color.parseColor("#000000"));// 曲线点线的颜色
		xyRenderer.setLineWidth(3f);// 曲线的线宽
		xyRenderer.setDisplayChartValues(false);// 是否显示曲线上的点的值
		xyRenderer.setChartValuesTextSize(30f);// 曲线值得字体大小
		xyRenderer.setPointStyle(PointStyle.CIRCLE);// 点的形状
		xyRenderer.setFillBelowLine(true);// 是否显示线下的阴影
		xyRenderer.setFillBelowLineColor(Color.parseColor("#4fc1e9"));// 阴影的颜色
		xyRenderer.setFillPoints(true);// 是否为实心点
		renderer.addSeriesRenderer(xyRenderer);

/*		renderer.clearXTextLabels();
		for (int k = 0; k < weekDaysName.length; k++) {// 填充x轴
			renderer.addXTextLabel(k, weekDaysName[k]);
		}*/
		
		// 进行显示
		XYMultipleSeriesDataset dataset = new XYMultipleSeriesDataset(); // 设置图下面显示的信息
		XYSeries series = new XYSeries("");
		for (int i = 0; i < dayList.size(); i++) {
			series.add(dayList.get(i)+1, Double.valueOf(valueList.get(i)));
		}
		dataset.addSeries(series);
		
		// 生成图表视图
		GraphicalView graphicalView = ChartFactory.getCubeLineChartView(
				context, dataset, renderer, 0.3f);
		graphicalView.setId(0);

		LinearLayout curveWeekLayout = (LinearLayout) findViewById(R.id.huli_curve_layout);
		curveWeekLayout.removeAllViews();
		// 添加至父容器
		curveWeekLayout.addView(graphicalView, new LayoutParams(
				LayoutParams.MATCH_PARENT, LayoutParams.MATCH_PARENT));
	}
}

```

<h1 id="28">28. 出入水量 HelpWaterActivity</h1>  

## [返回目录](#0)

> ## 1. 视图 ListView

```
 <ListView
                android:id="@+id/help_water_listview"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:listSelector="@android:color/transparent" >
            </ListView>
```

<h1 id="29">29. 心率详情 HelpHeartInfoActivity</h1>  

## [返回目录](#0)

> ## 1. 默认是读取本地的数据，只有点更新的时候才后下载服务端的数据。服务端数据下载成功后，先删除本地同步了的数据，在向数据库插入数据。

```
@SuppressWarnings({ "rawtypes", "unchecked" })
	public void getDataCallBack(Object data) {
		handlerBase.sendEmptyMessage(ConstantUtil.DIALOG_HINT);
		Map resultMap = (Map) data;
		if (resultMap == null) {
			ShowUtil.showToast(HelpHeartInfoActivity.this,
					R.string.check_network_timeout);
		} else {
			String result = (String) resultMap.get("head");
			if (result.equals("success")) {
				//删除已经同步的数据
				heartDB.deleteBySync(uid);
				List<Map> list = (List) resultMap.get("nurseInfoList");
				for (int i = 0; i < list.size(); i++) {
					//没有数据，跳出本次循环
					if(list.get(i).get("HEART_RATE") == null){
						continue;
					}
					
					HelpHeart heart = new HelpHeart();
					heart.uid = uid;
					heart.sync = ConstantUtil.SYNC_YES;
					String celingTime = (String) list.get(i).get("NURSE_DATE");
					heart.date = celingTime.substring(0, 10);
					heart.dateMonth = celingTime.substring(0, 7);
					heart.day = celingTime.substring(8, 10);
					heart.timeMill = DateUtil.getLongOfDayTime(celingTime);
				  //heart.time = celingTime.substring(11, 16);
					heart.heart = Double.valueOf(list.get(i).get("HEART_RATE").toString()).intValue();
					heartDB.insert(heart);
				}
				//刷新列表
				refreshDayListView();
				ShowUtil.showToast(HelpHeartInfoActivity.this,
						R.string.sync_success);
			} else if (result.equals("fail")) {
				ShowUtil.showToast(HelpHeartInfoActivity.this,
						R.string.sync_fail);
			}

		}
	}
```
> ## 2. 刷新数据列表，分别在Activity初始化时和数据改变时。

```
/**
	 * 刷新月份天数的表格
	 */
	private void refreshDayListView() {
		int height = 0;
		int normal = 0;
		int low = 0;
		String date = textViewMonth.getText().toString().trim();
		List<HelpHeart> dataAddList = new ArrayList<HelpHeart>();
		dataAddList = new HelpHeartDB(HelpHeartInfoActivity.this)
				.getHeartListByMonth(date, ConstantUtil.getUid(HelpHeartInfoActivity.this));
		HelpHeartInfoAdapter myAdapter = new HelpHeartInfoAdapter(
				HelpHeartInfoActivity.this, dataAddList);
		listView.setAdapter(myAdapter);
		listView.setFooterDividersEnabled(false);
		
		for(int i=0; i<dataAddList.size(); i++){
			if(dataAddList.get(i).heart < 60){
				low ++;
			}else if(dataAddList.get(i).heart >= 60 && dataAddList.get(i).heart <= 100){
				normal ++;
			}else if(dataAddList.get(i).heart >= 100){
				height ++;
			}
		}
		
		heartHeight.setText(String.valueOf(height));
		heartNormal.setText(String.valueOf(normal));
		heartLow.setText(String.valueOf(low));
	}
```
> ## 3. 当前 上一个 下一个 月份 日期的判断

```
//这个是上一个月的信息
	private void lastMonth() {
		String date = textViewMonth.getText().toString().trim();
		String[] strs = date.split("-");
		//获取到年和月的信息
		int year = Integer.parseInt(strs[0]);
		int month = Integer.parseInt(strs[1]);
		if (month == 1) {
			year -= 1;
			month = 12;
		} else {
			month -= 1;
		}
		//这个是判断月份是个位数还是2位数
		if (month < 10) {
			date = year + "-" + "0" + month;
		} else {
			date = year + "-" + month;
		}
		textViewMonth.setText(date);
		refreshDayListView();
	}


	//这个是下一个月的信息
	private void nextMonth() {
		String date1 = textViewMonth.getText().toString().trim();
		String[] strs1 = date1.split("-");
		int year1 = Integer.parseInt(strs1[0]);
		int month1 = Integer.parseInt(strs1[1]);
		if (month1 == 12) {
			year1 += 1;
			month1 = 1;
		} else {
			month1 += 1;
		}
		if (month1 < 10) {
			date1 = year1 + "-" + "0" + month1;
		} else {
			date1 = year1 + "-" + month1;
		}
		textViewMonth.setText(date1);
		refreshDayListView();
	}



public static final String YEAR_MONTH = "yyyy-MM";


//这个是获取当月的信息
		textViewMonth.setText(DateUtil.getNowDate(DateUtil.YEAR_MONTH));

/**
	 * 获取当前日期   用指定的格式来显示
	 * 
	 * @return
	 */

	public static String getNowDate(String dateFormat) {
		SimpleDateFormat sDateFormat = new SimpleDateFormat(dateFormat);

		return sDateFormat.format(new Date());
	}
```

<h1 id="30">30. 病情评估 MainPingGuActivity</h1>  

## [返回目录](#0)

> ## 1. 叠加布局的用法，设置图片作为背景，在设置一个文本作为相对布局，在底部并且距底10dp，左右居中。

```
 <RelativeLayout
        android:layout_width="wrap_content"
        android:layout_height="0dp"
        android:layout_weight="2"
        android:background="@drawable/pinggu_show" >

        <TextView
            android:id="@+id/pinggu_count"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignParentBottom="true"
            android:layout_centerHorizontal="true"
            android:layout_marginBottom="10dp"
            android:textColor="@color/white"
            android:textSize="20sp" />
    </RelativeLayout>
```
> ## 2. 从服务端取得所有评估次数 

```
//从服务端取得所有评估次数  
	@SuppressWarnings({ "rawtypes"})
	public void getCountCallBack(Object data) {
		handlerBase.sendEmptyMessage(ConstantUtil.DIALOG_HINT);
		Map resultMap = (Map) data;
		if (resultMap == null) {
			ShowUtil.showToast(MainPingGuActivity.this,R.string.check_network_timeout);
		} else {
			Map countMap = (Map) resultMap.get("body");
//			intValue()是把Integer对象类型变成int的基础数据类型；
			int count = Double.valueOf(countMap.get("COUNT").toString()).intValue();
			// 已有%d人进行评估  按照这个格式 格式字符串
			textViewCount.setText(String.format(getResources().getString(R.string.pinggu_count),count));
		}
	}
```

<h1 id="31">31. 心衰评估1 PingGuInfoActivity</h1>  

## [返回目录](#0)

> ## 1. 评估答题的页面

```
package com.yuzhi.framework.util;

import com.google.gson.Gson;

public class JsonUtil<T> {

	public Object convertJsonToObject(String value,Class<T> object){
		Object resultObject = new Object();
		Gson gson = new Gson();
		resultObject = gson.fromJson(value, object);
		return resultObject;
	}
	
	public static Object convertJsonToObject(String value){
		Object resultObject = new Object();
		Gson gson = new Gson();
		resultObject = gson.fromJson(value, Object.class);
		return resultObject;
	}
	
	//使用Gson将Java对象转换为JSON
	public static String convertObjectToJson(Object obj){
		String result = "";
		Gson gson = new Gson();
		result = gson.toJson(obj);
		return result;
	}
}

```

<h1 id="32">32. 历史评估 PingGuHistoryActivity</h1>  

## [返回目录](#0)

> ## 1. 评估报告的列表显示

> ## 2. Math 以及 DecimalFormat 学习总结

```
二DecimalFormat 学习总结
DecimalFormat 是 NumberFormat 的一个具体子类，用于格式化十进制数字。
DecimalFormat 包含一个模式 和一组符号
符号含义：
0 一个数字
“# ” (在文章中不显示 因此添加双引号)
一个数字，不包括 0
. 小数的分隔符的占位符
, 分组分隔符的占位符
; 分隔格式。

缺省负数前缀。
% 乘以 100 和作为百分比显示
例子：

DecimalFormat df1 = new DecimalFormat("0.0");

DecimalFormat df2 = new DecimalFormat("#.#");

DecimalFormat df3 = new DecimalFormat("000.000");

DecimalFormat df4 = new DecimalFormat("###.###");

System.out.println(df1.format(12.34));

System.out.println(df2.format(12.34));

System.out.println(df3.format(12.34));

System.out.println(df4.format(12.34));

结果：

12.3

12.3

012.340

12.34
```

<h1 id="33">33. 心衰评估2 PingGuForthwithActivity</h1>  

## [返回目录](#0)

> ## 1. 这个是笔记本形状的图片 这个是xml视图

```

        <TextView
            android:id="@+id/pingguForthwithResult"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginLeft="30dp"
            android:layout_marginRight="15dp"
            android:layout_marginTop="30dp"
            android:layout_marginBottom="25dp"
            android:lineSpacingExtra="4dp"
            android:textSize="18sp"
            android:textColor="@color/typeface"
             />
```
> ## 2. TextView linespacingextra&lineSpacingMultiplier

```
Mark一下这个知识点

Android TextView 调整行间距可以使用linespacingextra和lineSpacingMultiplier 这两个参数，但是设置这两个参数之后，间距会出现的文字的下面，文字并不会上下居中显示，具体效果可以打开Android 开发者模式->显示布局边界查看。

开发过程中可能会碰到一些奇怪的需求，需要自定义行距，又希望界面其他元素与文本垂直居中对齐，目前只能特殊处理，有说法是framework 里面默认了文本是左上开始显示的，如果需要文本居中需要修改framework 代码，不过这个还没有详细验证。
```
<h1 id="34">34. 心衰评估3 PingGuStageActivity</h1>  

## [返回目录](#0)

> ## 1. 这个是显示横向进度条和饼形进度条的页面

```
横向进度条的自定义方法
 <com.yikang.heartmark.view.ProgressDoubleView
                android:id="@+id/pingguResultProgress"
                android:layout_width="match_parent"
                android:layout_height="wrap_content" >
            </com.yikang.heartmark.view.ProgressDoubleView>



package com.yikang.heartmark.view;

import android.content.Context;
import android.util.AttributeSet;
import android.view.LayoutInflater;
import android.widget.LinearLayout;
import android.widget.SeekBar;

import com.example.heartmark.R;

public class ProgressDoubleView extends LinearLayout {
	private SeekBar seekBarTop;
	private SeekBar seekBarBottom;

	public ProgressDoubleView(Context context) {
		super(context);
		LayoutInflater.from(context).inflate(R.layout.progress_double_layout, this, true);
		init();
	}

	public ProgressDoubleView(Context context, AttributeSet attrs) {
		super(context, attrs);
		LayoutInflater.from(context).inflate(R.layout.progress_double_layout, this, true);
		init();
	}

	private void init() {
		seekBarTop = (SeekBar) findViewById(R.id.seekTop);
		seekBarBottom = (SeekBar) findViewById(R.id.seekBottom);
		seekBarTop.setEnabled(false);
		seekBarBottom.setEnabled(false);
	}

	public void setProgress(int progress) {
		seekBarTop.setProgress(progress);
		seekBarBottom.setProgress(progress);
	}

}



<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center_horizontal"
    android:orientation="vertical" >

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="15dp"
        android:text="病症评估指数"
        android:textColor="@color/app_color"
        android:textSize="22dp" />

    <SeekBar
        android:id="@+id/seekTop"
        android:layout_width="250dp"
        android:layout_height="wrap_content"
        android:layout_marginLeft="10dp"
        android:layout_marginRight="10dp"
        android:layout_marginTop="20dp"
        android:max="100"
        android:progress="50"
        android:progressDrawable="@drawable/pinggu_result_progress_img"
        android:thumb="@drawable/pinggu_result_thumb" />

    <!-- 这个是底部的横向导航条  背景是透明色，指示条是三角 -->
    <SeekBar
        android:id="@+id/seekBottom"
        android:layout_width="250dp"
        android:layout_height="wrap_content"
        android:layout_marginLeft="10dp"
        android:layout_marginRight="10dp"
        android:max="100"
        android:progress="50"
        android:progressDrawable="@color/transparent"
        android:thumb="@drawable/pinggu_result_progress_arrow" />

    <RelativeLayout
        android:layout_width="250dp"
        android:layout_height="wrap_content"
        android:layout_marginLeft="15dp"
        android:layout_marginRight="15dp" >

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="低"
            android:textColor="@color/typeface"
            android:textSize="22dp" />

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignParentRight="true"
            android:text="高"
            android:textColor="@color/typeface"
            android:textSize="22dp" />
    </RelativeLayout>

</LinearLayout>
```
> ## 2. xcl-charts.jar  这个是饼图的包 [使用xcl图表库简单实现android不平均点折线图绘制](http://www.jianshu.com/p/ad83e51ccb7c)

```
//饼形图
			//View pieChart = new PicChartUtil().execute(this,100-percent.intValue(),percent.intValue());
			PieChart01View pieChart = new PieChart01View(PingGuStageActivity.this);
			pieChart.setLayoutParams(new LayoutParams(LayoutParams.MATCH_PARENT, LayoutParams.MATCH_PARENT));
			pieChart.initView(percentInt);
			cakeLayout.addView(pieChart);
```

<h1 id="35">35. 智能咨询 MainYiShiActivity</h1>  

## [返回目录](#0)

> ## 1. 这个是咨询回复的环节

<h1 id="36">36. 咨询会话 YiShiChatActivity</h1>  

## [返回目录](#0)

> ## 1. 获取圆角位图的方法

```
//调用的方法
userBitmap = ImageUtilBase.toRound(
					BitmapFactory.decodeFile(MainActivity.IMAGE_PATH), 5000);



/**
	 * 获取圆角位图的方法
	 * 
	 * @param bitmap
	 *            需要转化成圆角的位图
	 * @param pixels
	 *            圆角的度数，数值越大，圆角越大
	 * @return 处理后的圆角位图
	 */
	public static Bitmap toRound(Bitmap bitmap, int pixels) {
		Bitmap output = Bitmap.createBitmap(bitmap.getWidth(),
				bitmap.getHeight(), Config.ARGB_8888);
		Canvas canvas = new Canvas(output);
		final int color = 0xff424242;
		final Paint paint = new Paint();
		final Rect rect = new Rect(0, 0, bitmap.getWidth(), bitmap.getHeight());
		final RectF rectF = new RectF(rect);
		final float roundPx = pixels;
		paint.setAntiAlias(true);
		canvas.drawARGB(0, 0, 0, 0);
		paint.setColor(color);
		canvas.drawRoundRect(rectF, roundPx, roundPx, paint);
		paint.setXfermode(new PorterDuffXfermode(Mode.SRC_IN));
		canvas.drawBitmap(bitmap, rect, rect, paint);
		return output;
	}
```
> ## 2. 从图库或拍照获取图片

```
protected void showChooseIconDialog() {
		AlertDialog.Builder builer = new Builder(YiShiChatActivity.this);
		builer.setTitle("提示");
		builer.setMessage("选择上传图片");
		builer.setPositiveButton("拍照",
				new android.content.DialogInterface.OnClickListener() {
					@SuppressLint("WorldWriteableFiles")
					public void onClick(DialogInterface dialog, int which) {
						// Intent intent = new
						// Intent(MediaStore.ACTION_IMAGE_CAPTURE);
						// startActivityForResult(intent,ACTION_CAMERA);

						Uri imageUri = null;
						String fileName = null;
						Intent openCameraIntent = new Intent(
								MediaStore.ACTION_IMAGE_CAPTURE);
						// 删除上一次截图的临时文件
						@SuppressWarnings("deprecation")
						SharedPreferences sharedPreferences = YiShiChatActivity.this
								.getSharedPreferences("temp",
										Context.MODE_WORLD_WRITEABLE);
						ImageTools.deletePhotoAtPathAndName(Environment
								.getExternalStorageDirectory()
								.getAbsolutePath(), sharedPreferences
								.getString("tempName", ""));

						// 保存本次截图临时文件名字
						fileName = String.valueOf(System.currentTimeMillis())
								+ ".jpg";
						Editor editor = sharedPreferences.edit();
						editor.putString("tempName", fileName);
						editor.commit();

						imageUri = Uri.fromFile(new File(Environment
								.getExternalStorageDirectory(), fileName));
						// 指定照片保存路径（SD卡），image.jpg为一个临时文件，每次拍照后这个图片都会被替换
						openCameraIntent.putExtra(MediaStore.EXTRA_OUTPUT,
								imageUri);
						startActivityForResult(openCameraIntent, ACTION_CROP);
					}
				});
		builer.setNegativeButton("图片库",
				new android.content.DialogInterface.OnClickListener() {
					public void onClick(DialogInterface dialog, int which) {
//						Intent openAlbumIntent = new Intent(
//								Intent.ACTION_GET_CONTENT);
//						openAlbumIntent.setDataAndType(
//								MediaStore.Images.Media.EXTERNAL_CONTENT_URI,
//								"image/*");
//						startActivityForResult(openAlbumIntent, ACTION_CROP);
						Intent intent = new Intent(Intent.ACTION_PICK, null);
						intent.setDataAndType(MediaStore.Images.Media.EXTERNAL_CONTENT_URI, "image/*");
						startActivityForResult(intent, ACTION_CROP);
					}
				});
		AlertDialog dialog = builer.create();
		dialog.show();
	}

	@SuppressLint("WorldWriteableFiles")
	@Override
	public void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		if (resultCode == RESULT_OK) {
			switch (requestCode) {
			case ACTION_CROP://这个是图库
				Uri uri = null;
				if (data != null) {
					uri = data.getData();
				} else {
					@SuppressWarnings("deprecation")
					String fileName = YiShiChatActivity.this
							.getSharedPreferences("temp",
									Context.MODE_WORLD_WRITEABLE).getString(
									"tempName", "");
					uri = Uri.fromFile(new File(Environment
							.getExternalStorageDirectory(), fileName));
				}
				cropImage(uri, 200, 200, CROP_PICTURE);
				break;
			case CROP_PICTURE:
				Bitmap photo = null;
				Uri photoUri = data.getData();
				if (photoUri != null) {
					photo = BitmapFactory.decodeFile(photoUri.getPath());
				}
				if (photo == null) {
					Bundle extra = data.getExtras();
					if (extra != null) {
						photo = (Bitmap) extra.get("data");
						ByteArrayOutputStream stream = new ByteArrayOutputStream();
						photo.compress(Bitmap.CompressFormat.JPEG, 100, stream);
					}
				}
				// if(photo.getWidth()<100 || photo.getHeight()<100){
				// photo = ImageUtilBase.resizeImage(photo, 200, 200);
				// }
				// headIcon.setImageBitmap(ImageUtilBase.toRound(photo,5000));
				// 保存到sd卡
				File excelFiles = new File(FOLDER_PATH);
				if (!excelFiles.exists()) {
					excelFiles.mkdirs();
				}
				File excelFile = new File(IMAGE_PATH);
				if (excelFile.exists()) {
					excelFile.mkdir();
				}
				ImageUtilBase.SaveImage(photo, IMAGE_PATH);

				File file = new File(IMAGE_PATH);
				if (file != null) {
					new Thread() {
						@SuppressWarnings("rawtypes")
						public void run() {
							Map resultMap = (Map) FileUploadUtil.upload("FN06070WD00U!uploadConsultationImage.action",
											IMAGE_PATH);
							String result = (String) resultMap.get("head");
							Message msg = new Message();
							if (result.equals("success")) {
								msg.what = UPLOAD_SUCCESS;
								Bundle b=new Bundle();
								b.putString("url", (String) resultMap.get("url"));
								b.putString("IMAGE_WIDTH", String.valueOf(Double.valueOf(resultMap.get("IMAGE_WIDTH").toString()).intValue()));
								b.putString("IMAGE_HEIGHT",String.valueOf(Double.valueOf(resultMap.get("IMAGE_HEIGHT").toString()).intValue()));
								msg.setData(b);
							} else if (result.equals("fail")) {
								msg.what = UPLOAD_FAIL;
								msg.obj = (String) resultMap.get("body");
							}
							handler.sendMessage(msg);
						}
					}.start();
				}
				break;
			default:
				break;
			}
		}

	}
```
> ## 3. //删除指定文件夹下指定名字的文件

```
//删除指定文件夹下指定名字的文件
	public static void deletePhotoAtPathAndName(String path,String fileName){
		//如果内存卡存在的化
		if (checkSDCardAvailable()) {
			File folder = new File(path);
			File[] files = folder.listFiles();
			for (int i = 0; i < files.length; i++) {
				System.out.println(files[i].getName());
				if (files[i].getName().equals(fileName)) {
					files[i].delete();
				}
			}
		}
	}


/**
	 * Check the SD card 检查SDcard是否存在
	 * @return
	 */
	public static boolean checkSDCardAvailable(){
		return android.os.Environment.getExternalStorageState().equals(android.os.Environment.MEDIA_MOUNTED);
	}
```
> ## 4. 图片剪切

```
private void cropImage(Uri uri, int outputX, int outputY, int requestCode) {
		Intent intent = new Intent("com.android.camera.action.CROP");
		intent.setDataAndType(uri, "image/*");
		intent.putExtra("crop", "true");
		intent.putExtra("aspectX", 1);
		intent.putExtra("aspectY", 1);
		intent.putExtra("outputX", outputX);
		intent.putExtra("outputY", outputY);
		intent.putExtra("outputFormat", "JPEG");
		intent.putExtra("noFaceDetection", true);
		intent.putExtra("return-data", true);
		startActivityForResult(intent, requestCode);
	}
```
> ## 5. //把图片保存到内存卡上

```
//把图片保存到内存卡上
	public static void SaveImage(Bitmap bitmap, String fileName) {
		FileOutputStream fout = null;
		try {
			fout = new FileOutputStream(fileName);
			bitmap.compress(Bitmap.CompressFormat.PNG, 100, fout);
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} finally {
			try {
				if (fout != null) {
					fout.flush();
					fout.close();
				}
			} catch (IOException e) {
				e.printStackTrace();
			}
		}

	}
```
<h1 id="37">37. 心衰百科 MainZiXunActivity</h1>  

## [返回目录](#0)

> ## 1. 初始化控件的监听

```
private void initData() {
		zixunViewPager = (ViewPager) findViewById(R.id.zixunViewPager);
		
		ArrayList<View> views = new ArrayList<View>();
		views.add(new ZiXunInfoView(this));
		views.add(new ZiXunExpertView(this));
		views.add(new ZiXunSportView(this));
		
		//views.add(new YongYaoInfoView(this));
		zixunViewPager.setAdapter(new ViewPagerAdapter(views));
		zixunViewPager.setOnPageChangeListener(new MyPageChangeListener());

		zixunMenuBarView = (MenuBarView) findViewById(R.id.zixunMenuBar);
		zixunMenuBarView.setOnMenuBarListener(this);
		zixunMenuBarView.setSelectedIndex(0);
	}
```
> ## 2. viewPager监听

```
// viewPager监听
	class MyPageChangeListener implements OnPageChangeListener {

		@Override
		public void onPageScrollStateChanged(int arg0) {

		}

		@Override
		public void onPageScrolled(int arg0, float arg1, int arg2) {

		}

		@Override
		public void onPageSelected(int arg0) {
			if (arg0 == 0) {

			}
			zixunMenuBarView.setSelectedIndex(arg0);
		}
	}
```

<h1 id="39">39. 日期的运用</h1>  

## [返回目录](#0)

> ## 1. 设置时间不能晚于当前时间

```
calendarDate = format.format(downDate);
				//通过string yyyy-mm-dd 时间获取时间码
				long calendarTime = DateUtil.getLongOfDayTime(calendarDate);
				//设置时间不能晚于当前时间
				if(calendarTime > DateUtil.getNowTimeInMillis()){
					ShowUtil.showToast(SetLifeDataActivity.this, R.string.time_early);
					calendar.setCalendarData(thisDownDate);
					return;
				}


// 通过string yyyy-mm-dd 时间获取时间码
	public static long getLongOfDayTime(String time) {
		int year = Integer.valueOf(time.substring(0, 4));
		int month = Integer.valueOf(time.substring(5, 7));
		int day = Integer.valueOf(time.substring(8, 10));
		Calendar calendar = Calendar.getInstance();
		calendar.set(calendar.YEAR, year);
		calendar.set(calendar.MONTH, month - 1);
		calendar.set(calendar.DAY_OF_MONTH, day);
		
		return calendar.getTimeInMillis();
	}

//返回现在的时间的时间码   格式为Long型
	public static long getNowTimeInMillis() {
		Calendar nowCalendar = Calendar.getInstance();
		nowCalendar.getTimeInMillis();
		
		return System.currentTimeMillis();
	}
```




<h1 id="39">39. 日期的运用</h1>  

## [返回目录](#0)

> ## 1. 

```
```
> ## 2. 

```
```
> ## 3. 

```
```
> ## 4. 

```
```
> ## 5. 

```
```