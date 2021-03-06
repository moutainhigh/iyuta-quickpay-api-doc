<h1>Xpay API文档</h1>

<!--ts-->
   * [Xpay API文档](#xpay-api文档)
      * [技术综述](#技术综述)
         * [请求格式说明](#请求格式说明)
         * [返回格式说明](#返回格式说明)
         * [接口地址](#接口地址)
         * [SDK(JAVA)下载](#sdkjava下载)
      * [接口介绍](#接口介绍)
         * [1. 获取调用token接口](#1-获取调用token接口)
         * [2. 快捷支付相关接口](#2-快捷支付相关接口)
            * [2.1 订单批次上传](#21-订单批次上传)
            * [2.2 订单批次触发支付](#22-订单批次触发支付)
            * [2.3 订单批次支付&amp;推送结果汇总查询](#23-订单批次支付推送结果汇总查询)
            * [2.4 单笔订单回执查询](#24-单笔订单回执查询)
            * [2.5 订单批次回执查询](#25-订单批次回执查询)
            * [2.6 单笔订单创建并请求支付](#26-单笔订单创建并请求支付)
            * [2.7 单笔订单请求重新安排支付](#27-单笔订单请求重新安排支付)
            * [2.8 单笔订单创建](#28-单笔订单创建)
         * [3. 接收异步通知](#3-接收异步通知)
            * [3.1 配置异步通知接收参数](#31-配置异步通知接收参数)
            * [3.2 消息签名方法](#32-消息签名方法)
            * [3.3 消息重发机制](#33-消息重发机制)
            * [3.4 支付状态异步通知](#34-支付状态异步通知)
            * [3.5 申报状态异步通知](#35-申报状态异步通知)
         * [4. 二维码收单](#4-二维码收单)
            * [4.1 创建订单并生成支付二维码](#41-创建订单并生成支付二维码)
            * [4.2 生成/刷新二维码](#42-生成刷新二维码)
            * [4.3 订单查询](#43-订单查询)
         * [5. 银行卡快捷支付收单](#5-银行卡快捷支付收单)
            * [5.1 快捷签约申请](#51-快捷签约申请)
            * [5.2 签约申请确认](#52-签约申请确认)
            * [5.3 创建订单并使用快捷协议进行支付](#53-创建订单并使用快捷协议进行支付)
            * [5.4 支付短信确认](#54-支付短信确认)
            * [5.5 重新申请支付和获取支付短信](#55-重新申请支付和获取支付短信)
            * [5.6 订单查询](#56-订单查询)
         * [6. 配单支付推单](#6-配单支付推单)
            * [6.1 创建订单并触发配单支付](#61-创建订单并触发配单支付)
            * [6.2 重新进行配单支付](#62-重新进行配单支付)
            * [6.3 订单查询](#63-订单查询)
            * [6.4 订单批次触发配单支付](#64-订单批次触发配单支付)
         * [7. 实名认证](#7-实名认证)
            * [7.1 身份证二要素认证](#71-身份证二要素认证)
         * [8. 支付信息推单](#8-支付信息推单)
            * [8.1 支付信息海关推单](#81-支付信息海关推单)
         * [9. 退款](#9-退款)
            * [9.1 退款申请](#91-退款申请)
            * [9.2 退款状态查询](#92-退款状态查询)
         * [10. 手机H5/小程序支付（微信公众号/小程序/支付宝服务窗支付）](#10-手机h5小程序支付微信公众号小程序支付宝服务窗支付)
            * [10.1 创建订单并生成手机中拉起支付所需参数](#101-创建订单并生成手机中拉起支付所需参数)
            * [10.2 刷新支付所需参数](#102-刷新支付所需参数)
            * [10.3 订单查询](#103-订单查询)
         * [11. 二维码被扫支付](#11-二维码被扫支付)
            * [11.1 创建订单并进行被扫支付](#111-创建订单并进行被扫支付)
            * [11.2 重新进行被扫支付](#112-重新进行被扫支付)
            * [11.3 订单查询](#113-订单查询)
         * [12. 一件代发支付推单](#12-一件代发支付推单)
            * [12.1 创建订单并触发一件代发支付](#121-创建订单并触发一件代发支付)
            * [12.2 重新进行一件代发支付](#122-重新进行一件代发支付)
            * [12.3 订单查询](#123-订单查询)
            * [12.4 订单批次触发一件代发支付](#124-订单批次触发一件代发支付)
      * [附录A](#附录a)
         * [A.1 支付状态](#a1-支付状态)
         * [A.2 申报状态](#a2-申报状态)
         * [A.3 二维码类型](#a3-二维码类型)
         * [A.4 支付公司代码](#a4-支付公司代码)
         * [A.5 银行代码](#a5-银行代码)
         * [A.6 海关及电子口岸代码](#a6-海关及电子口岸代码)
         * [A.7 实名认证结果代码](#a7-实名认证结果代码)
         * [A.8 退款状态代码](#a8-退款状态代码)
         * [A.9 H5支付类型](#a9-h5支付类型)
      * [附录B](#附录b)
         * [B.1 银行卡绑定流程说明](#b1-银行卡绑定流程说明)

<!-- Added by: raphael, at: Wed Oct 28 15:54:51 CST 2020 -->

<!--te-->


## 技术综述

### 请求格式说明
Xpay API整体采用RESTful API的风格，以application/json格式进行数据的传递。
本文档中所有的HTTP方法（无论其是GET/POST/DELETE/PUT或任何其他方法），其HTTP HEADER中必须加入OAuth2风格的Http header属性:

~~~
Authorization: Bearer 获取到的token
~~~

除Login外所有请求均需带上这个Authorization的HTTP请求头部，在POSTMAN中其表现形式如下，开发人员可根据自身使用的开发语言在HTTP请求头部组装该key-value:

![](doc/postman_header.png)

获取到的token为Xpay系统用于验证调用方身份的JWT风格的token, 该token的获得是通过使用系统分配的APP Id和APP Key并调用登录接口。其有效时间为<b>4小时</b>，且JWT本身包含了过期的时间的信息。关于JWT token，可参考 <https://jwt.io/>。若需要重新生成新token，只需再次调用登录接口获取token即可，token之间均为独立关系，获取新的token不会影响未过期的老token的使用。

### 返回格式说明

调用接口时的返回HTTP STATUS CODE遵循HTTP返回值的通用定义，常见HTTP返回值例如:

|HTTP STATUS CODE|说明|
|:--:|:--|
|200|SUCCESS, 调用成功(仅表示api调用成功，业务是否成功需查看返回的HTTP BODY)|
|400|BAD REQUEST, 通常用于请求的参数不正确|
|405|METHOD NOT ALLOWED, HTTP方法使用错误，例如错误的使用POST调用了一个GET方法|
|401|UNAUTHORIZED, access_token不正确|
|403|FORBIDDEN, 权限不足，出现此错误时，请再看一遍[技术综述](#技术综述),检查是否已按要求将Authorization相关的key-value加入HTTP请求头部中，并确保token没有过期(过期时间为4小时)|
|404|NOT FOUND, 不存在的接口url|
|500|INTERNAL SERVER ERROR, 服务器内部错误|

调用方应先根据HTTP STATUS CODE作为判断，过滤所有HTTP返回值即不成功的情况。

所有调用在HTTP正常调用成功即返回200的情况下，返回的HTTP BODY消息体内容为统一的JSON格式内容如下：

|字段名称|参数|类型|说明|
|:--:|:--:|:--|:--|
|业务层面是否正常完成| success | Boolean | 可以此字段作为标准判定业务调用是否完成，当success为false时，可以从errorMsg读取到错误原因等，errorCode作为参考便于向技术人员反馈问题 |
|业务错误代码| errorCode | String | |
|业务错误信息| errorMsg | String | |
|返回数据 | data | JSON | 具体返回的业务数据，本文后续所有api在"response"部分所述内容，为简便均表示的是data部分的内容 |

一个典型的业务成功的返回例子如下:

~~~
{
    "success": true,
    "errorMsg": null,
    "errorCode": null,
    "data": {
        "merchantId": "13",
        "orderBatchId": "11",
    }
}
~~~

一个典型的业务失败的返回例子如下:

~~~
{
    "success": false,
    "errorMsg": "参数 xxxx 未正确设置。",
    "errorCode": "30001",
    "data": null
}
~~~


### 接口地址 
使用如下链接代替本文中出现的{api\_url}字样

* 测试环境: https://dev-xpay.redharex.com
* 生产环境: https://xpay.redharex.com

### SDK(JAVA)下载
目前提供部分接口的调用示例，包括如下接口:

1. 获取access\_token
2. 单笔订单创建并支付
3. 监听系统异步消息通知
4. 陆续添加中

~~~
git clone https://github.com/iyuta-cn/iyuta-quickpay-api-doc
cd iyuta-quickpay-api-doc

# 进入项目置换application-test.yml文件中的username和password
# 为系统分配的测试账户密码

mvn clean install
mvn spring-boot:run 
~~~

## 接口介绍 

### 1. 获取调用token接口
通过本接口获取调用后续API所需的token。获取到的token为Xpay用于验证调用方身份的JWT风格的token, 其有效时间为<b>4小时</b>。若需重新获取token，只需再次调用登录接口获取token即可，token之间均为独立关系，获取新的token不会影响未过期的老token的使用。

初次调用前请登录商户后台，从右上角图标进入商户配置页面生成AppId与AppKey (AppKey只会显示一次，请妥善保管，重新生成AppKey将造成旧AppKey无法使用)，获取方式如下图所示:

![](doc/merchant_config.png)
![](doc/merchant_api_config.png)

* url: {api\_url}/auth/login
* method: POST
* request: Body parameter (application/json)

|字段名称|参数|例子|说明|
|:--|:--|:--|:--|
|用户名 | username| "abc" | 在商户后台所获取的APP Id |
|密码 | password| "p@ssw0rd" | 在商户后台所获取的APP Key |

* POSTMAN调用示例:
![](doc/auth.jpg)

* response:

|字段名称|参数|例子|说明|
|:--|:--|:--|:--|
|用户名|username| "admin"|
|token| token| "xxxxxx" | |
~~~
{
    "success": true,
    "errorMsg": null,
    "errorCode": null,
    "data": {
        "username": "admin",
        "token": "eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJhZG1pbiIsInJvbGVzIjpbIlJPTEVfVVNFUiIsIlJPTEVfQURNSU4iXSwiaWF0IjoxNTUzMDY2OTg1LCJleHAiOjE1NTMwODEzODV9.KIfG8LOk2FoMgqXAU8DCg_cbci36OqbLUIHUdIXDsF0"
    }
}
~~~

### 2. 快捷支付相关接口 ###

#### 2.1 订单批次上传 ####

若商户有一个批次的订单需要处理，可调用本接口创建订单批次。创建完订单批次后，登录商户端后台可查看到订单批次。请注意对于一次性需处理大量订单的商户(例如几千条)，建议使用本接口一次性提交所有订单。(若使用[2.6 单笔订单创建并请求支付](#26-单笔订单创建并请求支付)请注意为提高效率可考虑从技术架构上多线程进行接口调用避免顺序等待。）

* url: {api\_url}/orderBatch
* method: POST
* request: Body parameter (application/json)

请传入一个数组的order类型对象，order类型的结构如下

|字段名称|参数|类型|是否必填|例子|说明|
|:--|:--|:--|:--|:--|:--|
| 货币代码 | currency | String | 是 | "CNY" | 请固定为CNY |
| 需申报的电子口岸代码 | customsCode | String | 否 | "HG016" | 若需申报则为必填, 参见附录[A.6](#a6-海关及电子口岸代码) |
| 海关关区代码| customsAreaCode | String | 否 | "5130" | 若需申报且申报海关为广州海关时必填 |
| 检验检疫机构代码 | customsJyOrg | String | 否 | "440009" |  若需申报且申报为广州海关时必填|
| 进口类型 | customsInType | String | 否 | "1" | 若需申报且申报天津电子口岸时为必填，1-保税进口，2-直邮进口 |
| 商户订单编号 | mchtOrderNo | String| 是 | "2019032000000123" | 只能包含英文字母、数字、短划线-和下划线_，最大长度30位，并请确保商户订单不重复 |
| 订单下单时间 | orderDatetime | String | 否 | "2019-03-20 06:57:29" | 支持格式 yyyy-MM-dd HH:mm:ss |
| 订购人姓名 | payerName | String | 否 | "张三" | 若需申报则必填 |
| 订购人身份证号 | payerNumber | String | 否 | "310113198010101234" | 若需申报则必填|
| 订购人电话 | payerPhone | String | 否 | "18512001234" | 若需申报则必填 |
| 订单额度 | paymentAmount | Long | 是 | 4023 | 请务必注意单位为分 |
| 订单内主要商品信息 | subject | String | 是 | "XXXX化妆品" | 长度不超过200个字符 |
| 接收支付异步通知url | notifyUrl | String | 否 | | 本字段可不填，若不填写，异步通知将发送至本文档第三章[3. 接收异步通知](#3-接收异步通知)在商户后台所填写的商户级别的异步通知url中。若本字段填写则以本字段填写内容为准。消息体会进行签名，签名方式参考第三章。 |
| 订单内商品列表 | items | items类型数组 | 否 | | 可空 |

items类型的结构如下:

|字段名称|参数|类型|是否必填|例子|说明|
|:--|:--|:--|:--|:--|:--|
| 商品名称 | subject | String | 是 | "XXXX口红" | 长度不超过200个字符 |
| 商品链接 | itemLink | String | 是 | "http://www.baidu.com" |  |
| 货号 | articleNum | String | 否 | "WO11111" |  |


* request example: 

~~~
[
  {
    "currency": "CNY",
    "customsCode": "HG022",
    "customsAreaCode": "5130",
    "customsJyOrg": "440009",
    "customsInType": "2",
    "items": [
      {
        "articleNum": "HH00001",
        "itemLink": "http://www.baidu.com",
        "subject": "测试商品1"
      },
       {
        "articleNum": "HH00002",
        "itemLink": "http://www.baidu.com",
        "subject": "测试商品2"
      }
    ],
    "mchtOrderNo": "F20190402123",
    "orderDatetime": "2019-04-02 11:11:46",
    "payerName": "李白",
    "payerNumber": "310327198009270027",
    "payerPhone": "13800138000",
    "paymentAmount": 35302,
    "subject": "测试商品1"
  },
  {
    "currency": "CNY",
    "customsCode": "HG022",
    "customsAreaCode": "5130",
    "customsJyOrg": "440009",
    "customsInType": "2",
    "mchtOrderNo": "F20190402124",
    "orderDatetime": "2019-04-02 11:11:46",
    "payerName": "杜甫",
    "payerNumber": "360104199010101234",
    "payerPhone": "13300000000",
    "paymentAmount": 35000,
    "subject": "测试商品xxxx"
  }
]
~~~

* response:

|字段名称|参数|例子|说明|
|:--|:--|:--|:--|
|订单批次id| orderBatchId |  59 |
|订单批次号| dispBatchNum | "20190320162344842"|
|批次内订单总额(分)| orderTotalAmount | 70302 | 单位为分 |
|创建时间| createdTime | 1553070224475  | |

~~~
{
    "success": true,
    "errorMsg": null,
    "errorCode": null,
    "data": {
        "orderBatchId": 59,
        "merchantId": 1,
        "dispBatchNum": "20190320162344842",
        "isReconed": false,
        "feeAmount": null,
        "orderTotalAmount": 70302,
        "objectId": null,
        "feedbackObjectId": null,
        "createdTime": 1553070224475,
        "updatedTime": 1553070224817
    }
}
~~~


订单批次上传完成之后，在商户端可以查看到该订单批次信息:

![](doc/ob_screenshot.png)

#### 2.2 订单批次触发支付 ####
调用本接口对本批次内的订单进行支付与推关。本接口同步返回成功只表明系统接收到整个批次开始支付的指令，支付完成时间取决于协商的合作模式等其他因素。在发送支付指令成功之后，可以进行10分钟/次的订单批次支付&推送结果轮询。

* url: {api\_url}/orderBatch/{orderBatchId}/pay
* method: GET
* request Path Variable: url路径参数为创建该订单批次时返回的{orderBatchId}

* response: success参数返回为true时即表示系统已成功安排本批次支付任务

~~~
{
    "success": true,
    "errorMsg": null,
    "errorCode": null,
    "data": {
       “分配任务完成”
    }
}
~~~

* 错误代码: 若success为false，可能出现的errorCode和其对应解释如下

|errorCode|errorMsg| 备注|
|:--|:--|:--|
|50001| 未找到支持的银行卡和协议，可能与垫资模式的设置不正确有关 | 登陆商户后台进行银行卡绑定，参见[银行卡绑定流程说明](#B1-银行卡绑定流程说明)。若绑定后依然报此错误，请联系技术人员获取技术支持。
|50010| 未找到已签约的银行卡进行支付 | 登录商户后台进行银行卡绑定，参见[银行卡绑定流程说明](#B1-银行卡绑定流程说明) |
|50054| 没有需要被分配执行的订单 | 
|50056| 系统记录的银行卡当前额度可能无法支持支付本批次订单，请增加系统内银行卡额度并确保实际资金与额度大致匹配 | 在商户后台中录入的银行卡“当前余额“总额不足以支付当前订单批次，请确保银行卡真是余额足够支付整个订单批次，并在系统中填写入真实余额 |

订单批次中的每一笔订单在支付最终成功或失败后，会发送支付状态通知至商户配置的服务器，后续每一笔订单最终申报完成或失败也将发送申报状态通知至商户配置的服务器，参见[3 接收异步通知](#3-接收异步通知)。


#### 2.3 订单批次支付&推送结果汇总查询 ####

用于查询订单批次的支付及推单结果。

若结果中有支付失败的订单，可选择如下两种操作: 

* 1.重新调用[2.2 订单批次触发支付](#22-订单批次触发支付)，系统将只重新支付当前支付失败的订单；
* 2.针对支付失败订单号调用[2.7 单笔订单请求重新安排支付](#27-单笔订单请求重新安排支付)。

多次反复支付失败，需联系服务人员排查支付失败原因。
若推单失败原因为实名认证不通过，请运营人员自行登录商户后台修改申报的订购人身份信息，编辑并点击重新推单。其他原因请联系服务人员进行调查。

* url: {api\_url}/orderBatch/{orderBatchId}/summary
* method: GET
* request Path Variable: url路径参数为创建该订单批次时返回的{orderBatchId}

* response: 

|字段名称|参数|例子|说明|
|:--|:--|:--|:--|
|批次内订单总数| total |  159 |
|支付成功总数| paySuccessCount |150 | 单位为分 |
|支付失败总数|payFailedCount | 2|
|其他支付中间状态总数|payOtherCount |7  | |
|申报成功总数|declareSuccessCount |130  | |
|申报失败总数|declareFailedCount |7  | |
|其他申报中间状态总数|declareOtherCount | 22  | |
|总已支付金额(分)|totalPaymentAmount | 10489449  | |

~~~
{
    "data": {
        "declareFailedCount": 7,
        "declareOtherCount": 22,
        "declareSuccessCount": 130,
        "payFailedCount": 2,
        "payOtherCount": 7,
        "paySuccessCount": 150,
        "total": 159,
        "totalPaymentAmount": 10489449
    },
    "errorCode": null,
    "errorMsg": null,
    "success": true
}
~~~

#### 2.4 单笔订单回执查询 
用于查询单笔订单的详细状态及所有支付原始信息，供商家进行后续申报

* url: {api\_url}/order/feedback?mchtOrderNo={mchtOrderNo}
* method: GET
* request: Query Param {mchtOrderNo}为商家订单号


* response: orderResultDto

|字段名称|参数|例子|说明|
|:--|:--|:--|:--|
|商家订单号| mchtOrderNo |  2019041000011 |
|支付金额(分)| paymentAmount | 1 | 单位为分 |
|申报支付人姓名| payerName | 周Xx |
|申报支付人身份证号| payerNumber | 610327198509271234  | |
|申报支付人手机号| payerPhone | 13800138000  | |
|交易摘要| subject |YYYYYYYY-口红  | |
|支付状态| payStatus | PAY_SUCCEED  |	参见附录[A.1](#a1-支付状态)|
|申报状态| declareStatus | DECLARE_FAILED  | 参见附录[A.2](#a2-申报状态)|
|申报失败原因| declareFailReason | 支付人姓名和证件号不匹配 | |
|支付单号| paymentOrderNo | 111906650000561884 | |
|核验机构| verDept | null | 验核机构 1-银联 2-网联 3-其他 |
|支付类型| payType | 2 | 用户支付类型 1-APP 2-PC 3-扫码 4-其他 |
|支付原始请求| initRequest | ... | 支付的原始请求信息，海关179文请按此提供数据|
|支付原始返回| initResponse | ... | 支付的原始返回信息，海关179文请按此提供数据 |
|支付完成时间| paymentDatetime | 20190411213822 | 格式为yyyyMMddHHmmss |
|支付公司海关备案名称| customsPayCompanyName | XX支付网络服务股份有限公司 | |
|支付公司海关备案号| customsPayCompanyCode |  312228034T | |

~~~
{
  "success": true,
  "errorMsg": null,
  "errorCode": null,
  "data": {
    "mchtOrderNo": "2019041000011",
    "paymentAmount": 1,
    "payerName": "周Xx",
    "payerNumber": "610327198509271234",
    "payerPhone": "13800138000",
    "subject": "YYYYYYYY-口红",
    "payStatus": "PAY_SUCCEED",
    "declareStatus": "DECLARE_FAILED",
    "declareFailReason": "支付人姓名和证件号不匹配",
    "paymentOrderNo": "111906650000561884",
    "verDept": null,
    "payType": "2",
    "initRequest": "https://vsp.allinpay.com/apiweb/qpay/payapplyagree[data:{agreeid=201902221443545123, amount=1, appid=00152305, currency=CNY, cusid=55152104816ZLVW, notifyurl=https://dev-xpay.redharex.com/quickpay_notify/ALLINPAY/pengma, orderid=2019041000011, randomstr=1554989889665, subject=YYYYYYYY-口红, version=11}]",
    "initResponse": "{\"retcode\":\"SUCCESS\",\"retmsg\":null,\"randomstr\":\"917005450382\",\"sign\":\"B74D60CEB7141B3CB26FD4D7A5BD7B29\",\"orderid\":\"2019041000011\",\"trxstatus\":\"1999\",\"errmsg\":\"请输入短信验证码\",\"trxid\":null,\"chnltrxid\":null,\"fintime\":null,\"thpinfo\":\"{\\\"sign\\\":\\\"\\\",\\\"tphtrxcrtime\\\":\\\"\\\",\\\"tphtrxid\\\":0,\\\"trxflag\\\":\\\"trx\\\",\\\"trxsn\\\":\\\"\\\"}\"}",
    "paymentDatetime": "20190411213822",
    "customsPayCompanyName": "XX支付网络服务股份有限公司",
    "customsPayCompanyCode": "312228034T"
  }
}

~~~

#### 2.5 订单批次回执查询

用于批量查询一个订单批次中所有订单的详细状态及所有支付原始信息，供商家进行后续申报。请求需传递每页数据条数和当前的页数，每次最多请求100条数据。数据是按照原订单入库本系统的时间倒序排列。

* url: {api\_url}/orderBatch/{orderBatchId}/feedback?pagesize={pagesize}&page={page}
* method: GET
* request: Path Variable url路径参数为创建该订单批次时返回的{orderBatchId}

|字段名称|参数|是否必填|例子|说明|
|:--|:--|:--|:--|:--|
|订单批次id| orderBatchId(url路径参数) | 是 | 641 | |
|每页数据条数| pagesize |否| 10| 每页数据条数最大不能超过100条 |
|当前为全部数据的第几页| page |否| 1 | 数据从第1页开始|


一个请求例子

~~~
curl -X GET "http://127.0.0.1:9040/orderBatch/53/feedback?page=1&pagesize=10" -H "accept: */*" -H "Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJwZW5nbWEiLCJyb2xlcyI6WyJST0xFX1VTRVIiXSwiaWF0IjoxNTU1MTY3MTY5LCJleHAiOjE1NTUxODE1Njl9.EgRhAzPXVryIXMR_OnM-51gus5m0cm1zdjwds764ajk"
~~~

response: 

|字段名称|参数|例子|说明|
|:--|:--|:--|:--|
|订单回执数据| rows | ... | 为一个数组的orderResultDto，orderResultDto可参考[2.4](#24-单笔订单回执查询)的返回结果 |
|当前为全部数据的第几页| page | 1 | 数据从第1页开始|
|每页数据条数| pagesize | 10| 每页数据条数最大不能超过100条 |
|总数据条数| total | 465 | |

一个每页3条数据，请求第二页的返回例子:

~~~
{
  "success": true,
  "errorMsg": null,
  "errorCode": null,
  "data": {
    "rows": [
      {
        "mchtOrderNo": "BA1812-100937",
        "paymentAmount": 58130,
        "payerName": "赵XX",
        "payerNumber": "21080219930XXXX3X",
        "payerPhone": "1864170XXXX",
        "subject": "Svelty分解酵母120粒",
        "payStatus": "PAY_CANCELLED",
        "declareStatus": "NOT_DECLARED",
        "declareFailReason": null,
        "paymentOrderNo": null,
        "verDept": null,
        "payType": "2",
        "initRequest": null,
        "initResponse": null,
        "paymentDatetime": 20190313124233,
        "customsPayCompanyName": "XX支付网络服务股份有限公司",
        "customsPayCompanyCode": "312228034T"
      },
      {
        "mchtOrderNo": "BA1812-100937-1",
        "paymentAmount": 17162,
        "payerName": "赵XX",
        "payerNumber": "2108021993083XXX3X",
        "payerPhone": "1864170XXXX",
        "subject": "CLAYGE洗发水*1",
        "payStatus": "PAY_CANCELLED",
        "declareStatus": "NOT_DECLARED",
        "declareFailReason": null,
        "paymentOrderNo": null,
        "verDept": null,
        "payType": "2",
        "initRequest": null,
        "initResponse": null,
        "paymentDatetime": 20190313124233,
        "customsPayCompanyName": "XX支付网络服务股份有限公司",
        "customsPayCompanyCode": "312228034T"
      },
      {
        "mchtOrderNo": "BA1812-100953",
        "paymentAmount": 123616,
        "payerName": "龚XX",
        "payerNumber": "33068319870110XXXX",
        "payerPhone": "177173XXXX",
        "subject": "F.O.Online 儿童袜裤",
        "payStatus": "PAY_SUCCEED",
        "declareStatus": "DECLARED",
        "declareFailReason": null,
        "paymentOrderNo": "111906650000530919",
        "verDept": "1",
        "payType": "2",
        "initRequest": null,
        "initResponse": null,
        "paymentDatetime": "20190313124233",
        "customsPayCompanyName": "XX支付网络服务股份有限公司",
        "customsPayCompanyCode": "312228034T"
      }
    ],
    "page": 2,
    "pagesize": 3,
    "total": 465
  }
}
~~~

#### 2.6 单笔订单创建并请求支付

通过该接口可直接创建单笔订单并将此任务安排入系统后续的支付任务中。根据系统的风控规则和其他外部因素等，支付均非即时支付而是由系统安排支付时间和申报时间。当该支付任务被执行后，支付结果（成功/失败）将以异步通知的形式返回给商户服务器，参见[3.4](#34-支付状态异步通知)。若支付成功，将继续自动执行申报任务，申报结果也将以异步通知的形式发送，参见[3.5](#35-申报状态异步通知)。根据商户的支付公司渠道和出资方式等，支付一般预计在30秒-15分钟至内完成。支付成功后，根据各地海关的入库时间不同，海关申报一般在30秒-30分钟的不等时间内完成。

* url: {api\_url}/order/createAndPay
* method: POST
* request: Body parameter (application/json)

请传入一个单个的order类型对象，order类型的结构如下

|字段名称|参数|类型|是否必填|例子|说明|
|:--|:--|:--|:--|:--|:--|
| 货币代码 | currency | String | 是 | "CNY" | 请固定为CNY |
| 需申报的电子口岸代码 | customsCode | String | 否 | "HG016" | 若需申报则为必填, 参见附录[A.6](#a6-海关及电子口岸代码) |
| 海关关区代码| customsAreaCode | String | 否 | "5130" | 若需申报且申报海关为广州海关时必填 |
| 检验检疫机构代码 | customsJyOrg | String | 否 | "440009" |  若需申报且申报为广州海关时必填|
| 进口类型 | customsInType | String | 否 | "1" | 若需申报且申报天津电子口岸时为必填，1-保税进口，2-直邮进口 |
| 商户订单编号 | mchtOrderNo | String| 是 | "F20190402123" | 只能包含英文字母、数字、短划线-和下划线_，最大长度30位，并请确保商户订单不重复 |
| 订单下单时间 | orderDatetime | String | 否 | "2019-03-20 06:57:29" | 支持格式 yyyy-MM-dd HH:mm:ss |
| 订购人姓名 | payerName | String | 否 | "张三" | 若需申报则必填 |
| 订购人身份证号 | payerNumber | String | 否 | "310113198010101234" | 若需申报则必填|
| 订购人电话 | payerPhone | String | 否 | "18512001234" | 若需申报则必填 |
| 订单额度 | paymentAmount | Long | 是 | 4023 | 请务必注意单位为分 |
| 订单内主要商品信息 | subject | String | 是 | "XXXX化妆品" | 长度不超过200个字符 |
| 接收支付异步通知url | notifyUrl | String | 否 | | 本字段可不填，若不填写，异步通知将发送至本文档第三章[3. 接收异步通知](#3-接收异步通知)在商户后台所填写的商户级别的异步通知url中。若本字段填写则以本字段填写内容为准。消息体会进行签名，签名方式参考第三章。 |
| 订单内商品列表 | items | items类型数组 | 否 | | 可空 |

items类型的结构如下:

|字段名称|参数|类型|是否必填|例子|说明|
|:--|:--|:--|:--|:--|:--|
| 商品名称 | subject | String | 是 | "XXXX口红" | 长度不超过200个字符 |
| 商品链接 | itemLink | String | 是 | "http://www.baidu.com" |  |
| 货号 | articleNum | String | 否 | "WO11111" |  |


* request example: 

~~~
  {
    "currency": "CNY",
    "customsCode": "HG022",
    "customsAreaCode": "5130",
    "customsJyOrg": "440009",
    "customsInType": "2",
    "items": [
      {
        "articleNum": "HH00001",
        "itemLink": "http://www.baidu.com",
        "subject": "测试商品1"
      },
       {
        "articleNum": "HH00002",
        "itemLink": "http://www.baidu.com",
        "subject": "测试商品2"
      }
    ],
    "mchtOrderNo": "F20190402123",
    "orderDatetime": "2019-04-02 11:11:46",
    "payerName": "李白",
    "payerNumber": "310327198009270027",
    "payerPhone": "13800138000",
    "paymentAmount": 35302,
    "subject": "测试商品1"
  }
~~~

* response: 

|字段名称|参数|类型|例子|说明|
|:--|:--|:--|:--|:--|
| 商户订单编号 | mchtOrderNo | String| "F20190402123" | |

~~~
{
    "success": true,
    "errorMsg": null,
    "errorCode": null,
    "data": {
        "mchtOrderNo": "F20190402123"
    }
}
~~~

* 错误代码: 若success为false，可能出现的errorCode和其对应解释如下

|errorCode|errorMsg| 备注|
|:--|:--|:--|
|50001| 未找到支持的银行卡和协议，可能与垫资模式的设置不正确有关 | 登陆商户后台进行银行卡绑定，参见[银行卡绑定流程说明](#B1-银行卡绑定流程说明)。若绑定后依然报此错误，请联系技术人员获取技术支持。
|50010| 未找到已签约的银行卡进行支付 | 登录商户后台进行银行卡绑定，参见[银行卡绑定流程说明](#B1-银行卡绑定流程说明) |
|50056| 系统记录的银行卡当前额度可能无法支持支付本批次订单，请增加系统内银行卡额度并确保实际资金与额度大致匹配 | 在商户后台中录入的银行卡“当前余额“总额不足以支付当前订单批次，请确保银行卡真是余额足够支付整个订单批次，并在系统中填写入真实余额 |


#### 2.7 单笔订单请求重新安排支付
当收到订单支付失败的异步通知时，例如因银行卡实际余额不够（和系统中记录的余额不匹配等原因），商户可能需要线下解决这些问题，当问题解决后，可通过调用该接口重新申请对订单进行支付。若申请成功，该订单将进入待支付队列等待支付。

* url: {api\_url}/order/arrangePay?mchtOrderNo={mchtOrderNo}
* method: GET
* request: Query Params为商户订单号mchtOrderNo

|字段名称|参数| 是否必填 |例子|说明|
|:--|:--|:--|:--|:--|
|商户订单号| mchtOrderNo | 是 | 1904052344  |  |


* response: 

~~~
{
    "success": true,
    "errorMsg": null,
    "errorCode": null,
    "data": "订单进入支付队列成功"
}
~~~

#### 2.8 单笔订单创建
调用本接口将订单上送至本系统中供后续自行选择不同的支付方式进行支付

* url: {api\_url}/order/create
* method: POST
* request: Body parameter (application/json)

请传入一个单个的order类型对象，order类型的结构如下

|字段名称|参数|类型|是否必填|例子|说明|
|:--|:--|:--|:--|:--|:--|
| 货币代码 | currency | String | 是 | "CNY" | 请固定为CNY |
| 需申报的电子口岸代码 | customsCode | String | 否 | "HG016" | 若需申报则为必填, 参见附录[A.6](#a6-海关及电子口岸代码) |
| 海关关区代码| customsAreaCode | String | 否 | "5130" | 若需申报且申报海关为广州海关时必填 |
| 检验检疫机构代码 | customsJyOrg | String | 否 | "440009" |  若需申报且申报为广州海关时必填|
| 进口类型 | customsInType | String | 否 | "1" | 若需申报且申报天津电子口岸时为必填，1-保税进口，2-直邮进口 |
| 商户订单编号 | mchtOrderNo | String| 是 | "F20190402123" | 只能包含英文字母、数字、短划线-和下划线_，最大长度30位，并请确保商户订单不重复 |
| 订单下单时间 | orderDatetime | String | 否 | "2019-03-20 06:57:29" | 支持格式 yyyy-MM-dd HH:mm:ss |
| 订购人姓名 | payerName | String | 否 | "张三" | 若需申报则必填 |
| 订购人身份证号 | payerNumber | String | 否 | "310113198010101234" | 若需申报则必填|
| 订购人电话 | payerPhone | String | 否 | "18512001234" | 若需申报则必填 |
| 订单额度 | paymentAmount | Long | 是 | 4023 | 请务必注意单位为分 |
| 订单内主要商品信息 | subject | String | 是 | "XXXX化妆品" | 长度不超过200个字符 |
| 接收支付异步通知url | notifyUrl | String | 否 | | 本字段可不填，若不填写，异步通知将发送至本文档第三章[3. 接收异步通知](#3-接收异步通知)在商户后台所填写的商户级别的异步通知url中。若本字段填写则以本字段填写内容为准。消息体会进行签名，签名方式参考第三章。 |
| 订单内商品列表 | items | items类型数组 | 否 | | 可空 |

items类型的结构如下:

|字段名称|参数|类型|是否必填|例子|说明|
|:--|:--|:--|:--|:--|:--|
| 商品名称 | subject | String | 是 | "XXXX口红" | 长度不超过200个字符 |
| 商品链接 | itemLink | String | 是 | "http://www.baidu.com" |  |
| 货号 | articleNum | String | 否 | "WO11111" |  |


* request example: 

~~~
  {
    "currency": "CNY",
    "customsCode": "HG022",
    "customsAreaCode": "5130",
    "customsJyOrg": "440009",
    "customsInType": "2",
    "items": [
      {
        "articleNum": "HH00001",
        "itemLink": "http://www.baidu.com",
        "subject": "测试商品1"
      },
       {
        "articleNum": "HH00002",
        "itemLink": "http://www.baidu.com",
        "subject": "测试商品2"
      }
    ],
    "mchtOrderNo": "F20190402123",
    "orderDatetime": "2019-04-02 11:11:46",
    "payerName": "李白",
    "payerNumber": "310327198009270027",
    "payerPhone": "13800138000",
    "paymentAmount": 35302,
    "subject": "测试商品1"
  }
~~~

* response: 

|字段名称|参数|类型|例子|说明|
|:--|:--|:--|:--|:--|
| 商户订单编号 | mchtOrderNo | String| "F20190402123" | |

~~~
{
    "success": true,
    "errorMsg": null,
    "errorCode": null,
    "data": {
        "mchtOrderNo": "F20190402123"
    }
}
~~~




### 3. 接收异步通知
#### 3.1 配置异步通知接收参数

* 登录商户后台后，点击右上角图标并选择"商户配置"
![](doc/merchantConfig.png)

* 填写用于接收异步通知的url和签名Token。令牌Token为对通知消息进行加签用。请注意本文档多种订单创建、支付中都包含字段notifyUrl，在提交订单、支付信息时提交的notifyUrl的优先级将高于用户在此处设置的回调地址，但签名方式均一致（即以此处的signToken进行签名）
![](doc/notifySetup.png)

* 在填写的服务器地址实现处理业务逻辑的程序，可参考本项目的JavaSDK
* 所有通知的格式均相同，系统将发送一个Http Post请求至商户配置的服务器地址上，请求体的requestBody格式为application/json，其结构如下:

|字段名称|参数|例子|说明|
|:--|:--|:--|:--|
|服务器发送消息的时间戳| timestamp | 1555816968018 |  |
|消息类型| msgType| PAY\_STATUS\_NOTIFY | |
|消息内容| msgBody| ... | json格式字符串 |
|签名| sign | xxxxxx | 服务器将使用商户提供的token，对消息进行签名，签名方法参见 [3.2](#32-消息签名方法) | |

* 商户服务器端确认消息为本系统发送后（验证签名)，建议先返回String "OK"，然后可进行自己的业务逻辑处理。因本系统发送通知的http请求timeout时间较短，均为5秒，较长的处理时间将导致本系统认为该通知未发送成功，而重复发送。

#### 3.2 消息签名方法
将返回信息中的timestamp, msgBody以及商户自己保管的signToken三者以字典顺序进行排序并拼接成1个字符串，对字符串进行SHA1算法计算获取Hash值作为签名。

* Java: 可参考本项目提供的SDK中的相关代码。
* PHP: 下载相关签名用SHA1签名函数: <a href='https://github.com/iYuta-cn/iyuta-quickpay-api-doc/blob/master/php.zip?raw=true'>下载相关文件</a>

#### 3.3 消息重发机制
所有消息通知，商户服务器均需回复String "OK"在返回体中，否则本系统将认为商户未接收到该通知。未成功发送的消息，将被共计重发5次，分别为第一次消息发送后的1m, 5m, 10m, 1h, 6h后重试直至商户服务器发送OK的返回。

#### 3.4 支付状态异步通知
* msgType为 PAY\_STATUS\_NOTIFY
* msgBody为 [2.4](#24-单笔订单回执查询) 中orderResultDto，支付状态关注其中的PAY\_STATUS即可，状态代码参见 [A.1](#a1-支付状态)

#### 3.5 申报状态异步通知

* msgType为 DECLARE\_STATUS\_NOTIFY
* msgBody为 [2.4](#24-单笔订单回执查询) 中orderResultDto，海关申报状态关注其中的DECLARE\_STATUS即可，状态代码参见 [A.2](#a2-申报状态)
* 测试环境因支付公司渠道问题无法测试申报成功通知

### 4. 二维码收单
#### 4.1 创建订单并生成支付二维码
通过该接口可直接创建单笔订单并根据二维码类型返回对应的二维码url，请注意商户开发人员请自行将返回的url生成二维码展示在自己的商城中！而不是跳转至返回的url上([如何将url转换成二维码](https://www.baidu.com/s?wd=%E5%A6%82%E4%BD%95%E5%B0%86url%E8%BD%AC%E6%8D%A2%E4%B8%BA%E4%BA%8C%E7%BB%B4%E7%A0%81))！当二维码被扫码支付后，支付结果（成功/失败）将以异步通知的形式返回给商户服务器，参见[3.4](#34-支付状态异步通知)。若支付成功，根据订单设置的是否需要自动申报字段needDeclare，若需要则将继续自动执行申报任务，申报结果也将以异步通知的形式发送，参见[3.5](#35-申报状态异步通知)。订单的过期时间为15分钟。

![](doc/warning_qrcode.png)

* url: {api\_url}/order/createAndQrCode
* method: POST
* request: Body parameter (application/json)

请传入一个单个的order类型对象，order类型的结构如下

|字段名称|参数|类型|是否必填|例子|说明|
|:--|:--|:--|:--|:--|:--|
|二维码类型| qrCodeType | String | 是 | "WECHATPAY" | 支持微信、支付宝、银联二维码，参见 [A.3](#a3-二维码类型) |
| 是否需要申报至海关 | needDeclare | Boolean | 否 | true | 是否在支付成功后自动进行报关。若不设置该订单是否需要申报海关，则将按照商户在入网时的业务形态决定是否进行申报。若设置为false但之后需申报，可后置调用[8.1 支付信息海关推单](#81-支付信息海关推单) |
| 货币代码 | currency | String | 是 | "CNY" | 请固定为CNY |
| 需申报的电子口岸代码 | customsCode | String | 否 | "HG016" | 若需申报则为必填, 参见附录[A.6](#a6-海关及电子口岸代码) |
| 海关关区代码| customsAreaCode | String | 否 | "5130" | 若需申报且申报海关为广州海关时必填 |
| 检验检疫机构代码 | customsJyOrg | String | 否 | "440009" |  若需申报且申报为广州海关时必填|
| 进口类型 | customsInType | String | 否 | "1" | 若需申报且申报天津电子口岸时为必填，1-保税进口，2-直邮进口 |
| 商户订单编号 | mchtOrderNo | String| 是 | "F20190402123" | 只能包含英文字母、数字、短划线-和下划线_，最大长度30位，并请确保商户订单不重复 |
| 订单下单时间 | orderDatetime | String | 否 | "2019-03-20 06:57:29" | 支持格式 yyyy-MM-dd HH:mm:ss |
| 订购人姓名 | payerName | String | 否 | "张三" | 若需申报则必填 |
| 订购人身份证号 | payerNumber | String | 否 | "310113198010101234" | 若需申报则必填|
| 订购人电话 | payerPhone | String | 否 | "18512001234" | 若需申报则必填 |
| 订单额度 | paymentAmount | Long | 是 | 4023 | 请务必注意单位为分 |
| 订单内主要商品信息 | subject | String | 是 | "XXXX化妆品" | 长度不超过200个字符 |
| 接收支付异步通知url | notifyUrl | String | 否 | | 本字段可不填，若不填写，异步通知将发送至本文档第三章[3. 接收异步通知](#3-接收异步通知)在商户后台所填写的商户级别的异步通知url中。若本字段填写则以本字段填写内容为准。消息体会进行签名，签名方式参考第三章。 |
| 订单内商品列表 | items | items类型数组 | 否 | | 可空 |

items类型的结构如下:

|字段名称|参数|类型|是否必填|例子|说明|
|:--|:--|:--|:--|:--|:--|
| 商品名称 | subject | String | 是 | "XXXX口红" | 长度不超过200个字符 |
| 商品链接 | itemLink | String | 是 | "http://www.baidu.com" |  |
| 货号 | articleNum | String | 否 | "WO11111" |  |


* request example: 

~~~
  {
  	"qrCodeType" : "WECHATPAY",
  	"needDeclare" : false,
  	"currency": "CNY",
  	"customsCode": "HG022",
  	"customsAreaCode": "5130",
  	"customsJyOrg": "440009",
  	"customsInType": "2",
  	"items": [
      {
        "articleNum": "HH00001",
        "itemLink": "http://www.baidu.com",
        "subject": "测试商品1"
      },
       {
        "articleNum": "HH00002",
        "itemLink": "http://www.baidu.com",
        "subject": "测试商品2"
      }
    ],
    "mchtOrderNo": "F20190402123",
    "orderDatetime": "2019-04-02 11:11:46",
    "payerName": "李白",
    "payerNumber": "310327198009270027",
    "payerPhone": "13800138000",
    "paymentAmount": 3352,
    "subject": "测试商品1"
  }
~~~

* response:

|字段名称|参数| 例子|说明|
|:--|:--|:--|:--|
|商户订单号| mchtOrderNo |  F20190402123  |  |
|二维码类型| qrCodeType | WECHATPAY | 参见 [A.3](#a3-二维码类型) |
|二维码url| codeUrl | weixin://wxpay/bizpayurl?pr=X8Zn0PV | |
|支付公司代码 | psp | EASYPAY | 建议商户在生成二维码的前端商城中根据支付公司代码放上对应支付公司的LOGO, 参见 [A.4](#a4-支付公司代码) |

~~~
{
    "success": true,
    "errorMsg": null,
    "errorCode": null,
    "data": {
        "mchtOrderNo": "F20190402123",
        "psp": "EASYPAY",
        "codeUrl": "weixin://wxpay/bizpayurl?pr=aTWT2Jl",
        "qrCodeType": "WECHATPAY"
    }
}
~~~

#### 4.2 生成/刷新二维码
针对已经提交至系统的订单（例如通过订单批次上传的订单、已创建的订单但二维码长期未支付导致二维码过期的订单、想要切换微信/支付宝/银联二维码的订单，之前支付失败想重新使用二维码支付的订单），需要重新生成二维码，可调用此接口:

* url: {api\_url}/order/qrCode?mchtOrderNo={mchtOrderNo}&qrCodeType={qrCodeType}
* method: GET
* request: Query Params

|字段名称|参数| 是否必填 |例子|说明|
|:--|:--|:--|:--|:--|
|商户订单号| mchtOrderNo | 是 | 1904052344  |  |
|二维码类型| qrCodeType | 是 | WECHATPAY | 支持微信、支付宝、银联二维码，参见 [A.3](#a3-二维码类型) |

* response: 

|字段名称|参数| 例子|说明|
|:--|:--|:--|:--|
|商户订单号| mchtOrderNo |  19040523834344  |  |
|二维码类型| qrCodeType | WECHATPAY | 参见 [A.3](#a3-二维码类型) |
|二维码url| codeUrl | weixin://wxpay/bizpayurl?pr=X8Zn0PV | |
|支付公司代码 | psp | EASYPAY | 建议商户在生成二维码的前端商城中根据支付公司代码放上对应支付公司的LOGO, 参见 [A.4](#a4-支付公司代码) |


~~~
{
  "success": true,
  "errorMsg": null,
  "errorCode": null,
  "data": {
    "mchtOrderNo": "19040523834344",
    "psp": "EASYPAY",
    "codeUrl": "weixin://wxpay/bizpayurl?pr=X8Zn0PV",
    "qrCodeType": "WECHATPAY"
  }
}
~~~

#### 4.3 订单查询
若商户侧的服务器没有收到订单支付成功的异步消息通知，可以主动查询订单的支付结果等信息，避免在二维码支付场景下因服务器未收到通知而造成用户侧相关业务流程无法继续进行的问题。

* url: {api\_url}/order/queryOrder?mchtOrderNo={mchtOrderNo}
* method: GET
* request: Query Params

|字段名称|参数| 是否必填 |例子|说明|
|:--|:--|:--|:--|:--|
|商户订单号| mchtOrderNo | 是 | 1904052344  |  |

* response: 
返回结果为[2.4](#24-单笔订单回执查询) 中orderResultDto，重点关注其payStatus和paymentDatetime即可。

### 5. 银行卡快捷支付收单
#### 5.1 快捷签约申请
快捷支付需先进行协议的申请，申请时请自行定义请求流水号，之后需根据请求流水号和短信验证码在[5.2 签约申请确认](#52-签约申请确认)中使用。测试环境银行行号可使用任意真实银行卡号（可更换卡号最后4位）进行测试，测试环境中手机不会真实收到短信，可使用任意6位字符作为短信验证码完成认证步骤。

* url: {api\_url}/sdbc/agreeApply
* method: POST
* request: Body parameter (application/json)

需传入的json对象结构如下:

|字段名称|参数|类型|是否必填|例子|说明|
|:--|:--|:--|:--|:--|:--|
|请求流水号| requestId|String | 是| 201905040012 | 由商户自己定义的一个请求流水号，在[5.2 签约申请确认](#52-签约申请确认)中将被使用 | |
|银行卡账户名称|acctname| String | 是 | 张三 | |
|银行卡号| acctno | String | 是 | 6217920151050000 | |
|银行卡类型| accttype | String | 是 | "00" | "00"借记卡 <!--"02"信用卡--> |
|银行代码| bankcode | String | 是 | 0310 | 参见[A.5 银行代码](#a5-银行代码) |
|身份证号| idno | String | 是 | 310113198010101234 | |
|手机号| mobile| String | 是 | 13800138000 | |
<!--|cvv2号| cvv2 | String | 否 | | 信用卡为必填，指卡背面的3位CVV2号 |
|有效期至| validdate| String | 否| 1904 | 信用卡为必填，指卡的有效期年月，使用格式yyMM(年月）|-->

* request example:

~~~
{
  "acctname": "张三",
  "acctno": "6217920151050000",
  "accttype": "00",
  "bankcode": "999",
  "idno": "310113198010101234",
  "mobile": "13800138000",
  "requestId": "201905040012"
}
~~~

* response:

|字段名称|参数|例子|说明|
|:--|:--|:--|:--|
|请求流水号| requestId| 201905040012 | 由商户自己定义的一个请求流水号，在[5.2 签约申请确认](#52-签约申请确认)中将被使用 |
|银行卡账户名称|acctname|  张三 | |
|银行卡号| acctno | 6217920151050000 | |
|银行卡类型| accttype |  "00" | "00"借记卡, "02"信用卡 |
|银行代码| bankcode |  0310 | 参见[A.5 银行代码](#a5-银行代码) |
|银行名称| bankname |  上海浦东发展银行 | 参见[A.5 银行代码](#a5-银行代码) |
|身份证号| idno |  310113198010101234 | |
|手机号| mobile|  13800138000 | |
|cvv2号| cvv2 |  | 信用卡时有值，指卡背面的3位CVV2号 |
|有效期至| validdate|  | 信用卡时有值，指卡的有效期年月，使用格式yyMM(年月）|
|快捷支付协议号| agreeid | | 此步骤时agreeid返回均为空 |
|支付公司代码| psp | ALLINPAY | 实际该协议的签约渠道|
|消息| message | 请输入短信验证码 | 提示信息 | 

~~~
{
  "success": true,
  "errorMsg": null,
  "errorCode": null,
  "data": {
    "requestId": "201905040012",
    "accttype": "00",
    "acctno": "6217920151050000",
    "idno": "310113198010101234",
    "acctname": "张三",
    "mobile": "13800138000",
    "validdate": null,
    "cvv2": null,
    "bankcode": "0310",
    "bankname": "上海浦东发展银行",
    "agreeid": null,
    "psp": "ALLINPAY",
    "message": "请输入短信验证码"
  }
}
~~~

#### 5.2 签约申请确认
商户侧开发需将第一步所定义的requestId连同用户所收到的短信验证码smsCode提交至本接口，以进行快捷支付签约的确认，获取核心字段快捷支付协议号agreeid并保存，用于未来的支付。测试环境不会真实收到验证码短信，可使用任意6位验证码。

* url: {api\_url}/sdbc/agreeConfirm
* method: POST
* request: Body parameter (application/json)

需传入的json对象结构如下:

|字段名称|参数|类型|是否必填|例子|说明|
|:--|:--|:--|:--|:--|:--|
|请求流水号| requestId|String | 是| 201905040012 | 请使用在[5.1 快捷签约申请](#51-快捷签约申请)中所使用的requestId | 
|短信验证码| smsCode| String | 是 | 088407 | |


* request example: 

~~~
{
  "requestId": "201905040012",
  "smsCode": "088407"
}
~~~

* response:

|字段名称|参数|例子|说明|
|:--|:--|:--|:--|
|请求流水号| requestId| 201905040012 | 由商户自己定义的一个请求流水号 |
|银行卡账户名称|acctname|  张三 | |
|银行卡号| acctno | 6217920151050000 | |
|银行卡类型| accttype |  "00" | "00"借记卡, "02"信用卡 |
|银行代码| bankcode |  0310 | 参见[A.5 银行代码](#a5-银行代码) |
|银行名称| bankname |  上海浦东发展银行 | 参见[A.5 银行代码](#a5-银行代码) |
|身份证号| idno |  310113198010101234 | |
|手机号| mobile|  13800138000 | |
|cvv2号| cvv2 |  | 信用卡时有值，指卡背面的3位CVV2号 |
|有效期至| validdate|   | 信用卡时有值，指卡的有效期年月，使用格式yyMM(年月）|
|快捷支付协议号| agreeid | 201905042109498625 | 用于未来快捷支付的核心字段 |
|支付公司代码| psp | ALLINPAY | 实际该协议的签约渠道|
|消息| message | 签约成功 | 提示信息 | 

~~~
{
  "success": true,
  "errorMsg": null,
  "errorCode": null,
  "data": {
    "requestId": "201905040012",
    "accttype": "00",
    "acctno": "6217920151050000",
    "idno": "310113198010101234",
    "acctname": "张三",
    "mobile": "13800138000",
    "validdate": null,
    "cvv2": null,
    "bankcode": "0310",
    "bankname": "上海浦东发展银行",
    "agreeid": "201905042109498625",
    "psp": "ALLINPAY",
    "message": "协议支付-账户认证成功"
  }
}
~~~


#### 5.3 创建订单并使用快捷协议进行支付
通过该接口可直接创建单笔订单并使用指定的快捷支付协议(agreeid)进行支付，根据商户的实际签约支付渠道不同，可能有如下两种结果:

* 快捷支付需要短信验证码进行验证，商户侧需继续对接接口[5.4 支付短信确认](#54-支付短信确认)
* 快捷支付不需要短信验证码进行验证，无需对接[5.4 支付短信确认](#54-支付短信确认),由于渠道限制，支付状态可能无法直接变更为"PAY\_SUCCEED"，商户需等待异步通知或主动使用订单查询接口进行轮询。

调用方式详情:

* url: {api\_url}/order/createAndQuickpay
* method: POST
* request: Body parameter (application/json)

请传入一个单个的order类型对象，order类型的结构如下

|字段名称|参数|类型|是否必填|例子|说明|
|:--|:--|:--|:--|:--|:--|
|协议号| agreeid | String | 是 | "201905041150567656" | 从[5.2](#52-签约申请确认)返回的协议号agreeid |
| 是否需要申报至海关 | needDeclare | Boolean | 否 | true | 是否在支付成功后自动进行报关。若不设置该订单是否需要申报海关，则将按照商户在入网时的业务形态决定是否进行申报。若设置为false但之后需申报，可后置调用[8.1 支付信息海关推单](#81-支付信息海关推单)  |
| 货币代码 | currency | String | 是 | "CNY" | 请固定为CNY |
| 需申报的电子口岸代码 | customsCode | String | 否 | "HG016" | 若需申报则为必填, 参见附录[A.6](#a6-海关及电子口岸代码) |
| 海关关区代码| customsAreaCode | String | 否 | "5130" | 若需申报且申报海关为广州海关时必填 |
| 检验检疫机构代码 | customsJyOrg | String | 否 | "440009" |  若需申报且申报为广州海关时必填|
| 进口类型 | customsInType | String | 否 | "1" | 若需申报且申报天津电子口岸时为必填，1-保税进口，2-直邮进口 |
| 商户订单编号 | mchtOrderNo | String| 是 | "F20190402123" | 只能包含英文字母、数字、短划线-和下划线_，最大长度30位，并请确保商户订单不重复 |
| 订单下单时间 | orderDatetime | String | 否 | "2019-03-20 06:57:29" | 支持格式 yyyy-MM-dd HH:mm:ss |
| 订购人姓名 | payerName | String | 否 | "张三" | 若需申报则必填 |
| 订购人身份证号 | payerNumber | String | 否 | "310113198010101234" | 若需申报则必填|
| 订购人电话 | payerPhone | String | 否 | "18512001234" | 若需申报则必填 |
| 订单额度 | paymentAmount | Long | 是 | 4023 | 请务必注意单位为分 |
| 订单内主要商品信息 | subject | String | 是 | "XXXX化妆品" | 长度不超过200个字符 |
| 接收支付异步通知url | notifyUrl | String | 否 | | 本字段可不填，若不填写，异步通知将发送至本文档第三章[3. 接收异步通知](#3-接收异步通知)在商户后台所填写的商户级别的异步通知url中。若本字段填写则以本字段填写内容为准。消息体会进行签名，签名方式参考第三章。 |
| 订单内商品列表 | items | items类型数组 | 否 | | 可空 |

items类型的结构如下:

|字段名称|参数|类型|是否必填|例子|说明|
|:--|:--|:--|:--|:--|:--|
| 商品名称 | subject | String | 是 | "XXXX口红" | 长度不超过200个字符 |
| 商品链接 | itemLink | String | 是 | "http://www.baidu.com" |  |
| 货号 | articleNum | String | 否 | "WO11111" |  |


* request example: 

~~~
  {
  	"agreeid" : "201905041150567656",
  	"needDeclare" : false,
  	"currency": "CNY",
  	"customsCode": "HG022",
  	"customsAreaCode": "5130",
  	"customsJyOrg": "440009",
  	"customsInType": "2",
  	"items": [
      {
        "articleNum": "HH00001",
        "itemLink": "http://www.baidu.com",
        "subject": "测试商品1"
      },
       {
        "articleNum": "HH00002",
        "itemLink": "http://www.baidu.com",
        "subject": "测试商品2"
      }
    ],
    "mchtOrderNo": "F20190402123",
    "orderDatetime": "2019-04-02 11:11:46",
    "payerName": "李白",
    "payerNumber": "310327198009270027",
    "payerPhone": "13800138000",
    "paymentAmount": 3352,
    "subject": "测试商品1"
  }
~~~

* response:

|字段名称|参数| 例子|说明|
|:--|:--|:--|:--|
|商户订单号| mchtOrderNo |  F20190402123  |  |
|支付公司代码 | psp | ALLINPAY | 建议商户在前端商城中根据支付公司代码放上对应支付公司的LOGO, 参见 [A.4](#a4-支付公司代码) |
|协议号|agreeid| 201905041150567656 | |
|支付状态|payStatus| PAY_APPLIED| 参见附录[A.1](#a1-支付状态) |
|消息|message|请输入短信验证码| |


~~~
{
    "success": true,
    "errorMsg": null,
    "errorCode": null,
    "data": {
        "mchtOrderNo": "F20190402123",
        "psp": "ALLINPAY",
        "agreeid": "201905041150567656",
        "payStatus": "PAY_APPLIED",
        "message": "请输入短信验证码"
    }
}
~~~
#### 5.4 支付短信确认
本节仅针对对支付时需要短信验证码二次确认的支付渠道。
调用本接口将用户收取到的短信验证码进行提交完成支付。请注意，若短信验证码输入错误，则需再次调用[5.5 重新申请支付和获取支付短信](#55-重新申请支付和获取支付短信)以获取新的验证码，若不重新调用而只是更正请求内的验证码，系统会呈现"请求异常"字样。

* url: {api\_url}/order/confirmQuickpay
* method: POST
* request: Body Parameter (application/json)

需传入的json对象结构如下:

|字段名称|参数| 是否必填 |例子|说明|
|:--|:--|:--|:--|:--|
|商户订单号| mchtOrderNo | 是 | F20190402123  |  |
|快捷支付协议号|agreeid | 是 | 201905041150567656  |  |
|短信验证码|smsCode|是| 700336 | |

* request example:

~~~
{
	"mchtOrderNo": "F20190402123",
	"agreeid": "201905041150567656",
	"smsCode": "700336"
}
~~~

* response:

|字段名称|参数| 例子|说明|
|:--|:--|:--|:--|
|商户订单号| mchtOrderNo |  F20190402123  |  |
|支付公司代码 | psp | ALLINPAY | 建议商户在前端商城中根据支付公司代码放上对应支付公司的LOGO, 参见 [A.4](#a4-支付公司代码) |
|协议号|agreeid| 201905041150567656 | |
|支付状态|payStatus| PAY_APPLIED| 参见附录[A.1](#a1-支付状态) |
|消息|message| | |

~~~
{
    "success": true,
    "errorMsg": null,
    "errorCode": null,
    "data": {
        "mchtOrderNo": "F20190402123",
        "psp": "ALLINPAY",
        "agreeid": "201905041150567656",
        "payStatus": "PAY_SUCCEED",
        "message": null
    }
}
~~~

#### 5.5 重新申请支付和获取支付短信
本节仅针对对支付时需要短信验证码二次确认的支付渠道。
支付的短信验证码一般有效时间为3分钟，超时需重新申请短信验证码。或用户想使用其他银行卡的快捷支付协议进行支付，均可调用本接口。

* url: {api\_url}/order/redoQuickpay
* method: POST
* request: Body Parameter (application/json)

需传入的json对象结构如下:

|字段名称|参数| 是否必填 |例子|说明|
|:--|:--|:--|:--|:--|
|商户订单号| mchtOrderNo | 是 | F20190402123  |  |
|快捷支付协议号|agreeid | 是 | 201905041150567656  |  |

* request example:

~~~
{
	"agreeid": "201905041150567656",
	"mchtOrderNo": "F20190402123"
}
~~~

* response:

|字段名称|参数| 例子|说明|
|:--|:--|:--|:--|
|商户订单号| mchtOrderNo |  F20190402123  |  |
|支付公司代码 | psp | ALLINPAY | 建议商户在前端商城中根据支付公司代码放上对应支付公司的LOGO, 参见 [A.4](#a4-支付公司代码) |
|协议号|agreeid| 201905041150567656 | |
|支付状态|payStatus| PAY_APPLIED| 参见附录[A.1](#a1-支付状态) |
|消息|message| | |

~~~
{
    "success": true,
    "errorMsg": null,
    "errorCode": null,
    "data": {
        "mchtOrderNo": "F20190402123",
        "psp": "ALLINPAY",
        "agreeid": "201905041150567656",
        "payStatus": "PAY_APPLIED",
        "message": "请输入短信验证码"
    }
}
~~~



#### 5.6 订单查询
若同步调用的返回的payStatus为"PAY\_SMS\_CONFIRMED"状态，或商户侧的服务器没有收到订单支付成功的异步消息通知，可以主动查询订单的支付结果信息。

* url: {api\_url}/order/queryOrder?mchtOrderNo={mchtOrderNo}
* method: GET
* request: Query Params

|字段名称|参数| 是否必填 |例子|说明|
|:--|:--|:--|:--|:--|
|商户订单号| mchtOrderNo | 是 | 1904052344  |  |

* response: 
返回结果为[2.4](#24-单笔订单回执查询) 中orderResultDto，重点关注其payStatus和paymentDatetime。

### 6. 配单支付推单
#### 6.1 创建订单并触发配单支付

调用方式详情:

* url: {api\_url}/order/createAndMockpay
* method: POST
* request: Body parameter (application/json)

请传入一个单个的order类型对象，order类型的结构如下

|字段名称|参数|类型|是否必填|例子|说明|
|:--|:--|:--|:--|:--|:--|
| 是否需要自动申报至海关 | needDeclare | Boolean | 否 | true | 是否在支付成功后自动进行报关。若不设置该订单是否需要申报海关，则将按照商户在入网时的业务形态决定是否进行申报。若设置为false但之后需申报，可后置调用[8.1 支付信息海关推单](#81-支付信息海关推单)  |
| 货币代码 | currency | String | 是 | "CNY" | 请固定为CNY |
| 需申报的电子口岸代码 | customsCode | String | 否 | "HG016" | 若需申报则为必填, 参见附录[A.6](#a6-海关及电子口岸代码) |
| 海关关区代码| customsAreaCode | String | 否 | "5130" | 若需申报且申报海关为广州海关时必填 |
| 检验检疫机构代码 | customsJyOrg | String | 否 | "440009" |  若需申报且申报为广州海关时必填|
| 订单货款 | orderGoodsAmount | Long | 否 | 3300 | 单位为分，非必填 |
| 订单税款 | orderTaxAmount | Long | 否 | 50 | 单位为分，非必填 |
| 订单运费 | orderShipmentFeeAmount | Long | 否 | 300 | 单位为分，非必填 |
| 进口类型 | customsInType | String | 否 | "1" | 若需申报且申报天津电子口岸时为必填，1-保税进口，2-直邮进口 |
| 商户订单编号 | mchtOrderNo | String| 是 | "F20190402123" | 只能包含英文字母、数字、短划线-和下划线_，最大长度30位，并请确保商户订单不重复 |
| 订单下单时间 | orderDatetime | String | 否 | "2019-03-20 06:57:29" | 支持格式 yyyy-MM-dd HH:mm:ss |
| 订购人姓名 | payerName | String | 否 | "张三" | 若需申报则必填 |
| 订购人身份证号 | payerNumber | String | 否 | "310113198010101234" | 若需申报则必填|
| 订购人电话 | payerPhone | String | 否 | "18512001234" | 若需申报则必填 |
| 订单额度 | paymentAmount | Long | 是 | 4023 | 请务必注意单位为分 |
| 订单内主要商品信息 | subject | String | 是 | "XXXX化妆品" | 长度不超过200个字符 |
| 接收支付异步通知url | notifyUrl | String | 否 | | 本字段可不填，若不填写，异步通知将发送至本文档第三章[3. 接收异步通知](#3-接收异步通知)在商户后台所填写的商户级别的异步通知url中。若本字段填写则以本字段填写内容为准。消息体会进行签名，签名方式参考第三章。 |
| 订单内商品列表 | items | items类型数组 | 否 | | 可空 |

items类型的结构如下:

|字段名称|参数|类型|是否必填|例子|说明|
|:--|:--|:--|:--|:--|:--|
| 商品名称 | subject | String | 是 | "XXXX口红" | 长度不超过200个字符  |
| 商品链接 | itemLink | String | 是 | "http://www.baidu.com" |  |
| 货号 | articleNum | String | 否 | "WO11111" |  |

* request example:

~~~
{
    "needDeclare": true,
    "currency": "CNY",
    "customsCode": "HG022",
    "customsAreaCode": "5130",
    "customsJyOrg": "440009",
    "customsInType": "2",
    "items": [
      {
        "articleNum": "HH00001",
        "itemLink": "http://www.baidu.com",
        "subject": "测试商品1"
      },
       {
        "articleNum": "HH00002",
        "itemLink": "http://www.baidu.com",
        "subject": "测试商品2"
      }
    ],
    "mchtOrderNo": "F20190402123",
    "orderDatetime": "2019-04-02 11:11:46",
    "payerName": "张三",
    "payerNumber": "310113198010101234",
    "payerPhone": "13800138000",
    "paymentAmount": 4023,
    "subject": "测试商品1"
  }
~~~


* response:

|字段名称|参数| 例子|说明|
|:--|:--|:--|:--|
|商户订单号| mchtOrderNo |  F20190402123  |  |

~~~
{
    "success": true,
    "errorMsg": null,
    "errorCode": null,
    "data": {
        "mchtOrderNo": "F20190402123"
    }
}
~~~

#### 6.2 重新进行配单支付

本章节与[2.7 单笔订单请求重新安排支付](#27-单笔订单请求重新安排支付)完全一致，若客户已对接过，可直接跳过本节。通过本接口，可对支付失败的配单支付订单重新发起支付请求。

* url: {api\_url}/order/arrangePay?mchtOrderNo={mchtOrderNo}
* method: GET
* request: Query Params为商户订单号mchtOrderNo

|字段名称|参数| 是否必填 |例子|说明|
|:--|:--|:--|:--|:--|
|商户订单号| mchtOrderNo | 是 | 1904052344  |  |


* response: 

~~~
{
    "success": true,
    "errorMsg": null,
    "errorCode": null,
    "data": "订单进入支付队列成功"
}
~~~


<!--
#### 6.2 重新进行配单支付
调用方式详情:

* url: {api\_url}/order/redoMockpay
* method: POST
* request: Body parameter (application/json)

传入json对象如下:

|字段名称|参数|类型|是否必填|例子|说明|
|:--|:--|:--|:--|:--|:--|
|商户订单号|mchtOrderNo| String |  是 | |

* request example:

~~~
{
	"mchtOrderNo": "F20190402123"
}
~~~

* response:

|字段名称|参数| 例子|说明|
|:--|:--|:--|:--|
|商户订单号| mchtOrderNo |  F20190402123  |  |

~~~
{
    "success": true,
    "errorMsg": null,
    "errorCode": null,
    "data": {
        "mchtOrderNo": "F20190402123"
    }
}
~~~
-->

#### 6.3 订单查询

可以主动查询订单的支付结果信息。

* url: {api\_url}/order/queryOrder?mchtOrderNo={mchtOrderNo}
* method: GET
* request: Query Params

|字段名称|参数| 是否必填 |例子|说明|
|:--|:--|:--|:--|:--|
|商户订单号| mchtOrderNo | 是 | 1904052344  |  |

* response: 
返回结果为[2.4](#24-单笔订单回执查询) 中orderResultDto，重点关注其payStatus和paymentDatetime。

#### 6.4 订单批次触发配单支付 ####
本章和[2.2 订单批次触发支付](#22-订单批次触发支付)的内容基本一致，唯一区别为所调用的api url略有微小不同，前期使用2.2的用户可以快速切换为配单支付的批次触发接口。

调用本接口对本批次内的订单进行支付与推关。本接口同步返回成功只表明系统接收到整个批次开始支付的指令，支付完成时间取决于协商的合作模式等其他因素。在发送支付指令成功之后，可以进行10分钟/次的订单批次支付&推送结果轮询。

* url: {api\_url}/orderBatch/{orderBatchId}/mockpay
* method: GET
* request Path Variable: url路径参数为创建该订单批次时返回的{orderBatchId}

* response: success参数返回为true时即表示系统已成功安排本批次支付任务

~~~
{
    "success": true,
    "errorMsg": null,
    "errorCode": null,
    "data": {
       “分配任务完成”
    }
}
~~~

* 错误代码: 若success为false，可能出现的errorCode和其对应解释如下

|errorCode|errorMsg| 备注|
|:--|:--|:--|
|50054| 没有需要被分配执行的订单 | 

订单批次中的每一笔订单在支付最终成功或失败后，会发送支付状态通知至商户配置的服务器，后续每一笔订单最终申报完成或失败也将发送申报状态通知至商户配置的服务器，参见[3 接收异步通知](#3-接收异步通知)。

---

### 7. 实名认证
#### 7.1 身份证二要素认证
本接口用于对身份证姓名及身份证号进行二要素认证。为方便测试，在测试环境中，可使用如下数据进行测试: 1开头的身份证号表示认证通过，2开头的身份证表示身份证号不在库中，3开头的身份证号表示名字不合法，4开头的身份证号表示身份证号不合法，其他情况表示认证不通过。调用前需先在商户后台购买实名认证权益(少量客户可先进行调用，由系统后置发送账单，商家以一定周期支付款项)，请注意在测试环境中为测试的完整性，也需实际进行权益购买。本系统已对接多个认证渠道，单渠道无法确认身份是否一致的情况下自动切换备用认证渠道。

![购买实名认证权益页面](doc/realPerson.png)

* url: {api\_url}/realPerson/val?idno={idno}&name={name}
* method: GET
* request: Query Params

|字段名称|参数| 是否必填 |例子|说明|
|:--|:--|:--|:--|:--|
|身份证号| idno | 是 |110113198010101234  | 在测试环境中，可使用如下数据进行测试: 1开头的身份证号表示认证通过，2开头的身份证表示身份证号不在库中，3开头的身份证号表示名字不合法，4开头的身份证号表示身份证号不合法，其他情况表示认证不通过。 |
|姓名| name | 是 | 李白 | |
 
* response: 

|字段名称|参数| 例子|说明|
|:--|:--|:--|:--|
|实名认证订单号| realPersonValidationOrderId | 647ff383-06c1-4cf7-9a4a-6a58566efe5d  | 本次实名认证请求的唯一标识 |
|姓名 | name | 李白 | |
|身份证号| idno | 110113198010101234 |  |
|出生日期|birth|19801010 | |
|性别|sex| 男||
|地址|addr| 黑龙江省鹤岗市绥滨县 | |
|认证结果|result| PASS | 认证结果代码参见[A.7 实名认证结果代码](#a7-实名认证结果代码)

~~~
{
  "success": true,
  "errorMsg": null,
  "errorCode": null,
  "data": {
    "realPersonValidationOrderId": "647ff383-06c1-4cf7-9a4a-6a58566efe5d",
    "name": "李白",
    "idno": "110113198010101234",
    "birth": "19801010",
    "addr": "黑龙江省鹤岗市绥滨县",
    "sex": "男",
    "result": "PASS"
  }
}
~~~

### 8. 支付信息推单
#### 8.1 支付信息海关推单
本接口的使用场景有如下两种情形:

* 针对例如扫码支付、银行卡快捷支付等常规支付方式，将已成功支付的订单支付信息推送到指定海关。<!--请注意如果订单是经由[2.自动支付相关接口](#2-自动支付相关接口)创建，则订单本身会自动进行申报，无需再通过本接口触发。或-->若订单在创建支付请求时已指定了参数needDeclare为true，则订单再支付成功后也会自行申报，无需再单独调用本接口。
* 订单状态变更为“申报失败”后，可调用本接口进行申报信息的更新及重新申报。请注意重新申报仅针对部分申报失败原因有效，例如实名认证结果不一致等。其他因商户自身原因导致的申报失败（例如179文未对接完成等），与本系统无关。

接口技术参数如下:

* url: {api\_url}/order/declare
* method: POST
* request: Body parameter (application/json)

|字段名称| 参数| 类型 | 是否必填 |例子|说明|
|:--|:--|:--|:--|:--|:--|
|商户订单编号| mchtOrderNo | String | 是 | "S20190501"  | 商户订单编号，该订单号应已完成支付（即通过查询可查询到支付成功状态） |
| 订购人姓名 | payerName | String | 否 | "张三" | 若不填写则保留该订单最近一次填写的订购人姓名 |
| 订购人身份证号 | payerNumber | String | 否 | "310113198010101234" | 若不填写则保留该订单最近一次填写的订购人身份证号 |
| 订购人电话 | payerPhone | String | 否 | "18512001234" | 若不填写则保留该订单最近一次填写的订购人电话 |
| 需申报的电子口岸代码 | customsCode | String | 否 | "HG016" | 若不填写则保留该订单最近一次填写的申报垫资口岸代码。参见附录[A.6](#a6-海关及电子口岸代码) |
| 海关关区代码| customsAreaCode | String | 否 | "5130" | 若不填写则保留该订单最近一次填写的海关关区代码。若申报海关为广州海关时才需考虑本参数。|
| 检验检疫机构代码 | customsJyOrg | String | 否 | "440009" | 若不填写则保留该订单最近一次填写的检验检疫机构代码。若申报海关为广州海关时才需考虑本参数。 |
| 进口类型 | customsInType | String | 否 | "1" | 若不填写则保留该订单最近一次填写的进口类型。1-保税进口，2-直邮进口。若申报天津电子口岸时才需考虑本参数。 |

* request example:

~~~
{
  "customsCode": "HG016",
  "mchtOrderNo": "S20190501",
  "payerName": "张三",
  "payerNumber": "310113198010101234",
  "payerPhone": "18512001234"
}
~~~

* response: 

返回String: "申报信息已提交"。收到success为true的标识后，订单将进入后续的自动申报动作，申报完成后将发送异步通知给商户，参见[3.5 申报状态异步通知](#35-申报状态异步通知)。

~~~
{
  "success": true,
  "errorMsg": null,
  "errorCode": null,
  "data": "申报信息已提交"
}
~~~

### 9. 退款
#### 9.1 退款申请
<!--请注意如果订单是经由[2.自动支付相关接口](#2-自动支付相关接口)提交至系统，则无法进行退款。-->退款将从商户的现金账户中扣除申请的退款额度，若现金账户余额不足将导致退款失败。另微信/支付宝相关的支付方式，退款时需保证退款当日的总正向流水大于退款金额。

接口技术参数如下:

* url: {api\_url}/order/refund
* method: POST
* request: Body parameter (application/json)

|字段名称| 参数| 类型 | 是否必填 |例子|说明|
|:--|:--|:--|:--|:--|:--|
| 商户原始订单编号 | mchtOrderNo | String | 是 | "S20190501"  | 商户订单编号，该订单号应已完成支付（即通过查询可查询到支付成功状态） |
| 退款请求编号 | mchtRefundOrderNo | String | 是 | "REFUND_S20190501" | 商户对该退款请求的编号，退款请求编号不能重复 |
| 退款额度(分) | refundAmount | Long | 是 | 1225 | 退款额度，单位为分 |

* request example:

~~~
{
  "mchtOrderNo": "S20190501",
  "mchtRefundOrderNo": "REFUND_S20190501",
  "refundAmount": 1225
}
~~~

* response: 

|字段名称| 参数| 类型 |例子|说明|
|:--|:--|:--|:--|:--|
| 商户原始订单编号 | mchtOrderNo | String| "S20190501"  | 商户订单编号|
| 退款请求编号 | mchtRefundOrderNo | String | "REFUND_S20190501" | 商户对该退款请求的编号，退款请求编号不能重复 |
| 退款额度(分) | refundAmount | Long | 1225 | 退款额度，以分为单位 |
| 退款状态 | refundStatus | String | "REFUND_REQUESTED" | 参见[A.8 退款状态代码](#a8-退款状态代码), 一般正常返回REFUND_REQUESTED状态，需后置进行退款状态查询。 |

~~~
{
  "success": true,
  "errorMsg": null,
  "errorCode": null,
  "data": {
    "mchtOrderNo": "S20190501",
    "mchtRefundOrderNo": "REFUND_S20190501",
    "refundAmount": 1225,
    "refundStatus": "REFUND_REQUESTED"
  }
}
~~~

#### 9.2 退款状态查询

该接口用于查询退款状态，请注意退款成功状态仅表示退款已成功被渠道受理（例如支付宝、微信支付、银联等），并不代表款项已退回至用户处。具体用户收到退款的时间无法查询，一般在退款状态变更为退款成功后1个工作日。

接口技术参数如下:

* url: {api\_url}/order/refund?mchtRefundOrderNo={mchtRefundOrderNo}
* method: GET
* request: Query Params

|字段名称|参数| 是否必填 |例子|说明|
|:--|:--|:--|:--|:--|
|退款请求编号| mchtRefundOrderNo | 是 | "REFUND_S20190501"  |  |

* response: 

|字段名称| 参数| 类型 |例子|说明|
|:--|:--|:--|:--|:--|
| 商户原始订单编号 | mchtOrderNo | String| "S20190501"  | 商户订单编号 |
| 退款请求编号 | mchtRefundOrderNo | String | "REFUND_S20190501" | 商户对该退款请求的编号 |
| 退款额度(分) | refundAmount | Long | 1225 | 退款额度，以分为单位 |
| 退款状态 | refundStatus | String | "REFUND_SUCCEED" | 参见[A.8 退款状态代码](#a8-退款状态代码)|

~~~
{
  "success": true,
  "errorMsg": null,
  "errorCode": null,
  "data": {
    "mchtOrderNo": "S20190501",
    "mchtRefundOrderNo": "REFUND_S20190501",
    "refundAmount": 1225,
    "refundStatus": "REFUND_SUCCEED"
  }
}
~~~

### 10. 手机H5/小程序支付（微信公众号/小程序/支付宝服务窗支付）
#### 10.1 创建订单并生成手机中拉起支付所需参数
通过该接口可直接创建单笔订单并根据所需h5支付的类型(微信公众号/支付宝服务窗)返回在各自的手机浏览器中拉起对应支付的支付参数。当该订单在手机中支付完成时，支付结果（成功/失败）将以异步通知的形式返回给商户服务器，参见[3.4](#34-支付状态异步通知)。若支付成功，根据订单设置的是否需要自动申报字段needDeclare，若需要则将继续自动执行申报任务，申报结果也将以异步通知的形式发送，参见[3.5](#35-申报状态异步通知)。订单的过期时间为15分钟。

![](doc/warning_h5pay.png)

* url: {api\_url}/order/createAndH5Pay
* method: POST
* request: Body parameter (application/json)

请传入一个单个的order类型对象，order类型的结构如下

|字段名称|参数|类型|是否必填|例子|说明|
|:--|:--|:--|:--|:--|:--|
|h5支付类型| h5PayType | String | 是 | "WECHATPAY" | 支持微信公众号、支付宝服务窗，参见 [A.9](#a9-H5支付类型) |
| openId | openId | String | 是 | "oALT01I3_3N53eTx03kVgerL6iSU" | 微信渠道: 通过OAuth2.0协议标准得到的微信open_id [参考文档](https://open.weixin.qq.com/cgi%02bin/showdocument?action=dir_list&t=resource/res_list&verify=1&id=open1419316505&token=&lang=zh_CN); 支付宝渠道: 通过OAuth2.0协议标准得到支付宝买家的唯一用户号（ 2088 开头的 16 位纯数字） [参考文档](https://docs.open.alipay.com/220/105337) |
| 是否需要申报至海关 | needDeclare | Boolean | 否 | true | 是否在支付成功后自动进行报关。若不设置该订单是否需要申报海关，则将按照商户在入网时的业务形态决定是否进行申报。若设置为false但之后需申报，可后置调用[8.1 支付信息海关推单](#81-支付信息海关推单) |
| 货币代码 | currency | String | 是 | "CNY" | 请固定为CNY |
| 需申报的电子口岸代码 | customsCode | String | 否 | "HG016" | 若需申报则为必填, 参见附录[A.6](#a6-海关及电子口岸代码) |
| 海关关区代码| customsAreaCode | String | 否 | "5130" | 若需申报且申报海关为广州海关时必填 |
| 检验检疫机构代码 | customsJyOrg | String | 否 | "440009" |  若需申报且申报为广州海关时必填|
| 进口类型 | customsInType | String | 否 | "1" | 若需申报且申报天津电子口岸时为必填，1-保税进口，2-直邮进口 |
| 商户订单编号 | mchtOrderNo | String| 是 | "F20190402123" | 只能包含英文字母、数字、短划线-和下划线_，最大长度30位，并请确保商户订单不重复 |
| 订单下单时间 | orderDatetime | String | 否 | "2019-03-20 06:57:29" | 支持格式 yyyy-MM-dd HH:mm:ss |
| 订购人姓名 | payerName | String | 否 | "张三" | 若需申报则必填 |
| 订购人身份证号 | payerNumber | String | 否 | "310113198010101234" | 若需申报则必填|
| 订购人电话 | payerPhone | String | 否 | "18512001234" | 若需申报则必填 |
| 订单额度 | paymentAmount | Long | 是 | 4023 | 请务必注意单位为分 |
| 订单内主要商品信息 | subject | String | 是 | "XXXX化妆品" | 长度不超过200个字符 |
| 接收支付异步通知url | notifyUrl | String | 否 | | 本字段可不填，若不填写，异步通知将发送至本文档第三章[3. 接收异步通知](#3-接收异步通知)在商户后台所填写的商户级别的异步通知url中。若本字段填写则以本字段填写内容为准。消息体会进行签名，签名方式参考第三章。 |
| 订单内商品列表 | items | items类型数组 | 否 | | 可空 |

items类型的结构如下:

|字段名称|参数|类型|是否必填|例子|说明|
|:--|:--|:--|:--|:--|:--|
| 商品名称 | subject | String | 是 | "XXXX口红" | 长度不超过200个字符 |
| 商品链接 | itemLink | String | 是 | "http://www.baidu.com" |  |
| 货号 | articleNum | String | 否 | "WO11111" |  |


* request example: 

~~~
  {
  	"h5PayType": "WECHATPAY",
	"openId": "oALT01I3_3N53eTx03kVgerL6iSU",
  	"needDeclare" : false,
  	"currency": "CNY",
  	"customsCode": "HG022",
  	"customsAreaCode": "5130",
  	"customsJyOrg": "440009",
  	"customsInType": "2",
  	"items": [
      {
        "articleNum": "HH00001",
        "itemLink": "http://www.baidu.com",
        "subject": "测试商品1"
      },
       {
        "articleNum": "HH00002",
        "itemLink": "http://www.baidu.com",
        "subject": "测试商品2"
      }
    ],
    "mchtOrderNo": "F20190402123",
    "orderDatetime": "2019-04-02 11:11:46",
    "payerName": "李白",
    "payerNumber": "310327198009270027",
    "payerPhone": "13800138000",
    "paymentAmount": 3352,
    "subject": "测试商品1"
  }
~~~

* response:

|字段名称|参数| 例子|说明|
|:--|:--|:--|:--|
|商户订单号| mchtOrderNo |  F20190402123  |  |
|h5支付类型| h5PayType | WECHATPAY | 参见 [A.9](#a9-H5支付类型) |
|h5支付参数| h5PayInfo | 由appId,nonceStr,package,paySign,signType,timeStamp组成的json | 在手机的JS代码中使用返回的支付参数拉起对应的微信支付/支付宝支付。微信渠道[参考文档](https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=7_7&index=6); 支付宝渠道 [参考文档](https://doc.open.alipay.com/docs/doc.htm?&docType=1&articleId=105591)|
|支付公司代码 | psp | EASYPAY | 建议商户在前端商城中根据支付公司代码放上对应支付公司的LOGO, 参见 [A.4](#a4-支付公司代码) |
|订单支付状态| payStatus | "PAY_APPLIED" | 参见 [A.1](#a1-支付状态) |

~~~
{
    "success": true,
    "errorMsg": null,
    "errorCode": null,
    "data": {
        "mchtOrderNo": "8D19071021971",
        "psp": "EASYPAY",
        "h5PayInfo": "{\"timeStamp\":\"1563270374\",\"package\":\"prepay_id=wx1617461456376963add1da991526733300\",\"paySign\":\"L/PCmk3GLslqqhgAfP7bfBdtATrd3kXfHlA5KxXks+zuXYS9vGrWtYYdG0yfaCl2M2w59Hagf/LuhO+GCmSPpgrwJKNzazT/5SEICZ0IdPn+O4/NWG5aCiRidILanCip2PV2z8AbpyG8waEe6nC2my8JXgsQzZYinsg7GQ4lnWaXAHMu/eKSQvh4QTrG4p5XNYg5Uo+1A0k2m56GwTWiEmveMizk8D4SllTBFlplbfkkLIeRytTU51otPtXYjR+QmpbtbLOM3LTRsvEbK5qTIbp2V0S6H2AG3clndNbSzuhggYib6jfP1lSz2gEEBuGq8A9z3KUjKCGuGNRckv0oXg==\",\"appId\":\"wxe917f1907972497a\",\"signType\":\"RSA\",\"nonceStr\":\"1PkjRaOpn79qLUkpBSZlxBnxgsoZkxA9\"}",
        "h5PayType": "WECHATPAY",
        "payStatus": "PAY_APPLIED"
    }
}
~~~

#### 10.2 刷新支付所需参数
针对已经提交至系统的订单（例如通过订单批次上传的订单、已创建的订单但客户在手机中长期未支付导致过期的订单、想要切换微信/支付宝的订单，之前支付失败想重新使用h5支付的订单），需要重新生成h5支付参数，可调用此接口:

* url: {api\_url}/order/h5Pay?mchtOrderNo={mchtOrderNo}&h5PayType={h5PayType}
* method: GET
* request: Query Params

|字段名称|参数| 是否必填 |例子|说明|
|:--|:--|:--|:--|:--|
|商户订单号| mchtOrderNo | 是 | 1904052344  |  |
|h5支付类型| h5PayType | 是 | "WECHATPAY" | 支持微信公众号、支付宝服务窗，参见 [A.9](#a9-H5支付类型) |

* response:

|字段名称|参数| 例子|说明|
|:--|:--|:--|:--|
|商户订单号| mchtOrderNo |  F20190402123  |  |
|h5支付类型| h5PayType | WECHATPAY | 参见 [A.9](#a9-H5支付类型) |
|h5支付参数| h5PayInfo | 由appId,nonceStr,package,paySign,signType,timeStamp组成的json | 在手机的JS代码中使用返回的支付参数拉起对应的微信支付/支付宝支付。微信渠道[参考文档](https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=7_7&index=6); 支付宝渠道 [参考文档](https://doc.open.alipay.com/docs/doc.htm?&docType=1&articleId=105591)|
|支付公司代码 | psp | EASYPAY | 建议商户在前端商城中根据支付公司代码放上对应支付公司的LOGO, 参见 [A.4](#a4-支付公司代码) |
|订单支付状态| payStatus | "PAY_APPLIED" | 参见 [A.1](#a1-支付状态) |

~~~
{
    "success": true,
    "errorMsg": null,
    "errorCode": null,
    "data": {
        "mchtOrderNo": "8D19071021971",
        "psp": "EASYPAY",
        "h5PayInfo": "{\"timeStamp\":\"1563270374\",\"package\":\"prepay_id=wx1617461456376963add1da991526733300\",\"paySign\":\"L/PCmk3GLslqqhgAfP7bfBdtATrd3kXfHlA5KxXks+zuXYS9vGrWtYYdG0yfaCl2M2w59Hagf/LuhO+GCmSPpgrwJKNzazT/5SEICZ0IdPn+O4/NWG5aCiRidILanCip2PV2z8AbpyG8waEe6nC2my8JXgsQzZYinsg7GQ4lnWaXAHMu/eKSQvh4QTrG4p5XNYg5Uo+1A0k2m56GwTWiEmveMizk8D4SllTBFlplbfkkLIeRytTU51otPtXYjR+QmpbtbLOM3LTRsvEbK5qTIbp2V0S6H2AG3clndNbSzuhggYib6jfP1lSz2gEEBuGq8A9z3KUjKCGuGNRckv0oXg==\",\"appId\":\"wxe917f1907972497a\",\"signType\":\"RSA\",\"nonceStr\":\"1PkjRaOpn79qLUkpBSZlxBnxgsoZkxA9\"}",
        "h5PayType": "WECHATPAY",
        "payStatus": "PAY_APPLIED"
    }
}
~~~


#### 10.3 订单查询
若商户侧的服务器没有收到订单支付成功的异步消息通知，可以主动查询订单的支付结果等信息，避免在h5支付场景下因服务器未收到通知而造成用户侧相关业务流程无法继续进行的问题。

* url: {api\_url}/order/queryOrder?mchtOrderNo={mchtOrderNo}
* method: GET
* request: Query Params

|字段名称|参数| 是否必填 |例子|说明|
|:--|:--|:--|:--|:--|
|商户订单号| mchtOrderNo | 是 | 1904052344  |  |

* response: 
返回结果为[2.4](#24-单笔订单回执查询) 中orderResultDto，重点关注其payStatus和paymentDatetime即可。

### 11. 二维码被扫支付
#### 11.1 创建订单并进行被扫支付
通过该接口可直接创建单笔订单并根据被扫的二维码类型(微信/支付宝/银联)及所传入的二维码payCode完成支付。当该订单在手机中支付完成时，支付结果（成功/失败）将以异步通知的形式返回给商户服务器，参见[3.4](#34-支付状态异步通知)。若支付成功，根据订单设置的是否需要自动申报字段needDeclare，若需要则将继续自动执行申报任务，申报结果也将以异步通知的形式发送，参见[3.5](#35-申报状态异步通知)。订单的过期时间为15分钟。

测试环境无法进行二维码被扫测试，请使用

* url: {api\_url}/order/createAndScanCode
* method: POST
* request: Body parameter (application/json)

请传入一个单个的order类型对象，order类型的结构如下

|字段名称|参数|类型|是否必填|例子|说明|
|:--|:--|:--|:--|:--|:--|
| 被扫二维码类型 | qrCodeType | String | 是 | "WECHATPAY" | 微信二维码，参见 [A.3](#a3-二维码类型) |
| 被扫消费码 | payCode | String | 是 | "134936194387046267" |手机上的被扫的消费码 |
| 是否需要申报至海关 | needDeclare | Boolean | 否 | true | 是否在支付成功后自动进行报关。若不设置该订单是否需要申报海关，则将按照商户在入网时的业务形态决定是否进行申报。若设置为false但之后需申报，可后置调用[8.1 支付信息海关推单](#81-支付信息海关推单) |
| 货币代码 | currency | String | 是 | "CNY" | 请固定为CNY |
| 需申报的电子口岸代码 | customsCode | String | 否 | "HG016" | 若需申报则为必填, 参见附录[A.6](#a6-海关及电子口岸代码) |
| 海关关区代码| customsAreaCode | String | 否 | "5130" | 若需申报且申报海关为广州海关时必填 |
| 检验检疫机构代码 | customsJyOrg | String | 否 | "440009" |  若需申报且申报为广州海关时必填|
| 进口类型 | customsInType | String | 否 | "1" | 若需申报且申报天津电子口岸时为必填，1-保税进口，2-直邮进口 |
| 商户订单编号 | mchtOrderNo | String| 是 | "F20190402123" | 只能包含英文字母、数字、短划线-和下划线_，最大长度30位，并请确保商户订单不重复 |
| 订单下单时间 | orderDatetime | String | 否 | "2019-03-20 06:57:29" | 支持格式 yyyy-MM-dd HH:mm:ss |
| 订购人姓名 | payerName | String | 否 | "张三" | 若需申报则必填 |
| 订购人身份证号 | payerNumber | String | 否 | "310113198010101234" | 若需申报则必填|
| 订购人电话 | payerPhone | String | 否 | "18512001234" | 若需申报则必填 |
| 订单额度 | paymentAmount | Long | 是 | 4023 | 请务必注意单位为分 |
| 订单内主要商品信息 | subject | String | 是 | "XXXX化妆品" | 长度不超过200个字符 |
| 接收支付异步通知url | notifyUrl | String | 否 | | 本字段可不填，若不填写，异步通知将发送至本文档第三章[3. 接收异步通知](#3-接收异步通知)在商户后台所填写的商户级别的异步通知url中。若本字段填写则以本字段填写内容为准。消息体会进行签名，签名方式参考第三章。 |
| 订单内商品列表 | items | items类型数组 | 否 | | 可空 |

items类型的结构如下:

|字段名称|参数|类型|是否必填|例子|说明|
|:--|:--|:--|:--|:--|:--|
| 商品名称 | subject | String | 是 | "XXXX口红" | 长度不超过200个字符 |
| 商品链接 | itemLink | String | 是 | "http://www.baidu.com" |  |
| 货号 | articleNum | String | 否 | "WO11111" |  |


* request example: 

~~~
  {
  	"qrCodeType": "WECHATPAY",
	"payCode": "134936194387046267",
  	"needDeclare" : false,
  	"currency": "CNY",
  	"customsCode": "HG022",
  	"customsAreaCode": "5130",
  	"customsJyOrg": "440009",
  	"customsInType": "2",
  	"items": [
      {
        "articleNum": "HH00001",
        "itemLink": "http://www.baidu.com",
        "subject": "测试商品1"
      },
       {
        "articleNum": "HH00002",
        "itemLink": "http://www.baidu.com",
        "subject": "测试商品2"
      }
    ],
    "mchtOrderNo": "F20190402123",
    "orderDatetime": "2019-04-02 11:11:46",
    "payerName": "李白",
    "payerNumber": "310327198009270027",
    "payerPhone": "13800138000",
    "paymentAmount": 3352,
    "subject": "测试商品1"
  }
~~~

* response:

|字段名称|参数| 例子|说明|
|:--|:--|:--|:--|
|商户订单号| mchtOrderNo |  F20190402123  |  |
|支付公司代码 | psp | EASYPAY | 建议商户在生成二维码的前端商城中根据支付公司代码放上对应支付公司的LOGO, 参见 [A.4](#a4-支付公司代码) |
|订单支付状态| payStatus | "PAY_APPLIED" | 参见 [A.1](#a1-支付状态) |
|支付信息| message | | | 

~~~
{
    "success": true,
    "errorMsg": null,
    "errorCode": null,
    "data": {
        "mchtOrderNo": "F20190402123",
        "psp": "EASYPAY",
        "payStatus": "PAY_SUCCEED",
        "message": "c2b支付-消费成功"
    }
}
~~~

#### 11.2 重新进行被扫支付
针对已经提交至系统的订单（例如通过订单批次上传的订单、已创建的订单但二维码长期未被扫支付导致被扫码过期的订单、想要切换微信/支付宝/银联二维码的订单，之前支付失败想重新使用被扫支付的订单），需要重新进行被扫支付，可调用此接口:

* url: {api\_url}/order/scanCode?mchtOrderNo={mchtOrderNo}&qrCodeType={qrCodeType}&payCode={payCode}
* method: GET
* request: Query Params

|字段名称|参数| 是否必填 |例子|说明|
|:--|:--|:--|:--|:--|
|商户订单号| mchtOrderNo | 是 | 1904052344  |  |
|二维码类型| qrCodeType | 是 | WECHATPAY | 支持微信、支付宝、银联二维码，参见 [A.3](#a3-二维码类型) |
| 被扫消费码 | payCode | 是 | 134936194387046267 |手机上的被扫的消费码 |

* response: 

|字段名称|参数| 例子|说明|
|:--|:--|:--|:--|
|商户订单号| mchtOrderNo |  19040523834344  |  |
|二维码类型| qrCodeType | WECHATPAY | 参见 [A.3](#a3-二维码类型) |
|二维码url| codeUrl | weixin://wxpay/bizpayurl?pr=X8Zn0PV | |
|支付公司代码 | psp | EASYPAY | 建议商户在生成二维码的前端商城中根据支付公司代码放上对应支付公司的LOGO, 参见 [A.4](#a4-支付公司代码) |


~~~
{
  "success": true,
  "errorMsg": null,
  "errorCode": null,
  "data": {
    "mchtOrderNo": "19040523834344",
    "psp": "EASYPAY",
    "codeUrl": "weixin://wxpay/bizpayurl?pr=X8Zn0PV",
    "qrCodeType": "WECHATPAY"
  }
}
~~~

#### 11.3 订单查询
若商户侧的服务器没有收到订单支付成功的异步消息通知，可以主动查询订单的支付结果等信息，避免在被扫支付场景下因服务器未收到通知而造成用户侧相关业务流程无法继续进行的问题。

* url: {api\_url}/order/queryOrder?mchtOrderNo={mchtOrderNo}
* method: GET
* request: Query Params

|字段名称|参数| 是否必填 |例子|说明|
|:--|:--|:--|:--|:--|
|商户订单号| mchtOrderNo | 是 | 1904052344  |  |

* response: 
返回结果为[2.4](#24-单笔订单回执查询) 中orderResultDto，重点关注其payStatus和paymentDatetime即可。

### 12. 一件代发支付推单
#### 12.1 创建订单并触发一件代发支付

调用方式详情:

* url: {api\_url}/order/createAndTransferPay
* method: POST
* request: Body parameter (application/json)

请传入一个单个的order类型对象，order类型的结构如下

|字段名称|参数|类型|是否必填|例子|说明|
|:--|:--|:--|:--|:--|:--|
| 是否需要自动申报至海关 | needDeclare | Boolean | 否 | true | 是否在支付成功后自动进行报关。若不设置该订单是否需要申报海关，则将按照商户在入网时的业务形态决定是否进行申报。若设置为false但之后需申报，可后置调用[8.1 支付信息海关推单](#81-支付信息海关推单)  |
| 货币代码 | currency | String | 是 | "CNY" | 请固定为CNY |
| 需申报的电子口岸代码 | customsCode | String | 否 | "HG016" | 若需申报则为必填, 参见附录[A.6](#a6-海关及电子口岸代码) |
| 海关关区代码| customsAreaCode | String | 否 | "5130" | 若需申报且申报海关为广州海关时必填 |
| 检验检疫机构代码 | customsJyOrg | String | 否 | "440009" |  若需申报且申报为广州海关时必填|
| 进口类型 | customsInType | String | 否 | "1" | 若需申报且申报天津电子口岸时为必填，1-保税进口，2-直邮进口 |
| 商户订单编号 | mchtOrderNo | String| 是 | "F20190402123" | 只能包含英文字母、数字、短划线-和下划线_，最大长度30位，并请确保商户订单不重复 |
| 订单下单时间 | orderDatetime | String | 否 | "2019-03-20 06:57:29" | 支持格式 yyyy-MM-dd HH:mm:ss |
| 订购人姓名 | payerName | String | 否 | "张三" | 若需申报则必填 |
| 订购人身份证号 | payerNumber | String | 否 | "310113198010101234" | 若需申报则必填|
| 订购人电话 | payerPhone | String | 否 | "18512001234" | 若需申报则必填 |
| 订单额度 | paymentAmount | Long | 是 | 4023 | 请务必注意单位为分 |
| 订单内主要商品信息 | subject | String | 是 | "XXXX化妆品" | 长度不超过200个字符 |
| 接收支付异步通知url | notifyUrl | String | 否 | | 本字段可不填，若不填写，异步通知将发送至本文档第三章[3. 接收异步通知](#3-接收异步通知)在商户后台所填写的商户级别的异步通知url中。若本字段填写则以本字段填写内容为准。消息体会进行签名，签名方式参考第三章。 |
| 订单内商品列表 | items | items类型数组 | 否 | | 可空 |

items类型的结构如下:

|字段名称|参数|类型|是否必填|例子|说明|
|:--|:--|:--|:--|:--|:--|
| 商品名称 | subject | String | 是 | "XXXX口红" | 长度不超过200个字符  |
| 商品链接 | itemLink | String | 是 | "http://www.baidu.com" |  |
| 货号 | articleNum | String | 否 | "WO11111" |  |

* request example:

~~~
{
    "needDeclare": true,
    "currency": "CNY",
    "customsCode": "HG022",
    "customsAreaCode": "5130",
    "customsJyOrg": "440009",
    "customsInType": "2",
    "items": [
      {
        "articleNum": "HH00001",
        "itemLink": "http://www.baidu.com",
        "subject": "测试商品1"
      },
       {
        "articleNum": "HH00002",
        "itemLink": "http://www.baidu.com",
        "subject": "测试商品2"
      }
    ],
    "mchtOrderNo": "F20190402123",
    "orderDatetime": "2019-04-02 11:11:46",
    "payerName": "张三",
    "payerNumber": "310113198010101234",
    "payerPhone": "13800138000",
    "paymentAmount": 4023,
    "subject": "测试商品1"
  }
~~~


* response:

|字段名称|参数| 例子|说明|
|:--|:--|:--|:--|
|商户订单号| mchtOrderNo |  F20190402123  |  |

~~~
{
    "success": true,
    "errorMsg": null,
    "errorCode": null,
    "data": {
        "mchtOrderNo": "F20190402123"
    }
}
~~~

#### 12.2 重新进行一件代发支付

本章节与[2.7 单笔订单请求重新安排支付](#27-单笔订单请求重新安排支付)完全一致，若客户已对接过，可直接跳过本节。通过本接口，可对支付失败的一件代发支付订单重新发起支付请求。

* url: {api\_url}/order/arrangePay?mchtOrderNo={mchtOrderNo}
* method: GET
* request: Query Params为商户订单号mchtOrderNo

|字段名称|参数| 是否必填 |例子|说明|
|:--|:--|:--|:--|:--|
|商户订单号| mchtOrderNo | 是 | 1904052344  |  |


* response: 

~~~
{
    "success": true,
    "errorMsg": null,
    "errorCode": null,
    "data": "订单进入支付队列成功"
}
~~~

#### 12.3 订单查询

可以主动查询订单的支付结果信息。

* url: {api\_url}/order/queryOrder?mchtOrderNo={mchtOrderNo}
* method: GET
* request: Query Params

|字段名称|参数| 是否必填 |例子|说明|
|:--|:--|:--|:--|:--|
|商户订单号| mchtOrderNo | 是 | 1904052344  |  |

* response: 
返回结果为[2.4](#24-单笔订单回执查询) 中orderResultDto，重点关注其payStatus和paymentDatetime。

#### 12.4 订单批次触发一件代发支付 ####
本章和[2.2 订单批次触发支付](#22-订单批次触发支付)的内容基本一致，唯一区别为所调用的api url略有微小不同，前期使用2.2的用户可以快速切换为一件代发支付的批次触发接口。

调用本接口对本批次内的订单进行支付与推关。本接口同步返回成功只表明系统接收到整个批次开始支付的指令，支付完成时间取决于协商的合作模式等其他因素。在发送支付指令成功之后，可以进行10分钟/次的订单批次支付&推送结果轮询。

* url: {api\_url}/orderBatch/{orderBatchId}/transferPay
* method: GET
* request Path Variable: url路径参数为创建该订单批次时返回的{orderBatchId}

* response: success参数返回为true时即表示系统已成功安排本批次支付任务

~~~
{
    "success": true,
    "errorMsg": null,
    "errorCode": null,
    "data": {
       “分配任务完成”
    }
}
~~~

* 错误代码: 若success为false，可能出现的errorCode和其对应解释如下

|errorCode|errorMsg| 备注|
|:--|:--|:--|
|50054| 没有需要被分配执行的订单 | 

订单批次中的每一笔订单在支付最终成功或失败后，会发送支付状态通知至商户配置的服务器，后续每一笔订单最终申报完成或失败也将发送申报状态通知至商户配置的服务器，参见[3 接收异步通知](#3-接收异步通知)。

---


## 附录A

### A.1 支付状态
|状态代码|状态说明|
|:--|:--|
|INIT\_FEE\_PENDING|初始化订单，未进行手续费对账|
|NOT\_PAYED|未支付|
|PAY\_APPLIED|已申请支付|
|PAY\_SMS\_CONFIRMED|支付中间状态|
|PAY\_SUCCEED|支付成功|
|PAY\_FAILED|支付失败|

### A.2 申报状态
|状态代码|状态说明|
|:--|:--|
| NOT\_DECLARED | 未申报|
| PENDING_DECLARE | 待申报 |
| DECLARING | 申报中 |
| DECLARED | 已申报 |
| DECLARE_FAILED | 申报失败 |

### A.3 二维码类型
|二维码类型|说明|
|:--|:--|
|WECHATPAY| 微信二维码 |
|ALIPAY| 支付宝二维码 |
|UNIONPAY | 银联二维码 |

<!--
### A.4 支付公司代码
|支付公司代码|说明| logo url |
|:--|:--|:--|
|ALLINPAY| 通联支付 | [图标url](http://www.allinpay.com/images/logo1.png) |
|EASYPAY | 易生支付 | [图标url](http://www.bhecard.com/images_new/logo.jpg)|
|LYCHEEPAY| 快付通 | [图标url](https://www.kftpay.com.cn/templets/kuaifutong/images/img_logo.png)|
|SUMPAY| 商盟支付(统统付) | [图标url](https://www.sumpay.cn/portal/rec/public/img/LOGO-TTP.png) | -->

### A.5 银行代码
|银行代码|银行名称|单日上限|
|:--|:--|:--|
|0102|中国工商银行| |
|0103|中国农业银行| 5万 |
|0104|中国银行| 5万 |
|0105|中国建设银行| 5万 |
|0301|交通银行| 5万 |
|0302|中信银行|  |
|0303|中国光大银行| 5万 |
|0304|华夏银行| |
|0305|中国民生银行| |
|0306|广东发展银行| 5万 |
|0307|平安银行| |
|0308|招商银行| |
|0309|兴业银行| 5万 |
|0310|上海浦东发展银行| 5万 |
|04012900|上海银行|  |
|999|网联测试专用银行|

### A.6 海关及电子口岸代码
请注意由于使用的支付渠道不同，部分海关可能在商户入网的支付渠道上未完成对接，请将需要通关的口岸向业务人员预先咨询。

|海关代码 CustomsCode | 海关名称 | 说明|
|:--|:--|:--|
|HG013|郑州海关||
|HG014|宁波海关| 宁波海关对接需要填写支付公司编码，具体请询问相关业务人员 |
|HG016|重庆电子口岸（总署版）|若需要推送的海关不在列表中且其为总署版，可使用此代码进行推送|
|HG018|广州电子口岸3.0（总署版）||
|HG019|深圳电子口岸（总署版）||
|HG021|杭州电子口岸（总署版）||
|HG022|上海电子口岸（总署版）| 上海公服平台对接需要填写支付方式，具体请询问相关业务人员 |
|HG026|天津电子口岸（总署版）||
|HG044|山东海关 ||
|HG055|福州海关 (总署版)|其他总署版亦例如HG016福州亦可放行|

### A.7 实名认证结果代码

|认证结果代码|说明|
|:--|:--|
|PASS|实名认证通过|
|NOT_PASS|实名认证不通过|
|NAME_INVALID|名字不合法|
|IDNO_INVALID|身份证号不合法|
|CANNOT_FIND_ID|身份证号不在库中|
|INSUFFICIENT_FEE|实名认证手续费不足|
|OTHER_ERROR|实名认证服务异常，请联系技术人员排查|

### A.8 退款状态代码

|退款状态代码|说明|
|:--|:--|
|REFUND_INIT|收到退款请求|
|REFUND_REQUESTED|退款中|
|REFUND_SUCCEED|退款成功|
|REFUND_FAILED|退款失败|

### A.9 H5支付类型

|H5支付类型|说明|
|:--|:--|
|WECHATPAY| 微信公众号 |
|ALIPAY| 支付宝服务窗 |



## 附录B
### B.1 银行卡绑定流程说明
![](doc/binding1.png)
![](doc/binding2.png)
![](doc/binding3.png)
![](doc/binding4.png)
![](doc/binding5.png)



