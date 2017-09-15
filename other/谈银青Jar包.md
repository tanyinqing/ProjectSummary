 # 2017 06 09
> # [文档地址](http://pan.baidu.com/disk/home?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&#list/vmode=list&path=%2F%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6%E5%A4%B9%2F%E5%AE%89%E5%8D%93%E9%A1%B9%E7%9B%AE%E4%BB%A3%E7%A0%81%E4%BB%93%E5%BA%93%2FMarkDown%E5%BC%80%E5%8F%91%E6%96%87%E6%A1%A3 "查看")
> # [源文件相关](http://pan.baidu.com/disk/home?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&#list/vmode=list&path=%2F%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6%E5%A4%B9%2F%E9%A1%B9%E7%9B%AE%E6%A8%A1%E5%9D%97%2FAndBaseDemo%E6%A1%86%E6%9E%B6 "查看")

<h1 id="0">目录列表</h1> 

##  <h1 id="01">1. 简介</h1> 
> ## 1. 简介
>> ## [说明](#0101)
>> ## [如何创建](#0102)


# 参考文档
> # [订单](5%9D%97 "查看")



# 1. 简介  

> ## <h1 id="0101">说明</h1>

> ## [返回目录](#01)

源代码的名字叫 TanYinQingJar  这个文件的目的就是一些没有资源的源代码，记住包里不加入依赖，都是源代码，不和别的项目绑定。

> ## <h1 id="0102">如何创建</h1>

> ## [返回目录](#01)

```
建立子模块时一定要选中Android Library

但是必须apk要加入对module的依赖才可以生成jar

在android studio 提供的Terminal中（目录默认伟当前工程的）键入 gradlew makeJar 回车看到如下所示就OK了


//Copy类型  这个的子module中配置
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