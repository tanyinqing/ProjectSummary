

# 这是 utils 的综合文档
在写作时可以运用搜索的方法找到相应的位置


<h1 id="00">目录</h1> 

> # 简介  
>> ## 1.针对安卓常用到的工具类
> # 目录
>> ## 1. 内存卡日志  [链接](#01)  [源码调用](#0101)  [源码](#0102)       
>> ## 2. 日志 [链接](#02)  [源码调用](#0201) [源码](#0202)
       

<h1 id="01"> 内存卡日志</h1>

>> # 简介   [返回目录](#00)
>> ##  <h1 id="0101">1. 源码调用</h1>
>> ##  <h1 id="0102">2. 源码</h1>

```  
        package com.yzkj.codewarehouse.basiclibrary.MyUtils;

import android.os.Environment;
import android.util.Log;


import com.yzkj.codewarehouse.basiclibrary.Constant;

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

    //   LogTxt.writeLog("小谈你好","小谈测试");
    public static void writeLog(String context,String fileName){
        if (Constant.CeShiBanKai){  //这个值该为false后就不会在打印日志了

       // String filePath = "/sdcard/Test/";
        if(!Environment.getExternalStorageState().equals(Environment.MEDIA_MOUNTED)){
            Log.e("ImagesUtil.java", "没有SD卡,无法保存.");
            return ;
        }

        //文件命名的时间成分
        Calendar calendar=Calendar.getInstance();
        Date data=calendar.getTime();
       // SimpleDateFormat format=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        SimpleDateFormat format=new SimpleDateFormat("  HH:mm:ss");
        String time=format.format(data);

        // 获得外部SD卡,创建本应用程序的保存目录,保存相片
        File sdCard = Environment.getExternalStorageDirectory();
        File photoDir = new File(sdCard.getAbsolutePath() + "/"+"LogTan");
        if(!photoDir.exists()){
            photoDir.mkdirs();
        }


        // 每次写入时，都换行写
        String strContent = context + "\r\n";
        //String strContent = context;
        try {
            File file = new File(photoDir,String.valueOf(xuhao)+"  "+fileName+time+".txt");
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
            if (xuhao<50){
                xuhao++;
            }else {
                xuhao=0;
                //删除缓存的Log信息 每次启动时
                String  DATABASE_NAME="LogTan";
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

<h1 id="02"> 日志</h1>

>> # 简介   [返回目录](#00)
>> ## <h1 id="0201">1. 源码调用</h1>
>> ## <h1 id="0202">2. 源码</h1>


```
package com.yzkj.codewarehouse.basiclibrary.MyUtils;

import android.util.Log;

/**
 * Created by Administrator on 2016/9/27 0027.
 */
public class MyLog {
    //过滤 返回的所有数据
    private static String TAG="tanyinqing";

    //关闭所有的Log数据的打印
    private static Boolean ifShow=true;

    public static void ShowLog(String content){
      /*  if (Constant.CeShiBanKai){
            Log.d(TAG1, content);
        }*/
        if (ifShow){
            Log.d(TAG, content);
        }
    }
}

```










<h1 id="02"> 内存卡日志</h1>

>> # 简介   [返回目录](#00)
>> ##  <h1 id="0201">1. 源码调用</h1>
>> ##  <h1 id="0202">2. 源码</h1>

```

```