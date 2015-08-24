

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


