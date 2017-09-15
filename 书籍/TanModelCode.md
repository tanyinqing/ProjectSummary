 # 2017 08 17
>  [文档地址](http://pan.baidu.com/disk/home?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&#list/vmode=list&path=%2F%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6%E5%A4%B9%2F%E5%AE%89%E5%8D%93%E9%A1%B9%E7%9B%AE%E4%BB%A3%E7%A0%81%E4%BB%93%E5%BA%93%2FMarkDown%E5%BC%80%E5%8F%91%E6%96%87%E6%A1%A3 "查看")→[源文件相关](http://pan.baidu.com/disk/home?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&#list/vmode=list&path=%2F%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6%E5%A4%B9%2F%E9%A1%B9%E7%9B%AE%E6%A8%A1%E5%9D%97%2FAndBaseDemo%E6%A1%86%E6%9E%B6 "查看")→[首页](https://tanyinqing.github.io/)
 
<h1 id="01">目录列表</h1>  

* utils文件夹→[1. 控制台日志的打印模板](#0801)→[2. 把日志打印到内存卡上](#0802)→[3. 把连续的日志打印到内存卡的一个文件上](#0803)→[4. 像素和dp和sp单位的换算](#0804)→[5. 对象和Json字符串的相互转化](#0805)→[6. 日期APi的工具类](#0806) →[7. 缓存数据的工具类](#0807)→[8. 按钮加入3次点击的监听](#0808) 

* 常用技巧→[1. 最常用的调用方法代码](#001)→ [2. 浏览器常用的快捷键](#002)→[3. 结构命名规则](#003)→ [4. github设置](#004)→[常量](#0501)→[配置模块build.gradle(Module:app)](#0502)        

* activity文件夹→[1. activity父类](#040101)→ [2. activity标题类](#040102)→[3. activity带适配器的模板类](#040103)→[4. activity不带适配器的模板类](#040104)→[5. activity之间跳转](#040105)

* model文件夹→[1. model父类](#040201)

* adapter文件夹→[1. adapter父类](#040301)

* 数据存储文件夹→[1. db文件夹负责建立数据库](#011)→[2. databass文件夹负责写入数据](#012)→[3. databass文件夹中的特定方法](#013)→[5. SQL语句](#015)→[4. 缓存数据存储](#014)

<h1 id="02">目录列表2</h1>  

* 网络→[DataListener回调类](#0211)→[写一个接口的清单](#0221)→[定义父类](#0231)→[定义子类](#0232)→[调用网络  其他处调用 返回字符串](#0241)
 
* 多媒体→[访问网络  返回图片](#0301)

* 资源→[colors.xml](#0601)→[dimens.xml](#0602) →[styles.xml](#0603)→[drawable下的xml资源](#0604) →[5. layout文件夹下的xml资源](#0605)→[6. 动画](#0606)→[7. arrays.xml](#0607)

* 自定义控件→[1. 常用控件](#0701)→[2. 常用布局](#0702)

* 分布式管理→[1. 代码托管](#0901)→[2. 项目网址](#0902)

参考文档
[百度项目地址](http://pan.baidu.com/disk/home?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&#list/vmode=list&path=%2F%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6%E5%A4%B9%2F%E9%A1%B9%E7%9B%AE%E6%A8%A1%E5%9D%97 "查看")→[云端地址](https://github.com/tanyinqing/MarkDown/tree/master/app/src/main/java/codewarehouse/yzkj/com/markdown "查看")→[医疗框架结构图](https://github.com/tanyinqing/MarkDown/blob/master/app/src/main/java/codewarehouse/yzkj/com/markdown/%E5%8C%BB%E7%96%97%E6%A1%86%E6%9E%B6%E7%BB%93%E6%9E%84%E5%9B%BE.md "查看")→[Aar地址git](https://github.com/tanyinqing/TanYinQingAar)



 <h1 id="001">1. 最常用的调用方法代码</h1>
 
 [返回目录](#01) 

//控制台打印日志
``` 
 MyLog.ShowLog(json);  
``` 
//土司
``` 
PublicUtil.ShowToast("3次点击设置成功");
```
//把注释做到内存卡中
```
 LogTxt.writeLog(json, "网络下载返回的数据"); 
```

// 缓存数据
```
 mPrefUtil.putSetting("isLog", true);
```
注解绑定
```

 	@ViewInject(R.id.editPhone)
    private EditText editPhone; 

	 @OnClick(R.id.buttonLogin)
    public void login(View view)
    {       
    }

```
//这个是打印接口和参数日志
``` 
      StringBuilder mStringBuilder=new StringBuilder(LoginUrl);
        mStringBuilder.append("?phoneNum=");
        mStringBuilder.append(phoneNum);
        mStringBuilder.append("&password=");
        mStringBuilder.append(password);
        LogTxt.writeLog(mStringBuilder.toString(), "登录接口");

LogTxt.writeLog(json, "登录接口返回的数据");

```
选择语句
```
if ("".equals()) {
            
        }else if ("".equals()) {

        }else {
            
        }
        
        
        switch (){
            case 1:
                break;
            case 2:
                break;
            default:
                break;
        }
```
利用imageLoder下载图片
```
//下载图片
 	private static ImageLoader imageLoader;
	imageLoader = PublicUtil.getImageLoader();
	String pic=address.getPhotoUrl();
   if(null != pic && !pic.equals("") && !pic.equals("null"))
   {       
       imageLoader.displayImage(Constant.URLBASE+pic, imageHead,PublicUtil.getGoodsOption());
   }

```
访问网络的方法
```
	 /**
     * 获取配送员账号的列表
     * http://211.149.169.221:8080/umijoyappsvr/distribution/DistributionUserList.do?start=0&limit=15
     */

    private static String AccountListUrl = BaseUrl +"/distribution/DistributionUserList.do";

    /**
     * 获取配送员账号的列表
     *
     * @param phoneNum
     * @param dataListener
     */
    public void getAccountList(String phoneNum,final DataListener<List<User>> dataListener)
    {
        RequestParams params = new RequestParams();
        params.addBodyParameter("start", "0");
        params.addBodyParameter("limit", "15");
        post(AccountListUrl, params, new IRequestListener() {
            public void onSuccess(String json) {
                Type type = new TypeToken<List<User>>(){}.getType();
                parse(json,type, dataListener);
            }
            @Override
            public void onFailed() {
                dataListener.onFailed();
            }
        });
    }
```  
<h1 id="002">2. 浏览器常用的快捷键</h1>
 
[返回目录](#01)

studio最常用快捷键

Ctrl + Alt + M  但在android Studio中有了一个快速提取的方法

ctrl+D  复制本行到下一行
ctrl+alt+F7  看本应用中有几个地方用到了这个变量或方法
ctrl+F12 看到一个Activity内，所有的方法清单
ctrl+Home 回到Activity的第一行的位置
ctrl+alt+左右键  上一次或下一次编辑过的位置    
Alt+6 弹出Message框
Alt+1 弹出project结构
红锁为私有变量 钥匙为受保护的 m为方法 l变量
Ctrl＋tab 界面切换窗口
ctrl+n 查找类中的方法和变量
Ctrl+H 显示类结构图
Ctrl＋Shift＋上下 代码行向上和向下移动
F2 高亮定位错误行
Alt+F3  高亮往下查找相同文本
1.Ctrl＋E，可以显示最近编辑的文件列表
2.Shift＋Click可以关闭文件
3.Ctrl＋[或]可以跳到大括号的开头结尾
4.Ctrl＋Shift＋Backspace可以跳转到上次编辑的地方
5.Ctrl＋F12，可以显示当前文件的结构
6.Ctrl＋F7可以查询当前元素在当前文件中的引用，然后按F3可以
7.Ctrl＋N，可以快速打开类
8.Ctrl＋Shift＋N，可以快速打开文件
9.Alt＋Q可以看到当前方法的声明
10.Ctrl＋W可以选择单词继而语句继而行继而函数
11.Alt＋F1可以将正在编辑的元素在各个面板中定位
12.Ctrl＋P，可以显示参数信息
13.Ctrl＋Shift＋Insert可以选择剪贴板内容并插入
14.Alt＋Insert可以生成构造器/Getter/Setter等
15.Ctrl＋Alt＋V 可以引入变量。例如把括号内的SQL赋成一个变量
16.Ctrl＋Alt＋T可以把代码包在一块内，例如try/catch
17.Alt＋Up and Alt＋Down可在方法间快速移动 


Exlipse 快捷键
    Alt+左右键  表明前进和后退
    ctrl+D  删除本行

    idea 软件工具的使用
    Idea > File > Settings... > Keymap
    Main menu > Code > Completion > Basic
    Add Keyboard Shortcut: Alt+斜杠   设置自动补全的快捷键

    Idea > File > Settings > Editor > General > Code Completion
    Case sensitive completion: None  提示不区分大小写

	我用的的索尼笔记本
shift+Num lk键的作用是开启和关闭键盘中的数字键

VCS 版本控制
Import into Version Control 提交版本控制
Checkout from Version Control 从版本控制中切出来
font 前端字体修改 
Keymap 快捷键 
Fork 从别人的github中切过来

<h1 id="003">3. 结构命名规则</h1>
 
[返回目录](#01)

``` 
登录LoginAcitvity activity_login editPhone buttonLogin textForget
账号管理  AccountManagementAcitvity imageHead
添加账号 AddAccountAcitvity

```
> <h1 id="004">4. github设置</h1>
 
[返回目录](#01)

``` 
C:\Users\Administrator
.gitconfig  文件

idea或studio的配置
[user]
 name = tan***qingcuiyansheng
 email = 243548***@qq.com
或
[user]
  name = tan***qing
  email = 289367***@qq.com

eclipse的gitconfig配置

[core]
 repositoryformatversion = 0
 filemode = false
 bare = false
 logallrefupdates = true
 symlinks = false
 ignorecase = true
 hideDotFiles = dotGitOnly
[remote "origin"]
 url = "" 

fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
 remote = origin
 merge = refs/heads/master
[user]
 name = tan***qing
 email = 289367***@qq.com


环境变量的配置
JAVA_HOME
C:\Program Files\Java\jdk1.8.0_40

Path
%JAVA_HOME%\bin;     C:\ProgramData\Oracle\Java\javapath;%SystemRoot%\system32;%SystemRoot%;%SystemRoot%\System32\Wbem;%SYSTEMROOT%\System32\WindowsPowerShell\v1.0\;C:\Program Files\TortoiseSVN\bin

CLASSPATH
.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;
``` 
 [Eclipse配置Git全过程-----------附用EGit不能push的问题解决](http://blog.csdn.net/yanzi1225627/article/details/12885317/)

<h1 id="011">011. db文件夹负责建立数据库</h1>

[返回目录](#01)

```
package codewarehouse.yzkj.com.ceshi;

import android.content.Context;
import android.content.res.AssetManager;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteOpenHelper;
import android.util.Log;

import java.io.File;
import java.io.FileOutputStream;
import java.io.InputStream;

/**
 * 建立数据库和数据表
 */
public class DBHelper extends SQLiteOpenHelper {
    public static final int DATABASE_VERSION = 1;
    //这个是建立的数据库的库名
    public static final String DATABASE_NAME = "shujuku.db";   //数据库名称
    //拷贝数据库时用到的路径名
    private static final String DATABASE_PATH = "/data/data/com.gas.Securitycheck/databases/";
    /*
    *  main表建表语句
    */
    public static final String CREATE_PROVINCE = "create table main ("
            + "id integer NOT NULL primary key autoincrement,"//注释
            + "[depantment] VARCHAR(50), "
           // + "[alarmId] INTEGER NOT NULL, "
            //+ "[alarmTime] LONG, "
          //  + "[setTime] LONG, "
            + "[time] VARCHAR(100), "
            + "[data] VARCHAR(100), "
            + "[name] VARCHAR(100), "
            //+ "[yaoId] INTEGER, "
            + "[remarksDetail] text, "
            + "[isUpLoad] text, "
            + "[photoRoute] text, "  //这个是图片的保存
            + "[rejectReason] VARCHAR(100))";
     /*
    *    photo表建表语句
    */
    public static final String CREATE_PHOTO = "create table photo ("
            + "id integer NOT NULL primary key autoincrement,"//注释
            + "[photo] VARCHAR(100), "   //这个是图片的路径
            + "[rmd5] VARCHAR(100), "    //这个是图片的MD5值
            + "[time] VARCHAR(100))";

    /*
     * CoolWeatherOpenHelper的4参数构造方法
	 * 第一个参数:Context
	 * 第二个参数:数据库名
	 * 第三个参数:Cursor,通常传人null
	 * 第四个参数:数据库版本Version
	 */
    public DBHelper(Context context, String name, SQLiteDatabase.CursorFactory factory, int version) {
        super(context, name, factory, version);
    }

    @Override
    public void onCreate(SQLiteDatabase sqLiteDatabase) {
        //执行建立数据表的语句
        sqLiteDatabase.execSQL(CREATE_PROVINCE);
        sqLiteDatabase.execSQL(CREATE_PHOTO);
    }

    @Override //重写数据库升级的方法
    public void onUpgrade(SQLiteDatabase sqLiteDatabase, int oldVersion, int newVersion) {
        if (newVersion > oldVersion) {
            for (int i = (oldVersion + 1); i <= newVersion; i++) {
                upGrade(sqLiteDatabase, i);//升级程序时，修改了数据库，需要在以下用sql语句去修改
            }
        }

    }

    @Override
    protected void finalize() throws Throwable {
        if (this != null) {
            this.close();
        }
        super.finalize();
    }

    /*
	 * 升级程序时，修改了数据库，需要在以下用sql语句去修改
	 */
    private void upGrade(SQLiteDatabase db, int version) {
        switch (version) {
            case 1:
                break;
            case 2:
                db.beginTransaction();
//添加字段  必须开启事务
                //db.execSQL("alter table BaseUrl add column tanyinqing INTEGER default 0");
                //添加字段
//			db.execSQL("alter table yao add column yaoTest INTEGER default 0");
                //添加表
//			db.execSQL("create table MyBaodianFavorite ([Id] INTEGER DEFAULT '0' PRIMARY KEY AUTOINCREMENT,[NewsId] INTEGER NOT NULL,[AppType] VARCHAR(50) NOT NULL,[ImageUrl] VARCHAR(50),[Introduction] TEXT NOT NULL,[Title] VARCHAR(50) NOT NULL,[Author] VARCHAR(50) NOT NULL,[PubDate] VARCHAR(50) NOT NULL)");
                //db.execSQL("create table image ([content] VARCHAR(100),[image] VARCHAR(100),[newId] VARCHAR(100))");
                //db.setVersion(version);//设置版本号
                db.setTransactionSuccessful();//事务成功  否则可以回滚事务的
                db.endTransaction();  //事务结束
                break;
            case 3:
                break;
            case 4:
                break;
            default:
                break;
        }
    }

    // 复制数据库到sd卡中
    public static void copyDB(Context context) {
        // DBHelper.context = context;
        // 没有file先创建文件夹
        File dbFile = new File(DATABASE_PATH);
        if (!dbFile.exists()) {
            dbFile.mkdirs();
        } else {
            File dbContentFile = new File(DATABASE_PATH, DATABASE_NAME);
            if (dbContentFile.exists()) {
                return;
            }
        }

        InputStream is = null;
        FileOutputStream fos = null;
        try {
            AssetManager am = context.getAssets();  //管理器
            // 得到.db file
            File saveFile = new File(DATABASE_PATH, DATABASE_NAME);
            // 获取数据库本地资源
            is = am.open("securityCheckOne.db");
            // 获取数据库输入流
            fos = new FileOutputStream(saveFile);
            byte[] buffer = new byte[8192];
            int count = 0;
            while ((count = is.read(buffer)) > 0) {
                fos.write(buffer, 0, count);
            }

        } catch (Exception e) {
            Log.i("Exception", Log.getStackTraceString(e));
        } finally {
            try {
                if (fos != null)
                    fos.close();
                if (is != null)
                    is.close();
            } catch (Exception e) {
                Log.i("Exception", Log.getStackTraceString(e));
            }
        }
    }
}


```

<h1 id="012">012. databass文件夹负责写入数据</h1>

[返回目录](#01)

```
package codewarehouse.yzkj.com.ceshi;

import android.content.ContentValues;
import android.content.Context;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;


import java.util.ArrayList;

/**
 * Created by Administrator on 2017/4/18 0018.
 */
public class MainDB {
    private Context context;
    private DBHelper dbHelper;

    public MainDB(Context context) {
        this.context = context;
        dbHelper = new DBHelper(context,DBHelper.DATABASE_NAME,null,DBHelper.DATABASE_VERSION);
    }
//插入数据表中的数据
    public void insertAlarm(RenWu renWu) {
       SQLiteDatabase db=dbHelper.getWritableDatabase();
       /* db.execSQL("insert into main_1 (depantment,time,data,name,remarksDetail,isUpLoad,rejectReason，photoRoute) values (?,?,?,?,?,?,?,?);",
                new Object[]{renWu.getDepantment(),renWu.getTime(),renWu.getData(),renWu.getName(),renWu.getRemarksDetail(),renWu.getIsUpLoad(),renWu.getRejectReason(),renWu.getPhotoRoutePath()});*/
        ContentValues values = new ContentValues();
        values.put("depantment", renWu.getDepantment());
        values.put("time", renWu.getTime());
        values.put("data", renWu.getData());
        values.put("name", renWu.getName());
        values.put("remarksDetail", renWu.getRemarksDetail());
        values.put("isUpLoad", renWu.getIsUpLoad());
        values.put("rejectReason", renWu.getRejectReason());
        values.put("photoRoute", renWu.getPhotoRoutePath());
        db.insert("main", null, values);
        db.close();// 记得关闭数据库操作
    }
//修改数据表 返回的int值表明 修改的行数 大于0表明修改成功
    public int upData(RenWu renWu) {
        SQLiteDatabase db = dbHelper.getWritableDatabase();
        ContentValues values = new ContentValues();
        values.put("depantment", renWu.getDepantment());
        values.put("time", renWu.getTime());
        values.put("name", renWu.getName());
        values.put("remarksDetail", renWu.getRemarksDetail());
        int result=db.update("main",values,"id=?",new String[]{String.valueOf(renWu.getId())});
        db.close();
        return result;
    }
//清空数据表
    public void delete() {
        SQLiteDatabase db=dbHelper.getWritableDatabase();
        db.execSQL("delete from main;");
        db.close();
    }

    //获取全部的数据
    public ArrayList<RenWu> getAlarmListByTime() {
        SQLiteDatabase db=dbHelper.getWritableDatabase();
        ArrayList<RenWu> arr=new ArrayList<>();
        Cursor cursor=db.query("main", new String[]{"*"}, null, null, null, null, null);
        cursorMethed(cursor, arr);
        cursor.close();
        db.close();
        return arr;
    }
    //通过id来获取数据
    public RenWu getElementListByid(String id) {
        SQLiteDatabase db=dbHelper.getWritableDatabase();
        RenWu alarm=new RenWu();
        Cursor cursor=db.query("main",new String[]{"*"},"id=?",new String[]{id},null,null,null);
        while (cursor.moveToNext()){
            alarm.setId(cursor.getLong(cursor.getColumnIndex("id")));
            alarm.setDepantment(cursor.getString(cursor.getColumnIndex("depantment")));
            alarm.setTime(cursor.getString(cursor.getColumnIndex("time")));
            alarm.setData(cursor.getString(cursor.getColumnIndex("data")));

            alarm.setRejectReason(cursor.getString(cursor.getColumnIndex("rejectReason")));
            alarm.setIsUpLoad(cursor.getString(cursor.getColumnIndex("isUpLoad")));
            alarm.setName(cursor.getString(cursor.getColumnIndex("name")));
            alarm.setRemarksDetail(cursor.getString(cursor.getColumnIndex("remarksDetail")));
            alarm.setPhotoRoutePath(cursor.getString(cursor.getColumnIndex("photoRoute")));
        }
        cursor.close();
        db.close();
        return alarm;
    }

//数据组装
    private void cursorMethed(Cursor cursor, ArrayList<RenWu> arr) {
        while (cursor.moveToNext()){
            RenWu alarm=new RenWu();
            alarm.setId(cursor.getLong(cursor.getColumnIndex("id")));
            alarm.setDepantment(cursor.getString(cursor.getColumnIndex("depantment")));
            alarm.setTime(cursor.getString(cursor.getColumnIndex("time")));
            alarm.setData(cursor.getString(cursor.getColumnIndex("data")));

            alarm.setRejectReason(cursor.getString(cursor.getColumnIndex("rejectReason")));
            alarm.setIsUpLoad(cursor.getString(cursor.getColumnIndex("isUpLoad")));
            alarm.setName(cursor.getString(cursor.getColumnIndex("name")));
            alarm.setRemarksDetail(cursor.getString(cursor.getColumnIndex("remarksDetail")));
            alarm.setPhotoRoutePath(cursor.getString(cursor.getColumnIndex("photoRoute")));

            arr.add(alarm);
        }
    }
}

```

<h1 id="013">013. databass文件夹中的特定方法</h1>

[返回目录](#01)

```
//获得新插入的数据的id
public String getid() {
        SQLiteDatabase db = dbHelper.getWritableDatabase();
        Cursor cursor=db.query("photo",new String[]{"*"},null,null,null,null,null);
        cursor.moveToLast();
        int id=cursor.getInt(cursor.getColumnIndex("id"));
        cursor.close();
        db.close();
        return String.valueOf(id);
    }


//删除某种定时
	public void delete(int yaoId) {
		SQLiteDatabase db = helper.getWritableDatabase();
		db.delete("alarm", "yaoId=?",new String[] {String.valueOf(yaoId)});
		db.close();
	}


/*Cursor cursor = db.query(
		 * "celingData",   数据的表名
		 *  new String[] { "id", "uid","sync", "date",
				"dateMonth", "day", "time", "type","result", "state", "diag" },   要查询出来的列明
				 "uid=?",   查询的条件子句
				 new String[] {uid},   为子句中的占位符提供参数值
				 null,   用于控制分组
				 null,    用于对分组进行过滤
				 "date desc,time desc"  用于对记录进行排序
				 );*/


/**
	 * 获取是否有未同步的数据
	 */
	public boolean haveNoSync(String uid) {
		boolean isHave = false;
		SQLiteDatabase db = helper.getWritableDatabase();
		Cursor cursor = db.query("celingData", new String[] { "id", "uid","sync", "date",
				"dateMonth", "day", "time", "type","result", "state", "diag" }, "sync=? and uid=?", new String[] { String.valueOf(ConstantUtil.SYNC_NO), uid}, null, null,null);
		if(cursor.moveToFirst() == false){
			isHave = false;
		}else{
			isHave = true;
		}
		cursor.close();
		db.close();
		return isHave;
	}


/*判断是否有点赞的条目*/
	public boolean isHave(String goodId) {
		boolean isHave = false;
		SQLiteDatabase db = helper.getWritableDatabase();
		Cursor cursor = db.query("good", new String[] { "id", "goodId"}, "goodId=?", 
				new String[] {goodId}, null, null, null);
		if(cursor.moveToFirst() == false){
			isHave = false;
		}else{
			isHave = true;
		}
		cursor.close();
		db.close();
		return isHave;
	}


//把一个链表的数据插入数据库
	public void insertList(ArrayList<HelpHeart> list) {
		SQLiteDatabase db = helper.getWritableDatabase();
		for(int i = 0; i< list.size() ; i++){
			ContentValues values = new ContentValues();
			HelpHeart helpHeart = list.get(i);
			values.put("uid", helpHeart.uid);
			values.put("sync", helpHeart.sync);
			values.put("date", helpHeart.date);
			values.put("dateMonth", helpHeart.dateMonth);
			values.put("day", helpHeart.day);
			values.put("time", helpHeart.time);
			values.put("timeMill", helpHeart.timeMill);
			values.put("heart", helpHeart.heart);
			db.insert("heart", null, values);
		}
		db.close();
	}


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
				//helpHeartArray 这个是全局变量  每增加一个数据，就添加一个值
				helpHeartArray.add(helpHeart);
			}
			cursor.close();
		}
		
		
		db.close();
		return helpHeartArray;
	}


//查询  区间内  时间段  的数据
	public ArrayList<HelpHeart> getHeartListByTime(String uid, long startTime, long endTime){
		SQLiteDatabase db = helper.getWritableDatabase();
		ArrayList<HelpHeart> helpHeartArray = new ArrayList<HelpHeart>();
		Cursor cursor = db.query("heart", new String[] { "id", "uid", "sync","date",
				"dateMonth", "day", "time", "timeMill", "heart"}, 
				"uid=? and timeMill>? and timeMill<?", new String[] {uid, String.valueOf(startTime), 
				String.valueOf(endTime)}, null, null, "date asc");
		cursorMethod(helpHeartArray, cursor);
		cursor.close();
		db.close();
		return helpHeartArray;
	}


//查询对象的列表
	public ArrayList<ZiXun> getImageList() {
		SQLiteDatabase db = helper.getWritableDatabase();
		ArrayList<ZiXun> alarmArray = new ArrayList<ZiXun>();
		Cursor cursor = db.query("image", new String[] { "content", "image","newId"}, null, null, null, null, null);
		while (cursor.moveToNext()) {
			ZiXun ziXun = new ZiXun();
			ziXun.content = cursor.getString(cursor.getColumnIndex("content"));
			ziXun.image = cursor.getString(cursor.getColumnIndex("image"));
			ziXun.newId = cursor.getString(cursor.getColumnIndex("newId"));
			alarmArray.add(ziXun);
		}
		cursor.close();
		db.close();
		return alarmArray;
	}


/**
	 * 查询数据   只查要的类型  并且类型不能重复  set的数据不重复 类似分组
	 HashSet类，是存在于java.util包中的类。同时也被称为集合，该容器中只能存储不重复的对象
	 */
	public ArrayList<String> getTypeList() {
		SQLiteDatabase db = helper.getWritableDatabase();
		ArrayList<Yao> yaoArray = new ArrayList<Yao>();
		Cursor cursor = db.query("yao", new String[] { "id", "uid","yaoId","name", "type",
				"typeName", "firm", "content", "contentText"}, null, null, null, null, null);
		cursorMethod(yaoArray, cursor);
		cursor.close();
		db.close();
		Set<String> hashSet = new HashSet<String>(); 
		ArrayList<String> arrayList;
		for(int i=0; i<yaoArray.size(); i++){
			hashSet.add(yaoArray.get(i).typeName);
		}
		arrayList = new ArrayList<String>(hashSet);
		return arrayList;
	}

//最后一个添加的数据的id
	public int getLastId(){
		SQLiteDatabase db = helper.getWritableDatabase();
		Cursor cursor = db.query("yongyaoRemind", new String[] { "id", "uid","time", "timeShow",
				"name", "usage", "sideEffect"}, null, null, null, null, null);
		cursor.moveToLast();
		int lastId = cursor.getInt(cursor.getColumnIndex("id"));
		cursor.close();
		db.close();
		return lastId;
	
	}
```
<h1 id="015">015. SQL语句</h1>

[返回目录](#01)

```
唐山的数据库
选中SQ语句 点执行这个按钮

从数据库找这户的信息，我要找它的itnumber，下面这些信息对应哪些字段
任务编号  P20170630061-D20170630001000-62656
任务地址  乙区供电003-3-101
执行人    张振基(00127)

这个语句查询IT_NumberTime
select * from InformationTable where 
IT_Number='P20170630061-D20170630001000-62656'

表 
InformationTable  字段包括
DispatchTable

select * from InformationTable where DT_Id=20 and IT_AuditStatus=1 order by 
IT_ADId  and  IT_ADID  in() group by IT_ADId  

select * from PlannedUser where PU_PDId=1029 and PU_Type=1
```
<h1 id="014">014. 缓存数据存储</h1>

[返回目录](#01)

```
可以在父类中初始化  在子类中调用
 public static PreferenceUtil mPrefUtil;  //用于配制信息的业务类  继成了各种方法

 mPrefUtil = new PreferenceUtil(this, Constant.prefName, Context.MODE_PRIVATE);
        Date mDate=new Date();
        mPrefUtil.putSetting("tan",mDate);


package codewarehouse.yzkj.com.ceshi;

import android.content.Context;
import android.content.SharedPreferences;
import android.content.SharedPreferences.Editor;
import android.text.TextUtils;

import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.io.StreamCorruptedException;
import java.util.HashMap;
import java.util.Iterator;

/**
 * 
 * 配置存储工具类
 * 
 * @author zeroangus
 * 
 */
public class PreferenceUtil {

	private SharedPreferences preferences;

	public PreferenceUtil(Context context, String name, int Mode) {
		preferences = context.getSharedPreferences(name, Mode);
	}

	/**
	 * 保存对象  将对象序列化后再转化为16进制的字符串保存
	 * @param key
	 * @param value
	 */
	public void putSetting(String key, Object value) {
		Editor editor = preferences.edit();
		try {
			ByteArrayOutputStream baos = new ByteArrayOutputStream();
			ObjectOutputStream oos = new ObjectOutputStream(baos);
			oos.writeObject(value);
			// 将序列化的数据转为16进制保存
			String value2 = bytesToHexString(baos.toByteArray());
			editor.putString(key, value2);
			editor.commit();
		} catch (Exception e) {
			System.out.println("putSetting ----> "+e.toString());
		}
	}

	/**
	 * desc:将数组转为16进制  将数组转化为字符串
	 * 
	 * @param bArray
	 * @return modified:
	 */
	public static String bytesToHexString(byte[] bArray) {
		if (bArray == null) {
			return null;
		}
		if (bArray.length == 0) {
			return "";
		}
		StringBuffer sb = new StringBuffer(bArray.length);
		String sTemp;
		for (int i = 0; i < bArray.length; i++) {
			sTemp = Integer.toHexString(0xFF & bArray[i]);
			if (sTemp.length() < 2)
				sb.append(0);
			sb.append(sTemp.toUpperCase());
		}
		return sb.toString();
	}

	/**
	 * desc:获取保存的Object对象
	 * 
	 * @param key
	 * @return modified:
	 */
	public Object readObject(String key) {
		try {
			if (preferences.contains(key)) {
				System.out.println("配置信息preferences.contains -------------> " + key);
				String string = preferences.getString(key, "");
				if (TextUtils.isEmpty(string)) {

					System.out.println( key + "配置信息 -----> is empty"  );
					return null;
				} else {

					System.out.println( key + " 配置信息-----> is not empty"  );
					// 将16进制的数据转为数组，准备反序列化
					byte[] stringToBytes = StringToBytes(string);
					ByteArrayInputStream bis = new ByteArrayInputStream(
							stringToBytes);
					ObjectInputStream is = new ObjectInputStream(bis);
					// 返回反序列化得到的对象
					Object readObject = is.readObject();
					return readObject;
				}
			}
		} catch (StreamCorruptedException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (ClassNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		// 所有异常返回null
		return null;

	}

	/**
	 * desc:将16进制的数据转为数组  也就是把字符串转化为数组 一个单词一个组
	 * <p>
	 * 创建人：聂旭阳 , 2014-5-25 上午11:08:33
	 * </p>
	 * 
	 * @param data
	 * @return modified:
	 */
	public static byte[] StringToBytes(String data) {
		String hexString = data.toUpperCase().trim();
		if (hexString.length() % 2 != 0) {
			return null;
		}
		byte[] retData = new byte[hexString.length() / 2];
		for (int i = 0; i < hexString.length(); i++) {
			int int_ch; // 两位16进制数转化后的10进制数
			char hex_char1 = hexString.charAt(i); // //两位16进制数中的第一位(高位*16)
			int int_ch1;
			if (hex_char1 >= '0' && hex_char1 <= '9')
				int_ch1 = (hex_char1 - 48) * 16; // // 0 的Ascll - 48
			else if (hex_char1 >= 'A' && hex_char1 <= 'F')
				int_ch1 = (hex_char1 - 55) * 16; // // A 的Ascll - 65
			else
				return null;
			i++;
			char hex_char2 = hexString.charAt(i); // /两位16进制数中的第二位(低位)
			int int_ch2;
			if (hex_char2 >= '0' && hex_char2 <= '9')
				int_ch2 = (hex_char2 - 48); // // 0 的Ascll - 48
			else if (hex_char2 >= 'A' && hex_char2 <= 'F')
				int_ch2 = hex_char2 - 55; // // A 的Ascll - 65
			else
				return null;
			int_ch = int_ch1 + int_ch2;
			retData[i / 2] = (byte) int_ch;// 将转化后的数放入Byte里
		}
		return retData;
	}

	/**
	 * 
	 * 插入单个配置信息（string,string）
	 * 
	 * @param key
	 * @param value
	 */
	public void putSetting(String key, String value) {
		Editor editor = preferences.edit();
		editor.putString(key, value);
		editor.commit();
	}

	/**
	 * 
	 * 插入单个配置信息（string,int）
	 * 
	 * @param key
	 * @param value
	 */
	public void putSetting(String key, int value) {
		Editor editor = preferences.edit();
		editor.putInt(key, value);
		editor.commit();
	}

	/**
	 * 插入单个配置信息（string,boolean）
	 * 
	 * @param key
	 * @param value
	 */
	public void putSetting(String key, Boolean value) {

		Editor editor = preferences.edit();
		editor.putBoolean(key, value);
		editor.commit();
	}

	/**
	 * 
	 * 插入多个配置信息
	 * Java学习之Iterator(迭代器)的一般用法 （转）
	 * @param params
	 */
	public void putSettings(HashMap<String, Object> params) {
		Editor editor = preferences.edit();
		Iterator<String> iter = params.keySet().iterator();
		while (iter.hasNext()) {
			String name = (String) iter.next();
			if (params.get(name).getClass() == Boolean.class) {
				editor.putBoolean(name, (Boolean) params.get(name));
			} else {
				editor.putString(name, (String) params.get(name));
			}
		}
		editor.commit();
	}

	/**
	 * 缺省返回-1
	 * 
	 * @param key
	 * @return
	 */
	public int getIntSetting(String key) {
		return preferences.getInt(key, -1);
	}

	/**
	 * 缺省返回null
	 * 
	 * @param key
	 * @return
	 */
	public String getStrSetting(String key) {
		return preferences.getString(key, null);
	}

	/**
	 * 缺省返回false
	 * 
	 * @param key
	 * @return
	 */
	public boolean getBoolean(String key) {
		return preferences.getBoolean(key, false);
	}

}

```

<h1 id="0211">0211. DataListener回调类</h1> 

[返回目录](#02)

```
package codewarehouse.yzkj.com.ceshi;

/**
 * 数据相关
 * @author 志强
 *
 * @param <T>
 */
public class DataListener<T> {

	public void onSuccess() {
	};

	public void onSuccess(T data) {
	};

	public void onFailed() {
	};

	public void onFailed(T data) {
	};
}

```
<h1 id="0221">写一个接口的清单</h1> 

[返回目录](#02)

```
package codewarehouse.yzkj.com.ceshi;


import java.util.List;

public interface ICommonWeb {
	/**
	 * 获取区域列表
	 * @param dataListener
	 */
	/*public void findDistrict(final DataListener<List<District>> dataListener);

	*//*获取店铺的商品的类别*//*
	public void findClass(String storeid, final DataListener<List<Classfication>> dataListener);
	
	*//**
	 * 广告
	 * @param dataListener
	 *//*
	public void findAdvertisementList(final DataListener<List<Advertisement>> dataListener);
	
	*//**
	 * 获取评论列表
	 * @param goodsId
	 * @param limit
	 * @param start
	 *//*
	public void findGoodsCommentsByCon(String goodsId, String limit, String start, final DataListener<List<Comment>> dataListener);

*/
    /**
     * 忘记密码
     * @param phoneNum
     * @param phoneCode
     * @param dataListener
     */
    public void forgetPassword(String phoneNum, String phoneCode, DataListener<String> dataListener);
}

```
<h1 id="0231">0231. 定义父类</h1>

[返回目录](#02)

```
package codewarehouse.yzkj.com.ceshi;

import android.app.ProgressDialog;
import android.content.Context;
import android.util.Log;

import com.google.gson.Gson;
import com.lidroid.xutils.HttpUtils;
import com.lidroid.xutils.exception.HttpException;
import com.lidroid.xutils.http.RequestParams;
import com.lidroid.xutils.http.ResponseInfo;
import com.lidroid.xutils.http.callback.RequestCallBack;
import com.lidroid.xutils.http.client.HttpRequest.HttpMethod;


import org.apache.http.client.CookieStore;
import org.apache.http.cookie.Cookie;
import org.apache.http.impl.client.DefaultHttpClient;
import org.apache.http.impl.cookie.BasicClientCookie;
import org.json.JSONObject;

import java.io.IOException;
import java.io.InputStream;
import java.lang.reflect.Type;
import java.util.List;

/**
 * Web请求基类
 * 
 * @author zeroangus
 * 
 */
public class BaseWeb<T> {
	//protected static String BaseUrl = "http://211.149.169.221:8080" + "/umijoy";
	//无线服务器
	//protected static String BaseUrl = "http://192.168.10.122:8080" + "/umijoy";
	//有线服务器
	//protected static String BaseUrl = "http://210.56.209.74:9080" + "/umijoy";
	//真正的服务器
	protected static String BaseUrl = "http://211.149.169.221:8080" + "/umijoyappsvr";
	private static String TAG = "BaseWeb";
	private HttpUtils mHttpUtil = null;//网络请求的实例
	private Context mContext;

	/*public static PreferenceUtil mPrefUtil; //用于配制信息的业务类 继成了各种方法
	protected ServiceApplication serviceApplication;*/

	private static String JSESSIONID = "";//作用是换页面的情况下，不要重新登录
			/*private static String JSESSIONID = ServiceApplication.getInstance()
			.readSession();//作用是换页面的情况下，不要重新登录*/

	public BaseWeb(Context context) {
		this.mContext = context;
		/*mPrefUtil = new PreferenceUtil(context, Constant.prefName, Context.MODE_PRIVATE);
		serviceApplication=ServiceApplication.getInstance();*/
	}

	/**
	 * 获取Http实例的方法
	 * 
	 * @return
	 */
	private HttpUtils getHttpUtil() {
		if (mHttpUtil == null) {
			mHttpUtil = new HttpUtils();
			//mHttpUtil.configCurrentHttpCacheExpiry(1000 * 10); //设置当前请求的缓存时间
			mHttpUtil.configCurrentHttpCacheExpiry(600000 * 10); //设置当前请求的缓存时间
		}
		return mHttpUtil;
	}

	/**
	 * 解析json串   T是外部类定义的泛型
	 * 
	 * @param json
	 * @param type
	 * @param listener
	 */
	protected void parse(String json, Type type, DataListener<T> listener) {

		//System.out.println("从服务端返回的原始数据字符串  ----------> " + json);    //正式版关闭
		//MyLog.ShowLog(json);
		//LogTxt.writeLog(json,"邻优网网络返回的数据");
		//PromptManager.showDialogTest1(mContext, "从服务端返回的原始数据字符串 ----------> " + json);

		JSONObject jsonObject;
		try {
			jsonObject = new JSONObject(json);//把字符串转化成一个json对象
			if ("true".equals(jsonObject.getString("success"))) {
				// jsonObject = new JSONObject(jsonObject.getString("data"));
				Gson gson = new Gson();

			/*	System.out
						.println("从字符串解析的data字段对应的数据 ----------> "
								+ jsonObject.getString("data"));    正式版关闭 */
				//PromptManager.showDialogTest1(mContext, "从字符串解析的data字段对应的数据  ----------> "
				//		+ jsonObject.getString("data"));

				T obj = gson.fromJson(jsonObject.getString("data"), type);
				listener.onSuccess(obj);
				//listener.onFailed(obj);
			} else {
				/*switch (serviceApplication.mPrefUtil.getIntSetting("tiShi")){
//					弹出的提示是公共的
					case 0:
						PublicUtil.ShowToast("访问网络失败，请重新访问");
						serviceApplication.mPrefUtil.putSetting("tiShi",10);
						break;
					//					不弹出的提示是公共的
					case 1:
						serviceApplication.mPrefUtil.putSetting("tiShi",10);
						break;
					//					弹出的服务端的提示
					default:
						PublicUtil.ShowToast("" + jsonObject.getString("msg"));
						break;
				}*/
				listener.onFailed();
			}
		} catch (Exception e) {
			listener.onFailed();
			//PublicUtil.ShowToast("" + e.toString());
			Log.e(TAG, "json parse failed : " + e.toString());
			//PromptManager.showDialogTest1(mContext, "解析失败，弹出解析失败的原因 : " + e.toString());
			e.printStackTrace();
		}
	}

	/**
	 * 解析json串
	 * 
	 * @param json
	 * @param listener
	 */
	protected void parse(String json, DataListener<String> listener) {

		System.out.println("parse ----------> " + json);    //正式版关闭
	//	LogTxt.writeLog(json,"邻优网网络返回的数据2");
		//PromptManager.showToastTest1(mContext, "从服务端返回的原始数据字符串 ----------> " + json);

		JSONObject jsonObject;
		try {
			jsonObject = new JSONObject(json);
			if ("true".equals(jsonObject.getString("success"))) {
				listener.onSuccess();
				listener.onSuccess("" + jsonObject.getString("msg"));
			} else {
			//	PublicUtil.ShowToast("" + jsonObject.getString("msg"));
				listener.onFailed();
			}
		} catch (Exception e) {
			listener.onFailed();
			Log.e(TAG, "json parse failed : " + e.toString());
		//	PromptManager.showDialogTest1(mContext, "json parse failed : " + e.toString());
			e.printStackTrace();
		}
	}

	/**
	 * 请求  IRequestListener是被类定义的一个内部回调接口
	 * 
	 * @param url
	 * @param params
	 */
	protected void post(String url, RequestParams params,
			final IRequestListener listener) {
	//	LogTxt.writeLog(url,"邻优网访问");
		// HttpUtils mHttpUtil = getHttpUtil();
		// mHttpUtil.configCurrentHttpCacheExpiry(1000 * 10);
		// mHttpUtil.configTimeout(5000);
		if (null != JSESSIONID) {    //如果cookie不为空，带上cookie 服务器端叫session
			System.out.println("JSESSIONID ----> " + JSESSIONID);
			//运用构造方法  创建一个实例  cookie和settion是一个键值对
			BasicClientCookie c = new BasicClientCookie(Constant.session_pref,
					JSESSIONID);
			c.setVersion(0);
			c.setPath("/");
			//c.toString() 相当于省份识别码
			c.setDomain(Constant.COOKIE_DOMAIN);
			               	System.out.println("JSESSIONID ----> " + c.toString());
			//获得访问网络的http对象
			DefaultHttpClient dh = (DefaultHttpClient) getHttpUtil()
					.getHttpClient();
			CookieStore cookieStore = dh.getCookieStore();
			cookieStore.addCookie(c);
			getHttpUtil().configCookieStore(cookieStore);
		}
		Log.e("tanyinqing post", url);
		//PromptManager.showDialogTest1(mContext,url+"   "+params.toString());
		//RequestCallBack<String>()是工具本身自带的内置回调方法
		showProgressDialog();
		getHttpUtil().send(HttpMethod.POST, url, params,
				new RequestCallBack<String>() {

					@Override
					public void onFailure(HttpException arg0, String arg1) {
						Log.e("post", arg0.toString() + "  " + arg1);
						/*PublicUtil.ShowToast("网络请求出错，请稍后再试!");*/
						/*if (serviceApplication.mPrefUtil.getIntSetting("PhoneCode")==1){
							serviceApplication.mPrefUtil.putSetting("PhoneCode",2);
						}else {
							//PublicUtil.ShowToast("网络不畅，请刷新下哦");
						}*/
                        closeProgressDialog();
                        listener.onFailed();
					}

					@Override
					public void onSuccess(ResponseInfo<String> responseInfo) {
						closeProgressDialog();
						DefaultHttpClient dh = (DefaultHttpClient) getHttpUtil()
								.getHttpClient();
						CookieStore cs = dh.getCookieStore();
						//返回的数据是一个Cookie的集合
						List<Cookie> cookies = cs.getCookies();
						for (int i = 0; i < cookies.size(); i++) {
							//从返回的Cookie集合里找到一个名字为"JSESSIONID"的保存到本地
							if ("JSESSIONID".equals(cookies.get(i).getName())) {
								JSESSIONID = cookies.get(i).getValue();
							/*	ServiceApplication.getInstance()
										.saveSession(JSESSIONID);*/
								break;
							}
						}
						Log.d("jack", "比较sessionid  " + JSESSIONID);
						//PromptManager.showDialogTest1(mContext,responseInfo.result.toString());
						listener.onSuccess(responseInfo.result);
					}
				});
	}

	private ProgressDialog pd;

	protected void closeProgressDialog() {
		if (pd != null) {
			try {
				pd.dismiss();
			} catch (Exception e) {

			}
		}
	}

	protected void showProgressDialog() {
		if (pd != null) {
			pd.dismiss();
		}
		pd = ProgressDialog.show(mContext, "", "数据加载中...", true, false);
		pd.show();

	}

	protected void showProgressDialog(String title, String content) {
		if (pd != null) {
			pd.dismiss();
		}
		pd = ProgressDialog.show(mContext, title, content, true, false);
		pd.show();
	}

	//定义网络访问的回调方法
	protected interface IRequestListener {
		public void onSuccess(String json);
        public void onFailed();
	}

	//从assets文件夹中获得模拟的返回数据
	protected String getAssetsData(String name) {
		String result = "";
		try {
			//获取输入流
			InputStream mAssets = mContext.getAssets().open(name);

			//获取文件的字节数
			int lenght = mAssets.available();
			//创建byte数组
			byte[] buffer = new byte[lenght];
			//将文件中的数据写入到字节数组中
			mAssets.read(buffer);
			mAssets.close();
			result = new String(buffer);
			return result;
		} catch (IOException e) {
			e.printStackTrace();
			Log.e("fuck", "error");
			LogTxt.writeLog(e.toString(), "getAssetsData  发生异常");
			return result;
		}
	}


}

```
<h1 id="0232">定义子类</h1>

[返回目录](#02)

```
package codewarehouse.yzkj.com.ceshi;

import android.content.Context;

import com.lidroid.xutils.http.RequestParams;

/**
 *广告、区域相关
 * @author 志强
 *
 */
public class CommonWeb extends BaseWeb implements ICommonWeb{

	private static String CommonUrl = BaseUrl + "/common/";

	private static String FindDistrictUrl = CommonUrl + "findDistrict.do";

	//private static String FindClass = CommonUrl + "findClass.do";
	private static String FindClass = "http://211.149.169.221:8080/umijoyappsvr/goods/findServiceTypeByDistrict.do";

	/*http://211.149.169.221:8080/umijoyappsvr/goods/findServiceTypeByDistrict.do?storeId=10*/

	private static String FindAdvertisementList = CommonUrl + "findAdvertisementList.do";

	private static String FindGoodsCommentsList = CommonUrl + "findGoodsCommentsByCon.do";

    /**
     * 忘记密码
     */
    private static String ForgetPasswordUrl = "http://211.149.169.221:8080/umijoyappsvr/common/findDistrict.do";

	private Context context;
	//对参数  网址可以打印个日志  不用多次实例化
	private static StringBuilder mStringBuilder;

	public CommonWeb(Context context) {
		super(context);
		 mStringBuilder=new StringBuilder();
	}

	/*
	* 获取店铺类别的信息
	*/
	/*@Override
	public void findClass(String storeid, final DataListener<List<Classfication>> dataListener) {

		RequestParams params=new RequestParams();
		params.addBodyParameter("storeId",storeid);
		p.L("获得产品类别时传递的参数", storeid);
		//把访问的url改了，目的是访问网络成功  等接口写好后再把网址该过来
		post(FindClass, params, new IRequestListener() {
			public void onSuccess(String json) {    //利用模拟数据进行测试 数据处理能力的方法
				Type type = new TypeToken<List<Classfication>>() {
				}.getType();
				parse(json, type, dataListener);
			}

			@Override
			public void onFailed() {
				//如果访问网络失败要在主页回应   则调用该方法
				dataListener.onFailed();
			}

		});
	}*/


	/**
	 * 获取区域列表
	 * @param dataListener
	 */
	/*public void findDistrict(final DataListener<List<District>> dataListener)
	{
		//RequestParams就是一个请求是携带的一个数据参数  以键值对的形式
		RequestParams params = new RequestParams();
		post(FindDistrictUrl, params, new IRequestListener() {

            @Override
            public void onFailed() {
				*//*
				 //dataListener.onFailed();
				String json="{\"data\":[{\"createTime\":\"2015-02-14T14:41:46\",\"id\":1,\"name\":\"模拟数据\n" +
						"1\"},{\"createTime\":\"2015-02-14T14:41:46\",\"id\":1,\"name\":\"模拟数据2\"}],\"msg\":\"查询成功\n" +
						"！\",\"success\":true}";
				Type type = new TypeToken<List<District>>() {
				}.getType();
				parse(json, type, dataListener);
				 *//*

            }
			public void onSuccess(String json) {
				String json1=""; //这个是模拟数据
				Type type = new TypeToken<List<District>>() {
				}.getType();
				parse(json, type, dataListener);
			}
		});
	}



	public void findAdvertisementList(final DataListener<List<Advertisement>> dataListener)
	{
		RequestParams params = new RequestParams();
		serviceApplication.mPrefUtil.putSetting("tiShi",1);
		post(FindAdvertisementList, params, new IRequestListener() {
            @Override
            public void onFailed() {
                dataListener.onFailed();
            }
			public void onSuccess(String json) {
				Type type = new TypeToken<List<Advertisement>>() {
				}.getType();
				parse(json, type, dataListener);
			}
		});
	}*/
/*
	获取评论列表
 */
	/*@Override
	public void findGoodsCommentsByCon(String goodsId, String limit,
			String start, final DataListener<List<Comment>> dataListener) {
		RequestParams params = new RequestParams();
		params.addBodyParameter("goodsId", goodsId);
		params.addBodyParameter("limit", limit);
		params.addBodyParameter("start", start);
				post(FindGoodsCommentsList, params, new IRequestListener() {

					@Override
					public void onFailed() {
						dataListener.onFailed();
					}

					public void onSuccess(String json) {
						Type type = new TypeToken<List<Comment>>() {
						}.getType();
						parse(json, type, dataListener);
					}
				});

	}*/

    @Override
    public void forgetPassword(String phoneNum, String phoneCode,
                               final DataListener<String> dataListener) {
        RequestParams params = new RequestParams();
        params.addBodyParameter("phoneNum", phoneNum);
        params.addBodyParameter("phoneCode", phoneCode);

		mStringBuilder.delete(0,mStringBuilder.length());
		mStringBuilder.append("携带的参数是：");
		mStringBuilder.append("phoneNum:"+phoneNum+";");
		mStringBuilder.append("phoneCode:"+phoneCode+";");
		mStringBuilder.append("访问的网址是：");
		mStringBuilder.append(ForgetPasswordUrl);
		LogTxt.writeLog(mStringBuilder.toString(), "忘记密码访问的方法");

		post(ForgetPasswordUrl, params, new IRequestListener() {

			public void onSuccess(String json) {

				json=getAssetsData("ceshi.txt");


				LogTxt.writeLog(json,"忘记密码 返回的数据");
				/*Type type = new TypeToken<String>() {
				}.getType();
				parse(json, type, dataListener);*/

				dataListener.onSuccess(json);
			}

			@Override
			public void onFailed() {
				dataListener.onFailed();
			}
		});
    }




}

```
<h1 id="0241">调用网络  其他处调用 返回字符串</h1> 

[返回目录](#02)

```
 private CommonWeb mCommonWeb;

 mCommonWeb = new CommonWeb(this);

       mCommonWeb.forgetPassword("2", "3", new DataListener<String>() {

            @Override
            public void onSuccess(String data) {
//				PublicUtil.ShowToast("重置密码成功，请重新登陆！");
//				PublicUtil.ShowToast("随机密码："+data);

                Toast.makeText(MainActivity.this, data, Toast.LENGTH_LONG).show();

            }

            @Override
            public void onFailed() {

            }

        });
```
<h1 id="0301">访问网络  返回图片</h1> 

[返回目录](#02)

```
首先引入jar包
universal-image-loader-1.9.3.jar  引入这个jar包

其次进行初始，ImageLoader进行初始化，DisplayImageOptions，进行配置

就可以调用了，调用的方法

private static ImageLoader imageLoader;
    private static ImageView imageView;



 imageView= (ImageView) findViewById(R.id.imageView);

        imageLoader = PublicUtil.getImageLoader();

        String pic="http://upload-images.jianshu.io/upload_images/5358439-e03c26b421532d55.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240";
        if (null!=pic&&!pic.equals(""))
        {
            //imageLoader.displayImage(Constant.URLBASE+pics.get(0).getPic(), imageGoods,PublicUtil.getGoodsOption());
            imageLoader.displayImage(pic, imageView,PublicUtil.getGoodsOption());
        }
        else
        {
            imageView.setImageResource(R.drawable.default_goods);
        }



配置初始化
package codewarehouse.yzkj.com.ceshi;


import android.app.Activity;
import android.content.Context;
import android.content.res.Resources;
import android.graphics.Bitmap;
import android.view.View;
import android.view.inputmethod.InputMethodManager;
import android.widget.Toast;

import com.nostra13.universalimageloader.cache.memory.impl.WeakMemoryCache;
import com.nostra13.universalimageloader.core.DisplayImageOptions;
import com.nostra13.universalimageloader.core.ImageLoader;
import com.nostra13.universalimageloader.core.ImageLoaderConfiguration;
import com.nostra13.universalimageloader.core.assist.ImageScaleType;


public class PublicUtil {

    /**
     * 将时间转化
     *
     * @param content
     *            内容
     */
   /* public static String zhuanhuan(String content) {
        p.L("从数据库传入的时间",content);

        p.L("从数据库传入的时间方法2转化后的时间",DateUtil.TimeStamp2Date(content, " yyyy-MM-dd HH:mm:ss "));

        return  DateUtil.TimeStamp2Date(content, "yyyy-MM-dd HH:mm:ss ");
    }*/
    /**
     * 将字符串的后两位用**代替
     *
     * @param content
     *            内容
     */
    public static String tiHuan(String content) {
        int a=0;
        if (content.length()>3){
            a=3;
        }else if(content.length()>1&&content.length()<=3){
            a=1;
        }

        String b=content.substring(0,content.length()-a);
        StringBuffer result = new StringBuffer();
        result.append(b);
        result.append("***");
        return result.toString();
        //return  content;
    }

	/**
	 * Toast提醒
	 * 
	 * @param content
	 *            内容
	 */
	/*public static void ShowToast(String content) {
		Toast.makeText(ServiceApplication.getInstance(), content, Toast.LENGTH_SHORT)
				.show();
	}*/
	
	/**
	 * 获取设备宽度
	 * @return
	 */
/*	public static int getDeviceWidth() {
		return ServiceApplication.getInstance().getResources().getDisplayMetrics().widthPixels;
	}*/

	/**
	 * 获取设备高度
	 * @return
	 */
	/*public static int getDeviceHeight() {
		return ServiceApplication.getInstance().getResources().getDisplayMetrics().heightPixels;
	}*/
	
/*	public static int getResColor(int resid)
	{
		Resources rs = ServiceApplication.getInstance().getResources();
		return rs.getColor(resid);
	}*/
	
	/**
     * 判断输入合法性
     * @param name
     * @param addr
     * @param phone
     * @return
     */
    public static boolean isLegal(String name ,String addr,String phone)
    {
        if("".equals(name))
        {
           // PublicUtil.ShowToast("请输入联系人姓名");
            return false;
        }
        if("".equals(addr))
        {
           // PublicUtil.ShowToast("请输入联系人地址");
            return false;
        }
     /*   if("".equals(phone) || !RegexUtil.isPhone(phone))
        {
            PublicUtil.ShowToast("请输入正确的联系人电话");
            return false;
        }*/
        return true;
    }


    //图片下载的参数的配置
    private static DisplayImageOptions classOption;
    public static DisplayImageOptions getClassOption()
    {
        if (null==classOption)
        {
            classOption=new DisplayImageOptions.Builder().bitmapConfig(Bitmap.Config.RGB_565).showImageOnFail(R.drawable.class_default).showImageOnLoading(R.drawable.class_default).imageScaleType(ImageScaleType.EXACTLY).cacheOnDisk(true).build();
        }
        return classOption;
    }

    private static DisplayImageOptions adsOption;
    public static DisplayImageOptions getAdsOption()
    {
        if(null == adsOption)
        {
            adsOption = new DisplayImageOptions.Builder().bitmapConfig(Bitmap.Config.RGB_565).showImageOnFail(R.drawable.default_ad).showImageOnLoading(R.drawable.default_ad).imageScaleType(ImageScaleType.EXACTLY).cacheOnDisk(true).build();
        }
        return  adsOption;
    }
    private static DisplayImageOptions goodsOption;

    public static DisplayImageOptions getGoodsOption()
    {
        if(null == goodsOption)
        {
            goodsOption = new DisplayImageOptions.Builder().bitmapConfig(Bitmap.Config.RGB_565).showImageOnFail(R.drawable.default_goods).showImageOnLoading(R.drawable.default_goods).imageScaleType(ImageScaleType.EXACTLY).cacheOnDisk(true).build();
        }
        return  goodsOption;
    }

    private static DisplayImageOptions headOption;

    public static DisplayImageOptions getHeadOption()
    {
        if(null == headOption)
        {
            headOption = new DisplayImageOptions.Builder().bitmapConfig(Bitmap.Config.RGB_565).showImageOnFail(R.drawable.default_head).showImageOnLoading(R.drawable.default_head).imageScaleType(ImageScaleType.EXACTLY).cacheOnDisk(true).build();
        }
        return  headOption;
    }


    private static ImageLoader mImageLoader;

    public static ImageLoader getImageLoader() {
        if (mImageLoader == null) {
            mImageLoader = ImageLoader.getInstance();
            ImageLoaderConfiguration configuration = new ImageLoaderConfiguration.Builder(ServiceApplication.getInstance()).threadPoolSize(3).memoryCache(new WeakMemoryCache()).build();
            mImageLoader.init(configuration);
        }

        return mImageLoader;
    }
    
    public static void closeKeyBoard(Context context)
    {
        /**隐藏软键盘**/
        View view = ((Activity)context).getWindow().peekDecorView();
        if (view != null) {
            InputMethodManager inputmanger = (InputMethodManager) ((Activity)context).getSystemService(Context.INPUT_METHOD_SERVICE);
            inputmanger.hideSoftInputFromWindow(view.getWindowToken(), 0);
        }
    }

    /**
     * 将字符串价格 转换为 显示2位小数的字符串
     *
     * @param str
     * @return
     */
    public static String priceFormat(String str)
    {
        float price = Float.valueOf(str);
        return String.format("%.2f ", price);
    }
}

```



 
<h1 id="040101">040101. activity父类</h1> 

[返回](#01)

```
package codewarehouse.yzkj.com.ceshi;

import android.app.Activity;
import android.app.AlertDialog;
import android.content.Context;
import android.content.Intent;
import android.os.Bundle;
import android.support.v4.app.FragmentActivity;
import android.view.View;
import android.widget.ImageView;
import android.widget.Toast;

import com.lidroid.xutils.ViewUtils;


public abstract class BaseActivity extends FragmentActivity
{
    
	protected  static Context context;
    /*protected ServiceApplication application = null;
    protected RiZhiDB riZhiDB;*/

    
    @Override
    protected void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        /*application = ServiceApplication.getInstance();
        application.register(this);*/
        context = this;
        //这是进行注解绑定的初始化  xUtils-2.6.14.jar中的方法
        ViewUtils.inject(this);
       // riZhiDB=new RiZhiDB(this);
        
        createView();
        
        setListeners();
        
        initDatas();
        

    }
    
    /**
     * 通过Class启动Activity
     * 
     * @param cls
     */
    protected void startActivityByClass(Class cls)
    {
        Intent intent = new Intent();
        intent.setClass(this, cls);
        startActivity(intent);
    }
    
    /**
     * 设置事件监听
     */
    abstract void setListeners();
    
    /**
     * 初始化设置
     */
    abstract void initDatas();
    
    /**
     * 初始化
     */
    abstract void createView();
    
    @Override
    protected void onStart()
    {
        // TODO Auto-generated method stub
        super.onStart();
    }
    
    @Override
    protected void onResume()
    {
        // TODO Auto-generated method stub
        super.onResume();
    }
    
    @Override
    protected void onPause()
    {
        // TODO Auto-generated method stub
        super.onPause();
    }
    
    @Override
    protected void onStop()
    {
        // TODO Auto-generated method stub
        super.onStop();
    }

    public void p(String title,String msg) {
        if (true) {
            new AlertDialog.Builder(BaseActivity.this).setTitle(title).setMessage(msg).show();
        }
    }

    public  void tt(String msg) {
        if (true) {
            Toast.makeText(BaseActivity.this, msg, Toast.LENGTH_LONG).show();
        }
    }

   
}

```

<h1 id="040102">040102. activity标题类</h1>

[返回目录](#01)

```
package codewarehouse.yzkj.com.ceshi;

import android.graphics.Color;
import android.os.Bundle;
import android.os.PersistableBundle;
import android.os.SystemClock;
import android.view.Gravity;
import android.view.View;
import android.view.ViewGroup;
import android.widget.Button;
import android.widget.FrameLayout;
import android.widget.ImageButton;
import android.widget.LinearLayout;
import android.widget.LinearLayout.LayoutParams;
import android.widget.RelativeLayout;
import android.widget.TextView;
import android.widget.Toast;



/**
 * 标题的内容添加左右标题的代码
 *  mLinearTitleContent.addView(mButtonLeft);
 mLinearTitleContent.addView(mImgeTitle);
 mLinearTitleContent.addView(mButtonRight);
 */
public abstract class TitleBarActivity extends BaseActivity {
    private LinearLayout mLinearTitle; 
    private LinearLayout mLinearDivider;//这个是分割线
    private LinearLayout mMainView;
    private FrameLayout mContentView;
    
    // 这个是左右按钮 中间标题栏
    private RelativeLayout mLinearTitleContent;
    private ImageButton mButtonLeft;
    private TextView mImgeTitle;
    public Button mButtonRight;

    @Override
    public void onCreate(Bundle savedInstanceState, PersistableBundle persistentState) {
        super.onCreate(savedInstanceState, persistentState);
    }

    protected void createView() {
        System.out.println(" -----> initView");
        mMainView = new LinearLayout(this);
        mMainView.setLayoutParams(new LayoutParams(LayoutParams.MATCH_PARENT, LayoutParams.MATCH_PARENT));
        mMainView.setOrientation(LinearLayout.VERTICAL);

        initTitleView();
        mMainView.addView(mLinearTitle);
        mContentView = (FrameLayout) getWindow().getDecorView().findViewById(android.R.id.content);
        View v = null;
        if (mContentView.getChildCount() > 0) {
            v = mContentView.getChildAt(0);
            ViewGroup parent = (ViewGroup) v.getParent();
            if (parent != null) {
                parent.removeView(v);
            }
            mMainView.addView(v);
        }
        setContentView(mMainView, new LayoutParams(LayoutParams.MATCH_PARENT, LayoutParams.MATCH_PARENT));

    }

    /**
     * 设置title
     */
    public void setTitle(String resid) {
        mImgeTitle.setText(resid);
    }

    /**
     * 设置左侧按钮
     *
     * @param content
     * @param resid
     * @param listener
     */
    public void setButtonLeft(String content, int resid, View.OnClickListener listener) {
        //mButtonLeft.setText(content);
        mButtonLeft.setBackgroundResource(resid);
        mButtonLeft.setOnClickListener(listener);
    }

    /**
     * 设置左侧按钮
     *
     * @param content
     * @param
     */
    public void setButtonLeft(String content) {
        mButtonLeft.setVisibility(View.VISIBLE);
        //mButtonLeft.setText(content);
    }

    /**
     * 设置右侧按钮
     *
     * @param content
     * @param resid
     */
    public void setButtonRight(String content, int resid) {
        mButtonRight.setText(content);
        mButtonRight.setBackgroundResource(resid);
        mButtonRight.setVisibility(View.VISIBLE);
    }

    /**
     * 设置右侧按钮
     *
     * @param content
     * @param
     */
    public void setButtonRight(String content) {
        if ("".equals(content)) {
            mButtonRight.setVisibility(View.GONE);
        } else {
            mButtonRight.setText(content);
            mButtonRight.setVisibility(View.VISIBLE);
        }
    }

    void initTitleView() {
        /* title */
        mLinearTitle = new LinearLayout(this);
        LayoutParams mTitleLayoutParams = new LayoutParams(LayoutParams.MATCH_PARENT, DensityUtil.dip2px(this, 49));
        mLinearTitle.setLayoutParams(mTitleLayoutParams);
        mLinearTitle.setOrientation(LinearLayout.VERTICAL);

		/* start title divider  这个是分割线，高位1像素*/
        mLinearDivider = new LinearLayout(this);
        LayoutParams mTitleDividerParams = new LayoutParams(LayoutParams.MATCH_PARENT, DensityUtil.dip2px(this, 1));
        mLinearDivider.setLayoutParams(mTitleDividerParams);
        mLinearDivider.setBackgroundColor(Color.LTGRAY);
		/* end title divider*/

		/* start title content  这个是标题内容的布局  高被限制在48像素高*/
        mLinearTitleContent = new RelativeLayout(this);
       RelativeLayout.LayoutParams mTitleContentLayoutParams = new RelativeLayout.LayoutParams(RelativeLayout.LayoutParams.MATCH_PARENT, DensityUtil.dip2px(this, 48));
       // mTitleContentLayoutParams.gravity = Gravity.CLIP_VERTICAL;
       // mLinearTitleContent.setOrientation(LinearLayout.HORIZONTAL);
        mLinearTitleContent.setLayoutParams(mTitleContentLayoutParams);
       // mLinearTitleContent.setBackgroundColor(Color.DKGRAY);
      // mLinearTitleContent.setBackgroundColor(PublicUtil.getResColor(R.color.saletoexamineaar_biaoTiLan_color));
        mLinearTitleContent.setGravity(Gravity.CENTER_VERTICAL);

//这个是左边的按钮
        LayoutParams buttonParamsLeft = new LayoutParams(LayoutParams.WRAP_CONTENT, DensityUtil.dip2px(this, 48));
         buttonParamsLeft.gravity=Gravity.CENTER;

        mButtonLeft = new ImageButton(this);
        mButtonLeft.setLayoutParams(buttonParamsLeft);
        /*mButtonLeft.setText("左侧");
        mButtonLeft.setTextColor(PublicUtil.getResColor(R.color.app_color));
        mButtonLeft.setGravity(Gravity.CENTER_VERTICAL);*/
        //mButtonLeft.setBackgroundResource(R.drawable.back_selector);
       // mButtonLeft.setBackgroundColor(PublicUtil.getResColor(R.color.saletoexamineaar_biaoTiLan_color));
       // mButtonLeft.setImageResource(R.drawable.left_arrow);
        mButtonLeft.setVisibility(View.GONE);
        mButtonLeft.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View arg0) {
                LeftButtonClicked();
            }
        });

        //这个是中间的标题
        mImgeTitle = new TextView(this);
        RelativeLayout.LayoutParams params = new RelativeLayout.LayoutParams(RelativeLayout.LayoutParams.WRAP_CONTENT, RelativeLayout.LayoutParams.WRAP_CONTENT);
        params.addRule(RelativeLayout.CENTER_IN_PARENT);
        mImgeTitle.setLayoutParams(params);
       // mImgeTitle.setTextColor(PublicUtil.getResColor(R.color.saletoexamineaar_biaoTiLan_ziti_color));
        mImgeTitle.setTextSize(18);

        //这个是右边的按钮
        RelativeLayout.LayoutParams buttonParamsRight = new RelativeLayout.LayoutParams(RelativeLayout.LayoutParams.WRAP_CONTENT, RelativeLayout.LayoutParams.WRAP_CONTENT);
        buttonParamsRight.addRule(RelativeLayout.ALIGN_PARENT_RIGHT);
       //buttonParamsRight.setMarginEnd(10);

        mButtonRight = new Button(this);
        mButtonRight.setLayoutParams(buttonParamsRight);
        mButtonRight.setText("右侧按钮");
        mButtonRight.setTextSize(16);
       // mButtonRight.setTextColor(PublicUtil.getResColor(R.color.saletoexamineaar_biaoTiLan_ziti_color));
        mButtonRight.setGravity(Gravity.CENTER);
        mButtonRight.setVisibility(View.INVISIBLE);
      //  mButtonRight.setBackgroundResource(R.color.saletoexamineaar_biaoTiLan_color);
        mButtonRight.getBackground().setAlpha(0);//0~255透明度值  0全透明
        mButtonRight.setOnClickListener(new View.OnClickListener() {

            @Override
            public void onClick(View arg0) {
                RightButtonClicked();
            }
        });

        //按钮加入 3次点击的监听
        mImgeTitle.setOnClickListener(new View.OnClickListener() {
            //需要监听几次点击事件数组的长度就为几
            //如果要监听双击事件则数组长度为2，如果要监听3次连续点击事件则数组长度为3...
            long[] mHints = new long[2];//初始全部为0

            @Override
            public void onClick(View v) {
                //将mHints数组内的所有元素左移一个位置
                System.arraycopy(mHints, 1, mHints, 0,
                        mHints.length - 1);
                //获得当前系统已经启动的时间
                mHints[mHints.length - 1] =
                        SystemClock.uptimeMillis();
                if (SystemClock.uptimeMillis() - mHints[0] <= 500) {
                 //  Toast.makeText(TitleBarActivity.this, "点击了2次", Toast.LENGTH_SHORT).show();
                 //跳转到自定义的开发者页面
                	// startActivityByClass(Develope.class);
                }
            }
        });

        mLinearTitleContent.addView(mButtonLeft);
        mLinearTitleContent.addView(mImgeTitle);
        mLinearTitleContent.addView(mButtonRight);

       // mLinearTitleContent.setBackgroundColor(Color.WHITE);
		/* end title content*/

        mLinearTitle.addView(mLinearTitleContent);
        mLinearTitle.addView(mLinearDivider);
    }

    /**
     * 左侧按钮事件
     */
    protected abstract void RightButtonClicked();

    /**
     * 右侧按钮事件
     */
    protected abstract void LeftButtonClicked();
}

```

<h1 id="040103">040103. activity带适配器的模板类</h1>

[返回目录](#01)

```
Activity注册
 		<activity
            android:name=".activity.activity.AccountManagementAcitvity"
            android:label="账号管理"
            android:screenOrientation="portrait"
            android:theme="@android:style/Theme.Light.NoTitleBar" >
        </activity>




package codewarehouse.yzkj.com.ceshi;


import android.app.Activity;
import android.content.Context;
import android.graphics.Bitmap;
import android.os.Bundle;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ListView;
import android.widget.TextView;

import com.lidroid.xutils.ViewUtils;
import com.lidroid.xutils.view.annotation.ContentView;
import com.lidroid.xutils.view.annotation.ViewInject;

import java.util.ArrayList;
import java.util.List;

@ContentView(R.layout.activity_main)
public class mobanActivity extends TitleBarActivity{

注意：清单文件中注册
	 private MobanModel mMobanModel;

	@ViewInject(R.id.listDistrict)
	private ListView listDistrict;
	 
	 @Override
		void setListeners() {
			// TODO Auto-generated method stub
			
		}

		@Override
		void initDatas() {	
			 setTitle("拜访详情");
		        setButtonLeft("1");
		        setButtonRight("编辑");
			
			 if(mMobanModel == null)
		        {
				 mMobanModel = new MobanModel(this);
		        }			

			//向适配器中填充数据
			mMobanModel.requestDistrict();
			//数据适配布局
			listDistrict.setAdapter(mMobanModel.getDistrictAdapter());


		}
		
		@Override
		protected void RightButtonClicked() {
			// TODO Auto-generated method stub
			
		}

		@Override
		protected void LeftButtonClicked() {
			// TODO Auto-generated method stub
			 finish();
		}
	
		//这个是主导器
	private class MobanModel<T> extends BaseModel{
		private MybanAdapter mymobanAdapter;		
		public MobanModel(Context mContext) {
			super(mContext);
			// TODO Auto-generated constructor stub
			 mymobanAdapter=new MybanAdapter(mContext);
		}
		
		public MybanAdapter getDistrictAdapter()
		{
			return mymobanAdapter;
		}
		
		/**
		 * 请求数据,并把数据写入适配器中
		 */
		public void requestDistrict()
		{
			List<String> tan=new ArrayList<>();
			tan.add("tan1");
			tan.add("tan2");
			tan.add("tan3");
			mymobanAdapter.appendToListAndClear(tan);

			/*mDistrictWeb.findDistrict(new DataListener<List<District>>(){


				@Override
				public void onSuccess(List<District> data) {
					for(District d:data){
						//p.dd(context,d.toString());
						p.L("地址信息的对象", d.toString());
					}
					if(null != data)
					{
						mDistrictAdapter.appendToListAndClear(data);
					}
				}

				@Override
				public void onFailed(List<District> data) {

				}
			});*/
		}
		
	}
	
	//这个是适配器
	 private static class MybanAdapter extends AdapterBase {
	        private static Context mContext;
	        public MybanAdapter(Context baseContext) {
	            super(baseContext);
	            this.mContext = context;
	        }

	        @Override
	        protected View getExView(int position, View convertView, ViewGroup parent) {
	            //getItem是父类中的方法 从父类中的方法里得到数据 在这里运用
	            String address = (String) getItem(position);
	            ViewHolder holder;
	            if(convertView == null)
	            {
	                holder = new ViewHolder();
	                convertView = mInflater.inflate(R.layout.district_item, null);
	               ViewUtils.inject(holder, convertView);
	                convertView.setTag(holder);
	            }
	            else
	            {
	                holder = (ViewHolder) convertView.getTag();
	            }

	            holder.update(address);
	            return convertView;
	        }
	        private static class ViewHolder    {

	           @ViewInject(R.id.textDistrict)
	            private TextView iv_head;

	            String address;

	            void update(String address){
	                this.address = address;
	                iv_head.setText(address);
	            }

	          /*  @OnClick(R.id.iv_head)
	            private void getPhoto(View view){

	MyLog.ShowLog("点击被响应了2");
	            }*/

	        }
	    }	
}



对应的布局文件

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:gravity="center_vertical"
    android:orientation="horizontal" >
   
    <TextView
        android:id="@+id/textDistrict"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:text="成达小区"
        android:textSize="18sp" />

</LinearLayout>

```
<h1 id="040104">040104. activity不带适配器的模板类</h1>

[返回目录](#01)

```
package com.linyou.lifedelivery.activity.activity;

import android.app.Activity;
import android.content.Context;
import android.graphics.Bitmap;
import android.os.Bundle;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ListView;
import android.widget.TextView;

import com.lidroid.xutils.ViewUtils;
import com.lidroid.xutils.view.annotation.ContentView;
import com.lidroid.xutils.view.annotation.ViewInject;
import com.linyou.lifedelivery.R;
import com.linyou.lifedelivery.activity.adapter.AdapterBase;
import com.linyou.lifedelivery.activity.model.BaseModel;

import java.util.ArrayList;
import java.util.List;

@ContentView(R.layout.activity_addaccount)
public class AddAccountAcitvity extends TitleBarActivity {


    private MobanModel mMobanModel;

    @ViewInject(R.id.listDistrict)
    private ListView listDistrict;

    @Override
    void setListeners() {
        // TODO Auto-generated method stub

    }

    @Override
    void initDatas() {
        setTitle("拜访详情");
        setButtonLeft("1");
        setButtonRight("编辑");

        if (mMobanModel == null) {
            mMobanModel = new MobanModel(this);
        }

    }

    @Override
    protected void RightButtonClicked() {
        // TODO Auto-generated method stub

    }

    @Override
    protected void LeftButtonClicked() {
        // TODO Auto-generated method stub
 			finish();
    }

    //这个是主导器
    private class MobanModel<T> extends BaseModel {

        public MobanModel(Context mContext) {
            super(mContext);
            // TODO Auto-generated constructor stub
        }


    }
}
```
<h1 id="040105">5. activity之间跳转</h1>

[返回目录](#01)

```
	Intent i = new Intent();
        i.setAction(Constant.addr_sel);
        i.setClass(this, AddrManageActivity.class);
        startActivityForResult(i, Code.requestCode);


		 @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent 
	data) {

        if (Code.requestCode == requestCode && Code.addrSelResult == 
		resultCode) {
            mDeliveryAddress = (DeliveryAddress) 
			data.getBundleExtra(Constant.INTENT_ADDR).get(Constant.INTENT_ADDR)
			;
            mConfirmModel.setDeliveryAddress(mDeliveryAddress);
            editName.setText("" + mDeliveryAddress.getReciever());
            editPhone.setText("" + mDeliveryAddress.getRecieverPhone());
            textAddr.setText("" + mDeliveryAddress.getAddress());
        }

        super.onActivityResult(requestCode, resultCode, data);
    }


		action = getIntent().getAction();
		if(Constant.addr_sel.equals(action) )		
		{
			mAddrManageModel.selectAddr(position);
		}


		Intent data = new Intent();
		DeliveryAddress address = 
		(DeliveryAddress)mAddrAdapter.getItem(position);		
		Bundle b = new Bundle();
		b.putSerializable(Constant.INTENT_ADDR,address);
		data.putExtra(Constant.INTENT_ADDR, b);
		((Activity) mContext).setResult(Code.addrSelResult, data);
		closeActivity();

		//这个是把代码抽取出来
		public class Code {	
			public static int requestCode = 0;	
			public static int addrSelResult = 10;	
		}
```

<h1 id="040201">040201. model父类</h1>

[返回目录](#01)

```
package codewarehouse.yzkj.com.ceshi;

import android.app.Activity;
import android.content.Context;
import android.content.Intent;

public class BaseModel {
	
	protected Context mContext;
	
	/*protected ServiceApplication serviceApplication;//全局 成员变量 成员方法

	protected RiZhiDB riZhiDB;*/
	
	public BaseModel(Context mContext)
	{
		this.mContext = mContext;
		//serviceApplication = ServiceApplication.getInstance();
		//riZhiDB=new RiZhiDB(mContext);
	}
	

	/*public boolean isLogin()//判断是否登录
	{
		User user = serviceApplication.readUser();
		if(null != user)
		{
			return true;
		}
		else
		{
			return false;
		}
	}
	
	protected User getUser()//获取用户
	{
		return serviceApplication.readUser();
	}*/
	
	/**
	 * 关闭当前activity
	 */
	protected void closeActivity()
	{
		((Activity)mContext).finish();
	}
	
	/**
	 * 跳转到其他activity
	 * @param cls
	 */
	protected void startAcitityByClass(Class cls)
	{
		Intent intent = new Intent();
		intent.setClass(mContext, cls);
		mContext.startActivity(intent);
	}
	
	
}

```

<h1 id="040301">040301. adapter父类</h1>

[返回目录](#01)

```
package codewarehouse.yzkj.com.ceshi;

import java.util.ArrayList;
import java.util.List;

import android.app.Activity;
import android.content.Context;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.BaseAdapter;

public abstract class AdapterBase<T> extends BaseAdapter
{
    /*
      但对于一些容器类型（比如，ArrayList、HashMap）的实例变量，
    不可以改变容器变量本身，但可以修改容器中存放的对象，这一点在编程中用到很多
     */
    //运用List<T>这个对象集合存放多种形式的对象，运用了泛型替代
    public final List<T> mList = new ArrayList<T>();
    public Context context;
    //布局适配器  将布局转化成对象 从而和数据一一对应
    public LayoutInflater mInflater;
    
    public AdapterBase(Context baseContext)
    {
        this.context = baseContext;
        mInflater = LayoutInflater.from(baseContext);
        
    }
    
    public List<T> getList()
    {
        return mList;
    }

    //将一个对象添加到集合中
    public void appendToList(T t)
    {
        if (t == null)
        {
            return;
        }
        mList.add(t);
        notifyDataSetChanged();
    }

    //将一个对象集合添加到集合中
    public void appendToList(List<T> list)
    {
        if (list == null)
        {
            return;
        }
        mList.addAll(list);
        notifyDataSetChanged();
    }
    //先清空结合  在把一个新的集合添加到集合中
    public void appendToListAndClear(List<T> list)
    {
        mList.clear();
        this.appendToList(list);
    }

    //在把一个新的集合添加到集合的最上层
    public void appendToTopList(List<T> list)
    {
        if (list == null)
        {
            return;
        }
        mList.addAll(0, list);
        notifyDataSetChanged();
    }

    //请空集合
    public void clear()
    {
        mList.clear();
        notifyDataSetChanged();
    }
    
    @Override  //返回集合个个数
    public int getCount()
    {
        return mList.size();
    }
    
    @Override //返回集合中的某个元素
    public Object getItem(int position)
    {
        if (position > mList.size() - 1)
        {
            return null;
        }
        return mList.get(position);
    }
    //移除集合中的某个位置的元素
    public void removeItem(int position)
    {
        if (position >= 0 && position < mList.size())
        {
            mList.remove(position);
            notifyDataSetChanged();
        }
    }
    //移除集合中的某个指定元素
    public void removeItem(T item)
    {
        if (mList.contains(item))
        {
            mList.remove(item);
            notifyDataSetChanged();
        }
    }
    
    @Override
    public long getItemId(int position)
    {
        return position;
    }
    
    @Override
    public View getView(int position, View convertView, ViewGroup parent)
    {
        return getExView(position, convertView, parent);
    }
    //abstract加入这个关键词表示是抽象的方法，子类中必须进行重写这个方法

    protected abstract View getExView(int position, View convertView, ViewGroup parent);
    
}

```
05. 常量与配置模块

<h1 id="0501">常量</h1>  

[返回目录](#01)

```
package codewarehouse.yzkj.com.ceshi;

public class Constant {
	//下载图片是用到的网址
	//public static final String URLBASE = "http://210.56.209.74:9080/";
	// 下载图片是用到的网址
	public static final String URLBASE = "http://211.149.169.221/";


	//微信的真实数据 注册码
	public static final String APP_ID = "wx405f674449bed855";


	public static final String prefName = "umijoy_pref";

	//配置信息中用户值对应的键
	public static final String user_pref = "user";
	//配置信息中用户名字值对应的键
	public static final String user_name = "userName";

	//配置信息中session值对应的键
	public static final String session_pref = "JSESSIONID";
	//public static final String COOKIE_DOMAIN = "210.56.209.74:9080";
	public static final String COOKIE_DOMAIN = "211.149.169.221:8080";

	public static final String district_pref = "district";
	//配置信息中地址值对应的键
    public static final String address_pref = "address";

	//第一个图片对应的商品的type  用于区分四种不同的类型
	public static final String type_market = "1";
	public static final String type_food = "2";
	public static final String type_wash = "3";
	public static final String type_pack = "4";
	
//	public static final String ActionType = "type";
	
	public static final String addr_manage = "5";
	public static final String addr_sel = "6";
	
	public static final String INTENT_ADDR = "addr";
	public static final String INTENT_GOODS_ID = "goods_id";
	public static final String INTENT_ORDER_ID = "order_id";
    public static final String INTENT_ADS = "ads";

	public static final String ACTION_FORM_ORDER = "from_order";
	//测试的时候10个数据  真实的时候可以用到15个数据 Log只能打印10个量的数据
	public static final String DEFAULT_LIMIT = "15";
	

	public static final int ORDER_CHANGED = 7;

	public static final String leiXing_numbe ="leiXing_numbe";//选择商品的类型是第几个
	public static final int dianPu_numbe = 7;//选择商品的店铺代号	
}

```
> ## <h1 id="0502">配置模块build.gradle(Module:app)</h1>  

## [返回目录](#01)

```
apply plugin: 'com.android.application'

android {
    compileSdkVersion 22
    buildToolsVersion "22.0.1"

    defaultConfig {
        applicationId "codewarehouse.yzkj.com.ceshi"
        minSdkVersion 15
        targetSdkVersion 22
        versionCode 1
        versionName "1.0"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }

    //配置自定义打包名称  这个也是必须加上的
    repositories {
        flatDir {
            dirs 'libs'
        }
    }

    //配置自定义打包名称
    applicationVariants.all { variant ->
        variant.outputs.each { output ->
            def outputFile = output.outputFile
            def fileName
            if (outputFile != null && outputFile.name.endsWith('.apk')) {
                if (variant.buildType.name.equals('release')) {
                    variant.mergedFlavor.versionName = getVersionName()
                    //fileName = "XXXX_${variant.mergedFlavor.versionName}_release.apk"
                    fileName = "GasVerv100r001b170630.apk"//   让图片放开 改ip 关闭log与内存卡的log
                    //  fileName = "app-release.apk"// 内测版 让图片放开 改ip 关闭log与内存卡的log
                } else if (variant.buildType.name.equals('debug')) {
                    //variant.mergedFlavor.versionName = getVersionName()+"."+releaseTime()
                    variant.mergedFlavor.versionName = getVersionName()
                    fileName = "XXXX_${variant.mergedFlavor.versionName}_debug.apk"
                }
                output.outputFile = new File(outputFile.parent, fileName)
            }
        }
    }  //配置的部分到这里为止
}

dependencies {
    compile fileTree(include: ['*.jar'], dir: 'libs')
    compile 'com.android.support:appcompat-v7:22.1.1'
    compile files('libs/xUtils-2.6.14.jar')
    compile files('libs/andbase.jar')
    compile files('libs/universal-image-loader-1.9.3.jar')
}

```

<h1 id="0601">1. colors.xml</h1>  

[返回目录](#02)

```
建立colors文件夹 右键-New-values resource File建立

	<!-- 白色  这是白背景的颜色-->
    <color name="white">#ffffff</color>

	 <color name="primaryGreen">#33B5E5</color>
    <color name="baise">#ffffff</color>
    <color name="darkGreen">#0a7e07</color>
    <color name="accentGreen">#d0f8ce</color>
    <color name="accentPink">#E91E63</color>
    <color name="accentedPink">#FFFFFF</color>

    <color name="primaryBlue">#00BCD4</color>
    <color name="primaryDarkBlue">#0097A7</color>

    <color name="controlNormalGreen">#81C784</color>
    <color name="controlActivatedGreen">#4CAF50</color>
```
<h1 id="0602">2. dimens.xml</h1> 

[返回目录](#02) 

```
<!-- 按钮大小尺寸 -->
    <dimen name="buttonHeight">48dp</dimen>

    <!-- 按钮文本大小 -->
    <dimen name="buttonTextSize">16sp</dimen>

    <dimen name="widgetPadding">8dp</dimen>
```

<h1 id="0603">3. styles.xml</h1>  

[返回目录](#02)

```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
        <!--<style name="AppTheme" parent="android:Theme.Holo">-->
        <!-- Customize your theme here. -->
        <!--动画效果是旋转进入退出-->
        <item name="android:windowAnimationStyle">@style/ActivityAnimationRotateSlid</item>
       <!--这个是标题栏的颜色-->
        <item name="colorPrimary">@color/primaryGreen</item>
        <!--状态栏上的背景的颜色-->
        <item name="colorPrimaryDark">@color/darkGreen</item>
        <item name="colorAccent">@color/accentPink</item>
    </style>
    <!-- 自定义theme -->
    <style name="myAppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
        <item name="colorPrimary">#aa6633</item>
        <item name="colorPrimaryDark">#669933</item>
        <item name="colorAccent">#99cc99</item>
    </style>
    <!-- 自定义theme -->
    <style name="myAppTheme2" parent="Theme.AppCompat.Light.DarkActionBar">
        <item name="colorPrimary">#cc3366</item>
        <item name="colorPrimaryDark">#009999</item>
        <item name="colorAccent">#cccc00</item>
    </style>


    <!-- 窗口进入和退出效果 -->
    <style name="WindowPopupAnimation">
        <item name="android:windowEnterAnimation">@android:anim/slide_in_left</item>
        <item name="android:windowExitAnimation">@android:anim/slide_out_right</item>
    </style>

    <!-- activity转场动画 - 下方滑入滑出 -->
    <style name="ActivityAnimationBottom" parent="@android:style/Animation.Activity">
        <!-- activity2进入 -->
        <item name="android:activityOpenEnterAnimation">@anim/slide_bottom_in</item>
        <!-- activity1退出 -->
        <item name="android:activityOpenExitAnimation">@anim/retain</item>
        <!-- activity1返回进入 -->
        <item name="android:activityCloseEnterAnimation">@anim/retain</item>
        <!-- activity2在activity1返回后退出 -->
        <item name="android:activityCloseExitAnimation">@anim/slide_bottom_out</item>
    </style>

    <!-- activity转场动画 - 旋转进入退出 -->
    <style name="ActivityAnimationRotate" parent="@android:style/Animation.Activity">
        <item name="android:activityOpenEnterAnimation">@anim/activity_open_enter</item>
        <item name="android:activityOpenExitAnimation">@anim/activity_open_exit</item>
        <item name="android:activityCloseEnterAnimation">@anim/activity_close_enter</item>
        <item name="android:activityCloseExitAnimation">@anim/activity_close_exit</item>
    </style>

    <!-- activity转场动画 - 左右侧滑入滑出 -->
    <style name="ActivityAnimationRotateSlid" parent="@android:style/Animation.Activity">
        <item name="android:activityOpenEnterAnimation">@anim/in_from_left</item>
        <item name="android:activityOpenExitAnimation">@anim/out_from_right</item>
        <item name="android:activityCloseEnterAnimation">@anim/in_from_right</item>
        <item name="android:activityCloseExitAnimation">@anim/out_from_left</item>
    </style>
    <!-- Widget Styles 按钮的样式  使用方法  style="@style/MenuButton" -->
    <style name="MenuButton" parent="android:Widget.Button">
        <item name="android:minHeight">@dimen/buttonHeight</item>
        <item name="android:textSize">@dimen/buttonTextSize</item>
        <item name="android:textColor">@drawable/text_color_button</item>
        <item name="android:background">@drawable/background_button</item>
        <item name="android:layout_margin">5dp</item>
    </style>
</resources>
```
<h1 id="0604">4. drawable下的xml资源</h1>  

[返回目录](#02)

```
文字 颜色选择器
text_color_button.xml

<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <!-- 按下时的文本颜色 -->
    <item android:state_pressed="true" android:color="@color/accentedPink" />
    <!-- 默认的文本颜色 -->
    <item android:color="@color/accentPink" />
</selector>


按钮背景颜色选择器   background_button.xml

<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <!-- 按下时的颜色和背景 -->
    <item android:state_pressed="true">
        <shape android:shape="rectangle">
            <solid android:color="@color/accentPink" />
            <corners android:radius="10dp"/>
        </shape>
    </item>
    <!-- 默认的颜色和背景 -->
    <item>
        <shape android:shape="rectangle">
             <solid android:color="@color/primaryBlue" />
        </shape>
    </item>
</selector>

```
<h1 id="0605">5. layout文件夹下的xml资源</h1> 

[返回目录](#02) 

```
占位符
```
<h1 id="0606">6. 动画</h1> 

[返回目录](#02) 

```
从代码的角度去加载动画
<?xml version="1.0" encoding="utf-8"?>
<translate xmlns:android="http://schemas.android.com/apk/res/android"
    android:duration="300"
    android:fromXDelta="0"
    android:fromYDelta="0"
    android:toXDelta="-1000"
    android:toYDelta="0" />

 /**
         * 删除item动画
         * @param index
         * @param v
         */
        private void del(final int index, View v){
            final Animation animation = (Animation) AnimationUtils.loadAnimation(v.getContext(), R.anim.list_anim);

            animation.setAnimationListener(new Animation.AnimationListener() {
                public void onAnimationStart(Animation animation) {}
                public void onAnimationRepeat(Animation animation) {}
                public void onAnimationEnd(Animation animation) {
                    LogTxt.writeLog("", String.valueOf(index) + "个普通的配送员被删除了");
                    String id=data.get(index).getId();                   
                    animation.cancel();
                }
            });//监听的方法到此为止

            v.startAnimation(animation);
        }


从xml的方法去加载动画
 <ImageView
            android:id="@+id/xlistview_header_progressbar"
            android:layout_width="34dp"
            android:layout_height="34dp"
            android:layout_centerVertical="true"
            android:layout_marginLeft="-55dp"
            android:visibility="gone"
            android:layout_alignLeft="@id/xlistview_header_text"
            android:layout_marginRight="10dip"
            android:src="@drawable/bga_refresh_loding"/>


<?xml version="1.0" encoding="utf-8"?>
<animation-list xmlns:android="http://schemas.android.com/apk/res/android"
    android:oneshot="false" >

    <item
        android:drawable="@mipmap/bga_refresh_loading01"
        android:duration="100"/>
    <item
        android:drawable="@mipmap/bga_refresh_loading02"
        android:duration="100"/>
    <item
        android:drawable="@mipmap/bga_refresh_loading03"
        android:duration="100"/>
    <item
        android:drawable="@mipmap/bga_refresh_loading04"
        android:duration="100"/>
    <item
        android:drawable="@mipmap/bga_refresh_loading05"
        android:duration="100"/>
    <item
        android:drawable="@mipmap/bga_refresh_loading06"
        android:duration="100"/>
    <item
        android:drawable="@mipmap/bga_refresh_loading07"
        android:duration="100"/>
    <item
        android:drawable="@mipmap/bga_refresh_loading08"
        android:duration="100"/>
    <item
        android:drawable="@mipmap/bga_refresh_loading09"
        android:duration="100"/>
    <item
        android:drawable="@mipmap/bga_refresh_loading10"
        android:duration="100"/>
    <item
        android:drawable="@mipmap/bga_refresh_loading11"
        android:duration="100"/>
    <item
        android:drawable="@mipmap/bga_refresh_loading12"
        android:duration="100"/>

</animation-list>
```
<h1 id="0607">7. arrays.xml</h1> 

[返回目录](#02) 

```
String [] array=getResources().getStringArray(R.array.list)

<?xml version="1.0" encoding="utf-8"?>
<resources>      
    <string-array name="list">
        <item>阿妹</item>
        <item>阿郎</item>
        <item>陈奕迅</item>      
        <item>~夏先生</item>
    </string-array>
</resources>
```
<h1 id="0701">1. 常用控件</h1>  

[返回目录](#02)

```

<EditText
        android:id="@+id/editPhone"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_margin="12dp"
        android:layout_marginTop="24dp"
        android:background="@drawable/border_empty_shape"
        android:drawableLeft="@drawable/ic_login_acc"
        android:hint="请输入手机号"
        />
 		android:inputType="textPassword"  输入的类型是密码形式

		//代码加入对控件的监听
		editRemark.addTextChangedListener(new TextWatcher() {
            @Override
            public void onTextChanged(CharSequence s, int start, int before, int count) {
                textCount.setText("" + (100 - editRemark.getText().length()) + "字");
            }

            @Override
            public void beforeTextChanged(CharSequence s, int start, int count, int after) {

            }

            @Override
            public void afterTextChanged(Editable s) {
            }
        });

这个是背景的图片
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android" >
    <stroke
        android:width="1dp"
        android:color="@color/lightgray" />
    <corners android:radius="4dp" />
</shape>

 <Button
        android:layout_width="match_parent"
        android:layout_height="@dimen/buttonHeight"
        android:text="  使用指南"
        android:drawableEnd="@mipmap/arrow"
        android:drawableRight="@mipmap/arrow"
        android:drawableStart="@mipmap/more"
        android:drawableLeft="@mipmap/more"
        android:paddingLeft="15dp"
        style="@style/MenuButton"
        android:id="@+id/button3"
        android:gravity="left|center_vertical"/>

 <TextView
        android:id="@+id/textForget"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="right"   这个表明该控件在布局的右侧
        android:layout_marginRight="24dp"
        android:layout_marginTop="12dp"
        android:drawableBottom="@color/app_color"
        android:text="忘记密码?"
        android:textColor="@color/app_color"
        android:textSize="18sp" />

<ListView
        android:id="@+id/listDistrict"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="12dp"
        android:background="@color/white"
        android:divider="@color/lightgrey"
        android:dividerHeight="1dp" />

相对布局
 android:layout_alignParentRight="true"
 android:layout_toLeftOf="@+id/textAddPerson"

```
![忘记密码的位置](http://i.imgur.com/Dj4bwrW.jpg)

<h1 id="0702">1. 常用布局</h1>  

[返回目录](#02)

```
这个是线性布局
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/white"
    android:orientation="vertical" >

</LinearLayout>
```

<h1 id="0801">0801. 控制台日志的打印模板</h1>  

[返回目录](#01)

```
//这个是该工具的调用
MyLog.ShowLog(json);


package com.linyou.lifeservice.utils;

import android.util.Log;

/**
 * Created by Administrator on 2016/9/27 
 * 0027.
 */
public class MyLog {
    //过滤 返回的所有数据
    private static String TAG="tanyinqing";
    //过滤 接口返回的网络相关的数据
    private static String TAG1="tanyinqingWangLuoJieKou";

    //关闭所有的Log数据的打印
    private static Boolean ifShow=true;

    public static void ShowLog(String content){
        if (ifShow){
            Log.d(TAG,content);
        }
    }
}

```

<h1 id="0802">把日志打印到内存卡上</h1>

[返回目录](#01)
```

// 前面是内容  后面是文件名  日志写到内存卡上
 LogTxt.writeLog("小谈你好","小谈测试");  


package utils;
import android.os.Environment;
import android.util.Log;

import java.io.File;
import java.io.FileOutputStream;
import java.io.OutputStream;
import java.io.OutputStreamWriter;
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.Date;

/**
 * Created by Administrator on 2016/11/6 0006.
 */
public class LogTxt {
    public static long xuhao=1;

   
    public static void writeLog(String context,String fileName){
        if (true){  //这个值该为false后就不会在打印日志了

            // String filePath = "/sdcard/Test/";
            if(!Environment.getExternalStorageState().equals(Environment.MEDIA_MOUNTED)){
//            Toast.makeText(getApplicationContext(),
//                    "没有SD卡,无法保存图像.", Toast.LENGTH_SHORT).show();
                Log.e("ImagesUtil.java", "没有SD卡,无法保存图像.");
                return ;
            }

            //文件命名的时间成分
            Calendar calendar=Calendar.getInstance();
            Date data=calendar.getTime();
            // SimpleDateFormat format=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
            SimpleDateFormat format=new SimpleDateFormat("_HH:mm:ss");
            String time=format.format(data);

            // 获得外部SD卡,创建本应用程序的保存目录,保存相片
            File sdCard = Environment.getExternalStorageDirectory();
            // File photoDir = new1 File(sdCard.getAbsolutePath() + "/mycamera");
            File photoDir = new File(sdCard.getAbsolutePath() + "/"+"LogTan");
            // MyLog.ShowLog("保存图像地址"+photoDir.getAbsolutePath());
            if(!photoDir.exists()){
                photoDir.mkdirs();
            }

        /*File photo = new1 File(photoDir,fileName+time+".txt");
        MyLog.ShowLog("创建photo文件");
*/
            // 每次写入时，都换行写
            String strContent = context + "\r\n";
            //String strContent = context;
            try {
                File file = new File(photoDir,String.valueOf(xuhao)+"_"+fileName+time+".txt");
                if (!file.exists()) {
                    //Log.d("TestFile", "Create the file:" + strFilePath);
                    file.createNewFile();
                }
           /* RandomAccessFile raf = new1 RandomAccessFile(file, "rwd");
            raf.seek(file.length());
            raf.write(strContent.getBytes());
            raf.close();*/
                OutputStream outstream = new FileOutputStream(file);
                OutputStreamWriter out = new OutputStreamWriter(outstream);
                out.write(strContent);
                if (xuhao<=10){
                    xuhao++;
                }else {
                    xuhao=1;
                    //删除缓存的Log信息 每次启动时
                    String  DATABASE_NAME="LogTan";   //数据的存储路径
                    File sdCard1 = Environment.getExternalStorageDirectory();
                    String DATABASE_PATH= sdCard1.getAbsolutePath()+"/"+DATABASE_NAME+"/";
                    File dbContentFile = new File(DATABASE_PATH);
                    Boolean tan=true;
                    if (dbContentFile.exists()) {
                        //dbContentFile.delete();
                        if (tan){
                            delete(dbContentFile);
                        }
                    }
                }

                out.close();
            } catch (Exception e) {
                Log.e("TestFile", "Error on write File:" + e);
            }
        }
    }


    //删除一个文件夹
    public static void delete(File file) {
        if (file.isFile()) {
            file.delete();
            return;
        }

        if (file.isDirectory()) {
            File[] childFiles = file.listFiles();
            if (childFiles == null || childFiles.length == 0) {
                file.delete();
                return;
            }

            for (int i = 0; i < childFiles.length; i++) {
                delete(childFiles[i]);
            }
            // file.delete(); 删除这个文件夹
        }
    }
}


```
<h1 id="0803">0803. 把连续的日志打印到内存卡的一个文件上</h1>

[返回目录](#01)

```

// 前面是内容，后面是文件名 会把日志累加起来
   LogTxtLeiJi.writeLog("3","记录推送下来的订单号");
	


package utils;

import android.os.Environment;
import android.util.Log;

import java.io.File;
import java.io.FileOutputStream;
import java.io.OutputStream;
import java.io.OutputStreamWriter;
import java.io.RandomAccessFile;
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.Date;

/**
 * Created by Administrator on 2016/11/6 0006.
 */
public class LogTxtLeiJi {
	
	
    public static void writeLog(String context,String fileName){
        if (true){  //这个值该为false后就不会在打印日志了

       // String filePath = "/sdcard/Test/";
        if(!Environment.getExternalStorageState().equals(Environment.MEDIA_MOUNTED)){
//            Toast.makeText(getApplicationContext(),
//                    "没有SD卡,无法保存图像.", Toast.LENGTH_SHORT).show();
            Log.e("ImagesUtil.java", "没有SD卡,无法保存图像.");
            return ;
        }

        //文件命名的时间成分
        Calendar calendar=Calendar.getInstance();
        Date data=calendar.getTime();
        SimpleDateFormat format=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String time=format.format(data);

        // 获得外部SD卡,创建本应用程序的保存目录,保存相片
        File sdCard = Environment.getExternalStorageDirectory();
        // File photoDir = new1 File(sdCard.getAbsolutePath() + "/mycamera");
        File photoDir = new File(sdCard.getAbsolutePath() + "/"+"LogTan");
       // MyLog.ShowLog("保存图像地址"+photoDir.getAbsolutePath());
        if(!photoDir.exists()){
            photoDir.mkdirs();
        }

        /*File photo = new1 File(photoDir,fileName+time+".txt");
        MyLog.ShowLog("创建photo文件");
*/
        // 每次写入时，都换行写
        String strContent = context +"     "+time+"\r\n";
        //String strContent = context;
        try {
           // File file = new File(photoDir,fileName+time+".txt");
            File file = new File(photoDir,fileName+".txt");
            if (!file.exists()) {
                //Log.d("TestFile", "Create the file:" + strFilePath);
                file.createNewFile();
            }
            RandomAccessFile raf = new RandomAccessFile(file, "rwd");
            // 获取文件的长度即字节数  // 将写文件指针移到文件尾
            raf.seek(file.length());
            raf.write(strContent.getBytes());
            raf.close();

           /* OutputStream outstream = new FileOutputStream(file);
            OutputStreamWriter out = new OutputStreamWriter(outstream);
            out.write(strContent);
            out.close();*/
        } catch (Exception e) {
            Log.e("TestFile", "Error on write File:" + e);
        }
        }
    }
}


```
<h1 id="0804">0804. 像素和dp和sp单位的换算</h1>

[返回目录](#01)

```
package codewarehouse.yzkj.com.ceshi;

import android.content.Context;

//   这个是将dp单位转化成像素值  用来适配布局的尺寸   DensityUtil.dip2px(this, 48)
public class DensityUtil
{
    /**
     * 将px值转换为dip或dp值，保证尺寸大小不变
     * 
     * @param pxValue
     * @param
     *            （DisplayMetrics类中属性density）
     * @return
     */
    public static int px2dip(Context context, float pxValue)
    {
        final float scale = context.getResources().getDisplayMetrics().density;
        return (int) (pxValue / scale + 0.5f);
    }
    
    /**
     * 将dip或dp值转换为px值，保证尺寸大小不变
     * 
     * @param dipValue
     * @param
     *            （DisplayMetrics类中属性density）
     * @return
     */
    public static int dip2px(Context context, float dipValue)
    {
        final float scale = context.getResources().getDisplayMetrics().density;
        return (int) (dipValue * scale + 0.5f);
    }
    
    /**
     * 将px值转换为sp值，保证文字大小不变
     * 
     * @param pxValue
     * @param
     *            （DisplayMetrics类中属性scaledDensity）
     * @return
     */
    public static int px2sp(Context context, float pxValue)
    {
        final float fontScale = context.getResources().getDisplayMetrics().scaledDensity;
        return (int) (pxValue / fontScale + 0.5f);
    }
    
    /**
     * 将sp值转换为px值，保证文字大小不变
     * 
     * @param spValue
     * @param
     *            （DisplayMetrics类中属性scaledDensity）
     * @return
     */
    public static int sp2px(Context context, float spValue)
    {
        final float fontScale = context.getResources().getDisplayMetrics().scaledDensity;
        return (int) (spValue * fontScale + 0.5f);
    }
}
```
<h1 id="0805">0805. 对象和Json字符串的相互转化</h1>

[返回目录](#01)

```
package codewarehouse.yzkj.com.ceshi;

import com.google.gson.Gson;
/**
 * 对象和Json字符串的相互转化
 */
public class JsonUtil<T> {

	public Object convertJsonToObject(String value,Class<T> object){
		Object resultObject = new Object();
		Gson gson = new Gson();
		resultObject = gson.fromJson(value, object);
		return resultObject;
	}

	//使用Gson将JSON字符串转换为Java对象
	public static Object convertJsonToObject(String value){
		Object resultObject = new Object();
		Gson gson = new Gson();
		resultObject = gson.fromJson(value, Object.class);
		return resultObject;
	}
	
	//使用Gson将Java对象转换为JSON字符串
	public static String convertObjectToJson(Object obj){
		String result = "";
		Gson gson = new Gson();
		result = gson.toJson(obj);
		return result;
	}
}

```
<h1 id="0806">0806. 日期APi的工具类</h1>

[返回目录](#01)

```
package codewarehouse.yzkj.com.ceshi;

import java.text.DateFormat;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.Date;

import android.annotation.SuppressLint;
import android.text.format.Time;
import android.util.Log;

@SuppressLint("SimpleDateFormat")
@SuppressWarnings("static-access")
public class DateUtil {
	public static final String DATE_ALL_ALL = "yyyy-MM-dd HH:mm:ss";
	public static final String YEAR_MONTH_DAY = "yyyy-MM-dd";
	public static final String YEAR_MONTH = "yyyy-MM";
	public static final String DATE_ALL = "yyyy-MM-dd HH:mm";
	public static final String DATE_TIME = "MM-dd HH:mm";
	public static final String DATE_HOUR_MINUTE = "HH:mm";
	public static final String DATE_HOUR_MINUTE_SEC = "HH:mm:ss";
	  public static final long DAY_MILLIS = 86400000L;  //一天有多少秒
	public static final long WEEK_MILLIS = 604800000L;   //一周有多少秒
	//只有最后一位表明L 表明数据类型
  public static final long MONTH_MILLIS = 2592000000L;  //一月有多少秒

	/**
	 * 某月的天数
	 */
	private static int daysOfMonth = 0;

	/**
	 * 判断是否为闰年
	 * 
	 * @param year
	 *            指定的年份
	 * @return
	 */
	public static boolean isLeapYear(int year) {
		if (year % 100 == 0 && year % 400 == 0) {
			return true;
		} else if (year % 100 != 0 && year % 4 == 0) {
			return true;
		}
		return false;
	}

	/**
	 * 获取当前日期   用指定的格式来显示
	 * 
	 * @return
	 */

	public static String getNowDate(String dateFormat) {
		SimpleDateFormat sDateFormat = new SimpleDateFormat(dateFormat);

		return sDateFormat.format(new Date());
	}

	/**
	 * 得到某月有多少天数
	 * 
	 * @param year
	 *            目标年份
	 * @param month
	 *            目标月份
	 * @return
	 */
	public static int getDaysOfMonth(int year, int month) {
		switch (month) {
		case 1:
		case 3:
		case 5:
		case 7:
		case 8:
		case 10:
		case 12:
			daysOfMonth = 31;
			break;
		case 4:
		case 6:
		case 9:
		case 11:
			daysOfMonth = 30;
			break;
		case 2:
			if (isLeapYear(year)) {  //判断是否为闰年
				daysOfMonth = 29;
			} else {
				daysOfMonth = 28;
			}

		}
		return daysOfMonth;
	}

	private final static ThreadLocal<SimpleDateFormat> dateFormater2 = new ThreadLocal<SimpleDateFormat>() {
		@Override
		protected SimpleDateFormat initialValue() {
			return new SimpleDateFormat("yyyy-MM-dd");
		}
	};

	//将指定的时间 以指定的格式进行格式化成字符串
	public static String stringFromDate(Date date, String formatString) {
		DateFormat df = new SimpleDateFormat(formatString);
		return df.format(date);
	}

	//将指定的字符串格式的日期转换成时间对象
	public static Date dateFromString(String dateStr, String formatString) {
		DateFormat df = new SimpleDateFormat(formatString);
		Date date = null;

		try {
			date = df.parse(dateStr);
		} catch (ParseException e) {
			//Log.i("dateFromString exception:", Log.getStackTraceString(e));
			LogTxt.writeLog(Log.getStackTraceString(e),"dateFromString exception:");
		}
		return date;
	}

	//指定的时间 推迟多少天后的日期
	public static Date addDateOfDay(Date date, int addDay) {
		Calendar calendar = Calendar.getInstance();
		calendar.setTime(date);
		calendar.add(Calendar.DAY_OF_YEAR, addDay);
		Date d = calendar.getTime();

		return d;
	}

	//指定的时间 推迟多少月后的日期 例如现在是2017-05-30 11:00:34
	// 推迟4天后是 2017-06-03 11:02:08  不过得出的是手机上的时间
	public static Date addDateOfMonth(Date date, int addMonth) {
		Calendar calendar = Calendar.getInstance();
		calendar.setTime(date);
		calendar.add(Calendar.MONTH, addMonth);
		Date d = calendar.getTime();

		return d;
	}

	//返回现在的时间的时间码   格式为Long型  例如：1496121576992
	/*System.currentTimeMillis()产生一个当前的毫秒，这个毫秒其实就是自1970年1月1日0时起的毫秒数，*/
	public static long getNowTimeInMillis() {
		Calendar nowCalendar = Calendar.getInstance();
		nowCalendar.getTimeInMillis();
		
		return System.currentTimeMillis();
	}

	//返回当前天是当前月份的第多少天
	public static int getTadayOfMonth() {
		Calendar cal = Calendar.getInstance();
		return cal.get(Calendar.DAY_OF_MONTH);
	}

	//将Long型时间转化为小时 分钟  秒的形式 例如：415589:19:36
	@SuppressLint("DefaultLocale")
	public static String getStringUseTime(long useTime) {
		int sec = 0;
		int minute = 0;
		int hour = 0;
		String timeText = "";
		//这个是转化成秒值
		sec = (int) (useTime / 1000);
		minute = sec / 60;
		hour = minute / 60;
		timeText = String.format("%02d:%02d:%02d", hour, minute % 60, sec % 60);
		return timeText;
	}

	/**
	 * 以友好的方式显示时间  DATE_ALL = "yyyy-MM-dd HH:mm";
	 * 和现在的时间比较，超过24小时是前天，24小时以内是昨天
	 * 给出的时间和现在的时间相比   是几小时前  或前天  昨天 例如：2017-05-30 06:08  是 8小时前
	 * @param sdate
	 * @return
	 */
	public static String friendly_time(String sdate) {
		Date time = dateFromString(sdate, DATE_ALL);  //将指定的字符串格式的日期转换成时间对象
		if (time == null) {
			return "Unknown";
		}
		String ftime = "";
		Calendar cal = Calendar.getInstance();

		// 判断是否是同一天
		String curDate = dateFormater2.get().format(cal.getTime());
		String paramDate = dateFormater2.get().format(time);
		
		if (curDate.equals(paramDate)) {//表明是同一天
			int hour = (int) ((cal.getTimeInMillis() - time.getTime()) / 3600000);
			if (hour == 0)
				ftime = Math.max(  //两者取最大值
						(cal.getTimeInMillis() - time.getTime()) / 60000, 1)
						+ "分钟前";
			else
				ftime = hour + "小时前";
			return ftime;
		}

		long lt = time.getTime() / 86400000;
		long ct = cal.getTimeInMillis() / 86400000;
		int days = (int) (ct - lt);
		if (days == 0) {
			int hour = (int) ((cal.getTimeInMillis() - time.getTime()) / 3600000);
			if (hour == 0)
				ftime = Math.max(
						(cal.getTimeInMillis() - time.getTime()) / 60000, 1)
						+ "分钟前";
			else
				ftime = hour + "小时前";
		} else if (days == 1) {
			ftime = "昨天";
		} else if (days == 2) {
			ftime = "前天";
		} else if (days > 2 && days <= 10) {
			ftime = days + "天前";
		} else if (days > 10) { //这个是大于10天的情形
			ftime = dateFormater2.get().format(time);
		}
		return ftime;
	}

	/**
	 * 判断给定字符串时间是否为今日
	 * 
	 * @param sdate
	 * @return boolean
	 */
	public static boolean isToday(String sdate) {
		boolean b = false;
		Date time = dateFromString(sdate, DATE_ALL);  //将指定的字符串格式的日期转换成时间对象
		Date today = new Date();
		if (time != null) {
			String nowDate = dateFormater2.get().format(today);
			String timeDate = dateFormater2.get().format(time);
			if (nowDate.equals(timeDate)) {
				b = true;
			}
		}
		return b;
	}

	//获取到今年
	public static int getThisYear() {
		Calendar cal = Calendar.getInstance();
		return cal.get(Calendar.YEAR);
	}

	//获取到当月 这个月份需要加 1
	public static int getThisMonth() {
		Calendar cal = Calendar.getInstance();
		return cal.get(Calendar.MONTH);
	}

	//获取到当日的信息
	public static int getThisDay() {
		Calendar cal = Calendar.getInstance();
		return cal.get(Calendar.DAY_OF_MONTH);
	}
	
	
	//得到现在是周几
	public static int getThisWeek() {
		Calendar cal = Calendar.getInstance();
		return cal.get(Calendar.DAY_OF_WEEK) - 1;
	}

	//判断现在的时间是今年的第几周  全年是52周
	// 测试的语句  MyLog.ShowLog(String.valueOf(DateUtil.getWeekOfYear(DateUtil.getNowTimeInMillis())));
	public static int getWeekOfYear(long times) {
		Calendar mCal = Calendar.getInstance();
		mCal.setFirstDayOfWeek(Calendar.MONDAY);
		mCal.setTimeInMillis(times);
		return mCal.get(Calendar.WEEK_OF_YEAR);
	}

	//获得本周日的时间的毫秒值   得到现在是周几减1才是东方的时间，国际上是星期天为一周第一天
	// dayOfMonth + (7 - (dayOfWeek - 1))  30+(7-(3-1)))=35  也就是当前天比周日少5天
	public static long getThisWeekOfSunday() {
		Calendar cal = Calendar.getInstance();
		int dayOfWeek = cal.get(Calendar.DAY_OF_WEEK);
		int dayOfMonth = cal.get(Calendar.DAY_OF_MONTH);
		int year = cal.get(Calendar.YEAR);
		int month = cal.get(Calendar.MONTH);
		cal.set(year, month, dayOfMonth + (7 - (dayOfWeek - 1)),23,59,59);
		return cal.getTimeInMillis();
	}

	// MyLog.ShowLog(DateUtil.longToString(DateUtil.getThisWeekOfMonday())); 测试的代码
	//获得本周一的时间戳
//	System.out.println(cal.get(Calendar.DAY_OF_MONTH)); //输出当前日期对象cal是当前月份的第几天
//	dayOfMonth - (dayOfWeek - 2)  30-(3-2)=29  也就是第29天使周一  当前天比周一多2天
	public static long getThisWeekOfMonday() {
		Calendar cal = Calendar.getInstance();
		int dayOfWeek = cal.get(Calendar.DAY_OF_WEEK);
		int dayOfMonth = cal.get(Calendar.DAY_OF_MONTH);
		int year = cal.get(Calendar.YEAR);
		int month = cal.get(Calendar.MONTH);
		cal.set(year, month, dayOfMonth - (dayOfWeek - 2),0,0,0);
		return cal.getTimeInMillis();
	}

	//得到年份的值  android.text.format.Time包中的Time类是android平台的一个时间类，但是这个类目前已经不建议使用了
	public static int longTimeToYear(long times) {
		Time mTime = new Time();
		mTime.set(times);
		return mTime.year;
	}
	//得到月份的值
	public static int longTimeToMonth(long times) {
		Time mTime = new Time();
		mTime.set(times);
		return mTime.month;
	}

	//获得beforeOfMonth个月前那个月的第一天  0表示当月的第一天，例如 2017-07-01 00:00:00
	public static long getLongOfFirstDayOfMonth(int beforeOfMonth) {
		Calendar localCalendar = Calendar.getInstance();
		int latestMonth = localCalendar.get(Calendar.MONTH);
		localCalendar.set(localCalendar.MONTH, latestMonth - beforeOfMonth);
		//获取月中的最小值
		int latestDay = localCalendar.getActualMinimum(Calendar.DAY_OF_MONTH);
		
		localCalendar.set(localCalendar.DATE, latestDay);
		localCalendar.set(localCalendar.HOUR, 0);
		localCalendar.set(localCalendar.MINUTE, 0);
		localCalendar.set(localCalendar.SECOND, 0);
		localCalendar.set(localCalendar.MILLISECOND, 0);
		return localCalendar.getTimeInMillis();
	}

	//获得beforeOfMonth月前的最后一天  0为当月 2017-07-31 00:00:00
	public static long getLongOfLatestDayOfMonth(int beforeOfMonth) {

		Calendar localCalendar = Calendar.getInstance();
		int latestMonth = localCalendar.get(Calendar.MONTH);
		localCalendar.set(localCalendar.MONTH, latestMonth - beforeOfMonth);
		int latestDay = localCalendar.getActualMaximum(Calendar.DAY_OF_MONTH);
		localCalendar.set(localCalendar.DATE, latestDay);
		localCalendar.set(localCalendar.HOUR, 0);
		localCalendar.set(localCalendar.MINUTE, 0);
		localCalendar.set(localCalendar.SECOND, 0);
		localCalendar.set(localCalendar.MILLISECOND, 0);
		return localCalendar.getTimeInMillis();
	}

	// 通过string 指定  hh：ss  时间      获取long型时间码
	public static long getLongOfTime(String time) {
		int hour = Integer.valueOf(time.substring(0, 2));
		int min = Integer.valueOf(time.substring(3, 5));
		Calendar calendar = Calendar.getInstance();
		calendar.set(calendar.HOUR_OF_DAY, hour);//get 和 set 的字段数字，指示一天中的小时。
		calendar.set(calendar.MINUTE, min);// get 和 set 的字段数字，指示一小时中的分钟。
		calendar.set(Calendar.SECOND, 0);       //get 和 set 的字段数字，指示一分钟中的秒。
		calendar.set(Calendar.MILLISECOND, 0); //get 和 set 的字段数字，指示一秒中的毫秒。
		return calendar.getTimeInMillis();
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
	
	// 通过string yyyy-mm-dd, time    时间获取时间码
	public static long getLongOfDayTimeAll(String date, String time) {
		//依次获得年月日 时分秒 转换成时间的毫秒值
		int year = Integer.valueOf(date.substring(0, 4));
		int month = Integer.valueOf(date.substring(5, 7));
		int day = Integer.valueOf(date.substring(8, 10));
		
		int hour = Integer.valueOf(time.substring(0, 2));
		int min = Integer.valueOf(time.substring(3, 5));
		
		Calendar calendar = Calendar.getInstance();
		calendar.set(calendar.YEAR, year);
		calendar.set(calendar.MONTH, month - 1);
		calendar.set(calendar.DAY_OF_MONTH, day);
		calendar.set(calendar.HOUR_OF_DAY, hour);
		calendar.set(calendar.MINUTE, min);
		calendar.set(Calendar.SECOND, 0);           
		calendar.set(Calendar.MILLISECOND, 0);
		return calendar.getTimeInMillis();
	}
	
	//将字符串时间转化为星期几   2017:07:03
	public static int getTimeForWeek(String time){
		int year = Integer.valueOf(time.substring(0, 4));
		int month = Integer.valueOf(time.substring(5, 7));
		int day = Integer.valueOf(time.substring(8, 10));
		Calendar calendar = Calendar.getInstance();
		calendar.set(calendar.YEAR, year);
		calendar.set(calendar.MONTH, month-1);
		calendar.set(calendar.DAY_OF_MONTH, day);
		return calendar.get(Calendar.DAY_OF_WEEK)-1;
	}

	//将毫秒值转化成 字符串时间
	public static String longToString(long time){
		Calendar nowCalendar = Calendar.getInstance();
		nowCalendar.setTimeInMillis(time);
		//Calendar和Date的相互转化
		Date d = nowCalendar.getTime();
		SimpleDateFormat sDateFormat = new SimpleDateFormat(DateUtil.DATE_ALL_ALL);
		return sDateFormat.format(d);
	}
}


```
<h1 id="0807">7. 缓存数据的工具类</h1>

[返回目录](#01)

```
这个是进行初始化
public static PreferenceUtil mPrefUtil;  //用于配制信息的业务类  继成了各种方法
 mPrefUtil = new PreferenceUtil(this, Constant.prefName, Context.MODE_PRIVATE);


package com.linyou.lifedelivery.activity.utils;

import android.content.Context;
import android.content.SharedPreferences;
import android.content.SharedPreferences.Editor;
import android.text.TextUtils;

import com.linyou.lifedelivery.activity.Constant;

import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.io.StreamCorruptedException;
import java.util.HashMap;
import java.util.Iterator;

/**
 * 
 * 配置存储工具类
 * 
 * @author zeroangus
 * 
 */
public class PreferenceUtil {

	private SharedPreferences preferences;

	public PreferenceUtil(Context context, String name, int Mode) {
		preferences = context.getSharedPreferences(name, Mode);
	}


	//是否是第一次使用
	public static boolean getFirstUse(Context context) {
		SharedPreferences settings = context.getSharedPreferences(
				Constant.prefName, Context.MODE_PRIVATE);
		return settings.getBoolean("firstUse", true);
		//return true;
	}

	/**
	 * 保存对象  将对象序列化后再转化为16进制的字符串保存
	 * @param key
	 * @param value
	 */
	public void putSetting(String key, Object value) {
		Editor editor = preferences.edit();
		try {
			ByteArrayOutputStream baos = new ByteArrayOutputStream();
			ObjectOutputStream oos = new ObjectOutputStream(baos);
			oos.writeObject(value);
			// 将序列化的数据转为16进制保存
			String value2 = bytesToHexString(baos.toByteArray());
			editor.putString(key, value2);
			editor.commit();
		} catch (Exception e) {
			System.out.println("putSetting ----> "+e.toString());
		}
	}

	/**
	 * desc:将数组转为16进制  将数组转化为字符串
	 * 
	 * @param bArray
	 * @return modified:
	 */
	public static String bytesToHexString(byte[] bArray) {
		if (bArray == null) {
			return null;
		}
		if (bArray.length == 0) {
			return "";
		}
		StringBuffer sb = new StringBuffer(bArray.length);
		String sTemp;
		for (int i = 0; i < bArray.length; i++) {
			sTemp = Integer.toHexString(0xFF & bArray[i]);
			if (sTemp.length() < 2)
				sb.append(0);
			sb.append(sTemp.toUpperCase());
		}
		return sb.toString();
	}

	/**
	 * desc:获取保存的Object对象
	 * 
	 * @param key
	 * @return modified:
	 */
	public Object readObject(String key) {
		try {
			if (preferences.contains(key)) {
				System.out.println("配置信息preferences.contains -------------> " + key);
				String string = preferences.getString(key, "");
				if (TextUtils.isEmpty(string)) {

					System.out.println( key + "配置信息 -----> is empty"  );
					return null;
				} else {

					System.out.println( key + " 配置信息-----> is not empty"  );
					// 将16进制的数据转为数组，准备反序列化
					byte[] stringToBytes = StringToBytes(string);
					ByteArrayInputStream bis = new ByteArrayInputStream(
							stringToBytes);
					ObjectInputStream is = new ObjectInputStream(bis);
					// 返回反序列化得到的对象
					Object readObject = is.readObject();
					return readObject;
				}
			}
		} catch (StreamCorruptedException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (ClassNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		// 所有异常返回null
		return null;

	}

	/**
	 * desc:将16进制的数据转为数组  也就是把字符串转化为数组 一个单词一个组
	 * <p>
	 * 创建人：聂旭阳 , 2014-5-25 上午11:08:33
	 * </p>
	 * 
	 * @param data
	 * @return modified:
	 */
	public static byte[] StringToBytes(String data) {
		String hexString = data.toUpperCase().trim();
		if (hexString.length() % 2 != 0) {
			return null;
		}
		byte[] retData = new byte[hexString.length() / 2];
		for (int i = 0; i < hexString.length(); i++) {
			int int_ch; // 两位16进制数转化后的10进制数
			char hex_char1 = hexString.charAt(i); // //两位16进制数中的第一位(高位*16)
			int int_ch1;
			if (hex_char1 >= '0' && hex_char1 <= '9')
				int_ch1 = (hex_char1 - 48) * 16; // // 0 的Ascll - 48
			else if (hex_char1 >= 'A' && hex_char1 <= 'F')
				int_ch1 = (hex_char1 - 55) * 16; // // A 的Ascll - 65
			else
				return null;
			i++;
			char hex_char2 = hexString.charAt(i); // /两位16进制数中的第二位(低位)
			int int_ch2;
			if (hex_char2 >= '0' && hex_char2 <= '9')
				int_ch2 = (hex_char2 - 48); // // 0 的Ascll - 48
			else if (hex_char2 >= 'A' && hex_char2 <= 'F')
				int_ch2 = hex_char2 - 55; // // A 的Ascll - 65
			else
				return null;
			int_ch = int_ch1 + int_ch2;
			retData[i / 2] = (byte) int_ch;// 将转化后的数放入Byte里
		}
		return retData;
	}

	/**
	 * 
	 * 插入单个配置信息（string,string）
	 * 
	 * @param key
	 * @param value
	 */
	public void putSetting(String key, String value) {
		Editor editor = preferences.edit();
		editor.putString(key, value);
		editor.commit();
	}

	/**
	 * 
	 * 插入单个配置信息（string,int）
	 * 
	 * @param key
	 * @param value
	 */
	public void putSetting(String key, int value) {
		Editor editor = preferences.edit();
		editor.putInt(key, value);
		editor.commit();
	}

	/**
	 * 插入单个配置信息（string,boolean）
	 * 
	 * @param key
	 * @param value
	 */
	public void putSetting(String key, Boolean value) {

		Editor editor = preferences.edit();
		editor.putBoolean(key, value);
		editor.commit();
	}

	/**
	 * 
	 * 插入多个配置信息
	 * Java学习之Iterator(迭代器)的一般用法 （转）
	 * @param params
	 */
	public void putSettings(HashMap<String, Object> params) {
		Editor editor = preferences.edit();
		Iterator<String> iter = params.keySet().iterator();
		while (iter.hasNext()) {
			String name = (String) iter.next();
			if (params.get(name).getClass() == Boolean.class) {
				editor.putBoolean(name, (Boolean) params.get(name));
			} else {
				editor.putString(name, (String) params.get(name));
			}
		}
		editor.commit();
	}

	/**
	 * 缺省返回-1
	 * 
	 * @param key
	 * @return
	 */
	public int getIntSetting(String key) {
		return preferences.getInt(key, -1);
	}

	/**
	 * 缺省返回null
	 * 
	 * @param key
	 * @return
	 */
	public String getStrSetting(String key) {
		return preferences.getString(key, null);
	}

	/**
	 * 缺省返回false
	 * 
	 * @param key
	 * @return
	 */
	public boolean getBoolean(String key) {
		return preferences.getBoolean(key, false);
	}

}

```

<h1 id="0808">8. 按钮加入 3次点击的监听</h1>

[返回目录](#01)

```
mImgeTitle.setOnClickListener(new  View.OnClickListener() {
			  //需要监听几次点击事件数组的长度就为几
			  //如果要监听双击事件则数组长度为2，如果要监听3次连续点击事件则数组长度为3...
			  long[] mHints = new long[3];//初始全部为0

			  @Override
			  public void onClick(View v) {
				  //将mHints数组内的所有元素左移一个位置
				  System.arraycopy(mHints, 1, mHints, 0,
						  mHints.length - 1);
				  //获得当前系统已经启动的时间
				  mHints[mHints.length - 1] =SystemClock.uptimeMillis();
				  if (SystemClock.uptimeMillis() - mHints[0] <= 500) {
					  mPrefUtil.putSetting("isLog", true);
					  PublicUtil.ShowToast("3次点击设置成功");
				  }
			  }
		  });
```
<h1 id="0901">代码上传</h1>
 
[返回目录](#02)

[配置exlipce的版本控制](https://tanyinqing.gitbooks.io/xiangmujingyan/content/pei_zhi_eclipse_de_ban_ben_kong_zhi.html)

```java 
C:\Users\Administrator   目录下设置 .gitconfig
idea与studio的设置是

[user]
 name = tan**qing
 email = 28***7@qq.com

exlipce的设置是
url = git@github.com:yanzi1225627/TestHello_git.git 
要提前写上去，否则不容易生效
注意：那个url地址是你在github上建库的ssh地址

[core]
 repositoryformatversion = 0
 filemode = false
 bare = false
 logallrefupdates = true
 symlinks = false
 ignorecase = true
 hideDotFiles = dotGitOnly
[remote "origin"]
 url = "" 

fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
 remote = origin
 merge = refs/heads/master
[user]
 name = tan**qing
 email = 28***7@qq.com

```
七、在push之前记得先pull一下，把github上的仓库先pull到本地仓库。这个跟前面讲TortoiseGit时，新建一个文件夹然后第一步gitclone，从功能上讲是同样的作用。就把github上的代码同步到本地，同步完后可以看到本地仓库里多了两个文件，这都是github新建仓库时生成的。如果不pull就push，会报错只能用强推覆盖掉本地和github仓库上不一样的文件。在git命令里是加参数-f,在egit这个图像界面里是在push时选择 force update，但不建议这么干

要先在github上建立一个库，先pull，pull时用的网址是https://github.com/tanyinqing/AndBaseDemo.git，HTTPS网址，在push时也可以用HTTPS网址.

#注意的问题

   如果是首次提交会第一步：先在本地建立一个一样的仓库，称本地仓库。

第二步：在本地进行commit操作将把更新提交到本地仓库；
 第三步： 将服务器端的更新pull到本地仓库进行合并，最后将合并好的本地仓库push到服务器端，这样就进行了一次远程提交。

  如果非首次提交同样的道理
 第一步：将修改的代码commit操作更新到本地仓库；
第二步：第三步： 将服务器端的更新pull到本地仓库进行合并，最后将合并好的本地仓库push到服务器端

confim following expected push result
确认后的预期推动的结果(第二次刷新结果时出现)
出现的原因是，本地的和服务端的有冲突，应该先pull，在push就可以了。没有办法一同提交和上传。
apk至所以push不上去，是因为.gitignore中屏蔽了。

.gitconfig应用的技巧是用EditPlus打开，随时更改url。

换一个项目一定要改一次url

<h1 id="0902">git项目网址</h1>
 
[返回目录](#02)

[AndBaseDemo 实例以及最新apk](https://github.com/tanyinqing/AndBaseDemo)
[AndBase AndBaseDemo使用的库](https://github.com/tanyinqing/AndBase)
[]()
[]()
[]()
[]()

