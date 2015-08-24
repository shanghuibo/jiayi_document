
#任务列表
## 国栋:
* 医生个人信息内无钱包信息 (接口去掉这个字段) - 完成
* 修改 - 医生详情添加个人擅长、个人荣誉字段 - 完成
* 修改 - 团队邀请时二维码生成规范（团队信息、邀请人信息） - 二维码内容确认 - 团队名称，团队id，邀请人 - 进行中
* 增值服务删除（单个删除、全部删除） - 标记删除 - 进行中
* 设置诊所下某个医生为主管，没有邀请人的主管医生默认为诊所创始人 - 完成
* 会员通过诊所名称查找诊所 - 名称全匹配, 显示诊所介绍 - 进行中
* 退出登录接口 - 进行中
* 登陆上传 token 接口
* 增值服务，病人端确认接口 - 完成



## 运来:
* 医生可创建团队最多可以创建或者加入5个 - 进行中
* 医生可以通过搜索团队名称 查找团队  - 完成
* 修改 -  个人信息返回：余额、已消费总数、怀孕次数、产几、月经周期、初潮年龄、家庭成员数组（relation_user_id、relation_type、name、photo_id）
* 拉取消费详细记录接口 - 完成

## 家庭相关接口 - 运来 - 完成
* 家庭成员创建、家庭成员信息修改、家庭成员信息删除等接口 - 完成
* 新增 - 家庭成员详情list， 返回一个人的所有家庭成员，以及返回指定成员


## 团队相关接口 - 运来
* 修改 - 团队管理下增加团队收入接口：可提现总数、提现历史、剩余会费   - 进行中
* 团队管理－－团队收入－－可提现总数接口：返回该阶段所有参与咨询的医生的咨询次数、医生添加增值服务金额数
每月 1-5 号是可提现日期，过期不能提（具体根据文档）
* 团队管理－－团队收入－－提现历史接口：返回不同月份提现记录列表
* 团队管理－－团队收入－－提现历史－－具体月份记录接口：返回该月份下所有参与咨询的医生的咨询次数、医生添加增值服务金额数
* 团队管理－－团队收入－－剩余会费接口：所有会员会费余额列表
* 段对创建：增加会员加入协议字段


## IM, 咨询相关接口 - 林瑞 - 进行中
* IM 获取 ip 地址 接口 - 完成
* IM 获取 Token 接口 - 完成
* 新增 - 团队咨询历史接口 返回：团队总所得、团队处理咨询总数、我所服务的次数、我的增值服务次数
团队收入 - 咨询历史  - 完成
* 新增 - 团队处理咨询过的列表接口 - 完成
* 新增 - 我（医生）在团队下处理的咨询列表接口 - 完成
* 新增 - 我在团队咨询下发出的增值服务列表 - VAS - 需要修改
* 咨询删除（单个删除、全部删除）
* 创建新咨询 接口 
* 添加咨询type、语音字段、图片数组、家庭成员id（如何区分为自己咨询？）
* 咨询创建时只有群助手和病人
* 拉取正在进行咨询接口
* 拉取历史咨询接口
* 咨询增值服务 
* 定义 mimetype 类型
* 拉取固定 咨询 的信息
* 私信聊天IM  林瑞
* 多方通话   





# 1.咨询相关接口
##1.1 获取 im server ip 地址

```
GET           /im/servers 

Headers:
X-AUTH-TOKEN: accesstoken

Parameters:

Results:
    {
    "success": true,
    "result":[
    {
    "ip": "192.168.3.1"
    "port": 9501
    },
    {
    "ip": "192.168.3.2"
    "port": 9501
    },
    {
    "ip": "192.168.3.1"
    "port": 9502
    }
    ]
    }
```



## 1.2 获取 im password 
 
```
GET           /im/password 

> Blockquote

Headers:
X-AUTH-TOKEN: accesstoken

Parameters:

Results:
{
"success":true,
"result":
	{"expire":3600,
	"password":"3dd734329f5abcdf7dde9ba87301bb1f"
	}
}

```

## 1.3 创建新咨询接口
```
POST  /consult  

Header:
Content-Type application/json.
X-AUTH-TOKEN Users unique access-key.

Param:
{
	"creator_member_id": 1234,
	"target_member_id": 1234,
	"team_id":1234.
	"symptom_content": "文字或者语音的 uri",
	"symptom_type": "资料类型，文字或者图片，与 im 中消息类型保持一致",
	"images": ["image_uri", "image_uri", .....],
}


Results success::
{
"success":true,
"code":200,
"result":
	{
	 "status": 
	"consultation_id": 12334,
	"creator_member_id": 1234,
	"creator_member_name": "abld",
	"target_member_id":1234,
	"target_member_name": "asdf",
        "team_id":1234,
        "team_name": "asdf",
        "doctor_ids": [1234,1234,1234,1234,],
        "symptom_content": "文字或者语音的 uri",
	"symptom_type": "资料类型，文字或者图片，与 im 中消息类型保持一致",
	"images": ["image_uri", "image_uri", .....],
	},
	"created": 创建的毫秒时间
}

Results fail:
{
"success":false,
"code":500,
"message": "asdfasdgf"
}

```

## 1.4 获取指定咨询的信息

```
GET /consult/:id

Header:
Content-Type application/json.
X-AUTH-TOKEN Users unique access-key.


Results success:
Results success::
{
"success":true,
"code":200,
"result":
	{
	  "status": 
	"consultation_id": 12334,
	"creator_member_id": 1234,
	"creator_member_name": "abld",
	"target_member_id":1234,
	"target_member_name": "asdf",
        "team_id":1234,
        "team_name": "asdf",
        "doctor_ids": [1234,1234,1234,1234,],
        "symptom_content": "文字或者语音的 uri",
	"symptom_type": "资料类型，文字或者图片，与 im 中消息类型保持一致",
	"images": ["image_uri", "image_uri", .....],
	}
	"created": 创建的毫秒时间
}


Results fail:
{
"success":false,
"code":500,
"message": "asdfasdgf"
}
```

## 1.5 获取进行中的咨询列表
```
GET  /consult/in_process_list

Header:
Content-Type application/json.
X-AUTH-TOKEN Users unique access-key.


Results succee:
{
"success":true,
"code":200,
resutls:
	[
	  {
		  "status": 
		"consultation_id": 12334,
		"creator_member_id": 1234,
		"creator_member_name": "abld",
		"target_member_id":1234,
		"target_member_name": "asdf",
	        "team_id":1234,
	        "team_name": "asdf",
	        "doctor_ids": [1234,1234,1234,1234,],
	        "symptom_content": "文字或者语音的 uri",
		"symptom_type": "资料类型，文字或者图片，与 im 中消息类型保持一致",
		"images": ["image_uri", "image_uri", .....],
		"created": 创建的毫秒时间
	},
	{
		"status": 
		"consultation_id": 12334,
		"creator_member_id": 1234,
		"creator_member_name": "abld",
		"target_member_id":1234,
		"target_member_name": "asdf",
	        "team_id":1234,
	        "team_name": "asdf",
	        "doctor_ids": [1234,1234,1234,1234,],
	        "symptom_content": "文字或者语音的 uri",
		"symptom_type": "资料类型，文字或者图片，与 im 中消息类型保持一致",
		"images": ["image_uri", "image_uri", .....],
		"created": 创建的毫秒时间
	}
	]
}



Results fail:
{
"success":false,
"code":500,
"message": "asdfasdgf"
}
```

## 1.6 获取历史咨询

```
Results succee:
{
"success":true,
"code":200,
resutls:
	[
	  {
		"status": 
		"consultation_id": 12334,
		"creator_member_id": 1234,
		"creator_member_name": "abld",
		"target_member_id":1234,
		"target_member_name": "asdf",
	        "team_id":1234,
	        "team_name": "asdf",
	        "doctor_ids": [1234,1234,1234,1234,],
	        "symptom_content": "文字或者语音的 uri",
		"symptom_type": "资料类型，文字或者图片，与 im 中消息类型保持一致",
		"images": ["image_uri", "image_uri", .....],
		"created": 创建的毫秒时间
	},
	{
		"status": 
		"consultation_id": 12334,
		"creator_member_id": 1234,
		"creator_member_name": "abld",
		"target_member_id":1234,
		"target_member_name": "asdf",
	        "team_id":1234,
	        "team_name": "asdf",
	        "doctor_ids": [1234,1234,1234,1234,],
	        "symptom_content": "文字或者语音的 uri",
		"symptom_type": "资料类型，文字或者图片，与 im 中消息类型保持一致",
		"images": ["image_uri", "image_uri", .....],
		"created": 创建的毫秒时间
	}
	]
}
```


## 1.7 删除历史咨询
```
DELETE  /consult/history_list/:id

Header:
Content-Type application/json.
X-AUTH-TOKEN Users unique access-key.

Results success:
{
  "sucess":true,
  "code": 200
}


Results fail:
{
"success":false,
"code":500,
"message": "asdfasdgf"
}

```












#2. 个人资料相关接口
##2.1 医生添加个人详情接口，增加"个人擅长、个人荣誉"字段


