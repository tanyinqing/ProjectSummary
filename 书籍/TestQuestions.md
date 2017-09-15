 # 2017 08 17
>  [文档地址](http://pan.baidu.com/disk/home?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&#list/vmode=list&path=%2F%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6%E5%A4%B9%2F%E5%AE%89%E5%8D%93%E9%A1%B9%E7%9B%AE%E4%BB%A3%E7%A0%81%E4%BB%93%E5%BA%93%2FMarkDown%E5%BC%80%E5%8F%91%E6%96%87%E6%A1%A3 "查看") ——  [源文件相关](http://pan.baidu.com/disk/home?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&#list/vmode=list&path=%2F%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6%E5%A4%B9%2F%E9%A1%B9%E7%9B%AE%E6%A8%A1%E5%9D%97%2FAndBaseDemo%E6%A1%86%E6%9E%B6 "查看") ——  [发布网址](http://www.jianshu.com/p/86f8894e8990)——  [android 源码的地址](http://androidxref.com/6.0.1_r10/xref/frameworks/base/core/java/android/) ——  [个人首页](https://tanyinqing.github.io/)

<h1 id="1">1 一天一题</h1>  

[1. 对Service组件理解](#101) ——  [2. 广播的学习](#102) —— [3. Activity](#103) —— [4. 如何判断Activity是否在运行](#104) —— [5. 自定义View的状态是如何保存的](#105)  —— [7.Java的值传递和引用传递问题](#107)  —— [8. 讲讲Android的Handler机制吗](#108)  —— [9. 两个Activity之间如何传递参数](#109)  —— [10. 如何理解Android中的Context，它有什么用](#110)  —— [11. 一个人的工作年限和水平并不能成正比](#111)  —— [13. 在项目中使用AsyncTask会有什么问题吗](#113)  —— [14. 修改SharedPreferences后两种提交方式有什么区别？](#114)  —— [15. 能说说Android为什么要设计ContentProvider这个组件吗](#115)  —— [21. res目录－细节处见真章](#121)  —— [25. 进程和线程](#125) —— [26. ScrollView嵌套ListView的事件冲突](#126) —— [29. 内存泥潭](#129) —— [30. 老外的自定义View面试题](#130)  —— [34. 常去的Android相关站点](#134)  —— [36. AIDL](#136) 

<h1 id="2">2 个人实践理解</h1>  

[1. 面试要求](#0201)

参考文档

[goeasyway的106篇文章](http://www.jianshu.com/u/f9fbc7a39b36 "查看")

 <h1 id="101">1. 对Service组件理解</h1>
 
 [返回目录](#1) 
 [参考网站](http://www.jianshu.com/p/7a7db9f8692d)


面试题：
> 知道Service吗，它有几种启动方式？
 
Service是一个专门在后台处理长时间任务的Android组件，它没有UI。它有两种启动方式，startService和bindService。 
> 这两种启动方式的区别。

startService只是启动Service，启动它的组件（如Activity）和Service并没有关联，只有当Service调用stopSelf或者其他组件调用stopService服务才会终止。
bindService方法启动Service，其他组件可以通过回调获取Service的代理对象binder和Service交互，而这两方也进行了绑定，当启动方销毁时，Service也会自动进行unBind操作，当发现所有绑定都进行了unBind时才会销毁Service。
![](http://upload-images.jianshu.io/upload_images/1685558-5b9c3263c0af2ea2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
> Service的onCreate回调函数可以做耗时的操作吗？

如果知道Service的onCreate是在主线程（ActivityThread）中调用的，耗时操作会阻塞UI
> 如果需要做耗时的操作，你会怎么做？

 当面试者回答到线程和Handler方式时
> 是否知道IntentService，在什么场景下使用IntentService？

这也是面试官要看的点，真正的项目需要一个开发人员对某个问题有一定的深度，也需要对整个Android的知识点有一定的广度。深度代表这个人对问题认真对待有钻研的精神，广度代表这个人在面对同一个问题时，会更容易从多种可行的方案中选出最合适的一种。

>场景：如果一个应用要从网络上下载MP3文件，并在Activity上展示进度条，这个Activity要求是可以转屏的。那么在转屏时Actvitiy会重启，如何保证下载的进度条能正确展示进度呢？
没有Service概念的人，一般想出来的方案如下：

在转屏前将进度缓存，转屏后再读出来。
使用android:configChanges设置，让转屏时Activity不销毁和重建。
针对第1个方案，我会继续问他将进度值存在哪里？ 转屏的过程中，我们知道Activity的重建算是比较耗时的，会可能会有几百毫秒以上，那么这时候下载线程仍然在工作，进度肯定和保存时的进度不一致了，如何处理这个问题呢？

第2个方案，大家可以自己展开思考，实际的项目中可能会需要额外做一些事情来处理ContentView的横竖布局的问题。

如果使用Service来解决这个问题，看似是比较完美的，不过就会涉及Activity（UI）和Service的交互问题，这个我们以后再讨论。

>Service和UI的交互也让这个方式变得不那么简便。如果你只需要在当前界面去做一些耗时操作，界面退出或改变时，工作也要停止，那么这时直接使用Thread（或者AsyncTask, ThreadHandler）会更合适你。


 <h1 id="102">2. 广播的学习</h1>
 
 [返回目录](#1) 
 [参考网站](http://www.jianshu.com/p/df7af437e766)
> 常用的方式是直接调用Context的接口（sendBroadcast & sendOrderBroadcast）发送两类型的广播

Normal broadcasts无序广播，会异步的发送给所有的Receiver，接收到广播的顺序是不确定的，有可能是同时。
Ordered broadcasts有序广播，广播会先发送给优先级高(android:priority)的Receiver，而且这个Receiver有权决定是继续发送到下一个Receiver或者是直接终止广播。

>静态和动态的两种注册Receiver的方式,还有其他类型的广播吗？

可以使用sendStickyBroadcast发送Sticky类型的广播。Sticky简单说就是，在发送广播时Reciever还没有被注册，但它注册后还是可以收到在它之前发送的那条广播。

>有时候基于数据安全考虑，我们想发送广播只有自己（本进程）能接收到，那么该如何去做呢？

然后可能使用Handler，没错，往主线程的消息池（Message Queue）发送消息，只有主线程的Handler可以分发处理它，广播发送的内容是一个Intent对象，我们可以直接用Message封装一下，留一个和sendBroadcast一样的接口。在handleMessage时把Intent对象传递给已注册的Receiver。

后来在看项目组的其他同事写代码时，发现还有一个LocalBroadcastManager类，查了一下官方文档是Support V4包里的一个类，其实现方式也是使用Handler，思路也是一样的。

> BroadcastReceiver的生命周期

有些人并不态清楚Receiver也是有生命周期的，而且很短，当它的onReceive方法执行完成后，它的生命周期就结束了。这时BroadcastReceiver已经不处于active状态，被系统杀掉的概率极高，也就是说如果你在onReceive去开线程进行异步操作或者打开Dialog都有可能在没达到你要的结果时进程就被系统杀掉。因为这个进程可能只有这个Receiver这个组件在运行，当Receiver也执行完后就是一个empty进程，是最容易被系统杀掉的。替代的方案是用Notificaiton或者Service（这种情况当然不能用bindService）

> 回到今天的面试题，使用广播来更新界面是否合适？

更新界面也分很多种情况，如果不是频繁地刷新，使用广播来做也是可以的。但对于较频繁地刷新动作，建议还是不要使用这种方式。广播的发送和接收是有一定的代价的，它的传输是通过Binder进程间通信机制来实现的（细心人会发现Intent是实现了Parcelable接口的），那么系统定会为了广播能顺利传递做一些进程间通信的准备。

除此之外，还可能有其他的因素让广播发送和到达是不准时的（或者说接收是会延时）。曾经看到有人在论坛上抱怨发几个广播都卡，Google的工程师是怎么混饭吃的。

这种情况可能吗？很可能，而且很容易发生。我们要先了解Android的ActivityManagerService有一个专门的消息队列来接收发送出来的广播，sendBroadcast执行完后就立即返回，但这时发送来的广播只是被放入到队列，并不一定马上被处理。当处理到当前广播时，又会把这个广播分发给注册的广播接收分发器ReceiverDispatcher，ReceiverDispatcher最后又把广播交给接Receiver所在的线程的消息队列去处理（就是你熟悉的UI线程的Message Queue）。

整个过程从发送--ActivityManagerService--ReceiverDispatcher进行了两次Binder进程间通信，最后还要交到UI的消息队列，如果基中有一个消息的处理阻塞了UI，当然也会延迟你的onReceive的执行。

小结

>在项目里还是有遇到开发骨干也会在onReceive中开线程做耗时操作，很多时候他们这样做了并不会立刻就会产生问题，但是并不等于不会产生问题，当设备达到特定的临界条件时（如内存紧张），这些问题往往会在最终用户那里报出来。我们都有经验由用户报出来的随机BUG往往难于跟踪和修复，所以理解清楚一些基础的机制是很有必要的，它们能帮助我们避免一些隐藏的风险。

 <h1 id="103">3. Activity</h1>
 
 [返回目录](#1) 
 [参考网站](http://www.jianshu.com/p/ae6e1d93cc8e)
>Activity生命周期图
![](http://upload-images.jianshu.io/upload_images/1685558-d3176065dcf72d21.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如果一个Activity在用户可见时才处理某个广播，不可见时注销掉，那么应该在哪两个生命周期的回调方法去注册和注销BroadcastReceiver呢？

Activity 的可见生命周期发生在 onStart调用与 onStop调用之间。在这段时间，用户可以在屏幕上看到 Activity 并与其交互。我们可以在 onStart中注册一个 BroadcastReceiver以监控影响 UI 的变化，并在用户无法再看到您显示的内容时在 onStop中将其取消注册。

如果对方回答是在onResume和onPause方法中，那么你可以去引导对方看看在这两个方法有什么不好的地方。

>如果有一些数据在Activity跳转时（或者离开时）要保存到数据库，那么你认为是在onPause好还是在onStop执行这个操作好呢？

这题的要点和上一题是一样的，onPause较容易被触发，所以我们在做BroadcastReceiver注销时放在onStop要好些。onPause时Activity界面仍然是可见的，如弹出一个Dialog时。但在保存数据时，放在onPause去做可以保证数据存储的有效性，如果放在onStop去做，在某些情况下Activity走完onPause后有可能还没顺利走到onStop就被系统回收了。

>简单说一下Activity A启动Activity B时，两个Activity生命周期的变化

当一个 Activity 启动另一个 Activity 时，它们都会发生生命周期转变。第一个 Activity 暂停然后停止（但如果它在后台仍然可见，则不会停止，比如B是半透明的），系统会创建另一个 Activity。 如果这两个Activity 共用保存数据到文件或者数据库，必须要注意，在创建第二个 Activity 前，第一个 Activity 不会完全停止。更确切地说，启动第二个 Activity 的过程与停止第一个 Activity 的过程存在重叠。

>Activity A 的 onPause方法执行。
Activity B 的 onCreate、onStart和 onResume方法依次执行。
然后，如果 Activity A 在屏幕上不再可见，则其 onStop方法执行。

您可以利用这种可预测的生命周期回调顺序管理从一个 Activity 到另一个 Activity 的信息转变。 例如，如果您必须在第一个 Activity 停止时向数据库写入数据，以便下一个 Activity 能够读取该数据，则应在 onPause而不是 onStop执行期间向数据库写入数据。

>编程能力是一个很复杂的体系，不能光看有技术含量或者高大上的算法才叫有能力，和悟道一样，我认为认识理清Android体系，顺应它的道（机制）开发应用也是一种能力。


 <h1 id="104">4. 如何判断Activity是否在运行</h1>
 
 [返回目录](#1) 
 [参考网站](http://www.jianshu.com/p/f8a0c43b3dfe)

>* 我一般面试技术分两方面了解面试者，一是测重问面试者细节的地方，看对方是否真如简历上所说对XX“精通”、“熟悉”、“有一定的见解”，有实践经验的积累。别一种是侧重考察对方对问题（可以是未知问题）的理解和解决问题的思路。

>* 从Activity A 启动一个线程去进行网络上传操作，在A中设立一个回调函数，当上传操作完成以后，在A的这个回调函数中会弹出一个对话框，用来显示回调信息。可是当上传的过程还在进行的时候，我按下back键，A的activity 被销毁了，可是那个上传的线程还在进行，当那个线程结束后，本来应该在A中弹出一个对话框，可是由于A已经不存在了，系统就会报错提示，“将对话框显示在不存在的页面上”，然后程序就挂掉了。

我看到过很多人用Handler来充当上面所提到的“回调函数”，即工作线程完成工作后，通过主线程的Handler处理UI更新，如弹出提示Dialog。可能有些人没有弄明白，Activity都被系统销毁了，工作线程怎么还能调它的变量呢？其实所谓的Activity销毁只是不再受系统的AMS控制，但Activity这个对象的实例还是存在于内存中的，具体什么时候真正把这个对象实例也销毁（回收）了，就要看内存回收机制了，哪怕是这个实例没有可达的引用了也不一定会马上回收。

//判断Activity是否被回收了
 public boolean isFinishing() {
        return mFinished;
    }

而mFinished是在finish()中被赋值的，也就是说只有通过调用finish()结束的Activity，mFinished的值才会被置为true。所以有时候Activity的生命周期没有按我们预想的来走时（如内存紧张时），会出现判断出错的情况。

看看Google工程师是怎么判断的（来源于Android源码中的Call应用，AsyncTask中的onPostExecute片段）：

```
@Override
    protected void onPostExecute(Void result) {
        final Activity activity = progressDialog.getOwnerActivity();

        if (activity == null || activity.isDestroyed() || activity.isFinishing()) {
            return;
        }

        if (progressDialog != null && progressDialog.isShowing()) {
            progressDialog.dismiss();
        }
    }

```
 小结

>如果对方没听说过isFinishing函数，那可以让他从自己的角度看如何解决这个问题，正好可以看看他的逻辑思维是否清晰合理。工作中往往会遇到，一些求职者由于之前是做其他方面刚转Android开发，对Android的了解还不够，但有很强理解和学习能力，通过引导发现他可以快速的得到合理的解决方案的话，我一般都很乐意要这样的人。

 <h1 id="105">5. 自定义View的状态是如何保存的</h1>
 
 [返回目录](#1) 
 [参考网站](http://www.jianshu.com/p/7a7db9f8692d)

>面试题：自定义View的状态是如何保存的？

Android有一套标准的做法，做过自定义View的人很容易遇到这个问题，因为Activity转屏，或Home键到后台很容易在被系统销毁，恢复时我们肯定是希望看到View保持之前状态。

注：无法保证系统会在销毁Activity前一定调用onSaveInstanceState，例如用户使用“返回” 按退出 Activity 时，因为用户的行为是在显式关闭 Activity，所以不会调用onSaveInstanceState。

>如果系统调用onSaveInstanceState，那么它是在onStop还是在onPause之前执行呢？

可以肯定的是它会在调用 onStop之前，但是是不是在onPuase之前就不能确认了，要看情况，官方文档在说明这个执行顺序时用了“可能”这个词。

#小结

>Activity类的onSaveInstanceState默认实现会恢复Activity的状态，默认实现会为布局中的每个View调用相应的 onSaveInstanceState方法，让每个View都能保存自身的信息。

>这里需要注意一个细节：想要保存View的状态，需要在XML布局文件中提供一个唯一的ID（android:id），如果没有设置这个ID的话，View控件的onSaveInstanceState是不会被调用的。

 <h1 id="107">7. Java的值传递和引用传递问题</h1>
 
 [返回目录](#1) 
 [参考网站](http://www.jianshu.com/p/c0c5e0540928)

回到面试上，今天聊一下和Java相关的面试题。没错总有那么一些公司在招Android程序员时，比较侧重考察Java基础和能力的。Java的值传递和引用传递问题，相信很多人都被问题过，当然很多时候面试官都不会这么直白的问，他们会给你设计一个方法让你给出执行这个方法后的输出结果。

>面试题： Java的值传递和引用传递问题

>“在Java里面参数传递都是按值传递”
这句话的意思是：按值传递是传递的值的拷贝，按引用传递其实传递的是引用的地址值，所以统称按值传递。

简单的说，基本类型是按值传递的，方法的实参是一个原值的复本。类对象是按对象的引用地址（内存地址）传递地址的值，那么在方法内对这个对象进行修改是会直接反应在原对象上的（或者说这两个引用指向同一内存地址）。不过要注意String这个类型，如下代码

#结论
>我只能说，知道的话确实不比别人多能耐，只是多了一份从容。

 <h1 id="108">8. 讲讲Android的Handler机制吗</h1>
 
 [返回目录](#1) 
 [参考网站](http://www.jianshu.com/p/108db0240a34)
要讲清楚Android中的消息机制，肯定要先表述一下和Handler相关的一些类：
>Message：消息分为硬件产生的消息(如按钮、触摸)和软件生成的消息；
MessageQueue：消息队列的主要功能向消息池投递消息(MessageQueue.enqueueMessage)和取走消息池的消息(MessageQueue.next)；
Handler：消息辅助类，主要功能向消息池发送各种消息事件(Handler.sendMessage)和处理相应消息事件(Handler.handleMessage)；
Looper：不断循环执行(Looper.loop)，按分发机制将消息分发给目标处理者。

比如会问在一个工作线程中创建自己的消息队例应该怎么做？
是否知道要调用Looper.prepare（在每个线程只允许执行一次）。

再问问是否用过HandlerThread，它有什么优缺点等。

#注意：Handler可能会引起的内存泄露

#结论
诸如Handler这类耳熟能详的概念，但其实用起来又不复杂，面试时一般会更在意对方的表达上，看对方是否能用语言有效的组织语句。最后针对一个问题，还是要用一点小的细节验证对方是否正的做过。有些网友可能会觉得是被故意刁难，但如果面试官只提出一个问题，你说了答案后他就嗯一下就立即问下一主题，没有和你就这个问题再扩展一下，你是否也会觉得他什么都不懂，也会质疑他能否辨别出面试者的真实水平？

 <h1 id="109">9. 两个Activity之间如何传递参数</h1>
 
 [返回目录](#1) 
 [参考网站](http://www.jianshu.com/p/be593134eeae)

>大多数时候，我们也就传递一些简单的int，String类型的数据，实际中也有看到传递List和Bitmap的。

使用Intent的Bundle协带参数，就是我们常用的Intent.putExtra方法。

>除了传递基本类型外，如何传递自定义的对象呢？

这个问题就是想引出Android的Parcelable。一般很多面试者都有用过传递实现了Serializable接口的自定义对象的经验，因为这个很简单，加句代码就搞定了。而Parcelable的实现要多一些代码，典型的写法如下：

>那我们为什么要考察对方会不会用Parcelable呢？先看一下这Parcelable和Serializable的区别：

Serializalbe会使用反射，序列化和反序列化过程需要大量I/O操作，Parcelable自已实现封送和解封（marshalled &unmarshalled）操作不需要用反射，数据也存放在Native内存中，效率要快很多。

>现在我们知道了如何传递自定义的对象，那么在两个Activity之前传递对象还要注意什么呢？

一定要要注意对象的大小，Intent中的Bundle是在使用Binder机制进行数据传递的，能使用的Binder的缓冲区是有大小限制的（有些手机是2M），而一个进程默认有16个binder线程，所以一个线程能占用的缓冲区就更小了（以前做过测试，大约一个线程可以占用128KB）。所以当你看到“The Binder transaction failed because it was too large.”这类TransactionTooLargeException异常时，你应该知道怎么解决了。

 <h1 id="110">1. 如何理解Android中的Context，它有什么用</h1>
 
 [返回目录](#1) 
 [参考网站](http://www.jianshu.com/p/0754e65a5744)
 
>Application（或者Service）和Activity都可以调用Context的startActivity方法，那么在这两个地方调用startActivity有区别吗？

就会知道在Application（或者Service）需要给Intent设置Intent.FLAG_ACTIVITY_NEW_TASK才能正常启动Activity，这就会引出Activity的Task栈问题，以后再做分析。

理解Context，对于我经历的项目来说，最有用的就是对于插件框架的开发了。如果有面试官问你:
>Context的实例是什么时候创建的？一个应用里面会有几个Context的实例？

对于一般的应用来说，你会觉得这两个问题很无聊。但如果你需要做插件开发，上面的问题就变成是很关键的问题了。你的插件框架会是一个小型的Android Framework层，你当然得自己处理插件的Application和Activity创建，那么你肯定要解决好这两个问题。详情可以查看ActivityThread这个类的源码。

#小结

有网友问“面试官是怎么考虑求职者的经验、学历、编程水平”这些方面的，其实这个问题不能脱离实际的公司和项目来回答。我只能说几个场景，有些公司有人才培养计划 项目也不紧张，那么他们在招人时是以培养和贮备为目的，会更重视面试者的理解和学习能力。但如何一家公司急切需要人进来解决问题，他们就会更在乎你的项目经验了，最好是直接招以前就做过类似项目的。如果一家公司只是需要码农来搬代码，那么只要不是太差的，他们会更看重性价比。

所以有公司关注这些对Context或Framework方面的理解的面式题，一是他们应用可能遇到了一些问题，需要一些对机制比较了解的开发来解决；二是想通过这类问题，考察面试者是否真如简历上般资深，因为他们相信做多了项目的人，很容易遇到机制方面的问题

<h1 id="111">11. 一个人的工作年限和水平并不能成正比</h1>
 
 [返回目录](#1) 
 [参考网站](http://www.jianshu.com/p/8fd5fa90ee6c)
后来我经常思考，是什么样的原因导致一个人的工作年限和水平并不能成正比。我想到有两个方面：
>看待问题的眼界过窄，只能看到当前的可见的问题。（或者说他思考问题的角度和方式有较大的局限）
技术的要点没有掌握，常常找不到合理的解决问题的方案。

这两点都是需要慢慢地提升和积累，当一个人长时间在思维和眼界上没有进步，技术也只懂些皮毛（或者只是会用），那么他工作越长时间他的优势反而越不明显，甚至变成劣势。

##面试题：如何优化ListView的性能？##
>所以我们不妨先思考一下如下的几个问题：
在一次显示ListView的界面时，getView会被执行几次？
每次getView执行时间应该控制在多少毫秒之内？
getView中设置listener要注意什么？

了解了这几个问题，现在我们回来这次主要考查的面试题上，如何进行ListView的性能优化，让它滑动更加流畅。大家一般常用如下方法：

>重用ConvertView;
使用View Holder模式；
使用异步线程加载图片（一般都是直接使用图片库加载，如Glide, Picasso）；

我认为这些是面试者必备的知识点，如果连这些都说不清楚的话，也没有必要再深入问了。针对面试者的回答，可以适当选一两点追问一下，看是否真正明白。如：ViewHolder为什么能够起到优化性能的作用？

除此之前还有一些优化建议：

>在adapter的getView方法中尽可能的减少逻辑判断，特别是耗时的判断；
避免GC（可以从LOGCAT查看有无GC的LOG）；
在快速滑动时不要加载图片；
将ListView的scrollingCache和animateCache这两个属性设置为false（默认是true）;
尽可能减少List Item的Layout层次（如可以使用RelativeLayout替换LinearLayout，或使用自定的View代替组合嵌套使用的Layout）；

``` 
<Listview
 android:scrollingCache="false" 
 android:animationCache="false"
``` 

<h1 id="113">13. 在项目中使用AsyncTask会有什么问题吗</h1>
 
 [返回目录](#1) 
 [参考网站](http://www.jianshu.com/p/7a7db9f8692d)

>面试题：在项目中使用AsyncTask会有什么问题吗？

AnsycTask执行任务时，内部会创建一个进程作用域的线程池来管理要运行的任务，也就就是说当你调用了AsyncTask.execute()后，AsyncTask会把任务交给线程池，由线程池来管理创建Thread和运行Therad。最后和UI打交道就交给Handler去处理了

>AsyncTask容易引发的Activity内存泄露

如果AsyncTask被声明为Activity的非静态的内部类，那么AsyncTask会保留一个对创建了AsyncTask的Activity的引用。如果Activity已经被销毁，AsyncTask的后台线程还在执行，它将继续在内存里保留这个引用，导致Activity无法被回收，引起内存泄露。

<h1 id="114">1. 修改SharedPreferences后两种提交方式有什么区别？</h1>
 
 [返回目录](#1) 
 [参考网站](http://www.jianshu.com/p/4dd53e1be5ba)

commit这种方式很常用，在比较早的SDK版本中就有了，这种提交修改的方式是同步的，会阻塞调用它的线程，并且这个方法会返回boolean值告知保存是否成功（如果不成功，可以做一些补救措施）。
而apply是异步的提交方式，目前Android Studio也会提示大家使用这种方式。

多进程操作和读取SharedPreferences的问题

>在SDK 3.0及以上版本，可以通过Context.MODE_MULTI_PROCESS属性来实现SharedPreferences多进程共享。如下设置

``` 
public static SharedPreferences getSharedPreferences(String name) {
        if (null != context) {
            if (Build.VERSION.SDK_INT >= 11) {
                return context.getSharedPreferences(name, Context.MODE_MULTI_PROCESS);
            } else {
                return context.getSharedPreferences(name, Context.MODE_PRIVATE);
            }
        }

        return null;
    }

``` 
<h1 id="115">15. 能说说Android为什么要设计ContentProvider这个组件吗</h1>
 
 [返回目录](#1) 
 [参考网站](http://www.jianshu.com/p/380231307070)

android:exported属性非常重要。这个属性用于指示该服务是否能够被其他应用程序组件调用或跟它交互。

#小结

初学开发或者开发经验少的人，往往不喜欢在写代码时思考如何应对以后可能产生的变化和相关接口的扩展能力，所以他们往往看不到ContentProvider的巨大好处。我觉得一般常见到的组件或概念，大家不一定需要每个都去偿试写写代码Demo（当然这样最好），但我认为对它们仍然需要有足够的重视，要去理清它的计设思路和使用场景。这样对你是极好的，之后你在面对问题时才会有多种解决方案的选择机会。

人生，比的不就是谁有更多的选择吗？

正如一个后来参与我们讨论的阿里项目经理所说的观点一样，在面试时不一定非要看对方的技术能力，对方的理解力和解决问题的思路也很重要，而对理解力这方面的问题其实可以通过简单的交谈技巧来得到答案。

<h1 id="121">21. res目录－细节处见真章</h1>
 
 [返回目录](#1) 
 [参考网站](http://www.jianshu.com/p/46ce37b8553c)

#小结

我在面试是常把面试者分做两类。一类是打下手的开发，做一些功能或业务模块实现，修修BUG保证应用正常运行；另一类是主创型开发，也可以叫主力开发，他们对应用开发的各个模块都有了解，可以熟练地从零开始搭建出整个项目框架。

而现在面试者一但有几年工作经历，往往在简历和交谈中夸大他们对项目的贡献，本来只是一个打下手的却被抬高成了主力开发。一个人打过多年下手，也会积累很多开发经验，但并不等于他就能适应主力开发的工作，主力选手除了经验的积累外更重要的是思维方式的改变，注重接口的设计胜过功能代码的实现。

如果我们要招一个有经验的主力型选手，还是很有必要通过一个细节来检验他们的。不过还是要提醒一下面试官，对细节的提问要注意到必需的知识和冷门少用到的知识，问对方过于偏僻的细节点往往起不到效果。

<h1 id="125">25. 进程和线程</h1>
 
 [返回目录](#1) 
 [参考网站](http://www.jianshu.com/p/7a7db9f8692d)
 >面试题：如何理解Android应用的进程？
 
 进程是一个动态的过程，每一个App的运行都是在一个独立的进程中，进程有自己独立的内存和数据空间，进程的名字就是App的packageName,并受AMS（ActivityManagerService）管理。

同一App的所有组件均在相同的进程中运行，但也可以允许App有多个进程。在AndroidManifest.xml里边给四大组件配置android:process属性，就可以让这些组件在指定的进程中运行，这些进程名字都是packageName:name这种，以区分是属于哪个App，我一般称之为辅助进程。

常有些开发不知道为什么自己的Application.onCreate中的代码执行了两次，如果你遇到这样的情况可以检查一下AndroidManifest.xml是否给某个组件配置了android:process属性。每个进程创建后，都会启动一个主线程（Looper接收消息），每个组件启动前都会先创建Application实例（一个进程只创建一个）。

>对于一般提高进程优先级的方法，大家还是应该了解一些。

进程要运行一些组件，不要成为空进程。
远行一个Service，并设置为前台运行方式（startForeground）。
AndroidManifest.xml中配置persistent属性（persistent的App会被优先照顾，进程优先级设置为PERSISTENT_PROC_ADJ=-12）

```
private void keepAlive() {
        try {
            Notification notification = new Notification();
            notification.flags |= Notification.FLAG_NO_CLEAR;
            notification.flags |= Notification.FLAG_ONGOING_EVENT;
            startForeground(0, notification); // 设置为前台服务避免kill，Android4.3及以上需要设置id为0时通知栏才不显示该通知；
        } catch (Throwable e) {
            e.printStackTrace();
        }
    }

```
在Service的onCreate方法调用keepAlive()即可，其实就是是欺骗系统把自己当成一个一直在通知栏的Notification。不过这种方式，并不保证在所有的机型上都有效。
#线程#
线程是CPU调度的基本单元，一个应用都有一个主线程负责处理消息。一个应用启动后，至少会有3个线程，一个主线程（UI线程）和2个Binder线程

线程间可以共享资源，为了保存UI的更新不会混乱，所以更新UI控件时要求在主线程进行更新，即需要保证更新UI是线程安全的。有时还可以问问面试者，什么是线程安全，貌似不知道这个概念的人也不少。

<h1 id="126">26. ScrollView嵌套ListView的事件冲突</h1> 

 [返回目录](#1) 
 [参考网站](http://www.jianshu.com/p/9abf6a874feb)

>如何解决ScrollView嵌套中一个ListView的滑动冲突？

ScrollView的重写了measureChildWithMargins方法导致它的子View的高度被强制设置成了MeasureSpec.UNSPECIFIED模式。

```
public class MyListView extends ListView {

    public MyListView(Context context) {
        super(context);
    }

    public MyListView(Context context, AttributeSet attrs) {
        super(context, attrs);
    }

    public MyListView(Context context, AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
    }

    @Override
    protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
        int newHeightMeasureSpec = MeasureSpec.makeMeasureSpec(480, // 固定高度（实际中这个值应该是根据手机屏幕计算出来的）
                MeasureSpec.AT_MOST);
        super.onMeasure(widthMeasureSpec, newHeightMeasureSpec);
    }

    @Override
    public boolean onInterceptTouchEvent(MotionEvent ev) {
        switch (ev.getAction()) {
            case MotionEvent.ACTION_DOWN:
            case MotionEvent.ACTION_MOVE:
                getParent().requestDisallowInterceptTouchEvent(true);
                break;
            case MotionEvent.ACTION_UP:
            case MotionEvent.ACTION_CANCEL:
                getParent().requestDisallowInterceptTouchEvent(false);
                break;
        }
        return super.onInterceptTouchEvent(ev);
    }
}
```
<h1 id="129">29. 内存泥潭</h1>
 
 [返回目录](#1) 
 [参考网站](http://www.jianshu.com/p/7a7db9f8692d)

在开发中，我们也可以给一些初级的工程师相关的建议，如：
>注意单例模式和静态变量是否会持有对Context的引用；
注意监听器的注销；（在Android程序里面存在很多需要register与unregister的监听器，我们需要确保在合适的时候及时unregister那些监听器。）
不要在Thread或AsyncTask中的引用Activity；

<h1 id="130">30. 老外的自定义View面试题</h1>
 
 [返回目录](#1) 
 [参考网站](http://www.jianshu.com/p/7a7db9f8692d)

>invalidate和postInvalidate方法的区别？
自定义View的绘制流程？
View的Touch事件分发流程？

<h1 id="134">34. 常去的Android相关站点</h1>
 
 [返回目录](#1) 
 [参考网站](http://www.jianshu.com/p/7a7db9f8692d)

CodeKK
注于开源分享、源码解析、框架设计、好文推荐、Android内推，不知道要用什么框架时，看看CodeKK说不定会有意想不到的收获。
网址：http://p.codekk.com/

android-arsenal
从 2014 年开始做，囊括库最多的网站了，支持英文搜索、分类选择、显示最新开源项目。
网址：https://android-arsenal.com/

Android平台源码查看
androidxref：基于OpenGrok构建，可以快带检索Android源码的网站，通过方法名或者日志检索网站的速度非常快。
网址：http://androidxref.com/
grepcode：可快速搜索 Android、Java任何版本及部分开源项目源码，看各版本系统代码排查问题相当方便。
网址：http://www.grepcode.com/

大牛的网站

Jakewharton
网址：http://jakewharton.com/
Github：https://github.com/JakeWharton
所在公司：Square Open Source
网址：http://square.github.io/


<h1 id="136">36. AIDL</h1>
 
 [返回目录](#1) 

让服务在其他进程中运行
```
<service
            android:name=".RemoteService"
            android:process=":remote"
            android:enabled="true"
            android:exported="true"/>
```
<h1 id="0201">面试要求</h1>
 
 [返回目录](#2) 

# 阿里公司
Android(带薪年假)(20000-40000)
北京-朝阳区学历本科经验3-5年招聘若干来源：看准网

职位描述
职位类型：Android
发布时间：2017-08-19
有效日期：2017-09-23
负责阿里云Android客户端开发； 参与架构设计和讨论； 负责客户端的编码和模块设计； 维护现有的客户端代码，完成新版本发布； ,Boss 陈杰 15k-30k 诚聘

#公司介绍
阿里巴巴（中国）有限公司
公司性质：私企
公司规模：10000人以上
公司类型：计软/通信/互联网/电子
工作地点：北京市朝阳区望京 [查看地图]

Android高级工程师(移动互联网)(17000-34000)
北京-学历本科经验3-5年招聘若干来源：看准网

职位描述
职位类型：Android
发布时间：2017-08-19
有效日期：2017-09-23
&amp;quot;岗位职责： 1.参与众包项目移动app的需求评审 2.与产品、UI以及后端接口人员配合完成客户端功能的开发和优化 3.跟进android客户端的测试、Bug处理以及用户反馈 4.负责移动客户端的打包、上线等验收测试 岗位要求: 1.计算机相关专业本科以上学历，2年以上的android开发经验 2.熟悉android界面布局及常用控件的二次开发 3.熟悉Android下网络通信机制,有过实际的http协议应用开发经验 4.扎实的java语言和数据结构基础，熟练使用Android SDK及相关开发工具 5.有android app开发经验、各种机型和操作系统的适配经验优先 6.有过应用crash处理以及monkey自动化测试经验者优先考虑 &amp;quot; ,Boss Lenka 17k-34k 诚聘