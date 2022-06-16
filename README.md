#解决iOS微信分享两次跳转APP的问题

##1，apple开发者配置：
Identifiers（标识符）
勾选上 Associated Domains

##2，APP配置：关联域 （Associated Domains）
	applinks:xx.yyy.zz

##3，apple-app-site-association文件

	文件路径：xx.yyy.zz/.well-known/apple-app-site-association

'''
{
    "applinks": {
        "apps": [],
        "details": [{
            "appID": "App ID Prefix.Bundle ID",
            "paths": ["/app/*"]
        }]
    }
}
'''

	/.well-known;/.well-known/apple-app-site-association;/app;/app/* 都需要可以被直接访问，不能返回30X，401，500状态。


##4，微信开放平台-》移动应用：iOS平台
	Universal Links：https://xx.yyy.zz/app/
	
##5，APP打包设置：
	iOS平台通用链接（Universal Links）
	https://xx.yyy.zz/app/
	
问题：如果3和4配置不相同，跳转微信或微信账号登陆时会提示 验证不通过；如果3和4配置相同，但是不是设置的是apple-app-site-association
文件里pahts里的路径，微信分享时会出现两次跳转现象。
	
##6，可在测试环境先测试，配置后不会立刻生效，需要等3,4小时或更长时间才生效。
