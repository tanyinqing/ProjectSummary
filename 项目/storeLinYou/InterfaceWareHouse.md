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

