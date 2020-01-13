
# 合约市场行情接口

## 获取合约信息 

###  示例

- GET `swap-api/v1/swap_contract_info`

###  请求参数

参数名称     |  参数类型   |  必填   |  描述  |
---------------- |  -------------- |  ---------- |  ------------------------------------------------------------|

contract_code   |  string         |  false |      "BTC-USD",不填查询所有合约  |

>Response:

```json
    {
      "status": "ok",
      "data": [
        {
          "symbol": "BTC",
          "contract_code": "BTC-USD",
          "contract_size": 100,
          "price_tick": 0.001,
          "settlement_date": "1490759594752",
          "create_date": "14907595947",
          "contract_status": 1
         }
        ],
      "ts":158797866555
    }
```

###  返回参数

参数名称              |  是否必须   |  类型   |  描述                          |  取值范围|
-------------------------- |  ----------------- |  ---------- |  --------------------------------- |  -----------------------------------------------------------------------|
status                     |  true           |  string     |  请求处理结果                      |  "ok" , "error"  |
\<list\>(属性名称: data)    |                  |           |                               |   |
symbol                     |  true           |  string     |  品种代码                          |  "BTC","ETH"...  |
contract_code             |  true           |  string     |  合约代码                          |  "BTC-USD" ...  |
contract_size             |  true           |  decimal    |  合约面值，即1张合约对应多少美元   |  10, 100...  |
price_tick                |  true           |  decimal    |  合约价格最小变动精度             |  0.001, 0.01...  |
settlement_date             |  true           |  string     |  合约下次结算时间                     |  如"1490759594752"  |
create_date               |  true           |  string     |  合约上市时间                      |  如"1490759594752"  |
contract_status           |  true           |  int        |  合约状态                          |  合约状态: 1:上市、3:停牌、5:结算中、6:交割中、7:结算完成、8:交割完成  |
\</list\>    |             |               |                     |        |                 
ts                         |  true           |  long       |  响应生成时间点，单位：毫秒  |      

## 获取合约指数信息

###  示例

- GET `swap-api/v1/swap_index`

```shell
curl "https://api.hbdm.com/swap-api/v1/swap_index?contract_code=BTC-USD"
```

###  请求参数

参数名称   |  参数类型   | 必填   | 描述  |
-------------- |  -------------- |  ---------- |  ----------------  |
contract_code         |  string         |  true       |  "BTC-USD","ETH-USD"...  |

> Response:

```json
    {
      "status":"ok",
      "data": [
         {
           "contract_code": "BTC-USD",
           "index_price":471.0817,
           "index_ts": 1490759594752
          }
        ],
      "ts": 1490759594752
    }
```

###  返回参数

参数名称               | 是否必须   | 类型   |  描述             | 取值范围 |
--------------------------  | --------------| ----------  | ---------------------------- |  ----------------  |
status                    | true           |  string     |  请求处理结果                 |  "ok" , "error"  |
\<list\>(属性名称: data)    |                |           |                           |  |
contract_code                     |  true           |  string     |  指数代码                    | "BTC-USD","ETH-USD"...  |
index_price               |  true           |  decimal    |  指数价格   |                  |
index_ts                |  true           |  long   |  响应生成时间点，单位：毫秒   |                  |
\</list\>               |                |           |                           |  |                                                            
ts                         |  true           |  long       |  时间戳，单位：毫秒   |   |

## 获取合约最高限价和最低限价

###  示例

- GET `swap-api/v1/swap_price_limit`

###  请求参数

参数名称     | 参数类型    | 必填    | 描述 |
----------------  | --------------  | ---------- |  -----------------------------------------------------------------  |

contract_code   |  string         |  true |      BTC-USD  | 合约代码

> Response:

```json
    {
      "status":"ok",
      "data": 
       [{
          "symbol":"BTC",
          "high_limit":443.07,
          "low_limit":417.09,
          "contract_code": "BTC-USD"
         }],
      "ts": 1490759594752
    }
```

###  返回参数

参数名称              | 是否必须   | 类型    | 描述                      | 取值范围 |
-------------------------- |-------------- |---------- |---------------------------- |------------------------------------------------------ |
status  |  true  |  string  |  请求处理结果  |  "ok" ,"error"  |
\<list\>(属性名称: data)  |    |   |    |    |
symbol  |  true  |  string  |  品种代码  |  "BTC","ETH" ...                                    |
high_limit  |  true  |  decimal  |  最高买价|                                                          |
low_limit  | true  |  decimal   |  最低卖价|                                                          |
contract_code   |  true      |  string     |  合约代码      |  "BTC-USD" ...  |
\<list\>  |    |    |    |    |
ts  |    true  |  long  |  响应生成时间点，单位：毫秒              |            |


## 获取当前可用合约总持仓量 

###  示例

- GET `swap-api/v1/swap_open_interest`

###  请求参数

参数名称 | 参数类型    | 必填    | 描述 |
---------------- |  -------------- |  ---------- |  -----------------------------------------------------------------  |
contract_code   |  string         |  false |     "BTC-USD",不填查询所有合约  |

> Response:

```json
    {
      "status":"ok",
      "data":
        [{
          "symbol":"BTC",
          "volume":123,
          "amount":106,
          "contract_code": "BTC-USD"
         }],
      "ts": 1490759594752
    }
```

###  返回参数

参数名称 |     是否必须    | 类型    | 描述 | 取值范围 |
-------------------------- |  -------------- |  ---------- |  ----------------------------  | ------------------------------------------------------  |
status  |  true  |  string  |  请求处理结果| "ok" , "error"  |
\<list\>(属性名称: data)  |    |    |   |    |
symbol  |  true  |  string  |  品种代码  |  "BTC", "ETH" ...  |
volume  |  true  |  decimal  |  持仓量(张)|    |   
amount  |  true  |  decimal  |  持仓量(币)|    |   
contract_code             |  true           |  string     |  合约代码                          |  "BTC-USD" ...  |
\</list\>  |    |    |    |    |
ts  |    true  |  long  |  响应生成时间点，单位：毫秒   |


## 获取行情深度数据

###  示例

- GET `/swap-ex/market/depth`

###  请求参数

参数名称   |  参数类型     |  必填    |  描述  |
-------------- |  -------------- |  ---------- |  -------------------------------------------------------------------------------- |
contract_code   |  string         |  true |      "BTC-USD" ...  |
type  |  string  |    true  |  (150档数据)  step0, step1, step2, step3, step4, step5（合并深度1-5）；step0时，不合并深度, (20档数据)  step6, step7, step8, step9, step10, step11（合并深度7-11）；step6时，不合并深度  |

>tick 说明:

```
    "tick": {
      "id": 消息id.
      "ts": 消息生成时间，单位：毫秒.
      "bids": 买盘,[price(挂单价), vol(此价格挂单张数)], //按price降序.
      "asks": 卖盘,[price(挂单价), vol(此价格挂单张数)]  //按price升序.
      "ch": 数据所属的 channel,
      "mrid": 订单ID,
      "ts": 时间戳,
      "version": 版本
    }
```

> Response:

```json
    {
      "ch":"market.BTC-USD.depth.step5",
      "status":"ok",
        "tick":{
          "asks":[
            [6580,3000],
            [70000,100]
            ],
          "bids":[
            [10,3],
            [2,1]
            ],
          "ch":"market.BTC-USD.depth.step5",
          "id":1536980854,
          "mrid":6903717,
          "ts":1536980854171,
          "version":1536980854
        },
      "ts":1536980854585
    }
```

###  返回参数

参数名称   |   是否必须  |   数据类型   |   描述   |   取值范围   |
-------- | -------- | -------- |  --------------------------------------- | -------------- | 
ch | true |  string | 数据所属的 channel，格式： market.period | | 
status | true |  string | 请求处理结果 | "ok" , "error" | 
asks | true | object |卖盘,[price(挂单价), vol(此价格挂单张数)], 按price升序 | | 
bids | true| object | 买盘,[price(挂单价), vol(此价格挂单张数)], 按price降序 | | 
mrid  | true| string | 订单ID | | 
ts | true | number | 响应生成时间点，单位：毫秒 | |

## 获取K线数据

###  示例

- GET `/swap-ex/market/history/kline`

###  请求参数

参数名称    |  是否必须  |   类型     |  描述    |  默认值   |  取值范围  |
-------------- |  -------------- |  ---------- |  ---------- |  ------------ |  -----------------------------------------------------|
contract_code             |  true           |  string     |  合约代码                          |  "BTC-USD" ...  |
period  |    true  |  string  |  K线类型  |  |  1min, 5min, 15min, 30min, 60min,4hour,1day, 1mon  |
size  |  true  |  integer    |  获取数量   |  150  |  [1,2000]  |

> Data说明：

```
"data": [
  {
    "id": K线id,
    "vol": 成交量(张)，买卖双边成交量之和,
    "count": 成交笔数,
    "open": 开盘价,
    "close": 收盘价,当K线为最晚的一根时，是最新成交价
    "low": 最低价,
    "high": 最高价,
    "amount": 成交量(币), 即 sum(每一笔成交量(张)*单张合约面值/该笔成交价)
   }
]
```

> Response:

```json
    {
      "ch": "market.BTC-USD.kline.1min",
      "data": [
        {
          "vol": 2446,
          "close": 5000,
          "count": 2446,
          "high": 5000,
          "id": 1529898120,
          "low": 5000,
          "open": 5000,
          "amount": 48.92
         },
        {
          "vol": 0,
          "close": 5000,
          "count": 0,
          "high": 5000,
          "id": 1529898780,
          "low": 5000,
          "open": 5000,
          "amount": 0
         }
       ],
      "status": "ok",
      "ts": 1529908345313
    }
```

###  返回参数

参数名称   |  是否必须     |  数据类型     |  描述  |   取值范围  |
--------------  |  -------------- |  -------------- |  ------------------------------------------ |  ----------------  |
ch  |  true  |  string  |    数据所属的 channel，格式： market.period   |        |
data  |  true  |  object  |    KLine 数据  |   | 
status  |    true  |  string  |    请求处理结果  |  "ok" , "error"  |
ts  |  true  |  number  |    响应生成时间点，单位：毫秒  |    | 

## 获取聚合行情

###  示例

- GET `/swap-ex/market/detail/merged`

###  请求参数

参数名称   |  是否必须   |  类型   |  描述   |  默认值   |  取值范围  |
--------------  | --------------  | ---------- |  ----------  | ------------ |  --------------------------------------------------------------------------------  |
contract_code             |  true           |  string     |  合约代码                          |  "BTC-USD" ...  |

>tick说明:

```
    "tick": {
      "id": K线id,
      "vol": 成交量（张），买卖双边成交量之和,
      "count": 成交笔数,
      "open": 开盘价,
      "close": 收盘价,当K线为最晚的一根时，是最新成交价
      "low": 最低价,
      "high": 最高价,
      "amount": 成交量(币), 即 sum(每一笔成交量(张)*单张合约面值/该笔成交价)
      "bid": [买1价,买1量(张)],
      "ask": [卖1价,卖1量(张)]
     }
```

> Response:

```json
    {
      "ch": "market.BTC-USD.detail.merged",
      "status": "ok",
      "tick": 
        {
          "vol":"13304",
          "ask": [5001, 2],
          "bid": [5000, 1],
          "close": "5000",
          "count": "13305",
          "high": "5000",
          "id": 1529387841,
          "low": "5000",
          "open": "5000",
          "ts": 1529387842137,
          "amount": "266.1"
         },
      "ts": 1529387842137
    }
```

###  返回参数

参数名称     |  是否必须    |   数据类型     |  描述  |    取值范围  |
-------------- |  -------------- |  -------------- |  ----------------------------------------------------------| ----------------  |
ch  |  true  |  string  |    数据所属的 channel，格式： market.\$symbol.detail.merged   |     |
status  |    true  |  string  |    请求处理结果  |  "ok" , "error"  |
tick  |  true  |  object  |    24小时成交量、开盘价和收盘价  |    |
ts  |  true  |  number  |    响应生成时间点，单位：毫秒  |    | 

## 获取市场最近成交记录

###  示例

- GET `/swap-ex/market/trade`

###  请求参数

参数名称     |  是否必须   |  类型   |  描述   |  默认值  |  取值范围  |
-------------- |  -------------- |  ---------- |  ---------- |  ------------ |  --------------------------------------------------------------------------------  |
contract_code             |  true           |  string     |  合约代码                          |  "BTC-USD" ...  |

>Tick说明：

```
    "tick": {
      "id": 消息id,
      "ts": 最新成交时间,
      "data": [
        {
       "id": 成交id,
        "price": 成交价钱,
         "amount": 成交量(张)，买卖双边成交量之和,
         "direction": 主动成交方向,
         "ts": 成交时间
        }
      ]
    }
```


> Response:

```json
    {
      "ch": "market.BTC-USD.trade.detail",
      "status": "ok",
      "tick": {
        "data": [
          {
            "amount": "2",
            "direction": "sell",
            "id": 6010881529486944176,
            "price": "5000",
            "ts": 1529386945343
           }
         ],
        "id": 1529388202797,
        "ts": 1529388202797
        },
      "ts": 1529388202797
    }
```

###  返回参数

参数名称     |  是否必须   |  类型   |  描述  |  默认值   |  取值范围  |
--------------  | --------------  | ----------  | ---------------------------------------------------------  | ------------ |  --------------  |
ch  |  true  |  string  |  数据所属的 channel，格式： market.\$contract_code.trade.detail  |  |   |
status  |  true  |  string  |  |  |  "ok","error" |
tick  |  true  |  object  |  Trade 数据  |    |    |   
ts  |  true  |  number  |  发送时间  |   |    |


## 批量获取最近的交易记录

###  示例

- GET `/swap-ex/market/history/trade`

###  请求参数：

参数名称     |  是否必须     | 数据类型   |  描述  |    默认值    |  取值范围  |
-------------- |  -------------- |  -------------- |  -------------------- |  ------------ |  --------------------------------------------------------------------------------  |
contract_code             |  true           |  string     |  合约代码                          |  "BTC-USD" ...  |
size  |  true  |  number  |    获取交易记录的数量  | 1  |  [1, 2000]  |

>data说明：

```
    "data": {
      "id": 消息id,
      "ts": 最新成交时间,
      "data": [
        {
          "id": 成交id,
          "price": 成交价,
          "amount": 成交量(张)，买卖双边成交量之和,
          "direction": 主动成交方向,
          "ts": 成交时间
        }
      ]
    }
```

> Response:

```json
    {
      "ch": "market.BTC-USD.trade.detail",
      "status": "ok",
      "ts": 1529388050915,
      "data": [
        {
          "id": 601088,
          "ts": 1529386945343,
          "data": [
            {
             "amount": 2,
             "direction": "sell",
             "id": 6010881529486944176,
             "price": 5000,
             "ts": 1529386945343
             }
           ]
        }
       ]
    }
```

###  返回参数

参数名称   |  是否必须     |  数据类型    |  描述  |    取值范围   |
--------------  | --------------  | --------------  | ---------------------------------------------------------  | ---------------  |
ch  |  true  |  string  |    数据所属的 channel，格式： market.$contract_code.trade.detail   |    |
data  |  true  |  object  |    Trade 数据  |    |
status  |  true  |  string  |    |    "ok"，"error" |
ts  |  true  |  number  |    响应生成时间点，单位：毫秒  |    |

## 查询合约风险准备金余额和预估分摊比例

- GET `swap-api/v1/swap_risk_info`

### 请求参数

 参数名称               |   是否必须  |  类型  |  描述             |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
contract_code   |  string         |  false |     "BTC-USD",不填返回所有合约  |

> Response:

```json
{
  "status": "ok",
  "ts": 158797866555,
  "data": [
    {
      "contract_code": "BTC-USD",
      "insurance_fund": 3806.4615259197324414715719,
      "estimated_clawback": 0.0023
    }
  ]
}

```

### 返回参数

  参数名称                |   是否必须  |   类型   |   描述             |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
 status | true | string | 请求处理结果	 | "ok" , "error" |
 ts | true  | long | 响应生成时间点，单位：毫秒 |  |
 \<data\> |  |  |  |  |
contract_code             |  true           |  string     |  合约代码                          |  "BTC-USD" ...  |
 insurance_fund | true  | decimal | 风险准备金余额 |  |
 estimated_clawback | true  | decimal | 预估分摊比例 |  |
 \</data\> |  |  |  |  |

## 查询合约风险准备金余额历史数据

- GET `swap-api/v1/swap_insurance_fund`

### 请求参数

  参数名称                |   是否必须   |   类型    |    描述             |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |

> Response:

```json
{
  "status": "ok",
  "ts": 158797866555,
  "data":   {
     "symbol": "BTC",
     "contract_code": "BTC-USD",
     "tick": [
        {
          "insurance_fund": 3806.4615259197324414715719,
          "ts": 158797866555
         }
      ]
  }
}

```

### 返回参数

  参数名称                |   是否必须   |   类型    |    描述             |    取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
 status | true | string | 请求处理结果	 | "ok" , "error" |
 ts | true  | long | 响应生成时间点，单位：毫秒 |  |
 \<data\> |  |  |  | 字典数据 |
 symbol | true  | string | 品种代码 | "BTC","ETH"... |
 contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |
 \<tick\> |  |  |  |  |
 insurance_fund | true  | decimal | 风险准备金余额 |  |
 ts | true  | long | 数据时间点，单位：毫秒 |  |
 \</tick\> |  |  |  |  |
 \</data\> |  |  |  |  |

## 查询平台阶梯调整系数

- GET `swap-api/v1/swap_adjustfactor`

### 请求参数

  参数名称                |   是否必须   |    类型   |   描述             |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
 contract_code | false | string | 合约代码	 | "BTC-USD"... ,如果缺省，默认返回所有品种 |

> Response:

```json
{
  "status": "ok",
  "data": [
   {
      "symbol": "BTC",
      "contract_code": "BTC-USD",
      "list": [
       {
          "lever_rate": 10,
          "ladders": [
           {
             "ladder": 1,
             "min_size": 0,
             "max_size": 100,
             "adjust_factor": 0.1
           },
           {
             "ladder": 2,
             "min_size": 101,
             "max_size": 500,
             "adjust_factor": 0.2
           }
           ]
       }
       ]
   }
   ],
   "ts": 158797866555
}

```

### 返回参数

   参数名称                |   是否必须  |   类型   |    描述             |    取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
 status | true | string | 请求处理结果	 | "ok" , "error" |
 ts | true  | long | 响应生成时间点，单位：毫秒 |  |
 \<data\> |  |  |  |  |
 symbol | true  | string | 品种代码 | "BTC","ETH"... |
 contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |
 \<list\> |  |  |  |  |
 lever_rate   | true     | decimal  | 杠杆倍数               |                |
 \<ladderDetail\> |  |  |  |  |
 min_size | true | decimal | 净持仓量的最小值 |  |
 max_size | true | decimal | 净持仓量的最大值 |  |
 ladder | true | int | 档位 |  |
 adjust_factor | true | decimal | 调整系数 |  |
 \</ladderDetail\> |  |  |  |  |
 \</list\> |  |  |  |  |
 \</data\> |  |  |  |  |

## 平台持仓量的查询

### 实例

- GET `swap-api/v1/swap_his_open_interest`

### 请求参数

|  参数名称                |   是否必须   |   类型    |   描述             |   取值范围       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| contract_code | true | string | 合约代码   | "BTC-USD" ... |
| period | true | string | 时间周期类型 | 1小时:"60min"，4小时:"4hour"，12小时:"12hour"，1天:"1day" |
| size | false | int | 获取数量 | 默认为：48，取值范围 [1,200]  |
| amount_type | true | int | 计价单位 | 1:张，2:币  |

> Response:

```json
{
  "status": "ok",
  "data": 
        {
         "symbol": "BTC",
         "contract_code": "BTC-USD",
         "tick": [
            {
             "volume": 1,
             "amount_type": 1,
             "ts": 1529387842137
            }
          ]
        },
    "ts": 158797866555
}
```

### 返回参数

|   参数名称                |   是否必须   |   类型    |   描述             |   取值范围       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| status | true | string | 请求处理结果   | "ok" , "error" |
| ts | true  | long | 响应生成时间点，单位：毫秒 |  |
| \<data\> |  |  | 字典数据 |  |
| symbol | true | string | 品种代码   | "BTC","ETH"... |
| contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |
| \<tick\> |  |  |  |  |
| volume | true | decimal | 持仓量 |  |
| amount_type | true | int | 计价单位 | 1:张，2:币  |
| ts | true | long | 统计时间 |  |
| \</tick\> |  |  |  |  |
| \</data\> |  |  |  |  |

- 注意：
  
  tick字段：数组内的数据按照时间倒序排列；
  data字段：字典类型。

# 合约资产接口

## 获取用户账户信息

###  示例

- POST  `swap-api/v1/swap_account_info`

###  请求参数

参数名称     |  是否必须   |  类型   |  描述   |  默认值   |  取值范围  |
-------------- |  -------------- |  ---------- |  ----------  | ------------ |  ------------------------------------------ |
contract_code   |  false          | string |     "BTC-USD"... ,如果缺省，默认返回所有合约  |  |

> Response:

```json
    {
      "status": "ok",
      "data": [
        {
          "symbol": "BTC",
   	      "contract_code": "BTC-USD",
          "margin_balance": 1,
          "margin_static": 0.5,
          "margin_position": 0,
          "margin_frozen": 3.33,
          "margin_available": 0.34,
          "profit_real": 3.45,
          "profit_unreal": 7.45,
          "withdraw_available":4.0989898,
          "risk_rate": 100,
          "liquidation_price": 100,
          "adjust_factor": 0.1
         },
        {
          "symbol": "ETH",
          "contract_code": "ETH-USD",
          "margin_balance": 1,
          "margin_static": 0.5,
          "margin_position": 0,
          "margin_frozen": 3.33,
          "margin_available": 0.34,
          "profit_real": 3.45,
          "profit_unreal": 7.45,
          "withdraw_available":4.7389859,
          "risk_rate": 100,
          "liquidation_price": 100,
          "adjust_factor": 0.1
         }
       ],
      "ts":158797866555
    }
```

###  返回参数

参数名称  |    是否必须   |  类型   |  描述  |   取值范围  |
-------------------------- |  -------------- |  ---------- |  ------------------------------------------ |  ----------------  |
status  |  true  |  string  |  请求处理结果  |  "ok" , "error"  |
\<list\>(属性名称: data)  |    |    |    |    |    
symbol  |  true  |  string  |  品种代码  |  "BTC","ETH"...  |
contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |
margin_balance  |  true  |  decimal    |  账户权益   |    |  
margin_static  |  true  |  decimal    |  静态权益   |    |  
margin_position  |  true  |  decimal    |  持仓保证金（当前持有仓位所占用的保证金）   |    |
margin_frozen  |  true  |  decimal    |  冻结保证金  |   | 
margin_available  |  true  |  decimal   |  可用保证金  |    | 
profit_real  |    true  |  decimal    |  已实现盈亏  |    | 
profit_unreal  |  true  |  decimal    |  未实现盈亏  |   | 
risk_rate  | true  |  decimal    |  保证金率  |  |   
liquidation_price  |    true  |  decimal    |  预估强平价  |   | 
withdraw_available  |   true  |  decimal    |  可划转数量  |   | 
lever_rate  |  true  |  decimal    |  杠杠倍数  |    |   
adjust_factor                | true     | decimal  | 调整系数               |                |  
\</list\>  |    |    |    |       |
ts  |    number  |    long  |  响应生成时间点，单位：毫秒  |    | 


## 获取用户持仓信息

###  示例

- POST `swap-api/v1/swap_position_info`

###  请求参数

参数名称   |  是否必须   |  类型    |  描述    |  默认值    |  取值范围  |
-------------- |  --------------  | ---------- |  ----------  | ------------ |  ------------------------------------------  |
contract_code   |  false  | string |  合约代码 | | "BTC-USD"... ,如果缺省，默认返回所有合约  |

> Response:

```json
    {
      "status": "ok",
      "data": [
        {
          "symbol": "BTC",
          "contract_code": "BTC-USD",
          "volume": 1,
          "available": 0,
          "frozen": 0.3,
          "cost_open": 422.78,
          "cost_hold": 422.78,
          "profit_unreal": 0.00007096,
          "profit_rate": 0.07,
          "profit": 0.97,
          "position_margin": 3.4,
          "lever_rate": 10,
          "direction":"buy",
          "last_price":7900.17
         }
        ],
     "ts": 158797866555
    }
```

###  返回参数

参数名称  |     是否必须   |  类型   |  描述  |  取值范围  |
-------------------------- |  -------------- |  ---------- |  ---------------------------- |  ------------------------------------------------------  |
status  |  true  |  string  |  请求处理结果  |  "ok" , "error"  |
\<list\>(属性名称: data)  |    |    |    |     |
symbol  |  true  |  string  |  品种代码  |  "BTC","ETH"...  |
contract_code  |  true  |  string  |  合约代码  |  "BTC-USD" ...  |
volume  |  true  |  decimal    |  持仓量|   |
available  | true  |  decimal    |  可平仓数量  |    |   
frozen  |  true  |  decimal    |  冻结数量  |    |
cost_open  |  true  |  decimal    |  开仓均价  |    |
cost_hold  | true  |  decimal    |  持仓均价  |    |
profit_unreal  |  true  |  decimal    |  未实现盈亏  |    |   
profit_rate  |    true  |  decimal    |  收益率  |   | 
profit  |  true  |  decimal   |  收益  |    |
position_margin  |  true  |  decimal    |  持仓保证金  |    |   
lever_rate  |  true  |  int  |   杠杠倍数  |    |
direction  |  true  |  string  |  "buy":买 "sell":卖  |    |
last_price  |  true  |  decimal    |  最新价  |     | 
\</list\>  |    |    |    |    |
ts  |    true  |  long  |  响应生成时间点，单位：毫秒   |    |


## 查询母账户下所有子账户资产信息


### 请求参数

- POST `swap-api/v1/swap_sub_account_list`

参数名称    |  是否必须   |   类型   |   描述          |   默认值   |   取值范围                                   |
----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
contract_code   |  false  | string |  合约代码 | | "BTC-USD"... ,如果缺省，默认返回所有合约  |

> Response:

```json
  {
    "status": "ok",
    "ts": 1499223904680,
  	"data": [
  	  {
  	    "sub_uid": 9910049,
  	    "list": [
                {
  	          "symbol": "BTC",
  	          "contract_code": "BTC-USD",
              "margin_balance": 1,
              "liquidation_price": 100,
  	          "risk_rate": 100
  	        },
  	        {
  	           "symbol": "ETH",
  	           "contract_code": "ETH-USD",
               "margin_balance": 1,
               "liquidation_price": 100,
  	           "risk_rate": 100
  	        }
  	      ]
  	  },
        {
  	      "sub_uid": 9910048,
  	      "list": [
                  {
  	           "symbol": "BTC",
  	           "contract_code": "BTC-USD",
               "margin_balance": 1,
               "liquidation_price": 100,
  	           "risk_rate": 100
  	        },
  	        {
  	           "symbol": "ETH",
  	           "contract_code": "ETH-USD",
               "margin_balance": 1,
               "liquidation_price": 100,
  	           "risk_rate": 100
  	        }
  	        ]
        }
  	]
  }
  
```

### 返回参数

  参数名称                 |   是否必须   |   类型    |     描述               |   取值范围      |
---------------------- | -------- | ------- | ------------------ | ------------ |
status | true | string | 请求处理结果	 | "ok" , "error" |
ts | true  | long | 响应生成时间点，单位：毫秒 |  |
\<data\> |  |  |  |  |
sub_uid | true  | long | 子账户UID |  |
\<list\> |  |  |  |  |
symbol | true | string | 品种代码 | "BTC","ETH"... |
contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |
margin_balance | true | decimal | 账户权益 |  |
liquidation_price | true | decimal | 预估强平价 |  |
risk_rate | true | decimal | 保证金率 |  |
\</list\> |  |  |  |  |
\</data\> |  |  |  |  |

- 备注

  只返回已经开通合约交易的子账户数据.


## 查询单个子账户资产信息

- POST `swap-api/v1/swap_sub_account_info`

###  请求参数*


  参数名称     |   是否必须   |  类型  |  描述         |   默认值   |   取值范围                                 |
----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
contract_code   |  false  | string |  合约代码 | | "BTC-USD"... ,如果缺省，默认返回所有合约  |
sub_uid | true | long | 子账户的UID	 |  |

> Response:

```json
  {
    "status": "ok",
    "data":  [ 
       {
          "symbol": "BTC",
          "contract_code": "BTC-USD",
          "margin_balance": 1,
          "margin_position": 0,
          "margin_frozen": 3.33,
          "margin_available": 0.34,
          "profit_real": 3.45,
          "profit_unreal": 7.45,
          "withdraw_available":4.0989898,
          "risk_rate": 100,
          "liquidation_price": 100,
          "adjust_factor": 0.1,
          "lever_rate":1,
          "margin_static": 3
        }
      ],
    "ts":158797866555
  }
  
```

### 返回参数

  参数名称                |   是否必须   |  类型    |   描述               |   取值范围      |
---------------------- | -------- | ------- | ------------------ | ------------ |
status | true | string | 请求处理结果	 | "ok" , "error" |
ts                       | true | long | 响应生成时间点，单位：毫秒 |  |
\<data\> |  |  |  |  |
symbol                  | true     | string  | 品种代码               | "BTC","ETH"...，当 $symbol值为 * 时代表订阅所有品种 |
contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |
margin_balance                  | true     | decimal  | 账户权益               |                |
margin_position                 | true     | decimal  | 持仓保证金（当前持有仓位所占用的保证金）               |                |
margin_frozen                 | true     | decimal  | 冻结保证金               |                |
margin_available                 | true     | decimal  | 可用保证金               |                |
profit_real                 | true     | decimal  | 已实现盈亏               |                |
profit_unreal                 | true     | decimal  | 未实现盈亏               |                |
risk_rate                 | true     | decimal  | 保证金率               |                |
liquidation_price                | true     | decimal  | 预估爆仓价               |                |
withdraw_available                | true     | decimal  | 可划转数量               |                |
lever_rate                | true     | decimal  | 杠杆倍数               |                |
adjust_factor                | true     | decimal  | 调整系数               |                |  
margin_static                | true     | decimal  | 静态权益               |                |  
\</data\> |  |  |  |  |


- 备注

  只能查询到开通合约交易的子账户信息；
  
  子账户来过合约系统但是未开通合约交易也不返回对应的数据；

## 查询单个子账户持仓信息

- POST `swap-api/v1/swap_sub_position_info`

### 请求参数

  参数名称    |  是否必须  |  类型  |  描述        |   默认值  |  取值范围                                  |
----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
contract_code   |  false  | string |  合约代码 | | "BTC-USD"... ,如果缺省，默认返回所有合约  |
sub_uid | true | long | 子账户的UID	 |  |

> Response:

```json 
  {                                               
    "status": "ok",                               
    "ts": 158797866555                            
    "data":[                                      
       {                                          
           "symbol": "BTC",                       
           "contract_code": "BTC-USD",               
           "volume": 1,                           
           "available": 0,                        
           "frozen": 0.3,                         
           "cost_open": 422.78,                   
           "cost_hold": 422.78,                   
           "profit_unreal": 0.00007096,           
           "profit_rate": 0.07,                   
           "profit": 0.97,                        
           "position_margin": 3.4,                
           "lever_rate": 10,                      
           "direction":"buy",
           "last_price":6000                  
       }                                        
     ]                                          
  } 
                                                
```

### 返回参数

  参数名称                |   是否必须   |   类型    |   描述              |   取值范围       |
---------------------- | -------- | ------- | ------------------ | ------------ |
status | true | string | 请求处理结果	 | "ok" , "error" |
ts                       | true | long | 响应生成时间点，单位：毫秒 |  |
\<data\> |  |  |  |  |
symbol                  | true     | string  | 品种代码               | "BTC","ETH"... |
contract_code                | true     | string  |  合约代码             | "BTC-USD" ... |
volume                | true     | decimal	  |  持仓量             |  |
available               | true     | decimal	  | 可平仓数量              |  |
frozen               | true     | decimal	  |  冻结数量             |  |
cost_open               | true     | decimal	  |  开仓均价             |  |
cost_hold               | true     | decimal	  | 持仓均价              |  |
profit_unreal               | true     | decimal	  | 未实现盈亏              |  |
profit_rate               | true     | decimal	  | 收益率              |  |
profit               | true     | decimal	  | 收益              |  |
position_margin               | true     | decimal	  | 持仓保证金              |  |
lever_rate               | true     | int	  | 杠杆倍数              |  |
direction               | true     | string	  |   仓位方向           |  "buy":多 "sell":空 |
last_price               | true     | decimal	  |   最新价           |   |
\</data\> |  |  |  |  |

## 查询用户财务记录

- POST `swap-api/v1/swap_financial_record`

###  请求参数

参数名称                |  是否必须  |  类型   |  描述              |  取值范围       |
----------------------- | -------- | ------- | ------------------ | ------------------------------- |
contract_code | true | string | 合约代码   | "BTC-USD"... |
type | false | string | 不填查询全部类型,【查询多类型中间用，隔开】 | 平多：3，平空：4，开仓手续费-吃单：5，开仓手续费-挂单：6，平仓手续费-吃单：7，平仓手续费-挂单：8，交割平多：9，交割平空：10，交割手续费：11，强制平多：12，强制平空：13，从币币转入：14，转出至币币：15，结算未实现盈亏-多仓：16，结算未实现盈亏-空仓：17，穿仓分摊：19，系统：26，活动奖励：28，返利：29，资金费-收入：30，资金费-支出：31 |
create_date | false | int | 可随意输入正整数，如果参数超过90则默认查询90天的数据 |  |
page_index | false | int | 第几页,不填默认第一页 |  |
page_size | false | int | 不填默认20，不得多于50 |  |

> Response:

```json                                
  {                                  
    "status": "ok",              
    "data":{                         
      "financial_record" : [         
        {                            
        "id": 192838272,             
        "ts": 1408076414000,         
        "symbol":"BTC",  
        "contract_code": "BTC-USD",           
        "type":1,              
        "amount":1,                  
        },                           
        {                            
          .........                  
        }                            
      ],                             
      "total_page":15,          
      "current_page":3,         
      "total_size":3            
      },                         
    "ts": 1490759594752              
  }                                  
```

### 返回参数

参数名称                |   是否必须  |  类型   |  描述              |   取值范围        |
----------------------- | -------- | ------- | ------------------ | ------------------------------- |
status | true | string | 请求处理结果   | "ok" , "error" |
ts | true  | long | 响应生成时间点，单位：毫秒 |  |
\<data\> |  |  | 字典类型 |  |
\<financial_record\> |  |  |  |  |
id | true  | long |  |  |
ts | true  | long | 创建时间 |  |
symbol | true  | string | 品种代码 | "BTC","ETH"... |
contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |
type | true  | int | 交易类型 | 平多：3，平空：4，开仓手续费-吃单：5，开仓手续费-挂单：6，平仓手续费-吃单：7，平仓手续费-挂单：8，交割平多：9，交割平空：10，交割手续费：11，强制平多：12，强制平空：13，从币币转入：14，转出至币币：15，结算未实现盈亏-多仓：16，结算未实现盈亏-空仓：17，穿仓分摊：19，系统：26，活动奖励：28，返利：29，资金费-收入：30，资金费-支出：31  |
amount | true  | decimal | 金额 |  |
\</financial_record\> |  |  |  |  |
total_page | true  | int | 总页数 |  |
current_page | true  | int | 当前页 |  |
total_size | true  | int | 总条数 |  |
\</data\> |  |  |  |  |

## 查询用户当前的下单量限制

- POST `swap-api/v1/swap_order_limit`


### 请求参数

  参数名称               |   是否必须   |  类型  |  描述             |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
 contract_code   |  false  | string |  合约代码 | "BTC-USD"... ,如果缺省，默认返回所有合约 |
 order_price_type | true  | string | 订单报价类型 | "limit":限价，"opponent":对手价，"lightning":闪电平仓，"optimal_5":最优5档，"optimal_10":最优10档，"optimal_20":最优20档，"fok":FOK订单，"ioc":IOC订单 |

> Response:

```json
{
  "status": "ok",
  "data":  {
      "order_price_type": "limit",
      "list":[
      {
          "symbol": "BTC",
          "contract_code": "BTC-USD",
          "open_limit": 3000,
          "close_limit": 3000
      }
      ]
   },
 "ts": 158797866555
}

```

### 返回参数

 参数名称                |  是否必须 |  类型  |  描述            |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
 status | true | string | 请求处理结果	 | "ok" , "error" |
 ts | true  | long | 响应生成时间点，单位：毫秒 |  |
 \<data\> |  |  |  |  |    
 order_price_type | true  | string | 订单报价类型 | "limit":限价，"opponent":对手价，"lightning":闪电平仓，"optimal_5":最优5档，"optimal_10":最优10档，"optimal_20":最优20档，"fok":FOK订单，"ioc":IOC订单 |
 \<list\> |  |  |  |  |
 symbol | true  | string | 品种代码 | "BTC","ETH"... |
 contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |
 open_limit | true | long | 合约开仓单笔下单量最大值 |  |
 close_limit | true | long | 合约平仓单笔下单量最大值 |  |
 \</list\>  |  |  |  |  |
 \</data\> |  |  |  |  |

## 查询用户当前的手续费费率

- POST `swap-api/v1/swap_fee`

### 请求参数

  参数名称                |  是否必须 |  类型  |   描述             |  取值范围      |
----------------------- | -------- | ------- | ------------------ | -------------- |
contract_code   |  false  | string |  合约代码 |  "BTC-USD"... ,如果缺省，默认返回所有合约  |

> Response:

```json
{
  "status": "ok",
  "data": [
    {
      "symbol": "BTC",
      "contract_code": "BTC-USD",
      "fee_asset": "BTC", 
      "open_maker_fee": "-0.00025",
      "open_taker_fee": "0.00075",
      "close_maker_fee": "-0.00025",
      "close_taker_fee": "0.00075",
    }
 ],
 "ts": 158797866555
}

```

### 返回参数

  参数名称                |  是否必须  |  类型   |  描述            |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
 status | true | string | 请求处理结果	 | "ok" , "error" |
 ts | true  | long | 响应生成时间点，单位：毫秒 |  |
 \<data\> |  |  |  |  |
 symbol | true  | string | 品种代码 | "BTC","ETH"... |
 contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |
 fee_asset | true  | string | 手续费币种 | "BTC","ETH"... |
 open_maker_fee | true | string | 开仓挂单的手续费费率，小数形式 | |
 open_taker_fee | true | string | 开仓吃单的手续费费率，小数形式 | |
 close_maker_fee | true | string | 平仓挂单的手续费费率，小数形式 | |
 close_taker_fee | true | string | 平仓吃单的手续费费率，小数形式 | |
 \</data\>  |  |  |  |  |

## 查询用户当前的划转限制

- POST `swap-api/v1/swap_transfer_limit`

### 请求参数

  参数名称                |  是否必须  |  类型   |    描述             |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
 contract_code   |  false  | string |  合约代码 |  "BTC-USD"... ,如果缺省，默认返回所有合约  |

> Response:

```json
{
  "status": "ok",
  "data": [
    {
      "symbol": "BTC",
      "contract_code": "BTC-USD",
      "transfer_in_max_each": 5000,
      "transfer_in_min_each": 5000,
      "transfer_out_max_each": 5000,
      "transfer_out_min_each": 5000,
      "transfer_in_max_daily": 5000,
      "transfer_out_max_daily": 5000,
      "net_transfer_in_max_daily": 5000,
      "net_transfer_out_max_daily": 5000
    }
 ],
 "ts": 158797866555
}

```

### 返回参数

  参数名称                |  是否必须  |  类型  |   描述             |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
 status | true | string | 请求处理结果	 | "ok" , "error" |
 ts | true  | long | 响应生成时间点，单位：毫秒 |  |
 \<data\> |  |  |  |  |
 symbol | true  | string | 品种代码 | "BTC","ETH"... |
 contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |
 transfer_in_max_each | true | decimal | 单笔最大转入量 |  |
 transfer_in_min_each | true | decimal | 单笔最小转入量 |  |
 transfer_out_max_each | true | decimal | 单笔最大转出量 |  |
 transfer_out_min_each | true | decimal | 单笔最小转出量 |  |
 transfer_in_max_daily | true | decimal | 单日累计最大转入量 |  |
 transfer_out_max_daily | true | decimal | 单日累计最大转出量 |  |
 net_transfer_in_max_daily | true | decimal | 单日累计最大净转入量 |  |
 net_transfer_out_max_daily | true | decimal | 单日累计最大净转出量 |  |
 \</data\>  |  |  |  |  |

## 用户持仓量限制的查询

- post `swap-api/v1/swap_position_limit`
  
### 请求参数

  参数名称               |  是否必须 |  类型  |  描述             |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
 contract_code   |  false  | string |  合约代码 |  "BTC-USD"... ,如果缺省，默认返回所有合约  |

> Response:

```json
{
  "status": "ok",
  "data": [
    {
      "symbol": "BTC",
      "contract_code": "BTC-USD",
      "buy_limit": 3000,
      "sell_limit": 3000
    }
 ],
 "ts": 158797866555
}

```

### 返回参数

  参数名称                |   是否必须   |  类型   |   描述              |   取值范围        |
----------------------- | -------- | ------- | ------------------ | -------------- |
status | true | string | 请求处理结果	 | "ok" , "error" |
ts | true  | long | 响应生成时间点，单位：毫秒 |  |
\<data\> |  |  |  |  |
symbol | true  | string | 品种代码 | "BTC","ETH"... |
contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |
buy_limit | true | decimal | 合约多仓持仓的最大值，单位为张 |  |
sell_limit | true | decimal | 合约空仓持仓的最大值，单位为张 |  |
\</data\> |  |  |  |  |

# 合约交易接口

## 合约下单 

###  示例

- POST  `swap-api/v1/swap_order`


###  请求参数

参数名  |  参数类型    |  必填   |  描述  |
-------------------- |  -------------- |  ----------  | ---------------------------------------------------------------  |
contract_code  |  string   |  true   |  合约代码,"BTC-USD"  |
client_order_id |   long  |  false  |  客户自己填写和维护，必须为数字  |
price  |  decimal  |   false  |  价格  |
volume  |    long  |  true  |  委托数量(张)  |
direction  |  string  |    true  |  "buy":买 "sell":卖  |
offset  |    string  |    true  |  "open":开 "close":平  |
lever_rate  |  int  | true  |  杠杆倍数[“开仓”若有10倍多单，就不能再下20倍多单]  |
order_price_type |  string  |    true  |  订单报价类型 "limit":限价 "opponent":对手价 "post_only":只做maker单,post only下单只受用户持仓数量限制,optimal_5：最优5档、optimal_10：最优10档、optimal_20：最优20档，"fok":FOK订单，"ioc":IOC订单  |

###  备注

对手价下单price价格参数不用传，对手价下单价格是买一和卖一价,optimal_5：最优5档、optimal_10：最优10档、optimal_20：最优20档下单price价格参数不用传，"limit":限价，"post_only":只做maker单 需要传价格。


###   开平方向

开多：买入开多(direction用buy、offset用open)

平多：卖出平多(direction用sell、offset用close)

开空：卖出开空(direction用sell、offset用open)

平空：买入平空(direction用buy、offset用close)

> Response:

```json

    {
      "status": "ok",
      "data": {
	      	"order_id": 88,
	      	"order_id_str": "88"
	      },
      "ts": 158797866555
    }
```

###  返回参数

参数名称  |   是否必须   |  类型   |  描述  |  取值范围  |
------------------- | -------------- | ---------- | -------------------------------------------- | ---------------- |
status  |   true  |  string  |  请求处理结果  |  "ok" , "error"  |
order_id  |  true  |  long  |  订单ID  |    | 
order_id_str  |  true  |  string  |  订单ID，字符串类型  |    | 
client_order_id  | true  |  long  |  用户下单时填写的客户端订单ID，没填则不返回  | 
ts  |  true  |  long  |  响应生成时间点，单位：毫秒  |    |   


## 合约批量下单 


###  示例

- POST  `swap-api/v1/swap_batchorder`

###  请求参数

参数名  |    参数类型   |  必填   |  描述  |
---------------------------------- | -------------- |  ---------- | -------------------------------------------------------------- |
\<list\>(属性名称: orders_data)  |    |    |    |  
contract_code  |  string   |  true   |  合约代码,"BTC-USD"  |
client_order_id  |  long  |  false  |  客户自己填写和维护，必须为数字  |
price  |  decimal  |   false  |  价格  |
volume  |  long  |  true  |  委托数量(张)  |
direction  |  string  |    true  |  "buy":买 "sell":卖  |
offset  |  string  |    true  |  "open":开 "close":平  |
lever_rate  |   int  | true  |  杠杆倍数[“开仓”若有10倍多单，就不能再下20倍多单]  |
order_price_type |  string  |    true  |  订单报价类型 "limit":限价 "opponent":对手价 "post_only":只做maker单,post only下单只受用户持仓数量限制,optimal_5：最优5档、optimal_10：最优10档、optimal_20：最优20档，"fok":FOK订单，"ioc":IOC订单  |
\</list\>  |    |    |    |

###  备注

对手价下单price价格参数不用传，对手价下单价格是买一和卖一价,optimal_5：最优5档、optimal_10：最优10档、optimal_20：最优20档下单price价格参数不用传，"limit":限价，"post_only":只做maker单 需要传价格。

一次最多允许20个订单。

> Response:

```json
    {
      "status": "ok",
      "data": {
        "errors":[
          {
            "index":0,
            "err_code": 200417,
            "err_msg": "invalid contract_code"
           },
          {
            "index":3,
            "err_code": 200415,
            "err_msg": "invalid contract_code"
           }
         ],
        "success":[
          {
            "index":1,
            "order_id":161256,
            "order_id_str": "88",
            "client_order_id":1344567
           },
          {
            "index":2,
            "order_id":161257,
            "order_id_str": "88",
            "client_order_id":1344569
           }
         ]
       },
      "ts": 1490759594752
    }
```

###  返回参数

参数名称  |  是否必须   |  类型   |  描述  |  取值范围  |
----------------------------- | -------------- | ---------- | -------------------------------------------- | ---------------- |
status  |   true  |  string  |  请求处理结果  | "ok" , "error"  |
\<list\>(属性名称: errors)  |    |    |    |     |
index  |    true  |  int  |   订单索引  |    |
err_code  |  true  |  int  |   错误码  |    |
err_msg  | true  |  string  |  错误信息  |    |
\</list\>  |    |    |    |     |
\<list\>(属性名称: success)  |    |    |    |     |
index  |    true  |  int  |   订单索引  |    |
order_id  |  true  |  long  |  订单ID  |    |
order_id_str  |  true  |  string  |  订单ID，字符串类型  |    |  
client_order_id  |  true  |  long  |  用户下单时填写的客户端订单ID，没填则不返回  | 
\</list\>  |    |    |    |    |
ts  |  true  |  long  |  响应生成时间点，单位：毫秒  |

## 撤销订单 

###  示例

- POST `swap-api/v1/swap_cancel`

###  请求参数

参数名称  |   是否必须   |  类型   |  描述  |
------------------- | -------------- | ---------- | -------------------------------------------------------------- |
order_id |  false  |  string  |  订单ID(多个订单ID中间以","分隔,一次最多允许撤消20个订单)  |
client_order_id  |  false  |  string  |  客户订单ID(多个订单ID中间以","分隔,一次最多允许撤消20个订单)  |
contract_code  |  true   |  string   |  合约代码,"BTC-USD"  |

###备注：

order_id和client_order_id都可以用来撤单，同时只可以设置其中一种，如果设置了两种，默认以order_id来撤单。

撤单接口返回结果只代表撤单命令发送成功，建议根据订单查询接口查询订单的状态来确定订单是否已真正撤销。

> Response:

```json

    {
  "status": "ok",
  "data": {
    "errors":[
      {
        "order_id":"161251",
        "err_code": 200417,
        "err_msg": "invalid contract_code"
       },
      {
        "order_id":161253,
        "err_code": 200415,
        "err_msg": "invalid contract_code"
       }
      ],
    "successes":[161256,1344567]
   },
  "ts": 1490759594752
}   
```

###  返回参数

参数名称  |  是否必须  |  类型  |  描述  |  取值范围  |
---------------------------- | -------------- | ---------- | -------------------------------------------------- | ---------------- |
status  |  true  |  string  |  请求处理结果  | "ok" , "error"  | 
\<list\>(属性名称: errors)  |    |    |    |    |  
order_id  |    true  |  string  |  订单ID  |    |   
err_code  |   true  |  int  |   错误码  |    |   
err_msg  |  true  |  string  |  错误信息  |    | 
\</list\>  |    |    |    |    |
successes  |   true  |  string  |  撤销成功的订单的order_id或client_order_id列表  |   |
ts  |  true  |  long  |  响应生成时间点，单位：毫秒  |   |


## 全部撤单 

###  示例

- POST  `swap-api/v1/swap_cancelall`

###  请求参数

参数名称    |  是否必须    |  类型    |  描述  |
-------------- | -------------- | ---------- | ---------------------------- |
contract_code  |  true   |  string   |  合约代码,"BTC-USD"  |

> Response:(多笔订单返回结果(成功订单ID,失败订单ID))

```json
    {
      "status": "ok",
      "data": {
        "errors":[
          {
            "order_id":"161251",
            "err_code": 200417,
            "err_msg": "invalid symbol"
           },
          {
            "order_id":161253,
            "err_code": 200415,
            "err_msg": "invalid symbol"
           }
          ],
        "successes":[161256,1344567]
       },
      "ts": 1490759594752
    }
```

###  返回参数

参数名称  |  是否必须   |  类型  |  描述  |  取值范围  |
---------------------------- | -------------- | ---------- | ---------------------------- | ---------------- |
status  |  true  |  string  |  请求处理结果  | "ok" , "error"  | 
\<list\>(属性名称: errors)  |    |    |    |    |
order_id  |    true  |  String  |  订单id  |   | 
err_code  |    true  |  int  |   订单失败错误码  |   |   
err_msg  |  true  |  int  |   订单失败信息  |    | 
\</list\>    |    |    |    |    |
successes  |    true  |  string  |  成功的订单  |    |   
ts  | true  |  long  |  响应生成时间点，单位：毫秒  |   | 


## 获取合约订单信息

###  示例

- POST  `swap-api/v1/swap_order_info`

###  请求参数

参数名称  |    是否必须    |  类型    |  描述  |
------------------- | -------------- | ---------- | ------------------------------------------------------------- |
order_id  |  false  |  string  |  订单ID(多个订单ID中间以","分隔,一次最多允许查询50个订单)  |
client_order_id   |  false  |  string  |  客户订单ID(多个订单ID中间以","分隔,一次最多允许查询50个订单)  |
contract_code  |  true   |  string   |  合约代码,"BTC-USD"  |

###  备注：

order_id和client_order_id都可以用来查询，同时只可以设置其中一种，如果设置了两种，默认以order_id来查询。结算后，会把结束状态的订单（5部分成交已撤单 6全部成交 7已撤单）删除掉。

client_order_id，24小时有效，超过24小时的订单根据client_order_id将查询不到。

> Response:

```json
    {
      "status": "ok",
      "data":[
        {
          "symbol": "BTC",
          "contract_code": "BTC-USD",
          "volume": 111,
          "price": 1111,
          "order_price_type": "limit",
          "direction": "buy",
          "offset": "open",
          "lever_rate": 10,
          "order_id": 106837,
          "order_id_str": "88",
          "client_order_id": 10683,
          "order_source": "web",
          "order_type": "1",
          "created_at": 1408076414000,
          "trade_volume": 1,
          "trade_turnover": 1200,
          "fee": 0,
          "fee_asset": "BTC", 
          "trade_avg_price": 10,
          "margin_frozen": 10,
          "profit": 10,
          "status": 0
         },
        {
          "symbol": "ETH",
          "contract_code": "BTC-USD",
          "volume": 111,
          "price": 1111,
          "order_price_type": "limit",
          "direction": "buy",
          "offset": "open",
          "lever_rate": 10,
          "order_id": 106837,
          "order_id_str": "88",
          "client_order_id": 10683,
          "order_source": "web",
          "order_type": "1",
          "created_at": 1408076414000,
          "trade_volume": 1,
          "trade_turnover": 1200,
          "fee": 0,
          "fee_asset": "BTC", 
          "trade_avg_price": 10,
          "margin_frozen": 10,
          "profit ": 10,
          "status": 0
         }
        ],
      "ts": 1490759594752
    }
```

###  返回数据

  参数名称  |    是否必须   |  类型   |  描述  |  取值范围  |
-------------------------- | -------------- | ---------- | --------------------------------------------------------------------------------------------  | ---------------------------------------------------- |
status  |  true  |  string  |  请求处理结果  |  "ok" , "error"  |
\<list\>(属性名称: data)  |    |    |    |    | 
symbol  |  true  |  string  |  品种代码  |    |  
contract_code  |  true  |  string  |  合约代码  | "BTC-USD" ...  |
volume  |  true  |  decimal    |  委托数量  |    | 
price   |  true  |  decimal    |  委托价格  |    | 
order_price_type  |    true  |  string  |  订单报价类型  | 订单报价类型 "limit":限价 "opponent":对手价 "post_only":只做maker单,post only下单只受用户持仓数量限制  |  
direction  |  true  |  string  |  买卖方向  |  "buy":买 "sell":卖  |
offset  |  true  |  string  |  开平方向 |  "open":开 "close":平  |
lever_rate  |  true  |  int  |   杠杆倍数  |  1\\5\\10\\20  |
order_id  |  true  |  long  |  订单ID  |    | 
order_id_str  |  true  |  string  |  订单ID，字符串类型  |    | 
client_order_id  |  true  |  long  |  客户订单ID  |    |  
created_at  |  true  |  long  |  创建时间  |    |
trade_volume    |  true  |  decimal  |    成交数量  |    |
trade_turnover  |  true  |  decimal  |   成交总金额  |    |    
fee  |   true  |  decimal  |     手续费  |     |   
fee_asset | true  | string | 手续费币种 | "BTC","ETH"... |
trade_avg_price  |  true  |  decimal  |    成交均价  |    | 
margin_frozen    |  true  |  decimal  |    冻结保证金  |     |   
profit  |  true  |  decimal  |    收益  |    |
status  |  true  |  int  |   订单状态  |  (1准备提交 2准备提交 3已提交 4部分成交 5部分成交已撤单 6全部成交 7已撤单 11撤单中)  |  
order_type    |  true  |  string  |  订单类型  |    1:报单 、 2:撤单 、 3:强平、4:交割              |
order_source  |  true  |  string  |  订单来源  |  （1:system、2:web、3:api、4:m 5:risk、6:settlement） |   
\</list\>  |    |    |    |    |
ts  |    true  |  long  |  时间戳  |  |   


## 获取订单明细信息

###  示例

- POST `swap-api/v1/swap_order_detail`

###  请求参数

参数名称    |  是否必须     |  类型    |  描述  |
-------------- | -------------- | ---------- | ------------------------ |
contract_code  |  true   |  string   |  合约代码,"BTC-USD"  |
order_id  | true  |  long  |   订单id  |
created_at  |  false  |  long  |   下单时间戳  |
order_type  |  true  |  int  |   订单类型，1:报单 、 2:撤单 、 3:强平、4:交割  |
page_index  |    false  |  int  |   第几页,不填第一页  |
page_size  |  false  |  int  |   不填默认20，不得多于50  |

> Response:

```json
    {
      "status": "ok",
      "data":{
        "symbol": "BTC",
        "contract_code": "BTC-USD",
        "volume": 111,
        "price": 1111,
        "order_price_type": "limit",
        "direction": "buy",
        "offset": "open",
        "lever_rate": 10,
        "margin_frozen": 10,
        "profit": 10,
        "order_source": "web",
        "created_at": 1408076414000,
        "canceled_at": 1408076414000,
        "instrument_price" : 10000,
        "final_interest" : 0,
        "adjust_value" : 0,
        "trades":[
          {
            "trade_id":112,
            "id": "1232-213123-1231",
            "trade_volume":1,
            "trade_price":123.4555,
            "trade_fee":0.234,
            "fee_asset": "BTC", 
            "trade_turnover":34.123,
            "role": "maker",
            "created_at": 1490759594752
          }
        ],
        "total_page":15,
        "total_size":3,
        "current_page":3
        },
      "ts": 1490759594752
    }
```

>错误:

```json
    {
     "status":"error",
     "err_code":20029,
     "err_msg": "invalid contract_code",
     "ts": 1490759594752
    }
```

###  返回数据

参数名称  |  是否必须   |  类型   |  描述  |  取值范围  |
----------------------------- | -------------- | ---------- | --------------------------------------------- | ------------------------------------------------------ |
status  |   true  |  string  |  请求处理结果  | "ok" , "error"  |
\<object\> (属性名称: data)  |    |    |    |    | 
symbol  |   true  |  string  |  品种代码  |    | 
contract_code  |  true  |  string  |  合约代码  |  "BTC-USD" ...  |
lever_rate  |   true  |  int  |   杠杆倍数  |  1\5\10\20  |
direction  |  true  |  string  |  买卖方向  | "buy":买 "sell":卖 |  
offset  |     true  |  string  | 开平方向 |  "open":开 "close":平  |
volume  |     true  |  decimal    |  委托数量  |    | 
price  |      true  |  decimal    |  委托价格  |    | 
created_at  |   true  |  long    |    创建时间  |    |
canceled_at  |   true  |  long    |    撤单时间  |    |
order_source  | true  |  string  |  订单来源  |   | 
order_price_type  | true  |  string  |  订单报价类型  |  订单报价类型 "limit":限价 "opponent":对手价 "post_only":只做maker单,post only下单只受用户持仓数量限制   |  
margin_frozen  |  true  |  decimal    |  冻结保证金  |    |    
profit  |   true  |  decimal    |  收益  |     |
total_page  |   true  |  int  |   总共页数  |    |
current_page  | true  |  int  |   当前页数  |    | 
total_size  |   true  |  int  |   总条数  |    |   
instrument_price  |   true  |  decimal  |   爆仓单合约价格  |    |   
final_interest  |   true  |  decimal  |   爆仓时合约权益  |    |   
adjust_value  |   true  |  decimal  |   爆仓时调整系数  |    |   
\<list\> (属性名称: trades)  |    |    |    |    | 
trade_id  |  true  |  long  |  撮合结果id  |    |  
id     | true     | string    | 成交唯一ID               |              |  
trade_price  |  true  |  decimal  |  撮合价格  |    |
trade_volume  | true  |  decimal  |  成交量  |    |  
trade_turnover  |    true  |  decimal  |  成交金额  |    | 
trade_fee  |   true  |  decimal  |  成交手续费  |    |   
fee_asset | true  | string | 手续费币种 | "BTC","ETH"... | 
role  |   true  |  string  |  taker或maker  |   | 
created_at  |   true  |  long  |  创建时间  |    | 
\</list\>  |    |    |    |    |   
\</object \>  |    |     |    |    |
ts  |  true  |  long  |  时间戳  |     |


## 获取合约当前未成交委托 

###  示例

- POST `swap-api/v1/swap_openorders`  

###  请求参数

  参数名称   |  是否必须    |  类型    |  描述  |  默认值    |  取值范围  |
-------------- | -------------- | ---------- | ------------------------ | ------------ | ---------------- |
contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |
page_index   |  false  |  int  |   页码，不填默认第1页  |  1  |     |
page_size  |  false  |  int  |    |    |  不填默认20，不得多于50 |

> Response:

```json
    {
      "status": "ok",
      "data":{
        "orders":[
          {
             "symbol": "BTC",
             "contract_code": "BTC-USD",
             "volume": 111,
             "price": 1111,
             "order_price_type": "limit",
             "order_type": 1,
             "direction": "buy",
             "offset": "open",
             "lever_rate": 10,
             "order_id": 106837,
             "order_id_str": "88",
             "client_order_id": 10683,
             "order_source": "web",
             "created_at": 1408076414000,
             "trade_volume": 1,
             "trade_turnover": 1200,
             "fee": 0,
             "fee_asset": "BTC", 
             "trade_avg_price": 10,
             "margin_frozen": 10,
             "status": 1,
             "profit": 1.231
            }
           ],
        "total_page":15,
        "current_page":3,
        "total_size":3
       },
      "ts": 1490759594752
    }
```

###  返回参数

参数名称  |   是否必须  |  类型   |  描述  |   取值范围  |
-------------------------- | -------------- | ---------- | --------------------------------------------------------------- | ------------------------------------------------------ |
status  |  true  |  string  |  请求处理结果  |    |
\<list\>(属性名称: data)  |    |    |    |    |   
symbol  |  true  |  string  |  品种代码  |    |  
contract_code  |  true  |  string  |  合约代码  |  "BTC-USD" ...  |
volume  |  true  |  decimal    |  委托数量  |    |
price   |  true  |  decimal    |  委托价格  |    |   
order_price_type  |    true  |  string  |  订单报价类型 "limit":限价 "opponent":对手价 "post_only":只做maker单,post only下单只受用户持仓数量限制  |
order_type  |    true  |  int  |  订单类型，1:报单 、 2:撤单 、 3:强平、4:交割  |
direction  |  true  |  string  |  "buy":买 "sell":卖  |    |   
offset  |  true  |  string  |  "open":开 "close":平  |    |  
lever_rate  |  true  |  int  |   杠杆倍数  |   1\\5\\10\\20  |
order_id  |  true  |  long  |  订单ID  |    |
order_id_str  |  true  |  string  |  订单ID，字符串类型  |    | 
client_order_id  |  true  |  long  |  客户订单ID  |    |
created_at  |  true  |  long  |  订单创建时间  |    |
trade_volume  |   true  |  decimal    |  成交数量  |    |  
trade_turnover  | true  |  decimal    |  成交总金额  |     | 
fee  |   true  |  decimal    |  手续费  |    |
fee_asset | true  | string | 手续费币种 | "BTC","ETH"... |
trade_avg_price  |  true |  decimal    |  成交均价  |    |  
margin_frozen  |  true  |  decimal    |  冻结保证金  |    | 
profit  |  true  |  decimal   | 收益  |    |  
status  |  true  |  int  |   订单状态  |  (3未成交 4部分成交 5部分成交已撤单 6全部成交 7已撤单)  |  
order_source|   true  |  string  |  订单来源|    |
\</list\>  |    |    |    |    |
total_page  |  true  |  int  |   总页数  |    |
current_page  |   true  |  int  |   当前页  |    |
total_size  |  true  |  int  |   总条数  |    |
ts  |    true  |  long  |  时间戳  |    |


## 获取合约历史委托

###  示例

- POST `swap-api/v1/swap_hisorders` 

###  请求参数

参数名称   |  是否必须   |  类型    |  描述  |  默认值    |  取值范围  |
-------------- | -------------- | ---------- |------------------------ | ------------ | ------------------------------------------------------------------------------------------------------ |
contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |
trade_type  |   true  |  int  |   交易类型  |    0:全部,1:买入开多,2: 卖出开空,3: 买入平空,4: 卖出平多,5: 卖出强平,6: 买入强平,7:交割平多,8: 交割平空  |
type  |  true  |  int  |   类型  |  1:所有订单,2:结束状态的订单  |
status  |    true  |  string  |   订单状态  |  可查询多个状态，"3,4,5" , 0:全部,3:未成交, 4: 部分成交,5: 部分成交已撤单,6: 全部成交,7:已撤单  |
create_date |  true  |  int  |   日期  |   可随意输入正整数，如果参数超过90则默认查询90天的数据 |
page_index  |  false  |  int  |   |  页码，不填默认第1页  |  1  | 
page_size  |  false  |  int   |  每页条数，不填默认20  |  20  | 不得多于50  |

> Response:

```json
    {
      "status": "ok",
      "data":{
        "orders":[
          {
            "symbol": "BTC",
            "contract_code": "BTC-USD",
            "volume": 111,
            "price": 1111,
            "order_price_type": "1",
            "direction": "buy",
            "offset": "open",
            "lever_rate": 10,
            "order_id": 106837,
            "order_id_str": "88",
            "order_source": "web",
            "create_date": 1408076414000,
            "trade_volume": 1,
            "trade_turnover": 1200,
            "fee": 0,
            "fee_asset": "BTC", 
            "trade_avg_price": 10,
            "margin_frozen": 10,
            "profit": 10,
            "status": 1,
            "order_type": 1
          }
         ],
        "total_page":15,
        "current_page":3,
        "total_size":3
        },
      "ts": 1490759594752
    }
```

###  返回参数

参数名称  |  是否必须   |  类型    |  描述  |  取值范围  |
---------------------------- | -------------- | ---------- | --------------------------------------------- | ------------------------------------------------------ |
status  |  true  |  string  |  请求处理结果  |    |  
\<object\>(属性名称: data)  |    |    |    |    | 
\<list\>(属性名称: orders)  |    |    |    |    | 
order_id  |    true  |  long  |  订单ID  |  
order_id_str  |  true  |  string  |  订单ID，字符串类型  |    | 
symbol  |  true  |  string  |  品种代码  |
contract_code  |    true  |  string  |  合约代码  | "BTC-USD" ...  |
lever_rate  |  true  |  int  |   杠杆倍数  |  1\\5\\10\\20  |
direction  |    true  |  string  | 买卖方向 |  "buy":买 "sell":卖  |  
offset  |  true  |  string  |  开平方向  |  "open":开 "close":平  |
volume  |  true  |  decimal    |  委托数量  |    |
price  |   true  |  decimal    |  委托价格  |    | 
create_date   |  true  |  long    |  创建时间  |    | 
order_source  |  true  |  string  |  订单来源  |    | 
order_price_type  |  true  |  string  |  订单报价类型 |  1：限价单，3：对手价，4：闪电平仓，5：计划委托，6：post_only |  
margin_frozen  |    true  |  decimal    |  冻结保证金  |    |    
profit  |  true  |  decimal    |  收益  |    |
trade_volume  |  true  |  decimal    |  成交数量  |    | 
trade_turnover  |   true  |decimal    |  成交总金额  |    |    
fee  |  true  |  decimal    |  手续费  |    |   
fee_asset | true  | string | 手续费币种 | "BTC","ETH"... |
trade_avg_price  | true  |  decimal    |  成交均价  |    | 
status  |  true  |  int  |   订单状态  |    | 
order_type  |  true  |  int  |   订单类型  |  1:报单 、 2:撤单 、 3:强平、4:交割  |
\</list\>  |    |    |     |     |  
\</object\>|    |    |     |     |
total_page    |  true  |  int  |   总页数  |   |   
current_page  |  true  |  int  |   当前页  |   |   
total_size  |  true  |  int  |   总条数  |    |  
ts  |  true  |  long  |  时间戳  |    |  

## 获取历史成交记录

### 实例

- POST `swap-api/v1/swap_matchresults`

### 请求参数

 参数名称    | 是否必须 | 类型 |  描述        |  默认值 | 取值范围                             |
 ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
 contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |
 trade_type  | true     | int    | 交易类型          |         | 0:全部,1:买入开多,2: 卖出开空,3: 买入平空,4: 卖出平多,5: 卖出强平,6: 买入强平 |
 create_date | true     | int    | 日期            |         | 可随意输入正整数，如果参数超过90则默认查询90天的数据 |
 page_index  | false    | int    | 页码，不填默认第1页    | 1       |                                          |
 page_size   | false    | int    | 不填默认20，不得多于50 | 20      |                                          |

> Response: 

```json
{                                               
    "data": {                                      
 		"current_page": 1,                              
 		"total_page": 1,
 		"total_size": 2,                                
		"trades": [{
			"contract_code": "BTC-USD",
      "create_date": 1555553626736,
			"direction": "sell",
			"match_id": 3635853382,
      "id": "1232-213123-1231",
			"offset": "close",
			"offset_profitloss": 0.15646398812252696,
			"order_id": 1118,
			"order_id_str": "88",
			"symbol": "BTC",
      "order_source": "android",
			"trade_fee": -0.002897500905469032,
      "fee_asset": "BTC", 
			"trade_price": 5.522,
			"trade_turnover": 80,
			"role": "maker",
			"trade_volume": 8
		}]                                        
 	},                                                
 	"status": "ok",                                   
 	"ts": 1555654870867                               
}                                               
```

### 返回参数

 参数名称              |  是否必须 |  类型  |  描述             |  取值范围     |
 ---------------------- | -------- | ------- | ------------------ | ------------ |
 status                 | true     | string  | 请求处理结果             |              |
 \<object\>(属性名称: data) |          |         |                    |              |
 \<list\>(属性名称: trades) |          |         |                    |              |
 match_id               | true     | long    | 成交ID，不唯一，可能重复               |              |
 id               | true     | string    | 成交唯一ID               |              |
 order_id               | true     | long    | 订单ID               |              |
 order_id_str  |  true  |  string  |  订单ID，字符串类型  |    | 
 symbol                 | true     | string  | 品种代码               |              |
 order_source                 | true     | string  | 订单来源               |              |
 contract_code          | true     | string  | 合约代码               |  "BTC-USD" ...       |
 direction              | true     | string  | "buy":买 "sell":卖         |              |
 offset                 | true     | string  | "open":开 "close":平           |              |
 trade_volume           | true     | decimal | 成交数量               |              |
 trade_price                  | true     | decimal | 成交价格               |              |
 trade_turnover                  | true     | decimal | 成交总金额               |              |
 create_date            | true     | long    | 成交时间               |              |
 offset_profitloss                 | true     | decimal | 平仓盈亏                 |              |
 traded_fee                    | true     | decimal | 成交手续费                |              |
 fee_asset | true  | string | 手续费币种 | "BTC","ETH"... |
 role                   |   true    |       string  |  taker或maker  |         |
 \</list\>              |          |         |                    |              |
 total_page             | true     | int     | 总页数                |              |
 current_page           | true     | int     | 当前页                |              |
 total_size             | true     | int     | 总条数                |              |
 \</object\>            |          |         |                    |              |
 ts                     | true     | long    | 时间戳                |              |

### 备注

- 如果不传page_index和page_size，默认只查第一页的20条数据，详情请看参数说明:

## 闪电平仓下单

- POST `swap-api/v1/swap_lightning_close_position`

### 请求参数

   参数名称                |   是否必须  |   类型  |    描述            |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
 contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |
 volume | true | Number | 委托数量（张） |  |
 direction | true | String | “buy”:买，“sell”:卖 |  |
 client_order_id | false | Number | （API）客户自己填写和维护，必须保持唯一 |  |

> Response:

```json

{
  "status": "ok",
  "data": {
    "order_id": 986,
    "order_id_str": "88",
    "client_order_id": 9086
  },
  "ts": 158797866555
}

```


### 返回参数

  参数名称                |   是否必须  |  类型   |  描述            |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
status | true | string | 请求处理结果	 | "ok" :成功, "error"：失败 |
ts | true  | long | 响应生成时间点，单位：毫秒 |  |
\<data\> |  |  |  | 字典 |
order_id | true  | Number | 订单ID[用户级别的，不同的用户order_id可能相同] |  |
order_id_str  |  true  |  string  |  订单ID，字符串类型  |    | 
client_order_id | false | Number | 用户自己的订单id |  |
\</data\> |  |  |  |  |


> 错误信息：

```json

{
    "status": "error",
    "err_code": 20012,
    "err_msg": "invalid contract_code",
    "ts": 1490759594752
}

```



## 精英账户多空持仓对比-账户数

- 接口名称：精英账户多空持仓对比-账户数
- 接口URL：swap-api/v1/swap_elite_account_ratio
- 请求方式：GET
- 请求参数：
| **参数名称**                | **是否必须** | **类型**  | **描述**             | **取值范围**       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |
| period | true | string | 周期  | 5min, 15min, 30min, 60min,4hour,1day |

- 返回参数：
| **参数名称**                | **是否必须** | **类型**  | **描述**             | **取值范围**       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| status | true | string | 请求处理结果  | "ok" , "error" |
| ts | true  | long | 响应生成时间点，单位：毫秒 |  |
| <data> |  |  |  |  |
| symbol | true  | string | 品种代码 | "BTC","ETH"... |
| contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |
| <list> |  |  |  |  |
| buy_ratio | true | decimal | 净多仓的账户比例 |  |
| sell_ratio | true | decimal | 净空仓的账户比例 |  |
| locked_ratio | true | decimal | 锁仓的账户比例 |  |
| ts | true  | long | 生成时间 |  |
| </list> |  |  |  |  |
| </data> |  |  |  |  |

- 返回示例：
```
{
  "status": "ok",
  "data": [
    {
      "symbol": "BTC",
      "contract_code": "BTC-USD",
      "list": [
        {
         "buy_ratio": 0.2323,
         "sell_ratio": 0.4645,
         "locked_ratio": 0.4142,
         "ts": 158797866555
       }
       ]
    }
 ],
 "ts": 158797866555
}
```

## 精英账户多空持仓对比-持仓量

- 接口名称：精英账户多空持仓对比-持仓量
- 接口URL：swap-api/v1/swap_elite_position_ratio
- 请求方式：GET
- 请求参数：
| **参数名称**                | **是否必须** | **类型**  | **描述**             | **取值范围**       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |
| period | true | string | 周期  | 5min, 15min, 30min, 60min,4hour,1day |

- 返回参数：
| **参数名称**                | **是否必须** | **类型**  | **描述**             | **取值范围**       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| status | true | string | 请求处理结果  | "ok" , "error" |
| ts | true  | long | 响应生成时间点，单位：毫秒 |  |
| <data> |  |  |  |  |
| symbol | true  | string | 品种代码 | "BTC","ETH"... |
| contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |
| <list> |  |  |  |  |
| buy_ratio | true | decimal | 多仓的总持仓量占比 |  |
| sell_ratio | true | decimal | 空仓的总持仓量占比 |  |
| ts | true  | long | 生成时间 |  |
| </list> |  |  |  |  |
| </data> |  |  |  |  |

- 返回示例：
```
{
  "status": "ok",
  "data": [
    {
      "symbol": "BTC",
      "contract_code": "BTC-USD",
      "list": [
        {
         "buy_ratio": 0.2323,
         "sell_ratio": 0.4645,
         "ts": 158797866555
       }
       ]
    }
 ],
 "ts": 158797866555
}
```


## 获取强平订单

- 接口名称：获取强平订单
- 接口类型：公开接口
- 接口获取方式：GET
- 接口URL：swap-api/v1/swap_liquidation_orders

- 请求参数

| **参数名称**    | **是否必须** | **类型** | **描述**        | **默认值** | **取值范围**                                 |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| contract_code  |  true   |  string   |  合约代码   |    |  "BTC-USD" ... |
| trade_type      | true     | int  | 交易类型         |               |0:全部,5: 卖出强平,6: 买入强平 |
| create_date | true     | int    | 日期            |         | 7，90（7天或者90天）        |
| page_index | false     | int    | 页码,不填默认第1页            |         |         |
| page_size | false     | int    | 不填默认20，不得多于50            |         |        |

- 返回参数

| **参数名称**               | **是否必须** | **类型**  | **描述**             | **取值范围**     |
| ---------------------- | -------- | ------- | ------------------ | ------------ |
| status                 | true     | string  | 请求处理结果             |              |
| \<object\>(属性名称: data) |          |         |                    |              |
| \<list\>(属性名称: orders) |          |         |                    |              |
| symbol                 | true     | string  | 品种代码               |              |
| contract_code          | true     | string  | 合约代码               |"BTC-USD" ...  |
| direction              | true     | string  | "buy":买 "sell":卖         |              |
| offset              | true     | string  | "open":开 "close":平        |
| volume           | true     | decimal | 强平数量               |              |
| price      | true     | decimal | 破产价格               |              |
| created_at            | true     | long    | 强平时间               |              |
| \</list\>              |          |         |                    |              |
| total_page             | true     | int     | 总页数                |              |
| current_page           | true     | int     | 当前页                |              |
| total_size             | true     | int     | 总条数                |              |
| \</object\>            |          |         |                    |              |
| ts                     | true     | long    | 时间戳                |              |


- 返回示例：

```
{
  "status": "ok",
  "data":{
    "orders":[
      {
        "symbol": "BTC",
        "contract_code": "BTC-USD",     //合约代码
        "direction": "buy",
        "offset": "close",
        "volume": 111,
        "price": 1111,
        "created_at": 1408076414000,
      }
     ],
    "total_page":15,
    "current_page":3,
    "total_size":3
    },
  "ts": 1490759594752
}

```


## 查询系统状态

- 接口名称：查询系统状态
- 接口类型：公共接口
- 接口请求方式：GET
- 接口URL：swap-api/v1/swap_api_state

- 请求参数：
| **参数名称**                | **是否必须** | **类型**  | **描述**             | **取值范围**       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| contract_code   |  false  | string |  合约代码 |  "BTC-USD"... ,如果缺省，默认返回所有合约  |

- 返回参数：
| **参数名称**                | **是否必须** | **类型**  | **描述**             | **取值范围**       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| status | true | string | 请求处理结果  | "ok" , "error" |
| ts | true  | long | 响应生成时间点，单位：毫秒 |  |
| <data> |  |  |  |  |

| symbol | true  | string | 品种代码 | "BTC","ETH"... |
| contract_code  |  true   |  string   |  合约代码,"BTC-USD"  |
| open | true | int | 开仓下单权限："1"表示可用，“0”表示不可用 |  |
| close | true | int | 平仓下单权限："1"表示可用，“0”表示不可用 |  |
| cancel | true | int | 撤单权限："1"表示可用，“0”表示不可用 |  |
| transfer_in | true | int | 从币币转入的权限："1"表示可用，“0”表示不可用 |  |
| transfer_out | true | int | 转出至币币的权限："1"表示可用，“0”表示不可用 |  |

| </data|  |  |  |  |

- 返回示例

```
{
  "status": "ok",
  "data": [
    {
      "symbol": “BTC”,
      "contract_code": "BTC-USD",
      "open": 1,
      "close": 1,
      "cancel": 1,
      "transfer_in": 1,
      "transfer_out": 1,
    }
 ],
 "ts": 158797866555
}
```

- 说明
  - open，指交易权限中对应的“API-开仓-普通订单”的权限，开启为可用，关闭为不可用；
  - close，指交易权限中对应的“API-平仓-普通订单”的权限，开启为可用，关闭为不可用；
  - cancel，指交易权限中对应的“API-撤单-普通订单”的权限，开启为可用，关闭为不可用；
  - transfer_in，指交易权限中对应的“其他-划转-从币币转入”的权限，开启为可用，关闭为不可用；
  - transfer_out，指交易权限中对应的“其他-划转-转出至币币”的权限，开启为可用，关闭为不可用；



## 获取合约的资金费率

- 接口名称：获取合约的资金费率
- 接口类型：公共接口
- 接口请求方式：GET
- 接口URL：swap-api/v1/swap_funding_rate

- 请求参数：
| **参数名称**                | **是否必须** | **类型**  | **描述**             | **取值范围**       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |

- 返回参数：
| **参数名称**                | **是否必须** | **类型**  | **描述**             | **取值范围**       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| status | true | string | 请求处理结果  | "ok" , "error" |
| ts | true  | long | 响应生成时间点，单位：毫秒 |  |
| <data> |  |  |  |  |

| symbol | true  | string | 品种代码 | "BTC","ETH"... |
| contract_code  |  true   |  string   |  合约代码,"BTC-USD"  |
| fee_asset | true  | string | 资金费币种 | "BTC","ETH"... |
| funding_time | true | string | 当期资金费率时间 |  |
| funding_rate | true | string | 当期资金费率 |  |
| estimated_rate | true | string | 下一期预测资金费率 |  |
| next_funding_time  | true | string |  下一期资金费率时间    |   |

| </data|  |  |  |  |


- 返回示例

```
{
  "status": "ok",
  "data": [
    {
      "symbol": “BTC”,
      "contract_code": "BTC-USD",
      "fee_asset": "BTC", 
      "funding_time": "1577736000",
      "funding_rate": "-0.12000001",
      "estimated_rate": "-0.12000001",
      "next_funding_time": "1577764800"
    }
 ],
 "ts": 158797866555
}
```

## 获取合约的历史资金费率

- 接口名称：获取合约的历史资金费率
- 接口类型：公共接口
- 接口请求方式：GET
- 接口URL：swap-api/v1/swap_historical_funding_rate

- 请求参数：

| **参数名称**                | **是否必须** | **类型**  | **描述**             | **取值范围**       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| contract_code  |  true   |  string   |  合约代码   |  "BTC-USD" ...  |
| page_index  | false    | int    | 页码，不填默认第1页    | 1       |                                          |
| page_size   | false    | int    | 不填默认20，不得多于50 | 20      |                                          |


- 返回参数：

| **参数名称**                | **是否必须** | **类型**  | **描述**             | **取值范围**       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| status | true | string | 请求处理结果  | "ok" , "error" |
| ts | true  | long | 响应生成时间点，单位：毫秒 |  |
| <data> |  |  |  |  |

| symbol | true  | string | 品种代码 | "BTC","ETH"... |
| contract_code  |  true   |  string   |  合约代码,"BTC-USD"  |
| fee_asset | true  | string | 资金费币种 | "BTC","ETH"... |
| funding_time | true | string | 资金费率时间 |  |
| funding_rate | true | string | 当期资金费率 |  |
| realized_rate | true | string | 实际资金费率 |  |

| </data|  |  |  |  |


- 返回示例

```
{
  "status": "ok",
  "data": [
    {
      "symbol": “BTC”,
      "contract_code": "BTC-USD",
      "fee_asset": "BTC", 
      "funding_time":"1490759594752"
      "funding_rate":"-0.00010248",
      "realized_rate":"-0.00010248",
    }
 ],
 "ts": 158797866555
}
```

## 查询系统是否可用

- 接口名称：查询永续合约系统是否可用
- 接口类型：公共接口
- 接口请求方式：GET
- 请求URL：swap/heartbeat

| **参数名称**                | **是否必须** | **类型**  | **描述**             | **取值范围**       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| estimated_recovery_time | true | long | 预估恢复时间，单位：毫秒	 |  当系统状态为可用时，返回空值 |
| heartbeat | true | long | 系统是否可用	 |  1是可用，为0不可用 |

- 返回示例

```
{
	"status": "ok",
	"data": {
		"heartbeat": 1,
		"estimated_recovery_time": null
	},
	"ts": 1557714418033
}
```

市场行情接口
--------

#### 订阅 KLine 数据

成功建立和 WebSocket API 的连接之后，向 Server发送如下格式的数据来订阅数据：

    {
    "sub": "market.$contract_code.kline.$period",
    "id": "id generate by client"
    }

  |**参数名称**|   **是否必须**  | **类型**  | **描述** |  **默认值**  | **取值范围**
  |--------------| -----------------| ---------- |----------| ------------| --------------------------------------------------------------------------------|
  |contract_code  |  true   |  string   |  合约代码   |           | "BTC-USD" ...  |
  |period    |     true          | string   |  K线周期     |            |1min, 5min, 15min, 30min, 1hour,4hour,1day, 1mon|

正确订阅请求参数的例子：

    {
    "sub": "market.BTC-USD.kline.1min",
    "id": "id1"
    }

订阅成功返回数据的例子

    {
    "id": "id1",
    "status": "ok",
    "subbed": "market.BTC-USD.kline.1min",
    "ts": 1489474081631
    }

之后每当 KLine 有更新时，client 会收到数据，例子

    {
     "ch": "market.BTC-USD.kline.1min",
     "ts": 1489474082831,
     "tick": 
        {
         "id": 1489464480,
         "mrid": 268168237,
         "vol": 100,
         "count": 0,
         "open": 7962.62,
         "close": 7962.62,
         "low": 7962.62,
         "high": 7962.62,
         "amount": 0.3 //单位BTC 币种的数量
        }
    }

    tick 说明

    "tick": 
      {
       "id": K线id,
       "mrid": 268168237,
       "vol": 成交量张数,
       "count": 成交笔数,
       "open": 开盘价,
       "close": 收盘价,当K线为最晚的一根时，是最新成交价
       "low": 最低价,
       "high": 最高价,
       "amount": BTC, 即 sum(每一笔 该合约面值* 该笔的成交量/成交价)
    }

**错误订阅的列子**

错误订阅(错误的 contract_code)

    {
     "sub": "market.invalidcontract.kline.1min",
     "id": "id2"
    }

订阅失败返回数据的例子

    {
     "id": "id2",
     "status": "error",
     "err-code": "bad-request",
     "err-msg": "invalid topic market.invalidcontract.kline.1min",
     "ts": 1494301904959
    }

错误订阅(错误的 topic)

    {
     "sub": "market.BTC-USD.kline.3min",
     "id": "id3"
    }

订阅失败返回数据的例子

    {
     "id": "id3",
     "status": "error",
     "err-code": "bad-request",
     "err-msg": "invalid topic market.BTC-USD.kline.3min",
     "ts": 1494310283622
    }

#### 请求 KLine 数据 </a>

成功建立和 WebSocket API 的连接之后，向Server发送如下格式的数据来请求数据：

    {
     "req": "market.$contract_code.kline.$period",
     "id": "id generated by client",
     "from": " type: long, 2017-07-28T00:00:00+08:00 至2050-01-01T00:00:00+08:00 之间的时间点，单位：秒",
      "to": "type: long, 2017-07-28T00:00:00+08:00 至2050-01-01T00:00:00+08:00 之间的时间点，单位：秒，必须比 from 大"}

| **参数名称** | **是否必须** | **类型** | **描述** | **默认值** |**取值范围** | 
| -------- | -------- | ------ | ------ | ------- |---------------------------------------- | 
 | contract_code  |  true   |  string   |  合约代码   |           | "BTC-USD" ...  |
 | period | true | string | K线周期 | | 1min, 5min, 15min, 30min, 1hour,4hour,1day, 1mon|
 | from| true | long| 开始时间 | | |
 | to| true | long| 结束时间 | | |
    [t1, t5] 假设有 t1  ~ t5 的K线：

    from: t1, to: t5, return [t1, t5].
    from: t5, to: t1, which t5  > t1, return [].
    from: t5, return [t5].
    from: t3, return [t3, t5].
    to: t5, return [t1, t5].
    from: t which t3  < t  <t4, return [t4, t5].
    to: t which t3  < t  <t4, return [t1, t3].
    from: t1 and to: t2, should satisfy 1325347200  < t1  < t2  < 2524579200.

**备注**：一次最多2000条

请求 KLine 数据请求参数的例子：

    {
    "req": "market.BTC-USD.kline.1min",
    "id": "id4"
    }

请求成功返回数据的例子：

    {
     "rep": "market.BTC-USD.kline.1min",
     "status": "ok",
     "id": "id4",
     "tick": [
       {
        "vol": 100,
        "count": 27,
        "id": 1494478080,
        "open": 10050.00,
        "close": 10058.00,
        "low": 10050.00,
        "high": 10058.00,
        "amount": 175798.757708
       },
       {
        "vol": 300,
        "count": 28,
        "id": 1494478140,
        "open": 10058.00,
        "close": 10060.00,
        "low": 10056.00,
        "high": 10065.00,
        "amount": 158331.348600
       }
     ]
    }

#### 订阅 Market Depth 数据 </a>

成功建立和 WebSocket API 的连接之后，向 Server发送如下格式的数据来订阅数据：

    {
    "sub": "market.$contract_code.depth.$type",
    "id": "id generated by client"
    }

  |**参数名称**   |**是否必须**   |**类型**   |**描述**     |**默认值**   |**取值范围**|
  |-------------- |-------------- |---------- |------------ |------------ |---------------------------------------------------------------------------------|
  | contract_code  |  true   |  string   |  合约代码   |           | "BTC-USD" ...  |
  |type           |true           |string     |Depth 类型        |        |(150档数据)  step0, step1, step2, step3, step4, step5（合并深度1-5）,step0时，不合并深度;(20档数据)  step6, step7, step8, step9, step10, step11（合并深度7-11）；step6时，不合并深度|

**备注**：用户选择“合并深度”时，一定报价精度内的市场挂单将予以合并显示。合并深度仅改变显示方式，不改变实际成交价格。

正确订阅请求参数的例子：

    {
    "sub": "market.BTC-USD.depth.step0",
    "id": "id5"
    }

订阅成功返回数据的例子：

    {
      "id": "id5",
      "status": "ok",
      "subbed": "market.BTC-USD.depth.step0",
      "ts": 1489474081631
    }

之后每当 depth 有更新时，client 会收到数据，例子：

    {
     "ch": "market.BTC-USD.depth.step0",
     "ts": 1489474082831,
     "tick":
       { 
        "mrid": 269073229,
         "id": 1539843937,
            "bids": [
             [9999.9101,1], 
             [9992.3089,2]
                    ],
             "asks": [
              [10010.9800,10],
              [10011.3900,15]
                     ],
	      "ts": 1539843937417,
	       "version": 1539843937,
	       "ch": "market.BTC-USD.depth.step0"
        }
    }

    tick 说明：
    "tick": {
      "bids": [
        [买1价,买1量]
        [买2价,买2量]
         //more data here
       ],
       "asks": [
        [卖1价,卖1量]
        [卖2价,卖2量]
        //more data here
       ]
    }

#### 订阅 Market Detail 数据 </a>

成功建立和 WebSocket API 的连接之后，向 Server发送如下格式的数据来请求数据:

    {
     "sub": "market.$contract_code.detail",
     "id": "id generated by client"
    }

  |**参数名称**   |**是否必须**   |**类型**   |**描述**     |**默认值**   |**取值范围**|
  |-------------- |-------------- |---------- |------------ |------------ |--------------------------------------------------------------------------------|
  | contract_code  |  true   |  string   |  合约代码   |           | "BTC-USD" ...  |

订阅 Market Detail 数据请求参数的例子：

    {
     "sub": "market.BTC-USD.detail",
     "id": "id6"
    }

请求成功返回数据的例子：

    {
	"ch": "market.BTC-USD.detail",
	"ts": 1539842340724,
	"tick": {
		"id": 1539842340,
		"mrid": 268041138,
		"open": 6740.47,
		"close": 7800,
		"high": 7800,
		"low": 6726.13,
		"amount": 477.1200312075244664773339914558562673572,
		"vol": 32414,
		"count": 1716
	        }
       }

tick数据说明：

    "tick": 
         { 
           "id": id, 
           "mrid": 1494496390000, 
           "vol": 成交量(张), 
           "count": 成交笔数, 
           "open": 开盘价, 
           "close": 收盘价,当K线为最晚的一根时，是最新成交价 
           "low": 最低价, 
           "high": 最高价, 
           "amount": 成交量(币), 即 sum(每一笔成交量(张)*单张合约面值/该笔成交价)
         }

#### 请求 Trade Detail 数据

成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来请求数据：

    {
     "req": "market.$contract_code.trade.detail",
     "id": "id generated by client"
    }

仅返回当前 Trade Detail

请求 Market Detail 数据请求参数的例子：

    {
     "req": "market.BTC-USD.trade.detail",
     "id": "id8"
    }

请求成功返回数据的例子：



    {
     "ch": "market.BTC-USD.trade.detail",
     "ts": 1489474082831,
     "data": [
              {
               "id":601595424,
               "price":10195.64,
               "amount":100,
               "direction":"buy",
               "ts":1494495766000
               },
              {
              "id":601595423,
              "price":10195.64,
              "amount":200,
              "direction":"buy",
              "ts":1494495711000
              }
            ]
     }
    
tick数据说明：

    "data": [
      {
       "id": 消息ID,
       "price": 成交价,
       "amount": 成交量（张）,
       "direction": 成交方向,
       "ts": 时间戳
      }
     ]

#### 订阅 Trade Detail 数据 </a>

成功建立和 WebSocket API 的连接之后，向 Server发送如下格式的数据来订阅数据：

    {
    "sub": "market.$contract_code.trade.detail",
    "id": "id generated by client"
    }

**备注**：仅能获取最近 300 个 Trade Detail 数据。

  |**参数名称**   |**是否必须**   |**类型**   |**描述**   |**默认值**   |**取值范围**|
  |-------------- |-------------- |---------- |---------- |------------ |--------------------------------------------------------------------------------|
  | contract_code  |  true   |  string   |  合约代码   |           | "BTC-USD" ...  |

正确订阅请求参数的例子：

    {
     "sub": "market.BTC-USD.trade.detail",
     "id": "id7"
    }

订阅成功返回数据的例子：

    {
     "id": "id7",
     "status": "ok",
     "subbed": "market.BTC-USD.trade.detail",
     "ts": 1489474081631
    }

之后每当 Trade Detail 有更新时，client 会收到数据，例子：

    {
	"ch": "market.BTC-USD.trade.detail",
	"ts": 1539831709042,
	"tick": {
		"id": 265842227,
		"ts": 1539831709001,
		"data": [{
			"amount": 20,
			"ts": 1539831709001,
			"id": 265842227259096443,
			"price": 6742.25,
			"direction": "buy"
		        }]
	          }
     }

data 说明：

    "data": [
      {
       "id": 消息ID,
       "price": 成交价,
       "amount": 成交量（张）,
       "direction": 成交方向,
       "ts": 时间戳
      }
     ]



#### 订阅订单成交数据（sub）

成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来订阅数据:

#### 订阅请求数据格式

```
{
  “op”: “sub”,
  "cid": "id generated by client”,
  “topic": "topic to sub”
}
```

#### 订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                        |
| :------- | :----- | :------------------------------------------ |
| op       | string | 必填；操作名称，订阅固定值为sub             |
| cid      | string | 选填;Client 请求唯一 ID                     |
| topic    | string | 必填；订阅主题名称，详细主题列表请参考附录; |

#### 订阅请求示例

正确的订阅请求

```
{
  "op": "sub",
  "cid": "40sG903yz80oDFWr",
  "topic": "orders.BTC-USD"
}
```

订阅成功返回数据示例

```
{
  "op": "sub",
  "cid": "40sG903yz80oDFWr",
  "err-code": 0,
  "ts": 1489474081631,
  "topic": "orders.BTC-USD"
}
```

错误订阅请求示例（错误的topic）

```
{
  "op": "sub",
  "topic": "orders.bar",
  "cid": "40sG903yz80oDFWr"
}
```

订阅失败会返回下面示例数据

```
{
  "op": "sub",
  "topic": "orders.bar",
  "cid": "40sG903yz80oDFWr",
  "err-code": xxxx, //具体编码请参考响应码表 
  "err-msg": “详细的错误信息”，
  "ts": 1489474081631
}
```

#### 成交详情通知数据格式说明

```
{
"op": "notify", // 操作名称
"topic": "orders.btc", // 主题
"ts": 1489474082831, // 时间戳 
"symbol": "BTC", //品种
"contract_code": "BTC-USD", //合约代码
"volume": 111, //委托数量
"price": 1111, //委托价格 
"order_price_type": "limit", //订单报价类型 "limit":限价 "opponent":对手价 "post_only":只做maker单,post only下单只受用户持仓数量限制
"direction": "buy", //"buy":买 "sell":卖
"offset": "open", //"open":开 "close":平
"status": 6 //订单状态( 3已提交 4部分成交 5部分成交已撤单 6全部成交 7已撤单)
"lever_rate": 10, //杠杆倍数
"order_id": 106837, //订单ID
"order_id_str": "88",//订单ID，字符串类型
"client_order_id": 10683, //客户订单ID
"order_source": "web", //订单来源   （system:系统 web:用户网页 api:用户API m:用户M站 risk:风控系统）
"order_type": 1, //订单类型  (1:报单 、2:撤单 、3:强平、4:交割)
"created_at": 1408076414000, //订单创建时间
"trade_volume": 1, //累计成交数量
"trade_turnover": 1200, //累计成交总金额
"fee": 0, //手续费
"trade_avg_price": 10, //成交均价
"margin_frozen": 10, //冻结保证金
"profit": 2, //收益
"trade":[{
    "trade_id":112, //撮合结果id
    "id": "1232-213123-1231",//成交唯一ID
    "trade_volume":1, //成交量
    "trade_price":123.4555, //撮合价格
    "trade_fee":0.234, //成交手续费
    "fee_asset": "BTC", //手续费币种
    "trade_turnover":34.123, //成交金额 
    "created_at": 1490759594752, //成交创建时间
    "role": "maker" //taker或maker
  }]
}
```

#### 成交推送请求数据格式说明

| 字段名称                | 类型    | 说明                                                         |
| ----------------------- | ------- | ------------------------------------------------------------ |
| op                      | string  | 必填;操作名称，推送固定值为 notify;                          |
| topic                   | string  | 必填;推送的主题                                              |
| ts                      | long    | 服务端应答时间戳                                             |
| symbol                  | string  | 品种ID                                                       |
| contract_code           | string  | 合约代码                                                     |
| volume                  | decimal | 委托数量                                                     |
| price                   | decimal | 委托价格                                                     |
| order_price_type        | string  | 订单报价类型 "limit":限价 "opponent":对手价 "post_only":只做maker单,post only下单只受用户持仓数量限制                  |
| direction               | string  | "buy":买 "sell":卖                                           |
| offset                  | string  | "open":开 "close":平                                         |
| status                  | int     | 订单状态(1准备提交 2准备提交 3已提交 4部分成交 5部分成交已撤单 6全部成交 7已撤单 11撤单中) |
| lever_rate              | int     | 杠杆倍数                                                     |
| order_id                | long    | 订单ID                                                       |
| order_id_str            | string  | 订单ID,字符串类型                                              |
| client_order_id         | long    | 客户订单ID                                                   |
| order_source            | int     | 订单来源（system:系统 web:用户网页 api:用户API m:用户M站 risk:风控系统） |
| order_type              | int     | 订单类型  1:报单 、 2:撤单 、 3:强平、4:交割                 |
| created_at              | long    | 订单创建时间                                                 |
| trade_volume            | decimal | 成交数量                                                     |
| trade_turnover          | decimal | 成交总金额                                                   |
| fee                     | decimal | 手续费                                                       |
| trade_avg_price         | decimal | 成交均价                                                     |
| margin_frozen           | decimal | 冻结保证金                                                   |
| profit                  | decimal | 收益                                                         |
| <list>(属性名称: trade) |         |                                                              |
| trade_id                | long    | 撮合结果id 非唯一，可重复，注意：一个撮合结果代表一个taker单和N个maker单的成交记录的集合，如果一个taker单吃了N个maker单，那这N笔trade都是一样的撮合结果id                                                  |
| id                | string    | 成交唯一ID |
| trade_volume            | decimal | 成交量                                                       |
| trade_price             | decimal | 撮合价格                                                     |
| trade_fee               | decimal | 成交手续费                                                   |
| fee_asset               | string  | 手续费币种                                                    |
| trade_turnover          | decimal | 成交金额                                                     |
| created_at              | long    | 成交创建时间                                                 |
| role             | string  | taker或maker                                                 |
| </list>                  |         |                                                             |


### 取消订阅数据（unsub）

成功建⽴和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来取消订阅数据:

#### 取消订阅请求数据格式

```
{
  “op”: “unsub”,
  “topic": "topic to unsub”,
  "cid": "id generated by client”,
}
```

#### 取消订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                               |
| :------- | :----- | :------------------------------------------------- |
| op       | string | 必填;操作名称，订阅固定值为 unsub;                 |
| cid      | string | 选填;Client 请求唯一 ID                            |
| topic    | string | 必填;待取消订阅主题名称，详细主题列列表请参考附录; |

### 取消订阅请求示例

正确的取消订阅请求

```
{
  "op": "unsub",
  "topic": "orders.BTC-USD",
  "cid": "40sG903yz80oDFWr"
}
```

取消订阅成功返回数据示例

```
{
  "op": "unsub",
  "topic": "orders.BTC-USD",
  "cid": "id generated by client",
  "err-code": 0,
  "ts": 1489474081631
}
```

#### 订阅与取消订阅规则说明

| 订阅(sub)      | 取消订阅(unsub) | 规则   |
| -------------- | --------------- | ------ |
| orders.*       | orders.*        | 允许   |
| orders.contract_code1 | orders.*        | 允许   |
| orders.contract_code1 | orders.contract_code1  | 允许   |
| orders.contract_code1 | orders.contract_code2  | 不允许 |
| orders.*       | orders.contract_code1  | 不允许 |


### 资产变动数据（sub）

成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来订阅数据:

#### 订阅请求数据格式

```
{
  "op": "sub",
  "cid": "id generated by client”,
  “topic": "topic to sub”
}
```

#### 订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                        |
| :------- | :----- | :------------------------------------------ |
| op       | string | 必填；操作名称，订阅固定值为sub             |
| cid      | string | 选填;Client 请求唯一 ID                     |
| topic    | string | 必填；订阅主题名称，必填 (accounts.$contract_code)  订阅、取消订阅某个合约代码下的资产变更信息，当 $contract_code值为 * 时代表订阅所有合约代码; |

#### 订阅请求示例

正确的订阅请求

```
{
  "op": "sub",
  "cid": "40sG903yz80oDFWr",
  "topic": "accounts.BTC-USD"
}
```

订阅成功返回数据示例

```
{
  "op": "sub",
  "cid": "40sG903yz80oDFWr",
  "err-code": 0,
  "ts": 1489474081631,
  "topic": "accounts.BTC-USD"
}
```

错误订阅请求示例（错误的topic）

```
{
  "op": "sub",
  "topic": "accounts.bar",
  "cid": "40sG903yz80oDFWr"
}
```

订阅失败会返回下面示例数据

```
{
  "op": "sub",
  "topic": "accounts.bar",
  "cid": "40sG903yz80oDFWr",
  "err-code": xxxx, //具体编码请参考响应码表 
  "err-msg": “详细的错误信息”，
  "ts": 1489474081631
}
```

#### 当资产有更新时，返回的参数示例如下

```
{
    "op": “notify”,             // 操作名称
    "topic": “accounts.BTC-USD”,     // 主题
    "ts": 1489474082831,    
    "event": "order.match",
    "data":[
       {
    "symbol": "BTC",
    "contract_code": "BTC-USD",
    "margin_balance": 1,
    "margin_static": 1,
    "margin_position": 0,
    "margin_frozen": 3.33,
    "margin_available": 0.34,
    "profit_real": 3.45,
    "profit_unreal": 7.45,
    "withdraw_available":4.0989898,
    "risk_rate": 100,
    "liquidation_price": 100,
    "lever_rate": 10,
    "adjust_factor": 0.1
     }
   ]
}
```

#### 字段说明
| 字段名称                | 类型    | 说明                                                         |
| ----------------------- | ------- | ------------------------------------------------------------ |
| ts                        | long  | 响应生成时间点，单位：毫秒                           |
| event                     | string  | 资产变化通知相关事件说明，比如订单创建开仓(order.open) 、订单成交(order.match)（除开强平和结算交割）、结算交割(settlement)、订单强平成交(order.liquidation)（对钆和接管仓位）、订单撤销(order.cancel) 、合约账户划转（contract.transfer)（包括外部划转）、系统（contract.system)、其他资产变化(other)   、初始资金（init）                                              |
| symbol             | string    | 品种代码,"BTC","ETH"...                                             |
| contract_code             | string    | 合约代码 ,"BTC-USD"...，当 $contract_code值为 * 时代表订阅所有合约代码                                             |
| margin_balance            | decimal  | 账户权益                                                       |
| margin_static             | decimal  | 静态权益                                                     |
| margin_position           | decimal  | 持仓保证金（当前持有仓位所占用的保证金）                                                     |
| margin_frozen             | decimal | 冻结保证金                                                     |
| margin_available          | decimal | 可用保证金                                                     |
| profit_real               | decimal  | 已实现盈亏                |
| profit_unreal             | decimal  | 未实现盈亏                                          |
| risk_rate                 | decimal  |保证金率                                        |
| liquidation_price         | decimal     | 预估爆仓价 |
| withdraw_available        | decimal     | 可划转数量                                                     |
| lever_rate                | decimal    | 杠杆倍数                                                       |
| adjust_factor             | decimal    | 调整系数                                                       |


### 取消订阅数据（unsub）

成功建⽴和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来取消订阅数据:

#### 取消订阅请求数据格式

```
{
  “op”: “unsub”,
  “topic": "topic to unsub”,
  "cid": "id generated by client”,
}
```

#### 取消订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                               |
| :------- | :----- | :------------------------------------------------- |
| op       | string | 必填;操作名称，订阅固定值为 unsub;                 |
| cid      | string | 选填;Client 请求唯一 ID                            |
| topic    | string | 必填;必填；必填；订阅主题名称，必填 (accounts.$contract_code)  订阅、取消订阅某个合约代码下的资产变更信息，当 $contract_code值为 * 时代表订阅所有合约代码; |

### 取消订阅请求示例

正确的取消订阅请求

```
{
  "op": "unsub",
  "topic": "accounts.BTC-USD",
  "cid": "40sG903yz80oDFWr"
}
```

取消订阅成功返回数据示例

```
{
  "op": "unsub",
  "topic": "accounts.BTC-USD",
  "cid": "id generated by client",
  "err-code": 0,
  "ts": 1489474081631
}
```

#### 订阅与取消订阅规则说明

| 订阅(sub)      | 取消订阅(unsub) | 规则   |
| -------------- | --------------- | ------ |
| accounts.*       | accounts.*        | 允许   |
| accounts.contract_code1 | accounts.*        | 允许   |
| accounts.contract_code1 | accounts.contract_code1  | 允许   |
| accounts.contract_code1 | accounts.contract_code2  | 不允许 |
| accounts.*       | accounts.contract_code1  | 不允许 |


### 持仓变动更新数据（sub）

成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来订阅数据:

#### 订阅请求数据格式

```
{
  “op”: “sub”,
  "cid": "id generated by client”,
  “topic": "topic to sub”
}
```

#### 订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                        |
| :------- | :----- | :------------------------------------------ |
| op       | string | 必填；操作名称，订阅固定值为sub             |
| cid      | string | 选填;Client 请求唯一 ID                     |
| topic    | string | 必填；订阅主题名称，必填 (positions.$contract_code)  订阅、取消订阅某个合约代码下的持仓变更信息，当 $contract_code值为 * 时代表订阅所有合约代码 |

#### 订阅请求示例

正确的订阅请求

```
{
  "op": "sub",
  "cid": "40sG903yz80oDFWr",
  "topic": "positions.BTC-USD"
}
```

订阅成功返回数据示例

```
{
  "op": "sub",
  "cid": "40sG903yz80oDFWr",
  "err-code": 0,
  "ts": 1489474081631,
  "topic": "positions.BTC-USD"
}
```

错误订阅请求示例（错误的topic）

```
{
  "op": "sub",
  "topic": "positions.bar",
  "cid": "40sG903yz80oDFWr"
}
```

订阅失败会返回下面示例数据

```
{
  "op": "sub",
  "topic": "positions.bar",
  "cid": "40sG903yz80oDFWr",
  "err-code": xxxx, //具体编码请参考响应码表 
  "err-msg": “详细的错误信息”，
  "ts": 1489474081631
}
```

#### 当持仓有更新时，返回的参数示例如下

```
{ 

      “op”: “notify”,             // 操作名称
      “topic”: “positions.BTC-USD”,     // 主题
      "ts": 1489474082831,   
     "event": "order.match"
     "data":[
                   {
      "symbol": "BTC",
      "contract_code": "BTC-USD",
      "volume": 1,
      "available": 0,
      "frozen": 1,
      "cost_open": 422.78,
      "cost_hold": 422.78,
      "profit_unreal": 0.00007096,
      "profit_rate": 0.07,
      "profit": 0.97,
      "position_margin": 3.4,
      "lever_rate": 10,
      "direction":"buy"
      "last_price": 2.97,
                 }
             ]
}
```

#### 字段说明

**返回参数**

| 字段名称                | 类型    | 说明                                                         |
| ----------------------- | ------- | ------------------------------------------------------------ |
| ts                     | long  | 响应生成时间点，单位：毫秒                           |
| event                  | string  | 持仓变化通知相关事件说明，比如订单创建平仓(order.close) 、订单成交(order.match)（除开强平和结算交割）、结算交割(settlement)、订单强平成交(order.liquidation)（对钆和接管仓位）、订单撤销(order.cancel)  、初始持仓（init）                                             |
| symbol                 | string    | 品种代码 ,"BTC","ETH"...                                             |
| contract_code          | decimal  | 合约代码，"BTC-USD"                                                       |
| volume                 | decimal  | 持仓量                                                     |
| available              | decimal | 可平仓数量                                                     |
| frozen                 | decimal | 冻结数量                                                      |
| cost_open              | decimal  | 开仓均价                |
| cost_hold              | decimal  | 持仓均价                                          |
| profit_unreal          | decimal  |未实现盈亏                                        |
| profit_rate            | decimal     | 收益率 |
| profit                 | decimal     | 收益                                                     |
| position_margin        | decimal    | 持仓保证金                                                       |
| lever_rate             | decimal     | 杠杆倍数                                                      |
| direction              | decimal    | 仓位方向   "buy":买 "sell":卖                                                     |
| last_price             | decimal    | 最新价                                                       |


### 取消订阅数据（unsub）

成功建⽴和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来取消订阅数据:

#### 取消订阅请求数据格式

```
{
  “op”: “unsub”,
  “topic": "topic to unsub”,
  "cid": "id generated by client”,
}
```

#### 取消订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                               |
| :------- | :----- | :------------------------------------------------- |
| op       | string | 必填;操作名称，订阅固定值为 unsub;                 |
| cid      | string | 选填;Client 请求唯一 ID                            |
| topic    | string | 必填;必填；必填；订阅主题名称，必填 (positions.$contract_code)  订阅、取消订阅某个合约代码下的资产变更信息，当 $contract_code值为 * 时代表订阅所有合约代码; |

### 取消订阅请求示例

正确的取消订阅请求

```
{
  "op": "unsub",
  "topic": "positions.BTC-USD",
  "cid": "40sG903yz80oDFWr"
}
```

取消订阅成功返回数据示例

```
{
  "op": "unsub",
  "topic": "positions.BTC-USD",
  "cid": "id generated by client",
  "err-code": 0,
  "ts": 1489474081631
}
```

#### 订阅与取消订阅规则说明

| 订阅(sub)      | 取消订阅(unsub) | 规则   |
| -------------- | --------------- | ------ |
| positions.*       | positions.*        | 允许   |
| positions.contract_code1 | positions.*        | 允许   |
| positions.contract_code1 | positions.contract_code1  | 允许   |
| positions.contract_code1 | positions.contract_code2  | 不允许 |
| positions.*       | positions.contract_code1  | 不允许 |



## 获取强平订单

1、成功建立和 WebSocket API 的连接之后，订阅请求的数据中需包含
（1）op 操作名称，必填 （类型和火币一致，订阅为sub，取消订阅为unsub）   ；
（2）client ID，选填 (Client请求唯一ID)   ；
（3）主题，必填 (liquidationOrders.$contract_code)  订阅、取消订阅某个合约代码下的订单变更信息，当 $contract_code值为 * 时代表订阅所有合约代码；

2、当有订单被爆仓账户接管后，返回的参数示例如下：

```
{
    “op”: “notify”,             // 操作名称
    “topic”: “liquidationOrders.BTC-USD”,     // 主题
    "ts": 1489474082831,    
    "symbol": "BTC",
    "contract_code": "BTC-USD",     //合约代码
    "direction": "buy",
    "offset": "close",
    "volume": 111,
    "price": 1111,
    "created_at": 1408076414000,
}
```


### 资金费率变动数据（sub）

成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来订阅数据:

#### 订阅请求示例

正确的订阅请求

```
{
  "op": "sub",
  "cid": "40sG903yz80oDFWr",
  "topic": "funding_rate.BTC-USD"
}
```

订阅成功返回数据示例

```
{
  "op": "sub",
  "cid": "40sG903yz80oDFWr",
  "err-code": 0,
  "ts": 1489474081631,
  "topic": "funding_rate.BTC-USD"
}
```

错误订阅请求示例（错误的topic）

```
{
  "op": "sub",
  "topic": "funding_rate.bar",
  "cid": "40sG903yz80oDFWr"
}
```

订阅失败会返回下面示例数据

```
{
  "op": "sub",
  "topic": "funding_rate.bar",
  "cid": "40sG903yz80oDFWr",
  "err-code": xxxx, //具体编码请参考响应码表 
  "err-msg": “详细的错误信息”，
  "ts": 1489474081631
}
```

#### 当资金费率有更新时，返回的参数示例如下

```
{ 
      “op”: “notify”,             // 操作名称
      “topic”: “funding_rate.BTC-USD”,     // 主题
      "ts": 1489474082831,   
      "data": [
        {
          "symbol": “BTC”,
          "contract_code": "BTC-USD",
          "fee_asset": "BTC", 
          "funding_time": "1490759594752",
          "funding_rate": "-0.12000001",
          "estimated_rate": "-0.12000001",
          "settlement_time": "1490759594752"
        }
      ]
}
```

#### 字段说明

**返回参数**

| 字段名称                | 类型    | 说明                                                         |
| ----------------------- | ------- | ------------------------------------------------------------ |
| ts                     | long  | 响应生成时间点，单位：毫秒                           |
| symbol |string | 品种代码,"BTC","ETH"... |
| contract_code  | string   |  合约代码,"BTC-USD"  |
| fee_asset | string | 资金费币种,"BTC","ETH"... |
| funding_time | string | 当期资金费率时间 |
| funding_rate | string | 当期资金费率 |
| estimated_rate | string | 下一期预测资金费率 |
| settlement_time | string |  结算时间,如"1490759594752"  |


### 取消订阅数据（unsub）

成功建⽴和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来取消订阅数据:

#### 取消订阅请求数据格式

```
{
  “op”: “unsub”,
  “topic": "topic to unsub”,
  "cid": "id generated by client”,
}
```

#### 取消订阅请求数据格式说明

| 字段名称 | 类型   | 说明                                               |
| :------- | :----- | :------------------------------------------------- |
| op       | string | 必填;操作名称，订阅固定值为 unsub;                 |
| cid      | string | 选填;Client 请求唯一 ID                            |
| topic    | string | 必填;必填；必填；订阅主题名称，必填 (funding_rate.$contract_code)  订阅、取消订阅某个合约代码下的资产变更信息，当 $contract_code值为 * 时代表订阅所有合约代码; |

### 取消订阅请求示例

正确的取消订阅请求

```
{
  "op": "unsub",
  "topic": "funding_rate.BTC-USD",
  "cid": "40sG903yz80oDFWr"
}
```

取消订阅成功返回数据示例

```
{
  "op": "unsub",
  "topic": "funding_rate.BTC-USD",
  "cid": "id generated by client",
  "err-code": 0,
  "ts": 1489474081631
}
```

#### 订阅与取消订阅规则说明

| 订阅(sub)      | 取消订阅(unsub) | 规则   |
| -------------- | --------------- | ------ |
| funding_rate.*       | funding_rate.*        | 允许   |
| funding_rate.contract_code1 | funding_rate.*        | 允许   |
| funding_rate.contract_code1 | funding_rate.contract_code1  | 允许   |
| funding_rate.contract_code1 | funding_rate.contract_code2  | 不允许 |
| funding_rate.*       | funding_rate.contract_code1  | 不允许 |
