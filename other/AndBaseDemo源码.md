 # 2017 07 18
>  [文档地址](http://pan.baidu.com/disk/home?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&#list/vmode=list&path=%2F%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6%E5%A4%B9%2F%E5%AE%89%E5%8D%93%E9%A1%B9%E7%9B%AE%E4%BB%A3%E7%A0%81%E4%BB%93%E5%BA%93%2FMarkDown%E5%BC%80%E5%8F%91%E6%96%87%E6%A1%A3 "查看")

<h1 id="1">1 com.ab.util</h1>  
[1. 类 AbToastUtil](#101) ——  [2. View](#102)

参考文档
[百度项目地址](97 "查看")

 <h1 id="101">1. 类 AbToastUtil</h1>
 
 [返回目录](#1) 
 
```
package codewarehouse.yzkj.com.ceshi;


import android.content.Context;
import android.os.Bundle;
import android.os.Handler;
import android.os.Message;
import android.widget.Toast;
import com.ab.util.AbStrUtil;

public class AbToastUtil {
    private static Context mContext = null;
    public static final int SHOW_TOAST = 0;
    private static Handler baseHandler = new Handler() {
        public void handleMessage(Message msg) {
            switch(msg.what) {
                case 0:
                    //这个是静态的方法
                    AbToastUtil.showToast(AbToastUtil.mContext, msg.getData().getString("TEXT"));
                default:
            }
        }
    };

    public AbToastUtil() {
    }

    public static void showToast(Context context, String text) {
        mContext = context;
        if(!AbStrUtil.isEmpty(text)) {
            Toast.makeText(context, text,Toast.LENGTH_LONG).show();
        }

    }

    public static void showToast(Context context, int resId) {
        mContext = context;
        Toast.makeText(context, "" + context.getResources().getText(resId),Toast.LENGTH_LONG).show();
    }

    public static void showToastInThread(Context context, int resId) {
        mContext = context;
        Message msg = baseHandler.obtainMessage(0);
        Bundle bundle = new Bundle();
        bundle.putString("TEXT", context.getResources().getString(resId));
        msg.setData(bundle);
        baseHandler.sendMessage(msg);
    }

    public static void showToastInThread(Context context, String text) {
        mContext = context;
        Message msg = baseHandler.obtainMessage(0);
        Bundle bundle = new Bundle();
        bundle.putString("TEXT", text);
        msg.setData(bundle);
        baseHandler.sendMessage(msg);
    }
}

```