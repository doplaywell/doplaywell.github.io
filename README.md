# 个人中心


----------


## 获取用户个人信息
> GET /api/v2/inner/user/account
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 登陆tocken | - | - | header
source | 否 | string | 来源：0 web | - | -| body

### 返回信息
```javascript
ResponseMessage {
inSensitive (boolean, optional),
level (integer, optional): 用户实名认证的等级 ,
loginStrategy (integer, optional): 登陆验证策略 ,
mail (string, optional): 邮箱 ,
mailChecked (boolean, optional): 邮箱是否验证 ,
mfa (boolean, optional): 是否设置谷歌验证 ,
phone (string, optional): 手机 ,
security (integer, optional): 用户安全等级 ,
sensitiveCode (integer, optional): 导致敏感操作code 13 手机修改 14 谷歌修改 15 资金密码修改 ,
sensitiveDate (string, optional): 敏感操作时间 例如：2018-02-05 12:00:00 ,
tradePwd (boolean, optional): 是否设置交易密码 ,
tradeStrategy (integer, optional): 交易验证策略 ,
twiceStrategy (integer, optional): 二次验证策略 ,
withdrawStrategy (integer, optional): 提现验证策略
}
```

### 返回示例
```javascript
{
  "code": 0,
  "data": {
    "inSensitive": true,
    "level": 1,
    "loginStrategy": 0,
    "mail": "example@aa.com",
    "mailChecked": true,
    "mfa": false,
    "phone": "13112121111",
    "security": 0,
    "sensitiveCode": 13,
    "sensitiveDate": "2018-02-05 12:00:00",
    "tradePwd": false,
    "tradeStrategy": 0,
    "twiceStrategy": 0,
    "withdrawStrategy": 0
  },
  "err_msg": "string",
  "ts": 0
}

```


----------


## 找回密码相关

## 第一步 检查用户
> POST /api/v2/inner/user/findPassword/checkUser
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
userName | 是 | string | 用户名 | 邮箱或者手机 | - | body
csessionid | 是 | string | 阿里校验csessionid | - | -| body
sig | 是 | string | 阿里校验sig| - | -| body
token | 是 | string | 阿里校验token| - | -| body
scene | 是 | string | 阿里校验scene| - | -| body
lang | 否 | number | 语言代号 | 0 中文，1英文，2日文，泰3，越4 | 默认中文 | body

### 返回数据结构
```java
ResponseMessage {
  code (integer, optional): 状态码 ,
  data (object, optional): 数据 ,
  err_msg (string, optional): 错误信息 ,
  ts (integer, optional): 系统时间
} 
```

### 返回示例
```javascript
{
	"code": 0,
	"data": {
        "uuid":"858f1207-e94f-4e8b-b308-c855a1ced436",
        "nationCode":86
         },
	"ts": 1527488004308,
	"err_msg": "成功"
}

```

## 第二步 校验验证码
> POST /api/v2/inner/user/findPassword/checkCode
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
userName | 是 | string | 用户名 | 邮箱或者手机 | - | body
code | 是 | string | 验证码 |  - | - |body
uuid | 是 | string | uuid |  - |checkUser中返回的uuid|body

### 返回数据结构
```
ResponseMessage {
  code (integer, optional): 状态码 ,
  data (object, optional): 数据 ,
  err_msg (string, optional): 错误信息 ,
  ts (integer, optional): 系统时间
} 
```

### 返回示例
```javascript
{
	"code": 0,
	"data": "找回密码第二步完成！",
	"ts": 1527488004308,
	"err_msg": "成功"
}

```




## 第三步 重置密码
> POST /api/v2/inner/user/findPassword/resetPassword
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
userName | 是 | string | 用户名 | 邮箱或者手机 | - | body
newPassword | 是 | string | 密码| -| 前端加密并进行urlencode | body
confirmPassword| 是 | string | 密码| -| 前端加密并进行urlencode | body
uuid | 是 | string | uuid |  - |checkUser中返回的uuid |body

### 返回数据结构
```
ResponseMessage {
  code (integer, optional): 状态码 ,
  data (object, optional): 数据 ,
  err_msg (string, optional): 错误信息 ,
  ts (integer, optional): 系统时间
} 
```

### 返回示例
```javascript
{
	"code": 0,
	"data": "已成功找回密码！",
	"ts": 1527488421620,
	"err_msg": "成功"
}

```


----------


## 我的邀请信息
> GET  /api/v2/inner/user/inviteInfo
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
lang | 否 | Integer | 语言代号| -| 中文0 英文1 日文2 泰3 越 4 | body
### 返回数据结构
```
Response {
invite (string, optional): 邀请链接 ,
model (Array[string], optional): 模板链接不同语言链接 ,
month (string, optional): 当月返佣 ,
num (integer, optional): 邀请总人数 ,
today (string, optional): 今日返佣 ,
total (string, optional): 累计返佣
}
```
### 返回示例
```javascript
{
  "code": 0,
  "data": {
    "invite": "string",
    "model": [
      "string"
    ],
    "month": "string",
    "num": 0,
    "today": "string",
    "total": "string"
  },
  "err_msg": "string",
  "ts": 0
}

```
## 我的邀请记录
> GET  /api/v2/inner/user/inviteRecord
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
from | 否 | string | 开始查询的条数| -| -| body
to | 否 | string | 结束查询的条数| -| -| body
### 返回数据结构
```
Response {
feeBack (string, optional): 返佣金额 ,
lastTradeDate (integer, optional): 最后交易时间 ,
nickName (string, optional): 被邀请人昵称 ,
registerDate (integer, optional): 注册时间
}
```
### 返回示例
```javascript
{
  "code": 0,
  "data": [
    {
      "feeBack": "string",
      "lastTradeDate": 0,
      "nickName": "string",
      "registerDate": 0
    }
  ],
  "err_msg": "string",
  "ts": 0
}

```
## level1 认证
> POST /api/v2/inner/user/certify
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
cardType | 否 | string | 证件类型 | 1 身份证 2护照 3驾驶证 | body
nation | 否 | string | 国籍id | int值，"0","1" 等 | body
bankId | 否 | string | 银行id | 开放法币交易是使用 int值，"0","1" 等 | body
userName | 否 | string | 真实姓名 | --- | body
birthday | 否 | string | 生日 | 0000-00-00 00:00:00 格式 | body
cardNum | 否 | string | 证件号码 | 支持8-18位数字和字母组合 | body
bankCardNum | 否 |string | 银行卡号 | 开放法币交易是使用 | body
token |否 |string | 修改level token | 修改level1时使用 | body

### 返回信息
```javascript
ResponseMessage {
inSensitive (boolean, optional),
level (integer, optional): 用户实名认证的等级 ,
loginStrategy (integer, optional): 登陆验证策略 ,
mail (string, optional): 邮箱 ,
mailChecked (boolean, optional): 邮箱是否验证 ,
mfa (boolean, optional): 是否设置谷歌验证 ,
phone (string, optional): 手机 ,
security (integer, optional): 用户安全等级 ,
sensitiveCode (integer, optional): 导致敏感操作code 13 手机修改 14 谷歌修改 15 资金密码修改 ,
sensitiveDate (string, optional): 敏感操作时间 例如：2018-02-05 12:00:00 ,
tradePwd (boolean, optional): 是否设置交易密码 ,
tradeStrategy (integer, optional): 交易验证策略 ,
twiceStrategy (integer, optional): 二次验证策略 ,
withdrawStrategy (integer, optional): 提现验证策略
}
```

### 返回示例
```javascript
{
  "code": 0,
  "data": {
    "inSensitive": true,
    "level": 1,
    "loginStrategy": 0,
    "mail": "example@aa.com",
    "mailChecked": true,
    "mfa": false,
    "phone": "13112121111",
    "security": 0,
    "sensitiveCode": 13,
    "sensitiveDate": "2018-02-05 12:00:00",
    "tradePwd": false,
    "tradeStrategy": 0,
    "twiceStrategy": 0,
    "withdrawStrategy": 0
  },
  "err_msg": "string",
  "ts": 0
}

```

## 获取谷歌验证码 
> GET /api/v2/inner/user/getMfa

### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
### 返回信息
```javascript
secret : 谷歌secret
googleCode : 谷歌验证器时间和host
```
### 返回示例
```javascript
{
  "code": 0,
  "data": {
    "secret": "PBRKPO4TVII2XXIE",
    "googleCode": "otpauth://totp/15271803960?secret=PBRKPO4TVII2XXIE&issuer=Coinfex"
  },
  "ts": 1531117541853,
  "err_msg": "成功"
}
```
## 获取OSS上传服务端签名
 > GET /api/v2/inner/user/getOSSPostPolicy
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
### 返回信息
```javascript
accessid string 服务端签名参数
policy string 服务端签名参数
signature string 服务端签名参数
host string 服务端签名参数
expire string 服务端签名参数
```
### 返回示例
```javascript
{
  "code": 0,
  "data": {
    "accessid": "LTAIruvMOcZei5rE",
    "policy": "eyJleHBpcmF0aW9uIjoiMjAxOC0wNy0wOVQwNzoyMjo1Mi4zNTJaIiwiY29uZGl0aW9ucyI6W1siY29udGVudC1sZW5ndGgtcmFuZ2UiLDAsMTA0ODU3NjAwMF1dfQ==",
    "signature": "2g5tkpKdDNmLtKEozNI7q9Jqbj4=",
    "host": "http://rocktest012358.oss-cn-shanghai.aliyuncs.com",
    "expire": "1531120972"
  },
  "ts": 1531117972359,
  "err_msg": "成功"
}
```

## 实名认证状态信息
> GET /api/v2/inner/user/level
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
### 返回信息
```javascript
 level: 实名认证等级 0 未认证 1 level1 2 level2
 cardNo: 证件号码
 cardType: 证件类型
 realName: 真实姓名
 status: level2 等级状态
 nation: 国籍id
 message: level2 未审核通过原因
```
### 返回示例
```javascript
{
  "code": 0,
  "data": {
    "level": 2,
    "cardNo": "420 **** 2222",
    "cardType": 0,
    "realName": "非农人口",
    "status": 1,
    "nation": "0",
    "message": ""
  },
  "ts": 1531118361822,
  "err_msg": "成功"
}
```
## 获取level1 修改凭证
> GET /api/v2/inner/user/modifyLV1Info
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
