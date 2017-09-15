<h1 id="1"></h1>  
门店→[门店详情](#0101)→[门店接口](#0102)

仓库→[仓库详情](#0201)→[仓库接口](#0202)

<h1 id="0101">门店详情</h1>
 
 [返回目录](#1) 

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

<h1 id="0102">门店接口</h1>
 
 [返回目录](#1) 


## 门店端接口文档



> 注：每个接口请求数据皆需要在header头添加token值进行请求。具体token由登录成功后返回决定，注册登录相关接口无须添加token。请求接口皆遵循```RESTFUL```标准进行数据请求。请求地址：http://stores.api.umijoy.com/
>
> 返回数据格式：请求返回格式为标准JSON格式。
>
> 成功时返回：```{success:true,data:{},errors:null}```；其中data主要用于存放返回结果，data格式可能为JSON格式或者为数组JSON。
>
> 失败返回格式：```{success:false,data:null,errors:{code:404,message:'请求签名错误'}}```；errors主要为错误信息：其中code为错误码，message为错误信息。
>
> 接下来 文档所作返回值，默认只对成功时data数据作解释。
>
> 系统采用权限代码进行权限控制，前端应只显示当前登录用户所拥有的权限模块。具体权限模块权限代码：
>
> ```perl
> 订单管理      code: order
> 商品模块      code: goods
> 采购模块      code: proch
> 收货模块      code: rece
> 人员管理      code: staff
> 提现模块      code: withdraw
> 统计模块      code: statis
> ```
>
> 参数：必须参数在说明内标明“必须”，未标注则是可选参数



### 1、订单管理  （order）



##### 1）、订单列表

请求地址：order/lists

请求方式：get

请求参数：

| 参数名      | 数据类型   | 是否必须 | 说明                                |
| -------- | ------ | ---- | --------------------------------- |
| start    | int    | 否    | 当前偏移量，默认为：0。eg：若要从第200条数据开始则为200. |
| page_num | int    | 否    | 每页显示数量，默认为：10                     |
| order_sn | string | 否    | 订单编号查询                            |

返回值 （json）：

| 参数名   | 数据类型        | 说明      |
| :---- | :---------- | :------ |
| total | int         | 总条数     |
| data  | array\|json | 具体订单数据。 |

data数据 （array）：

| 参数名        | 数据类型        | 说明     |
| :--------- | ----------- | ------ |
| order_id   | int         | 订单ID   |
| buyer      | String      | 下单用户   |
| time       | String      | 下单时间   |
| amount     | float       | 订单价格   |
| status     | string      | 订单状态   |
| address    | string      | 收货地址   |
| phone      | string      | 收货电话   |
| note       | string      | 客户备注   |
| goods_data | array\|json | 订单商品信息 |

data.goods_data 数据 （array）

| 参数名        | 数据类型   | 说明   |
| ---------- | ------ | ---- |
| goods_name | string | 商品名称 |
| num        | int    | 商品数量 |
| price      | Float  | 单价   |
| amount     | Float  | 商品总价 |
| unit       | string | 单位   |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": {
        "total": 2,
        "data": [
            {
                "order_id": 1,
                "order_sn": "dfadgsdf34234",
                "buyer": "Tom",
                "time": "2017-07-25 11:02:11",
                "amount": 188,
                "status": "pay",
                "status_text": "待发货",
                "address": "天鹅湖花园",
                "phone": "18080092233",
                "note": "无",
                "goods_data": [
                    {
                        "goods_name": "",
                        "num": 5,
                        "price": 12,
                        "amount": 60,
                        "unit": "瓶"
                    },
                    {
                        "goods_name": "",
                        "num": 8,
                        "price": 15,
                        "amount": 120,
                        "unit": "瓶"
                    }
                ]
            },
            {
                "order_id": 2,
                "order_sn": "345678989878",
                "buyer": "Tom",
                "time": "2017-08-01 14:00:44",
                "amount": 188,
                "status": "pay",
                "status_text": "待发货",
                "address": "天鹅湖花园",
                "phone": "18080092233",
                "note": "无",
                "goods_data": [
                    {
                        "goods_name": "",
                        "num": 8,
                        "price": 15,
                        "amount": 120,
                        "unit": "瓶"
                    }
                ]
            }
        ]
    }
}
```



##### 2）、订单详情

请求地址：order/info

请求方式：get

请求参数：

| 参数名      | 数据类型 | 是否必须 | 说明   |
| -------- | ---- | ---- | ---- |
| order_id | int  | 是    | 订单ID |

返回值 （json）：

| 参数名             | 数据类型        | 说明                                  |
| :-------------- | ----------- | ----------------------------------- |
| order_id        | int         | 订单ID                                |
| buyer           | String      | 下单用户                                |
| time            | String      | 下单时间                                |
| amount          | String      | 订单价格                                |
| status          | string      | 订单状态                                |
| address         | string      | 收货地址                                |
| note            | string      | 客户备注                                |
| goods_data      | array\|json | 订单商品信息                              |
| phone           | string      | 收货电话                                |
| delivery_person | string      | 配送人员                                |
| delivery_phone  | string      | 配送人员电话                              |
| delivery_type   | string      | 配送方式 `deliver = 门店配送上门 since =  自提` |

data.goods_data 数据 （array）

| 参数名        | 数据类型   | 说明   |
| ---------- | ------ | ---- |
| goods_name | string | 商品名称 |
| num        | int    | 商品数量 |
| price      | Float  | 单价   |
| amount     | Float  | 商品总价 |
| unit       | string | 单位   |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": {
        "order_id": 1,
        "order_sn": "dfadgsdf34234",
        "buyer": "Tom",
        "time": "2017-07-25 11:02:11",
        "amount": 188,
        "status": "pay",
        "status_text": "待发货",
        "address": "天鹅湖花园",
        "phone": "18080092233",
        "note": "无",
        "delivery_person": "周红",
        "delivery_phone": "18080092211",
        "delivery_type": "deliver",
        "goods_data": [
            {
                "goods_name": "农夫山泉第一世",
                "num": 5,
                "price": 12,
                "amount": 60,
                "unit": "瓶"
            },
            {
                "goods_name": "农夫山泉第二世",
                "num": 8,
                "price": 15,
                "amount": 120,
                "unit": "瓶"
            }
        ]
    }
}
```





##### 3）、订单发货

请求地址：order/shipments

请求方式：patch

请求参数：

| 参数名      | 数据类型   | 是否必须 | 说明    |
| -------- | ------ | ---- | ----- |
| order_id | int    | 是    | 订单ID  |
| name     | string | 是    | 送货人姓名 |
| phone    | string | 是    | 送货人电话 |

返回值：无

```json
{
    "success": true,
    "errors": [],
    "data": []
}
```





##### 4）、取消订单

请求地址：order/cacel

请求方式：patch

请求参数：

| 参数名      | 数据类型 | 是否必须 | 说明   |
| -------- | ---- | ---- | ---- |
| order_id | int  | 是    | 订单ID |

返回值：无

```json
{
    "success": true,
    "errors": [],
    "data": []
}
```



##### 5）、完成订单

请求地址：order/complate

请求方式：patch

请求参数：

| 参数名      | 数据类型 | 说明   |
| -------- | ---- | ---- |
| order_id | int  | 订单ID |

返回值：无

```json
{
    "success": true,
    "errors": [],
    "data": []
}
```





### 2、商品模块  （goods）



##### 1）、商品列表

请求地址：goods/lists

请求方式：get

请求参数：

| 参数名      | 数据类型   | 说明                                |
| -------- | ------ | --------------------------------- |
| start    | int    | 当前偏移量，默认为：0。eg：若要从第200条数据开始则为200. |
| page_num | int    | 每页显示数量，默认为：10                     |
| keywords | string | 关键字搜索                             |



返回数据：（json）

| 参数名   | 数据类型        | 说明      |
| :---- | :---------- | :------ |
| total | int         | 总条数     |
| data  | array\|json | 具体商品数据。 |

data数据：（array）

| 参数名        | 数据类型   | 说明               |
| ---------- | ------ | ---------------- |
| goods_name | string | 商品名称             |
| goods_img  | string | 商品图片             |
| price      | string | 单价               |
| repertory  | string | 库存；包含单位 eg：15件2瓶 |
| sell_num   | string | 已售数量；包含单位        |
| goods_id   | int    | 商品ID             |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": {
        "total": 2,
        "data": [
            {
                "goods_id": 1,
                "goods_name": "农夫山泉矿泉水 水蜜桃 + 500ml",
                "goods_img": "https://umijoy.s3.cn-north-1.amazonaws.com.cn/umijoy-5cf65d9fed1b7e255b1be1c25da0e1b9.jpg",
                "price": "12.00",
                "repertory": "5箱1件8瓶",
                "sell_num": "5瓶"
            },
            {
                "goods_id": 2,
                "goods_name": "农夫山泉矿泉水 荔枝 + 500ml",
                "goods_img": "https://umijoy.s3.cn-north-1.amazonaws.com.cn/umijoy-d58d1467874ae93d40857c3187668f49.png",
                "price": "15.00",
                "repertory": "8箱1件",
                "sell_num": "8瓶"
            }
        ]
    }
}
```



##### 2）、商品详情

请求地址：goods/info

请求方式：get

请求参数：

| 参数       | 数据类型 | 说明        |
| -------- | ---- | --------- |
| goods_id | int  | 必须。具体商品ID |

返回数据：（json）

| 参数名        | 数据类型   | 说明               |
| ---------- | ------ | ---------------- |
| goods_name | string | 商品名称             |
| goods_img  | array  | 商品图片集合           |
| price      | string | 单价               |
| repertory  | string | 库存；包含单位 eg：15件2瓶 |
| sell_num   | string | 已售数量；包含单位        |
| content    | string | 商品图文介绍           |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": {
        "goods_name": "农夫山泉矿泉水 水蜜桃 + 500ml",
        "goods_img": "https://umijoy.s3.cn-north-1.amazonaws.com.cn/umijoy-5cf65d9fed1b7e255b1be1c25da0e1b9.jpg",
        "price": "1.50",
        "content": "hfhdsfsdfd",
        "repertory": "11箱4瓶",
        "sell_num": "5瓶",
        "goods_id": "1"
    }
}
```



##### 3）、更改商品库存

请求地址：goods/repertory

请求方式：patch

请求参数：

| 参数名    | 数据类型 | 说明          |
| ------ | ---- | ----------- |
| sku_id | int  | 必须。具体SKU ID |
| rep    | int  | 必须。库存量      |

返回值：

```json
{
    "success": true,
    "errors": [],
    "data": []
}
```





##### 4）、更改商品售价

请求地址：goods/pri

请求方式：patch

请求参数：

| 参数名    | 数据类型  | 说明          |
| ------ | ----- | ----------- |
| sku_id | int   | 必须。具体SKU ID |
| price  | float | 必须。商品售价     |

返回值：

```json
{
    "success": true,
    "errors": [],
    "data": []
}
```





### 3、采购申请  （proch）



##### 1）、采购申请界面商品数据

请求地址：proch/goods

请求方式：get

请求参数：无

返回值：（array）

| 参数名        | 数据类型        | 说明                   |
| ---------- | ----------- | -------------------- |
| sku_id     | int         | 具体SKU ID             |
| goods_name | string      | 商品具体名称               |
| price      | float       | 单价                   |
| unit       | array\|json | 商品所包含单位信息。第一个单位为默认单位 |

data.unit数据：（array）

| 参数名     | 数据类型   | 说明             |
| ------- | ------ | -------------- |
| unit_id | int    | 单位ID           |
| name    | string | 单位名称           |
| factor  | int    | 单位转换因子，每个单位换算比 |
| default | int    | 是否默认单位 1是 0 否  |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": [
        {
            "sku_id": 4,
            "goods_name": "乐事薯片 烧烤 + 500g",
            "price": "5.00",
            "unit": [
                {
                    "unit_id": 1,
                    "name": "包",
                    "factor": 1,
                    "default": "1"
                }
            ]
        },
        {
            "sku_id": 7,
            "goods_name": "乐事薯片 椒盐 + 500g",
            "price": "52.00",
            "unit": [
                {
                    "unit_id": 42,
                    "name": "包",
                    "factor": 1,
                    "default": "1"
                },
                {
                    "unit_id": 43,
                    "name": "箱",
                    "factor": 20,
                    "default": "0"
                }
            ]
        }
    ]
}
```





##### 2）、添加采购商品（搜索商品）

请求地址：proch/searchgoods

请求方式：get

请求参数：

| 参数名     | 数据类型   | 说明     |
| ------- | ------ | ------ |
| keyword | string | 必须。关键词 |

返回值：（array）

| 参数名        | 数据类型        | 说明                   |
| ---------- | ----------- | -------------------- |
| sku_id     | int         | 具体SKU ID             |
| goods_name | string      | 商品具体名称               |
| price      | float       | 单价                   |
| unit       | array\|json | 商品所包含单位信息。第一个单位为默认单位 |

data.unit数据：（array）

| 参数名     | 数据类型   | 说明             |
| ------- | ------ | -------------- |
| unit_id | int    | 单位ID           |
| name    | string | 单位名称           |
| factor  | int    | 单位转换因子，每个单位换算比 |
| default | int    | 是否默认单位 1是 0 否  |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": [
        {
            "sku_id": 3,
            "goods_name": "乐事薯片 椒盐 + 500g",
            "price": "5.00",
            "unit": [
                {
                    "unit_id": 1,
                    "name": "包",
                    "factor": 1,
                    "default": "1"
                }
            ]
        },
        {
            "sku_id": 4,
            "goods_name": "乐事薯片 烧烤 + 500g",
            "price": "5.00",
            "unit": [
                {
                    "unit_id": 1,
                    "name": "包",
                    "factor": 1,
                    "default": "1"
                }
            ]
        },
        {
            "sku_id": 7,
            "goods_name": "乐事薯片 椒盐 + 500g",
            "price": "52.00",
            "unit": [
                {
                    "unit_id": 42,
                    "name": "包",
                    "factor": 1,
                    "default": "1"
                },
                {
                    "unit_id": 43,
                    "name": "箱",
                    "factor": 20,
                    "default": "0"
                }
            ]
        },
        {
            "sku_id": 8,
            "goods_name": "乐事薯片 烧烤 + 500g",
            "price": "2.00",
            "unit": [
                {
                    "unit_id": 42,
                    "name": "包",
                    "factor": 1,
                    "default": "1"
                },
                {
                    "unit_id": 43,
                    "name": "箱",
                    "factor": 20,
                    "default": "0"
                }
            ]
        }
    ]
}
```



##### 3）、发起采购申请

请求地址：proch/apply

请求方式：post

请求参数：

| 参数名   | 数据类型        | 是否必须 | 说明        |
| ----- | ----------- | ---- | --------- |
| goods | array\|json | 是    | 必须。具体采购信息 |
| note  | string      | 否    | 其他采购      |

goods数据：

| 参数名    | 数据类型 | 是否必须 | 说明          |
| ------ | ---- | ---- | ----------- |
| sku_id | int  | 是    | 必须。具体sku ID |
| num    | int  | 是    | 必须。数量       |
| unit   | int  | 是    | 必须。单位ID     |

返回值：（json）

| 参数名     | 数据类型   | 说明   |
| ------- | ------ | ---- |
| prochsn | string | 采购单号 |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": {
        "prochsn": "CD201708022BBA2"
    }
}
```



##### 4）、采购申请列表

请求地址：porch/lists

请求方式：get

请求参数：

| 参数名      | 数据类型   | 是否必须 | 说明                                |
| -------- | ------ | ---- | --------------------------------- |
| start    | int    | 否    | 当前偏移量，默认为：0。eg：若要从第200条数据开始则为200. |
| page_num | int    | 否    | 每页显示数量，默认为：10                     |
| prochsn  | string | 否    | 采购单号搜索                            |



返回参数：（array）

| 参数名   | 数据类型        | 说明           |
| ----- | ----------- | ------------ |
| total | int         | 数量           |
| data  | array\|json | 具体数据，见data数据 |

data数据

| 参数名      | 数据类型   | 说明                                       |
| -------- | ------ | ---------------------------------------- |
| proch_id | int    | 具体采购单ID                                  |
| prochsn  | string | 采购单号                                     |
| status   | string | 该采购单状态 ```pending=待仓库确认； underway=仓库已确认、处理中； unaccepted=被仓库拒绝; deliverable=配送中; completed=已完成``` |
| note     | string | 备注                                       |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": {
        "total": 3,
        "data": [
            {
                "proch_id": 4,
                "seller_id": 2,
                "prochsn": "CD201708022BBA2",
                "amount": "536.00",
                "status": "pending",
                "pay_status": "pending",
                "note": "",
                "status_txt": "待仓库确认",
                "pay_text": "待支付"
            },
            {
                "proch_id": 3,
                "seller_id": 2,
                "prochsn": "CD201708029F6C2",
                "amount": "536.00",
                "status": "pending",
                "pay_status": "pending",
                "note": "",
                "status_txt": "待仓库确认",
                "pay_text": "待支付"
            },
            {
                "proch_id": 1,
                "seller_id": 2,
                "prochsn": "dfsdgfhgfjtyyt454",
                "amount": "23456.55",
                "status": "pending",
                "pay_status": "pending",
                "note": "hah",
                "status_txt": "待仓库确认",
                "pay_text": "待支付"
            }
        ]
    }
}
```



##### 5）、采购单详情

请求地址：proch/info

请求方式：get

请求参数：

| 参数名     | 数据类型   | 是否必须 | 说明      |
| ------- | ------ | ---- | ------- |
| prochsn | string | 是    | 必须。采购单号 |

返回数据：（json）

| 参数名        | 数据类型        | 说明              |
| ---------- | ----------- | --------------- |
| prochsn    | string      | 采购单号            |
| time       | datetime    | 采购              |
| pack       | array\|json | 已包装信息。见pack数据   |
| goods      | array\|json | 未包装的商品。见goods数据 |
| amount     | float       | 采购金额            |
| pay_status | string      | 采购支付状态          |
| pay_txt    | string      | 采购支付状态文字        |
| status     | string      | 采购订单            |
| status_txt | string      | 采购订单状态文字        |

pack数据：（array）

| 参数名        | 数据类型        | 说明      |
| ---------- | ----------- | ------- |
| packsn     | String      | 包装箱号    |
| goods_info | array\|json | 包装箱中的商品 |

pack.goods_info数据 ：（array）

| 参数名        | 数据类型   | 说明   |
| ---------- | ------ | ---- |
| goods_name | string | 商品名称 |
| num        | int    | 商品数量 |
| unit       | string | 商品单位 |

goods 数据：

| 参数名        | 数据类型   | 说明   |
| ---------- | ------ | ---- |
| goods_name | string | 商品名称 |
| num        | int    | 商品数量 |
| unit       | string | 商品单位 |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": {
        "prochsn": "CD201708022BBA2,CD201708023BBA2",
        "time": "2017-08-02 00:05:06",
        "amount": "536.00",
        "pay_text": "待支付",
        "pay_status": "pending",
        "status": "pending",
        "status_txt": "待支付",
        "pack": [
            {
                "packsn": "CDM124",
                "goods_info": [
                    {
                        "goods_name": "农夫山泉矿泉水 水蜜桃 + 500ml",
                        "num": 28,
                        "unit": "瓶"
                    }
                ]
            }
        ],
        "goods": [
            {
                "goods_name": "乐事薯片 烧烤 + 500g",
                "num": 12,
                "unit": "箱"
            }
        ]
    }
}
```



##### 6）、采购付款列表

请求地址：proch/paylists

请求方式：get

请求参数：

| 参数名      | 数据类型   | 是否必须 | 说明                                |
| -------- | ------ | ---- | --------------------------------- |
| start    | int    | 否    | 当前偏移量，默认为：0。eg：若要从第200条数据开始则为200. |
| page_num | int    | 否    | 每页显示数量，默认为：10                     |
| prochsn  | string | 否    | 采购单号搜索                            |

返回值：（array）

| 参数名      | 数据类型     | 说明    |
| -------- | -------- | ----- |
| prochsn  | string   | 采购单号  |
| amout    | float    | 付款金额  |
| proch_id | int      | 采购单   |
| lasttime | datetime | 最后付款日 |

返回示例:

```json
{
    "success": true,
    "errors": [],
    "data": {
        "total": 1,
        "data": [
            {
                "proch_id": 4,
                "seller_id": 2,
                "prochsn": "CD201708022BBA2",
                "amount": "536.00",
                "status": "pending",
                "pay_status": "pending",
                "note": "",
                "add_time": "2017-08-02 00:05:06",
                "status_txt": "待仓库确认",
                "pay_text": "待支付",
                "lasttime": "2017-08-17"
            }
        ]
    }
}
```



##### 7）、采购单付款动作

请求地址：porch/pay

请求地址：post

请求参数：

| 参数名       | 数据类型   | 是否必须 | 说明                          |
| --------- | ------ | ---- | --------------------------- |
| proch_ids | string | 是    | 必须。采购单合集，以英文半角“,”分割         |
| pay_type  | string | 是    | 支付方式：`wechat:微信，alipay：支付宝` |

返回值：（json）

| 参数名       | 数据类型   | 说明                                |
| --------- | ------ | --------------------------------- |
| amout     | float  | 付款金额 (元)                          |
| prepay_id | string | 支付平台支付编号（微信平台返回prepay_id,支付宝返回签名） |
| pay_sn    | string | 该支付单内部编号                          |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": {
        "amount": 24528.55,
        "prepay_id": "wx2017081017032017462ad8070803905653",
      	"pay_sn":"2017080709355221338561"
    }
}
```



##### 8）、查询微信付款状态

请求地址：porch/searchpay

请求方式：get

请求参数：

| 参数名    | 数据类型   | 是否必须 | 说明          |
| ------ | ------ | ---- | ----------- |
| pay_sn | string | 是    | 必须。该支付单内部编号 |

返回值：（json）

| 参数名              | 数据类型   | 说明   |
| ---------------- | ------ | ---- |
| paystatus   `*1` | string | 支付状态 |

`*1 paystatus `  支付状态：

SUCCESS—支付成功

REFUND—转入退款

NOTPAY—未支付

CLOSED—已关闭

REVOKED—已撤销（刷卡支付）

USERPAYING--用户支付中

PAYERROR--支付失败(其他原因，如银行返回失败) 



### 4、收货模块   （rece）



##### 1）、收货（扫码）

> 收货采取二维码扫描的模式进行。客户端需扫描箱体上的二维码。获取二维码当中的信息当中的打包编号进行请求

请求地址：rece/info

请求方式：get

请求参数：

| 参数名    | 数据类型   | 是否必须 | 说明            |
| ------ | ------ | ---- | ------------- |
| ercode | string | 是    | 必须。二维码扫描出来的编号 |

返回值：（array）

| 参数名     | 数据类型        | 说明                      |
| ------- | ----------- | ----------------------- |
| status  | string      | 当前采购单状态。` 0 未收货   1 收货` |
| boxdata | array\|json | 包装箱数据                   |

boxdata数据：

| 参数名     | 数据类型   | 说明           |
| ------- | ------ | ------------ |
| boxsn   | string | 货箱编号         |
| boximg  | string | 货箱           |
| prochsn | string | 采购单号         |
| status  | string | 0 未收货   1 收货 |

返回值：

```Json
{
    "success": true,
    "errors": [],
    "data": {
        "boxData": [
            {
                "boxsn": "CDM124",
                "boximg": "",
                "prochsn": "CD201708029F6C2",
                "status": 0
            },
            {
                "boxsn": "CDM125",
                "boximg": "",
                "prochsn": "CD201708029F6C2",
                "status": 0
            }
        ],
        "orderStatus": 0
    }
}
```



##### 2）、确认收货

请求地址：rece/comp

请求方式：patch

请求参数：

| 参数名    | 数据类型   | 说明            |
| ------ | ------ | ------------- |
| ercode | string | 必须。二维码扫描出来的编号 |

返回值：无

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": []
}
```



### 5、人员管理模块 （staff）



##### 1）、工作员工列表

请求地址：staff/lists

请求方式：get

请求参数：

| 参数名       | 数据类型   | 说明                                |
| --------- | ------ | --------------------------------- |
| start     | int    | 当前偏移量，默认为：0。eg：若要从第200条数据开始则为200. |
| page_num  | int    | 每页显示数量，默认为：10                     |
| keywords  | string | 工作人员姓名搜索                          |
| seller_id | int    | 必须。门店ID                           |

返回示例

```json
{
  "success": true,
  "errors": [],
  "data": {
    "total": 2,
    "data": [
      {
        "staff_id": 2,
        "name": "手动添加的店员",
        "phone": "13512398743",
        "registerTime": "2017-07-07 10:24:33"
      },
      {
        "staff_id": 3,
        "name": "zyytest2",
        "phone": "18280439265",
        "registerTime": "2017-07-22 14:33:23"
      }
    ]
  }
}
```



返回值：（array）

| 参数名   | 数据类型        | 说明             |
| ----- | ----------- | -------------- |
| total | int         | 数据总数           |
| data  | array\|json | 具体数据。详见：data数据 |

data数据

| 参数名      | 数据类型   | 说明   |
| -------- | ------ | ---- |
| staff_id | int    | 人员ID |
| name     | string | 用户名  |
| phone    | string | 电话   |



##### 2）、工作人员详情

请求地址：staff/info

请求方式：get

请求参数：

| 参数名      | 数据类型 | 说明        |
| -------- | ---- | --------- |
| staff_id | int  | 必须。工作人员ID |

返回示例

```Json
{
  "success": true,
  "errors": [],
  "data": {
    "name": "zyytest",
    "phone": "18280439265",
    "account": "zyytest",
    "auth": [
      {
        "auth_code": "order",
        "auth_name": "订单管理",
        "auth_has": false
      },
      {
        "auth_code": "goods",
        "auth_name": "商品模块",
        "auth_has": true
      },
      {
        "auth_code": "proch",
        "auth_name": "采购",
        "auth_has": true
      },
      {
        "auth_code": "rece",
        "auth_name": "收货",
        "auth_has": true
      },
      {
        "auth_code": "staff",
        "auth_name": "人员管理",
        "auth_has": false
      },
      {
        "auth_code": "withdraw",
        "auth_name": "提现",
        "auth_has": false
      },
      {
        "auth_code": "statis",
        "auth_name": "统计",
        "auth_has": true
      }
    ]
  }
}
```



返回值：（json）

| 参数名     | 数据类型        | 说明      |
| ------- | ----------- | ------- |
| name    | string      | 姓名      |
| phone   | string      | 电话      |
| account | string      | 该人员登录账号 |
| auth    | array\|json | 权限数据    |

auth数据：（array）

| 参数名       | 数据类型   | 说明             |
| --------- | ------ | -------------- |
| auth_code | string | 权限代码           |
| auth_name | string | 权限名称           |
| auth_has  | bool   | 是否拥有该权限，true 有 |



##### 3）、修改权限或添加工作人员

请求地址：staff/auth

请求方式：post

请求参数：

| 参数名     | 数据类型   | 说明                  |
| ------- | ------ | ------------------- |
| user_id | int    | 工作人员 ID             |
| auth    | string | 权限代码字符，用英文半角逗号“,”分割 |

返回值：无





##### 4）、人员搜索

> 搜索采用联想搜索

请求地址：staff/search

请求方式：get

请求参数：

| 参数名      | 数据类型   | 说明       |
| -------- | ------ | -------- |
| keywords | string | 必须。搜索关键字 |

返回示例

```json
{
  "success": true,
  "errors": [],
  "data": [
    {
      "staff_id": 3,
      "name": "zyytest2",
      "phone": "18280439265",
      "registerTime": "2017-07-22 14:33:23"
    }
  ]
}
```



返回值：（array）

| 参数名     | 数据类型   | 说明     |
| ------- | ------ | ------ |
| user_id | int    | 工作人员ID |
| name    | string | 姓名     |
| phone   | string | 电话     |



##### 5）、移除工作人员

请求地址：staff/delete

请求方式：delete

请求参数：

| 参数名     | 数据类型 | 说明        |
| ------- | ---- | --------- |
| user_id | int  | 必须。工作人员ID |

返回值：无。




### 6、提现  （withdraw）



##### 1）、提现页

请求地址：withdraw/index

请求方式：get

请求参数：

| 参数名      | 数据类型 | 说明                                    |
| -------- | ---- | ------------------------------------- |
| start    | int  | 提现数据当前偏移量，默认为：0。eg：若要从第200条数据开始则为200. |
| page_num | int  | 每页显示数量，默认为：10                         |

返回值：（array）

返回示例

```json
{
  "success": true,
  "errors": [],
  "data": {
    "payments": [
      {
        "time": "2017-07-20 07:22:34",
        "money": "3992.78",
        "payType": "支付宝",
        "status": "已完成"
      },
      {
        "time": "2017-07-22 08:07:01",
        "money": "2345.90",
        "payType": "支付宝",
        "status": "处理中"
      },
      {
        "time": "2017-08-01 05:36:07",
        "money": "2100.56",
        "payType": "支付宝",
        "status": "已拒绝"
      }
    ],
    "total": 3,
    "balance": "1684.00"
  }
}
```



返回值：（json）

| 参数名      | 数据类型        | 说明      |
| -------- | ----------- | ------- |
| balance  | float       | 可提现金额   |
| payments | array\|json | 提现数据    |
| total    | int         | 提现数据总条数 |

withdraw_log 数据：（array）

| 参数名     | 数据类型   | 说明   |
| ------- | ------ | ---- |
| time    | string | 日期   |
| money   | float  | 提现金额 |
| payType | string | 提现渠道 |
| status  | string | 提现状态 |

##### 2）、提交提现申请

请求地址：withdraw/create

请求方式：post

请求参数

| 参数           | 是否必选 | 说明                                       | 类型     |
| ------------ | ---- | ---------------------------------------- | ------ |
| paymentType  | 是    | 提现渠道（ wechat，alipay，unionpay，online，offline） wechat=微信支付 alipay=支付宝 unionpay=银联支付 online=线上支付 offline=线下支付 | string |
| paymentMoney | 是    | 提现金额                                     | float  |
| payee        | 是    | 收款人账号                                    | string |
| note         | 是    | 提现说明                                     | string |



返回数据

```Json
{
  "success": true,
  "errors": [],
  "data": {
    "id": 6
  }
}
```

返回说明

| 参数   | 类型   | 说明    |
| ---- | ---- | ----- |
| id   | int  | 结算单ID |

### 7、统计（statis）——暂无



### 8、注册登录相关



##### 1）、登录

请求地址：account/login

请求方式：post

请求参数：

| 参数名      | 数据类型   | 说明          |
| -------- | ------ | ----------- |
| account  | string | 必须。用户名或手机号码 |
| password | string | 必须。密码       |

返回值：（json）

| 参数名   | 数据类型        | 说明                                   |
| ----- | ----------- | ------------------------------------ |
| token | string      | 登录成功后token                           |
| name  | string      | 当前用户名                                |
| store | array\|json | 门店信息，若是具有多个门店进入门店选择界面，若只有一个门店则直接进入主页 |

store 数据：（array）

| 参数名        | 数据类型   | 说明                           |
| ---------- | ------ | ---------------------------- |
| store_id   | int    | 门店ID                         |
| store_name | string | 门店名称                         |
| auth       | String | 所拥有权限代码。eg：order,goods,porch |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": {
        "token": "A6NIEMYD7FEG2IE378E5AABCD1112AA4C744080D170731",
        "name": "张三",
        "store": [
            {
                "store_id": 2,
                "auth": "order,goods,proch,rece,staff,withdraw,statis",
                "store_name": "龙湖店"
            }
        ]
    }
}
```



##### 2）、门店选择

请求地址：account/chstore

请求方式：patch

请求参数：

| 参数名      | 数据类型 | 说明   |
| -------- | ---- | ---- |
| store_id | int  | 门店   |

返回值：

| 参数名  | 数据类型   | 说明               |
| ---- | ------ | ---------------- |
| auth | string | 当前门店所拥有权限,用“,”隔开 |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": {
        "auth": "order,goods,proch,rece,staff,withdraw,statis"
    }
}
```



##### 3）、注册

请求地址：account/register

请求方式：post

请求参数：

| 参数名      | 数据类型   | 说明       |
| -------- | ------ | -------- |
| account  | string | 必须。账号    |
| password | string | 必须。密码    |
| sure_pwd | string | 必须。确认密码  |
| phone    | string | 必须。手机号码  |
| yzm      | string | 必须。手机验证码 |

返回值：

```json
{
    "success": true,
    "errors": [],
    "data": []
}
```





##### 4）、账号是否存在验证

请求地址：account/yzacc

请求方式：get

请求参数：

| 参数名     | 数据类型   | 说明      |
| ------- | ------ | ------- |
| account | string | 必须。验证账号 |

返回值：（json）

| 参数名    | 数据类型 | 说明               |
| ------ | ---- | ---------------- |
| status | bool | TRUE 已存在，false 否 |

返回示例：

```
{
    "success": true,
    "errors": [],
    "data": [
      "status":true
    ]
}
```





##### 5）、验证手机号是否存在

请求地址：account/yztel

请求方式：get

请求参数：

| 参数名   | 数据类型   | 说明       |
| ----- | ------ | -------- |
| phone | string | 必须。验证手机号 |

返回值：（json）

| 参数名    | 数据类型 | 说明               |
| ------ | ---- | ---------------- |
| status | bool | TRUE 已存在，false 否 |

返回示例：

```
{
    "success": true,
    "errors": [],
    "data": [
      "status":true
    ]
}
```



##### 6）、忘记密码（重置密码）

请求地址：account/resetpwd

请求方式：patch

请求参数：

| 参数名      | 数据类型   | 说明    |
| -------- | ------ | ----- |
| phone    | string | 手机    |
| yzm      | string | 手机验证码 |
| password | string | 新密码   |
| sure_pwd | string | 确认密码  |

返回值：

```json
{
    "success": true,
    "errors": [],
    "data": []
}
```





##### 7）、发送手机验证码

请求地址：account/yzm

请求方式：get

请求参数：

| 参数名   | 数据类型   | 说明   |
| ----- | ------ | ---- |
| phone | string | 手机号码 |

返回值：

```json
{
    "success": true,
    "errors": [],
    "data": []
}
```
<h1 id="0201">仓库详情</h1>
 
 [返回目录](#1) 


<h1 id="0202">仓库接口</h1>
 
 [返回目录](#1) 

## 仓库端接口文档

> 注：每个接口请求数据皆需要在header头添加token值进行请求。具体token由登录成功后返回决定，注册登录相关接口无须添加token。请求接口皆遵循```RESTFUL```标准进行数据请求。请求地址：http://rep.api.umijoy.com/
>
> 返回数据格式：请求返回格式为标准JSON格式。
>
> 成功时返回：```{success:true,data:{},errors:null}```；其中data主要用于存放返回结果，data格式可能为JSON格式或者为数组JSON。
>
> 失败返回格式：```{success:false,data:null,errors:{code:404,message:'请求签名错误'}}```；errors主要为错误信息：其中code为错误码，message为错误信息。
>
> 接下来 文档所作返回值，默认只对成功时data数据作解释。





### 1、仓库管理员

#####  1）登录

请求URI：user/login

请求方式：post

请求参数

| 参数       | 类型     | 说明              | 是否必选 |
| -------- | ------ | --------------- | ---- |
| name     | string | 登录关键字（用户名或手机号码） | 是    |
| password | string | 登录密码            | 是    |

 返回示例

```json
{
    "success": true,
    "errors": [],
    "data": {
        "uid": 5,
        "uname": "CangKuUser01",
        "token": "A6NBIYM4BA25GI3D10E5F703DA335D781AE1D0B7170822"
    }
}
```

返回参数

| 参数    | 类型     | 说明               |
| ----- | ------ | ---------------- |
| uid   | int    | 用户ID             |
| uname | string | 用户姓名             |
| token | string | 用户登录token，有效期为7天 |

##### 2）修改密码

请求地址：user/updatepwd

请求方式：patch

请求参数

| 参数      | 类型     | 是否必须 | 说明   |
| ------- | ------ | ---- | ---- |
| pwd     | string | 是    | 原密码  |
| new_pwd | string | 是    | 新密码  |

无返回值。

##### 3）退出登录

请求地址：user/logout

请求参数：无

返回值：无

### 2、采购模块

##### 1）、采购申请


请求地址：proch/lists

请求方式：get

请求参数：

| 参数           | 是否必选 | 类型     | 说明                                       |
| ------------ | ---- | ------ | ---------------------------------------- |
| proch_status | 否    | string | 采购单状态。```pending=待仓库确认； underway=仓库已确认、处理中； unaccepted=被仓库拒绝; deliverable=配送中; completed=已完成``` |
| start        | 否    | int    | 起始条数                                     |
| page_num     | 否    | int    | 所需条数                                     |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": {
        "list": [
            {
                "prochsn": "DN0284997631",
                "store": "成都市 高新区 新会展中心南门",
                "proch_status": "pending",
                "seller": "会展店",
                "status_name": "待仓库确认",
                "stock": false
            },
            {
                "prochsn": "DN02781465531",
                "store": "成都市 高新区 新会展中心南门",
                "proch_status": "unaccepted",
                "seller": "会展店02",
                "status_name": "被仓库拒绝",
                "stock": true
            },
            {
                "prochsn": "CD201708148B7214",
                "store": "成都市 高新区 新会展中心南门",
                "proch_status": "pending",
                "seller": "唐大门店",
                "status_name": "待仓库确认",
                "stock": false
            }
        ],
        "total": 4
    }
}
```





| 参数名          | 数据类型   | 说明                                       |
| ------------ | ------ | ---------------------------------------- |
| prochsn      | string | 采购单号                                     |
| store        | string | 门店地址                                     |
| proch_status | string | 采购单状态。```pending=待仓库确认； underway=仓库已确认、处理中； unaccepted=被仓库拒绝; deliverable=配送中; completed=已完成``` |
| stock        | bool   | 是否包含库存不足的商品。true 充足，false：不充足            |
| seller       | string | 门店名称                                     |
| status_name  | string | 采购单状态说明（同proch_status）                   |



##### 2）、采购明细

请求地址：porch/info

请求方式：get

请求参数：

| 参数名     | 数据类型   | 说明        |
| ------- | ------ | --------- |
| prochsn | string | 必须。采购申请单号 |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": {
        "prochsn": "CD201708148B7214",
        "proch_time": "2017-08-14 09:25:24",
        "proch_person_name": "zyytest",
        "proch_person_phone": "18280439265",
        "goods": [
            {
                "goods_name": "农夫山泉 白色 + 300ml",
                "num": 120,
                "unit": "瓶",
                "stock": false
            }
        ],
        "remark": ""
    }
}
```



返回值 json：

| 参数名                | 数据类型        | 说明     |
| ------------------ | ----------- | ------ |
| prochsn            | string      | 采购单号   |
| proch_time         | datetime    | 采购申请日期 |
| proch_person_name  | string      | 采购申请人  |
| goods              | array\|json | 采购商品信息 |
| remark             | string      | 其他采购需求 |
| proch_person_phone | string      | 采购申请电话 |

goods数据 （array）：

| 参数名        | 数据类型   | 说明                       |
| ---------- | ------ | ------------------------ |
| goods_name | string | 商品名                      |
| num        | int    | 采购数量                     |
| unit       | string | 单位                       |
| stock      | bool   | 库存是否充足。true 充足，false：不充足 |



##### 3）、通过采购申请

请求地址：proch/passed

请求方式：patch

请求参数：

| 参数名     | 数据类型   | 说明        |
| ------- | ------ | --------- |
| prochsn | string | 必须。采购申请单号 |

返回值：无





##### 4）、拒绝采购申请

请求地址：proch/reject

请求方式：patch

请求参数：

| 参数名     | 数据类型   | 说明        |
| ------- | ------ | --------- |
| prochsn | string | 必须。采购申请单号 |
| note    | string | 拒绝原因      |

返回值：无。



##### 5）、采购汇总

请求地址：proch/all

请求方式：get

请求参数：

| 参数       | 类型   | 是否必选 | 说明   |
| -------- | ---- | ---- | ---- |
| start    | int  | 否    | 起始条数 |
| page_num | int  | 否    | 所需条数 |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": {
        "list": [
            {
                "goods_name": "农夫山泉 白色 + 300ml",
                "sku_id": 11,
                "num": 19,
                "unit": "箱",
                "unit_id": 3
            }
        ],
        "total": 1
    }
}
```





返回值 （array）：

| 参数名        | 数据类型   | 说明       |
| ---------- | ------ | -------- |
| goods_name | string | 商品名称     |
| sku_id     | int    | 商品具体     |
| num        | int    | 建议采购数量   |
| unit       | string | 建议采购单位   |
| unit_id    | int    | 建议采购单位ID |



##### 6）、开始采购

请求地址：proch/start

请求方式：post

请求参数：

| 参数   | 类型    | 是否必选 | 说明    |
| ---- | ----- | ---- | ----- |
| sku  | array | 是    | sku信息 |

sku参数说明：

```请求数据以array方式请求数据。每一个array包含以下数据```

| 参数名     | 数据类型 | 说明            |
| ------- | ---- | ------------- |
| sku_id  | int  | 必须。商品具体SKU ID |
| num     | int  | 必须。采购数量       |
| unit_id | int  | 必须。商品单位ID     |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": {
        "purchase_sn": "A4818278948304"
    }
}
```



返回值 （json）：

| 参数名         | 数据类型   | 说明        |
| ----------- | ------ | --------- |
| purchase_sn | string | 进行中的对外采购号 |



##### 7）、进行中的采购列表

请求地址：purchase/lists

请求方式：get

请求参数：无

```json
{
    "success": true,
    "errors": [],
    "data": [
        {
            "id": 20,
            "purchase_sn": "A4818155332945",
            "created_at": "2017-08-18 07:32:33"
        },
        {
            "id": 21,
            "purchase_sn": "A4818278948304",
            "created_at": "2017-08-18 07:53:09"
        }
    ]
}
```



返回值 （array）：

| 参数名         | 数据类型   | 说明       |
| ----------- | ------ | -------- |
| id          | int    | 采购       |
| purchase_sn | string | 进行中的采购编号 |
| created_at  | string | 采购发起时间   |





##### 8）、进行中的采购详情

请求地址：purchase/info

请求方式：get

请求参数：

| 参数名         | 数据类型   | 说明          |
| ----------- | ------ | ----------- |
| purchase_sn | string | 必须。进行中的采购单号 |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": [
        {
            "goods_name": "哇哈哈 规格",
            "sku_id": 17,
            "num": 10,
            "unit": "件2",
            "unit_id": 12
        },
        {
            "goods_name": "特仑苏有机牛奶 250ml + 原味",
            "sku_id": 27,
            "num": 20,
            "unit": "件",
            "unit_id": 18
        }
    ]
}
```





返回值 （json）：

| 参数名        | 数据类型   | 说明       |
| ---------- | ------ | -------- |
| goods_name | string | 商品名称     |
| sku_id     | int    | 商品具体     |
| num        | int    | 建议采购数量   |
| unit       | string | 建议采购单位   |
| unit_id    | int    | 建议采购单位ID |





##### 9）、结束采购单

请求地址：purchase/stop

请求方式：patch

请求参数：

| 参数名         | 数据类型   | 说明          |
| ----------- | ------ | ----------- |
| purchase_sn | string | 必须。进行中的采购单号 |
| sku         | array  | 必须。商品SKU    |

sku参数说明：

```请求数据以array方式请求数据。每一个array包含以下数据```

| 参数名     | 数据类型 | 说明            |
| ------- | ---- | ------------- |
| sku_id  | int  | 必须。商品具体SKU ID |
| num     | int  | 必须。采购数量       |
| unit_id | int  | 必须。商品单位ID     |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": [
        {
            "goodName": "特仑苏有机牛奶 250ml + 原味",
            "addNum": 120,
            "addLocation": "库位03"
        }
    ]
}
```



返回data说明：`返回的data为结束采购入库时，商品存在不同库存位置的数据，系统处理不同位置时默认是将商品存放在库存量最小的位置`

data参数说明：

| 参数          | 类型     | 说明   |
| ----------- | ------ | ---- |
| goodName    | string | 商品名称 |
| addNum      | string | 添加数量 |
| addLocation | string | 添加库位 |

##### 10）、搜索商品

请求地址：proch/search

请求方式：get

请求参数

| 参数   | 类型     | 是否必须 | 说明    |
| ---- | ------ | ---- | ----- |
| name | string | 是    | 商品关键字 |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": [
        {
            "sku_id": 11,
            "name": "农夫山泉 白色 + 300ml",
            "unit": "箱",
            "unit_id": 3
        }
    ]
}
```

返回值说明

| 参数      | 类型     | 说明     |
| ------- | ------ | ------ |
| sku_id  | int    | 具体sku  |
| name    | string | 商品名称   |
| unit    | string | 采购单位   |
| unit_id | int    | 采购单位id |

##### 

### 3、发货模块

##### 1）、待发货清单

请求地址：shipment/lists

请求方式：get

请求参数：

| 参数       | 是否必选 | 类型   | 说明   |
| -------- | ---- | ---- | ---- |
| start    | 否    | int  | 起始条数 |
| page_num | 否    | int  | 所需条数 |

返回示例：

{

```
"success": "true",
"errors": [],
"data": {
    "list": [
        {
            "prochsn": "CD20170818367714",
            "store": "新会展中心南门",
            "proch_status": "underway",
            "seller": "唐大门店",
            "status_name": "仓库已确认、处理中",
            "stock": true
        }
    ],
    "total": 1
}
```
}

返回值 （array）：

| 参数名          | 数据类型   | 说明                                       |
| ------------ | ------ | ---------------------------------------- |
| prochsn      | string | 采购单号                                     |
| store        | string | 门店地址                                     |
| proch_status | string | 采购单状态。```pending=待仓库确认； underway=仓库已确认、处理中； unaccepted=被仓库拒绝; deliverable=配送中; completed=已完成``` |
| stock        | bool   | 是否包含库存不足的商品。true 充足，false：不充足            |



##### 2）、发货——发货清单

> 该采购申请当中需要包装发货的商品。

请求地址：shipment/info

请求方式：get

请求参数：

| 参数名     | 数据类型   | 说明        |
| ------- | ------ | --------- |
| prochsn | string | 必须。采购申请单号 |

返回示例

```json
{
    "success": true,
    "errors": [],
    "data": [
        {
            "prochsn": "CD201708148B7214",
            "proch_time": "2017-08-14 09:25:24",
            "proch_person_name": "zyytest",
            "proch_person_phone": "18280439265",
            "goods": [
                {
                    "sku_id": 11,
                    "goods_name": "农夫山泉 白色 + 300ml",
                    "num": 120,
                    "unit": "瓶",
                    "stock": true
                }
            ],
            "remark": ""
        },
        {
            "prochsn": "CD20170818367714",
            "proch_time": "2017-08-18 03:23:38",
            "proch_person_name": "zyytest",
            "proch_person_phone": "18280439265",
            "goods": [
                {
                    "sku_id": 11,
                    "goods_name": "农夫山泉 白色 + 300ml",
                    "num": 120,
                    "unit": "瓶",
                    "stock": true
                }
            ],
            "remark": ""
        }
    ]
}
```

返回值 （array）：

返回data

| 参数                 | 类型          | 说明     |
| ------------------ | ----------- | ------ |
| prochsn            | string      | 采购单号   |
| proch_time         | datetime    | 采购申请日期 |
| proch_person_name  | string      | 采购申请人  |
| goods              | array\|json | 采购商品信息 |
| remark             | string      | 其他采购需求 |
| proch_person_phone | string      | 采购申请电话 |

返回goods

| 参数名        | 数据类型   | 说明          |
| ---------- | ------ | ----------- |
| sku_id     | int    | 商品具体 SKU ID |
| goods_name | string | 商品名称        |
| num        | int    | 数量          |
| unit       | string | 商品单位        |

##### 3）、采购单已发货包装信息

请求地址：shipment/proch/pack

请求方式：get

请求参数：

| 参数名     | 数据类型   | 说明        |
| ------- | ------ | --------- |
| prochsn | string | 必须。采购申请单号 |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": [
        {
            "boxsn": "CD4-TDMD261",
            "goods": [
                {
                    "num": "120",
                    "unit": "瓶",
                    "sku_id": "11",
                    "goods_name": "农夫山泉 白色 + 300ml"
                }
            ]
        }
    ]
}
```





返回值 array：

| 参数名   | 数据类型        | 说明     |
| ----- | ----------- | ------ |
| boxsn | string      | 箱号     |
| goods | array\|json | 该包装箱内的 |

pack.goods 数据：

| 参数名        | 数据类型   | 说明   |
| ---------- | ------ | ---- |
| goods_name | string | 商品名称 |
| num        | int    | 商品数量 |
| unit       | string | 商品单位 |



##### 4）、完成扫码包装

> 该接口用于仓库向门店发货，将商品打包组装时使用。工作人员扫描箱体上的二维码获取二维码编号信息进入商品打包详细界面，工作人员在该界面可以改变发货数量以及对该包装箱体拍照等动作。

请求地址：shipment/pack

请求方式：post

请求参数：

| 参数名        | 数据类型   | 说明                  |
| ---------- | ------ | ------------------- |
| qrcode     | string | 必须。二维码扫描后的long_code |
| imgs       | string | 箱体图片，多个图片用英文","分割   |
| prochsn    | string | 必须。采购申请单号           |
| goods_info | array  | 必须。商品信息。            |

goods_info参数说明

| 参数名        | 数据类型   | 说明          |
| ---------- | ------ | ----------- |
| sku_id     | int    | 商品具体 SKU ID |
| goods_name | string | 商品名称        |
| num        | int    | 数量          |
| unit       | string | 商品单位        |

##### 

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": {
        "ship_status": false,
        "prochsn": "CD201708148B7214",
        "short_code": "CD4-TDMD262"
    }
}
```

返回值 （ json）：

| 参数名         | 数据类型   | 说明                                       |
| ----------- | ------ | ---------------------------------------- |
| prochsn     | string | 采购申请单号                                   |
| ship_status | bool   | 当前采购申请是否还有未包装的商品，true 有 false 否。拥有未包装的商品需回到发货界面 |
| short_code  | string | 箱体短码                                     |



##### 5）获取可合并的采购单

请求地址：shipment/merge

请求方式：get

请求参数

| 参数名     | 数据类型   | 说明        |
| ------- | ------ | --------- |
| prochsn | string | 必须。采购申请单号 |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": [
        "CD201708148B7214"
    ]
}
```

返回数据说明

| 参数   | 类型    | 说明   |
| ---- | ----- | ---- |
| data | array | 采购单号 |

### 4、商品库存模块

​	

##### 1）、商品库存

> 每个区域下商品默认显示10条，更多区域商品查看 仓库区域下具体商品接口

请求地址：repertory/lists

请求方式：get

请求参数：

| 参数名      | 数据类型 | 是否必须 | 说明                                |
| -------- | ---- | ---- | --------------------------------- |
| start    | int  | 否    | 当前偏移量，默认为：0。eg：若要从第200条数据开始则为200. |
| page_num | int  | 否    | 每页显示数量，默认为：10                     |

返回数据  （json）：

| 参数名   | 数据类型        | 说明          |
| :---- | :---------- | :---------- |
| total | int         | 总条数         |
| data  | array\|json | 具体库房区域商品数据。 |

data 数据 （json）：

| 参数名           | 数据类型        | 说明          |
| ------------- | ----------- | ----------- |
| location_id   | int         | 区域ID        |
| location_name | string      | 区域          |
| goods         | array\|json | 商品数据（默认10条） |

goods 数据 （array）：

| 参数名        | 数据类型   | 说明         |
| ---------- | ------ | ---------- |
| goods_name | string | 商品名称       |
| sku_id     | ing    | 具体商品       |
| location   | string | 具体库位信息     |
| amount     | string | 库存数量（包含商品） |

返回值：

```json
{
    "success": true,
    "errors": [],
    "data": {
        "total": 3,
        "data": [
            {
                "location_id": 1,
                "location_name": "走廊区",
                "goods": [
                    {
                        "location": "L-S-01,T-S-120",
                        "goods_name": "乐事薯片 烧烤 + 500g",
                        "sku_id": 4,
                        "amount": "112 包 "
                    },
                    {
                        "location": "T-S-120",
                        "goods_name": "乐事薯片 椒盐 + 500g",
                        "sku_id": 7,
                        "amount": "5 箱 1 包 "
                    }
                ]
            },
            {
                "location_id": 3,
                "location_name": "饮料区",
                "goods": []
            },
            {
                "location_id": 5,
                "location_name": "零食一区",
                "goods": []
            }
        ]
    }
}
```



##### 2）、库存商品搜索

请求地址：repertory/lists/search

请求方式：get

请求参数：

| 参数名      | 数据类型   | 是否必须 | 说明                                |
| -------- | ------ | ---- | --------------------------------- |
| keywords | string | 是    | 商品名称                              |
| start    | int    | 否    | 当前偏移量，默认为：0。eg：若要从第200条数据开始则为200. |
| age_num  | int    | 否    | 每页显示数量，默认为：20                     |

返回值：

| 参数名   | 数据类型        | 说明   |
| ----- | ----------- | ---- |
| Total | int         | 数量   |
| data  | array\|json | 具体数据 |

data数据：

| 参数名        | 数据类型   | 说明     |
| ---------- | ------ | ------ |
| location   | string | 具体库位信息 |
| goods_name | string | 商品名称   |
| sku_id     | int    | SKUID  |
| amount     | string | 具体库存。  |

返回值:

```Json
{
    "success": true,
    "errors": [],
    "data": {
        "total": 4,
        "data": [
            {
                "location": "L-S-01,T-S-120",
                "goods_name": "乐事薯片 烧烤 + 500g",
                "sku_id": 4,
                "amount": "112 包 "
            },
            {
                "location": "T-S-120",
                "goods_name": "乐事薯片 椒盐 + 500g",
                "sku_id": 7,
                "amount": "5 箱 1 包 "
            }
        ]
    }
}
```





##### 3)、待分配库位的商品

请求地址：repertory/lists/wait

请求方式：get

请求参数：

| 参数名      | 数据类型 | 说明                                |
| -------- | ---- | --------------------------------- |
| start    | int  | 当前偏移量，默认为：0。eg：若要从第200条数据开始则为200. |
| page_num | int  | 每页显示数量，默认为：10                     |

返回值：

| 参数名   | 数据类型        | 说明   |
| ----- | ----------- | ---- |
| total | int         | 数量   |
| data  | array\|json | 具体数据 |

data数据：

| 参数名        | 数据类型   | 说明     |
| ---------- | ------ | ------ |
| location   | string | 具体库位信息 |
| goods_name | string | 商品名称   |
| sku_id     | int    | SKUID  |
| amount     | string | 具体库存。  |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": {
        "total": 1,
        "data": [
            {
                "location": "",
                "goods_name": "乐事薯片 烧烤 + 500g",
                "sku_id": 8,
                "amount": "6 箱 "
            }
        ]
    }
}
```





##### 4)、仓库区域下具体商品

请求地址：repertory/goods

请求方式：get

请求参数：

| 参数名      | 数据类型 | 是否必须 | 说明                                |
| -------- | ---- | ---- | --------------------------------- |
| start    | int  | 否    | 当前偏移量，默认为：0。eg：若要从第200条数据开始则为200. |
| page_num | int  | 否    | 每页显示数量，默认为：10                     |
| area_id  | int  | 是    | 必须。库房区域ID                         |

返回值：

| 参数名           | 数据类型        | 说明     |
| ------------- | ----------- | ------ |
| total         | int         | 数量     |
| location_name | string      | 区域位置名称 |
| data          | array\|json | 具体数据   |

data数据：

| 参数名        | 数据类型   | 说明     |
| ---------- | ------ | ------ |
| location   | string | 具体库位信息 |
| goods_name | string | 商品名称   |
| sku_id     | int    | SKUID  |
| amount     | string | 具体库存。  |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": {
        "total": 1,
        "data": [
            {
                "location": "L-S-01",
                "goods_name": "乐事薯片 烧烤 + 500g",
                "sku_id": 4,
                "amount": "100 包 "
            }
        ]
    }
}
```





##### 5）、库存商品详情

请求地址：repertory/goods/info

请求方式：get

请求参数：

| 参数名    | 数据类型 | 是否必须 | 说明        |
| ------ | ---- | ---- | --------- |
| sku_id | int  | 是    | 必须。sku id |

返回值 （json）：

| 参数名        | 数据类型        | 说明     |
| ---------- | ----------- | ------ |
| goods_name | string      | 商品名称   |
| location   | array\|json | 所在区域数据 |

location 数据 （array）：

| 参数名           | 数据类型   | 说明                  |
| ------------- | ------ | ------------------- |
| location_name | string | 库位名称                |
| location_id   | int    | 库位ID                |
| amout         | int    | 当前库位商品数量（以最小单品单位显示） |
| unit          | string | 单位                  |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": {
        "goods_name": "乐事薯片 烧烤 + 500g",
        "sku_id": "4",
        "location": [
            {
                "location_id": 7,
                "location_name": "L-S-01",
                "amount": 100,
                "unit": "包"
            },
            {
                "location_id": 2,
                "location_name": "T-S-120",
                "amount": 12,
                "unit": "包"
            },
            {
                "location_id": 5,
                "location_name": "零食一区",
                "amount": 12,
                "unit": "包"
            }
        ]
    }
}
```



##### 6）、获取所有库位信息

请求地址：repertory/location

请求方式：get

请求方式：无

返回值  （ array）：

| 参数名           | 数据类型   | 说明     |
| ------------- | ------ | ------ |
| location_id   | Int    | 位置ID   |
| location_name | String | 位置名称   |
| parent_id     | int    | 上级位置ID |

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": [
        {
            "location_id": 1,
            "location_name": "走廊区",
            "parent_id": 0
        },
        {
            "location_id": 2,
            "location_name": "T-S-120",
            "parent_id": 1
        },
        {
            "location_id": 3,
            "location_name": "饮料区",
            "parent_id": 0
        },
        {
            "location_id": 5,
            "location_name": "零食一区",
            "parent_id": 0
        },
        {
            "location_id": 7,
            "location_name": "L-S-01",
            "parent_id": 1
        },
        {
            "location_id": 8,
            "location_name": "L-S-01-01",
            "parent_id": 7
        }
    ]
}
```



##### 7）、更改商品库位

> 请求库位ID为该商品所存放的所有库位ID合集。

请求地址：retertory/goods/location

请求方式：put

请求参数：

| 参数名      | 数据类型   | 说明             |
| -------- | ------ | -------------- |
| sku_id   | int    | 商品SKU ID       |
| location | String | 库位ID，多个用“,"隔开。 |

返回值：无

返回示例：

```json
{
    "success": true,
    "errors": [],
    "data": []
}
```



##### 8）、商品库存数量位置迁移

请求地址：retertory/goods/remove

请求方式：path

请求参数：

| 参数名           | 数据类型 | 是否必须 | 说明       |
| ------------- | ---- | ---- | -------- |
| form_location | int  | 是    | 将要被迁移的库位 |
| to_location   | int  | 是    | 将要迁移到的库位 |
| amount        | int  | 是    | 要迁移的数量   |
| sku_id        | int  | 是    | 商品ID     |

返回值：无

