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
 status: level2 等级状态 2 驳回 1 通过 0 审核中
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
code | 否 | string | 谷歌验证码 | --- | --- | body
dubblePhoneMsgType | 否 | string | 短信类型 | "25" | --- | body
dubblePhoneCode | 否 | string | 短信验证码 | --- | --- | body
### 返回信息
```javascript
data 即是token
```
### 返回示例
```javascript
{
  "code": 0,
  "data": "23d5e9ff55b74303b20abe0565f1004dhoAl",
  "ts": 1531126019295,
  "err_msg": "成功"
}
```
## 解除谷歌验证器
> POST /api/v2/inner/user/removeMfa
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
dubblePhoneMsgType | 否 | string | 短信类型 | "9" | --- | body
dubblePhoneCode | 否 | string | 短信验证码 | --- | --- | body
csessionid | 否 | string | 阿里校验csessionid | - | -| body
sig | 否 | string | 阿里校验sig| - | -| body
token | 否 | string | 阿里校验token| - | -| body
scene | 否 | string | 阿里校验scene| - | -| body
### 返回信息
```javascript
code = 0 成功 返回用户信息
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
## 重置登陆密码
> POST /api/v2/inner/user/resetPwd
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
newPwd | 是 | string | 新密码 | --- | --- | body
oldPwd | 是 | string | 旧密码 | --- | --- | body
newPwdT | 是 | string | 新密码二次输入 | --- | --- | body
### 返回信息
```javascript
code = 0 成功 返回用户信息
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
## 高级实名认证提交
> POST /api/v2/inner/user/seniorCertify
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
front | 是 | string | 证件正面照 | 照片名称 | -- | body
back | 是 | string | 证件反面照 | 照片名称
hold | 是 | string | 手持照片名称 | 照片名称
start | 是 | string | 证件有效期开始时间 | 0000-00-00 00:00:00 | --- | body
end | 是 | string | 证件过期时间 | 0000-00-00 00:00:00 | --- | body
isLong | 是 | string | 是否长期有效 | "0" 非长期有效 "1" 长期有效 | --- | body
### 返回信息
```javascript
code = 0 成功 返回用户信息
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
## 绑定或者更换邮箱
> POST /api/v2/inner/user/setEmail
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
email | 是 | string | 需要绑定的邮箱名 | --- | --- | body
dubblePhoneMsgType | 否 | string | 短信类型 | "21" | --- | body
dubblePhoneCode | 否 | string | 短信验证码 | --- | --- | body
csessionid | 否 | string | 阿里校验csessionid | - | -| body
sig | 否 | string | 阿里校验sig| - | -| body
token | 否 | string | 阿里校验token| - | -| body
scene | 否 | string | 阿里校验scene| - | -| body
dubbleGoogleCode | 否 | string | 谷歌验证码 | --- | --- | body
withdrawPassword | 否 | string | 资金密码 | 修改邮箱时使用 | --- | body
### 返回信息
```javascript
code = 0 成功 返回用户信息
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
## 绑定或者更换谷歌验证器
>  POST /api/v2/inner/user/setMfa
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
code | 否 | string | 谷歌验证码 | --- | --- | body
dubbleGoogleCode | 否 | string | 原谷歌验证码 | --- |--- | body
dubblePhoneMsgType | 否 | string | 短信类型 | "9" | --- | body
dubblePhoneCode | 否 | string | 短信验证码 | --- | --- | body
status | 是 | boolean | 是否将谷歌设置未二次策略 | --- | --- | body
csessionid | 否 | string | 阿里校验csessionid | - | -| body
sig | 否 | string | 阿里校验sig| - | -| body
token | 否 | string | 阿里校验token| - | -| body
scene | 否 | string | 阿里校验scene| - | -| body
### 返回信息
```javascript
code = 0 成功 返回用户信息
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
## 绑定手机
> POST /api/v2/inner/user/setMobile
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
phone | 是 | string | 手机号码 | --- | --- | body
phoneMsgType | 是 | string | 短信类型 | "17" | --- | body
phoneCode | 是 | string | 短信验证码 | --- | --- | body
dubblePhoneMsgType | 否 | string | 短信类型 | "20" | --- | body
dubblePhoneCode | 否 | string | 短信验证码 | --- | --- | body
dubbleGoogleCode | 否 | string | 谷歌验证码 | --- | --- | body
status | 是 | boolean | 是否将手机设置未二次策略 | --- | --- | body
csessionid | 否 | string | 阿里校验csessionid | - | -| body
sig | 否 | string | 阿里校验sig| - | -| body
token | 否 | string | 阿里校验token| - | -| body
scene | 否 | string | 阿里校验scene| - | -| body
countryCode | 是 | string | 手机区号 | --- | --- | body
### 返回信息
```javascript
code = 0 成功 返回用户信息
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
## 设置策略（二次策略 交易策略 登陆策略）
> POST /api/v2/inner/user/setPolicy
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
code | 是 | string | 策略对应code | -- | --- | body
type | 是 | string |策略对应type | --- | --- | body
dubblePhoneMsgType | 否 | string | 短信类型 | "20" | --- | body
dubblePhoneCode | 否 | string | 短信验证码 | --- | --- | body
dubbleGoogleCode | 否 | string | 谷歌验证码 | --- | --- | body
status | 是 | boolean | 是否将手机设置未二次策略 | --- | --- | body
csessionid | 否 | string | 阿里校验csessionid | - | -| body
sig | 否 | string | 阿里校验sig| - | -| body
token | 否 | string | 阿里校验token| - | -| body
scene | 否 | string | 阿里校验scene| - | -| body

### 返回信息
```javascript
code = 0 成功 返回用户信息
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
## 设置或修改资金密码
 > POST /api/v2/inner/user/setTradePwd
 ### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
pwd | 是 | string | 资金密码 | --- | --- | body
pwdT | 是 |string | 资金密码二次输入 | --- | --- | body
dubblePhoneMsgType | 否 | string | 短信类型 | "20" | --- | body
dubblePhoneCode | 否 | string | 短信验证码 | --- | --- | body
dubbleGoogleCode | 否 | string | 谷歌验证码 | --- | --- | body
csessionid | 否 | string | 阿里校验csessionid | - | -| body
sig | 否 | string | 阿里校验sig| - | -| body
token | 否 | string | 阿里校验token| - | -| body
scene | 否 | string | 阿里校验scene| - | -| body
### 返回信息
```javascript
code = 0 成功 返回用户信息
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

# 资产中心


----------


## 账户资产信息
> GET /api/v2/inner/finance
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | body
assetType | 否 |string | 资产id，支持多个查询 用","分隔 | --- | --- | body
lang | 否 | int | 语言 | --- | --- | body
### 返回数据
```javascript
availableAmount 可用
frozenAmount 冻结
withdrawAmount 可提
```
### 返回示例
```javascript
{
  "code": 0,
  "data": [
    {
      "id": 1,
      "availableAmount": 9,
      "frozenAmount": 0,
      "name": "btc",
      "withdrawAmount": "7.9500"
    },
    {
      "id": 2,
      "availableAmount": 100,
      "frozenAmount": 0,
      "name": "eth",
      "withdrawAmount": "82.543"
    },
    {
      "id": 3,
      "availableAmount": 0,
      "frozenAmount": 0,
      "name": "ltc",
      "withdrawAmount": "0"
    }
  ],
  "ts": 1531126746076,
  "err_msg": "成功"
}
```
## 资金流水
> GET /api/v2/inner/finance/accountRecord
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
assetType | 否 | string | 资产类型 | --- | --- | body
handleType | 否 | string | 流水类型 | --- | --- | body
start | 否 | string | 查询开始时间 | 0000-00-00 00:00:00 | --- | body
end | 否 | string | 查询结束时间 | 0000-00-00 00:00:00 | --- | body
from | 否 | string | 查询起始id | --- | --- | body
size | 否 | string | 查询结束id | --- | --- | body
direction | 否 | string |  查询方向 | --- | --- | body
### 返回数据
```javascript
amount 数量
fee 手续费
```
### 返回示例
```javascript
{
  "code": 0,
  "data": [
    {
      "id": 53539707,
      "createdDate": 1529044214000,
      "modifyDate": null,
      "userId": 350861,
      "assetType": 1,
      "type": 12,
      "amount": 3.5,
      "fee": 0,
      "afterAmount": 3.5,
      "totalAmount": 0,
      "objectId": 123
    }
    {
      "id": 53532245,
      "createdDate": 1529042566000,
      "modifyDate": null,
      "userId": 350861,
      "assetType": 1,
      "type": 11,
      "amount": -4.1,
      "fee": 0,
      "afterAmount": -4.1,
      "totalAmount": 0,
      "objectId": 0
    }
  ],
  "ts": 1531126579555,
  "err_msg": "成功"
}
```
## 添加地址
> POST /api/v2/inner/finance/addAddress
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
address | 是 | string | 地址 | --- | --- | body
assetType | 是 | string |  地址对应的资产类型 | --- | --- | body
remark | 是 | string | 地址标注 | --- | --- | body
isAuth | 是 | boolean | 是否认证地址 | --- | --- | body
source | 是 | int | 0 , 网页 | --- | --- | body
withdrawPassword | 是 | string | 资金密码 | --- | --- | body
dubblePhoneCode | 否 | string | 短信验证码 | --- | --- | body
dubbleGoogleCode | 否 | string | 谷歌验证码 | --- | --- | body
### 返回数据
```javascript
code=0成功
```
### 返回示例
```javascript
{
  "code": 0,
  "data": {},
  "err_msg": "string",
  "ts": 0
}
```
## 申请提现
> POST /api/v2/inner/finance/applyWithdraw
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
assetType | 是 | int |  资产类型 | --- | --- | body
addressId | 是 | long | 地址id | --- | --- | body
withdrawFee | 是 | string | 手续费 | -- | --- | body
withdrawAmount | 是 | string | 提现数量 | --- | -- | body
source | 是 | int | 0 , 网页 | --- | --- | body
withdrawPassword | 是 | string | 资金密码 | --- | --- | body
dubblePhoneCode | 否 | string | 短信验证码 | --- | --- | body
dubbleGoogleCode | 否 | string | 谷歌验证码 | --- | --- | body
### 返回数据
```javascript
code=0 成功
```
### 返回示例
```javascript
{
  "code": 0,
  "data": {},
  "err_msg": "string",
  "ts": 0
}
```

## 取消体现
> GET /api/v2/inner/finance/cancelWithdraw
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
assetType | 是 | int |  资产类型 | --- | --- | body
id | 是 | long | 提现记录id | --- | --- | body
### 返回数据
```javascript
code=0 成功
```
### 返回示例
```javascript
{
  "code": 0,
  "data": {},
  "err_msg": "string",
  "ts": 0
}
```
## 删除提币地址
> POST /api/v2/inner/finance/disabledCoinAddress
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
id | 是 | long | 提现地址id | --- | --- | body
### 返回数据
```javascript
code = 0 成功
```
### 返回示例
```javascript
{
  "code": 0,
  "data": {},
  "ts": 1531126391068,
  "err_msg": "成功"
}
```

## 提现相关额度
> GET /api/v2/inner/finance/financeLimit
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
lang | 是 | int | 语言 | --- | --- | body
### 返回数据
```javascript
data list返回所有资产提币限额
```
### 返回示例
```javascript
{
  "code": 0,
  "data": [
    {
      "max": "100,000.0000",
      "remain": "100,000.0000",
      "name": "btc",
      "available": "7.9500",
      "id": 1,
      "tips": true
    },
    {
      "max": "90.000",
      "remain": "90.000",
      "name": "eth",
      "available": "82.543",
      "id": 2,
      "tips": true
    },
    {
      "max": "2.000",
      "remain": "2.000",
      "name": "ltc",
      "available": "0",
      "id": 3,
      "tips": true
    }
  ],
  "ts": 1531126391068,
  "err_msg": "成功"
}
```
## 获取充值地址
> GET /api/v2/inner/finance/rechargeAddress
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
lang | 是 | int | 语言 | --- | --- | body
assetType | 是 | int | 资产id | --- | --- | body
### 返回数据
```javascript
asset 资产id
assetName 资产名
address 地址
```
### 返回示例
```javascript
{
  "code": 0,
  "data": {
    "asset": 1,
    "assetName": "btc",
    "address": "jfckmgeorgmvl5io9vmfvw",
    "confirmNum": 0
  },
  "ts": 1531126320336,
  "err_msg": "成功"
}
```
## 提现记录
> GET /api/v2/inner/finance/withdrawRecord
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
assetType | 是 | int | 资产id | --- | --- | body
start | 否 | string | 查询开始时间 | 0000-00-00 00:00:00 | --- | body
end | 否 | string | 查询结束时间 | 0000-00-00 00:00:00 | --- | body
from | 否 | string | 查询起始id | --- | --- | body
size | 否 | string | 查询结束id | --- | --- | body
direction | 否 | string |  查询方向 | --- | --- | body
### 返回数据
```javascript
data list返回
```
### 返回示例
```javascript
{
  "code": 0,
  "data": [
    {
      "id": 7220,
      "createdDate": 1517393107000,
      "modifyDate": 1523627048000,
      "userId": 350861,
      "assetType": 1,
      "address": "1JkbhiWd6j9Z5iDA9qmE8DHVLsEnvUv2PQ",
      "amount": 0.999,
      "fee": 0.001,
      "status": 5,
      "targetUserid": 0,
      "targetType": -1,
      "outDesc": null,
      "adminDesc": null,
      "ipAddress": 2130706433,
      "txid": "",
      "isSendEmail": 0,
      "adminOperator": 22
    }
    {
      "id": 7225,
      "createdDate": 1517647447000,
      "modifyDate": null,
      "userId": 350861,
      "assetType": 1,
      "address": "1JkbhiWd6j9Z5iDA9qmE8DHVLsEnvUv2PQ",
      "amount": 9.999,
      "fee": 0.001,
      "status": -3,
      "targetUserid": 0,
      "targetType": -1,
      "outDesc": null,
      "adminDesc": null,
      "ipAddress": 3232235660,
      "txid": "",
      "isSendEmail": 0,
      "adminOperator": 0
    }
  ],
  "ts": 1531128838993,
  "err_msg": "成功"
}
```
## 获取提现地址
> GET /api/v2/inner/finance/withdrawAddress
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | header
assetType | 是 | int | 资产id | --- | --- | body
### 返回数据
```javascript
data list返回
### 返回示例
```javascript
{
  "code": 0,
  "data": {},
  "ts": 1531129074366,
  "err_msg": "成功"
}
```
# 交易
## 委托交易
> POST /api/v2/inner/trade/placeOrder

参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | jwt | - | - | header
tradePassword | 否 | string | 交易密码 | - | 返回值是57或111时，下次请求要带 | body
symbol | 是 | number| 交易对id | - | - | body
type | 是 | number| 交易类型 | 1买，2卖 | - | body
price | 是 | number| 金额 | 大于0 | - | body
amount | 是 | number | 数量 | 大于0 | - | body
source | 否 | number | 来源代号 | 网页0 手机网页1 第三方2 iso3 android 4 | 默认0 | body

### 返回值数据结构
```
ResponseMessage«委托下单返回值» {
  code (integer, optional): 状态码 ,
  data (委托下单返回值, optional): 数据 ,
  err_msg (string, optional): 错误信息 ,
  ts (integer, optional): 系统时间
}
委托下单返回值 {
  id (integer, optional): 订单id,
  createDate (string, optional): 委托时间 
}
```

### 返回结果示例
```javascript
{
  "code": 0,
  "data": {
    "id": 1037623,
    "createDate": 1527564817000
  },
  "ts": 1527564817585,
  "err_msg": "成功"
}
```
## 委托撤单
> /api/v2/inner/trade/cancelOrder

参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | jwt | - | - | header
symbol | 是 | number| 交易对id | - | - | body
orderId| 是 | number| 订单id | - | - | body
source | 否 | number | 来源代号 | 网页0 手机网页1 第三方2 iso3 android 4 | 默认0 | body

### 返回值数据结构
```
ResponseMessage«int» {
  code (integer, optional): 状态码 ,
  data (integer, optional): 数据 ,
  err_msg (string, optional): 错误信息 ,
  ts (integer, optional): 系统时间
}
```
### 返回示例
```javascript
{
    "code": 0,
    "data": {},
    "ts": 1527479211866,
    "err_msg": "成功"
}
```

## 委托记录 获取缓存
> GET /api/v2/inner/trade/entrustRecord

参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | jwt | - | - | header

### 返回值数据结构
```
ResponseMessage«委托详细信息» {
  code (integer, optional): 状态码 ,
  data (委托详细信息, optional): 数据 ,
  err_msg (string, optional): 错误信息 ,
  ts (integer, optional): 系统时间
}
委托详细信息 {
  allMoney (number, optional): 委托金额 当前委托 ,
  createDate (string, optional): 委托时间 ,
  dealAmount (number, optional): 成交数量 ,
  dealMoney (number, optional): 成交金额 历史委托 ,
  dealPrice (number, optional): 成交均价 历史委托 ,
  from (integer, optional): 来源 0 网页，1 手机网页，2 API，3 IOS 客户端 4 安卓客户端 ... ,
  option (integer, optional): 期权 ,
  orderID (integer, optional): 订单ID ,
  status (integer, optional): 交易状态 0 等待成交 1部分成交 2完全成交 4撤单中 -1撤单 8下单失败 ,
  symbol (integer, optional): 交易对id ,
  tradeAmount (number, optional): 委托数量 ,
  tradePrice (number, optional): 委托价格 当前委托 ,
  type (integer, optional): 委托类型
}
```

### 返回示例
```javascript

{
  "code": 0,
  "data": {
    "currentList": [
      {
        "orderID": 6073,
        "type": 1,
        "symbol": 101,
        "createDate": 1525694515000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.029719,
        "allMoney": 0.029719,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": 0,
        "from": 0
      }
    ],
    "historyList": [
      {
        "orderID": 6001,
        "type": 1,
        "symbol": 101,
        "createDate": 1525316424000,
        "option": null,
        "tradeAmount": 5,
        "tradePrice": 0.031532,
        "allMoney": 0.15766,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": -1,
        "from": 0
      },
      {
        "orderID": 6000,
        "type": 1,
        "symbol": 101,
        "createDate": 1525316414000,
        "option": null,
        "tradeAmount": 10,
        "tradePrice": 0.031532,
        "allMoney": 0.31532,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": 8,
        "from": 0
      },
      {
        "orderID": 5970,
        "type": 1,
        "symbol": 101,
        "createDate": 1524733018000,
        "option": null,
        "tradeAmount": 3,
        "tradePrice": 0.032204,
        "allMoney": 0.096612,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": -1,
        "from": 0
      },
      {
        "orderID": 5969,
        "type": 1,
        "symbol": 101,
        "createDate": 1524732999000,
        "option": null,
        "tradeAmount": 2,
        "tradePrice": 0.032204,
        "allMoney": 0.064408,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": 8,
        "from": 0
      },
      {
        "orderID": 5963,
        "type": 1,
        "symbol": 101,
        "createDate": 1524571642000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.033224,
        "allMoney": 0.033224,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": -1,
        "from": 0
      },
      {
        "orderID": 5962,
        "type": 1,
        "symbol": 101,
        "createDate": 1524571640000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.033224,
        "allMoney": 0.033224,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": -1,
        "from": 0
      },
      {
        "orderID": 5961,
        "type": 1,
        "symbol": 101,
        "createDate": 1524571639000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.033224,
        "allMoney": 0.033224,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": -1,
        "from": 0
      },
      {
        "orderID": 5960,
        "type": 1,
        "symbol": 101,
        "createDate": 1524571636000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.033224,
        "allMoney": 0.033224,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": -1,
        "from": 0
      },
      {
        "orderID": 5959,
        "type": 1,
        "symbol": 101,
        "createDate": 1524571622000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.033224,
        "allMoney": 0.033224,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": -1,
        "from": 0
      },
      {
        "orderID": 5958,
        "type": 1,
        "symbol": 101,
        "createDate": 1524571620000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.033224,
        "allMoney": 0.033224,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": -1,
        "from": 0
      },
      {
        "orderID": 5957,
        "type": 1,
        "symbol": 101,
        "createDate": 1524571618000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.033224,
        "allMoney": 0.033224,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": 8,
        "from": 0
      },
      {
        "orderID": 5956,
        "type": 1,
        "symbol": 101,
        "createDate": 1524571610000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.033155,
        "allMoney": 0.033155,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": 8,
        "from": 0
      },
      {
        "orderID": 5955,
        "type": 1,
        "symbol": 101,
        "createDate": 1524571608000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.033155,
        "allMoney": 0.033155,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": 8,
        "from": 0
      },
      {
        "orderID": 5954,
        "type": 1,
        "symbol": 101,
        "createDate": 1524571607000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.033155,
        "allMoney": 0.033155,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": 8,
        "from": 0
      },
      {
        "orderID": 5953,
        "type": 1,
        "symbol": 101,
        "createDate": 1524571606000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.033155,
        "allMoney": 0.033155,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": 8,
        "from": 0
      },
      {
        "orderID": 5952,
        "type": 1,
        "symbol": 101,
        "createDate": 1524571552000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.000006,
        "allMoney": 0.000006,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": 8,
        "from": 0
      },
      {
        "orderID": 5951,
        "type": 1,
        "symbol": 101,
        "createDate": 1524571547000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.000006,
        "allMoney": 0.000006,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": 8,
        "from": 0
      },
      {
        "orderID": 5950,
        "type": 1,
        "symbol": 101,
        "createDate": 1524571545000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.000006,
        "allMoney": 0.000006,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": 8,
        "from": 0
      },
      {
        "orderID": 5949,
        "type": 1,
        "symbol": 101,
        "createDate": 1524571543000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.000006,
        "allMoney": 0.000006,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": 8,
        "from": 0
      },
      {
        "orderID": 5948,
        "type": 1,
        "symbol": 101,
        "createDate": 1524571542000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.000006,
        "allMoney": 0.000006,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": 8,
        "from": 0
      },
      {
        "orderID": 5947,
        "type": 1,
        "symbol": 101,
        "createDate": 1524571540000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.000006,
        "allMoney": 0.000006,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": 8,
        "from": 0
      },
      {
        "orderID": 5946,
        "type": 1,
        "symbol": 101,
        "createDate": 1524571539000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.000006,
        "allMoney": 0.000006,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": 8,
        "from": 0
      },
      {
        "orderID": 5945,
        "type": 1,
        "symbol": 101,
        "createDate": 1524571537000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.000006,
        "allMoney": 0.000006,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": 8,
        "from": 0
      },
      {
        "orderID": 5944,
        "type": 1,
        "symbol": 101,
        "createDate": 1524571536000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.000006,
        "allMoney": 0.000006,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": 8,
        "from": 0
      },
      {
        "orderID": 5943,
        "type": 1,
        "symbol": 101,
        "createDate": 1524571534000,
        "option": null,
        "tradeAmount": 1,
        "tradePrice": 0.000006,
        "allMoney": 0.000006,
        "dealPrice": 0,
        "dealMoney": 0,
        "dealAmount": 0,
        "status": 8,
        "from": 0
      }
    ]
  },
  "ts": 1527496357919,
  "err_msg": "成功"
}

```

## 委托记录 根据条件查询
> /api/v2/inner/trade/orderRecord

参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | jwt | - | - | header
symbolId | 是 | number | 交易对id | - | 大于0 | body
orderType| 否 | number | 交易类型| 1买，2卖 不传则两个都包含 | -| body
status| 是| number | 要查询的订单状态组合|交易状态 0 等待成交 1部分成交 2完全成交 4撤单中 -1撤单 8下单失败 | 用,分开| body
from | 否 | number | 订单id | 大于0 | 空表示不用，0 表示从第一条开始查，其它正数表明从指定id开始查,必需与size组合| body
size | 否 | number | 查询条数 | 大于0 |  最大200 | body
start | 否 | string | 开始日期 | - | yyyy-MM-dd HH:mm:ss 可以与size 或者end 配合 | body
end | 否 | string | 结束日期  | - |   yyyy-MM-dd HH:mm:ss | body
direction | 否 | number | 查询方向 | 0,1 | 0 由id小到大，1 由id 大到小，默认1 | body

### 返回值数据结构
```
ResponseMessage«委托订单信息» {
  code (integer, optional): 状态码 ,
  data (委托订单信息, optional): 数据 ,
  err_msg (string, optional): 错误信息 ,
  ts (integer, optional): 系统时间
}
委托订单信息 {
  allMoney (number, optional): 委托金额 当前委托 ,
  createDate (string, optional): 委托创建时间 ,
  dealAmount (number, optional): 成交数量 ,
  dealMoney (number, optional): 成交金额 历史委托 ,
  dealPrice (number, optional): 成交均价 历史委托 ,
  from (integer, optional): 来源 0 网页，1 手机网页，2 API，3 IOS 客户端 4 安卓客户端 ... ,
  modifyDate (string, optional): 委托最后修改时间 ,
  option (integer, optional): 期权 ,
  orderID (integer, optional): 订单ID ,
  status (integer, optional): 交易状态 0 等待成交 1部分成交 2完全成交 4撤单中 -1撤单 8下单失败 ,
  symbol (integer, optional): 交易对ID ,
  tradeAmount (number, optional): 委托数量 ,
  tradePrice (number, optional): 委托价格 当前委托 ,
  type (integer, optional): 委托类型
}
```
### 返回示例
```javascript

{
  "code": 0,
  "data": [
    {
      "orderID": 6001,
      "type": 1,
      "symbol": 101,
      "option": null,
      "tradeAmount": 5,
      "tradePrice": 0.031532,
      "allMoney": 0.15766,
      "dealPrice": 0,
      "dealMoney": 0,
      "dealAmount": 0,
      "status": -1,
      "from": 0,
      "createDate": 1525316424000,
      "modifyDate": null
    },
    {
      "orderID": 6000,
      "type": 1,
      "symbol": 101,
      "option": null,
      "tradeAmount": 10,
      "tradePrice": 0.031532,
      "allMoney": 0.31532,
      "dealPrice": 0,
      "dealMoney": 0,
      "dealAmount": 0,
      "status": 8,
      "from": 0,
      "createDate": 1525316414000,
      "modifyDate": 1525415153000
    }
  ],
  "ts": 1527497565180,
  "err_msg": "成功"
}
```
# 注册相关
## 注册
> /api/v2/inner/user/regist

参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
userName |  是 | string | 用户名 | 邮箱号或手机号 | - | body
 code | 是 | String | 校验码 | - | 由对应（手机或邮箱）的发送接口获取| body 
password | 是 | string | 密码 | - | 用户输入的明文加密后进行urlencode | body
passwordAgain | 是 | string | 重复密码 | - | 用户输入的明文加密后进行urlencode | body
agreement| 是 | string | 同意协议| true或者false | - | body
channelId | 否 | number | 渠道 | [待确认] | 默认为0 | body
utmSource| 否 | string | 邀请人|  | 现阶段没用到 | body

### 响应数据格式

```
 ResponseMessage«用户登录后返回的基本信息» {
code (integer, optional):状态码 ,
data (用户登录后返回的基本信息, optional):数据 ,
err_msg (string, optional):错误信息 ,
ts (integer, optional):系统时间
}
用户登录后返回的基本信息 {
needEmail (boolean, optional):是否要绑定邮箱 ,
needTwice (boolean, optional):是否要二次登录 ,
nickName (string, optional):昵称 ,
sessionId (string, optional):sessionId ,
sessionKey (string, optional):sessionKey ,
sso (boolean, optional):是否是sso，true是sso ,
ssoUrl (string, optional):sso url ,
token (string, optional):token ,
uuid (string, optional):二次登录uuid
} 
```
### 响应示例
```javascript
{
	"code": 0,
	"data": {
		"nickName": "151****9785",
		"token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE1Mjc0NzI4NDYsInN1YiI6IntcImNhY2hlS2V5XCI6XCJ1c2Vyc2Vzc2lvbjNlNzMwN2E3LWFhNDQtNDQ5MS05ZDExLTQ0OTg0NTMxYmViNVNmR25cIixcInVzZXJJZFwiOjM1MjE1OH0iLCJpc3MiOiJ1c2VyaWQiLCJhdWQiOiJ3ZWIiLCJleHAiOjE1Mjc0OTA4NDYsIm5iZiI6MTUyNzQ3Mjg0Nn0.0cfAYvUAGkRQzUQ2794X9_MWCS3Sz8SrSyoCS5CPHH4",
		"sessionId": "3e7307a7-aa44-4491-9d11-44984531beb5SfGn",
		"sessionKey": "coinfex_session_id",
		"needTwice": false,
		"uuid": null,
		"sso": false,
		"ssoUrl": null,
		"needEmail": false
	},
	"ts": 1527472846614,
	"err_msg": "成功"
}
```
# 登录相关
## 登录
> POST /api/v2/inner/user/weblogin

参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
loginName | 是 | string | 用户名 | 邮箱或者手机 | - | body
password | 是 | string | 密码 | - | 前端要进行加密并进行urlencode | body
from | 否 | string | 来源 | zendesk | 现阶段只是用来区分是否从zendesk跳转过来 | body
udesk | 是 | string | 是否用到udesk | true,false| 默认false | body
returnTo | 否 | string | 跳回url | - | 配合from 使用 | body
csessionid | 否 | string | 阿里校验csessionid | - | 本接口返回106,-4 时要传| body
sig | 否 | string | 阿里校验sig| - | 本接口返回106,-4 时要传| body
token | 否 | string | 阿里校验token| - | 本接口返回106,-4 时要传| body
scene | 否 | string | 阿里校验scene| - | 本接口返回106,-4 时要传| body

### 返回值数据结构

```
ResponseMessage«用户登录后返回的基本信息» {
  code (integer, optional):状态码 ,
  data (用户登录后返回的基本信息, optional):数据 ,
  err_msg (string, optional):错误信息 ,
  ts (integer, optional):系统时间
}
用户登录后返回的基本信息 {
  needEmail (boolean, optional):是否要绑定邮箱 ,
  needTwice (boolean, optional):是否要二次登录 ,
  nickName (string, optional):昵称 ,
  sessionId (string, optional):sessionId ,
  sessionKey (string, optional):sessionKey ,
  sso (boolean, optional):是否是sso，true是sso ,
  ssoUrl (string, optional):sso url ,
  token (string, optional):token ,
  uuid (string, optional):二次登录uuid
} 
```

### 返回示例

```javascript
{
	"code": 0,
	"data": {
		"nickName": "***@b.com",
		"token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE1Mjc0NzcxMTQsInN1YiI6IntcImNhY2hlS2V5XCI6XCJ1c2Vyc2Vzc2lvbmE3ZDZkMGFhLWY5NjItNDE0ZS04OTMyLTU0MGZjMmE2OTYyNmZwZGRcIixcInVzZXJJZFwiOjB9IiwiaXNzIjoidXNlcmlkIiwiYXVkIjoid2ViIiwiZXhwIjoxNTI3NDk1MTE0LCJuYmYiOjE1Mjc0NzcxMTR9.kvVK4LazO827HmWiAdMCXknijpCN-xPifFYeJjq16rs",
		"sessionId": "a7d6d0aa-f962-414e-8932-540fc2a69626fpdd",
		"sessionKey": "coinfex_session_id",
		"needTwice": null,
		"uuid": null,
		"sso": false,
		"ssoUrl": null,
		"needEmail": false
	},
	"ts": 1527477114739,
	"err_msg": "成功"
}
```

## 登录二次验证

> POST /api/v2/inner/user/check

参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
username| 是 | string | 用户名 | 邮箱或者手机 | - | body
dubbleGoogleCode | 是 | string | 谷歌验证码 | - | - | body
uuid | 是 | string | 一次登录返回的uuid | - | - | body

### 返回值数据结构

```
ResponseMessage«用户登录后返回的基本信息» {
  code (integer, optional):状态码 ,
  data (用户登录后返回的基本信息, optional):数据 ,
  err_msg (string, optional):错误信息 ,
  ts (integer, optional):系统时间
}
用户登录后返回的基本信息 {
  needEmail (boolean, optional):是否要绑定邮箱 ,
  needTwice (boolean, optional):是否要二次登录 ,
  nickName (string, optional):昵称 ,
  sessionId (string, optional):sessionId ,
  sessionKey (string, optional):sessionKey ,
  sso (boolean, optional):是否是sso，true是sso ,
  ssoUrl (string, optional):sso url ,
  token (string, optional):token ,
  uuid (string, optional):二次登录uuid
} 
```

### 返回示例
```javascript
{
	"code": 0,
	"data": {
		"nickName": "***@f.com",
		"token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE1Mjc0Nzg4ODIsInN1YiI6IntcImNhY2hlS2V5XCI6XCJ1c2Vyc2Vzc2lvbmNhNmYxZWUyLTRlNTQtNDJmOS04ODAyLTgzYzc3ZTUyMWJmNmVyVWRcIixcInVzZXJJZFwiOjB9IiwiaXNzIjoidXNlcmlkIiwiYXVkIjoid2ViIiwiZXhwIjoxNTI3NDk2ODgyLCJuYmYiOjE1Mjc0Nzg4ODJ9.dqYWok8u1XG6cvq9PlYCqjmmMt9DjfYKNRi3dPNLPfs",
		"sessionId": "ca6f1ee2-4e54-42f9-8802-83c77e521bf6erUd",
		"sessionKey": "coinfex_session_id",
		"needTwice": null,
		"uuid": null,
		"sso": false,
		"ssoUrl": null,
		"needEmail": false
	},
	"ts": 1527478882453,
	"err_msg": "成功"
}

```

## 退出登录

>POST /api/v2/inner/user/logout

参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | jwt | - | - | header

### 返回值数据结构

```
ResponseMessage {
  code (integer, optional):状态码 ,
  data (object, optional):数据 ,
  err_msg (string, optional):错误信息 ,
  ts (integer, optional):系统时间
} 
```
### 返回示例
```javascript
{
	"code": 0,
	"data": {},
	"ts": 1527479211866,
	"err_msg": "成功"
}
```

## 登录页面初始化信息

> POST /api/v2/inner/user/login/pageInit

参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 否 | string | jwt | - | 判断用户登录状态要传 | header

### 返回值数据结构

```
ResponseMessage«登录界面初始化» {
  code (integer, optional):状态码 ,
  data (登录界面初始化, optional):数据 ,
  err_msg (string, optional):错误信息 ,
  ts (integer, optional):系统时间
}
登录界面初始化 {
  ali (boolean, optional):是否需要阿里验证 true需要 ,
  userlogin (boolean, optional):用户是否登录 true已登录
} 
```

### 返回示例
```javascript
{
	"code": 0,
	"data": {
		"userlogin": false,
		"ali": false
	},
	"ts": 1527487039934,
	"err_msg": "成功"
}
```


