# 阿里云盘API身份认证参考
由TES286抓取, 是web端的API

## 端点
Token端点为: https://websv.aliyundrive.com/
不检查referer和user-agent

## 参考
### 刷新Token
#### Request
`POST /token/refresh`

------------
`Content-Type: application/json`

------------
|key|type|
|---|---|
|refresh_token|string|

#### Response
以JSON格式返回
```json
{
    "default_sbox_drive_id": "4***7",   // 默认存储空间
    "role": "user",                    // 角色
    "device_id": "00........44",    // 设备ID, Api调用时需要
    "user_name": "1......9",    // 用户名
    "need_link": False,   // 是否需要跳转到绑定页面
    "expire_time": "2022-03-12T16:33:46Z",  // 过期时间
    "pin_setup": True,
    "need_rp_verify": False,
    "avatar": "https://ccp.....S2", // 头像URL
    "user_data":    // 用户信息, 用作展示
    {
        "DingDingRobotUrl": "https://oapi.d.......8687501916fec",
        "EncourageDesc": "内测期间有....费会员",
        "FeedBackSwitch": True,
        "FollowingDesc": "34...",
        "ding_ding_robot_url": "https://oapi.d....5485a916fec",
        "encourage_desc": "内测期间有....免费会员",
        "feed_back_switch": True,
        "following_desc": "34...",
        "share": "5f..........837ff6"
    },
    "token_type": "Bearer",  // token的类型, 只有Bearer
    "access_token": "eyJhbG........",  // token的值
    "default_drive_id": "4...6",  // 默认的网盘ID
    "domain_id": "bj29",    // 域名ID, 但是好像没有用
    "refresh_token": "d00690b......", // 刷新token的值
    "is_first_login": False,    // 是否是第一次登录
    "user_id": "8aa0b4def........", // 用户ID
    "nick_name": "TES286",  // 用户昵称
    "exist_link": [],
    "state": "",    // 状态
    "expires_in": 7200, // token的有效期(秒)
    "status": "enabled" // 状态
 }
````
