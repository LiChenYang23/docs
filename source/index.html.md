---
title: 火币 API 文档

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://www.hbg.com/zh-cn/apikey/'>创建 API Key </a>
includes:

search: False
---

# 简介

## API 简介

欢迎使用火币合约 API！ 你可以使用此 API 获得市场行情数据，进行交易，并且管理你的账户。

在文档的右侧是代码示例，目前我们仅提供针对 `shell` 的代码示例。

你可以通过选择上方下拉菜单的版本号来切换文档对应的 API 版本，也可以通过点击右上方的语言按钮来切换文档语言。


## 做市商项目

<aside class="notice">
做市商项目不支持点卡抵扣、VIP、交易量相关活动以及任何形式的返佣活动。
</aside>

欢迎有优秀 maker 策略且交易量大的用户参与长期做市商项目。如果您的火币现货账户或者合约账户中有折合大于3BTC资产（币币和合约账户分开统计），请提供以下信息发送邮件至：

- [MM_service@huobi.com](mailto:MM_service@huobi.com) Huobi Global（现货 / 杠杆）做市商申请；
- [dm_mm@huobi.com](mailto:dm_mm@huobi.com) HBDM（合约）做市商申请。


1. 提供 UID （需不存在返佣关系的 UID）；
2. 提供其他交易平台 maker 交易量截图证明（比如30天内成交量，或者 VIP 等级等）；
3. 请简要阐述做市方法，不需要细节。

# 更新日志

## 1.0.8【更新:增加order_id_str字段】

- 为了解决nodejs和Javascript的用户order_id返回是18位数字长度过长的问题,接口返回增加order_id_str字段，类型为字符串，来表示订单号。

涉及接口:

    api/v1/contract_order
    
    api/v1/contract_batchorder
    
    api/v1/contract_matchresults
    
    api/v1/contract_hisorders
    
    api/v1/contract_openorders
    
    api/v1/lightning_close_position 
    
    api/v1/contract_order_info
    
- 订单推送ws  增加 order_id_str

## 1.0.7

<aside class="warning">
nodejs和Javascript的用户请特别注意：order_id返回是18位，nodejs和javascript默认解析18位有问题，nodejs和javascript里面JSON.parse默认是int，大于等于18位的数字用json-bigint的包解析。
具体参考nodejs的demo，点击<a href='https://github.com/huobiapi/Futures-Node.js-demo/tree/master/REST-Node.js-demo'>查看</a>。
详细说明，请点击<a href='https://github.com/huobiapi/Futures-Node.js-demo/blob/master/Nodejs%20%E5%90%88%E7%BA%A6%20DEMO%E4%BF%AE%E6%94%B9.docx?raw=true'>下载</a>
</aside>

### 1、修改获取订单明细信息

  rest接口api/v1/contract_order_detail请求参数“ created_at”改为选填

### 2、修改接口获取用户账户信息

  rest接口api/v1/contract_account_info增加返回字段‘ margin_static’，表示用户的静态权益

### 3、修改获取订单明细信息

  rest接口api/v1/contract_order_detail、查询用户的成交记录

  rest接口api/v1/contract_matchresults、用户订单的成交推送的ws增加字段id,表示成交唯一ID

### 4、修改下单

  rest接口api/v1/contract_order和批量下单

  rest接口api/v1/contract_batchorder

  请求参数order_price_type中增加订单价格类型“ioc”(ioc:立即成交并取消剩余);

  请求参数order_price_type中增加订单价格类型“fok”(fok:全部成交或立即取消);

### 5、修改查询用户当前的下单量限制

  rest接口api/v1/contract_order_limit返回参数的“ order_price_type”，表示订单报价类型，

  增加"fok":FOK订单(fok:全部成交或立即取消)，"ioc":IOC订单(ioc:立即成交并取消剩余)

### 6、新增查询系统状态的API

  rest接口api/v1/contract_api_state

### 7、新增账户多空持仓对比-账户数

  rest接口api/v1/contract_elite_account_ratio

### 8、新增精英账户多空持仓对比-持仓量 

  rest接口api/v1/contract_elite_position_ratio

### 9、新增获取强平订单

  rest接口api/v1/contract_liquidation_orders和ws推送


## 1.0.6【更新:新增rest接口】

### 新增rest接口：

  请求访问地址：https://www.hbdm.com/heartbeat
  
  备注：查询系统是否可用，其中heartbeat为1是可用，为0不可用。
  
## 1.0.5【更新:查询及下单功能】

### 新增接口：

  新增rest接口,查询用户的下单量限制；
  
  新增rest接口,查询用户的手续费费率；
  
  新增rest接口,查询用户的划转限制；
  
  新增rest接口,查询用户的持仓量限制；
  
  新增rest接口,查询平台的风险准备金、预估分摊比例；
  
  新增rest接口,查询平台持仓量；
  
  新增rest接口,查询平台的风险准备金历史数据；
  
  新增rest接口,查询平台的阶梯调整系数；
  
  新增rest接口,闪电平仓下单；

### 对已有接口的修改：

  rest接口，查询用户账户信息接口增加返回用户的调整系数；
  
  rest接口，查询单个子账户资产信息接口增加返回用户的调整系数；

  ws接口，资金推送增加返回用户的调整系数；
  
  rest接口，下单接口和批量下单接口新增最优5、10、20档下单；
  
  rest接口，获取成交记录增加按照合约code查询；

## 1.0.4【更新: Restful查询接口】

### 1.查询母账户下所有子账户资产信息

  URL：api/v1/contract_sub_account_list
  
  备注：只返回已经开通合约交易的子账户数据

### 2.查询单个子账户资产信息

  URL：api/v1/contract_sub_account_info
  
  备注：只能查询到开通合约交易的子账户信息；子账户来过合约系统但是未开通合约交易也不返回对应的数据

### 3.查询单个子账户持仓信息的

  URL：api/v1/contract_sub_position_info

### 4.查询用户财务记录

  URL：api/v1/contract_financial_record
 

## 1.0.3【更新：WS增加资产信息推送】

WS增加资产信息推送 

WS增加持仓信息推送 

rest接口获取用户的持仓信息接口api/v1/contract_position_info增加返回字段“最新价”
 

## 1.0.2【更新:  币币账户和合约账户间进行资金的划转】

### 新增账户接口/v1/futures/transfer 

  币币账户和合约账户间进行资金的划转
  
  从现货现货账户转至合约账户，类型为pro-to-futures; 从合约账户转至现货账户，类型为futures-to-pro
  
  该接口的访问频次的限制为1分钟10次

### API限频

  限频时间间隔从1秒变为3秒
  
  私有接口限频由原来的10次/s变更为30次/3s，即请求发送3秒内不超过30次
  
  其他非行情类的公开接口限频由原来的20次/s变更为60次/3s，即请求发送3秒内不超过60次
 

## 1.0.1【更新：post_only高级限价委托功能上线】

### 全部撤单接口/v1/contract_cancelall

  只传symbol，撤销该品种下所有周期的合约
  
  只要有contract_code，则撤销该code的合约
  
  只传symbol+contract_type， 则撤销二者拼接所成的合约订单

### 下单接口/v1/ contract_order

  报单字段order_price_type中增加订单价格类型post_only，post_only是“只做Maker（post_only）”，不会立刻在市场成交，保证用户始终为Maker；如果委托会立即与已有委托成交，那么该委托会被取消。
  
  Post only只受用户持仓数量限制，单笔下单不受下单数量限制。

### 批量下单接口/v1/ contract_batchorder

  报单字段order_price_type中增加订单价格类型post_only，post_only是“只做Maker（post_only）”，不会立刻在市场成交，保证用户始终为Maker；如果委托会立即与已有委托成交，那么该委托会被取消。
  
  Post only只受用户持仓数量限制，单笔下单不受下单数量限制。

### 所有API接口返回数据中增加限频信息

  将在api接口response中的header返回以下字段
  
  ratelimit-limit： 单轮请求数上限，单位：次数
  
  ratelimit-interval：请求数重置的时间间隔，单位：毫秒
  
  ratelimit-remaining：本轮剩余可用请求数，单位：次数
  
  ratelimit-reset：请求数上限重置时间，单位：毫秒

### 查询订单详细信息/v1/contract_order_detail

  trades增加成交角色字段role：taker或maker
  
  获取成交记录/v1/contract_matchresults
  
  trades增加成交角色字段role：taker或maker
  
  获取该用户在某品种上的最新成交记录，可以按照交易类型进行过滤筛选。注意，该接口是需要API KEY验签的私有接口，只能查询属于该用户自己的最新成交记录。

### WS成交推送接口

  trades增加成交角色字段role：taker或maker
  
  WebSocket私有订单成交推送接口(需要API KEY验签)
  
  一个UID最多同时建立10个私有订单成交推送WS链接。该用户在一个品种(包含该品种的所有周期的合约)上，仅需要维持一个订单推送WS链接即可。
  
  注意: 订单推送WS的限频，跟用户RESTFUL私有接口的限频是分开的，相互不影响。
 

## 1.0.0 于2018年12月10日上线

# 合约交易接入说明

## 合约交易接口列表

### 接口列表

  权限类型  |    接口数据类型   |   请求方法      |          类型  |   描述                     |   需要验签  |
----------- |  ------------------ | ---------------------------------------- |  ---------- |  ------------------------------- |  --------------  |
读取     |  基础信息接口           |  api/v1/contract_contract_info  |                 GET        |  获取合约信息                 |  否  |
读取     |  基础信息接口           |  api/v1/contract_index  |                         GET        |  获取合约指数信息             |  否  |
读取     |  基础信息接口           |  api /v1/contract_price_limit  |                 GET         |  获取合约最高限价和最低限价   |  否  |
读取     |  基础信息接口           |   api/v1/contract_open_interest  |                  GET        |  获取当前可用合约总持仓量     |  否  |
读取     |  基础信息接口           |   api/v1/contract_delivery_price  |                  GET        |  获取预估交割价    |  否  |
读取     |  基础信息接口           |   https://www.hbdm.com/heartbeat   |                  GET        |  查询系统是否可用    |  否  |
读取     |  基础信息接口           |   api/v1/contract_api_state   |                  GET        |  查询系统状态    |  否  |
读取  |  市场行情接口           | /market/depth |                                GET        |  获取行情深度数据            |  否  |
读取     |  市场行情接口          |  /market/history/kline |                        GET        |  获取K线数据                  |  否  |
读取     |  市场行情接口          |   /market/detail/merged |                     GET        |  获取聚合行情                 |  否  |
读取     |  市场行情接口           |   /market/trade |                                GET        |  获取市场最近成交记录         |  否  |
读取     |  市场行情接口           |  /market/history/trade |                         GET        |  批量获取最近的交易记录       |  否  |
读取     |  市场行情接口           |  api/v1/contract_risk_info |    GET       |  查询合约风险准备金余额和预估分摊比例            |  否  |
读取     |  市场行情接口           |  api/v1/contract_insurance_fund |  GET       |  查询合约风险准备金余额历史数据            |  否  |
读取     |  市场行情接口           |  api/v1/contract_adjustfactor |   GET       |  查询平台阶梯调整系数            |  否  |
读取     |  市场行情接口           |  api/v1/contract_his_open_interest |   GET       |  平台持仓量的查询            |  否  |
读取     |  市场行情接口           |  api/v1/contract_elite_account_ratio |   GET       |  精英账户多空持仓对比-账户数            |  否  |
读取     |  市场行情接口           |  api/v1/contract_elite_position_ratio |   GET       |  精英账户多空持仓对比-持仓量            |  否  |
读取     |  市场行情接口           |  api/v1/api/v1/contract_liquidation_orders |   GET       |  获取强平订单            |  否  |
读取     |  资产接口           |   api/v1/contract_account_info |               POST        |  获取用户账户信息              |  是  | 
读取  |  资产接口              |  api/v1/contract_position_info |                POST       |  获取用户持仓信息              |  是  |
读取     | 账户接口           | api/v1/contract_sub_account_list  |      POST       |  币查询母账户下所有子账户资产信息         | 是 |
读取     | 账户接口           | api/v1/contract_sub_account_info |       POST       |  查询单个子账户资产信息            | 是 |
读取     | 账户接口           | api/v1/contract_sub_position_info |     POST       |  查询单个子账户持仓信息的            | 是 |
读取     | 账户接口           | api/v1/contract_financial_record |   POST       | 查询用户财务记录                    |  是  |
读取     |  账户接口           |  api/v1/contract_order_limit |  POST       |  查询用户当前的下单量限制            |  是  |
读取     |  账户接口           |  api/v1/contract_fee |  POST       |  查询用户当前的手续费费率            |  是  |
读取     |  账户接口           |  api/v1/contract_transfer_limit |  POST       |  查询用户当前的划转限制            |  是  |
读取     |  账户接口           |  api/v1/contract_position_limit |   POST       |  用户持仓量限制的查询            |  是  |
交易     |  交易接口           |  api/v1/contract_order |                        POST       |  合约下单                      |  是  |
交易     |  交易接口           |  api/v1/contract_batchorder |                    POST       |  合约批量下单                  |  是  |
交易     |  交易接口           |  api/v1/contract_cancel |                        POST       |  撤销订单                     |  是  |
交易     |  交易接口           |  api/v1/contract_cancelall |                     POST       |  全部撤单                     |  是  |
读取     |  交易接口          |  api/v1/contract_order_info |                   POST       |  获取合约订单信息             |  是  |
读取    |  交易接口           |   api/v1/contract_order_detail |               POST        |  获取订单明细信息             |  是  |
读取     |  交易接口           |   api/v1/contract_openorders |                   POST       |  获取合约当前未成交委托       |  是  |
读取     |  交易接口           |  api/v1/contract_hisorders |                    POST        |  获取合约历史委托             |  是  |
读取     |  交易接口           |  api/v1/contract_matchresults |                    POST       |  获取历史成交记录            |  是  |
交易     |  账户接口           |  v1/futures/transfer |                    POST       |  币币账户和合约账户间进行资金的划转            |  是  |
交易     |  账户接口           |  api/v1/lightning_close_position |    POST       |  闪电平仓下单            |  是  |

## 访问地址

访问地址 | 适用站点 | 适用功能 | 适用交易对 |
------ | ---- | ---- | ------ |
https://api.hbdm.com| 火币合约|   行情     | 火币合约的交易品种  |

### 备注

"https://api.hbdm.com"如果无法访问请使用："https://api.btcgateway.pro"。

## 签名认证

### 签名说明

API 请求在通过 internet 传输的过程中极有可能被篡改，为了确保请求未被更改，除公共接口（基础信息，行情数据）外的私有接口均必须使用您的 API Key 做签名认证，以校验参数或参数值在传输途中是否发生了更改。

一个合法的请求由以下几部分组成：

- 方法请求地址：即访问服务器地址 api.hbdm.com，比如 api.hbdm.com/api/v1/contract_order。

- API 访问密钥（AccessKeyId）：您申请的 API Key 中的 Access Key。

- 签名方法（SignatureMethod）：用户计算签名的基于哈希的协议，此处使用 HmacSHA256。

- 签名版本（SignatureVersion）：签名协议的版本，此处使用2。

- 时间戳（Timestamp）：您发出请求的时间 (UTC 时区) (UTC 时区) (UTC 时区) 。如：2017-05-11T16:22:06。在查询请求中包含此值有助于防止第三方截取您的请求。

- 必选和可选参数：每个方法都有一组用于定义 API 调用的必需参数和可选参数。可以在每个方法的说明中查看这些参数及其含义。 请一定注意：对于 GET 请求，每个方法自带的参数都需要进行签名运算； 对于 POST 请求，每个方法自带的参数不进行签名认证，即 POST 请求中需要进行签名运算的只有 AccessKeyId、SignatureMethod、SignatureVersion、Timestamp 四个参数，其它参数放在 body 中。

- 签名：签名计算得出的值，用于确保签名有效和未被篡改。


### 创建 API Key

您可以在 <a href='https://www.hbg.com/zh-cn/apikey/'>这里 </a> 创建 API Key。

API Key 包括以下两部分

- `Access Key`  API 访问密钥
  
- `Secret Key`  签名认证加密所使用的密钥（仅申请时可见）

<aside class="notice">
创建 API Key 时可以选择绑定 IP 地址，未绑定 IP 地址的 API Key 有效期为90天。
</aside>
<aside class="notice">
API Key 具有包括交易、借贷和充提币等所有操作权限。
</aside>
<aside class="warning">
这两个密钥与账号安全紧密相关，无论何时都请勿向其它人透露。
</aside>


### 签名步骤

规范要计算签名的请求 因为使用 HMAC 进行签名计算时，使用不同内容计算得到的结果会完全不同。所以在进行签名计算前，请先对请求进行规范化处理。下面以查询某订单详情请求为例进行说明：

查询某订单详情

`https://api.hbdm.com/api/v1/contract_order?`

`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`&SignatureMethod=HmacSHA256`

`&SignatureVersion=2`

`&Timestamp=2017-05-11T15:19:30`

#### 1. 请求方法（GET 或 POST），后面添加换行符 “\n”


`GET\n`

#### 2. 添加小写的访问地址，后面添加换行符 “\n”

`
api.hbdm.com\n
`

#### 3. 访问方法的路径，后面添加换行符 “\n”

`
/api/v1/contract_order\n
`

#### 4. 按照ASCII码的顺序对参数名进行排序。例如，下面是请求参数的原始顺序，进行过编码后


`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`SignatureMethod=HmacSHA256`

`SignatureVersion=2`

`Timestamp=2017-05-11T15%3A19%3A30`

<aside class="notice">
使用 UTF-8 编码，且进行了 URI 编码，十六进制字符必须大写，如 “:” 会被编码为 “%3A” ，空格被编码为 “%20”。
</aside>
<aside class="notice">
时间戳（Timestamp）需要以YYYY-MM-DDThh:mm:ss格式添加并且进行 URI 编码。
</aside>


#### 5. 经过排序之后

`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`SignatureMethod=HmacSHA256`

`SignatureVersion=2`

`Timestamp=2017-05-11T15%3A19%3A30`

#### 6. 按照以上顺序，将各参数使用字符 “&” 连接


`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30`

#### 7. 组成最终的要进行签名计算的字符串如下

`POST\n`

`api.hbdm.com\n`

`/api/v1/contract_order\n`

`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30`


#### 8. 用上一步里生成的 “请求字符串” 和你的密钥 (Secret Key) 生成一个数字签名

`4F65x5A2bLyMWVQj3Aqp+B4w+ivaA7n5Oi2SuYtCJ9o=`

1. 将上一步得到的请求字符串和 API 私钥作为两个参数，调用HmacSHA256哈希函数来获得哈希值。

2. 将此哈希值用base-64编码，得到的值作为此次接口调用的数字签名。

#### 9. 将生成的数字签名加入到请求的路径参数里

最终，发送到服务器的 API 请求应该为

`https://api.hbdm.com/api/v1/contract_order?AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30&Signature=4F65x5A2bLyMWVQj3Aqp%2BB4w%2BivaA7n5Oi2SuYtCJ9o%3D`

1. 把所有必须的认证参数添加到接口调用的路径参数里

2. 把数字签名在URL编码后加入到路径参数里，参数名为“Signature”。

## 访问次数限制

* 公开行情接口和用户私有接口都有访问次数限制

* 普通用户，需要密钥的私有接口，每个UID 3秒最多30次请求(该UID的所有币种和不同到期日的合约的所有私有接口共享3秒30次的额度)

* 其他非行情类的公开接口，比如获取指数信息，限价信息，交割结算、平台持仓信息等，所有用户都是每个IP3秒最多60次请求（所有该IP的非行情类的公开接口请求共享3秒60次的额度）

- 行情类的公开接口，比如：获取K线数据、获取聚合行情、市场行情、获取市场最近成交记录：

    （1） restful接口：同一个IP,  1秒最多200个请求 

    （2）  websocket：req请求，同一时刻最多请求50次；sub请求，无限制，服务器主动推送数据
    
- WebSocket私有订单成交推送接口(需要API KEY验签)

     一个UID最多同时建立10个私有订单成交推送WS链接。该用户在一个品种(包含该品种的所有周期的合约)上，仅需要维持一个订单推送WS链接即可。
   
     注意: 订单推送WS的限频，跟用户RESTFUL私有接口的限频是分开的，相互不影响。
     

- 所有API接口返回数据中增加限频信息

  将在api接口response中的header返回以下字段：
  
  ratelimit-limit： 单轮请求数上限，单位：次数
  
  ratelimit-interval：请求数重置的时间间隔，单位：毫秒
  
  ratelimit-remaining：本轮剩余可用请求数，单位：次数
  
  ratelimit-reset：请求数上限重置时间，单位：毫秒

## 查询系统是否可用

通过接口`https://www.hbdm.com/heartbeat`，可以查询系统是否可用,其中heartbeat为1是可用，为0不可用。

> 返回数据

```json
  {
  "status": "ok",
  "data": {"heartbeat": 1},
  "ts": 1557714418033,
  }

```
 


## 错误码详情

错误代码	 | 错误描述|
----- | ---------------------- |
403	|	无效身份                |
1000|	系统异常                |
1001|	系统未准备就绪             |
1002|	查询异常                |
1003|	操作redis异常           |
1010|	用户不存在               |
1011|	用户会话不存在             |
1012|	用户账户不存在             |
1013|	合约品种不存在             |
1014|	合约不存在               |
1015|	指数价格不存在             |
1016|	对手价不存在              |
1017|	查询订单不存在             |
1030|	输入错误                |
1031|	非法的报单来源             |
1032|	访问次数超出限制            |
1033|	合约周期字段值错误           |
1034|	报单价格类型字段值错误         |
1035|	报单方向字段值错误           |
1036|	报单开平字段值错误           |
1037|	杠杆倍数不符合要求           |
1038|	报单价格不符合最小变动价        |
1039|	报单价格超出限制            |
1040|	报单数量不合法             |
1041|	报单数量超出限制            |
1042|	超出多头持仓限制            |
1043|	超出多头持仓限制            |
1044|	超出平台持仓限制            |
1045|	杠杆倍数与所持有仓位的杠杆不符合    |
1046|	持仓未初始化              |
1047|	可用保证金不足             |
1048|	持仓量不足               |
1050|	客户报单号重复             |
1051|	没有可撤订单              |
1052|	超出批量数目限制            |
1053|	无法获取合约的最新价格区间       |
1054|	无法获取合约的最新价          |
1055|	平仓时权益不足             |
1056|	结算中无法下单和撤单          |
1057|	暂停交易中无法下单和撤单        |
1058|	停牌中无法下单和撤单          |
1059|	交割中无法下单和撤单          |
1060|	此合约在非交易状态中，无法下单和撤单  |
1061|	订单不存在，无法撤单          |
1062|	撤单中，无法重复撤单          |
1063|	订单已成交，无法撤单          |
1064|	报单主键冲突              |
1065|	客户报单号不是整数           |
1066|	字段不能为空              |
1067|	字段不合法               |
1068|	导出错误                |
1069|	报单价格不合法             |
1100|	用户没有开仓权限            |
1101|	用户没有平仓权限            |
1102|	用户没有入金权限            |
1103|	用户没有出金权限            |
1104|	合约交易权限,当前禁止交易       |
1105|	合约交易权限,当前只能平仓       |
1200|	登录错误                |
1220|	用户尚未开通合约交易          |
1221|	开户资金不足              |
1222|	开户天数不足              |
1223|	开户VIP等级不足           |
1224|	开户国家限制              |
1225|	开户不成功               |
1250|	无法获取HT_token        |
1251|	BTC折合资产无法获取         |
1252|	现货资产无法获取            |
1071|	订单已撤，无法撤单    |
1077|	交割结算中，当前品种资金查询失败    |
1078|	交割结算中，部分品种资金查询失败    |
1079|	交割结算中，当前品种持仓查询失败    |
1080|	交割结算中，部分品种持仓查询失败    |
1083|	账号异常，暂时无法平仓    |

## 代码实例

**REST**

- <a href='https://github.com/huobiapi/Futures-Java-demo'>Java</a>

- <a href='https://github.com/huobiapi/Futures-Python-demo'>Python</a>

- <a href='https://github.com/huobiapi/Futures-Go-demo'>Golang</a>

- <a href='https://github.com/huobiapi/Futures-CSharp-demo'>CSharp</a>

- <a href='https://github.com/huobiapi/Futures-PHP-demo'>PHP</a>

- <a href='https://github.com/huobiapi/Futures-Node.js-demo'>Node.js</a>

- <a href='https://github.com/huobiapi/Futures-Yi-demo'>易语言</a>
  
**Websocket**

- <a href='https://github.com/huobiapi/Futures-Java-demo/tree/master/WebSocket-JAVA-demo'>Java</a>

- <a href='https://github.com/huobiapi/Futures-Python-demo/tree/master/Websocket-Python3-demo'>Python</a>

- <a href='https://github.com/huobiapi/Futures-Node.js-demo/tree/master/WebSocket-Node.js-demo'>Node.js</a>


# 合约市场行情接口

## 获取合约信息 

###  示例
      
- GET `api/v1/contract_contract_info`

```shell
curl "https://api.hbdm.com/api/v1/contract_contract_info"
```

###  请求参数

参数名称     |  参数类型   |  必填   |  描述  |
---------------- |  -------------- |  ---------- |  ------------------------------------------------------------|
symbol           |  string         |  false|      "BTC","ETH"...  |
contract_type   |  string         |  false|      合约类型: （this_week:当周 next_week:下周 quarter:季度） |
contract_code   |  string         |  false|      BTC180914  |

### 备注： 

如果不填，默认查询所有所有合约信息;
如果contract_code填了值，那就按照contract_code去查询;
如果contract_code没有填值，则按照symbol+contract_type去查询;

>Response:

```json
    {
      "status": "ok",
      "data": [
        {
          "symbol": "BTC",
          "contract_code": "BTC180914",
          "contract_type": "this_week",
          "contract_size": 100,
          "price_tick": 0.001,
          "delivery_date": "20180704",
          "create_date": "20180604",
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
contract_code             |  true           |  string     |  合约代码                          |  "BTC180914" ...  |
contract_type             |  true           |  string     |  合约类型                          |  当周:"this_week", 次周:"next_week", 季度:"quarter"  |
contract_size             |  true           |  decimal    |  合约面值，即1张合约对应多少美元   |  10, 100...  |
price_tick                |  true           |  decimal    |  合约价格最小变动精度             |  0.001, 0.01...  |
delivery_date             |  true           |  string     |  合约交割日期                     |  如"20180720"  |
create_date               |  true           |  string     |  合约上市日期                      |  如"20180706"  |
contract_status           |  true           |  int        |  合约状态                          |  合约状态: 0:已下市、1:上市、2:待上市、3:停牌，4:暂停上市中、5:结算中、6:交割中、7:结算完成、8:交割完成、9:暂停上市  |
\</list\>    |             |               |                     |        |                 
ts                         |  true           |  long       |  响应生成时间点，单位：毫秒  |      


## 获取合约指数信息

###  示例

- GET `api/v1/contract_index`

```shell
curl "https://api.hbdm.com/api/v1/contract_index?symbol=BTC"
```

###  请求参数

参数名称   |  参数类型   | 必填   | 描述  |
-------------- |  -------------- |  ---------- |  ----------------  |
symbol         |  string         |  true       |  "BTC","ETH"...  |

> Response:

```json
    {
      "status":"ok",
      "data": [
         {
           "symbol": "BTC",
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
symbol                     |  true           |  string     |  指数代码                    | "BTC","ETH"...  |
index_price               |  true           |  decimal    |  指数价格   |                  |
index_ts                |  true           |  long   |  响应生成时间点，单位：毫秒   |                  |
\</list\>               |                |           |                           |  |                                                            
ts                         |  true           |  long       |  时间戳，单位：毫秒   |   |

## 获取合约最高限价和最低限价

###  示例

- GET `api/v1/contract_price_limit`

```shell
curl "https://api.hbdm.com/api/v1/contract_price_limit?symbol=BTC&contract_type=this_week"
```

###  请求参数

参数名称     | 参数类型    | 必填    | 描述 |
----------------  | --------------  | ---------- |  -----------------------------------------------------------------  |
symbol           |  string         |  false      |  "BTC","ETH"...  |
contract_type   |  string         |  false      |  合约类型 (当周:"this_week", 次周:"next_week", 季度:"quarter")  |
contract_code   |  string         |  false      |  BTC180914 ...  |

###  备注：

如果contract_code填了值，那就按照contract_code去查询；
如contract_code没有填值，则按照symbol+contract_type去查询，两个查询条件必填一个。

> Response:

```json
    {
      "status":"ok",
      "data": 
       [{
          "symbol":"BTC",
          "high_limit":443.07,
          "low_limit":417.09,
          "contract_code":"BTC180914",
          "contract_type":"this_week"
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
contract_code  |  true  |  string  |  合约代码  |  如"BTC180914" ...                                          |
contract_type  |  true  |  string  |  合约类型  |  当周:"this_week", 次周:"next_week", 季度:"quarter"              |
\<list\>  |    |    |    |    |
ts  |    true  |  long  |  响应生成时间点，单位：毫秒              |            |


## 获取当前可用合约总持仓量 

###  示例

- GET `api/v1/contract_open_interest`

```shell
curl "https://api.hbdm.com/api/v1/contract_open_interest?symbol=BTC&contract_type=this_week"
```

###  请求参数

参数名称 | 参数类型    | 必填    | 描述 |
---------------- |  -------------- |  ---------- |  -----------------------------------------------------------------  |
symbol  |  string  |    false  | "BTC","ETH"...  |
contract_type  |   string  |    false  | 合约类型 (当周:"this_week", 次周:"next_week", 季度:"quarter")  |
contract_code  |   string  |    false  | BTC180914  |

> Response:

```json
    {
      "status":"ok",
      "data":
        [{
          "symbol":"BTC",
          "contract_type": "this_week",
          "volume":123,
          "amount":106,
          "contract_code": "BTC180914"
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
contract_type  |  true  |  string  |  合约类型|  当周:"this_week", 次周:"next_week", 季度:"quarter"  |
volume  |  true  |  decimal  |  持仓量(张)|    |   
amount  |  true  |  decimal  |  持仓量(币)|    |   
contract_code  |  true  |  string  |  合约代码  |  如"BTC180914" ...  |
\</list\>  |    |    |    |    |
ts  |    true  |  long  |  响应生成时间点，单位：毫秒   |

## 获取预估交割价

###  示例

- GET `api/v1/contract_delivery_price`

```shell
curl "https://api.hbdm.com/api/v1/contract_delivery_price?symbol=BTC"
```

###  请求参数

参数名称 | 参数类型    | 必填    | 描述 |
---------------- |  -------------- |  ---------- |  -----------------------------------------------------------------  |
symbol  |  string  |    true  | "BTC","ETH"...  |

> Response:

```json
    {
      "status":"ok",
      "data":
        {
          "delivery_price": 3806.4615259197324414715719     
         },
      "ts": 1490759594752
    }
```

###  返回参数

参数名称  |    是否必须   |  类型   |  描述  |  取值范围  |
-------------------------- |  -------------- |  ---------- |  ----------------------------  | ------------------------------------------------------  |
status  |  true  |  string  |  请求处理结果  | "ok" , "error"  |
\<list\>(属性名称: data)  |    |    |    |       |
delivery_price  |  true  |  string  |  预估交割价  |   |
\</list\>  |    |    |    |    |
ts  |    true  |  long  |  响应生成时间点，单位：毫秒   |        |


## 查询系统状态

###  示例

- GET `api/v1/contract_api_state` 

```shell
curl "https://api.hbdm.com/api/v1/contract_api_state"
```

###  请求参数

参数名称   |  参数类型     |  必填    |  描述  |
-------------- |  -------------- |  ---------- |  -------------------------------------------------------------------------------- |
symbol  |    string  |    false  |  "BTC","ETH"...，如果缺省，默认返回所有品种  |

> Response:

```json

    {
      "status": "ok",
      "data": [
        {
          "symbol": "BTC",
          "open": 1,
          "close": 1,
          "cancel": 1,
          "transfer_in": 1,
          "transfer_out": 1
        }
     ],
     "ts": 158797866555
    }
    
```

###  返回参数

参数名称   |   是否必须  |   数据类型   |   描述   |   取值范围   |
-------- | -------- | -------- |  --------------------------------------- | -------------- | 
status | true | string | 请求处理结果	 | "ok" , "error" |
ts | true  | long | 响应生成时间点，单位：毫秒 |  |
\<data\> |  |  |  |  |
symbol | true  | string | 品种代码 | "BTC","ETH"... |
open | true | int | 开仓下单权限："1"表示可用，“0”表示不可用 |  |
close | true | int | 平仓下单权限："1"表示可用，“0”表示不可用 |  |
cancel | true | int | 撤单权限："1"表示可用，“0”表示不可用 |  |
transfer_in | true | int | 从币币转入的权限："1"表示可用，“0”表示不可用 |  |
transfer_out | true | int | 转出至币币的权限："1"表示可用，“0”表示不可用 |  |
\</data\>|  |  |  |  |

### 备注

  - open，指交易权限中对应的“API-开仓-普通订单”的权限，开启为可用，关闭为不可用；
  
  - close，指交易权限中对应的“API-平仓-普通订单”的权限，开启为可用，关闭为不可用；
  
  - cancel，指交易权限中对应的“API-撤单-普通订单”的权限，开启为可用，关闭为不可用；
  
  - transfer_in，指交易权限中对应的“其他-划转-从币币转入”的权限，开启为可用，关闭为不可用；
  
  - transfer_out，指交易权限中对应的“其他-划转-转出至币币”的权限，开启为可用，关闭为不可用；

## 获取行情深度数据

###  示例

- GET `/market/depth` 

```shell
curl "https://api.hbdm.com/market/depth?symbol=BTC_CQ&type=step5"
```

###  请求参数

参数名称   |  参数类型     |  必填    |  描述  |
-------------- |  -------------- |  ---------- |  -------------------------------------------------------------------------------- |
symbol  |    string  |    true  |  如"BTC_CW"表示BTC当周合约，"BTC_NW"表示BTC次周合约，"BTC_CQ"表示BTC季度合约  |
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
      "ch":"market.BTC_CQ.depth.step5",
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
          "ch":"market.BTC_CQ.depth.step5",
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

- GET  `/market/history/kline`

```shell
curl "https://api.hbdm.com/market/history/kline?period=1min&size=200&symbol=BTC_CQ"
```

###  请求参数

参数名称    |  是否必须  |   类型     |  描述    |  默认值   |  取值范围  |
-------------- |  -------------- |  ---------- |  ---------- |  ------------ |  -----------------------------------------------------|
symbol  |    true  |  string  |  合约名称  |  |  如"BTC_CW"表示BTC当周合约，"BTC_NW"表示BTC次周合约，"BTC_CQ"表示BTC季度合约  |
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
      "ch": "market.BTC_CQ.kline.1min",
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

- GET  `/market/detail/merged`

```shell
curl "https://api.hbdm.com/market/detail/merged?symbol=BTC_CQ"
```

###  请求参数

参数名称   |  是否必须   |  类型   |  描述   |  默认值   |  取值范围  |
--------------  | --------------  | ---------- |  ----------  | ------------ |  --------------------------------------------------------------------------------  |
symbol  |    true  |  string  |  合约名称  |  如"BTC_CW"表示BTC当周合约，"BTC_NW"表示BTC次周合约，"BTC_CQ"表示BTC季度合约  |                |

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
      "ch": "market.BTC_CQ.detail.merged",
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

- GET  `/market/trade`

```shell
curl "https://api.hbdm.com/market/trade?symbol=BTC_CQ"
```
###  请求参数

参数名称     |  是否必须   |  类型   |  描述   |  默认值  |  取值范围  |
-------------- |  -------------- |  ---------- |  ---------- |  ------------ |  --------------------------------------------------------------------------------  |
symbol  |    true  |  string  |  合约名称  |  |  如"BTC_CW"表示BTC当周合约，"BTC_NW"表示BTC次周合约，"BTC_CQ"表示BTC季度合约  |

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
      "ch": "market.BTC_CQ.trade.detail",
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
ch  |  true  |  string  |  数据所属的 channel，格式： market.\$symbol.trade.detail  |  |   |
status  |  true  |  string  |  |  |  "ok","error" |
tick  |  true  |  object  |  Trade 数据  |    |    |   
ts  |  true  |  number  |  发送时间  |   |    |


## 批量获取最近的交易记录

###  示例

- GET  `/market/history/trade`

```shell
curl "https://api.hbdm.com/market/history/trade?symbol=BTC_CQ&size=100"
```

###  请求参数：

参数名称     |  是否必须     | 数据类型   |  描述  |    默认值    |  取值范围  |
-------------- |  -------------- |  -------------- |  -------------------- |  ------------ |  --------------------------------------------------------------------------------  |
symbol  |    true  |  string  |    合约名称  |    |  如"BTC_CW"表示BTC当周合约，"BTC_NW"表示BTC次周合约，"BTC_CQ"表示BTC季度合约  |
size  |  false  |  number  |    获取交易记录的数量  | 1  |  [1, 2000]  |

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
      "ch": "market.BTC_CQ.trade.detail",
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
ch  |  true  |  string  |    数据所属的 channel，格式： market.\$symbol.trade.detail   |    |
data  |  true  |  object  |    Trade 数据  |    |
status  |  true  |  string  |    |    "ok"，"error" |
ts  |  true  |  number  |    响应生成时间点，单位：毫秒  |    |

## 查询合约风险准备金余额和预估分摊比例

- GET `api/v1/contract_risk_info`

```shell
curl "https://api.hbdm.com/api/v1/contract_risk_info"
```
 
### 请求参数

 参数名称               |   是否必须  |  类型  |  描述             |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
symbol | false | string | 品种代码	 | "BTC","ETH"...，如果缺省，默认返回所有品种 |

> Response:

```json
{
  "status": "ok",
  "ts": 158797866555,
  "data": [
    {
      "symbol": "ETH",
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
 symbol | true  | string | 品种代码 | "BTC","ETH"... |
 insurance_fund | true  | decimal | 风险准备金余额 |  |
 estimated_clawback | true  | decimal | 预估分摊比例 |  |
 \</data\> |  |  |  |  |

## 查询合约风险准备金余额历史数据

- GET `api/v1/contract_insurance_fund`

```shell
curl "https://api.hbdm.com/api/v1/contract_insurance_fund?symbol=ETH"
```
 
### 请求参数

  参数名称                |   是否必须   |   类型    |    描述             |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
 symbol | true | string | 品种代码	 | "BTC","ETH"... |

> Response:

```json
{
  "status": "ok",
  "ts": 158797866555,
  "data":   {
     "symbol": "ETH",
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
 \<tick\> |  |  |  |  |
 insurance_fund | true  | decimal | 风险准备金余额 |  |
 ts | true  | long | 数据时间点，单位：毫秒 |  |
 \</tick\> |  |  |  |  |
 \</data\> |  |  |  |  |

## 查询平台阶梯调整系数

- GET `api/v1/contract_adjustfactor`

```shell
curl "https://api.hbdm.com/api/v1/contract_adjustfactor"
```

### 请求参数

  参数名称                |   是否必须   |    类型   |   描述             |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
 symbol | false | string | 品种代码	 | "BTC","ETH"...，如果缺省，默认返回所有品种 |

> Response:

```json
{
  "status": "ok",
  "data": [
   {
      "symbol": "BTC",
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

- GET `api/v1/contract_his_open_interest`

```shell
curl "https://api.hbdm.com/api/v1/contract_his_open_interest?symbol=BTC&contract_type=this_week&period=60min&amount_type=1"
```

### 请求参数

|  参数名称                |   是否必须   |   类型    |   描述             |   取值范围       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| symbol | true | string | 品种代码   | "BTC","ETH"... |
| contract_type| true | string | 合约类型 | 当周:"this_week", 次周:"next_week", 季度:"quarter" |
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
         "contract_type": "this_week",
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
| contract_type| true | string | 合约类型 | 当周:"this_week", 次周:"next_week", 季度:"quarter"|
| \<tick\> |  |  |  |  |   
| volume | true | decimal | 持仓量 |  |
| amount_type | true | int | 计价单位 | 1:张，2:币  |
| ts | true | long | 统计时间 |  |
| \</tick\> |  |  |  |  |
| \</data\> |  |  |  |  |

- 注意：
  
  tick字段：数组内的数据按照时间倒序排列；
  data字段：字典类型。

## 精英账户多空持仓对比-账户数

### 实例

- GET `api/v1/contract_elite_account_ratio`

```shell
curl "https://api.hbdm.com/api/v1/contract_elite_account_ratio?symbol=BTC&period=60min"
```

### 请求参数

   参数名称               |  是否必须  |   类型   |   描述            |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
 symbol | true | string | 品种代码	 | "BTC","ETH"... |
 period | true | string | 周期	 | 5min, 15min, 30min, 60min,4hour,1day |

> Response:

```json
{
  "status": "ok",
  "data": [
    {
      "symbol": "BTC",
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

### 返回参数

|  参数名称                |   是否必须   |   类型   |    描述            |    取值范围       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| status | true | string | 请求处理结果	 | "ok" , "error" |
| ts | true  | long | 响应生成时间点，单位：毫秒 |  |
| \<data\> |  |  |  |  |
| symbol | true  | string | 品种代码 | "BTC","ETH"... |
| \<list\> |  |  |  |  |
| buy_ratio | true | decimal | 净多仓的账户比例 |  |
| sell_ratio | true | decimal | 净空仓的账户比例 |  |
| locked_ratio | true | decimal | 锁仓的账户比例 |  |
| ts | true  | long | 生成时间 |  |
| \</list\> |  |  |  |  |
| \</data\> |  |  |  |  |

## 精英账户多空持仓对比-持仓量

### 实例

- GET `api/v1/contract_elite_position_ratio`

```shell
curl "https://api.hbdm.com/api/v1/contract_elite_position_ratio?symbol=BTC&period=60min"
```

### 请求参数

   参数名称                |   是否必须   |   类型    |   描述             |    取值范围       |
 ----------------------- | -------- | ------- | ------------------ | -------------- |
 symbol | true | string | 品种代码	 | "BTC","ETH"... |
 period | true | string | 周期	 | 5min, 15min, 30min, 60min,4hour,1day |

> Response:

```json

{
  "status": "ok",
  "data": [
    {
      "symbol": "BTC",
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

### 返回参数

|   参数名称                |   是否必须   |   类型   |   描述             |   取值范围       |
| ----------------------- | -------- | ------- | ------------------ | -------------- |
| status | true | string | 请求处理结果	 | "ok" , "error" |
| ts | true  | long | 响应生成时间点，单位：毫秒 |  |
| \<data\> |  |  |  |  |
| symbol | true  | string | 品种代码 | "BTC","ETH"... |
| \<list\> |  |  |  |  |
| buy_ratio | true | decimal | 多仓的总持仓量占比 |  |
| sell_ratio | true | decimal | 空仓的总持仓量占比 |  |
| ts | true  | long | 生成时间 |  |
| \</list\> |  |  |  |  |
| \</data\> |  |  |  |  |

## 获取强平订单

### 实例

- GET `api/v1/contract_liquidation_orders`

```shell
curl "https://api.hbdm.com/api/v1/contract_liquidation_orders?symbol=BTC&trade_type=0&create_date=7"
```

### 请求参数

|   参数名称    |   是否必须  |   类型   |   描述        |   默认值   |    取值范围                                |
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| symbol      | true     | string | 品种代码          |         | "BTC","ETH"...                           |
| trade_type      | true     | int  | 交易类型         |               |0:全部,5: 卖出强平,6: 买入强平 |
| create_date | true     | int    | 日期            |         | 7，90（7天或者90天）        |
| page_index | false     | int    | 页码,不填默认第1页            |         |         |
| page_size | false     | int    | 不填默认20，不得多于50            |         |        |

> Response:

```json

{
   "status": "ok",
   "data":{
     "orders":[
       {
         "symbol": "BTC",
         "contract_code": "BTC180914",    
         "direction": "buy",
         "offset": "close",
         "volume": 111,
         "price": 1111,
         "created_at": 1408076414000
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

|  参数名称               |   是否必须   |   类型    |   描述             |   取值范围     |
| ---------------------- | -------- | ------- | ------------------ | ------------ |
| status                 | true     | string  | 请求处理结果             |              |
| \<object\>(属性名称: data) |          |         |                    |              |
| \<list\>(属性名称: orders) |          |         |                    |              |
| symbol                 | true     | string  | 品种代码               |              |
| contract_code          | true     | string  | 合约代码               |"BTC180914" ...  |
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

# 合约资产接口

## 获取用户账户信息

###  示例

- POST  `api/v1/contract_account_info`


###  请求参数

参数名称     |  是否必须   |  类型   |  描述   |  默认值   |  取值范围  |
-------------- |  -------------- |  ---------- |  ----------  | ------------ |  ------------------------------------------ |
symbol  |    false  |  string  |  品种代码  |    |  "BTC","ETH"...如果缺省，默认返回所有品种  |

> Response:

```json
    {
      "status": "ok",
      "data": [
        {
          "symbol": "BTC",
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
          "margin_static": 1
         },
        {
          "symbol": "ETH",
          "margin_balance": 1,
          "margin_position": 0,
          "margin_frozen": 3.33,
          "margin_available": 0.34,
          "profit_real": 3.45,
          "profit_unreal": 7.45,
          "withdraw_available":4.7389859,
          "risk_rate": 100,
          "liquidation_price": 100,
          "adjust_factor": 0.1,
          "margin_static": 1
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
margin_balance  |  true  |  decimal    |  账户权益   |    |   
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
margin_static                | true     | decimal  | 静态权益               |                |  
\</list\>  |    |    |    |       |
ts  |    number  |    long  |  响应生成时间点，单位：毫秒  |    | 


## 获取用户持仓信息

###  示例

- POST `api/v1/contract_position_info`

###  请求参数

参数名称   |  是否必须   |  类型    |  描述    |  默认值    |  取值范围  |
-------------- |  --------------  | ---------- |  ----------  | ------------ |  ------------------------------------------  |
symbol  |    false  |  string  |  品种代码  |    |  "BTC","ETH"...如果缺省，默认返回所有品种  |

> Response:

```json
    {
      "status": "ok",
      "data": [
        {
          "symbol": "BTC",
          "contract_code": "BTC180914",
          "contract_type": "this_week",
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
contract_code  |  true  |  string  |  合约代码  |  "BTC180914" ...  |
contract_type  |  true  |  string  |  合约类型  |  当周:"this_week", 次周:"next_week", 季度:"quarter"  |
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

- POST `api/v1/contract_sub_account_list`

参数名称    |  是否必须   |   类型   |   描述          |   默认值   |   取值范围                                   |
----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
symbol      | false     | string | 品种代码          |         | "BTC","ETH"...  ,如果缺省，默认返回所有品种                         |

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
                    "margin_balance": 1,
                    "liquidation_price": 100,
  	          "risk_rate": 100
  	        },
  	        {
  	           "symbol": "ETH",
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
                     "margin_balance": 1,
                     "liquidation_price": 100,
  	           "risk_rate": 100
  	        },
  	        {
  	           "symbol": "ETH",
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
margin_balance | true | decimal | 账户权益 |  |
liquidation_price | true | decimal | 预估强平价 |  |
risk_rate | true | decimal | 保证金率 |  |
\</list\> |  |  |  |  |
\</data\> |  |  |  |  |

- 备注

  只返回已经开通合约交易的子账户数据.


## 查询单个子账户资产信息

- POST `api/v1/contract_sub_account_info`

###  请求参数*


  参数名称     |   是否必须   |  类型  |  描述         |   默认值   |   取值范围                                 |
----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
symbol | false | string | 品种代码	 | "BTC","ETH"...，如果缺省，默认返回所有品种 |
sub_uid | true | long | 子账户的UID	 |  |

> Response:

```json
  {
    "status": "ok",
    "data":  [ 
       {
          "symbol": "BTC",
          "margin_balance": 1,
          "margin_position": 0,
          "margin_frozen": 3.33,
          "margin_available": 0.34,
          "profit_real": 3.45,
          "profit_unreal": 7.45,
          "withdraw_available":4.0989898,
          "risk_rate": 100,
          "liquidation_price": 100,
          "adjust_factor": 0.1
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
\</data\> |  |  |  |  |


- 备注

  只能查询到开通合约交易的子账户信息；
  
  子账户来过合约系统但是未开通合约交易也不返回对应的数据；

## 查询单个子账户持仓信息

- POST `api/v1/contract_sub_position_info`

### 请求参数

  参数名称    |  是否必须  |  类型  |  描述        |   默认值  |  取值范围                                  |
----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
symbol | false | string | 品种代码	 | "BTC","ETH"...，如果缺省，默认返回所有品种 |
sub_uid | true | long | 子账户的UID	 |  |

> Response:

```json 
  {                                               
    "status": "ok",                               
    "ts": 158797866555                            
    "data":[                                      
       {                                          
           "symbol": "BTC",                       
           "contract_code": "BTC180914",          
           "contract_type": "this_week",          
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
           "direction":"buy"                      
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
contract_code                | true     | string  |  合约代码             | "BTC180914" ... |
contract_type                | true     | string  | 合约类型              | 当周:"this_week", 次周:"next_week", 季度:"quarter" |
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
\</data\> |  |  |  |  |

## 查询用户财务记录

- POST `api/v1/contract_financial_record`
 
###  请求参数

参数名称                |  是否必须  |  类型   |  描述              |  取值范围       |
----------------------- | -------- | ------- | ------------------ | ------------------------------- |
symbol | true | string | 品种代码   | "BTC","ETH"... |
type | false | string | 不填查询全部类型,【查询多类型中间用，隔开】 | 平多：3，平空：4，开仓手续费-吃单：5，开仓手续费-挂单：6，平仓手续费-吃单：7，平仓手续费-挂单：8，交割平多：9，交割平空：10，交割手续费：11，强制平多：12，强制平空：13，从币币转入：14，转出至币币：15，结算未实现盈亏-多仓：16，结算未实现盈亏-空仓：17，穿仓分摊：19，系统：26，活动奖励：28，返利：29 |
create_date | false | int | 7，90 (7天 ，90天) ，不填默认为7|  |
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
type | true  | int | 交易类型 | 平多：3，平空：4，开仓手续费-吃单：5，开仓手续费-挂单：6，平仓手续费-吃单：7，平仓手续费-挂单：8，交割平多：9，交割平空：10，交割手续费：11，强制平多：12，强制平空：13，从币币转入：14，转出至币币：15，结算未实现盈亏-多仓：16，结算未实现盈亏-空仓：17，穿仓分摊：19，系统：26，活动奖励：28，返利：29 |
amount | true  | decimal | 金额 |  |
\</financial_record\> |  |  |  |  |
total_page | true  | int | 总页数 |  |
current_page | true  | int | 当前页 |  |
total_size | true  | int | 总条数 |  |
\</data\> |  |  |  |  |

## 查询用户当前的下单量限制

- POST `api/v1/contract_order_limit`
 
 
### 请求参数

  参数名称               |   是否必须   |  类型  |  描述             |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
 symbol | false | string | 品种代码	 | "BTC","ETH"...，如果缺省，默认返回所有品种 |
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
          "types": [
             {
              "contract_type": "this_week",
              "open_limit": 3000,
              "close_limit": 3000
             },
             {
              "contract_type": "next_week",
              "open_limit": 3000,
              "close_limit": 3000
             },     
             {
              "contract_type": "quarter",
              "open_limit": 3000,
              "close_limit": 3000
             }
           ]
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
 \<types\> |  |  |  |  |
 contract_type  | true | string | 合约类型 | 当周:"this_week", 次周:"next_week", 季度:"quarter" |
 open_limit | true | long | 合约开仓单笔下单量最大值 |  |
 close_limit | true | long | 合约平仓单笔下单量最大值 |  |
 \</types\>  |  |  |  |  |
 \</list\>  |  |  |  |  |
 \</data\> |  |  |  |  |

## 查询用户当前的手续费费率

- POST `api/v1/contract_fee`
 
### 请求参数

  参数名称                |  是否必须 |  类型  |   描述             |  取值范围      |
----------------------- | -------- | ------- | ------------------ | -------------- |
symbol | false | string | 品种代码	 | "BTC","ETH"...，如果缺省，默认返回所有品种 |

> Response:

```json
{
  "status": "ok",
  "data": [
    {
      "symbol": "BTC",
      "open_maker_fee": "-0.00025",
      "open_taker_fee": "0.00075",
      "close_maker_fee": "-0.00025",
      "close_taker_fee": "0.00075",
      "delivery_fee": "0.0005"
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
 open_maker_fee | true | string | 开仓挂单的手续费费率，小数形式 | |
 open_taker_fee | true | string | 开仓吃单的手续费费率，小数形式 | |
 close_maker_fee | true | string | 平仓挂单的手续费费率，小数形式 | |
 close_taker_fee | true | string | 平仓吃单的手续费费率，小数形式 | |
 delivery_fee | true | string | 交割的手续费费率，小数形式 | |
 \</data\>  |  |  |  |  |

## 查询用户当前的划转限制

- POST `api/v1/contract_transfer_limit`
 
### 请求参数

  参数名称                |  是否必须  |  类型   |    描述             |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
 symbol | false | string | 品种代码	 | "BTC","ETH"...，如果缺省，默认返回所有品种 |

> Response:

```json
{
  "status": "ok",
  "data": [
    {
      "symbol": "BTC",
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

- post `api/v1/contract_position_limit`
  
### 请求参数

  参数名称               |  是否必须 |  类型  |  描述             |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
 symbol | false | string | 品种代码	 | "BTC","ETH"...，如果缺省，默认返回所有品种 |

> Response:

```json
{
  "status": "ok",
  "data": [
    {
      "symbol": "BTC",
      "list": [
        {
         "contract_type": "all",
         "buy_limit": 5000,
         "sell_limit": 5000
       },
        {
         "contract_type": "this_week",
         "buy_limit": 3000,
         "sell_limit": 3000
       },
        {
         "contract_type": "next_week",
         "buy_limit": 3000,
         "sell_limit": 3000
       },     
        {
         "contract_type": "quarter",
         "buy_limit": 3000,
         "sell_limit": 3000
       }
       ]
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
\<list\> |  |  |  |  |
contract_type| true | string | 合约类型 | 当周:"this_week", 次周:"next_week", 季度:"quarter"，所有合约:“all” |
buy_limit | true | decimal | 合约多仓持仓的最大值，单位为张 |  |
sell_limit | true | decimal | 合约空仓持仓的最大值，单位为张 |  |
\</list\> |  |  |  |  |
\</data\> |  |  |  |  |

# 合约交易接口

## 合约下单 

###  示例

- POST  `api/v1/contract_order`


###  请求参数

参数名  |  参数类型    |  必填   |  描述  |
-------------------- |  -------------- |  ----------  | ---------------------------------------------------------------  |
symbol  |    string  |    true  | "BTC","ETH"...  |
contract_type  |  string  |    true  | 合约类型 ("this_week":当周 "next_week":下周 "quarter":季度)  |
contract_code  |  string  |    true  |  BTC180914  |
client_order_id |   long  |  false  |  客户自己填写和维护，必须为数字  |
price  |  decimal  |   false  |  价格  |
volume  |    long  |  true  |  委托数量(张)  |
direction  |  string  |    true  |  "buy":买 "sell":卖  |
offset  |    string  |    true  |  "open":开 "close":平  |
lever_rate  |  int  | true  |  杠杆倍数[“开仓”若有10倍多单，就不能再下20倍多单]  |
order_price_type |  string  |    true  |  订单报价类型 "limit":限价 "opponent":对手价 "post_only":只做maker单,post only下单只受用户持仓数量限制,optimal_5：最优5档、optimal_10：最优10档、optimal_20：最优20档，ioc:IOC订单，fok：FOK订单  |

###  备注

如果contract_code填了值，那就按照contract_code去下单，如果contract_code没有填值，则按照symbol+contract_type去下单。

对手价下单price价格参数不用传，对手价下单价格是买一和卖一价,optimal_5：最优5档、optimal_10：最优10档、optimal_20：最优20档下单price价格参数不用传，"limit":限价，"post_only":只做maker单 需要传价格，"fok"：全部成交或立即取消，"ioc":立即成交并取消剩余。


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
		    "order_id": 633766664829804544,
		    "order_id_str": "633766664829804544",
		    "client_order_id": 1234
	      },
      "ts": 158797866555
    }
```

###  返回参数

参数名称  |   是否必须   |  类型   |  描述  |  取值范围  |
------------------- | -------------- | ---------- | -------------------------------------------- | ---------------- |
status  |   true  |  string  |  请求处理结果  |  "ok" , "error"  |
order_id  |  true  |  bigint  |  订单ID  |    | 
order_id_str  |  true  |  string  |  String类型订单ID  |    | 
client_order_id  | true  |  long  |  用户下单时填写的客户端订单ID，没填则不返回  | 
ts  |  true  |  long  |  响应生成时间点，单位：毫秒  |    |   

### 备注

order_id返回是18位，nodejs和javascript默认解析18有问题，nodejs和javascript里面JSON.parse默认是int，超过18位的数字用json-bigint的包解析。

## 合约批量下单 


###  示例

- POST  `api/v1/contract_batchorder`

###  请求参数

参数名  |    参数类型   |  必填   |  描述  |
---------------------------------- | -------------- |  ---------- | -------------------------------------------------------------- |
\<list\>(属性名称: orders_data)  |    |    |    |  
symbol  |   string  |    false  | "BTC","ETH"...  |
contract_type  |  string  |    false  | 合约类型: "this_week":当周 "next_week":下周 "quarter":季度  |
contract_code  |  string  |    false  | BTC180914  |
client_order_id  |  long  |  false  |  客户自己填写和维护，必须为数字  |
price  |  decimal  |   false  |  价格  |
volume  |  long  |  true  |  委托数量(张)  |
direction  |  string  |    true  |  "buy":买 "sell":卖  |
offset  |  string  |    true  |  "open":开 "close":平  |
lever_rate  |   int  | true  |  杠杆倍数[“开仓”若有10倍多单，就不能再下20倍多单]  |
order_price_type |  string  |    true  |  订单报价类型 "limit":限价 "opponent":对手价 "post_only":只做maker单,post only下单只受用户持仓数量限制,optimal_5：最优5档、optimal_10：最优10档、optimal_20：最优20档，ioc：IOC订单，fok：FOK订单  |
\</list\>  |    |    |    |

###  备注

如果contract_code填了值，那就按照contract_code去下单，如果contract_code没有填值，则按照symbol+contract_type去下单。

对手价下单price价格参数不用传，对手价下单价格是买一和卖一价,optimal_5：最优5档、optimal_10：最优10档、optimal_20：最优20档下单price价格参数不用传，"limit":限价，"post_only":只做maker单 需要传价格，"fok"：全部成交或立即取消，"ioc":立即成交并取消剩余。

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
            "err_msg": "invalid symbol"
           },
          {
            "index":3,
            "err_code": 200415,
            "err_msg": "invalid symbol"
           }
         ],
        "success":[
          {
            "index":1,
            "order_id":633766664829804544,
            "order_id_str": "633766664829804544",
            "client_order_id":1344567
           },
          {
            "index":2,
            "order_id":633766664829804544,
            "order_id_str": "633766664829804544",
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
order_id  |  true  |  bigint  |  订单ID  |    | 
order_id_str  |  true  |  string  |  订单ID  |    | 
client_order_id  |  true  |  long  |  用户下单时填写的客户端订单ID，没填则不返回  | 
\</list\>  |    |    |    |    |
ts  |  true  |  long  |  响应生成时间点，单位：毫秒  |

### 备注

order_id返回是18位，nodejs和javascript默认解析18有问题，nodejs和javascript里面JSON.parse默认是int，超过18位的数字用json-bigint的包解析。

## 撤销订单 

###  示例

- POST `api/v1/contract_cancel`

###  请求参数

参数名称  |   是否必须   |  类型   |  描述  |
------------------- | -------------- | ---------- | -------------------------------------------------------------- |
order_id |  false  |  string  |  订单ID(多个订单ID中间以","分隔,一次最多允许撤消50个订单)  |
client_order_id  |  false  |  string  |  客户订单ID(多个订单ID中间以","分隔,一次最多允许撤消50个订单)  |
symbol  |   true  |  string  |  "BTC","ETH"...  |

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
        "order_id":"633766664829804544",
        "err_code": 200417,
        "err_msg": "invalid symbol"
       },
      {
        "order_id":"633766664829804544",
        "err_code": 200415,
        "err_msg": "invalid symbol"
       }
      ],
    "successes":"161256,1344567"
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

- POST  `api/v1/contract_cancelall`

###  请求参数

参数名称    |  是否必须    |  类型    |  描述  |
-------------- | -------------- | ---------- | ---------------------------- |
symbol  |    true  |  string   |  品种代码，如"BTC","ETH"...  |
contract_code  |    false  |  string  |  合约code  |
contract_type  |    false  |  string  |  合约类型  |

### 备注 
- 只传symbol，撤该该品种下所有周期的合约
- 只要有contract_code，则撤销该code的合约
- 只传symbol+contract_type， 则撤销二者拼接所成的合约订单

> Response:(多笔订单返回结果(成功订单ID,失败订单ID))
    
```json
    {
      "status": "ok",
      "data": {
        "errors":[
          {
            "order_id":"633766664829804544",
            "err_code": 200417,
            "err_msg": "invalid symbol"
           },
          {
            "order_id":"633766664829804544",
            "err_code": 200415,
            "err_msg": "invalid symbol"
           }
          ],
        "successes":"161256,161256"
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

- POST  `api/v1/contract_order_info`

###  请求参数

参数名称  |    是否必须    |  类型    |  描述  |
------------------- | -------------- | ---------- | ------------------------------------------------------------- |
order_id  |  false  |  string  |  订单ID(多个订单ID中间以","分隔,一次最多允许查询50个订单)  |
client_order_id   |  false  |  string  |  客户订单ID(多个订单ID中间以","分隔,一次最多允许查询50个订单)  |
symbol  |   true  |  string  |  "BTC","ETH"...  |

###  备注：

order_id和client_order_id都可以用来查询，同时只可以设置其中一种，如果设置了两种，默认以order_id来查询。周五交割结算后，会把结束状态的订单（5部分成交已撤单 6全部成交 7已撤单）删除掉。

client_order_id，24小时有效，超过24小时的订单根据client_order_id将查询不到。

> Response:

```json
    {
      "status": "ok",
      "data":[
        {
          "symbol": "BTC",
          "contract_type": "this_week",
          "contract_code": "BTC180914",
          "volume": 111,
          "price": 1111,
          "order_price_type": "limit",
          "direction": "buy",
          "offset": "open",
          "lever_rate": 10,
          "order_id": 633766664829804544,
          "order_id_str": "633766664829804544",
          "client_order_id": 10683,
          "order_source": "web",
          "order_type": "1",
          "created_at": 1408076414000,
          "trade_volume": 1,
          "trade_turnover": 1200,
          "fee": 0,
          "trade_avg_price": 10,
          "margin_frozen": 10,
          "profit ": 10,
          "status": 0
         },
        {
          "symbol": "ETH",
          "contract_type": "this_week",
          "contract_code": "ETH180921",
          "volume": 111,
          "price": 1111,
          "order_price_type": "limit",
          "direction": "buy",
          "offset": "open",
          "lever_rate": 10,
          "order_id": 633766664829804544,
          "order_id_str": "633766664829804544",
          "client_order_id": 10683,
          "order_source": "web",
           "order_type": "1",
          "created_at": 1408076414000,
          "trade_volume": 1,
          "trade_turnover": 1200,
          "fee": 0,
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
contract_type  |  true  |  string  |  合约类型  |  当周:"this_week", 周:"next_week", 季度:"quarter"  |
contract_code  |  true  |  string  |  合约代码  | "BTC180914" ...  |
volume  |  true  |  decimal    |  委托数量  |    | 
price   |  true  |  decimal    |  委托价格  |    | 
order_price_type  |    true  |  string  |  订单报价类型  | 订单报价类型 "limit":限价 "opponent":对手价 "post_only":只做maker单,post only下单只受用户持仓数量限制  |  
direction  |  true  |  string  |  买卖方向  |  "buy":买 "sell":卖  |
offset  |  true  |  string  |  开平方向 |  "open":开 "close":平  |
lever_rate  |  true  |  int  |   杠杆倍数  |  1\\5\\10\\20  |
order_id  |  true  |  long  |  订单ID  |    | 
order_id_str  |  true  |  string  |  String类型订单ID  |    | 
client_order_id  |  true  |  long  |  客户订单ID  |    |  
created_at  |  true  |  long  |  创建时间  |    |
trade_volume    |  true  |  decimal  |    成交数量  |    |
trade_turnover  |  true  |  decimal  |   成交总金额  |    |    
fee  |   true  |  decimal  |     手续费  |     |   
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

- POST `api/v1/contract_order_detail`

###  请求参数

参数名称    |  是否必须     |  类型    |  描述  |
-------------- | -------------- | ---------- | ------------------------ |
symbol  |    true  |  string  |  "BTC","ETH"...  |
order_id  | true  |  bigint  |   订单id  |
created_at  |  false  |  long  |   下单时间戳  |
order_type  |  true  |  int  |   订单类型，1:报单 、 2:撤单 、 3:强平、4:交割  |
page_index  |    false  |  int  |   第几页,不填第一页  |
page_size  |  false  |  int  |   不填默认20，不得多于50  |

### 备注

order_id返回是18位，nodejs和javascript默认解析18有问题，nodejs和javascript里面JSON.parse默认是int，超过18位的数字用json-bigint的包解析。

created_at使用13位long类型时间戳（包含毫秒时间），如果输入准确的时间戳，查询性能将会提升。例如:"2019/10/18 10:26:22"转换为时间戳为：1571365582123。也可以直接从contract_order下单接口返回的ts中获取时间戳查询对应的订单。

created_at禁止传0。

> Response:

```json
    {
      "status": "ok",
      "data":{
        "symbol": "BTC",
        "contract_type": "this_week",
        "contract_code": "BTC180914",
        "volume": 111,
        "price": 1111,
        "order_price_type": "limit",
        "direction": "buy",
        "offset": "open",
        "status": 1,
        "lever_rate": 10,
        "trade_avg_price": 10,
        "margin_frozen": 10,
        "profit": 10,
        "order_source": "web",
        "created_at": 1408076414000,
        "instrument_price" : 10000,
        "final_interest" : 0,
        "adjust_value" : 0,
        "trades":[
          {
            "id":"21315414825-6141291349-1",
            "trade_id":112,
            "trade_volume":1,
            "trade_price":123.4555,
            "trade_fee":0.234,
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
     "err_msg": "invalid symbol",
     "ts": 1490759594752
    }
```

###  返回数据

参数名称  |  是否必须   |  类型   |  描述  |  取值范围  |
----------------------------- | -------------- | ---------- | --------------------------------------------- | ------------------------------------------------------ |
status  |   true  |  string  |  请求处理结果  | "ok" , "error"  |
\<object\> (属性名称: data)  |    |    |    |    | 
symbol  |   true  |  string  |  品种代码  |    | 
contract_type  |  true  |  string  |  合约类型  |  当周:"this_week", 次周:"next_week", 季度:"quarter"  |
contract_code  |  true  |  string  |  合约代码  |  "BTC180914" ...  |
lever_rate  |   true  |  int  |   杠杆倍数  |  1\5\10\20  |
direction  |  true  |  string  |  买卖方向  | "buy":买 "sell":卖 |  
offset  |     true  |  string  | 开平方向 |  "open":开 "close":平  |
volume  |     true  |  decimal    |  委托数量  |    | 
price  |      true  |  decimal    |  委托价格  |    | 
created_at  |   true  |  long    |    创建时间  |    |
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
id               | true     | string    | 唯一成交id,由于trade_id并不是unique的，具体使用方式是用trade_id和id作为联合主键，拼接成unique的成交ID。               |              |
trade_id  |  true  |  long  |  撮合结果id,由于trade_id并不是unique的，具体使用方式是用trade_id和id作为联合主键，拼接成unique的成交ID。   |    |    
trade_price  |  true  |  decimal  |  撮合价格  |    |
trade_volume  | true  |  decimal  |  成交量  |    |  
trade_turnover  |    true  |  decimal  |  成交金额  |    | 
trade_fee  |   true  |  decimal  |  成交手续费  |    |    
role  |   true  |  string  |  taker或maker  |   | 
created_at  |   true  |  long  |  创建时间  |    | 
\</list\>  |    |    |    |    |   
\</object \>  |    |     |    |    |
ts  |  true  |  long  |  时间戳  |     |


## 获取合约当前未成交委托 

###  示例

- POST `api/v1/contract_openorders`  

###  请求参数

  参数名称   |  是否必须    |  类型    |  描述  |  默认值    |  取值范围  |
-------------- | -------------- | ---------- | ------------------------ | ------------ | ---------------- |
symbol  |    true  |  string  |  品种代码  |     |  "BTC","ETH"...  |
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
             "contract_type": "this_week",
             "contract_code": "BTC180914",
             "volume": 111,
             "price": 1111,
             "order_price_type": "limit",
             "order_type": 1,
             "direction": "buy",
             "offset": "open",
             "lever_rate": 10,
             "order_id": 633766664829804544,
             "order_id_str": "633766664829804544",
             "client_order_id": 10683,
             "order_source": "web",
             "created_at": 1408076414000,
             "trade_volume": 1,
             "trade_turnover": 1200,
             "fee": 0,
             "trade_avg_price": 10,
             "margin_frozen": 10,
             "profit": 0,
             "status": 1
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
contract_type  |  true  |  string  |  合约类型  |  当周:"this_week", 次周:"next_week", 季度:"quarter"  |
contract_code  |  true  |  string  |  合约代码  |  "BTC180914" ...  |
volume  |  true  |  decimal    |  委托数量  |    |
price   |  true  |  decimal    |  委托价格  |    |   
order_price_type  |    true  |  string  |  订单报价类型 "limit":限价 "opponent":对手价 "post_only":只做maker单,post only下单只受用户持仓数量限制  |
order_type  |  true  |  int  |   订单类型，1:报单 、 2:撤单 、 3:强平、4:交割  |
direction  |  true  |  string  |  "buy":买 "sell":卖  |    |   
offset  |  true  |  string  |  "open":开 "close":平  |    |  
lever_rate  |  true  |  int  |   杠杆倍数  |   1\\5\\10\\20  |
order_id  |  true  |  bigint  |  订单ID  |    |
order_id_str  |  true  |  string  |  String订单ID  |    |
client_order_id  |  true  |  long  |  客户订单ID  |    |
created_at  |  true  |  long  |  订单创建时间  |    |
trade_volume  |   true  |  decimal    |  成交数量  |    |  
trade_turnover  | true  |  decimal    |  成交总金额  |     | 
fee  |   true  |  decimal    |  手续费  |    |
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

- POST `api/v1/contract_hisorders` 

###  请求参数

参数名称   |  是否必须   |  类型    |  描述  |  默认值    |  取值范围  |
-------------- | -------------- | ---------- |------------------------ | ------------ | ------------------------------------------------------------------------------------------------------ |
symbol  |    true  |  string  |  品种代码  |   "BTC","ETH"...  |
trade_type  |   true  |  int  |   交易类型  |    0:全部,1:买入开多,2: 卖出开空,3: 买入平空,4: 卖出平多,5: 卖出强平,6: 买入强平,7:交割平多,8: 交割平空  |
type  |  true  |  int  |   类型  |  1:所有订单,2:结束状态的订单  |
status  |    true  |  int  |   订单状态  |    0:全部,3:未成交, 4: 部分成交,5: 部分成交已撤单,6: 全部成交,7:已撤单  |
create_date |  true  |  int  |   日期  |   7，90（7天或者90天） |
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
            "contract_type": "this_week",
            "contract_code": "BTC180914",
            "volume": 111,
            "price": 1111,
            "order_price_type": "limit",
            "direction": "buy",
            "offset": "open",
            "lever_rate": 10,
            "order_id": 633766664829804544,
            "order_id_str": "633766664829804544",
            "order_source": "web",
            "created_at": 1408076414000,
            "trade_volume": 1,
            "trade_turnover": 1200,
            "fee": 0,
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
order_id  |    true  |  bigint  |  订单ID  |  
order_id_str  |    true  |  string  |  String类型订单ID  |  
symbol  |  true  |  string  |  品种代码  |
contract_type  |    true  |  string  |  合约类型  | 当周:"this_week", 次周:"next_week", 季度:"quarter"  |
contract_code  |    true  |  string  |  合约代码  | "BTC180914" ...  |
lever_rate  |  true  |  int  |   杠杆倍数  |  1\\5\\10\\20  |
direction  |    true  |  string  | 买卖方向 |  "buy":买 "sell":卖  |  
offset  |  true  |  string  |  开平方向  |  "open":开 "close":平  |
volume  |  true  |  decimal    |  委托数量  |    |
price  |   true  |  decimal    |  委托价格  |    | 
create_date   |  true  |  long    |  创建时间  |    | 
order_source  |  true  |  string  |  订单来源  |    | 
order_price_type  |  true  |  string  |  订单报价类型 |  1限价单，3对手价，4闪电平仓，5计划委托，6post_only |  
margin_frozen  |    true  |  decimal    |  冻结保证金  |    |    
profit  |  true  |  decimal    |  收益  |    |
trade_volume  |  true  |  decimal    |  成交数量  |    | 
trade_turnover  |   true  |decimal    |  成交总金额  |    |    
fee  |  true  |  decimal    |  手续费  |    |   
trade_avg_price  | true  |  decimal    |  成交均价  |    | 
status  |  true  |  int  |   订单状态  |    | 
order_type  |  true  |  int  |   订单类型  |  1:报单 、 2:撤单 、 3:强平、4:交割  |
\</list\>  |    |    |     |     |  
\</object\>|    |    |     |     |
total_page    |  true  |  int  |   总页数  |   |   
current_page  |  true  |  int  |   当前页  |   |   
total_size  |  true  |  int  |   总条数  |    |  
ts  |  true  |  long  |  时间戳  |    |

### 备注

order_id返回是18位，nodejs和javascript默认解析18有问题，nodejs和javascript里面JSON.parse默认是int，超过18位的数字用json-bigint的包解析。

## 获取历史成交记录

### 实例

- POST `api/v1/contract_matchresults`

### 请求参数

 参数名称    | 是否必须 | 类型 |  描述        |  默认值 | 取值范围                             |
 ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
 symbol      | true     | string | 品种代码          |         | "BTC","ETH"...                           |
 trade_type  | true     | int    | 交易类型          |         | 0:全部,1:买入开多,2: 卖出开空,3: 买入平空,4: 卖出平多,5: 卖出强平,6: 买入强平 |
 create_date | true     | int    | 日期            |         | 7，90（7天或者90天）                            |
 contract_code      | false     | string | 合约code          |         |                          |
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
			"id": "2131234825-6124591349-1",
			"contract_code": "EOS190419",
			"contract_type": "this_week",
			"create_date": 1555553626736,
			"direction": "sell",
			"match_id": 3635853382,
			"offset": "close",
			"offset_profitloss": 0.15646398812252696,
			"order_id": 633766664829804544,
			"order_id_str": "633766664829804544",
			"symbol": "EOS",
			"trade_fee": -0.002897500905469032,
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
 id               | true     | string    | 唯一成交id,由于match_id并不是unique的，具体使用方式是用match_id和id作为联合主键，拼接成unique的成交ID。               |              |
 match_id               | true     | long    | 成交ID，不唯一，可能重复 ,由于match_id并不是unique的，具体使用方式是用match_id和id作为联合主键，拼接成unique的成交ID。              |              |
 order_id               | true     | bigint    | 订单ID               |              |
 order_id_str               | true     | string    | String类型订单ID               |              |
 symbol                 | true     | string  | 品种代码               |              |
 contract_type          | true     | string  | 合约类型               | 当周:"this_week", 次周:"next_week", 季度:"quarter" |
 contract_code          | true     | string  | 合约代码               |  "BTC180914" ...       |
 direction              | true     | string  | "buy":买 "sell":卖         |              |
 offset                 | true     | string  | "open":开 "close":平           |              |
 trade_volume           | true     | decimal | 成交数量               |              |
 trade_price                  | true     | decimal | 成交价格               |              |
 trade_turnover                  | true     | decimal | 成交总金额               |              |
 create_date            | true     | long    | 成交时间               |              |
 offset_profitloss                 | true     | decimal | 平仓盈亏                 |              |
 traded_fee                    | true     | decimal | 成交手续费                |              |
 role                   |   true    |       string  |  taker或maker  |         |
 \</list\>              |          |         |                    |              |
 total_page             | true     | int     | 总页数                |              |
 current_page           | true     | int     | 当前页                |              |
 total_size             | true     | int     | 总条数                |              |
 \</object\>            |          |         |                    |              |
 ts                     | true     | long    | 时间戳                |              |

### 备注

- 如果不传page_index和page_size，默认只查第一页的20条数据，详情请看参数说明:

- order_id返回是18位，nodejs和javascript默认解析18有问题，nodejs和javascript里面JSON.parse默认是int，超过18位的数字用json-bigint的包解析。

## 闪电平仓下单

- POST `api/v1/lightning_close_position`
 
### 请求参数

   参数名称                |   是否必须  |   类型  |    描述            |   取值范围       |
----------------------- | -------- | ------- | ------------------ | -------------- |
 symbol | false | string | 品种代码	 | "BTC","ETH"... |
 contract_type | false | string | 合约类型 | “this_week”:当周，“next_week”:次周，“quarter”:季度|
 contract_code | false | string | 合约代码 | BTC190903 |
 volume | true | int | 委托数量（张） |  |
 direction | true | string | “buy”:买，“sell”:卖 |  |
 client_order_id | false | int | （API）客户自己填写和维护，必须保持唯一 |  |

> Response:

```json

{
  "status": "ok",
  "data": {
    "order_id": 633766664829804544,
    "order_id_str": "633766664829804544",
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
order_id | true  | bigint | 订单ID[用户级别的，不同的用户order_id可能相同] |  |
order_id_str | true  | string | String类型订单ID |  |
client_order_id | false | int | 用户自己的订单id |  |
\</data\> |  |  |  |  |


> 错误信息：

```json

{
    "status": "error",
    "err_code": 20012,
    "err_msg": "invalid symbol",
    "ts": 1490759594752
}

```

# 合约划转接口

## 现货-合约账户间进行资金的划转

### 实例

- POST `https://api.huobi.pro/v1/futures/transfer`

### 备注

此接口用户币币现货账户与合约账户之间的资金划转。

从现货现货账户转至合约账户，类型为`pro-to-futures`; 从合约账户转至现货账户，类型为`futures-to-pro`

该接口的访问频次的限制为1分钟10次。

注意：请求地址为火币Global地址

### 请求参数

  参数名称   |  是否必须    |  类型   |  描述  |  默认值    |  取值范围  |
--------------  | --------------  | ---------- |  ------------------------  | ------------  | ------------------------------------------------------------------------------------------------------  |
currency  |    true  |  string  |  币种  |   e.g. btc  |
amount  |   true  |  Decimal  |   划转金额  |      |
type  |  true  |  string  |   划转类型   |  从合约账户到现货账户：“futures-to-pro”，从现货账户到合约账户： “pro-to-futures”  |

> Response:

```
   正确的返回：
	{
	"status": "ok",
	"data":56656,
   }
	错误的返回：
	{
	"status": "error",
	"data":null,
	"err-code":"dw-account-transfer-error",
	"err-msg":"由于其他服务不可用导致的划转失败"
  }

```

###  返回参数

参数名称  |  是否必须     |  类型    |  描述  |  取值范围  |
------------------ |  -------------- |  ---------- |  ---------------------  |  -----------------------------  |
status  |  true  |   string  |  状态  |  ok, error  |  
data  |    true  |   long    |    生成的划转订单id  |  |
err-code  |  true  |   string  |  错误码  |  具体错误码请见列表  |
err-msg  |    true  |  string  |  错误消息  |  具体错误码请见列表  |

## err-code列表

err-code | err-msg(中文） | err-msg(English)  |  补充说明   |
------------------ | ------------------------------------ | --------------------------------  |  ----------------------------------- |
base-msg  |    |    |  其他错误，具体的err-msg, 请参照对应的错误消息列表  |
base-currency-error  |  币种无效  |  The currency is invalid  |           |
frequent-invoke  |  操作过于频繁，请稍后重试。（如果超过1分钟10次，系统返回该error-code） |  the operation is too frequent. Please try again later  |  如果请求次数超过1分钟10次，系统返回该error-code    |
banned-by-blacklist  |  黑名单限制  |  Blacklist restriction  |             |
dw-insufficient-balance  |  可划转余额不足，最大可划转 {0}。（币币账户的余额不足。） |  Insufficient balance. You can only transfer {0} at most.  |  币币账户的余额不足。     |
dw-account-transfer-unavailable  |  转账暂时不可用  |  account transfer unavailable  |  该接口暂时不可用     |
dw-account-transfer-error  |  由于其他服务不可用导致的划转失败  |  account transfer error  |              |
dw-account-transfer-failed  |  划转失败。请稍后重试或联系客服 |  Failed to transfer. Please try again later.  |  由于系统异常导致的划转失败         |
dw-account-transfer-failed-account-abnormality  |  账户异常，划转失败。请稍后重试或联系客服  |  Account abnormality, failed to transfer。Please try again later.  |               |

## base-msg对应的err-msg列表

err-msg(中文） |  err-msg(English)  |  补充说明   |
------------------------------------  |  --------------------------------  |  ------------------------- |
用户没有入金权限  |  Unable to transfer in currently. Please contact customer service  |           |
用户没有出金权限  |  Unable to transfer out currently. Please contact customer service  |          |
合约状态异常，无法出入金  |  Abnormal contracts status. Can’t transfer  |            |
子账号没有入金权限，请联系客服  |  Sub-account doesn't own the permissions to transfer in. Please contact customer service  |         |
子账号没有出金权限，请联系客服  |  Sub-account doesn't own the permissions to transfer out. Please contact customer service  |        |
子账号没有划转权限，请登录主账号授权  |  The sub-account does not have transfer permissions. Please login main account to authorize  |       |
可划转余额不足  |  Insufficient amount available  |  合约账户的余额不足       |
单笔转出的数量不能低于{0}{1}  |  The single transfer-out amount must be no less than {0}{1}  |       |
单笔转出的数量不能高于{0}{1}  |  The single transfer-out amount must be no more than {0}{1}  |       |
单笔转入的数量不能低于{0}{1}  |  The single transfer-in amount must be no less than {0}{1}  |         |
单笔转入的数量不能高于{0}{1}  |  The single transfer-in amount must be no more than {0}{1}  |         |
您当日累计转出量超过{0}{1}，暂无法转出  |  Your accumulative transfer-out amount is over the daily maximum, {0}{1}. You can't transfer out for the time being   |         |
您当日累计转入量超过{0}{1}，暂无法转入  |  Your accumulative transfer-in amount is over the daily maximum, {0}{1}. You can't transfer in for the time being   |           |
您当日累计净转出量超过{0}{1}，暂无法转出  |  Your accumulative net transfer-out amount is over the daily maximum, {0}{1}. You can't transfer out for the time being   |          |
您当日累计净转入量超过{0}{1}，暂无法转入  |  Your accumulative net transfer-in amount is over the daily maximum, {0}{1}. You can't transfer in for the time being   |            |
超过平台当日累计最大转出量限制，暂无法转出  |  The platform's accumulative transfer-out amount is over the daily maximum. You can't transfer out for the time being   |              |
超过平台当日累计最大转入量限制，暂无法转入  |  The platform's accumulative transfer-in amount is over the daily maximum. You can't transfer in for the time being   |                |
超过平台当日累计最大净转出量限制，暂无法转出  |  The platform's accumulative net transfer-out amount is over the daily maximum. You can't transfer out for the time being   |         |
超过平台当日累计最大净转入量限制，暂无法转入  |  The platform's accumulative net transfer-in amount is over the daily maximum. You can't transfer in for the time being   |           |
划转失败，请稍后重试或联系客服  |  Transfer failed. Please try again later or contact customer service   |                     |
服务异常，划转失败，请稍后再试  |  Abnormal service, transfer failed. Please try again later   |                           |
您尚未开通合约交易，无访问权限  |  You don’t have access permission as you have not opened contracts trading   |                    |
合约品种不存在  |  This contract type doesn't exist.  |  没有相应币种的合约       |

    

# 合约Websocket简介

## 接口列表

  权限类型  |   接口数据类型   |  请求方法   |  类型    |  描述                     |  需要验签       |                                                                                                                                            
----------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |---------- |---------------------------- |--------------|
  读取   |  市场行情接口 |         market.$symbol.kline.$period  |      sub        |  订阅 KLine 数据              |  否  |
  读取   |  市场行情接口  |           market.$symbol.kline.$period  |              req        |  请求 KLine 数据              |  否  |
  读取   |  市场行情接口           |  market.$symbol.depth.$type  |               sub        |  订阅 Market Depth 数据       |  否  | 
  读取   |  市场行情接口           |  market.$symbol.detail  |               sub        |  订阅 Market detail 数据       |  否  |
  读取   |  市场行情接口           |  market.$symbol.trade.detail  |               req        |  请求 Trade detail 数据       |  否  |
  读取   |  市场行情接口           |  market.$symbol.trade.detail  |        sub |  订阅 Trade Detail 数据  |  否  | 
  交易   |  交易接口           |  orders.$symbol  |        sub |  订阅订单成交数据  | 是  | 
  读取   |  资产接口           |  accounts.$symbol  |        sub  |  订阅某个品种下的资产变动信息  | 是  | 
  读取   |  资产接口          |  positions.$symbol  |        sub  |  订阅某个品种下的持仓变动信息  | 是  | 
  读取   |  交易接口          |  liquidationOrders.$symbol  |        sub  |  订阅某个品种下的强平订单信息  | 是  | 

## 合约订阅地址

 合约站行情请求以及订阅地址为：wss://www.hbdm.com/ws
 
 合约站订单推送订阅地址：wss://api.hbdm.com/notification
 
 如果这个两个地址访问不了，可使用：合约站行情请求以及订阅地址为：wss://www.btcgateway.pro/ws
 
 合约站订单推送订阅地址：wss://api.btcgateway.pro/notification
 
 如果对合约订单推送订阅有疑问，可以参考[Demo](https://github.com/huobiapi/Futures-Java-demo)
 
## 访问次数限制

公开行情接口和用户私有接口都有访问次数限制

- 普通用户，需要密钥的私有接口，每个UID 3秒最多30次请求(该UID的所有币种和不同到期日的合约的所有私有接口共享3秒30次的额度)

- 其他非行情类的公开接口，比如获取指数信息，限价信息，交割结算、平台持仓信息等，所有用户都是每个IP3秒最多60次请求（所有该IP的非行情类的公开接口请求共享3秒60次的额度）

- 行情类的公开接口，比如：获取K线数据、获取聚合行情、市场行情、获取市场最近成交记录：

    （1） restful接口：同一个IP,  1秒最多200个请求 

    （2）  websocket：req请求，同一时刻最多请求50次；sub请求，无限制，服务器主动推送数据

- WebSocket私有订单成交推送接口(需要API KEY验签)

    一个UID最多同时建立10个私有订单推送WS链接。该用户在一个品种(包含该品种的所有周期的合约)上，仅需要维持一个订单推送WS链接即可。

    注意: 订单推送WS的限频，跟用户RESTFUL私有接口的限频是分开的，相互不影响。

api接口response中的header返回以下字段

- ratelimit-limit： 单轮请求数上限，单位：次数

- ratelimit-interval：请求数重置的时间间隔，单位：毫秒

- ratelimit-remaining：本轮剩余可用请求数，单位：次数

- ratelimit-reset：请求数上限重置时间，单位：毫秒 
 
 
# 合约WebSocket市场行情接口

## 订阅 KLine 数据

### 成功建立和 WebSocket API 的连接之后，向 Server发送如下格式的数据来订阅数据：


{
   
"req": "market.$symbol.kline.$period",
        
"id": "id generated by client",

"period": "K线周期",
        
"from": " type: long, 2017-07-28T00:00:00+08:00 至2050-01-01T00:00:00+08:00 之间的时间点，单位：秒",
        
"to": "type: long, 2017-07-28T00:00:00+08:00 至2050-01-01T00:00:00+08:00 之间的时间点，单位：秒，必须比 from 大"

}

### 请求参数

  参数名称  |    是否必须   |   类型  |   描述   |    默认值    |   取值范围
-------- | -------- | ------ | ------ | ------- |---------------------------------------- 
  symbol | true | string |交易对 | |如"BTC\_CW"表示BTC当周合约，"BTC\_NW"表示BTC次周合约，"BTC\_CQ"表示BTC季度合约|
  period | true | string | K线周期 | | 1min, 5min, 15min, 30min, 1hour,4hour,1day, 1mon|
  period | false | string | K线周期 | | 1min, 5min, 15min, 30min, 1hour,4hour,1day, 1mon|
  from   | true | long  |  开始时间 | | |
  to      | true | long | 结束时间 | | |
  
#### 备注

[t1, t5] 假设有 t1  ~ t5 的K线：

from: t1, to: t5, return [t1, t5].

from: t5, to: t1, which t5  > t1, return [].

from: t5, return [t5].

from: t3, return [t3, t5].

to: t5, return [t1, t5].

from: t which t3  < t  <t4, return [t4, t5].

to: t which t3  < t  <t4, return [t1, t3].

from: t1 and to: t2, should satisfy 1325347200  < t1  < t2  < 2524579200.

一次最多2000条。

> 订阅成功返回数据的例子：

```json
  {
  "id": "id1",
  "status": "ok",
  "subbed": "market.BTC_CQ.kline.1min",
  "ts": 1489474081631
  }

```

### 返回参数  

  参数名称  |    是否必须   |   类型  |   描述   |
-------------- | -----------------  | ---------- |  -------------- |
  rep  |       true         |  string  |   请求参数   | 
  status  |       true         |  string  |   状态   | 
  id  |       true         |  string  |   请求id   | 
  ts    |     true          | long   |  响应生成时间点，单位：毫秒     |           
  \<tick\>    |               |    |  tick数据集合    |            | 
  id    |     true          | long   |  ID     |            
  vol    |     true          | decimal   |  成交量张数     |            
  count    |     true          | decimal   |  开盘价     |            
  open    |     true          | decimal   |  成交笔数     |            
  close    |     true          | decimal   |  收盘价,当K线为最晚的一根时，是最新成交价     |            
  low    |     true          | decimal   |  最低价    |            
  high    |     true          | decimal   |  最高价    |            
  amount    |     true          | decimal   |  成交量(币), 即 sum(每一笔成交量(张)*单张合约面值/该笔成交价)    |            
  \</tick\>    |               |     |      |          

  

> 之后每当 KLine 有更新时，client 会收到数据：

```json
    
    {
     "rep": "market.BTC_CQ.kline.1min",
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
    
```

## 订阅 Market Depth 数据

### 成功建立和 WebSocket API 的连接之后，向 Server发送如下格式的数据来订阅数据：

{

"sub": "market.$symbol.depth.$type",

"id": "id generated by client"

}

正确订阅请求参数的例子：

    {
    "sub": "market.BTC_CQ.depth.step0",
    "id": "id5"
    }

### 请求参数

  参数名称**   |  是否必须    |  类型     |  描述      |  默认值     |  取值范围  |
  -------------- |   -------------- |  ---------- |  ------------ |  ------------ |  ---------------------------------------------------------------------------------  |
  symbol         |  true           |  string     |  交易对            |        |  如"BTC\_CW"表示BTC当周合约，"BTC\_NW"表示BTC次周合约，"BTC\_CQ"表示BTC季度合约.  |
  type           |  true           |  string     |  Depth 类型        |        |  (150档数据)  step0, step1, step2, step3, step4, step5（合并深度1-5）,step0时，不合并深度;(20档数据)  step6, step7, step8, step9, step10, step11（合并深度7-11）；step6时，不合并深度  |

### 备注

用户选择“合并深度”时，一定报价精度内的市场挂单将予以合并显示。合并深度仅改变显示方式，不改变实际成交价格。

### 返回参数
//todo




之后每当 depth 有更新时，client 会收到数据，例子：

```json

    {
     "ch": "market.BTC_CQ.depth.step0",
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
	       "ch": "market.BTC_CQ.depth.step0"
        }
    }
    
```

## 订阅 Market Detail 数据 </a>

### 成功建立和 WebSocket API 的连接之后，向 Server发送如下格式的数据来请求数据:

`{`

`"sub": "market.$symbol.detail",`

`"id": "id generated by client"`

`}`

### 请求参数

  参数名称**   |  是否必须**   |  类型     |  描述      |  默认值    |  取值范围  |
-------------- |  -------------- |  ---------- |  ------------ |  ------------ |  --------------------------------------------------------------------------------  |
  symbol         |  true           |  string     |  交易对      |              |  如"BTC\_CW"表示BTC当周合约，"BTC\_NW"表示BTC次周合约，"BTC\_CQ"表示BTC季度合约  |

订阅 Market Detail 数据请求参数的例子：

    {
     "sub": "market.BTC_CQ.detail",
     "id": "id6"
    }

### 返回参数

> 请求成功返回数据的例子：

```json

  {
	"ch": "market.BTC_CW.detail",
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

```

<br>

<br>
<br>
<br>
<br>
