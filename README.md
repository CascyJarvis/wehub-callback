微信最新版本下载:https://dldir1.qq.com/weixin/Windows/WeChatSetup.exe  
wehub最新版本下载:http://wxbs.oss-cn-hangzhou.aliyuncs.com/wetool/WeHubSetup0.2.0.exe  

目前wehub支持2.6.3.78|2.6.4.38|2.6.4.56 这三个版本的微信

------

wehub 回调接口开发文档: 

由于wehub自发布第一个版本至今,有多个版本的迭代,接口规范也在调整优化

若使用的wehub版本号<=0.1.6,接口规范文档为  
https://github.com/fangqing/wehub-callback/blob/master/wehub-api-doc-v1.md  
自0.2.0版本之后,使用新的协议,简化了旧版本协议中繁琐的ack_type,接口规范文档为  
https://github.com/fangqing/wehub-callback/blob/master/wehub-api-doc-v2.md

faq:在与第三方企业在对接过程中遇到的相关问题的记录(整理中)     
https://github.com/fangqing/wehub-callback/blob/master/faq.md	

------
对接的demo(php版) : https://github.com/tuibao/wehub-demo-php  
对接的demo(python版): https://github.com/fangqing/wehub_callback_server  

(demo仅展示数据的处理方式,不保证数据结构的完整性)

------
版本更新记录:  
2018.9.28:
发布wehub 0.2.0 
http://wxbs.oss-cn-hangzhou.aliyuncs.com/wetool/WeHubSetup0.2.0.exe

```
1.简化了ack中的协议
2."发消息任务"的任务类型数据结构有调整:  
调整前的数据结构为: 
{
    "task_type": 1,  
    "task_dict":
    {	
    	"room_wxid": "xxxxxx",  
    	"wxid":"xxxxxxx",	   				  
    	"msg_list":[$push_msgunit,$push_msgunit,....] 
	}
}

调整后的数据结构为
{
   "task_type": 1,  
   "task_dict":
    {	
        "wxid_to":"xxxxxx",  	
        "at_list":['xxxx','xxxx'],  
    	"msg_list":[$push_msgunit,$push_msgunit,....] 
	}
}

调整后发群消息时可以at多个微信号了(原来只能at一个微信号)
```


2018.9.21:
http://wxbs.oss-cn-hangzhou.aliyuncs.com/wetool/WeHubSetup0.1.6.exe

```
发布wehub 0.1.6版本
修复可能导致微信卡死的bug
```

2018.9.20
```
发布wehub 0.1.5版本
1.设置界面去掉了上传文件类型的复选框,wehub完全根据回调接口的"上传文件"的任务指令来上传文件(只要收到指令就上传,没收到指令就不上传,所以原来的复选框就完全没必要了)
2.相关bug修复,优化
3.在login和logout中增加client_version字段;report_friend_add_request中增加notice_word字段；
```

2018.9.18
```
发布wehub 0.1.4版本
1.新增"小程序,转账,发文件,个人名片,表情,语音,视频,微信系统消息"等消息事件的上报;
2.新增report_friend_add_request,report_new_room两个action;
3.新增发群公告,个人名片,删除好友,自动通过好友验证等4种新任务类型; 
4.新增视频文件上传(微信版本号必须>=2.6.4.56);相关数据结构有微调(格式向下兼容)
```

2018.8.31
```
1.新增文件上传功能:在wehub上可以配置上传的文件类型(只支持上传图片)
第三方需开发一个文件上传的接口并在wehub上进行配置,wehub_callback_server项目中有文件上传的示范代码  
https://github.com/fangqing/wehub_callback_server
   图片消息增加file_index 字段,该字段用来标识图片文件的索引值
2.groupinfo 结构增加member_wxid_list字段(这会导致report_contact 的包比较大)
3.群成员发生变化时增量上报 (action为report_room_member_change)
4.wehub和回调接口之间的http连接可设置http代理,方便调试
  在本机上开发和部署回调接口服务的开发者,需下载最新版wehub,打开设置界面,切换到"其他设置", 
  设置http代理为127.0.0.1:8888(保持和fiddler默认的代理设置一致),然后就可以在fiddler中查看wehub发送的http request
```

2018.8.22
```
pull task的定时轮询时间可在wehub上设置;上报链接消息;修正wehub多实例运行中的bug
```


