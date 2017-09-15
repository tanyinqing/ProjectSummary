 # 2017 08 17
>  [文档地址](http://pan.baidu.com/disk/home?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&#list/vmode=list&path=%2F%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6%E5%A4%B9%2F%E5%AE%89%E5%8D%93%E9%A1%B9%E7%9B%AE%E4%BB%A3%E7%A0%81%E4%BB%93%E5%BA%93%2FMarkDown%E5%BC%80%E5%8F%91%E6%96%87%E6%A1%A3 "查看")→[源文件相关](http://pan.baidu.com/disk/home?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&#list/vmode=list&path=%2F%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6%E5%A4%B9%2F%E9%A1%B9%E7%9B%AE%E6%A8%A1%E5%9D%97%2FAndBaseDemo%E6%A1%86%E6%9E%B6 "查看")→[首页](https://tanyinqing.github.io/)

<h1 id="1">目录1</h1> 

* ### 1应用和环境→
* ### 2界面编程→
* ### 3事件处理→[基于监听的事件处理](#0301)→[基于回调的事件处理](#0302)→[相应系统设置的事件和响应系统设置的更改](#0303)→[Handler消息传递机制](#0304)→[异步任务](#0305)
* ### 4Activity与Fragment→[Activity](#0401)→[Fragment](#0402)
* ### 5意图和意图过滤器通信→
* ### 6资源→
* ### 7图形与图像处理→[使用简单图片](#0701)→[绘图](#0702)→[图形特效处理](#0703)→[逐帧动画](#0704)→[补间动画](#0705)

<h1 id="2">目录2</h1>  

* ### 8数据存储与io→
* ### 9ContentProvider实现数据共享→[ContentProvider](#0901)
* ### 10 服务与广播→[绑定服务并通信](#1001)→[IntentService](#1002)→[电话管理器](#1003)→[短信管理器](#1004)→[音频管理器](#1005)→[振动管理器](#1006)→[手机闹钟服务](#1007)→[接受广播服务](#1008)→[接受系统广播](#1009)


* ### 11多媒体应用开发→
* ### 12 OpenGL与3D开发→
* ### 13 网络应用→
* ### 14 管理手机桌面→

<h1 id="3">目录3</h1> 

* ### 15 传感器应用开发→
* ### 16 GPS应用开发→
* ### 17 高德map服务→
* ### 18 合金弹头→
* ### 19 电子拍卖系统→

# 参考文档
 [百度项目地址](http://pan.baidu.com/disk/home?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&#list/vmode=list&path=%2F%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6%E5%A4%B9%2F%E9%A1%B9%E7%9B%AE%E6%A8%A1%E5%9D%97 "查看")

<h1 id="0901">ContentProvider 数据共享标准</h1>
 
[返回目录](#2) 
需要2个应用，一个是ContentProvider，一个是ContentResolver。一个应用调用其他应用的信息
ContentProvider是安卓不同程序之间数据交换的标准接口

[基本定义和应用方法](#0901_1) 
[创建一个生词本](#0901_2) 
[操作系统的ContentProvider管理联系人](#0901_3) 
[ContentProvider管理多媒体内容](#0901_4)
[监听ContentProvider的数据改变](#0901_5)

<h1 id="0901_1">ContentProvider 数据共享标准</h1>
 
[返回目录](#0901) 
![](http://i.imgur.com/BcpN2XX.jpg)

定义一个应用ContentProvider的子类
```
<!-- 注册一个ContentProvider  android:authorities这个是地址-->
		<provider
			android:exported="true"
			android:name=".FirstProvider"
			android:authorities="org.crazyit.providers.firstprovider">
		</provider>


package org.crazyit.content;

import android.content.ContentProvider;
import android.content.ContentValues;
import android.database.Cursor;
import android.net.Uri;

public class FirstProvider extends ContentProvider
{
	// 第一次创建该ContentProvider时调用该方法
	@Override
	public boolean onCreate()
	{
		System.out.println("===onCreate方法被调用===");
		return true;
	}
	// 该方法的返回值代表了该ContentProvider所提供数据的MIME类型
	@Override
	public String getType(Uri uri)
	{
		return null;
	}
	// 实现查询方法，该方法应该返回查询得到的Cursor
	@Override
	public Cursor query(Uri uri, String[] projection, String where,
						String[] whereArgs, String sortOrder)
	{
		System.out.println(uri + "===query方法被调用===");
		System.out.println("where参数为：" + where);
		return null;
	}
	// 实现插入的方法，该方法应该返回新插入的记录的Uri
	@Override
	public Uri insert(Uri uri, ContentValues values)
	{
		System.out.println(uri + "===insert方法被调用===");
		System.out.println("values参数为：" + values);
		return null;
	}
	// 实现删除方法，该方法应该返回被更新的记录条数
	@Override
	public int update(Uri uri, ContentValues values, String where,
					  String[] whereArgs)
	{
		System.out.println(uri + "===update方法被调用===");
		System.out.println("where参数为："
				+ where + ",values参数为：" + values);
		return 0;
	}
	// 实现删除方法，该方法应该返回被删除的记录条数
	@Override
	public int delete(Uri uri, String where, String[] whereArgs)
	{
		System.out.println(uri + "===delete方法被调用===");
		System.out.println("where参数为：" + where);
		return 0;
	}
}

```
调用前一个ContentProvider的子类的方法，实现增删改查的操作
```
package org.crazyit.resolver;

import android.app.Activity;
import android.content.ContentResolver;
import android.content.ContentValues;
import android.database.Cursor;
import android.net.Uri;
import android.os.Bundle;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.widget.Toast;


public class MainActivity extends Activity
{
	ContentResolver contentResolver;
	Uri uri = Uri.parse("content://org.crazyit.providers.firstprovider/");
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		setContentView(R.layout.main);
		// 获取系统的ContentResolver对象
		contentResolver = getContentResolver();
	}
	public void query(View source)
	{
		// 调用ContentResolver的query()方法
		// 实际返回的是该Uri对应的ContentProvider的query()的返回值
		Cursor c = contentResolver.query(uri, null
			, "query_where", null, null);
		Toast.makeText(this, "远程ContentProvide返回的Cursor为：" + c,
				Toast.LENGTH_SHORT).show();
	}
	public void insert(View source)
	{
		ContentValues values = new ContentValues();
		values.put("name", "fkjava");
		// 调用ContentResolver的insert()方法。
		// 实际返回的是该Uri对应的ContentProvider的insert()的返回值
		Uri newUri = contentResolver.insert(uri, values);
		Toast.makeText(this, "远程ContentProvide新插入记录的Uri为："
				+ newUri, Toast.LENGTH_SHORT).show();
	}
	public void update(View source)
	{
		ContentValues values = new ContentValues();
		values.put("name", "fkjava");
		// 调用ContentResolver的update()方法。
		// 实际返回的是该Uri对应的ContentProvider的update()的返回值
		int count = contentResolver.update(uri, values
				, "update_where", null);
		Toast.makeText(this, "远程ContentProvide更新记录数为："
				+ count, Toast.LENGTH_SHORT).show();
	}
	public void delete(View source)
	{
		// 调用ContentResolver的delete()方法
		// 实际返回的是该Uri对应的ContentProvider的delete()的返回值
		int count = contentResolver.delete(uri
				, "delete_where", null);
		Toast.makeText(this, "远程ContentProvide删除记录数为："
				+ count, Toast.LENGTH_SHORT).show();
	}
}
```
<h1 id="0901_2">创建一个生词本</h1>
 
[返回目录](#0901) 

实际上就是一个应用对另一个应用的数据进行增删改查的操作
![](http://i.imgur.com/r8PCrcf.jpg)
![](http://i.imgur.com/0uKGLjM.jpg)

分为两个应用，一个是能被操纵的应用Provider，一个是执行操作的应用ContentResolver

[被操纵的应用Provide](#0901_2_1) 
[执行操作的应用ContentResolver](#0901_2_2) 

<h1 id="0901_2_1">被操纵的应用Provide</h1>
 
[返回目录](#0901_2) 
定义2个uri和三个数据列的工具类
```
package org.crazyit.content;

import android.net.Uri;
import android.provider.BaseColumns;

public final class Words
{
	// 定义该ContentProvider的Authorities
	public static final String AUTHORITY
			= "org.crazyit.providers.dictprovider";
	// 定义一个静态内部类，定义该ContentProvider所包含的数据列的列名
	public static final class Word implements BaseColumns
	{
		// 定义Content所允许操作的三个数据列
		public final static String _ID = "_id";
		public final static String WORD = "word";
		public final static String DETAIL = "detail";
		// 定义该Content提供服务的两个Uri
		public final static Uri DICT_CONTENT_URI = Uri
			.parse("content://" + AUTHORITY + "/words");
		public final static Uri WORD_CONTENT_URI = Uri
			.parse("content://"	+ AUTHORITY + "/word");
	}
}


```
定义数据库操作类  使用代码建立数据库
```
package org.crazyit.content;

import android.content.Context;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteOpenHelper;

public class MyDatabaseHelper extends SQLiteOpenHelper
{
	final String CREATE_TABLE_SQL =
			"create table dict(_id integer primary " +
					"key autoincrement , word , detail)";
	public MyDatabaseHelper(Context context, String name, int version)
	{
		super(context, name, null, version);
	}
	@Override
	public void onCreate(SQLiteDatabase db)
	{
		// 第一次使用数据库时自动建表
		db.execSQL(CREATE_TABLE_SQL);
	}
	@Override
	public void onUpgrade(SQLiteDatabase db
			, int oldVersion, int newVersion)
	{
		System.out.println("--------onUpdate Called--------"
				+ oldVersion + "--->" + newVersion);
	}
}

```
定义DictProvider，对外提供接口和注册
```
<!-- 注册一个ContentProvider -->
		<provider android:name=".DictProvider"
				  android:authorities="org.crazyit.providers.dictprovider"
				  android:exported="true"/>

package org.crazyit.content;

import android.content.ContentProvider;
import android.content.ContentUris;
import android.content.ContentValues;
import android.content.UriMatcher;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.net.Uri;

public class DictProvider extends ContentProvider
{
	private static UriMatcher matcher
			= new UriMatcher(UriMatcher.NO_MATCH);
	private static final int WORDS = 1;
	private static final int WORD = 2;
	private MyDatabaseHelper dbOpenHelper;
	static
	{
		// 为UriMatcher注册两个Uri 它是Uri的管理器
		matcher.addURI(Words.AUTHORITY, "words", WORDS);
		matcher.addURI(Words.AUTHORITY, "word/#", WORD);
	}
	// 第一次调用该DictProvider时，系统先创建DictProvider对象，并回调该方法
	@Override
	public boolean onCreate()
	{
		dbOpenHelper = new MyDatabaseHelper(this.getContext(),
				"myDict.db3", 1);
		return true;
	}
	// 返回指定Uri参数对应的数据的MIME类型
	@Override
	public String getType(Uri uri)
	{
		switch (matcher.match(uri))
		{
			// 如果操作的数据是多项记录
			case WORDS:
				return "vnd.android.cursor.dir/org.crazyit.dict";
			// 如果操作的数据是单项记录
			case WORD:
				return "vnd.android.cursor.item/org.crazyit.dict";
			default:
				throw new IllegalArgumentException("未知Uri:" + uri);
		}
	}
	// 查询数据的方法  一个代表操作全部数据项 一个代表操作部分数据项
	@Override
	public Cursor query(Uri uri, String[] projection, String where,
						String[] whereArgs, String sortOrder)
	{
		SQLiteDatabase db = dbOpenHelper.getReadableDatabase();
		switch (matcher.match(uri))
		{
			// 如果Uri参数代表操作全部数据项
			case WORDS:
				// 执行查询
				return db.query("dict", projection, where,
						whereArgs, null, null, sortOrder);
			// 如果Uri参数代表操作指定数据项
			case WORD:
				// 解析出想查询的记录ID
				long id = ContentUris.parseId(uri);
				String whereClause = Words.Word._ID + "=" + id;
				// 如果原来的where子句存在，拼接where子句
				if (where != null && !"".equals(where))
				{
					whereClause = whereClause + " and " + where;
				}
				return db.query("dict", projection, whereClause, whereArgs,
						null, null, sortOrder);
			default:
				throw new IllegalArgumentException("未知Uri:" + uri);
		}
	}
	// 插入数据方法
	@Override
	public Uri insert(Uri uri, ContentValues values)
	{
		// 获得数据库实例
		SQLiteDatabase db = dbOpenHelper.getReadableDatabase();
		switch (matcher.match(uri))
		{
			// 如果Uri参数代表操作全部数据项
			case WORDS:
				// 插入数据，返回插入记录的ID
				long rowId = db.insert("dict", Words.Word._ID, values);
				// 如果插入成功返回uri
				if (rowId > 0)
				{
					// 在已有的 Uri的后面追加ID
					Uri wordUri = ContentUris.withAppendedId(uri, rowId);
					// 通知数据已经改变
					getContext().getContentResolver()
							.notifyChange(wordUri, null);
					return wordUri;
				}
				break;
			default :
				throw new IllegalArgumentException("未知Uri:" + uri);
		}
		return null;
	}
	// 修改数据的方法
	@Override
	public int update(Uri uri, ContentValues values, String where,
					  String[] whereArgs)
	{
		SQLiteDatabase db = dbOpenHelper.getWritableDatabase();
		// 记录所修改的记录数
		int num = 0;
		switch (matcher.match(uri))
		{
			// 如果Uri参数代表操作全部数据项
			case WORDS:
				num = db.update("dict", values, where, whereArgs);
				break;
			// 如果Uri参数代表操作指定数据项
			case WORD:
				// 解析出想修改的记录ID
				long id = ContentUris.parseId(uri);
				String whereClause = Words.Word._ID + "=" + id;
				// 如果原来的where子句存在，拼接where子句
				if (where != null && !where.equals(""))
				{
					whereClause = whereClause + " and " + where;
				}
				num = db.update("dict", values, whereClause, whereArgs);
				break;
			default:
				throw new IllegalArgumentException("未知Uri:" + uri);
		}
		// 通知数据已经改变
		getContext().getContentResolver().notifyChange(uri, null);
		return num;
	}
	// 删除数据的方法
	@Override
	public int delete(Uri uri, String where, String[] whereArgs)
	{
		SQLiteDatabase db = dbOpenHelper.getReadableDatabase();
		// 记录所删除的记录数
		int num = 0;
		// 对uri进行匹配
		switch (matcher.match(uri))
		{
			// 如果Uri参数代表操作全部数据项
			case WORDS:
				num = db.delete("dict", where, whereArgs);
				break;
			// 如果Uri参数代表操作指定数据项
			case WORD:
				// 解析出所需要删除的记录ID
				long id = ContentUris.parseId(uri);
				String whereClause = Words.Word._ID + "=" + id;
				// 如果原来的where子句存在，拼接where子句
				if (where != null && !where.equals(""))
				{
					whereClause = whereClause + " and " + where;
				}
				num = db.delete("dict", whereClause, whereArgs);
				break;
			default:
				throw new IllegalArgumentException("未知Uri:" + uri);
		}
		// 通知数据已经改变
		getContext().getContentResolver().notifyChange(uri, null);
		return num;
	}
}


```
主页面应用数据库提取数据  应用SQL语句 查询时应用了模糊查询
```
package org.crazyit.content;

import android.app.Activity;
import android.content.Intent;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map;


public class MainActivity extends Activity
{
	MyDatabaseHelper dbHelper;
	Button insert = null;
	Button search = null;
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		setContentView(R.layout.main);
		// 创建MyDatabaseHelper对象，指定数据库版本为1，此处使用相对路径即可
		// 数据库文件自动会保存在程序的数据文件夹的databases目录下
		dbHelper = new MyDatabaseHelper(this, "myDict.db3", 1);
		insert = (Button) findViewById(R.id.insert);
		search = (Button) findViewById(R.id.search);
		insert.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View source)
			{
				// 获取用户输入
				String word = ((EditText) findViewById(R.id.word))
						.getText().toString();
				String detail = ((EditText) findViewById(R.id.detail))
						.getText().toString();
				// 插入生词记录
				insertData(dbHelper.getReadableDatabase(), word, detail);
				// 显示提示信息
				Toast.makeText(MainActivity.this, "添加生词成功！"
						, Toast.LENGTH_LONG).show();
			}
		});
		search.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View source)
			{
				// 获取用户输入
				String key = ((EditText) findViewById(R.id.key)).getText()
						.toString();
				// 执行查询
				Cursor cursor = dbHelper.getReadableDatabase().rawQuery(
						"select * from dict where word like ? or detail like ?",
						new String[] { "%" + key + "%", "%" + key + "%" });
				// 创建一个Bundle对象
				Bundle data = new Bundle();
				data.putSerializable("data", converCursorToList(cursor));
				// 创建一个Intent
				Intent intent = new Intent(MainActivity.this
						, ResultActivity.class);
				intent.putExtras(data);
				// 启动Activity
				startActivity(intent);
			}
		});
	}
	//把cursor对应的数据收集成链表
	protected ArrayList<Map<String, String>>
	converCursorToList(Cursor cursor)
	{
		ArrayList<Map<String, String>> result =
				new ArrayList<Map<String, String>>();
		// 遍历Cursor结果集
		while (cursor.moveToNext())
		{
			// 将结果集中的数据存入ArrayList中
			Map<String, String> map = new HashMap<>();
			// 取出查询记录中第2列、第3列的值
			map.put("word", cursor.getString(1));
			map.put("detail", cursor.getString(2));
			result.add(map);
		}
		return result;
	}
	private void insertData(SQLiteDatabase db, String word
			, String detail)
	{
		// 执行插入语句
		db.execSQL("insert into dict values(null , ? , ?)"
				, new String[] {word, detail });
	}
	@Override
	public void onDestroy()
	{
		super.onDestroy();
		// 退出程序时关闭MyDatabaseHelper里的SQLiteDatabase
		if (dbHelper != null)
		{
			dbHelper.close();
		}
	}
}

```
把数据库数据提取成列表
```
package org.crazyit.content;

import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.widget.ListView;
import android.widget.SimpleAdapter;

import java.util.List;
import java.util.Map;

public class ResultActivity extends Activity
{
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		setContentView(R.layout.popup);
		ListView listView = (ListView) findViewById(R.id.show);
		Intent intent = getIntent();
		// 获取该intent所携带的数据
		Bundle data = intent.getExtras();
		// 从Bundle数据包中取出数据
		@SuppressWarnings("unchecked")
		List<Map<String, String>> list = (List<Map<String, String>>)
				data.getSerializable("data");
		// 将List封装成SimpleAdapter
		SimpleAdapter adapter = new SimpleAdapter(ResultActivity.this
				, list,
				R.layout.line, new String[] { "word", "detail" }
				, new int[] {R.id.word, R.id.detail });
		// 填充ListView
		listView.setAdapter(adapter);
	}
}
```
<h1 id="0901_2_2">执行操作的应用ContentResolver</h1>
 
[返回目录](#0901_2) 

应用接口进行数据查询
```
package org.crazyit.resolver;

import android.app.Activity;
import android.content.ContentResolver;
import android.content.ContentValues;
import android.content.Intent;
import android.database.Cursor;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import org.crazyit.content.Words;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map;


public class MainActivity extends Activity
{
	ContentResolver contentResolver;
	Button insert = null;
	Button search = null;
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		setContentView(R.layout.main);
		// 获取系统的ContentResolver对象
		contentResolver = getContentResolver();
		insert = (Button) findViewById(R.id.insert);
		search = (Button) findViewById(R.id.search);
		// 为insert按钮的单击事件绑定事件监听器
		insert.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View source)
			{
				// 获取用户输入
				String word = ((EditText) findViewById(R.id.word))
					.getText().toString();
				String detail = ((EditText) findViewById(R.id.detail))
					.getText().toString();
				// 插入生词记录
				ContentValues values = new ContentValues();
				values.put(Words.Word.WORD, word);
				values.put(Words.Word.DETAIL, detail);
				contentResolver.insert(
					Words.Word.DICT_CONTENT_URI, values);
				// 显示提示信息
				Toast.makeText(MainActivity.this, "添加生词成功！"
					, Toast.LENGTH_SHORT).show();
			}
		});
		// 为search按钮的单击事件绑定事件监听器
		search.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View source)
			{
				// 获取用户输入
				String key = ((EditText) findViewById(R.id.key))
					.getText().toString();
				// 执行查询
				Cursor cursor = contentResolver.query(
					Words.Word.DICT_CONTENT_URI, null,
					"word like ? or detail like ?", new String[] {
					"%" + key + "%", "%" + key + "%" }, null);
				// 创建一个Bundle对象
				Bundle data = new Bundle();
				data.putSerializable("data", converCursorToList(cursor));
				// 创建一个Intent
				Intent intent = new Intent(MainActivity.this,
					ResultActivity.class);
				intent.putExtras(data);
				// 启动Activity
				startActivity(intent);
			}
		});
	}
	private ArrayList<Map<String, String>> converCursorToList(Cursor cursor)
	{
		ArrayList<Map<String, String>> result = new ArrayList<>();
		// 遍历Cursor结果集
		while (cursor.moveToNext())
		{
			// 将结果集中的数据存入ArrayList中
			Map<String, String> map = new HashMap<>();
			// 取出查询记录中第2列、第3列的值
			map.put(Words.Word.WORD, cursor.getString(1));
			map.put(Words.Word.DETAIL, cursor.getString(2));
			result.add(map);
		}
		return result;
	}
}

```
<h1 id="0901_3">操作系统的ContentProvider管理联系人</h1>
 
[返回目录](#0901) 

![](http://i.imgur.com/xHk0e6J.jpg)

![](http://i.imgur.com/NEbqooD.jpg)

读写联系人的权限
向操作系统中加入联系人的信息
```.
<!-- 授予读联系人ContentProvider的权限 -->
	<uses-permission android:name="android.permission.READ_CONTACTS"/>
	<!-- 授予写联系人ContentProvider的权限 -->
	<uses-permission android:name="android.permission.WRITE_CONTACTS"/>

// 为add按钮的单击事件绑定监听器
		add.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View v)
			{
				// 获取程序界面中的三个文本框的内容
				String name = ((EditText) findViewById(R.id.name))
					.getText().toString();
				String phone = ((EditText) findViewById(R.id.phone))
					.getText().toString();
				String email = ((EditText) findViewById(R.id.email))
					.getText().toString();
				// 创建一个空的ContentValues
				ContentValues values = new ContentValues();
				// 向RawContacts.CONTENT_URI执行一个空值插入
				// 目的是获取系统返回的rawContactId
				Uri rawContactUri = getContentResolver().insert(
					ContactsContract.RawContacts.CONTENT_URI, values);
				//用于从指定的Uri中解析出所包含的ID值
				long rawContactId = ContentUris.parseId(rawContactUri);
				
				//添加联系人名字 分别定义行号和列号	
				values.clear();
				values.put(Data.RAW_CONTACT_ID, rawContactId);
				// 设置内容类型
				values.put(Data.MIMETYPE, StructuredName.CONTENT_ITEM_TYPE);
				// 设置联系人名字
				values.put(StructuredName.GIVEN_NAME, name);
				// 向联系人URI添加联系人名字
				getContentResolver().insert(android.provider.ContactsContract
					.Data.CONTENT_URI, values);

			//添加电话号码 分别定义行号和列号
				values.clear();
				values.put(Data.RAW_CONTACT_ID, rawContactId);
				values.put(Data.MIMETYPE, Phone.CONTENT_ITEM_TYPE);
				// 设置联系人的电话号码
				values.put(Phone.NUMBER, phone);
				// 设置电话类型
				values.put(Phone.TYPE, Phone.TYPE_MOBILE);
				// 向联系人电话号码URI添加电话号码
				getContentResolver().insert(android.provider.ContactsContract
					.Data.CONTENT_URI, values);
				
				//添加邮箱信息 分别定义行号和列号
				values.clear();
				values.put(Data.RAW_CONTACT_ID, rawContactId);//行号
				values.put(Data.MIMETYPE, Email.CONTENT_ITEM_TYPE);
				// 设置联系人的E-mail地址
				values.put(Email.DATA, email);
				// 设置该电子邮件的类型
				values.put(Email.TYPE, Email.TYPE_WORK);
				// 向联系人E-mail URI添加E-mail数据
				getContentResolver().insert(android.provider.ContactsContract
					.Data.CONTENT_URI, values);
				Toast.makeText(MainActivity.this, "联系人数据添加成功",
					Toast.LENGTH_SHORT).show();
			}
		});

```
从操作系统中读取联系人的信息
```
// 获取系统界面中查找、添加两个按钮
		search = (Button) findViewById(R.id.search);
		add = (Button) findViewById(R.id.add);
		search.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View source)
			{
				// 定义两个List来封装系统的联系人信息、指定联系人的电话号码、Email等详情
				final ArrayList<String> names = new ArrayList<>();
				final ArrayList<ArrayList<String>> details = new ArrayList<>();
				// 使用ContentResolver查找联系人数据 Contact 接触
				Cursor cursor = getContentResolver().query(
					ContactsContract.Contacts.CONTENT_URI, null, null,
					null, null);
				// 遍历查询结果，获取系统中所有联系人
				while (cursor.moveToNext())
				{
					// 获取联系人ID
					String contactId = cursor.getString(cursor
						.getColumnIndex(ContactsContract.Contacts._ID));
					// 获取联系人的名字
					String name = cursor.getString(cursor.getColumnIndex(
						ContactsContract.Contacts.DISPLAY_NAME));
					names.add(name);  
					// 使用ContentResolver查找联系人的电话号码
					Cursor phones = getContentResolver().query(
						ContactsContract.CommonDataKinds.Phone.CONTENT_URI,
						null, ContactsContract.CommonDataKinds.Phone.CONTACT_ID
						+ " = " + contactId, null, null);
					ArrayList<String> detail = new ArrayList<>();
					// 遍历查询结果，获取该联系人的多个电话号码
					while (phones.moveToNext())
					{
						// 获取查询结果中电话号码列中数据
						String phoneNumber = phones.getString(phones
							.getColumnIndex(ContactsContract
									.CommonDataKinds.Phone.NUMBER));
						detail.add("电话号码：" + phoneNumber);
					}
					phones.close();
					// 使用ContentResolver查找联系人的E-mail地址
					Cursor emails = getContentResolver().query(
						ContactsContract.CommonDataKinds.Email.CONTENT_URI,
						null, ContactsContract.CommonDataKinds.Email
						.CONTACT_ID + " = " + contactId, null, null);
					// 遍历查询结果，获取该联系人的多个E-mail地址
					while (emails.moveToNext())
					{
						// 获取查询结果中E-mail地址列中数据
						String emailAddress = emails.getString(emails
							.getColumnIndex(ContactsContract
									.CommonDataKinds.Email.DATA));
						detail.add("邮件地址：" + emailAddress);
					}
					emails.close();
					details.add(detail);
				}
				cursor.close();
				// 加载result.xml界面布局代表的视图
				View resultDialog = getLayoutInflater().inflate(
					R.layout.result, null);
				// 获取resultDialog中ID为list的ExpandableListView
				ExpandableListView list = (ExpandableListView) resultDialog
					.findViewById(R.id.list);
				// 创建一个ExpandableListAdapter对象
				ExpandableListAdapter adapter =
					new BaseExpandableListAdapter()
					{
						// 获取指定组位置、指定子列表项处的子列表项数据
						@Override
						public Object getChild(int groupPosition,
											   int childPosition)
						{
							return details.get(groupPosition).get(
									childPosition);
						}
						@Override
						public long getChildId(int groupPosition,
											   int childPosition)
						{
							return childPosition;
						}
						@Override
						public int getChildrenCount(int groupPosition)
						{
							return details.get(groupPosition).size();
						}
						private TextView getTextView()
						{
							AbsListView.LayoutParams lp = new AbsListView
								.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT
								, 64);
							TextView textView = new TextView(
								MainActivity.this);
							textView.setLayoutParams(lp);
							textView.setGravity(Gravity.CENTER_VERTICAL
								| Gravity.LEFT);
							textView.setPadding(36, 0, 0, 0);
							textView.setTextSize(20);
							return textView;
						}
						// 该方法决定每个子选项的外观
						@Override
						public View getChildView(int groupPosition,
							int childPosition, boolean isLastChild,
							View convertView, ViewGroup parent)
						{
							TextView textView = getTextView();
							textView.setText(getChild(groupPosition,
								childPosition).toString());
							return textView;
						}
						// 获取指定组位置处的组数据
						@Override
						public Object getGroup(int groupPosition)
						{
							return names.get(groupPosition);
						}
						@Override
						public int getGroupCount()
						{
							return names.size();
						}
						@Override
						public long getGroupId(int groupPosition)
						{
							return groupPosition;
						}
						// 该方法决定每个组选项的外观
						@Override
						public View getGroupView(int groupPosition,
							boolean isExpanded, View convertView,
							ViewGroup parent)
						{
							TextView textView = getTextView();
							textView.setText(getGroup(groupPosition)
								.toString());
							return textView;
						}
						@Override
						public boolean isChildSelectable(int groupPosition,
							int childPosition)
						{
							return true;
						}
						@Override
						public boolean hasStableIds()
						{
							return true;
						}
					};
				// 为ExpandableListView设置Adapter对象
				list.setAdapter(adapter);
				// 使用对话框来显示查询结果
				new AlertDialog.Builder(MainActivity.this)
					.setView(resultDialog).setPositiveButton("确定", null)
					.show();
			}
		});
```
<h1 id="0901_4">操作系统的ContentProvider管理联系人</h1>
 
[返回目录](#0901) 
![](http://i.imgur.com/eoEQTlN.jpg)
![](http://i.imgur.com/e42PmTw.jpg)
添加 就是将程序中指定图片添加到多媒体的数据中
```
package org.crazyit.content;

import android.app.Activity;
import android.app.AlertDialog;
import android.content.ContentValues;
import android.database.Cursor;
import android.graphics.Bitmap;
import android.graphics.BitmapFactory;
import android.net.Uri;
import android.provider.MediaStore.Images.Media;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.AdapterView;
import android.widget.AdapterView.OnItemClickListener;
import android.widget.Button;
import android.widget.ImageView;
import android.widget.ListView;
import android.widget.SimpleAdapter;

import java.io.IOException;
import java.io.OutputStream;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;


public class MainActivity extends Activity
{
	Button add;
	Button view;
	ListView show;
	ArrayList<String> names = new ArrayList<>();
	ArrayList<String> descs = new ArrayList<>();
	ArrayList<String> fileNames = new ArrayList<>();
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		setContentView(R.layout.main);
		add = (Button) findViewById(R.id.add);
		view = (Button) findViewById(R.id.view);
		show = (ListView) findViewById(R.id.show);

		// 为view按钮的单击事件绑定监听器
		view.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View v)
			{
				// 清空names、descs、fileNames集合里原有的数据
				names.clear();
				descs.clear();
				fileNames.clear();
				// 通过ContentResolver查询所有图片信息 
				//import android.provider.MediaStore.Images.Media;
				//存储在外部sd卡上的图片文件
				Cursor cursor = getContentResolver().query(
					Media.EXTERNAL_CONTENT_URI, null, null, null, null);
				while (cursor.moveToNext())
				{
					// 获取图片的显示名
					String name = cursor.getString(cursor
						.getColumnIndex(Media.DISPLAY_NAME));
					// 获取图片的详细描述
					String desc = cursor.getString(cursor
						.getColumnIndex(Media.DESCRIPTION));
					// 获取图片的保存位置的数据
					byte[] data = cursor.getBlob(cursor
						.getColumnIndex(Media.DATA));
					// 将图片名添加到names集合中
					names.add(name);
					// 将图片描述添加到descs集合中
					descs.add(desc);
					// 将图片保存路径添加到fileNames集合中
					fileNames.add(new String(data, 0, data.length - 1));
				}
				// 创建一个List集合，List集合的元素是Map
				List<Map<String, Object>> listItems = new ArrayList<>();
				// 将names、descs两个集合对象的数据转换到Map集合中
				for (int i = 0; i < names.size(); i++)
				{
					Map<String, Object> listItem = new HashMap<>();
					listItem.put("name", names.get(i));
					listItem.put("desc", descs.get(i));
					listItems.add(listItem);
				}
				// 创建一个SimpleAdapter
				SimpleAdapter simpleAdapter = new SimpleAdapter(
					MainActivity.this, listItems ,
					R.layout.line, new String[] { "name", "desc" }
					, new int[] {R.id.name, R.id.desc });
				// 为show ListView组件设置Adapter
				show.setAdapter(simpleAdapter);
			}
		});
		// 为show ListView的列表项单击事件添加监听器
		show.setOnItemClickListener(new OnItemClickListener()
		{
			@Override
			public void onItemClick(AdapterView<?> parent
				, View source, int position, long id)
			{
				// 加载view.xml界面布局代表的视图
				View viewDialog = getLayoutInflater().inflate(
					R.layout.view, null);
				// 获取viewDialog中ID为image的组件
				ImageView image = (ImageView) viewDialog
					.findViewById(R.id.image);
				// 设置image显示指定图片
				image.setImageBitmap(BitmapFactory.decodeFile(
					fileNames.get(position)));
				// 使用对话框显示用户单击的图片
				new AlertDialog.Builder(MainActivity.this)
					.setView(viewDialog).setPositiveButton("确定", null)
					.show();
			}
		});

		// 为add按钮的单击事件绑定监听器 
		add.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View v)
			{
				// 创建ContentValues对象，准备插入数据
				ContentValues values = new ContentValues();
				values.put(Media.DISPLAY_NAME, "jinta");
				values.put(Media.DESCRIPTION, "金塔");
				values.put(Media.MIME_TYPE, "image/jpeg");
				// 插入数据，返回所插入数据对应的Uri
				Uri uri = getContentResolver().insert(
					Media.EXTERNAL_CONTENT_URI, values);
				// 加载应用程序下的jinta图片
				Bitmap bitmap = BitmapFactory.decodeResource(
					MainActivity.this.getResources(),
					R.drawable.jinta);
				System.out.println("======");
				OutputStream os = null;
				try
				{
					// 获取刚插入的数据的Uri对应的输出流
					os = getContentResolver().openOutputStream(uri); // ①
					// 将bitmap图片保存到Uri对应的数据节点中
					bitmap.compress(Bitmap.CompressFormat.JPEG, 100, os);
					os.close();
				}
				catch (IOException e)
				{
					e.printStackTrace();
				}
			}
		});

	}
}

```
<h1 id="0901_5">监听ContentProvider的数据改变</h1>

 
[返回目录](#0901) 
```
	<!-- 授予本应用读取短信的权限 -->
	<uses-permission android:name="android.permission.READ_SMS"/>

package org.crazyit.content;

import android.app.Activity;
import android.database.ContentObserver;
import android.database.Cursor;
import android.net.Uri;
import android.os.Bundle;
import android.os.Handler;
import android.view.Menu;
import android.view.MenuItem;

public class MainActivity extends Activity
{
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		setContentView(R.layout.main);
		// 为content://sms的数据改变注册监听器
		getContentResolver().registerContentObserver(
			Uri.parse("content://sms"), true,
			new SmsObserver(new Handler()));
	}
	// 提供自定义的ContentObserver监听器类
	private final class SmsObserver extends ContentObserver
	{
		public SmsObserver(Handler handler)
		{
			super(handler);
		}
		public void onChange(boolean selfChange)
		{
			// 查询发送箱中的短信（处于正在发送状态的短信放在发送箱）
			Cursor cursor = getContentResolver().query(
				Uri.parse("content://sms/outbox")
				, null, null, null, null);
			// 遍历查询得到的结果集，即可获取用户正在发送的短信
			while (cursor.moveToNext())
			{
				StringBuilder sb = new StringBuilder();
				// 获取短信的发送地址
				sb.append("address=").append(cursor
					.getString(cursor.getColumnIndex("address")));
				// 获取短信的标题
				sb.append(";subject=").append(cursor
					.getString(cursor.getColumnIndex("subject")));
				// 获取短信的内容
				sb.append(";body=").append(cursor
					.getString(cursor.getColumnIndex("body")));
				// 获取短信的发送时间
				sb.append(";time=").append(cursor
					.getLong(cursor.getColumnIndex("date")));
				System.out.println("发送短信：" + sb.toString());
			}
		}
	}
}


```

<h1 id="1001">1. 绑定服务并通信</h1>
 
[返回目录](#2) 

服务的运行流程是
先服务自己创建，绑定，然后界面和服务连接成功
然后服务自己解绑，和销毁

![](http://i.imgur.com/zGWAF2M.jpg)
![](http://i.imgur.com/LhNCj79.jpg)
服务的注册
``` 
  <service android:name=".BindService">
        </service>
``` 
绑定服务并通信  [服务的自定义](#1001_1)
```
package utilcode.tyq.com.ceshi4;

import android.app.Activity;
import android.app.Service;
import android.content.ComponentName;
import android.content.Intent;
import android.content.ServiceConnection;
import android.os.Bundle;
import android.os.IBinder;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.Toast;

public class MainActivity extends Activity
{
    Button bind, unbind, getServiceStatus;
    // 保持所启动的Service的IBinder对象 启动成功后返回给调用者的一个对象 连接成功是实例化
    BindService.MyBinder binder;
    // 定义一个ServiceConnection对象  监听Activity与服务的连接情况
    private ServiceConnection conn = new ServiceConnection()
    {
        // 当该Activity与Service连接成功时回调该方法
        @Override
        public void onServiceConnected(ComponentName name
                , IBinder service)
        {
            System.out.println("--Service Connected--");
            // 获取Service的onBind方法所返回的MyBinder对象
            binder = (BindService.MyBinder) service;  // ①
        }
        // 当该Activity与Service由于异常情况断开连接时回调该方法
        @Override
        public void onServiceDisconnected(ComponentName name)
        {
            System.out.println("--Service Disconnected--");
        }
    };
    @Override
    public void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
        // 获取程序界面中的start、stop、getServiceStatus按钮
        bind = (Button) findViewById(R.id.bind);
        unbind = (Button) findViewById(R.id.unbind);
        getServiceStatus = (Button) findViewById(R.id.getServiceStatus);
        // 创建启动Service的Intent
        final Intent intent = new Intent(this, BindService.class);
        bind.setOnClickListener(new OnClickListener()
        {
            @Override
            public void onClick(View source)
            {
                // 绑定指定Service  Service.BIND_AUTO_CREATE表示服务未创建就创建一个服务
                // 把监听器放到服务中
                bindService(intent, conn, Service.BIND_AUTO_CREATE);
            }
        });
        unbind.setOnClickListener(new OnClickListener()
        {
            @Override
            public void onClick(View source)
            {
                // 解除绑定Service  这个是content中的方法 释放监听器
                unbindService(conn);
            }
        });
        getServiceStatus.setOnClickListener(new OnClickListener()
        {
            @Override
            public void onClick(View source)
            {
                // 获取、并显示Service的count值 Activity与服务之间对象的传递
                Toast.makeText(MainActivity.this,
                        "Service的count值为：" + binder.getCount(),
                        Toast.LENGTH_SHORT).show();  // ②
            }
        });
    }
}




```
<h1 id="1001_1">1. 服务的自定义</h1>
 
[返回目录](#1001) 
```
package utilcode.tyq.com.ceshi4;

import android.app.Service;
import android.content.Intent;
import android.os.Binder;
import android.os.IBinder;

public class BindService extends Service
{
	private int count;
	private boolean quit;
	// 定义onBinder方法所返回的对象
	private MyBinder binder = new MyBinder();
	// 通过继承Binder来实现IBinder类
	public class MyBinder extends Binder  // ①
	{
		//继承类，并自定义一个方法
		public int getCount()
		{
			// 获取Service的运行状态：count
			return count;
		}
	}
	// 必须实现的方法，绑定该Service时回调该方法
	@Override
	public IBinder onBind(Intent intent)
	{
		System.out.println("Service is Binded");
		// 返回IBinder对象
		return binder;
	}
	// Service被创建时回调该方法
	@Override
	public void onCreate()
	{
		super.onCreate();
		System.out.println("Service is Created");
		// 启动一条线程，动态地修改count状态值
		new Thread()
		{
			@Override
			public void run()
			{
				while (!quit)
				{
					try
					{
						Thread.sleep(1000);
					}
					catch (InterruptedException e)
					{
					}
					count++;
				}
			}
		}.start();
	}
	// Service被断开连接时回调该方法
	@Override
	public boolean onUnbind(Intent intent)
	{
		System.out.println("Service is Unbinded");
		return true;
	}
	// Service被关闭之前回调该方法
	@Override
	public void onDestroy()
	{
		super.onDestroy();
		this.quit = true;
		System.out.println("Service is Destroyed");
	}
}

```
<h1 id="1002">2. IntentService</h1>
 
[返回目录](#2) 

IntentService会创建单独的worer线程来处理所有的Intent请求。
处理完成后，会自动终止线程。
![](http://i.imgur.com/qhl9bxI.jpg)

启动服务的代码
```
public void startService(View source)
	{
		// 创建需要启动的Service的Intent
		Intent intent = new Intent(this, MyService.class);
		// 启动Service
		startService(intent);
	}
	public void startIntentService(View source)
	{
		// 创建需要启动的IntentService的Intent
		Intent intent = new Intent(this, MyIntentService.class);
		// 启动IntentService
		startService(intent);
	}
```
普通服务
```
package org.crazyit.service;

import android.app.Service;
import android.content.Intent;
import android.os.IBinder;

public class MyService extends Service
{
	@Override
	public IBinder onBind(Intent intent)
	{
		return null;
	}
	@Override
	public int onStartCommand(Intent intent, int flags, int startId)
	{
		// 该方法内执行耗时任务可能导致ANR（Application Not Responding）异常
		long endTime = System.currentTimeMillis() + 20 * 1000;
		System.out.println("onStart");
		while (System.currentTimeMillis() < endTime)
		{
			synchronized (this)
			{
				try
				{
					wait(endTime - System.currentTimeMillis());
				}
				catch (Exception e)
				{
				}
			}
		}
		System.out.println("---耗时任务执行完成---");
		return START_STICKY;
	}
}

```
IntentService的实现
```
package org.crazyit.service;

import android.app.IntentService;
import android.content.Intent;

public class MyIntentService extends IntentService
{
	public MyIntentService()
	{
		super("MyIntentService");
	}
	// IntentService会使用单独的线程来执行该方法的代码
	@Override
	protected void onHandleIntent(Intent intent)
	{
		// 该方法内可以执行任何耗时任务，比如下载文件等，此处只是让线程暂停20秒
		long endTime = System.currentTimeMillis() + 20 * 1000;
		System.out.println("onStartCommand");
		while (System.currentTimeMillis() < endTime)
		{//线程暂停
			synchronized (this)
			{
				try
				{
					wait(endTime - System.currentTimeMillis());
				}
				catch (Exception e)
				{
				}
			}
		}
		System.out.println("---耗时任务执行完成---");
	}
}

```

<h1 id="1003">1. 电话管理器</h1>
 
[返回目录](#2) 

SimpleAdapter 适配器的运用
需要权限

[监听手机来电](1003_1)

![](http://i.imgur.com/QUch1T7.jpg)
列表
```
<ListView 
	android:id="@+id/show"
	android:layout_width="match_parent" 
	android:layout_height="match_parent" 
	android:entries="@array/statusNames"
	/>
```
字符串列表
```
<?xml version="1.0" encoding="utf-8"?>
<resources>
	<!-- 声明一个名为statusNames的字符串数组 -->
	<string-array name="statusNames">
		<item>设备编号</item>
		<item>软件版本</item>
		<item>网络运营商代号</item>
		<item>网络运营商名称</item>
		<item>手机制式</item>
		<item>设备当前位置</item>
		<item>SIM卡的国别</item>
		<item>SIM卡序列号</item>
		<item>SIM卡状态</item>		
	</string-array>
	<!-- 声明一个名为simState的字符串数组 -->
	<string-array name="simState">
		<item>状态未知</item>
		<item>无SIM卡</item>
		<item>被PIN加锁</item>
		<item>被PUK加锁</item>
		<item>被NetWork PIN加锁</item>
		<item>已准备好</item>
	</string-array>
	<!-- 声明一个名为phoneType的字符串数组 -->
	<string-array name="phoneType">	
		<item>未知</item>
		<item>GSM</item>
		<item>CDMA</item>
	</string-array>	
</resources>

```
源代码实现
```
package utilcode.tyq.com.ceshi4;

import android.app.Activity;
import android.content.Context;
import android.os.Bundle;
import android.telephony.TelephonyManager;
import android.view.Menu;
import android.view.MenuItem;
import android.widget.ListView;
import android.widget.SimpleAdapter;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map;


public class MainActivity extends Activity
{
    ListView showView;
    // 声明代表状态名的数组
    String[] statusNames;
    // 声明代表手机状态的集合
    ArrayList<String> statusValues = new ArrayList<>();
    @Override
    public void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
        // 获取系统的TelephonyManager对象
        TelephonyManager tManager = (TelephonyManager)
                getSystemService(Context.TELEPHONY_SERVICE);
        // 获取各种状态名称的数组
        statusNames = getResources().getStringArray(R.array.statusNames);
        // 获取代表SIM卡状态的数组
        String[] simState = getResources()
                .getStringArray(R.array.simState);
        // 获取代表电话网络类型的数组
        String[] phoneType = getResources().getStringArray(
                R.array.phoneType);
        // 获取设备编号
        statusValues.add(tManager.getDeviceId());
        // 获取系统平台的版本
        statusValues.add(tManager.getDeviceSoftwareVersion()
                != null ? tManager.getDeviceSoftwareVersion() : "未知");
        // 获取网络运营商代号
        statusValues.add(tManager.getNetworkOperator());
        // 获取网络运营商名称
        statusValues.add(tManager.getNetworkOperatorName());
        // 获取手机网络类型
        statusValues.add(phoneType[tManager.getPhoneType()]);
        // 获取设备所在位置
        statusValues.add(tManager.getCellLocation() != null ? tManager
                .getCellLocation().toString() : "未知位置");
        // 获取SIM卡的国别
        statusValues.add(tManager.getSimCountryIso());
        // 获取SIM卡序列号
        statusValues.add(tManager.getSimSerialNumber());
        // 获取SIM卡状态
        statusValues.add(simState[tManager.getSimState()]);
        // 获得ListView对象
        showView = (ListView) findViewById(R.id.show);
        ArrayList<Map<String, String>> status = new ArrayList<>();
        // 遍历statusValues集合，将statusNames、statusValues
        // 的数据封装到List<Map<String , String>>集合中
        for (int i = 0; i < statusValues.size(); i++)
        {
            HashMap<String, String> map = new HashMap<>();
            map.put("name", statusNames[i]);
            map.put("value", statusValues.get(i));
            status.add(map);
        }
        // 使用SimpleAdapter封装List数据
        SimpleAdapter adapter = new SimpleAdapter(this, status,
                R.layout.line, new String[] { "name", "value" }
                , new int[] { R.id.name, R.id.value });
        // 为ListView设置Adapter
        showView.setAdapter(adapter);
    }
}


```
<h1 id="1003_1">1. 监听手机来电</h1>
 
[返回目录](#1003) 

需要权限
```
package org.crazyit.manager;

import android.app.Activity;
import android.content.Context;
import android.os.Bundle;
import android.telephony.PhoneStateListener;
import android.telephony.TelephonyManager;

import java.io.FileNotFoundException;
import java.io.OutputStream;
import java.io.PrintStream;
import java.util.Date;

public class MainActivity extends Activity
{
	TelephonyManager tManager;
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		setContentView(R.layout.main);
		// 取得TelephonyManager对象
		tManager = (TelephonyManager)
				getSystemService(Context.TELEPHONY_SERVICE);
		// 创建一个通话状态监听器
		PhoneStateListener listener = new PhoneStateListener()
		{
			@Override
			public void onCallStateChanged(int state, String number)
			{
				switch (state)
				{
					// 无任何状态
					case TelephonyManager.CALL_STATE_IDLE:
						break;
					case TelephonyManager.CALL_STATE_OFFHOOK:
						break;
					// 来电铃响时
					case TelephonyManager.CALL_STATE_RINGING:
						OutputStream os = null;
						try
						{
							os = openFileOutput("phoneList", MODE_APPEND);
						}
						catch (FileNotFoundException e)
						{
							e.printStackTrace();
						}
						PrintStream ps = new PrintStream(os);
						// 将来电号码记录到文件中
						ps.println(new Date() + " 来电：" + number);
						ps.close();
						break;
					default:
						break;
				}
				super.onCallStateChanged(state, number);
			}
		};
		// 监听电话通话状态的改变
		tManager.listen(listener, PhoneStateListener.LISTEN_CALL_STATE);
	}
}

```
<h1 id="1004">1. 短信管理器</h1>
 
[返回目录](#2) 

发送短信 需要权限
```
	// 创建一个PendingIntent对象
				PendingIntent pi = PendingIntent.getActivity(
						MainActivity.this, 0, new Intent(), 0);
				// 发送短信 分别获取收件人和内容
				sManager.sendTextMessage(number.getText().toString(),
						null, content.getText().toString(), pi, null);
				// 提示短信发送完成
				Toast.makeText(MainActivity.this, "短信发送完成", 8000).show();
```
群发短信
![](http://i.imgur.com/ZgqQm2u.png)
```
package org.crazyit.manager;

import android.app.Activity;
import android.app.AlertDialog;
import android.app.PendingIntent;
import android.content.DialogInterface;
import android.content.Intent;
import android.database.Cursor;
import android.os.Bundle;
import android.provider.ContactsContract;
import android.telephony.SmsManager;
import android.view.View;
import android.view.View.OnClickListener;
import android.view.ViewGroup;
import android.widget.BaseAdapter;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.EditText;
import android.widget.ListView;
import android.widget.Toast;

import java.util.ArrayList;


public class MainActivity extends Activity
{
	EditText numbers, content;
	Button select, send;
	SmsManager sManager;
	// 记录需要群发的号码列表
	ArrayList<String> sendList = new ArrayList<String>();
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		setContentView(R.layout.main);
		sManager = SmsManager.getDefault();
		// 获取界面上的文本框、按钮组件
		numbers = (EditText) findViewById(R.id.numbers);
		content = (EditText) findViewById(R.id.content);
		select = (Button) findViewById(R.id.select);
		send = (Button) findViewById(R.id.send);
		// 为send按钮的单击事件绑定监听器
		send.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View v)
			{
				for (String number : sendList)
				{
					// 创建一个PendingIntent对象
					PendingIntent pi = PendingIntent.getActivity(
							MainActivity.this, 0, new Intent(), 0);
					// 发送短信
					sManager.sendTextMessage(number, null, content
							.getText().toString(), pi, null);
				}
				// 提示短信群发完成
				Toast.makeText(MainActivity.this, "短信群发完成"
						, Toast.LENGTH_SHORT).show();
			}
		});
		// 为select按钮的单击事件绑定监听器
		select.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View v)
			{
				// 查询联系人的电话号码 从公共资源中查询联系人
				final Cursor cursor = getContentResolver().query(
						ContactsContract.CommonDataKinds.Phone.CONTENT_URI,
						null, null, null, null);
				BaseAdapter adapter = new BaseAdapter()
				{
					@Override
					public int getCount()
					{
						return cursor.getCount();
					}
					@Override
					public Object getItem(int position)
					{
						return position;
					}
					@Override
					public long getItemId(int position)
					{
						return position;
					}
					@Override
					public View getView(int position, View convertView,
										ViewGroup parent)
					{
						cursor.moveToPosition(position);
						CheckBox rb = new CheckBox(MainActivity.this);
						// 获取联系人的电话号码，并去掉中间的中画线、空格
						String number = cursor
								.getString(cursor.getColumnIndex(ContactsContract
										.CommonDataKinds.Phone.NUMBER))
								.replace("-", "")
								.replace(" " , "");
						rb.setText(number);
						// 如果该号码已经被加入发送人名单，默认勾选该号码
						if (isChecked(number))
						{
							rb.setChecked(true);
						}
						return rb;
					}
				};
				// 加载list.xml布局文件对应的View
				View selectView = getLayoutInflater().inflate(
						R.layout.list, null);
				// 获取selectView中的名为list的ListView组件
				final ListView listView = (ListView) selectView
						.findViewById(R.id.list);
				listView.setAdapter(adapter);
//这个是弹出对话框的代码
				new AlertDialog.Builder(MainActivity.this)
						.setView(selectView)
						.setPositiveButton("确定",
								new DialogInterface.OnClickListener()
								{
									@Override
									public void onClick(DialogInterface dialog,
														int which)
									{
										// 清空sendList集合
										sendList.clear();
										// 遍历listView组件的每个列表项
										for (int i = 0; i < listView.getCount(); i++)
										{
											CheckBox checkBox = (CheckBox) listView
													.getChildAt(i);
											// 如果该列表项被勾选
											if (checkBox.isChecked())
											{
												// 添加该列表项的电话号码
												sendList.add(checkBox.getText()
														.toString());
											}
										}
										numbers.setText(sendList.toString());
									}
								}).show();
			}
		});
	}
	// 判断某个电话号码是否已在群发范围内
	public boolean isChecked(String phone)
	{
		for (String s1 : sendList)
		{
			if (s1.equals(phone))
			{
				return true;
			}
		}
		return false;
	}
}


```
<h1 id="1005">1. 音频管理器</h1>
 
[返回目录](#2) 

![](http://i.imgur.com/OMa078T.jpg)

静音或正常的按钮
```
<ToggleButton
	android:id="@+id/mute"
	android:layout_width="wrap_content" 
	android:layout_height="wrap_content" 
	android:textOn="@string/normal"
	android:textOff="@string/mute"
/>
```
实现的代码

```
package org.crazyit.manager;

import android.app.Activity;
import android.app.Service;
import android.media.AudioManager;
import android.media.MediaPlayer;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.CompoundButton;
import android.widget.CompoundButton.OnCheckedChangeListener;
import android.widget.ToggleButton;


public class MainActivity extends Activity
{
	Button play, up, down;
	ToggleButton mute;
	AudioManager aManager;
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		setContentView(R.layout.main);
		// 获取系统的音频服务
		aManager = (AudioManager) getSystemService(
				Service.AUDIO_SERVICE);
		// 获取界面中三个按钮和一个ToggleButton控件
		play = (Button) findViewById(R.id.play);
		up = (Button) findViewById(R.id.up);
		down = (Button) findViewById(R.id.down);
		mute = (ToggleButton) findViewById(R.id.mute);
		// 为play按钮的单击事件绑定监听器
		play.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View source)
			{
				//从raw文件夹中读取文件
				// 初始化MediaPlayer对象，准备播放音乐
				MediaPlayer mPlayer = MediaPlayer.create(
						MainActivity.this, R.raw.earth);
				// 设置循环播放
				mPlayer.setLooping(true);
				// 开始播放
				mPlayer.start();
			}
		});
		up.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View source)
			{
				// STREAM_MUSIC指定调节音乐的音频，ADJUST_RAISE增大音量，FLAG_SHOW_UI而且显示音量图形示意
				aManager.adjustStreamVolume(AudioManager.STREAM_MUSIC,
						AudioManager.ADJUST_RAISE, AudioManager.FLAG_SHOW_UI);
			}
		});
		down.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View source)
			{
				// 指定调节音乐的音频，降低音量，而且显示音量图形示意
				aManager.adjustStreamVolume(AudioManager.STREAM_MUSIC,
						AudioManager.ADJUST_LOWER, AudioManager.FLAG_SHOW_UI);
			}
		});
		mute.setOnCheckedChangeListener(new OnCheckedChangeListener()
		{
			@Override
			public void onCheckedChanged(CompoundButton source,
										 boolean isChecked)
			{
				// 指定调节音乐的音频，根据isChecked确定是否需要静音
				aManager.setStreamMute(AudioManager.STREAM_MUSIC,
						isChecked);
			}
		});
	}
}

```
<h1 id="1006">1. 振动管理器</h1>
 
[返回目录](#2) 

```
package org.crazyit.manager;

import android.app.Activity;
import android.app.Service;
import android.os.Bundle;
import android.os.Vibrator;
import android.view.Menu;
import android.view.MenuItem;
import android.view.MotionEvent;
import android.widget.Toast;


public class MainActivity extends Activity
{
	Vibrator vibrator;
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		setContentView(R.layout.main);
		// 获取系统的Vibrator服务
		vibrator = (Vibrator) getSystemService(
				Service.VIBRATOR_SERVICE);
	}
	// 重写onTouchEvent方法，当用户触碰触摸屏时触发该方法
	@Override
	public boolean onTouchEvent(MotionEvent event)
	{
		Toast.makeText(this, "手机振动"
				, Toast.LENGTH_SHORT).show();
		// 控制手机振动2秒
		vibrator.vibrate(2000);
		return super.onTouchEvent(event);
	}
}

```
<h1 id="1007">1. 手机闹钟服务</h1>
 
[返回目录](#2) 

[定时更换壁纸](#1007_1)

全局定时器使用，当宿主进程被杀死以后，运行在宿主进程上的组件也就不存在了。
如果进程关闭了，闹钟就不响了
![](http://i.imgur.com/dF7XCtu.jpg)
```
package org.crazyit.manager;

import android.app.Activity;
import android.app.AlertDialog;
import android.content.DialogInterface;
import android.content.DialogInterface.OnClickListener;
import android.media.MediaPlayer;
import android.os.Bundle;

public class AlarmActivity extends Activity
{
	MediaPlayer alarmMusic;
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		// 加载指定音乐，并为之创建MediaPlayer对象
		alarmMusic = MediaPlayer.create(this, R.raw.alarm);
		alarmMusic.setLooping(true);
		// 播放音乐
		alarmMusic.start();
		// 创建一个对话框
		new AlertDialog.Builder(AlarmActivity.this).setTitle("闹钟")
				.setMessage("闹钟响了,Go！Go！Go！")
				.setPositiveButton("确定", new OnClickListener()
				{
					@Override
					public void onClick(DialogInterface dialog, int which)
					{
						// 停止音乐
						alarmMusic.stop();
						// 结束该Activity
						AlarmActivity.this.finish();
					}
				}).show();
	}
}


```
![](http://i.imgur.com/qVYss4F.jpg)

```
package org.crazyit.manager;

import android.app.Activity;
import android.app.AlarmManager;
import android.app.PendingIntent;
import android.app.TimePickerDialog;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.TimePicker;
import android.widget.Toast;

import java.util.Calendar;

public class MainActivity extends Activity
{
	Button setTime;
	Calendar currentTime = Calendar.getInstance();
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		setContentView(R.layout.main);
		// 获取程序界面的按钮
		setTime = (Button) findViewById(R.id.setTime);
		// 为“设置闹铃”按钮绑定监听器。
		setTime.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View source)
			{
				Calendar currentTime = Calendar.getInstance();
				// 创建一个TimePickerDialog实例，并把它显示出来。
				new TimePickerDialog(MainActivity.this, 0, // 绑定监听器
					new TimePickerDialog.OnTimeSetListener()
					{
						@Override
						public void onTimeSet(TimePicker tp,
							int hourOfDay, int minute)
						{
							// 指定启动AlarmActivity组件
							Intent intent = new Intent(MainActivity.this,
								AlarmActivity.class);
							// 创建PendingIntent对象  打开一个Activity页面
							PendingIntent pi = PendingIntent.getActivity(
									MainActivity.this, 0, intent, 0);
							分割时间
							Calendar c = Calendar.getInstance();
							c.setTimeInMillis(System.currentTimeMillis());
							// 根据用户选择时间来设置Calendar对象
							c.set(Calendar.HOUR, hourOfDay);
							c.set(Calendar.MINUTE, minute);
							// 获取AlarmManager对象
							AlarmManager aManager = (AlarmManager)
								getSystemService(ALARM_SERVICE);
							// 设置AlarmManager将在Calendar对应的时间启动指定组件
							aManager.set(AlarmManager.RTC_WAKEUP,
									c.getTimeInMillis(), pi);
							// 显示闹铃设置成功的提示信息
							Toast.makeText(MainActivity.this, "闹铃设置成功啦"
								, Toast.LENGTH_SHORT).show();
						}
					}, currentTime.get(Calendar.HOUR_OF_DAY), currentTime
					.get(Calendar.MINUTE), false).show();
			}
		});
	}
}

```
<h1 id="1007_1">1. 定时更换壁纸</h1>
 
[返回目录](#1007) 

壁纸管理服务
```
package org.crazyit.manager;

import android.app.Service;
import android.app.WallpaperManager;
import android.content.Intent;
import android.os.IBinder;

public class ChangeService extends Service
{
	// 定义定时更换的壁纸资源
	int[] wallpapers = new int[]{
			R.drawable.shuangta,
			R.drawable.lijiang,
			R.drawable.qiao,
			R.drawable.shui
	};
	// 定义系统的壁纸管理服务
	WallpaperManager wManager;
	// 定义当前所显示的壁纸
	int current = 0;
	@Override
	public int onStartCommand(Intent intent, int flags, int startId)
	{
		// 如果到了最后一张，系统重新开始
		if(current >= 4)
			current = 0;
		try
		{
			// 改变壁纸
			wManager.setResource(wallpapers[current++]);
		}
		catch (Exception e)
		{
			e.printStackTrace();
		}
		return START_STICKY;
	}
	@Override
	public void onCreate()
	{
		super.onCreate();
		// 初始化WallpaperManager
		wManager = WallpaperManager.getInstance(this);
	}
	@Override
	public IBinder onBind(Intent intent)
	{
		return null;
	}
}


```
每5秒钟去启动一个服务
```
package org.crazyit.manager;

import android.app.Activity;
import android.app.AlarmManager;
import android.app.PendingIntent;
import android.app.Service;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.Toast;


public class MainActivity extends Activity
{
	Button start, stop;
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		setContentView(R.layout.main);
		start = (Button) findViewById(R.id.start);
		stop = (Button) findViewById(R.id.stop);
		// 指定启动ChangeService组件
		Intent intent = new Intent(MainActivity.this, ChangeService.class);
		// 创建PendingIntent对象 定时去启动一个服务
		final PendingIntent pi = PendingIntent.getService(MainActivity.this, 0, intent, 0);
		start.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View arg0)
			{
				// 获取AlarmManager对象
				AlarmManager aManager = (AlarmManager) getSystemService(
					Service.ALARM_SERVICE);
				// 设置每隔5秒执行pi代表的组件一次
				aManager.setRepeating(AlarmManager.ELAPSED_REALTIME_WAKEUP
					, 0, 5000, pi);
				start.setEnabled(false);
				stop.setEnabled(true);
				Toast.makeText(MainActivity.this
					, "壁纸定时更换启动成功啦",
					Toast.LENGTH_SHORT).show();
			}
		});
		stop.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View arg0)
			{
			start.setEnabled(true);
			stop.setEnabled(false);
			// 获取AlarmManager对象
			AlarmManager aManager = (AlarmManager) getSystemService(
				Service.ALARM_SERVICE);
			// 取消对pi的调度
			aManager.cancel(pi);
			}
		});
	}
}
```
<h1 id="1008">1. 接受广播服务</h1>
 
[返回目录](#2) 

这是一个全局的、系统级别的监听器，拥有自己的进程。程序级别的监听器，当程序关闭后，就退出了。
如果进程内没有任何活动组件，当内存紧张时，就会有些结束该进程

[有序广播](#1008_1)
[音乐播放器](#1008_2)
后台负责播放音乐，前台进行控制。通过广播进行通信

简单的广播
![](http://i.imgur.com/p1Sy47J.jpg)
```
注册全局广播
<receiver android:name=".MyReceiver">
			<intent-filter>
				<!-- 指定该BroadcastReceiver所响应的Intent的Action -->
				<action android:name="org.crazyit.action.CRAZY_BROADCAST" />
			</intent-filter>
		</receiver>


广播接受的实例
public class MyReceiver extends BroadcastReceiver
{
	@Override
	public void onReceive(Context context, Intent intent)
	{
		Toast.makeText(context,
			"接收到的Intent的Action为：" + intent.getAction()
			+ "\n消息内容是：" + intent.getStringExtra("msg")
			, Toast.LENGTH_LONG).show();
	}
}

发送一条广播
send.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View v)
			{
				// 创建Intent对象
				Intent intent = new Intent();
				// 设置Intent的Action属性
				intent.setAction("org.crazyit.action.CRAZY_BROADCAST");
				intent.putExtra("msg", "简单的消息");
				// 发送广播
				sendBroadcast(intent);
			}
		});
```
<h1 id="1008_1">1. 有序广播</h1>
 
[返回目录](#1008) 

注册优先级 两个广播的优先级不同
```
<receiver android:name=".MyReceiver">
			<intent-filter android:priority="20">
				<action android:name="org.crazyit.action.CRAZY_BROADCAST" />
			</intent-filter>
		</receiver>
		<receiver android:name=".MyReceiver2">
			<intent-filter android:priority="0">
				<action android:name="org.crazyit.action.CRAZY_BROADCAST" />
			</intent-filter>
		</receiver>
```
发送广播
```
// 创建Intent对象
				Intent intent = new Intent();
				intent.setAction("org.crazyit.action.CRAZY_BROADCAST");
				intent.putExtra("msg", "简单的消息");
				// 发送有序广播
				sendOrderedBroadcast(intent, null);
```
第二个广播
```
public class MyReceiver2 extends BroadcastReceiver
{
	@Override
	public void onReceive(Context context, Intent intent)
	{
		Bundle bundle = getResultExtras(true);
		// 解析前一个BroadcastReceiver所存入的key为first的消息
		String first = bundle.getString("first");
		Toast.makeText(context, "第一个Broadcast存入的消息为："
			+ first, Toast.LENGTH_LONG).show();
	}
}
```
第一个广播
```
public class MyReceiver extends BroadcastReceiver
{
	@Override
	public void onReceive(Context context, Intent intent)
	{
		Toast.makeText(context,	"接收到的Intent的Action为："
				+ intent.getAction() + "\n消息内容是："
				+ intent.getStringExtra("msg")
				, Toast.LENGTH_LONG).show();
		// 创建一个Bundle对象，并存入数据
		Bundle bundle = new Bundle();
		bundle.putString("first", "第一个BroadcastReceiver存入的消息");
		// 将bundle放入结果中
		setResultExtras(bundle);
		// 取消Broadcast的继续传播
		//abortBroadcast(); // ①
	}
}
```
<h1 id="1008_2">1. 音乐播放器</h1>
 
[返回目录](#1008) 

![](http://i.imgur.com/sJ1WkjM.jpg)

activity与服务中各注册了一个监听器，相互监听，因为采用了后台播放程序，所以就是退出程序，只要进程还在，音乐就可以正常播放。
前台
```
package org.crazyit.broadcast;

import android.app.Activity;
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.content.IntentFilter;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.ImageButton;
import android.widget.TextView;

public class MainActivity extends Activity implements OnClickListener
{
	// 获取界面中显示歌曲标题、作者文本框
	TextView title, author;
	// 播放/暂停、停止按钮
	ImageButton play, stop;
	ActivityReceiver activityReceiver;
	public static final String CTL_ACTION =
			"org.crazyit.action.CTL_ACTION";
	public static final String UPDATE_ACTION =
			"org.crazyit.action.UPDATE_ACTION";
	// 定义音乐的播放状态，0x11代表没有播放；0x12代表正在播放；0x13代表暂停
	int status = 0x11;
	String[] titleStrs = new String[] { "心愿", "约定", "美丽新世界" };
	String[] authorStrs = new String[] { "未知艺术家", "周蕙", "伍佰" };
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		setContentView(R.layout.main);
		// 获取程序界面界面中的两个按钮
		play = (ImageButton) this.findViewById(R.id.play);
		stop = (ImageButton) this.findViewById(R.id.stop);
		title = (TextView) findViewById(R.id.title);
		author = (TextView) findViewById(R.id.author);
		// 为两个按钮的单击事件添加监听器
		play.setOnClickListener(this);
		stop.setOnClickListener(this);
		页面注册广播
		activityReceiver = new ActivityReceiver();
		// 创建IntentFilter
		IntentFilter filter = new IntentFilter();
		// 指定BroadcastReceiver监听的Action
		filter.addAction(UPDATE_ACTION);
		// 注册BroadcastReceiver
		registerReceiver(activityReceiver, filter);
		开启服务
		Intent intent = new Intent(this, MusicService.class);
		// 启动后台Service
		startService(intent);
	}
	// 自定义的BroadcastReceiver，负责监听从Service传回来的广播
	public class ActivityReceiver extends BroadcastReceiver
	{
		@Override
		public void onReceive(Context context, Intent intent)
		{
			// 获取Intent中的update消息，update代表播放状态
			int update = intent.getIntExtra("update", -1);
			// 获取Intent中的current消息，current代表当前正在播放的歌曲
			int current = intent.getIntExtra("current", -1);
			-1代表返回的默认值
			if (current >= 0)
			{
				title.setText(titleStrs[current]);
				author.setText(authorStrs[current]);
			}
			switch (update)
			{
				case 0x11:
					play.setImageResource(R.drawable.play);
					status = 0x11;
					break;
				// 控制系统进入播放状态
				case 0x12:
					// 播放状态下设置使用暂停图标
					play.setImageResource(R.drawable.pause);
					// 设置当前状态
					status = 0x12;
					break;
				// 控制系统进入暂停状态
				case 0x13:
					// 暂停状态下设置使用播放图标
					play.setImageResource(R.drawable.play);
					// 设置当前状态
					status = 0x13;
					break;
			}
		}
	}
	@Override
	public void onClick(View source)
	{
		// 创建Intent
		Intent intent = new Intent("org.crazyit.action.CTL_ACTION");
		switch (source.getId())
		{
			// 按下播放/暂停按钮
			case R.id.play:
				intent.putExtra("control", 1);
				break;
			// 按下停止按钮
			case R.id.stop:
				intent.putExtra("control", 2);
				break;
		}
		// 发送广播，将被Service组件中的BroadcastReceiver接收到
		sendBroadcast(intent);
	}
}
```
后台
```
package org.crazyit.broadcast;

import java.io.IOException;

import android.app.Service;
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.content.IntentFilter;
import android.content.res.AssetFileDescriptor;
import android.content.res.AssetManager;
import android.media.MediaPlayer;
import android.media.MediaPlayer.OnCompletionListener;
import android.os.IBinder;

public class MusicService extends Service
{
	MyReceiver serviceReceiver;
	AssetManager am;
	String[] musics = new String[] { "wish.mp3", "promise.mp3",
			"beautiful.mp3" };
	MediaPlayer mPlayer;
	// 当前的状态，0x11代表没有播放；0x12代表正在播放；0x13代表暂停
	int status = 0x11;
	// 记录当前正在播放的音乐
	int current = 0;
	@Override
	public IBinder onBind(Intent intent)
	{
		return null;
	}
	@Override
	public void onCreate()
	{
		super.onCreate();
		am = getAssets();
		// 创建BroadcastReceiver
		serviceReceiver = new MyReceiver();
		// 创建IntentFilter
		IntentFilter filter = new IntentFilter();
		filter.addAction(MainActivity.CTL_ACTION);
		registerReceiver(serviceReceiver, filter);
		// 创建MediaPlayer
		mPlayer = new MediaPlayer();
		// 为MediaPlayer播放完成事件绑定监听器
		mPlayer.setOnCompletionListener(new OnCompletionListener() // ①
		{
			@Override
			public void onCompletion(MediaPlayer mp)
			{
				current++;
				if (current >= 3)
				{
					current = 0;
				}
				//发送广播通知Activity更改文本框
				Intent sendIntent = new Intent(MainActivity.UPDATE_ACTION);
				sendIntent.putExtra("current", current);
				// 发送广播，将被Activity组件中的BroadcastReceiver接收到
				sendBroadcast(sendIntent);
				// 准备并播放音乐
				prepareAndPlay(musics[current]);
			}
		});
	}
	public class MyReceiver extends BroadcastReceiver
	{
		@Override
		public void onReceive(final Context context, Intent intent)
		{
			int control = intent.getIntExtra("control", -1);
			switch (control)
			{
				// 播放或暂停
				case 1:
					// 原来处于没有播放状态
					if (status == 0x11)
					{
						// 准备并播放音乐
						prepareAndPlay(musics[current]);
						status = 0x12;
					}
					// 原来处于播放状态
					else if (status == 0x12)
					{
						// 暂停
						mPlayer.pause();
						// 改变为暂停状态
						status = 0x13;
					}
					// 原来处于暂停状态
					else if (status == 0x13)
					{
						// 播放
						mPlayer.start();
						// 改变状态
						status = 0x12;
					}
					break;
				// 停止声音
				case 2:
					// 如果原来正在播放或暂停
					if (status == 0x12 || status == 0x13)
					{
						// 停止播放
						mPlayer.stop();
						status = 0x11;
					}
			}
			// 广播通知Activity更改图标、文本框
			Intent sendIntent = new Intent(MainActivity.UPDATE_ACTION);
			sendIntent.putExtra("update", status);
			sendIntent.putExtra("current", current);
			// 发送广播，将被Activity组件中的BroadcastReceiver接收到
			sendBroadcast(sendIntent);
		}
	}
	private void prepareAndPlay(String music)
	{
		try
		{
			// 打开指定音乐文件
			AssetFileDescriptor afd = am.openFd(music);
			mPlayer.reset();
			// 使用MediaPlayer加载指定的声音文件。
			mPlayer.setDataSource(afd.getFileDescriptor(),
					afd.getStartOffset(), afd.getLength());
			// 准备声音
			mPlayer.prepare();
			// 播放
			mPlayer.start();
		}
		catch (IOException e)
		{
			e.printStackTrace();
		}
	}
}


```
<h1 id="1009">1. 接受系统广播</h1>
 
[返回目录](#2) 

开机自动运行服务
```
开机运行的权限
<!-- 授予应用程序访问系统开机事件的权限 -->
	<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>

<!-- 定义一个BroadcastReceiver,监听系统开机广播  -->
		<receiver android:name=".LaunchReceiver">
			<intent-filter>
				<action android:name="android.intent.action.BOOT_COMPLETED" />
			</intent-filter>
		</receiver>

public class LaunchReceiver extends BroadcastReceiver
{
	@Override
	public void onReceive(Context context, Intent intent)
	{
		Intent tIntent = new Intent(context
				, LaunchService.class);
		// 启动指定Service
		context.startService(tIntent);
	}
}


public class LaunchService extends Service
{
	@Override
	public IBinder onBind(Intent intent)
	{
		return null;
	}
	@Override
	public void onCreate()
	{
		// 定义1秒执行一行输出
		new Timer().schedule(new TimerTask()
		{

			@Override
			public void run()
			{
				System.out.println("-----"
						+ new Date() + "-----");
			}
		}, 0, 1000);
	}
}
```
短信提醒
```
<receiver android:name="SmsReceiver">
			<intent-filter android:priority="1000">
				<action android:name="android.provider.Telephony.SMS_RECEIVED" />
			</intent-filter>
		</receiver>

<!-- 授予程序接收短信的权限 -->
	<uses-permission android:name="android.permission.RECEIVE_SMS"/>


package org.crazyit.broadcast;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.os.Bundle;
import android.telephony.SmsMessage;
import android.widget.Toast;

import java.text.SimpleDateFormat;
import java.util.Date;

public class SmsReceiver extends BroadcastReceiver
{
	// 当接收到短信时被触发
	@Override
	public void onReceive(Context context, Intent intent)
	{
		// 如果是接收到短信
		if (intent.getAction().equals(
				"android.provider.Telephony.SMS_RECEIVED"))
		{
			// 取消广播（这行代码将会让系统收不到短信）
			abortBroadcast();  // ①
			StringBuilder sb = new StringBuilder();
			// 接收由SMS传过来的数据
			Bundle bundle = intent.getExtras();
			// 判断是否有数据
			if (bundle != null)
			{
				// 通过pdus可以获得接收到的所有短信消息
				Object[] pdus = (Object[]) bundle.get("pdus");
				// 构建短信对象array,并依据收到的对象长度来创建array的大小
				SmsMessage[] messages = new SmsMessage[pdus.length];
				for (int i = 0; i < pdus.length; i++)
				{
					messages[i] = SmsMessage
							.createFromPdu((byte[]) pdus[i]);
				}
				// 将发送来的短信合并自定义信息于StringBuilder当中
				for (SmsMessage message : messages)
				{
					sb.append("短信来源:");
					// 获得接收短信的电话号码
					sb.append(message.getDisplayOriginatingAddress());
					sb.append("\n------短信内容------\n");
					// 获得短信的内容
					sb.append(message.getDisplayMessageBody());
				}
			}
			Toast.makeText(context, sb.toString()
					, Toast.LENGTH_LONG).show();
		}
	}
```
电量提醒
```
<uses-permission android:name="android.permission.BATTERY_STATS"/>

<receiver android:name=".BatteryReceiver">
			<!-- 监听电池电量改变 -->
			<intent-filter>
				<action android:name="android.intent.action.BATTERY_CHANGED" />
			</intent-filter>
		</receiver>

package org.crazyit.broadcast;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.os.Bundle;
import android.widget.Toast;

public class BatteryReceiver extends BroadcastReceiver
{
	@Override
	public void onReceive(Context context, Intent intent)
	{
		System.out.println("+++++++++++++++++++++++");
		Bundle bundle = intent.getExtras();
		// 获取当前电量
		int current = bundle.getInt("level");
		// 获取总电量
		int total = bundle.getInt("scale");
		// 如果当前电量小于总电量的15%
		if (current * 1.0 / total < 0.15)
		{
			Toast.makeText(context, "电量过低，请尽快充电！"
					, Toast.LENGTH_LONG).show();
		}
	}
}

```
<h1 id="0301">基于监听的事件处理</h1>

[返回目录](#1) 

就是界面组件绑定特定的事件监听器。是一种更面向对象的事件处理。分为事件源，事件，事件监听器（一个特殊的Java对象）。是一种委派式的事件处理方式。
回调，就是重写组件特定的回调方法，或重写Activity的回调方法。处理一些具有通用性的事件。

[基于监听的事件处理模型](#0301_1)
[事件和事件监听器](#0301_2)
[外部类作为事件监听器类](#0301_3)
Activity本身作为事件监听器。
匿名内部类作为事件监听器
还有一种就是直接绑定到标签

<h1 id="0301_1">基于监听的事件处理模型</h1>

[返回目录](#0301) 

```
// 获取应用程序中的bn按钮
		Button bn = (Button) findViewById(R.id.bn);
		// 为按钮绑定事件监听器
		bn.setOnClickListener(new MyClickListener()); // ①


// 定义一个单击事件的监听器
	class MyClickListener implements View.OnClickListener
	{
		// 实现监听器类必须实现的方法，该方法将会作为事件处理器
		@Override
		public void onClick(View v)
		{
			EditText txt = (EditText) findViewById(R.id.txt);
			txt.setText("bn按钮被单击了！");
		}
	}
```
<h1 id="0301_2">事件和事件监听器</h1>

[返回目录](#0301) 

这种多数采用内部类作为事件监听器，可以访问调用它的各个内部组件，所以比较普及。

![](http://i.imgur.com/3w0Qi2K.jpg)

绘制一个飞机
```
package org.crazyit.event;

import android.content.Context;
import android.graphics.Bitmap;
import android.graphics.BitmapFactory;
import android.graphics.Canvas;
import android.graphics.Paint;
import android.view.View;

public class PlaneView extends View
{//通过设置这两个值，来设计飞机的位置
	public float currentX;
	public float currentY;
	Bitmap plane;
	public PlaneView(Context context)
	{
		super(context);
		// 定义飞机图片
		plane = BitmapFactory.decodeResource(context.getResources(),
			R.drawable.plane);
		setFocusable(true);
	}
	@Override
	public void onDraw(Canvas canvas)
	{
		super.onDraw(canvas);
		// 创建画笔
		Paint p = new Paint();
		// 绘制飞机
		canvas.drawBitmap(plane, currentX, currentY, p);
	}
}

```
启动键盘的事件监听器
```
package org.crazyit.event;

import android.app.Activity;
import android.os.Bundle;
import android.util.DisplayMetrics;
import android.view.Display;
import android.view.KeyEvent;
import android.view.View;
import android.view.View.OnKeyListener;
import android.view.Window;
import android.view.WindowManager;


public class MainActivity extends Activity
{
	// 定义飞机的移动速度
	private int speed = 10;
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		// 去掉窗口标题
		requestWindowFeature(Window.FEATURE_NO_TITLE);
		// 全屏显示
		getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN,
				WindowManager.LayoutParams.FLAG_FULLSCREEN);
		// 创建PlaneView组件
		final PlaneView planeView = new PlaneView(this);
		setContentView(planeView);
		planeView.setBackgroundResource(R.drawable.back);
		// 获取窗口管理器
		WindowManager windowManager = getWindowManager();
		Display display = windowManager.getDefaultDisplay();
		DisplayMetrics metrics = new DisplayMetrics();
		// 获得屏幕宽和高
		display.getMetrics(metrics);
		// 设置飞机的初始位置
		planeView.currentX = metrics.widthPixels / 2;
		planeView.currentY = metrics.heightPixels - 100;
		// 为planeView组件的键盘事件绑定监听器
		planeView.setOnKeyListener(new OnKeyListener()
		{
			@Override
			public boolean onKey(View source, int keyCode, KeyEvent event)
			{
				// 获取由哪个键触发的事件
				switch (event.getKeyCode())
				{
					// 控制飞机下移
					case KeyEvent.KEYCODE_S:
						planeView.currentY += speed;
						break;
					// 控制飞机上移
					case KeyEvent.KEYCODE_W:
						planeView.currentY -= speed;
						break;
					// 控制飞机左移
					case KeyEvent.KEYCODE_A:
						planeView.currentX -= speed;
						break;
					// 控制飞机右移
					case KeyEvent.KEYCODE_D:
						planeView.currentX += speed;
						break;
				}
				// 通知planeView组件重绘
				planeView.invalidate();
				return true;
			}
		});
	}
}


```
<h1 id="0301_3">外部类作为事件监听器类</h1>

[返回目录](#0301) 

能为多个界面所共享，完成某种业务逻辑。可以写成抽象方法，运用泛型，调用的时候再去试下接口的方法。
![](http://i.imgur.com/nYP6fHt.jpg)

定义的外部类监听器
```
package org.crazyit.event;

import android.app.Activity;
import android.app.PendingIntent;
import android.content.Intent;
import android.telephony.SmsManager;
import android.view.View;
import android.view.View.OnLongClickListener;
import android.widget.EditText;
import android.widget.Toast;

public class SendSmsListener implements OnLongClickListener
{
	private Activity act;
	private EditText address;
	private EditText content;
	public SendSmsListener(Activity act, EditText address
		, EditText content)
	{
		this.act = act;
		this.address = address;
		this.content = content;
	}
	@Override
	public boolean onLongClick(View source)
	{
		String addressStr = address.getText().toString();
		String contentStr = content.getText().toString();
		// 获取短信管理器 负责发送短信
		SmsManager smsManager = SmsManager.getDefault();
		// 创建发送短信的PendingIntent
		PendingIntent sentIntent = PendingIntent.getBroadcast(act
				, 0, new Intent(), 0);
		// 发送文本短信
		smsManager.sendTextMessage(addressStr, null, contentStr
				, sentIntent, null);
		Toast.makeText(act, "短信发送完成", Toast.LENGTH_LONG).show();
		return false;
	}
}

```
界面调用外部类的逻辑
```
package org.crazyit.event;

import android.app.Activity;
import android.os.Bundle;
import android.view.Menu;
import android.view.MenuItem;
import android.widget.Button;
import android.widget.EditText;


public class MainActivity extends Activity
{
	EditText address;
	EditText content;
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		setContentView(R.layout.main);
		// 获取页面中收件人地址、短信内容
		address = (EditText)findViewById(R.id.address);
		content = (EditText)findViewById(R.id.content);
		Button bn = (Button)findViewById(R.id.send);
		// 使用外部类的实例作为事件监听器
		bn.setOnLongClickListener(new SendSmsListener(
			this , address, content));
	}
}

```
<h1 id="0302">基于回调的事件处理</h1>

[返回目录](#1) 

基于回调的事件处理模型，事件源和事件监听器是统一的。安卓为所有的组件提供了一些事件处理的回调方法。

[基于回调的事件传播](#0302_1)
[通过回调实现跟随手指的小球](#0302_2)

<h1 id="0302_1">基于回调的事件传播</h1>

[返回目录](#0302) 

这个没能实现，总是出现错误。
![](http://i.imgur.com/x5deVDB.jpg)
系统最先触发的是按键上绑定的事件监听器
```
Button bn = (Button) findViewById(R.id.bn);
		// 为bn绑定事件监听器
		bn.setOnKeyListener(new OnKeyListener() {
			@Override
			public boolean onKey(View source
					, int keyCode, KeyEvent event) {
				// 只处理按下键的事件
				if (event.getAction() == KeyEvent.ACTION_DOWN) {
					Log.v("-Listener-", "the onKeyDown in Listener");
				}
				// 返回false，表明该事件会向外传播
				return true; // ①
			}
		});
```
然后触发的是组件提供的事件回调方法
```
package org.crazyit.event;

import android.content.Context;
import android.util.AttributeSet;
import android.util.Log;
import android.view.KeyEvent;
import android.widget.Button;

public class MyButton extends Button
{
	public MyButton(Context context , AttributeSet set)
	{
		super(context , set);
	}
	@Override
	public boolean onKeyDown(int keyCode, KeyEvent event)
	{
		super.onKeyDown(keyCode , event);
		Log.v("-MyButton-", "the onKeyDown in MyButton");
		// 返回false，表明并未完全处理该事件，该事件依然向外扩散
		return false;
	}
}

```
最后传播到组件所在的Activity
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
	android:orientation="vertical"
	android:layout_width="match_parent"
	android:layout_height="match_parent"
	>
	<!-- 使用自定义View时应使用全限定类名 -->
	<studydiary.tyq.com.ceshi1.MyButton
		android:id="@+id/bn"
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:text="单击我"/>
</LinearLayout>


// 重写onKeyDown方法，该方法可监听它所包含的所有组件的按键被按下事件
	@Override
	public boolean onKeyDown(int keyCode, KeyEvent event)
	{
		super.onKeyDown(keyCode , event);
		Log.v("-Activity-" , "the onKeyDown in Activity");
		//返回false，表明并未完全处理该事件，该事件依然向外扩散
		return false;
	}
```
如果任何一个事件处理方法返回true，事件将不会继续向外传播。如果返回false，事件将会继续传播到下一层。

<h1 id="0302_2">通过回调实现跟随手指的小球</h1>

[返回目录](#0302) 

![](http://i.imgur.com/Mbatq5N.jpg)
通过回调的方法把事件处理方法封装在View内部，可以提高程序的内聚性，更适合处理事件逻辑比较固定的view
```
<!-- 使用自定义组件 -->
	<org.crazyit.event.DrawView
		android:orientation="vertical"
		android:layout_width="match_parent"
		android:layout_height="match_parent"/>

package org.crazyit.event;

import android.content.Context;
import android.graphics.Canvas;
import android.graphics.Color;
import android.graphics.Paint;
import android.util.AttributeSet;
import android.view.MotionEvent;
import android.view.View;

public class DrawView extends View
{
	public float currentX = 40;
	public float currentY = 50;
	// 定义、创建画笔
	Paint p = new Paint();
	public DrawView(Context context, AttributeSet set)
	{
		super(context, set);
	}
	//这个方法在两个地方调用  一个是刚开始的时候，一个是重绘的时候
	// 画布的大小就是这个控件的大小
	@Override
	public void onDraw(Canvas canvas)
	{
		super.onDraw(canvas);
		// 设置画笔的颜色
		p.setColor(Color.RED);
		// 绘制一个小圆（作为小球） 15为半径
		canvas.drawCircle(currentX, currentY, 15, p);
	}
	@Override
	public boolean onTouchEvent(MotionEvent event)
	{
		// 当前组件的currentX、currentY两个属性
		this.currentX = event.getX();
		this.currentY = event.getY();
		// 通知改组件重绘
		this.invalidate();
		// 返回true表明处理方法已经处理该事件
		return true;
	}
}

```
<h1 id="0303">相应系统设置的事件和响应系统设置的更改</h1>

[返回目录](#1) 

![](http://i.imgur.com/UFhuiAv.jpg)
![](http://i.imgur.com/kd9Dvx3.jpg)
```
bn.setOnClickListener(new OnClickListener()
		{
			// 为按钮绑定事件监听器
			@Override
			public void onClick(View source)
			{
				// 获取系统的Configuration对象
				Configuration cfg = getResources().getConfiguration();
				
				String screen = cfg.orientation ==
					Configuration.ORIENTATION_LANDSCAPE
					? "横向屏幕": "竖向屏幕";
				//这个是移动网络代号
				String mncCode = cfg.mnc + "";
				
				String naviName = cfg.orientation ==
					Configuration.NAVIGATION_NONAV
					? "没有方向控制" :
					cfg.orientation == Configuration.NAVIGATION_WHEEL
						? "滚轮控制方向" :
						cfg.orientation == Configuration.NAVIGATION_DPAD
						? "方向键控制方向" : "轨迹球控制方向";
				navigation.setText(naviName);
				
				String touchName = cfg.touchscreen ==
					Configuration.TOUCHSCREEN_NOTOUCH
					? "无触摸屏" : "支持触摸屏";
				ori.setText(screen);
				mnc.setText(mncCode);
				touch.setText(touchName);
			}
		});
```
响应系统设置的更改
![](http://i.imgur.com/k6trkeS.jpg)
```
<!-- 设置Activity可以监听屏幕方向改变的事件 -->
		<activity
			android:configChanges="orientation|screenSize"
			android:name=".MainActivity"
			android:label="@string/app_name" >
			<intent-filter>
				<action android:name="android.intent.action.MAIN" />
				<category android:name="android.intent.category.LAUNCHER" />
			</intent-filter>
		</activity>


Button bn = (Button) findViewById(R.id.bn);
		// 为按钮绑定事件监听器
		bn.setOnClickListener(new OnClickListener() {
			@Override
			public void onClick(View source) {
				Configuration config = getResources().getConfiguration();
				// 如果当前是横屏
				if (config.orientation == Configuration.ORIENTATION_LANDSCAPE) {
					// 设为竖屏
					MainActivity.this.setRequestedOrientation(
						ActivityInfo.SCREEN_ORIENTATION_PORTRAIT);
				}
				// 如果当前是竖屏
				if (config.orientation == Configuration.ORIENTATION_PORTRAIT) {
					// 设为横屏
					MainActivity.this.setRequestedOrientation(
						ActivityInfo.SCREEN_ORIENTATION_LANDSCAPE);
				}
			}
		});


// 重写该方法，用于监听系统设置的更改，主要是监控屏幕方向的更改
	@Override
	public void onConfigurationChanged(Configuration newConfig)
	{
		super.onConfigurationChanged(newConfig);
		String screen = newConfig.orientation ==
			Configuration.ORIENTATION_LANDSCAPE ? "横向屏幕" : "竖向屏幕";
		Toast.makeText(this, "系统的屏幕方向发生改变" + "\n修改后的屏幕方向为："
				+ screen, Toast.LENGTH_LONG).show();
	}

```
<h1 id="0304">Handler消息传递机制</h1>

[返回目录](#1) 

[自动播放的动画](#0304_1)
[使用新线程计算质数](#0304_2)

主线程Main Thread，把相关的事件分发给对应的组件去处理。Handler是另外一种形式的事件处理，主要是为了解决多线程的问题，它允许新线程周期性的改变界面组件的属性值。

# 作用有两个：
1 在新线程中发送消息。
2在主线程中获取和处理消息。
原理 主要是通过回调的方式来实现。

<h1 id="0304_1">自动播放的动画</h1>

[返回目录](#0304) 

![](http://i.imgur.com/BMXLoWF.jpg)
```
package org.crazyit.handler;

import android.app.Activity;
import android.os.Bundle;
import android.os.Handler;
import android.os.Message;
import android.view.Menu;
import android.view.MenuItem;
import android.widget.ImageView;

import java.util.Timer;
import java.util.TimerTask;

public class MainActivity extends Activity
{
	// 定义周期性显示的图片的ID
	int[] imageIds = new int[]
		{
			R.drawable.java,
			R.drawable.javaee,
			R.drawable.ajax,
			R.drawable.android,
			R.drawable.swift
		};
	int currentImageId = 0;
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		setContentView(R.layout.main);
		final ImageView show = (ImageView) findViewById(R.id.show);
		final Handler myHandler = new Handler()
		{
			@Override
			public void handleMessage(Message msg)
			{
				// 如果该消息是本程序所发送的
				if (msg.what == 0x1233)
				{
					// 动态地修改所显示的图片
					show.setImageResource(imageIds[currentImageId++
							% imageIds.length]);
				}
			}
		};
		// 定义一个计时器，让该计时器周期性地执行指定任务
		//TimerTask 本质就是启动一条新线程
		new Timer().schedule(new TimerTask()
		{
			@Override
			public void run()
			{
				// 发送空消息
				myHandler.sendEmptyMessage(0x1233);
			}
		}, 0, 1200);
	}
}


```
<h1 id="0304_2">使用新线程计算质数</h1>

[返回目录](#0304) 

Message Handler接受和处理的消息对象
Looper 每个线程只能有一个，它的loop方法复制读取MessageQueue中的消息，读到消息之后就把消息交给发送消息的Handler进行处理。
MessageQueue 消息队列，采用先进先从的方式来管理Message，
程序创建Looper对象是，会在他的构造器中创建MessageQueue对象。

程序员自己启动的线程，必须自己创建一个Looper对象，并启动它，也就是调用它的prepare()方法。这个方法保证每个线程最多只有一个Looper对象。Looper对象调用静态的loop（）方法，使用一个死循环不断的取出MessageQueue中的消息。

![](http://i.imgur.com/kv3MNEv.jpg)
```
package org.crazyit.handler;

import android.app.Activity;
import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.os.Message;
import android.view.View;
import android.widget.EditText;
import android.widget.Toast;

import java.util.ArrayList;
import java.util.List;

public class MainActivity extends Activity
{
	static final String UPPER_NUM = "upper";
	EditText etNum;
	CalThread calThread;
	// 定义一个线程类
	class CalThread extends Thread
	{
		public Handler mHandler;
		public void run()
		{
			Looper.prepare();//创建一个Looper的对象
			mHandler = new Handler()
			{
				// 定义处理消息的方法
				@Override
				public void handleMessage(Message msg)
				{
					if(msg.what == 0x123)
					{
						int upper = msg.getData().getInt(UPPER_NUM);
						List<Integer> nums = new ArrayList<Integer>();
						// 计算从2开始、到upper的所有质数
						outer:
						for (int i = 2 ; i <= upper ; i++)
						{
							// 用i除以从2开始、到i的平方根的所有数
							for (int j = 2 ; j <= Math.sqrt(i) ; j++)
							{
								// 如果可以整除，则表明这个数不是质数
								if(i != 2 && i % j == 0)
								{
									continue outer;
								}
							}
							nums.add(i);
						}
						// 使用Toast显示统计出来的所有质数  土司出来
						Toast.makeText(MainActivity.this, nums.toString()
							, Toast.LENGTH_LONG).show();
					}
				}
			};
			Looper.loop();//启动Looper
		}
	}
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		setContentView(R.layout.main);
		etNum = (EditText)findViewById(R.id.etNum);
		calThread = new CalThread();
		// 启动新线程
		calThread.start();
	}
	// 为按钮的点击事件提供事件处理方法
	public void cal(View source)
	{
		// 创建消息
		Message msg = new Message();
		msg.what = 0x123;
		Bundle bundle = new Bundle();
		bundle.putInt(UPPER_NUM ,
				Integer.parseInt(etNum.getText().toString()));
		msg.setData(bundle);
		// 向新线程中的Handler发送消息
		calThread.mHandler.sendMessage(msg);
	}
}


```

<h1 id="0305">异步任务</h1>

[返回目录](#1) 

![](http://i.imgur.com/ZUj9Jj8.jpg)

针对新线程不能更新UI组件的问题，几种方案
1 使用Handler实现线程之间的通信
2 Activity.runOnUiThread(Runnable)
3 View.post(Runnable)
4 View.postDelayed(Runnable,long)
5 异步任务类。

规则
必须在UI线程中创建实例，
主线程中调用execute()方法。
每个AsyncTask只能被执行一次，多次调用将会引发异常。
```
package studydiary.tyq.com.ceshi1;
import android.app.Activity;
import android.app.ProgressDialog;
import android.content.Context;
import android.os.AsyncTask;
import android.os.Bundle;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.widget.TextView;

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.MalformedURLException;
import java.net.URL;
import java.net.URLConnection;

public class MainActivity extends Activity {
    private TextView show;
    @Override
    public void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
        show = (TextView) findViewById(R.id.show);
    }
    // 重写该方法，为界面的按钮提供事件响应方法
    public void download(View source) throws MalformedURLException
    {
        DownTask task = new DownTask(this);
        task.execute(new URL("http://211.149.169.221:8080/umijoyappsvr/distribution/DistributionUserList.do?start=0&limit=15"));
    }
    //三个泛型参数 Params 启动任务执行的输入参数的类型  Progress 后台任务完成的进度值的类型
    // Result 后台执行任务完成后返回结果的类型
    class DownTask extends AsyncTask<URL, Integer, String>
    {
        // 可变长的输入参数，与AsyncTask.exucute()对应
        ProgressDialog pdialog;
        // 定义记录已经读取行的数量
        int hasRead = 0;
        Context mContext;
        public DownTask(Context ctx)
        {
            mContext = ctx;
        }
        //后台线程将要完成的任务  调用publishProgress方法更新任务的执行进度
        @Override
        protected String doInBackground(URL... params)
        {
            StringBuilder sb = new StringBuilder();
            try
            {
                URLConnection conn = params[0].openConnection();
                // 打开conn连接对应的输入流，并将它包装成BufferedReader
                BufferedReader br = new BufferedReader(
                        new InputStreamReader(conn.getInputStream()
                                , "utf-8"));
                String line = null;
                while ((line = br.readLine()) != null)
                {
                    sb.append(line + "\n");
                    hasRead++;
                    publishProgress(hasRead);
                }
                //这个的值有onPostExecute 接受和使用这个值
                return sb.toString();
            }
            catch (Exception e)
            {
                e.printStackTrace();
            }
            return null;
        }
        //当doInBackground（）完成后，系统后自动调用该方法。并将doInBackground()方法的返回值传给该方法。
        @Override
        protected void onPostExecute(String result)
        {
            // 返回HTML页面的内容
            show.setText(result);
            pdialog.dismiss();
        }
        //这个方法将在耗时操作启动前调用，做一些初始化的准备工作
        @Override
        protected void onPreExecute()
        {
            pdialog = new ProgressDialog(mContext);
            // 设置对话框的标题
            pdialog.setTitle("任务正在执行中");
            // 设置对话框显示的内容
            pdialog.setMessage("任务正在执行中，敬请等待...");
            // 设置对话框不能用“取消”按钮关闭
            pdialog.setCancelable(false);
            // 设置该进度条的最大进度值
            pdialog.setMax(202);
            // 设置对话框的进度条风格
            pdialog.setProgressStyle(ProgressDialog.STYLE_HORIZONTAL);
            // 设置对话框的进度条是否显示进度
            pdialog.setIndeterminate(false);
            pdialog.show();
        }

        //在doInBackground()方法中调用publishProgress()方法更新任务的执行进度后，触发该方法
        @Override
        protected void onProgressUpdate(Integer... values)
        {
            // 更新进度
            show.setText("已经读取了【" + values[0] + "】行！");
            pdialog.setProgress(values[0]);
        }
    }
}

```
<h1 id="0401">1. 使用Activity</h1>

[返回目录](#1) 

[配置设置参数的Activity](#0401_1)
[Activity跳转时交换数据](#0401_2)
[启动Activity并返回结果](#0401_3)
[Activity生命周期和加载模式](#0401_4)

![](http://i.imgur.com/mt8fJNc.jpg)

一个点击项对应一个参数
```
public class MainActivity extends LauncherActivity
{
	//定义两个Activity的名称
	String[] names = {"设置程序参数" ,  "查看星际兵种"};
	//定义两个Activity对应的实现类
	Class<?>[] clazzs = {PreferenceActivityTest.class
			, ExpandableListActivityTest.class};
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		ArrayAdapter<String> adapter = new ArrayAdapter<String>(this,
				android.R.layout.simple_list_item_1 , names);
		// 设置该窗口显示的列表所需的Adapter
		setListAdapter(adapter);
	}
	//根据列表项返回指定Activity对应的Intent
	@Override
	public Intent intentForPosition(int position)
	{
		return new Intent(MainActivity.this , clazzs[position]);
	}
}
```
![](http://i.imgur.com/gTR38SP.jpg)

```
package org.crazyit.app;

import android.app.ExpandableListActivity;
import android.os.Bundle;
import android.view.Gravity;
import android.view.View;
import android.view.ViewGroup;
import android.widget.AbsListView;
import android.widget.BaseExpandableListAdapter;
import android.widget.ExpandableListAdapter;
import android.widget.ImageView;
import android.widget.LinearLayout;
import android.widget.TextView;

public class ExpandableListActivityTest extends ExpandableListActivity
{
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		ExpandableListAdapter adapter = new BaseExpandableListAdapter()
		{
			//以下是设置内部类的变量
			int[] logos = new int[]
					{
							R.drawable.p,
							R.drawable.z,
							R.drawable.t
					};
			private String[] armTypes = new String[]
					{ "神族兵种", "虫族兵种", "人族兵种"};
			private String[][] arms = new String[][]
					{
							{ "狂战士", "龙骑士", "黑暗圣堂", "电兵" },
							{ "小狗", "刺蛇", "飞龙", "自爆飞机" },
							{ "机枪兵", "护士MM" , "幽灵" }
					};
			//获取指定组位置、指定子列表项处的子列表项数据
			@Override
			public Object getChild(int groupPosition, int childPosition)
			{
				return arms[groupPosition][childPosition];
			}
			@Override
			public long getChildId(int groupPosition, int childPosition)
			{
				return childPosition;
			}
			@Override
			public int getChildrenCount(int groupPosition)
			{
				return arms[groupPosition].length;
			}
			//自定义一个文本框
			private TextView getTextView()
			{
				AbsListView.LayoutParams lp = new AbsListView.LayoutParams(
						ViewGroup.LayoutParams.MATCH_PARENT, 64);
				TextView textView = new TextView(ExpandableListActivityTest.
						this);
				textView.setLayoutParams(lp);
				textView.setGravity(Gravity.CENTER_VERTICAL | Gravity.LEFT);
				textView.setPadding(36, 0, 0, 0);
				textView.setTextSize(20);
				return textView;
			}
			//该方法决定每个子选项的外观
			@Override
			public View getChildView(int groupPosition, int childPosition,
									 boolean isLastChild, View convertView, ViewGroup parent)
			{
				TextView textView = getTextView();
				textView.setText(getChild(groupPosition, childPosition).
						toString());
				return textView;
			}
			//获取指定组位置处的组数据
			@Override
			public Object getGroup(int groupPosition)
			{
				return armTypes[groupPosition];
			}
			@Override
			public int getGroupCount()
			{
				return armTypes.length;
			}
			@Override
			public long getGroupId(int groupPosition)
			{
				return groupPosition;
			}
			//该方法决定每个组选项的外观
			@Override
			public View getGroupView(int groupPosition, boolean isExpanded,
									 View convertView, ViewGroup parent)
			{
				LinearLayout ll = new LinearLayout(
						ExpandableListActivityTest.this);
				ll.setOrientation(LinearLayout.HORIZONTAL);
				ImageView logo = new ImageView(
						ExpandableListActivityTest.this);
				logo.setImageResource(logos[groupPosition]);
				ll.addView(logo);
				TextView textView = getTextView();
				textView.setText(getGroup(groupPosition).toString());
				ll.addView(textView);
				return ll;
			}
			@Override
			public boolean isChildSelectable(int groupPosition,
											 int childPosition)
			{
				return true;
			}
			@Override
			public boolean hasStableIds()
			{
				return true;
			}
		};
		// 设置该窗口显示列表
		setListAdapter(adapter);
	}
}
``` 
<h1 id="0401_1">1. 配置设置参数的Activity</h1>
 
[返回目录](#0401) 
![](http://i.imgur.com/GEnQHlf.jpg)

app节点 右键 Android resource file建立资源文件
布局是
``` 
<?xml version="1.0" encoding="utf-8"?>
<preference-headers
	xmlns:android="http://schemas.android.com/apk/res/android">
	<!-- 指定启动指定PreferenceFragment的列表项 -->
	<header android:fragment=
				"utilcode.tyq.com.ceshi4.PreferenceActivityTest$Prefs1Fragment"
			android:icon="@drawable/ic_settings_applications"
			android:title="程序选项设置"
			android:summary="设置应用的相关选项" />
	<!-- 指定启动指定PreferenceFragment的列表项 -->
	<header android:fragment=
				"utilcode.tyq.com.ceshi4.PreferenceActivityTest$Prefs2Fragment"
			android:icon="@drawable/ic_settings_display"
			android:title="界面选项设置 "
			android:summary="设置显示界面的相关选项">
		<!-- 使用extra可向Activity传入额外的数据 -->
		<extra android:name="website"
			   android:value="www.crazyit.org" />
	</header>
	<!-- 使用Intent启动指定Activity的列表项 -->
	<header
		android:icon="@drawable/ic_settings_display"
		android:title="使用Intent"
		android:summary="使用Intent启动某个Activity">
		<intent android:action="android.intent.action.VIEW"
				android:data="http://www.crazyit.org" />
	</header>
</preference-headers>

``` 
实现的代码是
``` 
package utilcode.tyq.com.ceshi4;

import android.os.Bundle;
import android.preference.PreferenceActivity;
import android.preference.PreferenceFragment;
import android.widget.Button;
import android.widget.Toast;

import java.util.List;

public class PreferenceActivityTest extends PreferenceActivity
{
	@Override
	protected void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		// 该方法用于为该界面设置一个标题按钮
		if (hasHeaders())
		{
			Button button = new Button(this);
			button.setText("设置操作");
			// 将该按钮添加到该界面上
			setListFooter(button);
		}
	}
	// 重写该该方法，负责加载页面布局文件
	@Override
	public void onBuildHeaders(List<Header> target)
	{
		// 加载选项设置列表的布局文件
		loadHeadersFromResource(R.xml.preference_headers, target);
	}
	// 重写该方法，验证各PreferenceFragment是否有效
	@Override
	public boolean isValidFragment(String fragmentName)
	{
		return true;
	}
	//这个是内部类 Fragment
	public static class Prefs1Fragment extends PreferenceFragment
	{
		@Override
		public void onCreate(Bundle savedInstanceState)
		{
			super.onCreate(savedInstanceState);
			addPreferencesFromResource(R.xml.preferences);
		}
	}
	public static class Prefs2Fragment extends PreferenceFragment
	{
		@Override
		public void onCreate(Bundle savedInstanceState)
		{
			super.onCreate(savedInstanceState);
			addPreferencesFromResource(R.xml.display_prefs);
			// 获取传入该Fragment的参数
			String website = getArguments().getString("website");
			Toast.makeText(getActivity()
					, "网站域名是：" + website , Toast.LENGTH_LONG).show();
		}
	}
}
``` 
两个Fragment的布局是
![](http://i.imgur.com/f8YN01o.jpg)
``` 
<?xml version="1.0" encoding="utf-8"?>
<PreferenceScreen
	xmlns:android="http://schemas.android.com/apk/res/android">
	<!-- 设置系统铃声 -->
	<RingtonePreference
		android:ringtoneType="all"
		android:title="设置铃声"
		android:summary="选择铃声（测试RingtonePreference)"
		android:showDefault="true"
		android:key="ring_key"
		android:showSilent="true">
	</RingtonePreference>
	<PreferenceCategory android:title="个人信息设置组">
		<!-- 通过输入框填写用户名 -->
		<EditTextPreference
			android:key="name"
			android:title="填写用户名"
			android:summary="填写您的用户名（测试EditTextPreference)"
			android:dialogTitle="您所使用的用户名为：" />
		<!-- 通过列表框选择性别 -->
		<ListPreference
			android:key="gender"
			android:title="性别"
			android:summary="选择您的性别（测试ListPreference）"
			android:dialogTitle="ListPreference"
			android:entries="@array/gender_name_list"
			android:entryValues="@array/gender_value_list" />
	</PreferenceCategory>
	<PreferenceCategory android:title="系统功能设置组 ">
		<CheckBoxPreference
			android:key="autoSave"
			android:title="自动保存进度"
			android:summaryOn="自动保存: 开启"
			android:summaryOff="自动保存: 关闭"
			android:defaultValue="true" />
	</PreferenceCategory>
</PreferenceScreen>
``` 
![](http://i.imgur.com/r3DdCDN.jpg)
``` 
<?xml version="1.0" encoding="utf-8"?>
<PreferenceScreen
    xmlns:android="http://schemas.android.com/apk/res/android">
<PreferenceCategory android:title="背景灯光组">
	<!-- 通过列表框选择灯光强度 -->
	<ListPreference
		android:key="light"
		android:title="灯光强度"
		android:summary="请选择灯光强度（测试ListPreference）"
		android:dialogTitle="请选择灯光强度"
		android:entries="@array/light_strength_list"
		android:entryValues="@array/light_value_list" />
</PreferenceCategory>
<PreferenceCategory android:title="文字显示组 ">
	<!-- 通过SwitchPreference设置是否自动滚屏 -->
	<SwitchPreference
		android:key="autoScroll"
		android:title="自动滚屏"
		android:summaryOn="自动滚屏: 开启"
		android:summaryOff="自动滚屏: 关闭"
		android:defaultValue="true" />
</PreferenceCategory>
</PreferenceScreen>

``` 
<h1 id="0401_2">1. Activity跳转时携带参数</h1>
 
[返回目录](#0401) 
![](http://i.imgur.com/1kkbZZm.jpg)
实现的代码
``` 
定义的可实例化对象
public class Person implements Serializable{
public Person(String name, String passwd, String gender) {
		this.name = name;
		this.passwd = passwd;
		this.gender = gender;
	}
}


传递数据
EditText name = (EditText)findViewById(R.id.name);
				EditText passwd = (EditText)findViewById(R.id.passwd);
				RadioButton male = (RadioButton) findViewById(R.id.male);
				String gender = male.isChecked() ? "男 " : "女";
				Person p = new Person(name.getText().toString(), passwd
						.getText().toString(), gender);
				// 创建一个Bundle对象
				Bundle data = new Bundle();
				data.putSerializable("person", p);
				// 创建一个Intent
				Intent intent = new Intent(MainActivity.this,
						ResultActivity.class);
				intent.putExtras(data);
				// 启动intent对应的Activity
				startActivity(intent);

接受数据
// 获取启动该Activity的Intent
		Intent intent = getIntent();
		// 直接通过Intent取出它所携带的Bundle数据包中的数据
		Person p = (Person) intent.getSerializableExtra("person");
		name.setText("您的用户名为：" + p.getName());
		passwd.setText("您的密码为：" + p.getPasswd());
		gender.setText("您的性别为：" + p.getGender());

``` 
这个布局有网格布局来实现 
``` 
<?xml version="1.0" encoding="utf-8"?>
<TableLayout xmlns:android="http://schemas.android.com/apk/res/android"
	android:layout_width="match_parent"
	android:layout_height="match_parent">
	<TextView
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:text="请输入您的注册信息"
		android:textSize="20sp"/>
	这个是网格布局的一列
	<TableRow>
		<TextView
			android:layout_width="match_parent"
			android:layout_height="wrap_content"
			android:text="用户名:"
			android:textSize="16sp"/>
		<!-- 定义一个EditText，用于收集用户的账号 -->
		<EditText
			android:id="@+id/name"
			android:layout_width="match_parent"
			android:layout_height="wrap_content"
			android:hint="请填写想注册的账号"
			android:selectAllOnFocus="true"/>
	</TableRow>
	这个是网格布局的一列
	<TableRow>
		<TextView
			android:layout_width="match_parent"
			android:layout_height="wrap_content"
			android:text="密码:"
			android:textSize="16sp"/>
		<!-- 用于收集用户的密码 -->
		<EditText
			android:id="@+id/passwd"
			android:layout_width="match_parent"
			android:layout_height="wrap_content"
			android:password="true"
			android:selectAllOnFocus="true"/>
	</TableRow>
	<TableRow>
		<TextView
			android:layout_width="match_parent"
			android:layout_height="wrap_content"
			android:text="性别:"
			android:textSize="16sp"/>
		<!-- 定义一组单选框，用于收集用户注册的性别 -->
		<RadioGroup
			android:layout_width="match_parent"
			android:layout_height="wrap_content"
			android:orientation="horizontal">
			<RadioButton
				android:id="@+id/male"
				android:layout_width="wrap_content"
				android:layout_height="wrap_content"
				android:text="男"
				android:textSize="16sp"/>
			<RadioButton
				android:id="@+id/female"
				android:layout_width="wrap_content"
				android:layout_height="wrap_content"
				android:text="女"
				android:textSize="16sp"/>
		</RadioGroup>
	</TableRow>
	<Button
		android:id="@+id/bn"
		android:layout_width="wrap_content"
		android:layout_height="wrap_content"
		android:text="注册"
		android:textSize="16sp"/>
</TableLayout>
``` 
<h1 id="0401_3">1. 启动Activity并返回结果</h1>
 
[返回目录](#0401) 
![](http://i.imgur.com/BP4lcxD.jpg)
![](http://i.imgur.com/vRdCHez.jpg)
启动页面代码
``` 
// 创建需要对应于目标Activity的Intent
				Intent intent = new Intent(MainActivity.this,
						SelectCityActivity.class);
				// 启动指定Activity并等待返回的结果，其中0是请求码，用于标识该请求
				startActivityForResult(intent, 0);


// 重写该方法，该方法以回调的方式来获取指定Activity返回的结果
	@Override
	public void onActivityResult(int requestCode
			, int resultCode, Intent intent)
	{
		// 当requestCode、resultCode同时为0时，也就是处理特定的结果
		if (requestCode == 0 && resultCode == 0)
		{
			// 取出Intent里的Extras数据
			Bundle data = intent.getExtras();
			// 取出Bundle中的数据
			String resultCity = data.getString("city");
			// 修改city文本框的内容
			city.setText(resultCity);
		}
	}
``` 
返回数据页面代码 
``` 
package org.crazyit.app;

import android.app.ExpandableListActivity;
import android.content.Intent;
import android.os.Bundle;
import android.view.Gravity;
import android.view.View;
import android.view.ViewGroup;
import android.widget.AbsListView;
import android.widget.BaseExpandableListAdapter;
import android.widget.ExpandableListAdapter;
import android.widget.ExpandableListView;
import android.widget.ExpandableListView.OnChildClickListener;
import android.widget.ImageView;
import android.widget.LinearLayout;
import android.widget.TextView;

public class SelectCityActivity extends ExpandableListActivity
{
	// 定义省份数组
	private String[] provinces = new String[]
		{ "广东", "广西", "湖南"};
	private String[][] cities = new String[][]
		{
			{ "广州", "深圳", "珠海", "中山" },
			{ "桂林", "柳州", "南宁", "北海" },
			{ "长沙", "岳阳" , "衡阳" , "株洲" }
		};
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		ExpandableListAdapter adapter = new BaseExpandableListAdapter()
		{
			// 获取指定组位置、指定子列表项处的子列表项数据
			@Override
			public Object getChild(int groupPosition, int childPosition)
			{
				return cities[groupPosition][childPosition];
			}
			@Override
			public long getChildId(int groupPosition, int childPosition)
			{
				return childPosition;
			}
			@Override
			public int getChildrenCount(int groupPosition)
			{
				return cities[groupPosition].length;
			}
			private TextView getTextView()
			{
				AbsListView.LayoutParams lp = new AbsListView.LayoutParams(
						ViewGroup.LayoutParams.MATCH_PARENT, 64);
				TextView textView = new TextView(SelectCityActivity.this);
				textView.setLayoutParams(lp);
				textView.setGravity(Gravity.CENTER_VERTICAL | Gravity.LEFT);
				textView.setPadding(36, 0, 0, 0);
				textView.setTextSize(20);
				return textView;
			}
			// 该方法决定每个子选项的外观
			@Override
			public View getChildView(int groupPosition, int childPosition,
				boolean isLastChild, View convertView, ViewGroup parent)
			{
				TextView textView = getTextView();
				textView.setText(getChild(groupPosition, childPosition)
						.toString());
				return textView;
			}
			// 获取指定组位置处的组数据
			@Override
			public Object getGroup(int groupPosition)
			{
				return provinces[groupPosition];
			}
			@Override
			public int getGroupCount()
			{
				return provinces.length;
			}
			@Override
			public long getGroupId(int groupPosition)
			{
				return groupPosition;
			}
			// 该方法决定每个组选项的外观
			@Override
			public View getGroupView(int groupPosition, boolean isExpanded,
				View convertView, ViewGroup parent)
			{
				LinearLayout ll = new LinearLayout(SelectCityActivity.this);
				ll.setOrientation(LinearLayout.HORIZONTAL);
				ImageView logo = new ImageView(SelectCityActivity.this);
				ll.addView(logo);
				TextView textView = getTextView();
				textView.setText(getGroup(groupPosition).toString());
				ll.addView(textView);
				return ll;
			}
			@Override
			public boolean isChildSelectable(int groupPosition,
				int childPosition)
			{
				return true;
			}
			@Override
			public boolean hasStableIds()
			{
				return true;
			}
		};
		// 设置该窗口显示列表
		setListAdapter(adapter);
		getExpandableListView().setOnChildClickListener(
			new OnChildClickListener()
			{
				@Override
				public boolean onChildClick(ExpandableListView parent,
					View source, int groupPosition, int childPosition,
											long id)
				{
					// 获取启动该Activity之前的Activity对应的Intent
					Intent intent = getIntent();
					intent.putExtra("city",
							cities[groupPosition][childPosition]);
					// 设置该SelectCityActivity的结果码，并设置结束之后退回的Activity
					SelectCityActivity.this.setResult(0, intent);
					// 结束SelectCityActivity。
					SelectCityActivity.this.finish();
					return false;
				}
			});
	}
}


``` 
<h1 id="0401_4">1. Activity生命周期和加载模式</h1>
 
[返回目录](#0401) 

![](http://i.imgur.com/MMAHp64.jpg)
Activity是有Task栈来管理的。
android:launchMode="singleTask"
# standard 标准模式 默认
![](http://i.imgur.com/N9hCTrg.jpg) 
tv.setText("Activity为：" + this.toString()
			+ "\n" + "，Task ID为:" + this.getTaskId());
不同的实例，所在的Task ID是相同的，但hashCode值有差异
# singleTop Task栈顶单例模式
实例在栈顶不创建，没在栈顶，就创建新实例。
# singleTask Task内单例模式
# singgleInstance 全局单例模式
```
<activity android:name=".SecondActivity"
				  android:label="@string/second"
				  <!-- 这个表明应用可以被其他隐形Intent调用 -->
				  android:exported="true"
				  android:launchMode="singleInstance">
			<intent-filter>
				<!-- 指定该Activity能响应Action为指定字符串的Intent -->
				<action android:name="org.crazyit.intent.action.CRAZYIT_ACTION" />
				<category android:name="android.intent.category.DEFAULT" />
			</intent-filter>
		</activity>
```
<h1 id="0402">1. Fragment</h1>
 
[返回目录](#1) 

这个被称为片段。

[显示详情的Fragment](#0402_1)
[兼顾屏幕分辨率的应用](#0402_2)
[Fragment的生命周期](#0402_3)
 
<h1 id="0402_1">显示详情的Fragment</h1>

[返回目录](#0402) 

![](http://i.imgur.com/bN4P7B1.jpg)

先自定义一个类
```
package utilcode.tyq.com.ceshi4;

import android.app.Activity;
import android.app.ListFragment;
import android.os.Bundle;
import android.view.View;
import android.widget.ArrayAdapter;
import android.widget.ListView;

public class BookListFragment extends ListFragment
{
	private Callbacks mCallbacks;
	// 定义一个回调接口，该Fragment所在Activity需要实现该接口
	// 该Fragment将通过该接口与它所在的Activity交换数据
	public interface Callbacks
	{
		public void onItemSelected(Integer id);
	}
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		// 为该ListFragment设置Adapter BookContent.ITEMS是放入了数据
		setListAdapter(new ArrayAdapter<BookContent.Book>(getActivity(),
				android.R.layout.simple_list_item_activated_1,
				android.R.id.text1, BookContent.ITEMS));  //①
	}
	// 当该Fragment被添加、显示到Activity时，回调该方法
	@Override
	public void onAttach(Activity activity)
	{
		super.onAttach(activity);
		// 如果Activity没有实现Callbacks接口，抛出异常
		if (!(activity instanceof Callbacks))
		{
			throw new IllegalStateException(
					"BookListFragment所在的Activity必须实现Callbacks接口!");
		}
		// 刚进入时 把该Activity当成Callbacks对象
		mCallbacks = (Callbacks)activity;
	}
	// 当该Fragment从它所属的Activity中被删除时回调该方法
	@Override
	public void onDetach()
	{
		super.onDetach();
		// 将mCallbacks赋为null。
		mCallbacks = null;
	}
	// 当用户单击某列表项时激发该回调方法
	@Override
	public void onListItemClick(ListView listView
		, View view, int position, long id)
	{
		super.onListItemClick(listView, view, position, id);
		// 激发mCallbacks的onItemSelected方法
		mCallbacks.onItemSelected(BookContent
				.ITEMS.get(position).id);
	}
	public void setActivateOnItemClick(boolean activateOnItemClick)
	{
		getListView().setChoiceMode(
			activateOnItemClick ? ListView.CHOICE_MODE_SINGLE
			: ListView.CHOICE_MODE_NONE);
	}
}

```
定义主要的布局，在主要的布局中加入自定义的类
```
<?xml version="1.0" encoding="utf-8"?>
<!-- 定义一个水平排列的LinearLayout，并指定使用中等分隔条 -->
<LinearLayout
	xmlns:android="http://schemas.android.com/apk/res/android"
	android:orientation="horizontal"
	android:layout_width="match_parent"
	android:layout_height="match_parent"
	android:layout_marginLeft="16dp"
	android:layout_marginRight="16dp"
	android:divider="?android:attr/dividerHorizontal"
	android:showDividers="middle">
	<!-- 添加一个Fragment 左边的目录 在设置布局时就已经加入进来-->
	<fragment
		android:name="utilcode.tyq.com.ceshi4.BookListFragment"
		android:id="@+id/book_list"
		android:layout_width="0dp"
		android:layout_height="match_parent"
		android:layout_weight="1" />
	<!-- 添加一个FrameLayout容器 右边的-->
	<FrameLayout
		android:id="@+id/book_detail_container"
		android:layout_width="0dp"
		android:layout_height="match_parent"
		android:layout_weight="3" />
</LinearLayout>

```
定义主页面的代码 每次点击的时候初始化Fragment
```
package utilcode.tyq.com.ceshi4;
import android.app.Activity;
import android.app.AlarmManager;
import android.app.PendingIntent;
import android.app.TimePickerDialog;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.TimePicker;
import android.widget.Toast;

import java.util.Calendar;

public class MainActivity extends Activity implements
        BookListFragment.Callbacks
{
    @Override
    public void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        // 加载/res/layout目录下的activity_book_twopane.xml布局文件
        setContentView(R.layout.activity_book_twopane);
    }
    // 实现Callbacks接口必须实现的方法 只有点击时才实现的方法 每点击一次
    //携带的参数都会发生改变
    @Override
    public void onItemSelected(Integer id)
    {
        // 创建Bundle，准备向Fragment传入参数
        Bundle arguments = new Bundle();
        arguments.putInt(BookDetailFragment.ITEM_ID, id);
        // 创建BookDetailFragment对象
        BookDetailFragment fragment = new BookDetailFragment();
        // 向Fragment传入参数
        fragment.setArguments(arguments);
        // 使用fragment替换book_detail_container容器当前显示的Fragment beginTransaction开启事务
动态的更新了容器中的内容 getFragmentManager().beginTransaction()代表Activity对Fragment执行的多个改变
        getFragmentManager().beginTransaction()
                .replace(R.id.book_detail_container, fragment)
                .commit();  // ①
    }

}

```
每次点击的时候的片段和它的布局
```
package utilcode.tyq.com.ceshi4;

import android.app.Fragment;
import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.TextView;

public class BookDetailFragment extends Fragment
{
	public static final String ITEM_ID = "item_id";
	// 保存该Fragment显示的Book对象
	BookContent.Book book;
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		// 如果启动该Fragment时包含了ITEM_ID参数 根据传入的参数获取图书的信息
		if (getArguments().containsKey(ITEM_ID))
		{//在这里，初始化数据对象
			book = BookContent.ITEM_MAP.get(getArguments()
				.getInt(ITEM_ID)); // ①
		}
	}
	// 重写该方法，该方法返回的View将作为Fragment显示的组件
	@Override
	public View onCreateView(LayoutInflater inflater
		, ViewGroup container, Bundle savedInstanceState)
	{
		// 加载/res/layout/目录下的fragment_book_detail.xml布局文件
		View rootView = inflater.inflate(R.layout.fragment_book_detail,
				container, false);
		if (book != null)
		{
			// 让book_title文本框显示book对象的title属性
			((TextView) rootView.findViewById(R.id.book_title))
				.setText(book.title);
			// 让book_desc文本框显示book对象的desc属性
			((TextView) rootView.findViewById(R.id.book_desc))
				.setText(book.desc);
		}
		return rootView;
	}
}



<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
	android:layout_width="match_parent"
	android:layout_height="match_parent"
	android:orientation="vertical">
	<!-- 定义一个TextView来显示图书标题 -->
	<TextView
		style="?android:attr/textAppearanceLarge"
		android:id="@+id/book_title"
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:padding="16dp"/>
	<!-- 定义一个TextView来显示图书描述 -->
	<TextView
		style="?android:attr/textAppearanceMedium"
		android:id="@+id/book_desc"
		android:layout_width="match_parent"
		android:layout_height="match_parent"
		android:padding="16dp"/>
</LinearLayout>

```
模拟系统的数据类型
```
package utilcode.tyq.com.ceshi4;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class BookContent
{
	// 定义一个内部类，作为系统的业务对象
	public static class Book
	{
		public Integer id;
		public String title;
		public String desc;
		public Book(Integer id, String title, String desc)
		{
			this.id = id;
			this.title = title;
			this.desc = desc;
		}
		@Override
		public String toString()
		{
			return title;
		}
	}
	// 使用List集合记录系统所包含的Book对象
	public static List<Book> ITEMS = new ArrayList<Book>();
	// 使用Map集合记录系统所包含的Book对象
	public static Map<Integer, Book> ITEM_MAP
			= new HashMap<Integer, Book>();
	static
	{  //利用构造器来初始化类的信息
		// 使用静态初始化代码，将Book对象添加到List集合、Map集合中
		addItem(new Book(1, "疯狂Java讲义"
				, "一本全面、深入的Java学习图书，已被多家高校选做教材。"));
		addItem(new Book(2, "疯狂Android讲义"
				, "Android学习者的首选图书，常年占据京东、当当、 "
				+ "亚马逊3大网站Android销量排行榜的榜首"));
		addItem(new Book(3, "轻量级Java EE企业应用实战"
				, "全面介绍Java EE开发的Struts 2、Spring 3、Hibernate 4框架"));
	}
	private static void addItem(Book book)
	{
		ITEMS.add(book);
		ITEM_MAP.put(book.id, book);
	}
}

```
<h1 id="0402_2">兼顾屏幕分辨率的应用</h1>
 
[返回目录](#0402) 

![](http://i.imgur.com/80fVWJl.jpg)
建立资源文件夹 values-large
refs.xml  在打屏幕手机上activity_book_list文件会取代activity_book_twopane
```
<?xml version="1.0" encoding="utf-8"?>
<resources>
	<!-- 定义activity_book_list实际引用@layout/activity_book_twopane资源 -->
	<item type="layout" name="activity_book_list">
		@layout/activity_book_twopane</item>
</resources>
```
Activity根据不同的分辨率进行分别处理
```
package org.crazyit.app;

import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;

public class BookListActivity extends Activity implements
		BookListFragment.Callbacks
{
	// 定义一个旗标，用于标识该应用是否支持大屏幕
	private boolean mTwoPane;
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		// 指定加载R.layout.activity_book_list对应的界面布局文件
		// 但实际上该应用会根据屏幕分辨率加载不同的界面布局文件
		setContentView(R.layout.activity_book_list);
		// 如果加载的界面布局文件中包含ID为book_detail_container的组件
		if (findViewById(R.id.book_detail_container) != null)
		{
			mTwoPane = true; //这个就表示是大屏幕
			((BookListFragment) getFragmentManager()
					.findFragmentById(R.id.book_list))
					.setActivateOnItemClick(true);
		}
	}
	@Override
	public void onItemSelected(Integer id)
	{
		if (mTwoPane)
		{//大屏幕
			// 创建Bundle，准备向Fragment传入参数
			Bundle arguments = new Bundle();
			arguments.putInt(BookDetailFragment.ITEM_ID, id);
			// 创建BookDetailFragment对象
			BookDetailFragment fragment = new BookDetailFragment();
			// 向Fragment传入参数
			fragment.setArguments(arguments);
			// 使用fragment替换book_detail_container容器当前显示的Fragment
			getFragmentManager().beginTransaction()
					.replace(R.id.book_detail_container, fragment).commit();
		}
		else
		{
			// 创建启动BookDetailActivity的Intent
			Intent detailIntent = new Intent(this, BookDetailActivity.class);
			// 设置传给BookDetailActivity的参数
			detailIntent.putExtra(BookDetailFragment.ITEM_ID, id);
			// 启动Activity
			startActivity(detailIntent);
		}
	}
}

```
Activity页面加载一个Fragment
```
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
	android:id="@+id/book_detail_container"
	android:layout_width="match_parent"
	android:layout_height="match_parent"/>


package org.crazyit.app;

import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.view.MenuItem;

public class BookDetailActivity extends Activity
{
	@Override
	protected void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		// 指定加载/res/layout目录下的activity_book_detail.xml布局文件
		// 该界面布局文件内只定义了一个名为book_detail_container的FrameLayout
		setContentView(R.layout.activity_book_detail);
		// 将ActionBar上应用图标转换成可点击的按钮
		getActionBar().setDisplayHomeAsUpEnabled(true);
		if (savedInstanceState == null)
		{
			// 创建BookDetailFragment对象
			BookDetailFragment fragment = new BookDetailFragment();
			// 创建Bundle对象，
			Bundle arguments = new Bundle();
			arguments.putInt(BookDetailFragment.ITEM_ID, getIntent()
					.getIntExtra(BookDetailFragment.ITEM_ID, 0));
			// 向Fragment传入参数
			fragment.setArguments(arguments);
			// 将指定fragment添加到book_detail_container容器中
			getFragmentManager().beginTransaction()
					.add(R.id.book_detail_container, fragment).commit();
		}
	}
	@Override
	public boolean onOptionsItemSelected(MenuItem item)
	{
		if (item.getItemId() == android.R.id.home)
		{
			// 创建启动BookListActivity的Intent
			Intent intent = new Intent(this, BookListActivity.class);
			// 添加额外的Flag，将Activity栈中处于FirstActivity之上的Activity弹出
			intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
			// 启动intent对应的Activity
			startActivity(intent);
			return true;
		}
		return super.onOptionsItemSelected(item);
	}
}

```

<h1 id="0402_3">Fragment的生命周期</h1>
 
[返回目录](#0402) 
启动Fragment时的回调方法
![](http://i.imgur.com/rfVfOu0.jpg)
其他的生命周期
![](http://i.imgur.com/xe4gYmY.jpg)
![](http://i.imgur.com/ZvJZrIM.jpg)
```
// 为addFragment按钮绑定事件监听器
		addFragment.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View source)
			{
				LifecycleFragment fragment = new LifecycleFragment();
				getFragmentManager().beginTransaction()
						.replace(R.id.container, fragment)
						.commit();
			}
		});
		// 为backFragment按钮绑定事件监听器
		backFragment.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View source)
			{
				SecondFragment fragment = new SecondFragment();
				getFragmentManager().beginTransaction()
						.replace(R.id.container, fragment)
						.addToBackStack("aa")// 将替换前的Fragment添加到Back栈,按back后会恢复之前的碎片
						.commit();
			}
		});
		// 为replaceFragment按钮绑定事件监听器
		replaceFragment.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View v)
			{
				SecondFragment fragment = new SecondFragment();
				getFragmentManager().beginTransaction()
						.replace(R.id.container, fragment)
						.commit();
			}
		});
```
碎片对应的容器
```
<LinearLayout 
    android:id="@+id/container"
	android:orientation="vertical"
    android:layout_width="wrap_content"
	android:layout_height="160dp">
</LinearLayout>
```

<h1 id="0701">使用简单图片</h1>
 
[返回目录](#1) 
R.drawable.file R清单中的索引项 是一个int型常量
Resources的getDrawable(int id) 获取实际的Drawable对象

Bitmap 代表一个位图
BitmapDrawable 里封装的图片就是一个Bitmap对象
它们可以相互转化
BitmapFactory是一个工具类，它提供了大量的方法，可用于从不同的数据源解析和创建Bitmap对象，例如取出内存卡中的图片。

assets文件夹图片查看器
![](http://i.imgur.com/hUZxkAU.jpg)
```
package studydiary.tyq.com.ceshi1;

import android.app.Activity;
import android.content.res.AssetManager;
import android.graphics.BitmapFactory;
import android.graphics.drawable.BitmapDrawable;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.ImageView;

import java.io.IOException;
import java.io.InputStream;


public class MainActivity extends Activity {
  //文件夹内的文件
    String[] images = null;
    //文件管理器
    AssetManager assets = null;
    int currentImg = 0;
    ImageView image;

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
        image = (ImageView) findViewById(R.id.image);
        try {
            assets = getAssets();
            // 获取/assets/目录下所有文件
            images = assets.list("");
        } catch (IOException e) {
            e.printStackTrace();
        }
        // 获取next按钮
        final Button next = (Button) findViewById(R.id.next);
        // 为next按钮绑定事件监听器，该监听器将会查看下一张图片
        next.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View sources) {
                // 如果发生数组越界
                if (currentImg >= images.length) {
                    currentImg = 0;
                }
                // 找到下一个图片文件
                while (!images[currentImg].endsWith(".png")
                        && !images[currentImg].endsWith(".jpg")
                        && !images[currentImg].endsWith(".gif")) {
                    currentImg++;
                    // 如果已发生数组越界
                    if (currentImg >= images.length) {
                        currentImg = 0;
                    }
                }
                InputStream assetFile = null;
                try {
                    // 打开指定资源对应的输入流
                    assetFile = assets.open(images[currentImg++]);
                } catch (IOException e) {
                    e.printStackTrace();
                }
                //获取按钮上显示的图片
                BitmapDrawable bitmapDrawable = (BitmapDrawable) image
                        .getDrawable();
                // 如果图片还未回收，先强制回收该图片
                if (bitmapDrawable != null
                        && !bitmapDrawable.getBitmap().isRecycled()) // ①
                {
                    bitmapDrawable.getBitmap().recycle();
                }
                // 改变ImageView显示的图片 从指定输入流解析并创建Bitmap对象
                image.setImageBitmap(BitmapFactory
                        .decodeStream(assetFile)); // ②
            }
        });
    }
}


```
<h1 id="0702">绘图</h1>
 
[返回目录](#1)

[绘图基础](#0702_1)
[绘制路径](#0702_2)
[采用双缓冲实现画图板](#0702_3)
[弹球游戏](#0702_4)

<h1 id="0702_1">绘图基础</h1>

[返回目录](#0702) 

![](http://i.imgur.com/invSmtr.jpg)
```
<org.crazyit.image.MyView  
	android:layout_width="wrap_content" 
	android:layout_height="wrap_content"
	/>


package org.crazyit.image;

import android.content.Context;
import android.graphics.Canvas;
import android.graphics.Color;
import android.graphics.LinearGradient;
import android.graphics.Paint;
import android.graphics.Path;
import android.graphics.RectF;
import android.graphics.Shader;
import android.util.AttributeSet;
import android.view.View;

public class MyView extends View
{
	public MyView(Context context, AttributeSet set)
	{
		super(context, set);
	}
	@Override
	// 重写该方法，进行绘图
	protected void onDraw(Canvas canvas)
	{
		super.onDraw(canvas);
		// 把整张画布绘制成白色
		canvas.drawColor(Color.WHITE);

		Paint paint = new Paint();
		// 去锯齿
		paint.setAntiAlias(true);
		paint.setColor(Color.BLUE);
		paint.setStyle(Paint.Style.STROKE);
		paint.setStrokeWidth(4);
		//这个是画布的宽度
		int viewWidth = this.getWidth();
		// 绘制圆形
		canvas.drawCircle(viewWidth / 10 + 10, viewWidth / 10 + 10
			, viewWidth / 10, paint);
		// 绘制正方形
		canvas.drawRect(10 , viewWidth / 5 + 20 , viewWidth / 5 + 10
			, viewWidth * 2 / 5 + 20 , paint);
		// 绘制矩形
		canvas.drawRect(10, viewWidth * 2 / 5 + 30, viewWidth / 5 + 10
			, viewWidth / 2 + 30, paint);
		RectF re1 = new RectF(10, viewWidth / 2 + 40
			, 10 + viewWidth / 5 ,viewWidth * 3 / 5 + 40);
		// 绘制圆角矩形
		canvas.drawRoundRect(re1, 15, 15, paint);
		RectF re11 = new RectF(10, viewWidth * 3 / 5 + 50
			, 10 + viewWidth / 5 ,viewWidth * 7 / 10 + 50);
		// 绘制椭圆
		canvas.drawOval(re11, paint);
		// 定义一个Path对象，封闭成一个三角形
		Path path1 = new Path();
		path1.moveTo(10, viewWidth * 9 / 10 + 60);
		path1.lineTo(viewWidth / 5 + 10, viewWidth * 9 / 10 + 60);
		path1.lineTo(viewWidth / 10 + 10, viewWidth * 7 / 10 + 60);
		path1.close();
		// 根据Path进行绘制，绘制三角形
		canvas.drawPath(path1, paint);
		// 定义一个Path对象，封闭成一个五角形
		Path path2 = new Path();
		path2.moveTo(10 + viewWidth / 15, viewWidth * 9 / 10 + 70);
		path2.lineTo(10 + viewWidth * 2 / 15, viewWidth * 9 / 10 + 70);
		path2.lineTo(10 + viewWidth / 5, viewWidth + 70);
		path2.lineTo(10 + viewWidth / 10, viewWidth * 11/10 + 70);
		path2.lineTo(10 , viewWidth + 70);
		path2.close();
		// 根据Path进行绘制，绘制五角形
		canvas.drawPath(path2, paint);

		// ----------设置填充风格后绘制----------
		paint.setStyle(Paint.Style.FILL);
		paint.setColor(Color.RED);
		// 绘制圆形
		canvas.drawCircle(viewWidth * 3 / 10 + 20, viewWidth / 10 + 10
			, viewWidth / 10, paint);
		// 绘制正方形
		canvas.drawRect(viewWidth / 5 + 20 , viewWidth / 5 + 20
			, viewWidth * 2 / 5 + 20 , viewWidth * 2 / 5 + 20 , paint);
		// 绘制矩形
		canvas.drawRect(viewWidth / 5 + 20, viewWidth * 2 / 5 + 30
			, viewWidth * 2 / 5 + 20 , viewWidth / 2 + 30, paint);
		RectF re2 = new RectF(viewWidth / 5 + 20, viewWidth / 2 + 40
			, 20 + viewWidth * 2 / 5 ,viewWidth * 3 / 5 + 40);
		// 绘制圆角矩形
		canvas.drawRoundRect(re2, 15, 15, paint);
		RectF re21 = new RectF(20 + viewWidth / 5, viewWidth * 3 / 5 + 50
			, 20 + viewWidth * 2 / 5 ,viewWidth * 7 / 10 + 50);
		// 绘制椭圆
		canvas.drawOval(re21, paint);
		// 定义一个Path对象，封闭成一个三角形
		Path path3 = new Path();
		path3.moveTo(20 + viewWidth / 5, viewWidth * 9 / 10 + 60);
		path3.lineTo(viewWidth * 2 / 5 + 20, viewWidth * 9 / 10 + 60);
		path3.lineTo(viewWidth * 3 / 10 + 20, viewWidth * 7 / 10 + 60);
		path3.close();
		// 根据Path进行绘制，绘制三角形
		canvas.drawPath(path3, paint);
		// 定义一个Path对象，封闭成一个五角形
		Path path4 = new Path();
		path4.moveTo(20 + viewWidth *4 / 15, viewWidth * 9 / 10 + 70);
		path4.lineTo(20 + viewWidth / 3, viewWidth * 9 / 10 + 70);
		path4.lineTo(20 + viewWidth * 2 / 5, viewWidth + 70);
		path4.lineTo(20 + viewWidth * 3 / 10, viewWidth * 11/10 + 70);
		path4.lineTo(20 + viewWidth / 5 , viewWidth + 70);
		path4.close();
		// 根据Path进行绘制，绘制五角形
		canvas.drawPath(path4, paint);


		// ----------设置渐变器后绘制----------
		// 为Paint设置渐变器
		Shader mShader = new LinearGradient(0, 0, 40, 60
			, new int[] {Color.RED, Color.GREEN, Color.BLUE, Color.YELLOW }
			, null , Shader.TileMode.REPEAT);
		paint.setShader(mShader);
		//设置阴影
		paint.setShadowLayer(25 , 20 , 20 , Color.GRAY);
		// 绘制圆形
		canvas.drawCircle(viewWidth / 2 + 30, viewWidth / 10 + 10
			, viewWidth / 10, paint);
		// 绘制正方形
		canvas.drawRect(viewWidth * 2 / 5 + 30 , viewWidth / 5 + 20
			, viewWidth * 3 / 5 + 30 , viewWidth * 2 / 5 + 20 , paint);
		// 绘制矩形
		canvas.drawRect(viewWidth * 2 / 5 + 30, viewWidth * 2 / 5 + 30
			, viewWidth * 3 / 5 + 30 , viewWidth / 2 + 30, paint);
		RectF re3 = new RectF(viewWidth * 2 / 5 + 30, viewWidth / 2 + 40
			, 30 + viewWidth * 3 / 5 ,viewWidth * 3 / 5 + 40);
		// 绘制圆角矩形
		canvas.drawRoundRect(re3, 15, 15, paint);
		RectF re31 = new RectF(30 + viewWidth *2 / 5, viewWidth * 3 / 5 + 50
			, 30 + viewWidth * 3 / 5 ,viewWidth * 7 / 10 + 50);
		// 绘制椭圆
		canvas.drawOval(re31, paint);
		// 定义一个Path对象，封闭成一个三角形
		Path path5 = new Path();
		path5.moveTo(30 + viewWidth * 2/ 5, viewWidth * 9 / 10 + 60);
		path5.lineTo(viewWidth * 3 / 5 + 30, viewWidth * 9 / 10 + 60);
		path5.lineTo(viewWidth / 2 + 30, viewWidth * 7 / 10 + 60);
		path5.close();
		// 根据Path进行绘制，绘制三角形
		canvas.drawPath(path5, paint);
		// 定义一个Path对象，封闭成一个五角形
		Path path6 = new Path();
		path6.moveTo(30 + viewWidth * 7 / 15, viewWidth * 9 / 10 + 70);
		path6.lineTo(30 + viewWidth * 8 / 15, viewWidth * 9 / 10 + 70);
		path6.lineTo(30 + viewWidth * 3 / 5, viewWidth + 70);
		path6.lineTo(30 + viewWidth / 2, viewWidth * 11/10 + 70);
		path6.lineTo(30 + viewWidth * 2 / 5 , viewWidth + 70);
		path6.close();
		// 根据Path进行绘制，绘制五角形
		canvas.drawPath(path6, paint);


		// ----------设置字符大小后绘制----------
		paint.setTextSize(48);
		paint.setShader(null);
		// 绘制7个字符串
		canvas.drawText(getResources().getString(R.string.circle)
			, 60 + viewWidth * 3 / 5, viewWidth / 10 + 10, paint);
		canvas.drawText(getResources().getString(R.string.square)
			, 60 + viewWidth * 3 / 5, viewWidth * 3 / 10 + 20, paint);
		canvas.drawText(getResources().getString(R.string.rect)
			, 60 + viewWidth * 3 / 5, viewWidth * 1 / 2 + 20, paint);
		canvas.drawText(getResources().getString(R.string.round_rect)
			, 60 + viewWidth * 3 / 5, viewWidth * 3 / 5 + 30, paint);
		canvas.drawText(getResources().getString(R.string.oval)
			, 60 + viewWidth * 3 / 5, viewWidth * 7 / 10 + 30, paint);
		canvas.drawText(getResources().getString(R.string.triangle)
			, 60 + viewWidth * 3 / 5, viewWidth * 9 / 10 + 30, paint);
		canvas.drawText(getResources().getString(R.string.pentagon)
			, 60 + viewWidth * 3 / 5, viewWidth * 11 / 10 + 30, paint);
	}
}

```
<h1 id="0702_2">绘制路径</h1>

[返回目录](#0702) 

![](http://i.imgur.com/uhlnKRN.jpg)

Path是一个非常有用的类，它可以预先在View上将N个点练成一条路径。
PathEffect来定义绘制效果。
这个实例看的不太明白
```
package studydiary.tyq.com.ceshi1;

import android.app.Activity;
import android.content.Context;
import android.graphics.Canvas;
import android.graphics.Color;
import android.graphics.ComposePathEffect;
import android.graphics.CornerPathEffect;
import android.graphics.DashPathEffect;
import android.graphics.DiscretePathEffect;
import android.graphics.Paint;
import android.graphics.Path;
import android.graphics.PathDashPathEffect;
import android.graphics.PathEffect;
import android.graphics.SumPathEffect;
import android.os.Bundle;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;

public class MainActivity extends Activity
{
    @Override
    protected void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        setContentView(new MyView(this));
    }
    class MyView extends View
    {//改参数，用于指定路径效果的相位，当它改变时，绘制效果也略有变化
        float phase;
        PathEffect[] effects = new PathEffect[7];
        int[] colors;
        private Paint paint;
        Path path;
        public MyView(Context context)
        {
            super(context);
            paint = new Paint();
            paint.setStyle(Paint.Style.STROKE);
            paint.setStrokeWidth(4);
            // 创建并初始化Path
            path = new Path();
            path.moveTo(0, 0);
            for (int i = 1; i <= 40; i++)
            {
                // 生成40个点，随机生成它们的Y坐标，并将它们连成一条Path路径
                path.lineTo(i * 20, (float) Math.random() * 60);
            }
            // 初始化7个颜色
            colors = new int[] { Color.BLACK, Color.BLUE, Color.CYAN,
                    Color.GREEN, Color.MAGENTA, Color.RED, Color.YELLOW };
        }
        @Override
        protected void onDraw(Canvas canvas)
        {
            // 将背景填充成白色
            canvas.drawColor(Color.WHITE);
            // -----------下面开始初始化7种路径效果----------
            // 不使用路径效果
            effects[0] = null;
            // 使用CornerPathEffect路径效果
            effects[1] = new CornerPathEffect(10);
            // 初始化DiscretePathEffect
            effects[2] = new DiscretePathEffect(3.0f, 5.0f);
            // 初始化DashPathEffect
            effects[3] = new DashPathEffect(new float[] { 20, 10, 5, 10 },
                    phase);
            // 初始化PathDashPathEffect
            Path p = new Path();
            p.addRect(0, 0, 8, 8, Path.Direction.CCW);
            effects[4] = new PathDashPathEffect(p, 12, phase,
                    PathDashPathEffect.Style.ROTATE);
            // 初始化ComposePathEffect
            effects[5] = new ComposePathEffect(effects[2], effects[4]);
            effects[6] = new SumPathEffect(effects[4], effects[3]);
            // 将画布移动到(8、8)处开始绘制 正数是向下，向右移动
            canvas.translate(8, 8);
            // 依次使用7种不同路径效果、7种不同的颜色来绘制路径
            for (int i = 0; i < effects.length; i++)
            {   //PathEffect来定义绘制效果
                paint.setPathEffect(effects[i]);
                paint.setColor(colors[i]);
                canvas.drawPath(path, paint);
                canvas.translate(0, 60);
            }
            // 改变phase值，形成动画效果
            phase += 1;
            invalidate();
        }
    }
}
```
沿着path绘制文本 没看懂
![](http://i.imgur.com/Ygi2zJb.jpg)
```
package studydiary.tyq.com.ceshi1;
import android.app.Activity;
import android.content.Context;
import android.graphics.Canvas;
import android.graphics.Color;
import android.graphics.Paint;
import android.graphics.Path;
import android.graphics.RectF;
import android.os.Bundle;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;

public class MainActivity extends Activity
{
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		setContentView(new TextView(this));
	}
	class TextView extends View
	{
		final String DRAW_STR = "疯狂Android讲义";
		Path[] paths = new Path[3];
		Paint paint;
		public TextView(Context context)
		{
			super(context);
			paths[0] = new Path();
			paths[0].moveTo(0, 0);
			for (int i = 1; i <= 20; i++)
			{
				// 生成20个点，随机生成它们的Y坐标，并将它们连成一条Path
				paths[0].lineTo(i * 30, (float) Math.random() * 30);
			}
			paths[1] = new Path();
			RectF rectF = new RectF(0, 0, 600, 360);
			paths[1].addOval(rectF, Path.Direction.CCW);
			paths[2] = new Path();
			paths[2].addArc(rectF, 60, 180);
			// 初始化画笔
			paint = new Paint();
			paint.setAntiAlias(true);
			paint.setColor(Color.CYAN);
			paint.setStrokeWidth(1);
		}
		@Override
		protected void onDraw(Canvas canvas)
		{
			canvas.drawColor(Color.WHITE);
			canvas.translate(40, 40);
			// 设置从右边开始绘制（右对齐）
			paint.setTextAlign(Paint.Align.RIGHT);
			paint.setTextSize(20);
			// 绘制路径
			paint.setStyle(Paint.Style.STROKE);
			canvas.drawPath(paths[0], paint);
			paint.setTextSize(40);
			// 沿着路径绘制一段文本
			paint.setStyle(Paint.Style.FILL);
			canvas.drawTextOnPath(DRAW_STR, paths[0], -8, 20, paint);
			// 对Canvas进行坐标变换：画布下移60
			canvas.translate(0, 60);
			// 绘制路径
			paint.setStyle(Paint.Style.STROKE);
			canvas.drawPath(paths[1], paint);
			// 沿着路径绘制一段文本
			paint.setStyle(Paint.Style.FILL);
			canvas.drawTextOnPath(DRAW_STR, paths[1], -20, 20, paint);
			// 对Canvas进行坐标变换： 画布下移360
			canvas.translate(0, 360);
			// 绘制路径
			paint.setStyle(Paint.Style.STROKE);
			canvas.drawPath(paths[2], paint);
			// 沿着路径绘制一段文本
			paint.setStyle(Paint.Style.FILL);
			canvas.drawTextOnPath(DRAW_STR, paths[2], -10, 20, paint);
		}
	}
}


```
<h1 id="0702_3">采用双缓冲实现画图板</h1>

[返回目录](#0702) 

![](http://i.imgur.com/cB3TLnz.jpg)

动画就是重复的调用onDraw方法。
表面现象是，自由的画曲线，实际上依然利用的是Canvas 的drawLine（）的方法画直线。每条直线都是从上一次拖到事件的发生点画到本次拖动事件的发生点。
双缓冲技术：程序并不直接绘制到该View上，而是先绘制到内存中的一个bitmap图片上（这就是缓冲区），等到内存中的Bitmap绘制好后，在一次性将bitmap绘制到View组件上。

自定义绘图的View
```
package studydiary.tyq.com.ceshi1;

import android.content.Context;
import android.graphics.Bitmap;
import android.graphics.Canvas;
import android.graphics.Color;
import android.graphics.Paint;
import android.graphics.Path;
import android.util.AttributeSet;
import android.view.MotionEvent;
import android.view.View;

public class DrawView extends View
{
	// 定义记录前一个拖动事件发生点的坐标
	float preX;
	float preY;
	private Path path;
	public Paint paint = null;
	// 定义一个内存中的图片，该图片将作为缓冲区
	Bitmap cacheBitmap = null;
	// 定义cacheBitmap上的Canvas对象
	Canvas cacheCanvas = null;
	public DrawView(Context context, int width , int height)
	{
		super(context);
		// 创建一个与该View相同大小的缓存区
		cacheBitmap = Bitmap.createBitmap(width, height,
			Bitmap.Config.ARGB_8888);
		cacheCanvas = new Canvas();
		path = new Path();
		// 设置cacheCanvas将会绘制到内存中的cacheBitmap上
		cacheCanvas.setBitmap(cacheBitmap);
		// 设置画笔的颜色
		paint = new Paint(Paint.DITHER_FLAG);
		paint.setColor(Color.RED);
		// 设置画笔风格
		paint.setStyle(Paint.Style.STROKE);
		paint.setStrokeWidth(1);
		// 反锯齿
		paint.setAntiAlias(true);
		paint.setDither(true);
	}

	@Override
	public boolean onTouchEvent(MotionEvent event)
	{
		// 获取拖动事件的发生位置
		float x = event.getX();
		float y = event.getY();
		switch (event.getAction())
		{
			case MotionEvent.ACTION_DOWN:
				// 从前一个点绘制到当前点之后，把当前点定义成下次绘制的前一个点
				path.moveTo(x, y);
				preX = x;
				preY = y;
				break;
			case MotionEvent.ACTION_MOVE:
				// 从前一个点绘制到当前点之后，把当前点定义成下次绘制的前一个点
				path.quadTo(preX, preY, x, y);
				preX = x;
				preY = y;
				break;
			case MotionEvent.ACTION_UP:
				//这个表明是向缓冲区的画布绘图
				cacheCanvas.drawPath(path, paint); // ①
				path.reset();
				break;
		}
		//只要用户有操作 就要重绘图形
		invalidate();
		// 返回true表明处理方法已经处理该事件
		return true;
	}
	@Override
	public void onDraw(Canvas canvas)
	{
		Paint bmpPaint = new Paint();
		// 将cacheBitmap绘制到该View组件上
		canvas.drawBitmap(cacheBitmap, 0, 0, bmpPaint); // ②
		// 沿着path绘制
		canvas.drawPath(path, paint);
	}
}

```
界面中引用View
```
package studydiary.tyq.com.ceshi1;
import android.app.Activity;
import android.graphics.BlurMaskFilter;
import android.graphics.Color;
import android.graphics.EmbossMaskFilter;
import android.os.Bundle;
import android.util.DisplayMetrics;
import android.view.Menu;
import android.view.MenuInflater;
import android.view.MenuItem;
import android.widget.LinearLayout;


public class MainActivity extends Activity
{//EmbossMaskFilter 浮雕效果实现
	EmbossMaskFilter emboss;
	//绘图的阴影效果
	BlurMaskFilter blur;
	DrawView drawView;
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		LinearLayout line = new LinearLayout(this);
		DisplayMetrics displayMetrics = new DisplayMetrics();
		// 获取创建的宽度和高度
		getWindowManager().getDefaultDisplay()
				.getRealMetrics(displayMetrics);
		// 创建一个DrawView，该DrawView的宽度、高度与该Activity保持相同 Pixels 像素
		drawView = new DrawView(this, displayMetrics.widthPixels
				, displayMetrics.heightPixels);
		drawView.paint.setMaskFilter(emboss);//浮雕效果
		drawView.paint.setColor(Color.GREEN);//颜色
		drawView.paint.setStrokeWidth(5);//5像素
		line.addView(drawView);
		setContentView(line);


		emboss = new EmbossMaskFilter(new float[]
				{ 1.5f, 1.5f, 1.5f }, 0.6f,	6, 4.2f);
		blur = new BlurMaskFilter(8, BlurMaskFilter.Blur.NORMAL);
	}
	@Override
	// 负责创建选项菜单
	public boolean onCreateOptionsMenu(Menu menu)
	{
		MenuInflater inflator = new MenuInflater(this);
		// 装载R.menu.my_menu对应的菜单，并添加到menu中
		inflator.inflate(R.menu.menu_main, menu);
		return super.onCreateOptionsMenu(menu);
	}
	@Override
	// 菜单项被单击后的回调方法
	public boolean onOptionsItemSelected(MenuItem mi)
	{
		// 判断单击的是哪个菜单项，并有针对性地作出响应
		switch (mi.getItemId())
		{
			case R.id.red:
				drawView.paint.setColor(Color.RED);
				mi.setChecked(true);
				break;
			case R.id.green:
				drawView.paint.setColor(Color.GREEN);
				mi.setChecked(true);
				break;
			case R.id.blue:
				drawView.paint.setColor(Color.BLUE);
				mi.setChecked(true);
				break;
			case R.id.width_1:
				drawView.paint.setStrokeWidth(1);
				break;
			case R.id.width_3:
				drawView.paint.setStrokeWidth(3);
				break;
			case R.id.width_5:
				drawView.paint.setStrokeWidth(5);
				break;
			case R.id.blur:
				drawView.paint.setMaskFilter(blur);
				break;
			case R.id.emboss:
				drawView.paint.setMaskFilter(emboss);
				break;
		}
		return true;
	}
}
```
<h1 id="0702_4">弹球游戏</h1>

[返回目录](#0702) 

![](http://i.imgur.com/Aqm8SiE.jpg)
![](http://i.imgur.com/MVbtFqi.jpg)
绘图坐标不断的变幻，就产生了动画的效果
```
package org.crazyit.image;

import android.app.Activity;
import android.content.Context;
import android.graphics.Canvas;
import android.graphics.Color;
import android.graphics.Paint;
import android.os.Bundle;
import android.os.Handler;
import android.os.Message;
import android.util.DisplayMetrics;
import android.view.Display;
import android.view.KeyEvent;
import android.view.View;
import android.view.View.OnKeyListener;
import android.view.Window;
import android.view.WindowManager;

import java.util.Random;
import java.util.Timer;
import java.util.TimerTask;


public class MainActivity extends Activity
{
	// 桌面的宽度  正数是向下，向右移动
	private int tableWidth;
	// 桌面的高度
	private int tableHeight;
	// 球拍的垂直位置 racket 球拍
	private int racketY;
	// 下面定义球拍的高度和宽度
	private final int RACKET_HEIGHT = 30;
	private final int RACKET_WIDTH = 90;
	// 小球的大小
	private final int BALL_SIZE = 16;
	// 小球纵向的运行速度
	private int ySpeed = 15;
	Random rand = new Random();
	// 返回一个-0.5~0.5的比率，用于控制小球的运行方向 Rate 比率
	private double xyRate = rand.nextDouble() - 0.5;
	// 小球横向的运行速度
	private int xSpeed = (int) (ySpeed * xyRate * 2);
	// ballX和ballY代表小球的坐标
	private int ballX = rand.nextInt(200) + 20;
	private int ballY = rand.nextInt(10) + 20;
	// racketX代表球拍的水平位置
	private int racketX = rand.nextInt(200);
	// 游戏是否结束的旗标
	private boolean isLose = false;
	private GameView contentView;

	@Override
	public void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		// 去掉窗口标题
		requestWindowFeature(Window.FEATURE_NO_TITLE);
		// 全屏显示
		getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN,
			WindowManager.LayoutParams.FLAG_FULLSCREEN);
		// 创建GameView组件
		final GameView gameView = new GameView(this);
		setContentView(gameView);
		// 获取窗口管理器 Display 显示 DisplayMetrics 韵律学
		WindowManager windowManager = getWindowManager();
		Display display = windowManager.getDefaultDisplay();
		DisplayMetrics metrics = new DisplayMetrics();
		display.getMetrics(metrics);
		// 获得屏幕宽和高  像素 Pixels
		tableWidth = metrics.widthPixels;
		tableHeight = metrics.heightPixels;
		racketY = tableHeight - 80;
		final Handler handler = new Handler() {
			public void handleMessage(Message msg) {
				if (msg.what == 0x123) {
					gameView.invalidate();
				}
			}
		};
		gameView.setOnKeyListener(new OnKeyListener() // ②
		{
			@Override
			public boolean onKey(View source, int keyCode, KeyEvent event) {
				// 获取由哪个键触发的事件
				switch (event.getKeyCode()) {
					// 控制挡板左移  代表x的值变小
					case KeyEvent.KEYCODE_A:
						if (racketX > 0) racketX -= 10;
						break;
					// 控制挡板右移
					case KeyEvent.KEYCODE_D:
						if (racketX < tableWidth - RACKET_WIDTH) racketX += 10;
						break;
				}
				// 通知gameView组件重绘
				gameView.invalidate();
				//表明事件已经完全处理 不会继续传播
				return true;
			}
		});
		final Timer timer = new Timer();
		// schedule日程安排  Timer 定时器
		timer.schedule(new TimerTask() // ①
		{
			@Override
			public void run() {
				// 如果小球碰到左边边框
				if (ballX <= 0 || ballX >= tableWidth - BALL_SIZE) {
					xSpeed = -xSpeed;
				}
				// 如果小球高度超出了球拍位置racketY - BALL_SIZE也就是球拍最底下的y坐标，且横向不在球拍范围之内，游戏结束
				// 正数是向下，向右移动
				if (ballY >= racketY - BALL_SIZE
						&& (ballX < racketX || ballX > racketX
						+ RACKET_WIDTH)) {
					timer.cancel();
					// 设置游戏是否结束的旗标为true
					isLose = true;
				}
				// 如果小球位于球拍之内，且到达球拍位置，小球反弹
				// 正数是向下，向右移动
				else if (ballY <= 0
						|| (ballY >= racketY - BALL_SIZE
						&& ballX > racketX && ballX <= racketX
						+ RACKET_WIDTH)) {
					ySpeed = -ySpeed;
				}
				// 小球坐标增加
				ballY += ySpeed;
				ballX += xSpeed;
				// 发送消息，通知系统重绘组件
				handler.sendEmptyMessage(0x123);
			}
		}, 0, 100);//每100秒监听一次
	}
	class GameView extends View
	{
		Paint paint = new Paint();
		public GameView(Context context)
		{
			super(context);
			setFocusable(true);
		}
		// 重写View的onDraw方法，实现绘画
		public void onDraw(Canvas canvas)
		{
			paint.setStyle(Paint.Style.FILL);
			// 设置去锯齿 AntiAlias 抗锯齿
			paint.setAntiAlias(true);
			// 如果游戏已经结束
			if (isLose)
			{
				paint.setColor(Color.RED);
				paint.setTextSize(40);
				canvas.drawText("游戏已结束", tableWidth / 2 - 100, 200, paint);
			}
			// 如果游戏还未结束
			else
			{
				// 设置颜色，并绘制小球
				paint.setColor(Color.rgb(255, 0, 0));
				canvas.drawCircle(ballX, ballY, BALL_SIZE, paint);
				// 设置颜色，并绘制球拍
				paint.setColor(Color.rgb(80, 80, 200));
				canvas.drawRect(racketX, racketY, racketX + RACKET_WIDTH,
						racketY + RACKET_HEIGHT, paint);
			}
		}
	}
}

```
<h1 id="0703">图形特效处理</h1>
 
[返回目录](#1)

[对绘制的图形进行旋转和倾斜变换](#0703_1)
[移动游戏背景](#0703_2)
[使用Shader填充图形](#0703_3)

<h1 id="0703_1">对绘制的图形进行旋转和倾斜变换</h1>

[返回目录](#0703) 

![](http://i.imgur.com/GEwyq7s.jpg)
matrix是矩阵工具类，可与其他api结合其他控制图形和图像的变化。既可以重新创建也可以获取其他对象中封装的类。

涉及的主要方法
```
// 重置Matrix
		matrix.reset();
		if (!isScale)
		{
			// 旋转Matrix
			matrix.setSkew(sx, 0);
		}
		else
		{
			// 缩放Matrix
			matrix.setScale(scale, scale);
		}
		// 根据原始位图和Matrix创建新图片
		Bitmap bitmap2 = Bitmap.createBitmap(bitmap, 0, 0, width, height,
				matrix, true);
		// 绘制新位图
		canvas.drawBitmap(bitmap2, matrix, null);
```
```
		<studydiary.tyq.com.ceshi1.MyView
		android:layout_width="match_parent"
		android:layout_height="match_parent"
		/>


package studydiary.tyq.com.ceshi1;

import android.content.Context;
import android.graphics.Bitmap;
import android.graphics.Canvas;
import android.graphics.Matrix;
import android.graphics.drawable.BitmapDrawable;
import android.util.AttributeSet;
import android.view.KeyEvent;
import android.view.View;

public class MyView extends View
{
	// 初始的图片资源
	private Bitmap bitmap;
	// Matrix 实例
	private Matrix matrix = new Matrix();
	// 设置倾斜度
	private float sx = 0.0f;
	// 位图宽和高
	private int width, height;
	// 缩放比例
	private float scale = 1.0f;
	// 判断缩放还是旋转
	private boolean isScale = false;
	public MyView(Context context , AttributeSet set)
	{
		super(context , set);
		// 获得位图
		bitmap = ((BitmapDrawable) context.getResources().getDrawable(
			R.drawable.a)).getBitmap();
		// 获得位图宽
		width = bitmap.getWidth();
		// 获得位图高
		height = bitmap.getHeight();
		// 使当前视图获得焦点
		this.setFocusable(true);
	}
	@Override
	protected void onDraw(Canvas canvas)
	{
		super.onDraw(canvas);
		// 重置Matrix
		matrix.reset();
		if (!isScale)
		{
			// 旋转Matrix
			matrix.setSkew(sx, 0);
		}
		else
		{
			// 缩放Matrix
			matrix.setScale(scale, scale);
		}
		// 根据原始位图和Matrix创建新图片
		Bitmap bitmap2 = Bitmap.createBitmap(bitmap, 0, 0, width, height,
				matrix, true);
		// 绘制新位图
		canvas.drawBitmap(bitmap2, matrix, null);
	}
	@Override
	public boolean onKeyDown(int keyCode, KeyEvent event)
	{
		switch(keyCode)
		{
			// 向左倾斜 postInvalidate其他线程里更新界面
			case KeyEvent.KEYCODE_A:
				isScale = false;
				sx += 0.1;
				postInvalidate();
				break;
			// 向右倾斜
			case KeyEvent.KEYCODE_D:
				isScale = false;
				sx -= 0.1;
				postInvalidate();
				break;
			// 放大
			case KeyEvent.KEYCODE_W:
				isScale = true;
				if (scale < 2.0)
					scale += 0.1;
				postInvalidate();
				break;
			// 缩小
			case KeyEvent.KEYCODE_S:
				isScale = true;
				if (scale > 0.5)
					scale -= 0.1;
				postInvalidate();
				break;
		}
		return super.onKeyDown(keyCode, event);
	}
}

```
<h1 id="0703_2">移动游戏背景</h1>

[返回目录](#0703) 

createBitmap不断的挖取源位图中不同位置的块，看到背景移动的假想。
![](http://i.imgur.com/RZVBH8L.jpg)
![](http://i.imgur.com/Y8Ljc4T.jpg)
```
package org.crazyit.image;

import android.app.Activity;
import android.content.Context;
import android.graphics.Bitmap;
import android.graphics.BitmapFactory;
import android.graphics.Canvas;
import android.graphics.Matrix;
import android.os.Bundle;
import android.os.Handler;
import android.os.Message;
import android.util.DisplayMetrics;
import android.view.Display;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.view.WindowManager;

import java.util.Timer;
import java.util.TimerTask;


public class MainActivity extends Activity
{
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		setContentView(new MyView(this));
	}
	class MyView extends View
	{
		// 记录背景位图的实际高度
		final int BACK_HEIGHT = 1700;
		// 背景图片 分别是背景和飞机
		private Bitmap back;
		private Bitmap plane;
		// 定义图片的宽度
		final int WIDTH = 640;
		final int HEIGHT = 880;
		private Matrix matrix = new Matrix();
		// 背景图片的开始位置
		private int startY = BACK_HEIGHT - HEIGHT;
		public MyView(Context context)
		{
			super(context);
			back = BitmapFactory.decodeResource(context.getResources(),
					R.drawable.back_img);
			// 获取窗口管理器
			WindowManager windowManager = getWindowManager();
			Display display = windowManager.getDefaultDisplay();
			DisplayMetrics metrics = new DisplayMetrics();
			display.getMetrics(metrics);
			// 获得屏幕的宽度
			float screenWidth = metrics.widthPixels;
			// 获取图片的缩放比例
			float scale = screenWidth / WIDTH;
			matrix.setScale(scale , scale);
			plane = BitmapFactory.decodeResource(context.getResources(),
					R.drawable.plane);
			final Handler handler = new Handler()
			{
				public void handleMessage(Message msg)
				{
					if (msg.what == 0x123)
					{
						// 重新开始移动
						if (startY <= 3)
						{
							startY = BACK_HEIGHT - HEIGHT;
						}
						else
						{
							startY -= 3;
						}
					}
					invalidate();
				}
			};
			new Timer().schedule(new TimerTask()
			{
				@Override
				public void run()
				{
					handler.sendEmptyMessage(0x123);
				}
			}, 0, 100);
		}
		@Override
		public void onDraw(Canvas canvas)
		{

			// 根据原始位图和缩放Matrix创建新图片
			Bitmap bitmap2 = Bitmap
				.createBitmap(back, 0, startY, WIDTH, HEIGHT , matrix , false); 
				// ①
			// 绘制新位图
			canvas.drawBitmap(bitmap2, 0, 0, null);
			// 绘制飞机
			canvas.drawBitmap(plane, 320, 700, null);
		}
	}
}
```
![](http://i.imgur.com/TlUWpIz.jpg)
```
package studydiary.tyq.com.ceshi1;
import android.app.Activity;
import android.content.Context;
import android.graphics.Bitmap;
import android.graphics.BitmapFactory;
import android.graphics.Canvas;
import android.graphics.Color;
import android.os.Bundle;
import android.view.Menu;
import android.view.MenuItem;
import android.view.MotionEvent;
import android.view.View;


public class MainActivity extends Activity
{
	private Bitmap bitmap;
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		setContentView(new MyView(this, R.drawable.jinta));
	}
	private class MyView extends View
	{
		// 定义两个常量，这两个常量指定该图片横向、纵向上都被划分为20格
		private final int WIDTH = 20;
		private final int HEIGHT = 20;
		// 记录该图片上包含441个顶点
		private final int COUNT = (WIDTH + 1) * (HEIGHT + 1);
		// 定义一个数组，保存Bitmap上的21 * 21个点的坐标
		private final float[] verts = new float[COUNT * 2];
		// 定义一个数组，记录Bitmap上的21 * 21个点经过扭曲后的坐标
		// 对图片进行扭曲的关键就是修改该数组里元素的值
		private final float[] orig = new float[COUNT * 2];
		public MyView(Context context, int drawableId)
		{
			super(context);
			setFocusable(true);
			// 根据指定资源加载图片
			bitmap = BitmapFactory.decodeResource(getResources()
					, drawableId);
			// 获取图片宽度、高度
			float bitmapWidth = bitmap.getWidth();
			float bitmapHeight = bitmap.getHeight();
			int index = 0;
			for (int y = 0; y <= HEIGHT; y++)
			{
				float fy = bitmapHeight * y / HEIGHT;
				for (int x = 0; x <= WIDTH; x++)
				{
					float fx = bitmapWidth * x / WIDTH;
					// 初始化orig、verts数组。 初始化后，orig、verts
					// 两个数组均匀地保存了21 * 21个点的x,y坐标
					orig[index * 2 + 0] = verts[index * 2 + 0] = fx;
					orig[index * 2 + 1] = verts[index * 2 + 1] = fy;
					index += 1;
				}
			}
			// 设置背景色
			setBackgroundColor(Color.WHITE);
		}
		@Override
		protected void onDraw(Canvas canvas)
		{
			//对bitmap按verts数组进行扭曲
			//从第一个点（由第5个参数0控制）开始扭曲
			canvas.drawBitmapMesh(bitmap, WIDTH, HEIGHT, verts
					, 0, null, 0,null);
		}
		// 工具方法，用于根据触摸事件的位置计算verts数组里各元素的值
		private void warp(float cx, float cy)
		{
			for (int i = 0; i < COUNT * 2; i += 2)
			{
				float dx = cx - orig[i + 0];
				float dy = cy - orig[i + 1];
				float dd = dx * dx + dy * dy;
				// 计算每个坐标点与当前点（cx、cy）之间的距离
				float d = (float) Math.sqrt(dd);
				// 计算扭曲度，距离当前点（cx、cy）越远，扭曲度越小
				float pull = 100000 / ((float) (dd * d));
				// 对verts数组（保存bitmap上21 * 21个点经过扭曲后的坐标）重新赋值
				if (pull >= 1)
				{
					verts[i + 0] = cx;
					verts[i + 1] = cy;
				}
				else
				{
					// 控制各顶点向触摸事件发生点偏移
					verts[i + 0] = orig[i + 0] + dx * pull;
					verts[i + 1] = orig[i + 1] + dy * pull;
				}
			}
			// 通知View组件重绘
			invalidate();
		}
		@Override
		public boolean onTouchEvent(MotionEvent event)
		{
			// 调用warp方法根据触摸屏事件的坐标点来扭曲verts数组
			warp(event.getX(), event.getY());
			return true;
		}
	}
}

```
<h1 id="0703_3">使用Shader填充图形</h1>

[返回目录](#0703) 

![](http://i.imgur.com/kOuGucp.jpg)
shaders 在Paint时控制画笔的渲染效果
实则是一种图形的填充任务

自定义View
```
/**
 *
 */
package org.crazyit.image;

import android.content.Context;
import android.graphics.Canvas;
import android.graphics.Color;
import android.graphics.Paint;
import android.util.AttributeSet;
import android.view.View;

public class MyView extends View
{
	// 声明画笔
	public Paint paint;
	public MyView(Context context , AttributeSet set)
	{
		super(context , set);
		paint = new Paint();
		paint.setColor(Color.RED);
	}
	@Override
	protected void onDraw(Canvas canvas)
	{
		super.onDraw(canvas);
		// 使用指定Paint对象画矩形
		canvas.drawRect(0, 0, getWidth(), getHeight(), paint);
	}
}
```
不同的填充方式
```
package org.crazyit.image;

import android.app.Activity;
import android.graphics.Bitmap;
import android.graphics.BitmapFactory;
import android.graphics.BitmapShader;
import android.graphics.Color;
import android.graphics.ComposeShader;
import android.graphics.LinearGradient;
import android.graphics.PorterDuff;
import android.graphics.RadialGradient;
import android.graphics.Shader;
import android.graphics.Shader.TileMode;
import android.graphics.SweepGradient;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;

public class MainActivity extends Activity
		implements OnClickListener
{
	// 声明位图渲染对象
	private Shader[] shaders = new Shader[5];
	// 声明颜色数组
	private int[] colors;
	MyView myView;
	// 自定义视图类
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		setContentView(R.layout.main);
		myView = (MyView)findViewById(R.id.my_view);
		// 获得Bitmap实例
		Bitmap bm = BitmapFactory.decodeResource(getResources()
				, R.drawable.water);
		// 设置渐变的颜色组，也就是按红、绿、蓝的方式渐变
		colors = new int[] { Color.RED, Color.GREEN, Color.BLUE };
		// 实例化BitmapShader，x坐标方向重复图形，y坐标方向镜像图形
		shaders[0] = new BitmapShader(bm, TileMode.REPEAT,
				TileMode.MIRROR);
		// 实例化LinearGradient
		shaders[1] = new LinearGradient(0, 0, 100, 100
				, colors, null, TileMode.REPEAT);
		// 实例化RadialGradient
		shaders[2] = new RadialGradient(100, 100, 80, colors, null,
				TileMode.REPEAT);
		// 实例化SweepGradient
		shaders[3] = new SweepGradient(160, 160, colors, null);
		// 实例化ComposeShader
		shaders[4] = new ComposeShader(shaders[1], shaders[2],
				PorterDuff.Mode.DARKEN);
		Button bn1 = (Button)findViewById(R.id.bn1);
		Button bn2 = (Button)findViewById(R.id.bn2);
		Button bn3 = (Button)findViewById(R.id.bn3);
		Button bn4 = (Button)findViewById(R.id.bn4);
		Button bn5 = (Button)findViewById(R.id.bn5);
		bn1.setOnClickListener(this);
		bn2.setOnClickListener(this);
		bn3.setOnClickListener(this);
		bn4.setOnClickListener(this);
		bn5.setOnClickListener(this);
	}
	@Override
	public void onClick(View source)
	{
		switch(source.getId())
		{
			case R.id.bn1:
				myView.paint.setShader(shaders[0]);
				break;
			case R.id.bn2:
				myView.paint.setShader(shaders[1]);
				break;
			case R.id.bn3:
				myView.paint.setShader(shaders[2]);
				break;
			case R.id.bn4:
				myView.paint.setShader(shaders[3]);
				break;
			case R.id.bn5:
				myView.paint.setShader(shaders[4]);
				break;
		}
		// 重绘界面
		myView.invalidate();
	}
}

```
<h1 id="0704">逐帧动画</h1>
 
[返回目录](#1)

[运动的熊猫](#0704_1)
[指定点爆炸](#0704_2)

<h1 id="0704_1">运动的熊猫</h1>

[返回目录](#0704) 
res下anim文件
oneshot 表示动画是否重复 true 不会重复 false 重复
duration 表明动画运行的时间
```
<?xml version="1.0" encoding="utf-8"?>
<!-- 指定动画循环播放 -->
<animation-list xmlns:android="http://schemas.android.com/apk/res/android"
	android:oneshot="false">
	<!-- 添加多个帧 -->
	<item android:drawable="@drawable/fat_po_f01" android:duration="60" />
	<item android:drawable="@drawable/fat_po_f02" android:duration="60" />
	<item android:drawable="@drawable/fat_po_f03" android:duration="60" />
	<item android:drawable="@drawable/fat_po_f04" android:duration="60" />
	<item android:drawable="@drawable/fat_po_f05" android:duration="60" />
	<item android:drawable="@drawable/fat_po_f06" android:duration="60" />
	<item android:drawable="@drawable/fat_po_f07" android:duration="60" />
	<item android:drawable="@drawable/fat_po_f08" android:duration="60" />
	<item android:drawable="@drawable/fat_po_f09" android:duration="60" />
	<item android:drawable="@drawable/fat_po_f10" android:duration="60" />
	<item android:drawable="@drawable/fat_po_f11" android:duration="60" />
	<item android:drawable="@drawable/fat_po_f12" android:duration="60" />
	<item android:drawable="@drawable/fat_po_f13" android:duration="60" />
	<item android:drawable="@drawable/fat_po_f14" android:duration="60" />
	<item android:drawable="@drawable/fat_po_f15" android:duration="60" />
	<item android:drawable="@drawable/fat_po_f16" android:duration="60" />
	<item android:drawable="@drawable/fat_po_f17" android:duration="60" />
	<item android:drawable="@drawable/fat_po_f18" android:duration="60" />
	<item android:drawable="@drawable/fat_po_f19" android:duration="60" />
	<item android:drawable="@drawable/fat_po_f20" android:duration="60" />
	<item android:drawable="@drawable/fat_po_f21" android:duration="60" />	
	<item android:drawable="@drawable/fat_po_f22" android:duration="60" />	
	<item android:drawable="@drawable/fat_po_f23" android:duration="60" />	
	<item android:drawable="@drawable/fat_po_f24" android:duration="60" />	
	<item android:drawable="@drawable/fat_po_f25" android:duration="60" />	
	<item android:drawable="@drawable/fat_po_f26" android:duration="60" />	
	<item android:drawable="@drawable/fat_po_f27" android:duration="60" />														
</animation-list>
```
动画的运行
```
// 获取AnimationDrawable动画对象
		final AnimationDrawable anim = (AnimationDrawable) imageView
				.getBackground();
		play.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View v)
			{
				// 开始播放动画
				anim.start();
			}
		});
		stop.setOnClickListener(new OnClickListener()
		{
			@Override
			public void onClick(View v)
			{
				// 停止播放动画
				anim.stop();
			}
		});
```

<h1 id="0704_2">指定点爆炸</h1>

[返回目录](#0704) 

资源
```
<?xml version="1.0" encoding="utf-8"?>
<!-- 定义动画只播放一次，不循环 -->
<animation-list xmlns:android="http://schemas.android.com/apk/res/android"
	android:oneshot="true" >
	<item android:drawable="@drawable/bom_f01" android:duration="80" />
	<item android:drawable="@drawable/bom_f02" android:duration="80" />
	<item android:drawable="@drawable/bom_f03" android:duration="80" />
	<item android:drawable="@drawable/bom_f04" android:duration="80" />
	<item android:drawable="@drawable/bom_f05" android:duration="80" />
	<item android:drawable="@drawable/bom_f06" android:duration="80" />
	<item android:drawable="@drawable/bom_f07" android:duration="80" />
	<item android:drawable="@drawable/bom_f08" android:duration="80" />
	<item android:drawable="@drawable/bom_f09" android:duration="80" />
	<item android:drawable="@drawable/bom_f10" android:duration="80" />
	<item android:drawable="@drawable/bom_f11" android:duration="80" />
	<item android:drawable="@drawable/bom_f12" android:duration="80" />
	<item android:drawable="@drawable/bom_f13" android:duration="80" />
	<item android:drawable="@drawable/bom_f14" android:duration="80" />
	<item android:drawable="@drawable/bom_f15" android:duration="80" />
	<item android:drawable="@drawable/bom_f16" android:duration="80" />
	<item android:drawable="@drawable/bom_f16" android:duration="80" />
	<item android:drawable="@drawable/bom_f17" android:duration="80" />
	<item android:drawable="@drawable/bom_f18" android:duration="80" />
	<item android:drawable="@drawable/bom_f19" android:duration="80" />
	<item android:drawable="@drawable/bom_f20" android:duration="80" />
	<item android:drawable="@drawable/bom_f21" android:duration="80" />
	<item android:drawable="@drawable/bom_f22" android:duration="80" />
	<item android:drawable="@drawable/bom_f23" android:duration="80" />
	<item android:drawable="@drawable/bom_f24" android:duration="80" />
	<item android:drawable="@drawable/bom_f25" android:duration="80" />
	<item android:drawable="@drawable/bom_f26" android:duration="80" />
	<item android:drawable="@drawable/bom_f27" android:duration="80" />
</animation-list>
```
资源代码的运用
```java
package org.crazyit.image;

import android.app.Activity;
import android.content.Context;
import android.graphics.Canvas;
import android.graphics.drawable.AnimationDrawable;
import android.media.MediaPlayer;
import android.os.Bundle;
import android.view.MotionEvent;
import android.view.View;
import android.view.View.OnTouchListener;
import android.widget.FrameLayout;
import android.widget.ImageView;

import java.lang.reflect.Field;


public class MainActivity extends Activity
{
	private MyView myView;
	private AnimationDrawable anim;
	private MediaPlayer bomb;
	public void onCreate(Bundle savedInstanceState)
	{
		super.onCreate(savedInstanceState);
		// 使用FrameLayout布局管理器，它允许组件自己控制位置
		FrameLayout frame = new FrameLayout(this);
		setContentView(frame);
		// 设置使用背景
		frame.setBackgroundResource(R.drawable.back);
		// 加载音效
		bomb = MediaPlayer.create(this, R.raw.bomb);
		myView = new MyView(this);
		// 设置myView用于显示blast动画
		myView.setBackgroundResource(R.anim.blast);
		// 设置myView默认为隐藏
		myView.setVisibility(View.INVISIBLE);
		// 获取动画对象
		anim = (AnimationDrawable) myView.getBackground();
		frame.addView(myView);
		frame.setOnTouchListener(new OnTouchListener()
		{
			@Override
			public boolean onTouch(View source, MotionEvent event)
			{
				// 只处理按下事件（避免每次产生两个动画效果）
				if (event.getAction() == MotionEvent.ACTION_DOWN)
				{
					// 先停止动画播放
					anim.stop();
					float x = event.getX();
					float y = event.getY();
					// 控制myView的显示位置
					myView.setLocation((int) y - 40, (int) x - 20);
					myView.setVisibility(View.VISIBLE);
					// 启动动画
					anim.start();
					// 播放音效
					bomb.start();
				}
				return false;
			}
		});
	}
	// 定义一个自定义View，该自定义View用于播放“爆炸”效果
	class MyView extends ImageView
	{
		public MyView(Context context)
		{
			super(context);
		}
		// 定义一个方法，该方法用于控制MyView的显示位置
		public void setLocation(int top, int left)
		{
			this.setFrame(left, top, left + 40, top + 40);
		}
		// 重写该方法，控制如果动画播放到最后一帧时，隐藏该View
		@Override
		protected void onDraw(Canvas canvas) // ①
		{
			try
			{
				Field field = AnimationDrawable.class
						.getDeclaredField("mCurFrame");
				field.setAccessible(true);
				// 获取anim动画的当前帧
				int curFrame = field.getInt(anim);
				// 如果已经到了最后一帧
				if (curFrame == anim.getNumberOfFrames() - 1)
				{
					// 让该View隐藏
					setVisibility(View.INVISIBLE);
				}
			}
			catch (Exception e)
			{
			}
			super.onDraw(canvas);
		}
	}
}

```
位置计算
![](http://i.imgur.com/s7nxIOP.jpg)

<h1 id="0705"></h1>

[返回目录](#1) 

[](#0705_1)
[](#0705_2)
[](#0705_3)


<h1 id="0705_1"></h1>

[返回目录](#0705) 

```
1
```

<h1 id="0705_2"></h1>

[返回目录](#0705) 

```
1
```

<h1 id="0705_3"></h1>

[返回目录](#0705) 

```
1
```