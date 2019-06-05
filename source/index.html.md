---
title: Huobi API Reference v1.0

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://www.huobi.pro/apikey/'>Sign Up for a Huobi API key </a>
  - Login is required for creating an API key

includes:

search: true
---

# Introduction

## Documentation Summary

Welcome to the HuobiDM API! You can use our API to access all market data, trading, and account management endpoints.

We have code example in Shell! You can view code examples in the dark area to the right.

You can use the drop down list above to change the API version. You can also use the language option at the top right to switch documentation language.

## Market Maker Program

Market maker program gives clients with good market making strategy an opportunity to access customized trading fee structure.

<aside class="notice">
Market makers will not be able to use point cards, VIP rate, rebate or any other fee promotion.
</aside>

### Eligibility Criteria as a Market Maker on HuobiDM

1. You should possess good market strategy
2. You must have at least 5 BTC or equivalent assets, not including rebates in your account with HuobiDM

### Application Process as Market Maker on Huobidm

If you satisfied our eligibility criteria and is interested to participate in our market-making project, please email to MM_service@huobi.com with following information:

1. UIDs (not linked to any rebate program in any accounts)
2. Provide screenshot of trading volume for the past 30 days or VIP/corporate status with other Exchanges
3. A brief description in writing of your market-making strategy
 
# Huobi Derivative Market (HBDM) API Access Illustration

##  API List

API Type  |  Content Type  |  Context                                       |  Request Type  |  Desc                                        |  Signature Required  |
--------- | ---------------- | ------------------------------------------------ | ---------------- | ---------------------------------------------- | ---------------------- |
Restful   | Market Data      | api/v1/contract_contract_info      | GET              | Get Contracts Information                      | No                     |
Restful   | Market Data      | api/v1/contract_index           | GET              | Get contract Index Price Information           | No                     |
Restful   | Market Data      |  api/v1/contract_price_limit       | GET              | Get Contract Price Limits                      | No                     |
Restful   | Market Data      |  api/v1/contract_open_interest     | GET              | Get Contract Open Interest Information         | No                     |
Restful   | Market Data      |  /market/depth                 | GET              | Get Market Depth                               | No                     |
Restful   | Market Data      | /market/history/kline           | GET              | Get K-Line Data                                | No                     |
Restful   | Market Data      |  /market/detail/merged          | GET              | Get Market Data Overview                       | No                     |
Restful   | Market Data      |  /market/trade                 | GET              | The Last Trade of a Contract                   | No                     |
Restful   | Market Data      | /market/history/trade          | GET              | Request a Batch of Trade Records of a Contract | No                     |
Restful   | Account          |  api/v1/contract_account_info    | POST             | User’s Account Information                     | Yes                    |
Restful   | Account          | api/v1/contract_position_info   | POST             | User’s position Information                    | Yes                    |
Restful   | Trade            |  api/v1/contract_order           | POST             | Place an Order                                 | Yes                    |
Restful   | Trade            | api/v1/contract_batchorder       | POST             | Place a Batch of Orders                        | Yes                    |
Restful   | Trade            | api/v1/contract_cancel          | POST             | Cancel an Order                                | Yes                    |
Restful   | Trade            | api/v1/contract_cancelall        | POST             | Cancel All Orders                              | Yes                    |
Restful   | User Order Info  | api/v1/contract_order_info       | POST             | Get Information of an Order                    | Yes                    |
Restful   | User Order Info  |  api/v1/contract_order_detail  | POST             | Get Trade Details of an Order                  | Yes                    |
Restful   | User Order Info  |  api/v1/contract_openorders      | POST             | Get Current Orders                             | Yes                    |
Restful   | User Order Info  |  api/v1/contract_hisorders      | POST             | Get History Orders                             | Yes                    |
Restful   | User Order Info  |  api/v1/contract_matchresults    | POST             | Acquire History Match Results              | Yes |
Restful   | User Account  |  v1/futures/transfer     | POST             | Transfer margin between Spot account and Future account                          | Yes  |

##  Address

Address | Applicable sites | Applicable functions | Applicable trading pairs |
------ | ---- | ---- | ------ |
https://api.hbdm.com  | Huobi DM |    Market     | Trading pairs provided by Huobi DM  |

## Signature Authentication & Verification

### Signature Illustration

Considering that API requests may get tampered in the process of transmission, to keep the transmission secure, you have to use your API Key to do Signature Authentication for all private interface except for public interface (used for acuqiring basic information and market data), in this way to verify whether the parameters/ parameter value get tampered or not in the process of transmission

A legitimate request consists of following parts：

- Request address of method, i.e. visit server address--api.hbdm.com, e.g.:  api.hbdm.com/api/v1/contract_order

- API Access Key ID (AccessKeyId): Access Key of the API Key that you apply.

- Method of Signature (SignatureMethod): Based on the Hash Aggrement, users calculate the signature via HmacSHA256.

- aSignature Version (SignatureVersion): It adopts version 2 in terms of Signature Version.

- Timestamp (Timestamp): The time when you send the request (UTC time zone) : (UTC time zone) : (UTC time zone), e.g.: 2017-05-11T16:22:06

- Must-fill parameters & optional parameters: For each method, there are a group of must-fill parameters and optional parameters used to address the API request, which can be found in the illustration of each method as well as their meaning. Please note that, in terms of "Get" requests, it needs to do Signature calculation for all the original parameters in each method ; In terms of "Post" requests, no need to do Signature calculation for the original parameters in each method, which means only four parameters need to do Signature calculation in "Post" requests, i.e. AccessKeyId, SignatureMethod, SignatureVersion, Timestamp with other parameters placed in "body".

- Signature: The result of Signature calculation which is used to verify if signature is valid and not tampered.


### Create API Key

<a href='https://www.hbg.com/zh-cn/apikey/'>You could  create API Key at</a>

API Key consists of the following two parts.

- "Access Key", the Key used to visit API.
  
- "Secret Key", the Key used to do Signature authentication and verification (visible during application period).

<aside class="notice">
When create API Key, users could bind IP address, as the validity of unbond IP address is only 90 days.
</aside>
<aside class="notice">
API Key has operation authorization of trading, borrowing, deposit and withdrawal etc..
</aside>
<aside class="warning">
Both Access Key and Secret Key are closely related with account security, please do not disclose them to others for any reasons anytime.
</aside>


### Steps for Signature

Normative request for Signature calculation     Different contents will get totally different results when use HMAC to calculate Signature, therefore, please normalize the requests before doing Signature calculation. Take the request of inquering order details as an example:

query details of one order 

`https://api.hbdm.com/api/v1/contract_order?`

`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`&SignatureMethod=HmacSHA256`

`&SignatureVersion=2`

`&Timestamp=2017-05-11T15:19:30`

`&symbol=BTC`

#### 1. Request methods (GET/POST): add line breaker "\n".


`GET\n`

#### 2. Text the visit address in lowercase, adding line breake "\n"

`
api.hbdm.com\n
`

#### 3. Visit the path of methods, adding line breaker "\n"

`
/api/v1/contract_order\n
`

#### 4. Rank the parameter names according to the sequence of ASCII codes, for example, below is the parameters in original sequence and the new sequence:


`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`symbol=BTC`

`SignatureMethod=HmacSHA256`

`SignatureVersion=2`

`Timestamp=2017-05-11T15%3A19%3A30`

<aside class="notice">
Use UTF-8 to encode when it has already been encoded by URI with hexadecimals in Uppercase, e.g., ":" wiil be encoded to "%3A" while space to "%20".
</aside>
<aside class="notice">
Timestamp should be written in the form of YYYY-MM-DDThh:mm:ss and encoded with URI.
</aside>


#### 5. After ranking

`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`SignatureMethod=HmacSHA256`

`SignatureVersion=2`

`Timestamp=2017-05-11T15%3A19%3A30`

`symbol=BTC`

#### 6.  Following the sequence above, link parameters with "&"


`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30&symbol=BTC`

#### 7. Form the final character strings that need to do Signature calculation as following:

`GET\n`

`api.hbdm.com\n`

`/api/v1/contract_order\n`

`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30&symbol=BTC`


#### 8. Use the "request character strings" formed in the last step and your Secret Key to create a digital Signature.

`4F65x5A2bLyMWVQj3Aqp+B4w+ivaA7n5Oi2SuYtCJ9o=`

1. Take the request character string formed in the last step and API Secret Key as two parameters, encoding them with the Hash Function HmacSHA256 to get corresponding Hash value.

2. Encoding the Hash value with base-64 code, the result will be the digital Signature of this request.

#### 9. Add the digital Signature into the parameters of request path.

The final request sent to Server via API should be like:

`https://api.hbdm.com/api/v1/contract_order?AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&order-id=1234567890&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30&Signature=4F65x5A2bLyMWVQj3Aqp%2BB4w%2BivaA7n5Oi2SuYtCJ9o%3D`

1. Add all the must authentication parameters into the parameters of request path;

2. Add the digital Signature encoded with URL code into the path parameters with the parameter name of "Signature".

## API Rate Limit Illustration

Please note that, for both public interface and private interface, there are rate limits, more details are as below:
* Generally, the private interface rate limit of API key is at most 30 times every 3 second for each UID (this 30 times every 3 second rate limit is shared by all the altcoins contracts delivered by different date).
* For public interface used to get information of index, price limit, settlement, delivery, open positions and so on, the rate limit is 60 times every 3 second at most for each IP (this 60 times every 3 second public interface rate limit is shared by all the requests from that IP of non-marketing information, like above).
* In terms of public interface used to get candle chart data, the latest transaction record and information of aggregate market, order book and so on, the rate limit is as below:

    （1） For restful interface: 200 times/second for one IP at most.

    （2）For websocket: The rate limit for “req” request is 50 times at once. No limit for “sub” request as the data will be pushed by sever voluntarily.

* WebSoket, the private order push interface, requires API KEY Verification:

    Each UID can build at most create 10 WS connections for private order push at the same time. For each account, 
    contracts of the same underlying coin only need to subscribe one WS order push, e.g. users only need to create one WS 
    order push connection for BTC Contract which will automatically push orders of BTC weekly, BTC biweekly and BTC quarterly
    contracts. Please note that the rate limit of WS order push and RESTFUL private interface are separated from each other, with no relations.

* Will response following string for "header" via api 

    ratelimit-limit: the upper limit of requests per time, unit: time

    ratelimit-interval: reset interval (reset the number of request), unit: ms

    ratelimit-remaining: the left available request number for this round, unit: time

    ratelimit-reset: upper limit of reset time used to reset request number, unit: ms 

## Details of Each Error Code

Error Code | Error Details Description|
----- | ---------------------- |
403	|	invalid ID                |
1000|	system exception                |
1001|	system not on deck             |
1002|	query exception               |
1003|	redis operation exception           |
1010|	user not existing              |
1011|	user session not exists            |
1012|	user account not exists             |
1013|	contract type not exists             |
1014|	contract not exists               |
1015|	index price not exists            |
1016|	BBO price not exists             |
1017|	query order not exists             |
1030|	input error                |
1031|	illegal order source             |
1032|	beyond visit limits            |
1033|	wrong field value of contract period       |
1034|	wrong field value of order type          |
1035|	wrong field value of order direction           |
1036|	wrong closing/opening field value of  orders          |
1037|	invalid leverage ratio          |
1038|	order price beyond the requirement of minimum variable price        |
1039|	order price beyond the limits            |
1040|	illegal order quantity             |
1041|	order quantity beyond limits            |
1042|	long positions beyond limits            |
1043|	short positions beyond limits            |
1044|	beyond position limits            |
1045|	leverage ratio not in accordance with the leverage ratio of open positions    |
1046|	uninitialized open positions              |
1047|	lack of available margin             |
1048|	lack of open positions               |
1050|	repeated order id              |
1051|	no orders could be withdrawed               |
1052|	beyond the limits of bacth order quantity             |
1053|	cannot acquire contracts' latest price range      |
1054|	cannot acquire contracts' latest           |
1055|	cannot close positions for lack of equity             |
1056|	cannot place or withdraw orders during settlement       |
1057|	cannot place or withdraw orders during trading pause        |
1058|	cannot place or withdraw orders when trading suspended           |
1059|	cannot place or withdraw orders during delivery          |
1060|	cannot place or withdraw orders under no-trading status  |
1061|	cannot withdraw not existed orders          |
1062|	cannot repeatedly withdraw orders when in withdrawing status          |
1063|	cannot withdraw filled orders          |
1064|	order primary key duplication              |
1065|	user's order id is not integer           |
1066|	do not leave the field blank               |
1067|	illegal fields               |
1068|	output error                |
1069|	illegal order price             |
1100|	users do not have rights to open positions            |
1101|	users do not have rights to close positions            |
1102|	users do not have rights to deposit            |
1103|	users do not have rights to withdraw            |
1104|	without contract trading permission, you are banned to trade       |
1105|	with current contract trading permission, you are only allowed to close positions       |
1200|	login error                |
1220|	user has not onboarded Huobi DM or activate the account          |
1221|	lack of margin to open account              |
1222|	insufficient account opening days             |
1223|	account VIP level not high enough          |
1224|	account registration place restricted               |
1225|	unsuccessful account opening               |
1250|	token cannot acquire HT_token        |
1251|	cannot acquire BTC equivalent assets         |
1252|	cannot acquire spot assets            |
1077|	failed query of current contract assets during settlement and delivery    |
1078|	failed query of partial contracts' assets during settlement and delivery    |
1079|	failed query of current contract open positions during settlement and delivery    |
1080|	failed query of partial contract assets during settlement and delivery    |

## Code Demo

**REST**

- <a href='https://github.com/huobiapi/Futures-Java-demo'>Java</a>

- <a href='https://github.com/huobiapi/Futures-Python-demo'>Python</a>

- <a href='https://github.com/huobiapi/Futures-Go-demo'>Golang</a>

- <a href='https://github.com/huobiapi/Futures-CSharp-demo'>CSharp</a>

- <a href='https://github.com/huobiapi/Futures-PHP-demo'>PHP</a>

- <a href='https://github.com/huobiapi/Futures-Node.js-demo'>Node.js</a>

**Websocket**

- <a href='https://github.com/huobiapi/Futures-Java-demo/tree/master/WebSocket-JAVA-demo'>Java</a>

- <a href='https://github.com/huobiapi/Futures-Python-demo/tree/master/Websocket-Python3-demo'>Python</a>

- <a href='https://github.com/huobiapi/Futures-Node.js-demo/tree/master/WebSocket-Node.js-demo'>Node.js</a>

# HuobiDM Market Data interface

## Get Contract Info 

### Example              
                                   
- GET  `api/v1/contract_contract_info`

```shell
curl "https://api.hbdm.com/api/v1/contract_contract_info"      
```
                                                           
### Request Parameter

  Parameter Name   |   Type   |   Mandatory   |   Description   |
------------------ | -------- | ------------- | --------------- |
symbol             | string   | false         | "BTC","ETH"...  |
contract_type | string   | false      | "this_week","next_week", "quarter" |
contract_code | string   | false      | BTC180914|

### Note：

Note：If there is a number in the Contract Code row，inquiry with Contract_Code. If there is no number，inquiry by Symbol + Contract Type. One of the query conditions must be chosen.

> Response

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

### Returning Parameter

Parameter Name               |   Mandatory   |   Type   |   Description                                |   Value Range                                                |
------------------------------ | ------------- | -------- | --------------------------------------------- | ------------------------------------------------------------ |
status                         | true          | string   | Request Processing Result                     | "ok" , "error"                                               |
\<list\>(Attribute Name: data) |               |          |                                               |                                                              |
symbol                         | true          | string   | Product Code                                  | "BTC","ETH"...                                               |
contract_code                  | true          | string   | Contract Code                                 | "BTC180914" ...                                              |
contract_type                  | true          | string   | Contract Type                                 | "this_week","next_week", "quarter"                           |
contract_size                  | true          | decimal  | Contract Value (USD of one contract)          | 10, 100...                                                   |
price_tick                     | true          | decimal  | Minimum Variation of Contract Price           | 0.001, 0.01...                                               |
delivery_date                  | true          | string   | Contract Delivery Date                        | eg "20180720"                                                |
create_date                    | true          | string   | Contract Listing Date                         | eg "20180706"                                                |
contract_status                | true          | int      | Contract Status                               | 0: Delisting,1: Listing,2: Pending Listing,3: Suspension,4: Suspending of Listing,5: In Settlement,6: Delivering,7: Settlement Completed,8: Delivered,9: Suspended Listing |
\</list\>                      |               |          |                                               |                                                              |
ts                             | true          | long     | Time of Respond Generation，Unit：Millisecond |                                                              |


## Get Contract Index Price Information 

### Example                                                
                                                            
- GET `api/v1/contract_index` 

```shell
curl "https://api.hbdm.com/api/v1/contract_index?symbol=BTC" 
```

### Request Parameter

| Parameter Name | Parameter Type | Mandatory   |   Desc         |
| ------------------ | ------------------ | ------------- | -------------- |
| symbol             | string             | true          | "BTC","ETH"... |

> Response

```json
{
  "status":"ok",
  "data": [
     {
       "symbol": "BTC",
       "index_price":471.0817
      }
    ],
  "ts": 1490759594752
}
```

###  Returning Parameter  

|   Parameter Name               |   Mandatory   |   Type   |   Desc                                        |   Value Range   |
| ------------------------------ | ------------- | -------- | --------------------------------------------- | --------------- |
| status                         | true          | string   | Request Processing Result                     | "ok" , "error"  |
| \<list\>(Attribute Name: data) |               |          |                                               |                 |
| symbol                         | true          | string   | symbol                                        | "BTC","ETH"...  |
| index_price                    | true          | decimal  | Index Price                                   |                 |
| \</list\>                      |               |          |                                               |                 |
| ts                             | true          | long     | Time of Respond Generation，Unit：Millisecond |                 |

  
## Contract Price Limitation

###  Example      
                                                                          
- GET `api/v1/contract_price_limit` 
 
```shell
curl "https://api.hbdm.com/api/v1/contract_price_limit?symbol=BTC&contract_type=this_week"
```

###  Request Parameter  

|   Parameter Name   |   Parameter Type   |   Mandatory   |   Desc                                            |
| ------------------ | ------------------ | ------------- | ------------------------------------------------- |
| symbol             | string             | false         | "BTC","ETH"...                                    |
| contract_type      | string             | false         | Contract Type ("this_week","next_week","quarter") |
| contract_code      | string             | false         | BTC180914  ...                                    |

###  Note  ：

If there is a number in the Contract Code row，inquiry with Contract_Code. 
If there is no number，inquiry by Symbol + Contract Type. 
One of the query conditions must be chosen.

> Response

```json
{
  "status":"ok",
  "data": 
    {
      "symbol":"BTC",
      "high_limit":443.07,
      "low_limit":417.09,
      "contract_code":"BTC180914",
      "contract_type":"this_week"
     },
  "ts": 1490759594752
}
```

###  Returning Parameter  

|   Parameter Name               |   Mandatory   |   Type   |   Desc                                        |   Value Range                     |
| ------------------------------ | ------------- | -------- | --------------------------------------------- | --------------------------------- |
| status                         | true          | string   | Request Processing Result                     | "ok" ,"error"                     |
| \<list\>(Attribute Name: data) |               |          |                                               |                                   |
| symbol                         | true          | string   | Variety code                                  | "BTC","ETH" ...                   |
| high_limit                     | true          | decimal  | Highest Buying Price                          |                                   |
| low_limit                      | true          | decimal  | Lowest Selling Price                          |                                   |
| contract_code                  | true          | string   | Contract Code                                 | eg "BTC180914"  ...               |
| contract_type                  | true          | string   | Contract Type                                 | "this_week","next_week","quarter" |
| \<list\>                       |               |          |                                               |                                   |
| ts                             | true          | long     | Time of Respond Generation, Unit: Millisecond |                                   |


## Get Contract Open Interest Information

###  Example   
                                                                                 
- GET `api/v1/contract_open_interest` 

```shell
curl "https://api.hbdm.com/api/v1/contract_open_interest?symbol=BTC&contract_type=this_week"
```

###  Request Parameter  

|   Parameter Name   |   Parameter Type   |   Mandatory   |   Desc                                            |
| ------------------ | ------------------ | ------------- | ------------------------------------------------- |
| symbol             | string             | false         | "BTC","ETH"...                                    |
| contract_type      | string             | false         | Contract Type ("this_week","next_week","quarter") |
| contract_code      | string             | false         | BTC180914                                         |

> Response:

```json
{
  "status":"ok",
  "data":
    {
      "symbol":"BTC",
      "contract_type": "this_week",
      "volume":123,
      "amount":106,
      "contract_code": "BTC180914"
     },
  "ts": 1490759594752
}
```

###  Returning Parameter  

|   Parameter Name               |   Mandatory   |   Type   |   Desc                                        |   Value Range                     |
| ------------------------------ | ------------- | -------- | --------------------------------------------- | --------------------------------- |
| status                         | true          | string   | Request Processing Result                     | "ok" , "error"                    |
| \<list\>(Attribute Name: data) |               |          |                                               |                                   |
| symbol                         | true          | string   | Variety code                                  | "BTC", "ETH" ...                  |
| contract_type                  | true          | string   | Contract Type                                 | "this_week","next_week","quarter" |
| volume                         | true          | decimal  | Position quantity(amount)                     |                                   |
| amount                         | true          | decimal  | Position quantity(Currency)                   |                                   |
| contract_code                  | true          | string   | Contract Code                                 | eg "BTC180914"   ...              |
| \</list\>                      |               |          |                                               |                                   |
| ts                             | true          | long     | Time of Respond Generation, Unit: Millisecond |                                   |


## Get Market Depth

###  Example            
                                            
- GET `/market/depth` 

```shell
curl "https://api.hbdm.com/market/depth?symbol=BTC_CQ&type=step5"
```  

###  Request Parameter  

|   Parameter Name   |   Parameter Type   |   Mandatory   |   Desc                                                       |
| ------------------ | ------------------ | ------------- | ------------------------------------------------------------ |
| symbol             | string             | true          | e.g. "BTC_CQ" represents BTC “This Week”，"BTC_CQ" represents BTC “Next Week”，"BTC_CQ" represents BTC “Quarter” |
| type               | string             | true          | step0, step1, step2, step3, step4, step5（merged deep data 0-5）；when step is 0，deep data not merged |

>tick illustration:

```
"tick": {
    "id": Message id.
    "ts": Time of Message Generation, unit: millisecond
    "bids": Buying, [price(hanging unit price), vol(this price represent single contract)], According to the descending order of Price
    "asks": Selling, [price(hanging unit Price), vol(this price represent single contract)], According to the ascending order of Price  
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

###  Returning Parameter  

|   Parameter Name   |   Mandatory   |   Data Type   |   Desc                                                       |   Value Range   |
| ------------------ | ------------- | ------------- | ------------------------------------------------------------ | --------------- |
| ch                 | true          | string        | Data belonged channel，Format： market.period                |                 |
| status             | true          | string        | Request Processing Result                                    | "ok" , "error"  |
| asks               | true          | object        | Selling, [price(hanging unit Price), vol(this price represent single contract)], According to the ascending order of Price |                 |
| bids               | true          | object        | Buying, [price(hanging unit price), vol(this price represent single contract)], According to the descending order of Price |                 |
| ts                 | true          | number        | Time of Respond Generation，Unit：Millisecond                |                 |


## Get K-Line Data

###  Example     
                                                                   
- GET `/market/history/kline` 

```shell
curl "https://api.hbdm.com/market/history/kline?period=1min&size=200&symbol=BTC_CQ"
```

###  Request Parameter  

|   Parameter Name   |   Mandatory   |   Type   |   Desc               |   Default   |   Value Range                                                |
| ------------------ | ------------- | -------- | -------------------- | ----------- | ------------------------------------------------------------ |
| symbol             | true          | string   | Contract Name        |             | e.g. "BTC_CQ" represents BTC “This Week”，"BTC_CQ" represents BTC “Next Week”，"BTC_CQ" represents BTC “Quarter” |
| period             | true          | string   | K-Line Type          |             | 1min, 5min, 15min, 30min, 60min, 1hour,4hour,1day, 1mon      |
| size               | false         | integer  | Acquisition Quantity | 150         | [1,2000]                                                     |

> Data Illustration：

```
"data": [
  {
        "id": K-Line id,
        "vol": Transaction Volume(amount),
        "count": transaction count
        "open": opening Price
        "close": Closing Price, when the K-line is the latest one，it means the latest price
        "low": Lowest price
        "high": highest price
        "amount": transaction volume(currency), sum(every transaction volume(amount)*every contract value/transaction price for this contract)
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

###  Returning Parameter  

|   Parameter Name   |   Mandatory   |   Data Type   |   Desc                                        |   Value Range   |
| ------------------ | ------------- | ------------- | --------------------------------------------- | --------------- |
| ch                 | true          | string        | Data belonged channel，Format： market.period |                 |
| data               | true          | object        | KLine Data                                    |                 |
| status             | true          | string        | Request Processing Result                     | "ok" , "error"  |
| ts                 | true          | number        | Time of Respond Generation, Unit: Millisecond |                 |


##  Get Market Data Overview

###  Example            
                                         
- GET `/market/detail/merged`
   
```shell
curl "https://api.hbdm.com/market/detail/merged?symbol=BTC_CQ"
```


###  Request Parameter  

|   Parameter Name   |   Mandatory   |   Type   |   Desc        |   Default   |   Value Range                                                |
| ------------------ | ------------- | -------- | ------------- | ----------- | ------------------------------------------------------------ |
| symbol             | true          | string   | Contract Name |             | e.g. "BTC_CQ" represents BTC “This Week”，"BTC_CQ" represents BTC “Next Week”，"BTC_CQ" represents BTC “Quarter” |

> tick Illustration:

```
"tick": {
    "id": K-Line id,
    "vol": transaction volume（contract）,
    "count": transaction count
    "open": opening price,
    "close": Closing Price, when the K-line is the latest one，it means the latest price
        "low": Lowest price
        "high": highest price
        "amount": transaction volume(currency), sum(every transaction volume(amount)*every contract value/transaction price for this contract)
    "bid": [price of buying one (amount)],
    "ask": [price of selling one (amount)]

  }
```

> Response:

```json
{
  "ch": "market.BTC_CQ.detail.merged",
  "status": "ok",
  "tick": 
    {
      "vol":"13305",
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

###  Returning Parameter  

|   Parameter Name   |   Mandatory   |   Data Type   |   Desc                                                       |   Value Range   |
| ------------------ | ------------- | ------------- | ------------------------------------------------------------ | --------------- |
| ch                 | true          | string        | Data belonged channel，format： market.$symbol.detail.merged |                 |
| status             | true          | string        | Request Processing Result                                    | "ok" , "error"  |
| tick               | true          | object        | K-Line Data                                                  |                 |
| ts                 | true          | number        | Time of Respond Generation, Unit: Millisecond                |                 |


## The Last Trade of a Contract

###  Example   
                                          
- GET `/market/trade`   

```shell
curl "https://api.hbdm.com/market/trade?symbol=BTC_CQ"
```
 
###  Request Parameter  

|   Parameter Name   |   Mandatory   |   Type   |   Desc        |   Default   |   Value Range                                                |
| ------------------ | ------------- | -------- | ------------- | ----------- | ------------------------------------------------------------ |
| symbol             | true          | string   | Contract Name |             | e.g. "BTC_CQ" represents BTC “This Week”，"BTC_CQ" represents BTC “Next Week”，"BTC_CQ" represents BTC “Quarter” |

> Tick Illustration：

```
"tick": {
  "id": Message id,
  "ts": Latest Transaction time,
  "data": [
    {
      "id": Transaction id,
      "price": Transaction price,
      "amount": transaction amount,
      "direction": Active transaction direction,
      "ts": transaction time

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
        "amount": "1",
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

###  Returning Parameter  

|   Parameter Name   |   Mandatory   |   Type   |   Desc                                                      |   Default   |   Value Range   |
| ------------------ | ------------- | -------- | ----------------------------------------------------------- | ----------- | --------------- |
| ch                 | true          | string   | Data belonged channel，Format： market.$symbol.trade.detail |             |                 |
| status             | true          | string   |                                                             |             | "ok","error"    |
| tick               | true          | object   | Trade Data                                                  |             |                 |
| ts                 | true          | number   | Sending time                                                |             |                 |


## Request a Batch of Trade Records of a Contract

###  Example  
                                                            
- GET `/market/history/trade`
   
```shell 
curl "https://api.hbdm.com/market/history/trade?symbol=BTC_CQ&size=100"
```

###  Request Parameter  

|   Parameter Name   |   Mandatory   |   Data Type   |   Desc                                |   Default   |   Value Range                                                |
| ------------------ | ------------- | ------------- | ------------------------------------- | ----------- | ------------------------------------------------------------ |
| symbol             | true          | string        | Contract Name                         |             | e.g. "BTC_CQ" represents BTC “This Week”，"BTC_CQ" represents BTC “Next Week”，"BTC_CQ" represents BTC “Quarter” |
| size               | false         | number        | Number of Trading Records Acquisition | 1           | [1, 2000]                                                    |

> data Illustration：

```
"data": {
  "id": Message id,
  "ts": Latest transaction time,
  "data": [
    {
      "id": Transaction id,
      "price": transaction price,
      "amount": transaction (amount),
      "direction": active transaction direction
      "ts": transaction time
      }
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
         "amount": 1,
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

###  Returning Parameter  

|   Parameter Name   |   Mandatory   |   Data Type   |   Desc                                                      |   Value Range   |
| ------------------ | ------------- | ------------- | ----------------------------------------------------------- | --------------- |
| ch                 | true          | string        | Data belonged channel，Format： market.$symbol.trade.detail |                 |
| data               | true          | object        | Trade Data                                                  |                 |
| status             | true          | string        |                                                             | "ok"，"error"   |
| ts                 | true          | number        | Time of Respond Generation, Unit: Millisecond               |                 |

# HuobiDM Account Interface

## User’s Account Information

###  Example          
                                      
- POST `api/v1/contract_account_info`  

###  Request Parameter  

|   Parameter Name   |   Mandatory   |   Type   |   Desc       |   Default   |   Value Range                                           |
| ------------------ | ------------- | -------- | ------------ | ----------- | ------------------------------------------------------- |
| symbol             | false         | string   | Variety code |             | "BTC","ETH"...if default, return to all types defaulted |

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
      "liquidation_price": 100
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
      "liquidation_price": 100
     }
   ],
  "ts":158797866555
}
```

###  Returning Parameter  

|   Parameter Name               |   Mandatory   |   Type   |   Desc                                        |   Value Range   |
| ------------------------------ | ------------- | -------- | --------------------------------------------- | --------------- |
| status                         | true          | string   | Request Processing Result                     | "ok" , "error"  |
| \<list\>(Attribute Name: data) |               |          |                                               |                 |
| symbol                         | true          | string   | Variety code                                  | "BTC","ETH"...  |
| margin_balance                 | true          | decimal  | Account rights                                |                 |
| margin_position                | true          | decimal  | Position Margin                               |                 |
| margin_frozen                  | true          | decimal  | Freeze margin                                 |                 |
| margin_available               | true          | decimal  | Available margin                              |                 |
| profit_real                    | true          | decimal  | Realized profit                               |                 |
| profit_unreal                  | true          | decimal  | Unrealized profit                             |                 |
| risk_rate                      | true          | decimal  | risk rate                                     |                 |
| liquidation_price              | true          | decimal  | Estimated liquidation price                   |                 |
| withdraw_available             | true          | decimal  | Available withdrawal                          |                 |
| lever_rate                     | true          | decimal  | Leverage Rate                                 |                 |
| \</list\>                      |               |          |                                               |                 |
| ts                             | number        | long     | Time of Respond Generation, Unit: Millisecond |                 |



## User’s Position Information

###  Example                           
                     
- POST  `api/v1/contract_position_info` 

### Request Parameter  

|   Parameter Name   |   Mandatory   |   Type   |   Desc       |   Default   |   Value Range                                           |
| ------------------ | ------------- | -------- | ------------ | ----------- | ------------------------------------------------------- |
| symbol             | false         | string   | Variety code |             | "BTC","ETH"...if default, return to all types defaulted |

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

### Returning Parameter  

|   Parameter Name               |   Mandatory   |   Type   |   Desc                                        |   Value Range                       |
| ------------------------------ | ------------- | -------- | --------------------------------------------- | ----------------------------------- |
| status                         | true          | string   | Request Processing Result                     | "ok" , "error"                      |
| \<list\>(Attribute Name: data) |               |          |                                               |                                     |
| symbol                         | true          | string   | Variety code                                  | "BTC","ETH"...                      |
| contract_code                  | true          | string   | Contract Code                                 | "BTC180914" ...                     |
| contract_type                  | true          | string   | Contract Type                                 | "this_week", "next_week", "quarter" |
| volume                         | true          | decimal  | Position quantity                             |                                     |
| available                      | true          | decimal  | Available position can be closed              |                                     |
| frozen                         | true          | decimal  | frozen                                        |                                     |
| cost_open                      | true          | decimal  | Opening average price                         |                                     |
| cost_hold                      | true          | decimal  | Average price of position                     |                                     |
| profit_unreal                  | true          | decimal  | Unrealized profit and loss                    |                                     |
| profit_rate                    | true          | decimal  | Profit rate                                   |                                     |
| profit                         | true          | decimal  | profit                                        |                                     |
| position_margin                | true          | decimal  | Position margin                               |                                     |
| lever_rate                     | true          | int      | Leverage rate                                 |                                     |
| direction                      | true          | string   | Transaction direction                         |                                     |
| last_price                     | true          | decimal  | Latest price                                  |                                     |
| \</list\>                      |               |          |                                               |                                     |
| ts                             | true          | long     | Time of Respond Generation, Unit: Millisecond |                                     |


# HuobiDM Trade Interface

##  Place an Order 

###  Example  

- POST `api/v1/contract_order`

###  Request Parameter  

|   Parameter Name   |   Parameter Type   |   Mandatory   |   Desc                                                       |
| ------------------ | ------------------ | ------------- | ------------------------------------------------------------ |
| symbol             | string             | false         | "BTC","ETH"...                                               |
| contract_type      | string             | false         | Contract Type ("this_week": "next_week": "quarter":)         |
| contract_code      | string             | false         | BTC180914                                                    |
| client_order_id    | long               | false         | Clients fill and maintain themselves, and this time must be greater than last time |
| price              | decimal            | true          | Price                                                        |
| volume             | long               | true          | Numbers of orders (amount)                                   |
| direction          | string             | true          | Transaction direction                                        |
| offset             | string             | true          | "open", "close"                                              |
| lever_rate         | int                | true          | Leverage rate [if“Open”is multiple orders in 10 rate, there will be not multiple orders in 20 rate |
| order_price_type   | string             | true          | "limit", "opponent"，"post_only"                                          |

###  Note ： 

If there is a number in the Contract Code row，inquiry with Contract_Code. 

If there is no number，inquiry by Symbol + Contract Type.

Description of post_only: assure that the maker order remains as maker order, it will not be filled immediately with the use of post_only, for the match system will automatically check whether the price of the maker order is higher/lower than the opponent first price, i.e. higher than bid price 1 or lower than the ask price 1. If yes, the maker order will placed on the orderbook, if not, the maker order will be cancelled.

open long: direction - buy、offset - open

close long: direction -sell、offset - close

open short: direction -sell、offset - open

close short: direction -buy、offset - close

> Response:

```json
{
  "status": "ok",
  "order_id": 986,
  "client_order_id": 9086,
  "ts": 158797866555
}
```


###  Returning Parameter  

|   Parameter Name   |   Mandatory   |   Type   |   Desc                                                       |   Value Range   |
| ------------------ | ------------- | -------- | ------------------------------------------------------------ | --------------- |
| status             | true          | string   | Request Processing Result                                    | "ok" , "error"  |
| order_id           | true          | long     | Order ID                                                     |                 |
| client_order_id    | true          | long     | the client ID that is filled in when the order is placed, if it’s not filled, it won’t be returned |                 |
| ts                 | true          | long     | Time of Respond Generation, Unit: Millisecond                |                 |


##  Place a Batch of Orders

###  Example  

- POST `/v1/contract_batchorder`

###  Request Parameter  

|   Parameter Name                      |   Parameter Type   |   Mandatory   |   Desc                                                       |
| ------------------------------------- | ------------------ | ------------- | ------------------------------------------------------------ |
| \<list\>(Attribute Name: orders_data) |                    |               |                                                              |
| symbol                                | string             | false         | "BTC","ETH"...                                               |
| contract_type                         | string             | false         | Contract Type: "this_week": "next_week": "quarter":          |
| contract_code                         | string             | false         | BTC180914                                                    |
| client_order_id                       | long               | true          | Clients fill and maintain themselves, and this time must be greater than last time |
| price                                 | decimal            | true          | Price                                                        |
| volume                                | long               | true          | Numbers of orders (amount)                                   |
| direction                             | string             | true          | Transaction direction                                        |
| offset                                | string             | true          | "open": "close"                                              |
| lever_rate                            | int                | true          | Leverage rate [if“Open”is multiple orders in 10 rate, there will be not multiple orders in 20 rate |
| order_price_type                      | string             | true          | "limit","opponent","post_only"                                        |
| \</list\>                             |                    |               |                                                              |

###  Note  ：

If there is a number in the Contract Code row,inquiry with Contract_Code. 

If there is no number,inquiry by Symbol + Contract Type.

Description of post_only: assure that the maker order remains as maker order, it will not be filled immediately with the use of post_only, for the match system will automatically check whether the price of the maker order is higher/lower than the opponent first price, i.e. higher than bid price 1 or lower than the ask price 1. If yes, the maker order will placed on the orderbook, if not, the maker order will be cancelled.

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
        "order_id":161256,
        "client_order_id":1344567
       },
      {
        "index":2,
        "order_id":161257,
        "client_order_id":1344569
       }
     ]
   },
  "ts": 1490759594752
}
```

###  Returning Parameter  

|   Parameter Name                  |   Mandatory   |   Type   |   Desc                                                       |   Value Range   |
| --------------------------------- | ------------- | -------- | ------------------------------------------------------------ | --------------- |
| status                            | true          | string   | Request Processing Result                                    | "ok" , "error"  |
| \<list\>(Attribute Name: errors)  |               |          |                                                              |                 |
| index                             | true          | int      | order Index                                                  |                 |
| err_code                          | true          | int      | Error code                                                   |                 |
| err_msg                           | true          | string   | Error information                                            |                 |
| \</list\>                         |               |          |                                                              |                 |
| \<list\>(Attribute Name: success) |               |          |                                                              |                 |
| index                             | true          | int      | order Index                                                  |                 |
| order_id                          | true          | long     | Order ID                                                     |                 |
| client_order_id                   | true          | long     | the client ID that is filled in when the order is placed, if it’s not filled, it won’t be returned |                 |
| \</list\>                         |               |          |                                                              |                 |
| ts                                | true          | long     | Time of Respond Generation, Unit: Millisecond                |                 |

## Cancel an Order 

###  Example   

- POST  `api/v1/contract_cancel`

###  Request Parameter  

|   Parameter Name   |   Mandatory   |   Type   |   Desc                                                       |
| ------------------ | ------------- | -------- | ------------------------------------------------------------ |
| order_id           | false         | string   | Order ID（different IDs are separated by ",", maximum 50 orders can be withdrew at one time） |
| client_order_id    | false         | string   | Client order ID (different IDs are separated by ",", maximum 50 orders can be withdrew at one time) |
| symbol             | true          | string   | "BTC","ETH"...                                               |

###  Note  ：

Both order_id and client_order_id can be used for order withdrawl，one of them needed at one time，if both of them are set，the default will be order id。

> Response: result of multiple order withdrawls (successful withdrew order ID, failed withdrew order ID)

```json
{
  "status": "ok",
  "errors":[
    {
      "order_id":161251,
      "err_code": "1002",
      "err_msg": "order doesn’t exist"
     },
    {
      "order_id":161253,
      "err_code": "1002",
      "err_msg": "order doesn’t exist"
     }
   ],
  "success":["161256","1344567"],
  "ts": 1490759594752
}
```

###  Returning Parameter  

|   Parameter Name                 |   Mandatory   |   Type   |   Desc                                                    |   Value Range   |
| -------------------------------- | ------------- | -------- | --------------------------------------------------------- | --------------- |
| status                           | true          | string   | Request Processing Result                                 | "ok" , "error"  |
| \<list\>(Attribute Name: errors) |               |          |                                                           |                 |
| order_id                         | true          | string   | Order ID                                                  |                 |
| err_code                         | true          | int      | Error code                                                |                 |
| err_msg                          | true          | string   | Error information                                         |                 |
| \</list\>                        |               |          |                                                           |                 |
| successes                        | true          | string   | Successfully withdrew list of order_id or client_order_id |                 |
| ts                               | true          | long     | Time of Respond Generation, Unit: Millisecond             |                 |


## Cancel All Orders 

###  Example  

- POST `api/v1/contract_cancelall`

> Request:
```json
{
 "symbol": "BTC"
}
```

###  Request Parameter  

|   Parameter Name   |   Mandatory   |   Type   |   Desc                          |
| ------------------ | ------------- | -------- | ------------------------------- |
| symbol             | true          | string   | Variety code，eg "BTC","ETH"... |
| contract_code             | false         | string   | contract_code            |
| contract_type             | false         | string   | contract_type           |

### Note

1.  Send symbol to cancel all the contracts of that kind of symbol, e.g. send “BTC” to cancel all BTC weekly, biweekly and quarterly contracts.

2.  Send contract_code to cancel the contracts of that code.

3.  Send symbol+contract_type to cancel the certain contracts under the symbol of that contract_type, e.g. send “BTC” and “this week”, then the BTC weekly contracts will be cancelled.

> Response:result of multiple order withdrawls (successful withdrew order ID, failed withdrew order ID)
 
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

> Error：

```json
{
  "status": "error",
  "err_code": 20012,
  "err_msg": "invalid symbol",
  "ts": 1490759594752
}
```

###  Returning Parameter  

|   Parameter Name                 |   Mandatory   |   Type   |   Desc                                        |   Value Range   |
| -------------------------------- | ------------- | -------- | --------------------------------------------- | --------------- |
| status                           | true          | string   | Request Processing Result                     | "ok" , "error"  |
| successes                        | true          | string   | Successful order                              |                 |
| \<list\>(Attribute Name: errors) |               |          |                                               |                 |
| order_id                         | true          | String   | Order ID                                      |                 |
| err_code                         | true          | int      | failed order error messageError code          |                 |
| err_msg                          | true          | int      | failed order information                      |                 |
| \</list\>                        |               |          |                                               |                 |
| successes                        | true          | string   | Successful order                              |                 |
| ts                               | true          | long     | Time of Respond Generation, Unit: Millisecond |                 |


## Get Information of an Order

###  Example   

- POST `api/v1/contract_order_info`

###  Request Parameter  

|   Parameter Name   |   Mandatory   |   Type   |   Desc                                                       |
| ------------------ | ------------- | -------- | ------------------------------------------------------------ |
| order_id           | false         | string   | Order ID（different IDs are separated by ",", maximum 20 orders can be withdrew at one time） |
| client_order_id    | false         | string   | Client order ID Order ID（different IDs are separated by ",", maximum 20 orders can be withdrew at one time) |
| symbol             | true          | string   | "BTC","ETH"...                                               |

###  Note  ：

Both order_id and client_order_id can be used for order withdrawl，one of them needed at one time，if both of them are set，the default will be order id。

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
      "order_id": 106837,
      "client_order_id": 10683,
      "order_source": "web",
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
      "order_id": 106837,
      "client_order_id": 10683,
      "order_source": "web",
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

###  Returning Parameter  

|   Parameter Name               |   Mandatory   |   Type   |   Desc                                                       |   Value Range                       |
| ------------------------------ | ------------- | -------- | ------------------------------------------------------------ | ----------------------------------- |
| status                         | true          | string   | Request Processing Result                                    | "ok" , "error"                      |
| \<list\>(Attribute Name: data) |               |          |                                                              |                                     |
| symbol                         | true          | string   | Variety code                                                 |                                     |
| contract_type                  | true          | string   | Contract Type                                                | "this_week", "next_week", "quarter" |
| contract_code                  | true          | string   | Contract Code                                                | "BTC180914" ...                     |
| volume                         | true          | decimal  | Numbers of order                                             |                                     |
| price                          | true          | decimal  | Price committed                                              |                                     |
| order_price_type               | true          | string   | Order price type [limited price，opponent price，market price] |                                     |
| direction                      | true          | string   | Transaction direction                                        |                                     |
| offset                         | true          | string   | "open": "close"                                              |                                     |
| lever_rate                     | true          | int      | Leverage rate                                                | 1\\5\\10\\20                        |
| order_id                       | true          | long     | Order ID                                                     |                                     |
| client_order_id                | true          | long     | Client order ID                                              |                                     |
| created_at                     | true          | long     | Creation time                                             |                                     |
| trade_volume                   | true          | decimal  | Transaction quantity                                         |                                     |
| trade_turnover                 | true          | decimal  | Transaction aggregate amount                                 |                                     |
| fee                            | true          | decimal  | Servicefee                                                   |                                     |
| trade_avg_price                | true          | decimal  | Transaction average price                                    |                                     |
| margin_frozen                  | true          | decimal  | Freeze margin                                                |                                     |
| profit                         | true          | decimal  | profit                                                       |                                     |
| status                         | true          | int      | Order status (1ready to submit 2ordered 3submitted 4partially transacted 5partially withdrew 6all transacted 7withdrew 11withdrawing) |                                     |
| order_source                   | true          | string   | Order source（1:system、2:web、3:api、4:m 5:risk、6:settlement） |                                     |
| \</list\>                      |               |          |                                                              |                                     |
| ts                             | true          | long     | Timestamp                                                    |                                     |



## Order details acquisition

###  Example   

- POST `api/v1/contract_order_detail`

###  Request Parameter  

|   Parameter Name   |   Mandatory   |   Type   |   Desc                        |
| ------------------ | ------------- | -------- | ----------------------------- |
| symbol             | true          | string   | "BTC","ETH"...                |
| order_id           | true          | long     | Order ID                      |
| createAt           | true          | long     | Timestamp                     |
| page_index         | false         | int      | Page number, default 1st page |
| page_size          | false         | int      | Default 20，no more than 50   |

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
    "order_id": 106837,
    "order_source": "web",
    "created_at": 1408076414000,
    "trades":[
      {
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

> Error:

```json
{
 "status":"error",
 "err_code":20029,
 "err_msg": "invalid symbol",
 "ts": 1490759594752
}
```

###  Returning Parameter 

|   Parameter Name                  |   Mandatory   |   Type   |   Desc                                                       |   Value Range                     |
| --------------------------------- | ------------- | -------- | ------------------------------------------------------------ | --------------------------------- |
| status                            | true          | string   | Request Processing Result                                    | "ok" , "error"                    |
| \<object\> (Attribute Name: data) |               |          |                                                              |                                   |
| symbol                            | true          | string   | Variety code                                                 |                                   |
| contract_type                     | true          | string   | Contract Type                                                | "this_week","next_week","quarter" |
| contract_code                     | true          | string   | Contract Code                                                | "BTC180914" ...                   |
| lever_rate                        | true          | int      | Leverage Rate                                                | 1\\5\\10\\20                      |
| direction                         | true          | string   | Transaction direction                                        |                                   |
| offset                            | true          | string   | "open": "close"                                              |                                   |
| volume                            | true          | decimal  | Number of Order                                              |                                   |
| price                             | true          | decimal  | Price committed                                              |                                   |
| created_at                        | true          | long     | Creation time                                             |                                   |
| order_source                      | true          | string   | Order Source                                                 |                                   |
| order_price_type                  | true          | string   | Order price type [limited price，opponent price，market price] |                                   |
| margin_frozen                     | true          | decimal  | Freeze margin                                                |                                   |
| profit                            | true          | decimal  | profit                                                       |                                   |
| total_page                        | true          | int      | Page in total                                                |                                   |
| current_page                      | true          | int      | Current Page                                                 |                                   |
| total_size                        | true          | int      | Total Size                                                   |                                   |
| \<list\> (Attribute Name: trades) |               |          |                                                              |                                   |
| trade_id                          | true          | long     | Match Result id                                              |                                   |
| trade_price                       | true          | decimal  | Match Price                                                  |                                   |
| trade_volume                      | true          | decimal  | Transaction quantity                                         |                                   |
| trade_turnover                    | true          | decimal  | Transaction price                                            |                                   |
| trade_fee                         | true          | decimal  | Transaction Service fee                                      |                                   |
| role                        | true          | string  |   taker or maker                              |                                                         |
| created_at                        | true          | long     | Creation time                                                |                                   |
| \</list\>                         |               |          |                                                              |                                   |
| \</object \>                      |               |          |                                                              |                                   |
| ts                                | true          | long     | Timestamp                                                    |                                   |


## Current unfilled commission acquisition

###  Example  

- POST  `api/v1/contract_openorders`

###  Request Parameter  

|   Parameter Name   |   Mandatory   |   Type   |   Desc                      |   Default   |   Value Range   |
| ------------------ | ------------- | -------- | --------------------------- | ----------- | --------------- |
| symbol             | false         | string   | Variety code                |             | "BTC","ETH"...  |
| page_index         | false         | int      | Page, default 1st page      | 1           |                 |
| page_size          | false         | int      | Default 20，no more than 50 | 20          |                 |

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
         "order_id": 106837,
         "client_order_id": 10683,
         "order_source": "web",
         "created_at": 1408076414000,
         "trade_volume": 1,
         "trade_turnover": 1200,
         "fee": 0,
         "trade_avg_price": 10,
         "margin_frozen": 10,
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

###  Returning Parameter  

|   Parameter Name               |   Mandatory   |   Type   |   Desc                                                       |   Value Range                     |
| ------------------------------ | ------------- | -------- | ------------------------------------------------------------ | --------------------------------- |
| status                         | true          | string   | Request Processing Result                                    |                                   |
| \<list\>(Attribute Name: data) |               |          |                                                              |                                   |
| symbol                         | true          | string   | Variety code                                                 |                                   |
| contract_type                  | true          | string   | Contract Type                                                | "this_week","next_week","quarter" |
| contract_code                  | true          | string   | Contract Code                                                | "BTC180914" ...                   |
| volume                         | true          | decimal  | Number of Order                                              |                                   |
| price                          | true          | decimal  | Price committed                                              |                                   |
| order_price_type               | true          | string   | Order price type [limited price，opponent price，market price] |                                   |
| direction                      | true          | string   | Transaction direction                                        |                                   |
| offset                         | true          | string   | "open": "close"                                              |                                   |
| lever_rate                     | true          | int      | Leverage Rate                                                | 1\\5\\10\\20                      |
| order_id                       | true          | long     | Order ID                                                     |                                   |
| client_order_id                | true          | long     | Client order ID                                              |                                   |
| created_at                     | true          | long     | Order Creation time                                          |                                   |
| trade_volume                   | true          | decimal  | Transaction quantity                                         |                                   |
| trade_turnover                 | true          | decimal  | Transaction aggregate amount                                 |                                   |
| fee                            | true          | decimal  | Servicefee                                                   |                                   |
| trade_avg_price                | true          | decimal  | Transaction average price                                    |                                   |
| margin_frozen                  | true          | decimal  | Freeze margin                                                |                                   |
| profit                         | true          | decimal  | profit                                                       |                                   |
| status                         | true          | int      | Order status (3didn’t transact 4partially transacted 5partially withdrew 6all transacted 7withdrew) |                                   |
| order_source                   | true          | string   | Order Source                                                 |                                   |
| \</list\>                      |               |          |                                                              |                                   |
| total_page                     | true          | int      | Total Pages                                                  |                                   |
| current_page                   | true          | int      | Current Page                                                 |                                   |
| total_size                     | true          | int      | Total Size                                                   |                                   |
| ts                             | true          | long     | Timestamp                                                    |                                   |

## Get History Orders

###  Example  

- POST `api/v1/contract_hisorders`

###  Request Parameter  

|   Parameter Name   |   Mandatory   |   Type   |   Desc                      |   Default   |   Value Range                                                |
| ------------------ | ------------- | -------- | --------------------------- | ----------- | ------------------------------------------------------------ |
| symbol             | true          | string   | Variety code                |             | "BTC","ETH"...                                               |
| trade_type         | true          | int      | Transaction type            |             | 0:all,1: buy long,2: sell short,3: buy short,4: sell  long,5: sell liquidation,6: buy liquidation,7:Delivery long,8: Delivery short |
| type               | true          | int      | Type                        |             | 1:All Orders,2:Order in Finished Status                      |
| status             | true          | int      | Order Status                |             | 0:all 3:unsettled, 4: partly transacted,5: partly transaction withdrawl,6: all transacted,7:withdrew |
| create_date        | true          | int      | Date                        |             | 7，90（7days or 90 days）                                    |
| page_index         | false         | int      | Page, default 1st page      | 1           |                                                              |
| page_size          | false         | int      | Default 20，no more than 50 | 20          |                                                              |

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
        "order_id": 106837,
        "client_order_id": 10683,
        "order_source": "web",
        "created_at": 1408076414000,
        "trade_volume": 1,
        "trade_turnover": 1200,
        "fee": 0,
        "trade_avg_price": 10,
        "margin_frozen": 10,
        "profit": 10,
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


###  Returning Parameter  

|   Parameter Name                 |   Mandatory   |   Type   |   Desc                                                       |   Value Range                     |
| -------------------------------- | ------------- | -------- | ------------------------------------------------------------ | --------------------------------- |
| status                           | true          | string   | Request Processing Result                                    |                                   |
| \<object\>(Attribute Name: data) |               |          |                                                              |                                   |
| \<list\>(Attribute Name: orders) |               |          |                                                              |                                   |
| order_id                         | true          | long     | Order ID                                                     |                                   |
| symbol                           | true          | string   | Variety code                                                 |                                   |
| contract_type                    | true          | string   | Contract Type                                                | "this_week","next_week","quarter" |
| contract_code                    | true          | string   | Contract Code                                                | "BTC180914" ...                   |
| lever_rate                       | true          | int      | Leverage Rate                                                | 1\\5\\10\\20                      |
| direction                        | true          | string   | Transaction direction                                        |                                   |
| offset                           | true          | string   | "open": "close"                                              |                                   |
| volume                           | true          | decimal  | Number of Order                                              |                                   |
| price                            | true          | decimal  | Price committed                                              |                                   |
| create_date                      | true          | long     | Creation time                                                |                                   |
| order_source                     | true          | string   | Order Source                                                 |                                   |
| order_price_type                 | true          | string   | Order price type [limited price，opponent price，market price] |                                   |
| margin_frozen                    | true          | decimal  | Freeze margin                                                |                                   |
| profit                           | true          | decimal  | profit                                                       |                                   |
| trade_volume                     | true          | decimal  | Transaction quantity                                         |                                   |
| trade_turnover                   | true          | decimal  | Transaction aggregate amount                                 |                                   |
| fee                              | true          | decimal  | Servicefee                                                   |                                   |
| trade_avg_price                  | true          | decimal  | Transaction average price                                    |                                   |
| status                           | true          | int      | Order Status                                                 |                                   |
| \</list\>                        |               |          |                                                              |                                   |
| \</object\>                      |               |          |                                                              |                                   |
| total_page                       | true          | int      | Total Pages                                                  |                                   |
| current_page                     | true          | int      | Current Page                                                 |                                   |
| total_size                       | true          | int      | Total Size                                                   |                                   |
| ts                               | true          | long     | Timestamp                                                    |                                   |

## Acquire History Match Results

###  Example 

- POST `api/v1/contract_matchresults`

### Request Parameter

Parameter Name |  Mandatory  |  Type  |  Desc                    |  Default  |  Value Range   
----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
symbol      | true     | string | contract types code          |         | "BTC","ETH"...                           |
trade_type  | true     | int    | trasanction types          |         |  0:All; 1: Open long; 2: Open short; 3: Close short; 4: Close long; 5: Liquidate long positions; 6: Liquidate short positions |
create_date | true     | int    | date            |         | 7, 90 (7 or 90 days)                            |
page_index  | false    | int    | page; if not enter, it will be the default value of the 1st page.  | 1       |                                          |
page_size   | false    | int    | if not enter, it will be the default value of 20; the number should ≤50 | 20      |                                          |

> Response:

```json
    {
     "data": {
		"current_page": 1,
		"total_page": 1,
		"total_size": 2,
		"trades": [{
			"contract_code": "EOS190419",
			"contract_type": "this_week",
			"create_date": 1555553626736,
			"direction": "sell",
			"match_id": 3635853382,
			"offset": "close",
			"offset_profitloss": 0.15646398812252696,
			"order_id": 1118,
			"symbol": "EOS",
			"trade_fee": -0.002897500905469032,
			"trade_price": 5.522,
			"trade_turnover": 80,
			"trade_volume": 8,
			"role": "maker"
		}]
	},
	"status": "ok",
	"ts": 1555654870867
    }
```

### Returning Parameter

 Parameter Name                |  Mandatory   |  Type  |  Desc                                                      | **Value Range**                   |
---------------------- | -------- | ------- | ------------------ | ------------ |
status                 | true     | string  | request handling result            |              |
\<object\>(attribute name: data: data) |          |         |                    |              |
\<list\>(attribute name: data: trades) |          |         |                    |              |
match_id               | true     | long    | traded ID               |              |
order_id               | true     | long    | order ID              |              |
symbol                 | true     | string  | contract type code               |              |
contract_type          | true     | string  | contract type               |  deliver on this Friday then "this_week"; deliver on next Friday then "next_week"; for quarterly contract then "quarter"  |
contract_code          | true     | string  | contract code              |  "BTC180914" ...       |
direction              | true     | string  | "buy": to bid/ go long; "sell": to ask/ go short.         |              |
offset                 | true     | string  | "open": open positions; "close": close positions           |              |
trade_volume           | true     | decimal | the number of traded contract with unit of lot               |              |
trade_price                  | true     | decimal | the price at which orders get filled               |              |
trade_turnover                  | true     | decimal | the number of total traded amout with number of USD               |              |
create_date            | true     | long    | the time when orders get filled               |              |
offset_profitloss                 | true     | decimal | profits and losses generated from closing positions                 |              |
traded_fee                    | true     | decimal | fees charged by platform                |              |
 role                        | true          | string |   taker or maker     |                  |
\</list\>              |          |         |                    |              |
total_page             | true     | int     | total pages                |              |
current_page           | true     | int     | current page                |              |
total_size             | true     | int     | total size of the list                |              |
\</object\>            |          |         |                    |              |
ts                     | true     | long    | timestamp                |              |

### Notice

- If users don’t upload/fill the page_index or page_size, it will automatically be set as the default value of the top 20 data on the first page, for more details, please follow the parameters illustration.

# HuobiDM Transferring Interface

##  Transfer margin between Spot account and Future account 

### Example

- POST `https://api.huobi.pro/v1/futures/transfer`

### Notice

This interface is used to transfer assets between Spot account and Future account.

The type is “pro-to-futures” when transferring assets from Spot account to Future; “futures-to-pro” when transferring from Future account to Spot account. 

API rate limit for this interface is up to 10 times per minute.

### Request Parameter

| Parameter Name  |  Mandatory  |  Type  |  Desc                    |  Default   |  Value Range  |  
| ----------- | -------- | ------ | ------------- | ------- | ---------------------------------------- |
| currency      | true     | string | currency          |         | e.g. btc                          |
| amount  | true     | Decimal    | Transferring amount         |         |   |
| type | true     | string  |  type of the transfer            |         | Transfer from Future account to Spot account: “futures-to-pro”  Transfer from Spot account to Future account: "pro-to-futures" |

> Response:

  ```
	{
	"status": "ok",
	"data":56656,
    }
	Error response
	{
	"status": "error",
	"data":null,
	"err-code":"dw-account-transfer-error",
	"err-msg":"account transfer error"
    }
	
 ```

### Returning Parameter

|  Parameter Name                |  Mandatory  |  Type  |  Desc         |  Value Range                    |
| ---------------------- | -------- | ------- | ------------------ | ------------ |
| status                 | true     | string  | Response status           | ok, error             |
| data               | true     | long    | Transfer ID             |       If status="error", data will be null.        |
| order_id               | true     | long    | order ID              |              |
| err-code                 | true     | string  | Error code              |              |
| err-msg          | true     | string  | Error code description              |   |


## Error Code Table

err-code | err-msg  |  Comments     |
------  | --------------------------------- |-----------------------------     |
base-msg|    |    Other errors, please refer to err-msg list below for details。
base-currency-error  |  The currency is invalid  |       |
frequent-invoke  |  the operation is too frequent. Please try again later  |                 |
banned-by-blacklist  |  Blacklist restriction  |                      |
dw-insufficient-balance  |  Insufficient balance. You can only transfer {0} at most.  |                   |
dw-account-transfer-unavailable  |  account transfer unavailable  |         |
dw-account-transfer-error  |  account transfer error  |               |
dw-account-transfer-failed  |  Failed to transfer. Please try again later.  |           |
dw-account-transfer-failed-account-abnormality  |  Account abnormality, failed to transfer。Please try again later.  |        |

## Error message when err-code is ‘base-msg’.

err-msg  |  Comments   |
----------------------- |----------------------------------    |
Unable to transfer in currently. Please contact customer service.  |         |
Unable to transfer out currently. Please contact customer service.  |        |
Abnormal contracts status. Can’t transfer.  |           |
Sub-account doesn't own the permissions to transfer in. Please contact customer service.  |            |
Sub-account doesn't own the permissions to transfer out. Please contact customer service.  |           |
The sub-account does not have transfer permissions. Please login main account to authorize.  |         |
Insufficient amount available.|Insufficient amount of Future Contract Account  |                       |
The single transfer-out amount must be no less than {0}{1}.  |         |
The single transfer-out amount must be no more than {0}{1}.  |         |
The single transfer-in amount must be no less than {0}{1}.  |          |
The single transfer-in amount must be no more than {0}{1}.  |          |                                                           
Your accumulative transfer-out amount is over the daily maximum, {0}{1}. You can't transfer out for the time being.  |              |
Your accumulative transfer-in amount is over the daily maximum, {0}{1}. You can't transfer in for the time being.  |                |
Your accumulative net transfer-out amount is over the daily maximum, {0}{1}. You can't transfer out for the time being.  |          |
Your accumulative net transfer-in amount is over the daily maximum, {0}{1}. You can't transfer in for the time being.  |            |
The platform's accumulative transfer-out amount is over the daily maximum. You can't transfer out for the time being.  |            |
The platform's accumulative transfer-in amount is over the daily maximum. You can't transfer in for the time being.  |              |
The platform's accumulative net transfer-out amount is over the daily maximum. You can't transfer out for the time being.  |        |
The platform's accumulative net transfer-in amount is over the daily maximum. You can't transfer in for the time being.  |          |
Transfer failed. Please try again later or contact customer service.  |       |
Abnormal service, transfer failed. Please try again later.  |           |
You don’t have access permission as you have not opened contracts trading.  |     |
This contract type doesn't exist.  |              |

# Websocket General

## API List

|**TYPE**|   **Market Type**   |**Context** |**Req Method**   |**Desc**                     |**Auth Required**        |
|----------- |------------------ |------------------------------------------------------------------------------------------------------------------------------------------------------------------- |---------- |---------------------------- |--------------|
|Websocket   |Market Interface |         market.$symbol.kline.$period|                                                                                                            sub        |Subscribe Candlestick Data              |No|
|Websocket   |Market Interface|           market.$symbol.kline.$period|                                                                                                                    req        |Request Candlestick Data              |No|
|Websocket   |Market Interface           |market.$symbol.depth.$type |                                                                                                                     sub        |Subscribe Market Depth Data        |No|
|Websocket   |Market Interface           |market.$symbol.detail |                                                                                                                     sub        |Subscribe Trade Detail Data       |No|
|Websocket   |Market Interface           |market.$symbol.trade.detail |                                                                                                                     req        |Request Trade Detail Data        |No|
|Websocket   |Market Interface           |market.$symbol.trade.detail|        sub |Subscribe Trade Detail Data   | No  |
|Websocket   |Trade Interface           |orders.$symbol|        sub |Subscribe Order Trade Data   | Yes  |
|Websocket   |accounts Interface           |accounts.$symbol|        sub |Subscribe accounts Data   | Yes  |
|Websocket   |accounts Interface           |positions.$symbol|        sub |Subscribe positions Data   | Yes  |

## Huobi DM subscription address

Market data request and subscription: wss://www.hbdm.com/ws

Order push subscription: wss://api.hbdm.com/notification

If you have further queries about Huobi DM order push subscription, please refer to the [Demo](https://github.com/huobiapi/Futures-Java-demo)

## API Rate Limit Illustration

Please note that, for both public interface and private interface, there are rate limits, more details are as below:
* Generally, the private interface rate limit of API key is at most 30 times every 3 second for each UID (this 30 times every 3 second rate limit is shared by all the altcoins contracts delivered by different date).
* For public interface used to get information of index, price limit, settlement, delivery, open positions and so on, the rate limit is 60 times every 3 second at most for each IP (this 60 times every 3 second public interface rate limit is shared by all the requests from that IP of non-marketing information, like above).
* In terms of public interface used to get candle chart data, the latest transaction record and information of aggregate market, order book and so on, the rate limit is as below:

    （1） For restful interface: 200 times/second for one IP at most.

    （2）For websocket: The rate limit for “req” request is 50 times at once. No limit for “sub” request as the data will be pushed by sever voluntarily.


* WebSoket, the private order push interface, requires API KEY Verification:

    Each UID can build at most create 10 WS connections for private order push at the same time. For each account, 
contracts of the same underlying coin only need to subscribe one WS order push, e.g. users only need to create one WS 
order push connection for BTC Contract which will automatically push orders of BTC weekly, BTC biweekly and BTC quarterly
contracts. Please note that the rate limit of WS order push and RESTFUL private interface are separated from each other, with no relations.

response following string for "header" via api 
* ratelimit-limit: the upper limit of requests per time, unit: time
* ratelimit-interval: reset interval (reset the number of request), unit: ms
* ratelimit-remaining: the left available request number for this round, unit: time
* ratelimit-reset: upper limit of reset time used to reset request number, unit: ms

## Authentication

### Authentication Description

Users need to create Access Key and Secret Key on Huobi Global, with Secret Key kept by users themselves and Access Key used to visit API secret key. As for now, in terms of the application and change of apikey, please create a new API Key under “Account-API Management”, filling in the note (optionally binding your IP) and clicking “Create”.  As Access Key is used to visit API secret key, Secret Key is used to request signature (only can be seen during the application). Users need to follow the rules to create Signature. To build the WS trading function connection, users need to get the authentication. Detailed formats are laid out below:

Important Note: Access Key and Secret Key are closely linked with account security, please not disclose to others. 

### Formats of authentication request

```json
  {
    "op": "auth",
    "type": "api",
    "AccessKeyId": "e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx",
    "SignatureMethod": "HmacSHA256",
    "SignatureVersion": "2",
    "Timestamp": "2017-05-11T15:19:30",
    "Signature": "4F65x5A2bLyMWVQj3Aqp+B4w+ivaA7n5Oi2SuYtCJ9o="
  }
```

###  Authentication request illustration

| Name         | Type   | Illustration                                                         |
| :--------------- | :----- | :----------------------------------------------------------- |
| op               | string | Required; operation name, the fixed value of authentication is "auth"                             |
| type             | string | Required; verification method with "api" standing for interface verification and "ticket" for end verification          |
| cid              | string | Required; Client requests the unique ID                                       |
| AccessKeyId      | string | Required if the type value is "api"; AccessKey is the API visit key API |
| SignatureMethod  | string | Required if the type value is "api"; Methods of signature, users calculate the signature based on the Hash aggreement, here utilizing "HmacSHA256"  |
| SignatureVersion | string | Required if the type value is "api"; signature aggreement version，here utilizing "2"              |
| Timestamp        | string | Required if the type value is "api"; timestamp, the time you send request (UTC time zone) put timestamp into your query request helping to prevent the third party intercept your request; e.g.: 2017-05-11T16:22:06. Please note (UTC time zone) |
| Signature        | string | Required if the type value is "api"; signature, calculated value to make sure signature valid and not tampered |
| ticket           | string | Required if the type value is "ticket"; response when login                           |

Note：

* In order to reduce the work of getting access to the interface, the authentication is executed via the same signature calculation as REST interface.
* Please pay attention to the case sensitivity
*  When the type is "api", parameters including op, type, cid and Signature do not join the calculation of Signature.
* In this Signature calculation, the fixed vauled of request method is "GET"; for other parameters please refer to REST interface Signature calculation document.

Steps：

Process of example parameter Signature calculation

* Please follow the request of Signature calculation, by using of HMAC, the different contents will turn out totally different results. Therefore, please standardize the requests before doing Signature calculation.

* Request methods (GET/POST): add line breaker of "\n".

  ```
  GET\n
  ```
* Text the visit address in lowercase, adding line breaker of "\n".
  ```
   api.hbdm.com\n

  ```

* Visit methods path, adding line breaker of "\n".

  ```
    /notification\n
  ```


* Rank the parameter names according to ASCII code (Use UTF-8 to encode when it has already encoded by URI. hexadecimal characters must capitalize, e.g. ":" will be encoded as "%3A" and space as "%20" ) . Below is the example of the original ranking of request parameters and the corresponding encoding forms.

  ```
  AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-
  7xxxx&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-
  11T15%3A19%3A30
  ```

* Following the sequence above, link the parameters with "&" 
  * The final character string used to do Signature calculation is laid out as below:
    * Signature calculation, add the two parameters into cryptographic hash function: the charactor string, Secret Key used to Signature calculation 
     
    * Encode the result of Signature calculation by Base64
  * Take the encoding result above as Signature parameter, encoding it with URI and then, adding it into API request.

### Format illustration of authentication response data 

| Name    | Type    | Illustration                                                 |
| :------- | :------ | :--------------------------------------------------- |
| op       | string  | Required；operation name，fixed value of authentication is "auth"                    |
| type     | string  | Required；respond according to the request parameters                       |
| cid      | string  | Required；if request includes cid then response will also include.                           |
| err-code | integer | If successful, respond with "0"; if not, respond other values; for detailed response code, please refer to appendix |
| err-msg  | string  | Optional，If wrong, it will lay out the error details                         |
| ts       | long    | Server-end response timestamp                                     |
| user-id  | long    | User id                                              |

> Sample of successful responded authentication 

```json
  {
    "op": "auth",
    "type":"api",
    "ts": 1489474081631,
    "err-code": 0,
    "data": {
      "user-id": 12345678
    }
  }
```

> Sample of failed responded authentication 


```json
  {
    "op": "auth",
    "type":"api",
    "ts": 1489474081631, 
    "err-code": "xxxx", 
    "err-msg": "error details"
  }
```

# Websocket Market Data

## General

### Market Heartbeat
WebSocket API supports two-way heartbeat. Both Server and Client can send ping message, which the opposite side can return with pong message.

> WebSocket Server sends heartbeat:

```json
{"ping": 18212558000}

```

> WebSocket Client should respond:

```json
 {"pong": 18212558000}

```

Note: The "pong"  value from the responded data is the sent "ping" value--Once the WebSocket Client and WebSocket Server get connected, the Server will send a heartbeat every 5 seconds (the frequency might change) to Websocket Client. It will get disconnected automatically if Websocket Client ignores the heartbeat message for 2 times. Websocket Server will remain the connection as Websocket Client sends one "ping" value of the latest 2 heartbeat message back. 


## Subscribe Candlestick Data

### Topic

After establish connection with WebSocket API, describing data formed as following to Server：

```json
  {                                      
    "sub": "market.$symbol.kline.$period", 
    "id": "id generate by client"          
  }
                                        
```
### Topic Parameter

|**Parameter**|   **Name**  | **Type**  | **Description** |  **Default Value**  | **Range**|
|--------------| -----------------| ---------- |----------| ------------| --------------------------------------------------------------------------------|
|symbol  |       true         |  string  |   Contract Symbol   |               |e.g. "BTC_CW" represents BTC “this_week”、"BTC_NW" represents BTC “next_week”、"BTC_CQ" represents BTC “quarter“|
|period    |     true          | string   | Kline Period |            |1min, 5min, 15min, 30min, 60min, 1day, 1mon, 1week, 1year|

### Example

> Example for correct subscription parameter：

```json
  {                                     
    "sub": "market.BTC_CQ.kline.1min",    
    "id": "id1"                           
  }  
                                     
```

> Example for correct subscription return parameter

```json
  {                                          
    "id": "id1",                               
    "status": "ok",                            
    "subbed": "market.BTC_CQ.kline.1min",      
    "ts": 1489474081631                        
  }                                          

```

> whenever KLine updated，client will receive the data，for example

```
   {                                                                                              
    "ch": "market.BTC_CQ.kline.1min",                                                             
    "ts": 1489474082831,                                                                          
    "tick":                                                                                       
       {                                                                                          
        "id": 1489464480,                                                                         
        "vol": 100,                                                                               
        "count": 0,                                                                               
        "open": 7962.62,                                                                          
        "close": 7962.62,                                                                         
        "low": 7962.62,                                                                           
        "high": 7962.62,                                                                          
        "amount": 0.3 //BTC quantity                                                              
       }                                                                                          
   }                                                                                              
                                                                                                  
   tick                                                                                           
                                                                                                  
   "tick":                                                                                        
     {                                                                                            
      "id": Kline id,                                                                             
      "vol": transaction (contract),                                                              
      "count": transaction count,                                                                 
      "open": opening price,                                                                      
      "close": closing price, when Kline is the last one, the price is the latest price           
      "low": lowest price,                                                                        
      "high": highest price,                                                                      
      "amount": BTC, sum(denomination of the contract* transaction amount/transaction price)      
   }                                                                                              

```

### Example for mistaken subscription

Mistaken subscription (mistaken symbol)

```json
  {                                                  
    "sub": "market.invalidsymbol.kline.1min",         
    "id": "id2"                                       
  }
                                                    
```

> Example for failed subscription and return parameter

```json
  {                                                               
   "id": "id2",                                                   
   "status": "error",                                             
   "err-code": "bad-request",                                     
   "err-msg": "invalid topic market.invalidsymbol.kline.1min",    
   "ts": 1494301904959                                            
  }  
                                                               
```

> Mistaken subscription (mistaken topic)

```json
    {                                     
     "sub": "market.BTC_CQ.kline.3min",   
     "id": "id3"                          
    }                                     

```

> Example for failed subscription and return parameter

```json
  {                                                                             
   "id": "id3",                                                                 
   "status": "error",                                                           
   "err-code": "bad-request",                                                   
   "err-msg": "invalid topic market.BTC_CQ.kline.3min",                         
   "ts": 1494310283622                                                          
  }                                                                             

```

## Request Candlestick Data

### Topic

Response：

```json
  {                                                                                                                         
   "req": "market.$symbol.kline.$period",                                                                                   
   "id": "id generated by client",                                                                                          
   "from": "optional, type: long, 2017-07-28T00:00:00+08:00 to 2050-01-01T00:00:00+08:00，unit：second",                      
   "to": "optional, type: long, 2017-07-28T00:00:00+08:00 to 2050-01-01T00:00:00+08:00，unit：second，must larger than from"
   } 

```

### Topic Parameter

|**Parameter**|   **Name**  | **Type**  | **Description** |  **Default Value**  | **Range**|
| -------- | -------- | ------ | ------ | ------- |---------------------------------------- |
| symbol | true | string |Contract Code | |e.g. "BTC_CW" represents BTC “this_week”、"BTC_NW" represents BTC “next_week”、"BTC_CQ" represents BTC “quarter“|
| period | true | string | Kline Period | | 1min, 5min, 15min, 30min, 60min, 1hour,4hour,1day, 1mon |

- [t1, t5] assumes that there is Kline oft1 ~ t5 ：

    from: t1, to: t5, return [t1, t5].
    from: t5, to: t1, which t5  > t1, return [].
    from: t5, return [t5].
    from: t3, return [t3, t5].
    to: t5, return [t1, t5].
    from: t which t3  < t  <t4, return [t4, t5].
    to: t which t3  < t  <t4, return [t1, t3].
    from: t1 and to: t2, should satisfy 1325347200  < t1  < t2  < 2524579200.

**NOTE**：maximum 2000 per time

### Example

> Example for Requesting parameter of KLine data：

```json
  {                                                
    "req": "market.BTC_CQ.kline.1min",               
    "id": "id4"                                      
  }      
                                            
```

> Example of successful requesting and return data：

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

## Subscribe Market Depth Data

### Topic

After establish connection with WebSocket API, describing data formed as following to Server：

```json
  {                                        
    "sub": "market.$symbol.depth.$type",     
    "id": "id generated by client"           
  }                                        
```

### Topic Parameter

|**Parameter**|   **Name**  | **Type**  | **Description** |  **Default Value**  | **Range**|
|-------------- |-------------- |---------- |------------ |------------ |---------------------------------------------------------------------------------|
|symbol         |true           |string     |Contract Code            |        |e.g. "BTC_CW" represents BTC “this_week”、"BTC_NW" represents BTC “next_week”、"BTC_CQ" represents BTC “quarter“.|
|type           |true           |string     |Depth Type        |        |step0, step1, step2, step3, step4, step5（merged depth 0-5）；step0 means doesn’t merge|

**NOTE**：When the user selects “Merged Depth”, the market pending orders within the certain quotation accuracy will be combined and displayed. The merged depth only changes the display mode and does not change the actual order price。

### Example

> Example of correct subscription of requesting parameter：

```json
  {                                      
    "sub": "market.BTC_CQ.depth.step0",    
    "id": "id5"                            
  }
                                        
```

> example of successful subscription and returning parameter：

```json
  {                                             
    "id": "id5",                                
    "status": "ok",                             
    "subbed": "market.BTC_CQ.depth.step0",      
    "ts": 1489474081631                         
  }                                             

```

> Whenever depth updated，client will receive data，for example：

```
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
                                                      
  tick illustration                                   
  "tick": {                                           
    "bids": [                                         
      [price of buy 1, amount of buy 1]               
      [price of buy 2, amount of buy 2]               
       //more data here                               
     ],                                               
     "asks": [                                        
      [price of sell 1, amount of sell 1]             
      [price of sell 2, amount of sell 2]             
      //more data here                                
     ]                                                
  }                                                   

```

## Subscribe Trade Detail Data

### Topic

After establish connection with WebSocket API, describing data formed as following to Server:

```json
  {                                    
    "sub": "market.$symbol.detail",     
    "id": "id generated by client"      
  } 
                                     
```
	
### Topic Parameter

|**Parameter**|   **Name**  | **Type**  | **Description** |  **Default Value**  | **Range**|
|-------------- |-------------- |---------- |------------ |------------ |--------------------------------------------------------------------------------|
|symbol         |true           |string     |Contract Code      |              |e.g. "BTC_CW" represents BTC “this_week”、"BTC_NW" represents BTC “next_week”、"BTC_CQ" represents BTC “quarter“.|

### Example

> Example of successful subscription of request parameter：

```json
  {                                  
   "sub": "market.BTC_CQ.detail",    
   "id": "id6"                       
  }    
                                
```

> Example of successful subscription and return parameter：

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

> tick illustration：

```
  "tick":                                                                                                   
       {                                                                                                    
         "id":  Kline id,                                                                                   
         "mrid": 1494496390000,                                                                             
         "vol": Trading volume,                                                                             
         "count": transaction count,                                                                        
         "open": opening price,                                                                             
         "close": closing price, when Kline is the last one, price is the latest price                      
         "low": Lowest Price,                                                                               
         "high": Highest Price,                                                                             
         "amount": Transaction amount(currency), sum(trading volume(amount)*denomination/transaction price) 
       }  
                                                                                                         
```

## Request Trade Detail Data

### Topic

Whenever depth updated，client will receive data，for example：

```json
  {                                         
    "req": "market.$symbol.trade.detail",    
    "id": "id generated by client"           
  }  
                                         
```

return Trade Detail

### Example

> Example for request parameter of requesting Market Detail Data：

```json
  {                                             
    "req": "market.BTC_CQ.trade.detail",         
    "id": "id8"                                  
  } 
                                              
```

> Example of successful request and return data：

```json
  {                                         
   "ch": "market.BTC_CQ.trade.detail",      
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

```

> tick date illustration：

```
  "data": [                                           
    {                                                 
     "id": message ID,                                
     "price": transaction price,                      
     "amount": transaction amount ,                   
     "direction": transaction direction,              
     "ts": timestamp                                  
    }                                                 
   ]
                                                     
```


## Subscribe Trade Detail Data

### Topic

After establish connection with WebSocket API, describing data formed as following to Server：

```json
  {                                              
    "sub": "market.$symbol.trade.detail",          
    "id": "id generated by client"                 
  }
                                                
```

**NOTE**：Can only obtain the latest 300 Trade Detail Data。

### Topic Parameter

|**Parameter**|   **Name**  | **Type**  | **Description** |  **Default Value**  | **Range**|
|-------------- |-------------- |---------- |---------- |------------ |--------------------------------------------------------------------------------|
|symbol         |true           |string     |Contract Name    |            |e.g. "BTC_CW" represents BTC “This Week”、"BTC_NW" represents BTC “Next Week”、"BTC_CQ" represents BTC “Quarter“.|

### Example

> Example of successful subscription of request parameter：

```json
  {                                            
   "sub": "market.BTC_CQ.trade.detail",        
   "id": "id7"                                 
  }  
                                            
```

> Example of successful subscription and return parameter：

```json
  {                                              
   "id": "id7",                                  
   "status": "ok",                               
   "subbed": "market.BTC_CQ.trade.detail",       
   "ts": 1489474081631                           
  }                                              

```

> Whenever Trade Detail updated，client will receive data，for example：

```json
  {                                            
    "ch": "market.BTC_NW.trade.detail",          
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

```

> data illustration：

```
  "data": [                                 
    {                                       
      "id": message ID,                      
      "price": transaction price,             
      "amount": transaction amount ,         
      "direction": transaction direction,    
      "ts": timestamp                        
    }                                       
  ]                                        

```
	 
# Websocket Asset and Order

## General

### Order Push Heartbeat

> WebSocket API supports one-way heartbeat. The Server initiates ping message and the Client will return pong message. The Server sends back a heartbeat:

```json
  {
    "op": "ping",
    "ts": 1492420473058
  }
  
```

> WebSocket Client should return:

```json
  {
    "op": "pong",
    "ts": 1492420473058
  }
  
```

Note: 
"ts" value in the return "pong" message is the "ts" value from "ping" push
Once the WebSocket Client and WebSocket Server connected, Websocket Server will send a heartbeat every 5 seconds (the frequency might change) to Wesocket Client. If WebSocket Client ignores the heartbeat message for 3 times, it will get disconnected with Websocket Sever automatically. 
Under abnormal conditions, WebSocket Server will return error message like:

```json
  {
    "op": "pong",
    "ts": 1492420473027,
    "err-code": 2011,
    "err-msg": "detailed error message"
  }
  
```

Websocket Server disconnects automatically
During period of building connection and authentication, Websocket Server will disconnect automatically if there is any error. The data structure before closing pushing are as below:

```
  {
    "op": "close", // indicate Websocket Server disconnected automatically 
    "ts": long   // The local timestamp of Server push
  }

```

Server return error but remain connection
After successful authentication, Server will return error but not disconnect if Client provides illegal Op or there is any internal error.

```
  {
    "op": "error", // indicate that receive illegal Op or internal error
    "ts": long// The local timestamp of Server push
  }
  
```

## Subscribe data（sub）

After successfully building WebSocket API connection, send data to Server in the formats as below to subscribe data:

### Data formats of subscription request

```json
  {
    "op": "sub",
    "cid": "id generated by client",
    "topic": "topic to sub"
  }

```

### Subscription request formats illustration

| Charactor string name | Type   | Illustration                                        |
| :------- | :----- | :------------------------------------------ |
| op       | string | Required；operation name, fixed value of subscription is "sub"             |
| cid      | string | Required; Client requests unique ID                     |
| topic    | string | Required；topic name of subscription, for detailed topic list, please refer to appendix |

### Sample of subscription request

> Correct subscription request

```json
  {
    "op": "sub",
    "cid": "40sG903yz80oDFWr",
    "topic": "orders.btc"
  }
  
```

> Response sample to successful subscription request

```json
  {
    "op": "sub",
    "cid": "40sG903yz80oDFWr",
    "err-code": 0,
    "ts": 1489474081631,
    "topic": "orders.btc"
  }
  
```

> Sample of incorrect subscription request (wrong topic)

```json
  {
    "op": "sub",
    "topic": "orders.bar",
    "cid": "40sG903yz80oDFWr"
  }
```

> Response sample of failed subscription request 

```json
  {
    "op": "sub",
    "topic": "orders.bar",
    "cid": "40sG903yz80oDFWr",
    "err-code": "xxxx", // For specific encoding, please refer to response code list 
    "err-msg": "Error details",
    "ts": 1489474081631
  }
  
```

### Data formats illustration of detailed information of filled orders  

```json
  {
    "op": "notify",
    "topic": "orders.btc", 
    "ts": 1489474082831, 
    "symbol": "BTC",
    "contract_type": "this_week",
    "contract_code": "BTC180914", 
    "volume": 111, 
    "price": 1111, 
    "order_price_type": "limit", 
    "direction": "buy",
    "offset": "open", 
    "status": 6, //order status( 3 submitted 4 partially filled 5 withdrawal with partially filled  6 fully filled 7 withdrawal)
    "lever_rate": 10, 
    "order_id": 106837, 
    "client_order_id": 10683, 
    "order_source": "web", 
    "order_type": 1, //Order type  (1:quotation 、2: withdrawal 、3: liquadation、4:delivery)
    "created_at": 1408076414000,
    "trade_volume": 1, 
    "trade_turnover": 1200, 
    "fee": 0, 
    "trade_avg_price": 10, 
    "margin_frozen": 10, 
    "profit": 2, 
    "trade":[{
        "trade_id":112,
        "trade_volume":1, 
        "trade_price":123.4555,
        "trade_fee":0.234, 
        "trade_turnover":34.123, 
        "created_at": 1490759594752, 
        "role": "maker"
      }]
  }
  
```

### Data formats illustration of orders push  

| Charactor string name                | Type    | Illustration                                                         |
| ----------------------- | ------- | ------------------------------------------------------------ |
| op                      | string  | Required; Operation name，fixed value of the push is "notify;                          |
| topic                   | string  | Required; Topic of the push                                             |
| ts                      | long    | Server-end response timestamp                                             |
| symbol                  | string  | Contract type ID                                                       |
| contract_type           | string  | Contract type                                                   |
| contract_code           | string  | Contract code                                                   |
| volume                  | decimal | Order volume                                                     |
| price                   | decimal | Order price                                                     |
| order_price_type        | string  | "limit", "opponent","post_only"   Position limit will be applied to post_only while order limit will not.                 |
| direction               | string  | "buy", "sell"                                        |
| offset                  | string  | "open", "close"                                       |
| status                  | int     | (1prepare to submit 2 prepare to submit 3 submitted 4 partially filled 5 withdrawal with partially filled  6 fully filled 7 withdrawal 11 during withdrawal) |
| lever_rate              | int     | Leverage ratio                                                     |
| order_id                | long    | Order ID                                                       |
| client_order_id         | long    | Client order ID                                                   |
| order_source            | int     | Order source） |
| order_type              | int     | Order type  1:Quotation 、 2: withdrawal 、 3: liquidation、4: delivery                 |
| created_at              | long    | Order created time                                                 |
| trade_volume            | decimal | Trade volume                                                     |
| trade_turnover          | decimal | Trade turnover                                                   |
| fee                     | decimal | fee                                                       |
| trade_avg_price         | decimal | Average price                                                     |
| margin_frozen           | decimal | Frozen margin                                                   |
| profit                  | decimal | Profit                                                         |
| <list>(属性名称: trade) |         |                                                              |
| trade_id                | long    | match result id, not unique, note:  one match result represents a trade set of one taker order and N maker orders, if the taker order matches with the N maker orders, it will generate N trades with same match result id                                                  |
| trade_volume            | decimal | Trade volume                                                      |
| trade_price             | decimal | Match price                                                     |
| trade_fee               | decimal | Trade fee                                                   |
| trade_turnover          | decimal | Trade turnover                                                     |
| created_at              | long    | Order filled time                                                 |
| role              | string  | taker or maker                                                |
| <list>                  |         |                                                              |


## Unsubscribe data (unsub)

After successfully building WebSocket API connection, send data to Server in the formats as below to unsubscribe data:

### Data formats of cancel subscription request

```json
  {
    "op": "unsub",
    "topic": "topic to unsub",
    "cid": "id generated by client"
  }

```

### Formats illustration of unsubscribing

| Name | Type   | Illustration                                               |
| :------- | :----- | :------------------------------------------------- |
| op       | string | Required; operation name, fixed value of unsubscribing "unsub";                 |
| cid      | string | optionally fill;Client requests unique ID                            |
| topic    | string | Required; topic name of the unsubscribing, detailed topic list please refer to the appendix; |

### Requset examples of cancel subscription

> The correct way to unsubscribe 

```json
  {
    "op": "unsub",
    "topic": "orders.btc",
    "cid": "40sG903yz80oDFWr"
  }
  
```

> Examples of return data when unsubscribe successufully

```json
  {
    "op": "unsub",
    "topic": "orders.btc",
    "cid": "id generated by client",
    "err-code": 0,
    "ts": 1489474081631
  }
```

### Subscribe and unsubscribe rules

| Subscribe (sub)      | Unsubscribe (ubsub) | Rules   |
| -------------- | --------------- | ------ |
| orders.*       | orders.*        | allowed   |
| orders.symbol1 | orders.*        | allowed   |
| orders.symbol1 | orders.symbol1  | allowed   |
| orders.symbol1 | orders.symbol2  | disallowed |
| orders.*       | orders.symbol1  | disallowed |


## Data of balances (sub)

After building connection with WebSocket API successfully, please send data in the following format to the Server to subscribe corresponding data:

### The required format for corresponding data subscription

```json
  {
    "op": "sub",
    "cid": "id generated by client",
    "topic": "topic to sub"
  }
  
```

### More illustration of the required format

| String Name | Type   | Illustration                                        |
| :------- | :----- | :------------------------------------------ |
| op       | string | Must fill；Operation name, the fixed value for subscription should be "sub"             |
| cid      | string | Must fill; Client unique ID for requests                     |
| topic    | string | Must fill；Must fill；Topic name of the subscription，Must fill (accounts.$symbol)  Subscribe/unsubscribe the assets changes information of one contract type; when the value of $symbol is "*" then it means subscribing/unsubscribing all contract types; |

### Sample for subscription request

> The correct subscription request

```json
  {
    "op": "sub",
    "cid": "40sG903yz80oDFWr",
    "topic": "accounts.btc"
  }           
  
```

> Response for successful subscription

```json
  {
    "op": "sub",
    "cid": "40sG903yz80oDFWr",
    "err-code": 0,
    "ts": 1489474081631,
    "topic": "accounts.btc"
  }

```

> Sample of incorrect subscription request（wrong topic）

```json
  {
    "op": "sub",
    "topic": "accounts.bar",
    "cid": "40sG903yz80oDFWr"
  }
  
```
> Response  data sample for failed subscription
 
```json
  {
    "op": "sub",
    "topic": "accounts.bar",
    "cid": "40sG903yz80oDFWr",
    "err-code": "xxxx", // For the specific code please refer to Error Code List  
    "err-msg": "Details of the error message",
    "ts": 1489474081631
  }
```

### Sample of return parameters  for assests change

```json
  {
      "op": "notify",          // Operation name
      "topic": "accounts",     // Topic
      "ts": 1489474082831,    
      "event": "order.match",
      "data":[
        {
          "symbol": "BTC",
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
          "lever_rate": 10
        }
     ]
  }
  
```

### String Illustration

| String Name                | Type    | Illustration                                                         |
| ----------------------- | ------- | ------------------------------------------------------------ |
| ts                        | long  | Response generation time, unit: millisecond                           |
| event                     | string  | Illustration for assets changes information, i.e., create order and open positions (order.open), orders matched (order.match) (except for liquidated, settled and delivered positions), Settlement and delivery (settlement), orders liquidated (order.liquidation)(net and positions taken-over), order canceled (order.cancel), contract account transferring (contract.transfer)(including external-transferring), system (contract.system), other assets changes (other), initial margin (init)                                              |
| symbol                    | string    | contract types code ,"BTC","ETH"...，when the value of $symbol is "*" means subscribing all types of contracts                                            |
| margin_balance            | decimal  | Account Equity                                                       |
| margin_static             | decimal  | Static Equity                                                     |
| margin_position           | decimal  | Position margin (the margin of open positions)                                                     |
| margin_frozen             | decimal | Frozen margin                                                     |
| margin_available          | decimal | Available margin                                                     |
| profit_real               | decimal  | Realized profits and losses               |
| profit_unreal             | decimal  | Unrealized profits and losses                                         |
| risk_rate                 | decimal  | Margin rate                                     |
| liquidation_price         | decimal     | Estimated liquidation price |
| withdraw_available        | decimal     | Available tranferring amount                                                  |
| lever_rate                | decimal    | Leverage ratios                                                    |


## Unsubscribe（ubsub）

After building connection with WebSocket API successfully, please send data in the following format to the Server to unsubscribe data:

### Request format of unsubscription

```json
  {
    "op": "unsub",
    "topic": "topic to unsub",
    "cid": "id generated by client"
  }

```

### Request format illustration of unsubscription 

| String Name | Type   | Illustration                                               |
| :------- | :----- | :------------------------------------------------- |
| op       | string | Must fill;Operation name, the fixed value for unsubscription should be "unsub" ;                 |
| cid      | string | Optional fill; Client unique ID for requests                             |
| topic    | string | Must fill;Must fill；Must fill；Topic name of the subscription，Must fill (accounts.$symbol)  Subscribe/unsubscribe the assets changes information of one contract type; when the value of $symbol is "*" then it means subscribing/unsubscribing all contract types; |

### Request sample of unsubscription 

> The correct request of unsubscription

```json
  {
    "op": "unsub",
    "topic": "accounts.btc",
    "cid": "40sG903yz80oDFWr"
  }     
  
```

> Response for successful unsubscription

```json
  {
    "op": "unsub",
    "topic": "accounts.btc",
    "cid": "id generated by client",
    "err-code": 0,
    "ts": 1489474081631
  }
  
```

###  Illustration for the rules of Subscription and Unsubscription

| Subscribe (sub)      | Unsubscribe (ubsub) | Rules   |
| -------------- | --------------- | ------ |
| accounts.*       | accounts.*        | Permit   |
| accounts.symbol1 | accounts.*        | Permit   |
| accounts.symbol1 | accounts.symbol1  | Permit   |
| accounts.symbol1 | accounts.symbol2  | Not permit |
| accounts.*       | accounts.symbol1  | Not permit |


## Subscribe Position Change Data (sub)

After building connection with WebSocket API successfully, please send data in the following format to the Server to subscribe:

### Request format of subscription

```json
  {
    "op": "sub",
    "cid": "id generated by client",
    "topic": "topic to sub"
  }      
  
```

### Request format illustration of subscribtion

| String Name | Type   | Illustration                                        |
| :------- | :----- | :------------------------------------------ |
| op       | string | Must fill；Operation name, the fixed value for subscription should be "sub"             |
| cid      | string | Optional fill; Client unique ID for requests                     |
| topic    | string | Must fill；Topic name of the subscription，Must fill (positions.$symbol)  Subscribe/unsubscribe the assets changes information of one contract type; when the value of $symbol is "*" then it means subscribing/unsubscribing all contract types; |

### Sample for subscription request

The correct subscription request

```json
  {
    "op": "sub",
    "cid": "40sG903yz80oDFWr",
    "topic": "positions.btc"
  }

```

> Response for successful subscription

```json
  {
    "op": "sub",
    "cid": "40sG903yz80oDFWr",
    "err-code": 0,
    "ts": 1489474081631,
    "topic": "positions.btc"
  }
  
```

> Sample for incorrect subscription request（Wrong topic）

```json
  {
    "op": "sub",
    "topic": "positions.bar",
    "cid": "40sG903yz80oDFWr"
  }
  
```

> Response  data sample for failed subscription

```json
  {
    "op": "sub",
    "topic": "positions.bar",
    "cid": "40sG903yz80oDFWr",
    "err-code": "xxxx", //For the specific code please refer to Error Code List  
    "err-msg": "Details of the error message",
    "ts": 1489474081631
  }
  
```

### Sample of return parameters  for position change

```json
  { 
    "op": "notify",           // Operation name
    "topic": "positions",     // Topic
    "ts": 1489474082831,   
    "event": "order.match",
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

### Return Parameter

| String Name                | Type    | Illustration                                                         |
| ----------------------- | ------- | ------------------------------------------------------------ |
| ts                     | long  | Response generation time, unit: millisecond                           |
| event                  | string  | Illustration for assets changes information, i.e., create order and open positions (order.open), orders matched (order.match) (except for liquidated, settled and delivered positions), Settlement and delivery (settlement), orders liquidated (order.liquidation)(net and positions taken-over), order canceled (order.cancel), contract account transferring (contract.transfer)(including external-transferring), system (contract.system), other assets changes (other), initial margin (init)   |
| symbol                 | string    | contract types code ,"BTC","ETH"...，when the value of $symbol is "*" means subscribing all types of contracts                                               |
| contract_code          | decimal  | Contract code                                                      |
| contract_type          | decimal  | Contract type, weekly: "this_week"; Biweekly:"next_week"; Quarterly:"quarter"; Already delivered: "delivered"                                                    |
| volume                 | decimal  | Open positions                                                     |
| available              | decimal | Available positions for closing                                                     |
| frozen                 | decimal | Frozen amount                                                    |
| cost_open              | decimal  | Average open price                |
| cost_hold              | decimal  | Average position price                                        |
| profit_unreal          | decimal  | Unrealized profits and losses                                        |
| profit_rate            | decimal     | Profit rate |
| profit                 | decimal     | Profit                                                     |
| position_margin        | decimal    | Position margin                                                       |
| lever_rate             | decimal     | Leverage ratios                                                 |
| direction              | decimal    | The trading direction: "buy", "sell"                                                   |


## Unsubscribe data (ubsub)

After building connection with WebSocket API successfully, please send data in the following format to the Server to unsubscribe data:

### Request format of unsubscription

```json
  {
    "op": "unsub",
    "topic": "topic to unsub",
    "cid": "id generated by client"
  }
  
```

### Request format illustration for unsubscription

| String Name | Type   | Illustration                                               |
| :------- | :----- | :------------------------------------------------- |
| op       | string | Must fill;Operation name, the fixed value for unsubscription should be "unsub" ;              |
| cid      | string | Optional fill; Client unique ID for requests                          |
| topic    | string | Must fill;Must fill；Must fill；Topic name of the subscription，Must fill (positions.$symbol), when the value of $symbol is "*" means subscribing all types of contracts;         |

### Sample for unsubscription request

> Correct request sample for unsubscription

```json
  {
    "op": "unsub",
    "topic": "positions.btc",
    "cid": "40sG903yz80oDFWr"
  }
  
```

> Response for successful unsubscription

```json
  {
    "op": "unsub",
    "topic": "positions.btc",
    "cid": "id generated by client",
    "err-code": 0,
    "ts": 1489474081631
  }
  
```

### Illustration for the rules of Subscription and Unsubscription

| Subsribe (sub)      | Unsubscribe (ubsub) | Rules   |
| -------------- | --------------- | ------ |
| positions.*       | positions.*        | permit   |
| positions.symbol1 | positions.*        | permit   |
| positions.symbol1 | positions.symbol1  | permit   |
| positions.symbol1 | positions.symbol2  | not permit |
| positions.*       | positions.symbol1  | not permit |

# Websocket Appendix

## Operation (OP) Type illustration

| Type   | Description                 |
| ------ | -------------------- |
| ping   | heartbeat initiate (server)     |
| pong   | heartbeat response             |
| auth   | authentication                 |
| sub    | subscribe information             |
| unsub  | unsubscribe         |
| notify | push subscription (server) |

## topic type illustration

| Type           | Operation type | Description                                                         |
| -------------- | ------------ | ------------------------------------------------------------ |
| orders.$symbol | sub,ubsub    | subscribe/unsubscribe to order change of specified trading pairs when the value of $symbol is "*" standing for subscribing all trading pairs |

## Err-Code illustration

| Error code | Error description                                 |
| ------ | ---------------------------------------- |
| 0      | Request successfully.                    |
| 2001   | Invalid authentication.                  |
| 2002   | Authentication required.                 |
| 2003   | Authentication failed.                   |
| 2004   | Number of visits exceeds limit.          |
| 2005   | Connection has been authenticated.       |
| 2010   | Topic error.                             |
| 2011   | Contract doesn't exist.                  |
| 2012   | Topic not subscribed.                    |
| 2013   | Authentication type doesn't exist.       |
| 2014   | Repeated subscription.                   |
| 2030   | Exceeds connection limit of single user. |
| 2040   | Missing required parameter.              |

</br>
</br>
</br>
</br>
</br>
