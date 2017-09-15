
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


