# GET /api/v2/inner/user/inviteInfo
### 邀请页信息(邀请人数， 今日返佣，当月返佣，所有返佣，邀请模板图片url
，邀请链接)
### 请求参数：
```bash
headerToken 令牌 string
```
#### 响应示例
`
{
  "code": 0,
  "data": {
    "num": 7,
    "today": "0.000586032772500000000000000000000000",
    "month": "0.000586032772500000000000000000000000",
    "total": "0.064269741064984470907500000000000000",
    "invite": "http://test.coinfex.com/account/doRegisterPhone?utmSource=F29201022DD578A2193",
    "model": [
      "https://rocktest012358.oss-cn-shanghai.aliyuncs.com/20180702_Ri8JMsGpkh.jpg?Expires=1845891438&OSSAccessKeyId=LTAIruvMOcZei5rE&Signature=BFa2gGElS%2FmQhNzp60voEZgWbq0%3D"
    ]
  },
  "ts": 1530697842187,
  "err_msg": "成功"
}
`
# GET /api/v2/inner/user/inviteRecord
## 邀请记录（邀请人，返佣金额， 注册时间 ，交易时间）
### 请求参数
```bash
headerToken 令牌 string
from 起始查询条数
to 查询到第几条，如查1-20 条 from=1 to=20 查询21到40条 from=21 to=40；
```
#### 响应示例
`
{
  "code": 0,
  "data": [
    {
      "nickName": "13*****2236",
      "feeBack": "0.000347399262754417125000000000000000",
      "registerDate": 1529649674000,
      "lastTradeDate": 1530696710000
    },
    {
      "nickName": "13*****2145",
      "feeBack": "0.008164666466250000000000000000000000",
      "registerDate": 1529649953000,
      "lastTradeDate": 1530696708000
    },
    {
      "nickName": "137****0062",
      "feeBack": "",
      "registerDate": 1525835350000,
      "lastTradeDate": 0
    },
    {
      "nickName": "13*****5565",
      "feeBack": "0.055757675335980053782500000000000000",
      "registerDate": 1530177922000,
      "lastTradeDate": 1530254520000
    },
    {
      "nickName": "102***@qq.com",
      "feeBack": "",
      "registerDate": 1529639892000,
      "lastTradeDate": 0
    },
    {
      "nickName": "102***@qq.com",
      "feeBack": "",
      "registerDate": 1529649524000,
      "lastTradeDate": 0
    },
    {
      "nickName": "15*****4621",
      "feeBack": "",
      "registerDate": 1529639482000,
      "lastTradeDate": 0
    }
  ],
  "ts": 1530697902798,
  "err_msg": "成功"
}
`

