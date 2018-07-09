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

```
### 返回示例
```javascript

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

```
### 返回示例
```javascript

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

```
### 返回示例
```javascript

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

```
### 返回示例
```javascript

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

```
### 返回示例
```javascript

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

```
### 返回示例
```javascript

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

```
### 返回示例
```javascript

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

```
### 返回示例
```javascript

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

```
### 返回示例
```javascript

```

# 资产中心


----------


## 账户资产信息
> GET /api/v2/inner/finance
### 入参信息
参数  |  必须  | 类型  | 描述  | 取值范围  | 特别说明或默认值|位置
--- | --- | --- | --- | --- | --- | ---
headerToken | 是 | string | 用户登录token | - | - | body
### 返回数据
```javascript

```
### 返回示例
```javascript

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

```
### 返回示例
```javascript

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

```
### 返回示例
```javascript

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

```
### 返回示例
```javascript

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

```
### 返回示例
```javascript

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

```
### 返回示例
```javascript

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

```
### 返回示例
```javascript

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

```
### 返回示例
```javascript

```

