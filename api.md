# 阿里云盘API参考
由TES286抓取, 是web端的API

## 端点
目前是: https://api.aliyundrive.com/v2/
不会验证referer和user-agent

## 身份认证
见[身份认证](auth.md)

获取到access_token后, 可以使用access_token来访问阿里云盘API.
refresh_token可以用来刷新access_token

目前Token的格式是Bearer + access_token, 并添加到Authorization头中.

## 参考
### 获取文件元数据
#### Request
`POST /file/get`

------------
`Content-Type: application/json`

------------
|key|type|description|example|
|---|---|---|---|
|drive_id|string|网盘ID|4...6|
|file_id|string|文件ID(对于根目录使用root)|root|

#### Response
以JSON格式返回
```json
{
    "drive_id":"4...6", // 网盘ID
    "domain_id":"bj29", // 域名ID, 但是好像没有用
    "file_id":"root",   // 文件ID
    "name":"Default",   // 文件名
    "type":"folder",    // 文件类型, folder, file
    "status":"available", // 文件状态
    "revision_id":""
}
```

### 获取文件列表
#### Request
`POST /file/list`

------------
`Content-Type: application/json`

------------
|key|type|description|example|
|---|---|---|---|
|drive_id|string|网盘ID|40636
|parent_file_id|string|文件ID|60f...
|limit|int|最大文件数量|100
|all|boolean|返回全部(优先被limit控制)|False
|url_expire_sec|int|下载链接最大有效期(秒)|1600
|image_thumbnail_process|string|略缩图选项|image/resize,w_400/format,jpeg
|image_url_process|string|图像选项|image/resize,w_1920/format,jpeg
|video_thumbnail_process|string|视频略缩图选项|video/snapshot,t_1000,f_jpg,ar_auto,w_300
|fields|string|字段(过滤用的???)|*
|order_by|string|排列顺序|updated_at
|order_direction|string|排列方向|DESC

#### Response
以JSON格式返回
```json
{
    "items":[
        {
            "drive_id":"40636", // 网盘ID
            "domain_id":"bj29", // 域名ID, 但是好像没有用
            "file_id":"60f56...",   // 文件ID
            "name":"文件夹",    // 文件名
            "type":"folder",    // 文件类型, folder, file
            "created_at":"2021-07-19T11:45:36.127Z",    // 创建时间
            "updated_at":"2021-07-19T11:45:36.127Z",    // 更新时间
            "hidden":false,   // 是否隐藏
            "starred":false,    // 是否加星
            "status":"available",   // 文件状态
            "parent_file_id":"60f56...",    // 父文件ID
            "encrypt_mode":"none",  // 加密模式
            "revision_id":""    // 修订ID
        },
        {
            "drive_id":"40636", // 网盘ID
            "domain_id":"bj29", // 域名ID, 但是好像没有用
            "file_id":"60f565e.....",   // 文件ID
            "name":"电影.mkv",  // 文件名
            "type":"file",  // 文件类型, folder, file
            "created_at":"2021-07-19T11:45:38.172Z",    // 创建时间
            "updated_at":"2021-07-19T14:25:04.463Z",    // 更新时间
            "file_extension":"mkv", // 文件扩展名
            "mime_type":"video/x-matroska", // 文件MIME类型
            "mime_extension":"mkv", // 文件MIME扩展名
            "hidden":false,  // 是否隐藏
            "size":1981928081,  // 文件大小(字节)
            "starred":false,    // 是否加星
            "status":"available",   // 文件状态
            "parent_file_id":"60...",   // 父文件ID
            "content_hash":"DA54136......", // 文件内容哈希
            "content_hash_name":"sha1", // 文件内容哈希算法
            "category":"video", // 文件类别
            "encrypt_mode":"none",  // 加密模式
            "video_media_metadata": // 视频媒体元数据
            {
                "video_media_video_stream":[],  // 视频流
                "video_media_audio_stream":[]   // 音频流
            },
            "punish_flag":0,    // 是否被禁止下载
            "revision_id":""    // 修订ID
        }
    ],
    "next_marker":"",   // 下一页标记(在limit > 文件数量时有效)
    "punished_file_count":0  // 被禁止下载的文件数量
}