门店详情
本电脑笔记地址
D:\TanYinQingJavaEEStudy\ShiShiXiangMu\ProjectSummary\bootstrap\storeLinYou
[原型图](https://modao.cc/app/eDQBhJichJPsGO8016yJa6UlqURBdys#screen=s0C2E4B00611494208831827)
桌面上出现多个入口的原因是，引入的多个aar中，清单文件有重复或重名的地方。

做界面的时候，要建立盒子的概念，不断的划分盒子。

```
 android:gravity="center_vertical" 让子元素在父类中位置居中。
 让子元素靠左，并且相对布局方便控制位置。
 android:layout_marginRight="20dp" 右外边距
android:layout_alignParentRight="true" 相对布局居中
android:layout_centerInParent="true"  相对布局居中
```
首页是只带主导器
订单管理是带了主导器和适配器

做的顺序就是，先搭框架，在写界面。写界面时先做一个草图，在逐渐细化和美化。

