### 注册机器人 WebHook

#### 接口说明

```
/机器人token/setWebhook

例子 
https://api.telegram.org/bot6743114088:AAEfHLRhVHPm2fJ_5Gst1gem6VcCEAy58q8/setWebhook
```

提交方式： POST

提交格式： FORM表单

#### 属性定义

| **属性定义**   | **说明**         | **是否必选**   | **数据类型** | **备注**                                                                                             |
|:-----------| :--------------- | :----------- | :----------- | :--------------------------------------------------------------------------------------------------- |
| url   | 回调域名  HTTPS URL, 使用空字符串删除Webhook | 是           | String          |                     |

##### 请求示例
```
{
    "url": "https://www.callback.com"
}
```

##### 返回示例
```
{
    "ok": true,
    "result": true,
    "description": "Webhook is already set"
}
```

### 1. 发送文本消息

#### 1.1.1 接口说明

接口名称

```
sendMessage
```
提交方式： POST


##### 1.1.2 属性定义

| **属性定义**   | **说明**         | **是否必选**   | **数据类型** | **备注**                                                                                             |
|:-----------| :--------------- | :----------- | :----------- | :--------------------------------------------------------------------------------------------------- |
| chat_id   | 群ID  | 是           | Integer or String          |                     |
| text   | 消息内容  | 是           | String          |                     |
| reply_to_message_id   | 回复消息ID  | 否           | String          |                     |
| reply_markup   | 内联键盘、自定义回复键盘的说明的 JSON 序列化对象  | 否           | InlineKeyboardMarkup or ReplyKeyboardMarkup  |              |

**InlineKeyboardMarkup**

| **属性定义**   | **说明**         | **是否必选**   | **数据类型** | **备注**                                                                                             |
|:-----------| :--------------- | :----------- | :----------- | :--------------------------------------------------------------------------------------------------- |
| inline_keyboard   | 按钮行的数组,每个由的数组表示 InlineKeyboardButton 对象（跟随在文字下面的按钮）  | 是           |  List<List < InlineKeyboardButton >>           | |


**InlineKeyboardButton**

| **属性定义**   | **说明**         | **是否必选**   | **数据类型** | **备注**                                                                                             |
|:-----------| :--------------- | :----------- | :----------- | :--------------------------------------------------------------------------------------------------- |
| text   | 按钮显示文字  | 是           |  String        | |
| url   | 按下按钮时将打开HTTP或tg:// URL。链接 tg://user?id=<user_id> 如果用户的隐私设置允许,则无需使用用户名即可通过其标识符提及用户  | 否           |  String        | |
| callback_data   | 数据以 回调查询 按下按钮时调用回调接口将这个数据传回来  | 否           |  String        | |




**ReplyKeyboardMarkup**


| **属性定义**   | **说明**         | **是否必选**   | **数据类型** | **备注**                                                                                             |
|:-----------| :--------------- | :----------- | :----------- | :--------------------------------------------------------------------------------------------------- |
| keyboard   | 按钮行的数组,每个由的数组表示 KeyboardButton 对象（输入框下面的键盘） | 是           |  List<List < KeyboardButton >>            | |

**KeyboardButton**

| **属性定义**   | **说明**         | **是否必选**   | **数据类型** | **备注**                                                                                             |
|:-----------| :--------------- | :----------- | :----------- | :--------------------------------------------------------------------------------------------------- |
| text   | 按钮显示文字 如果未使用任何可选字段,则在按下按钮时它将作为消息发送  | 是           |  String        | |



##### 1.1.3 发送文本消息

```json
当发送群消息给机器人时 返回消息
{
    "ok": true,
    "error_code": 0,
    "description": "",
    "result": {
        "date": 1720763615,
        "newChatMembers": [],
        "messageId": 100,
        "chat": {
            "type": "private",
            "userName": "96",
            "firstName": "fit",
            "id": 7064472996
        },
        "from": {
            "isBot": false,
            "userName": "96",
            "languageCode": "zh-hans",
            "firstName": "fit",
            "id": 7064472996
        },
        "text": "文本消息"
    }
}

当发送群消息时 返回消息
{
    "ok": true,
    "error_code": 0,
    "description": "",
    "result": {
        "date": 1720763831,
        "newChatMembers": [],
        "messageId": 192,
        "chat": {
            "type": "group",
            "title": "群名称",
            "allMembersAreAdministrators": true,
            "id": -4224766529
        },
        "from": {
            "isBot": false,
            "userName": "96",
            "firstName": "fit",
            "id": 7064472996
        },
        "text": "123"
    }
}

```


##### 1.1.4 发送图片消息

##### 1.1.5 发送群消息

```
{
    "chat_id": "7064472996",
    "text": "你好啊",
    "reply_to_message_id": "77299665", // 回复消息ID
    "method": "sendmessage" 
}
```

##### 1.1.6 发送私聊消息

```

```

##### 1.1.7 发送群消息包含 InlineKeyboardMarkup
```
{
    "chat_id": "7064472996",
    "text": "文本消息",
    "reply_markup": {
        "inline_keyboard": [
            [
                {
                    "text": "获取用户名",
                    "callback_data": "user_menu_1"
                },
                {
                    "text": "修改用户名",
                    "callback_data": "user_menu_2"
                }
            ],
            [
                {
                    "text": "修改密码",
                    "callback_data": "user_menu_3"
                },
                {
                    "text": "App下载",
                    "url": "http://www.baidu.com"
                }
            ]
        ]
    },
    "method": "sendmessage"
}
```

##### 1.1.8 发送私聊消息包含 ReplyKeyboardMarkup
```
{
    "chat_id": "7064472996",
    "text": "您好，欢迎使用游戏助手,游戏助手提供如下功能：\n<b>     修改账号/修改密码",
    "reply_markup": {
        "keyboard": [
            [
                {
                    "text": "📝修改用户名"
                },
                {
                    "text": "🔐修改密码"
                }
            ],
            [
                {
                    "text": "🏧绑定支付账号"
                },
                {
                    "text": "⬇App下载地址"
                }
            ]
        ],
    },
    "method": "sendmessage"
}
```

### 2. 系统回调

#### 2.1 管理员邀请人进群

```
{
    "ok": true,
    "error_code": 0,
    "description": "",
    "result": {
         "date": 1720764296, // 进群时间
         "newChatMembers": [  // 进群人数组
             {
                 "isBot": false,  // 是否是机器人
                 "lastName": "mse",  // 用户名
                 "firstName": "mse", // 用户姓
                 "id": 6358829188  // 用户ID
             }
         ],
         "messageId": 197, // 消息ID
         "chat": {
             "type": "group",   // 聊天类型 (group 群, private: 私聊 )
             "title": "群名称",  // 群名称
             "allMembersAreAdministrators": true,  //
             "id": -4224766529   // 群id
         },
         "from": {
             "isBot": false, // 是否是机器人
             "userName": "96", // 用户名
             "firstName": "fit", // 用户姓
             "id": 7064472996 // 用户ID
         }
     }
}
```

#### 2.2 管理员踢出用户

```
{
    "ok": true,
    "error_code": 0,
    "description": "",
    "result": {
         "date": 1720764408, // 退群时间
         "newChatMembers": [],
         "leftChatMember": {  // 离开群用户数组
               "isBot": false,  // 是否是机器人
               "lastName": "mse",  // 用户名
               "firstName": "mse", // 用户姓
               "id": 6358829188  // 用户ID
         },
         "messageId": 198, // 消息ID
         "chat": {
             "type": "group",   // 聊天类型 (group 群, private: 私聊 )
             "title": "群名称",  // 群名称
             "allMembersAreAdministrators": true,  //
             "id": -4224766529   // 群id
         },
        "from": {
             "isBot": false, // 是否是机器人
             "userName": "96", // 用户名
             "firstName": "fit", // 用户姓
             "id": 7064472996 // 用户ID
         }
     }
}
```


#### 2.3 用户主动进群
!> `用户主动加群/退群与 邀请进出群区别 :` **from字段**   一个是  **邀请人**   一个是  **自己**；

```
{
    "ok": true,
    "error_code": 0,
    "description": "",
    "result": {
         "date": 1720764602,
         "newChatMembers": [
             {
                 "isBot": false,
                 "lastName": "mse",
                 "firstName": "..",
                 "id": 6358829188
             }
         ],
         "messageId": 199,
         "chat": {
             "type": "group",
             "title": "群名称",
             "allMembersAreAdministrators": true,
             "id": -4224766529
         },
         "from": {
             "isBot": false,
             "lastName": "mse",
             "firstName": "..",
             "id": 6358829188
         }
     }
}
```

#### 2.4 用户主动退群

!> `用户主动加群/退群与 邀请进出群区别 :` **from字段**   一个是  **邀请人**   一个是  **自己**；

```
{
    "ok": true,
    "error_code": 0,
    "description": "",
    "result": {
         "date": 1720764638,
         "newChatMembers": [],
         "leftChatMember": {
             "isBot": false,
             "lastName": "mse",
             "firstName": "..",
             "id": 6358829188
         },
         "messageId": 203,
         "chat": {
             "type": "group",
             "title": "群名称",
             "allMembersAreAdministrators": true,
             "id": -4224766529
         },
         "from": {
             "isBot": false,
             "lastName": "mse",
             "firstName": "..",
             "id": 6358829188
         }
     }
}
```


#### 2.5 用户发送群消息回调


```
{
    "ok": true,
    "error_code": 0,
    "description": "",
    "result": {
         "date": 1720764629,
         "newChatMembers": [],
         "messageId": 202,
         "chat": {
             "type": "group",
             "title": "群名称",
             "allMembersAreAdministrators": true,
             "id": -4224766529
         },
         "from": {
             "isBot": false,
             "lastName": "mes",
             "firstName": "..",
             "id": 6358829188
         },
         "text": "发送了一个文本消息"
     }
}
```