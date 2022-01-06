# Godot-AndroidTools
Godot TapTap 基础插件

最近做了一个Godot 安卓插件分享给大家，目前只做了一些小功能，如果需要拓展可以留言。

功能如下：

1.获取手机信息（sha1签名，包名，应用版本号，屏幕大小）

2.Toast（安卓系统自带提示）

3.打开网站（内置浏览器）

4.TapTap SDK

   TapSdk：使用TapTap登录、获取Tap登录状态、打开Tap内嵌游戏动态、Tap数据统计、Tap数据统计自定义事件

使用方法如下：

导入构建模板

[upl-image-preview url=https://godoter.cn/assets/files/2022-01-06/1641447607-529202-image.png]

添加文件到plugins目录下：

[upl-image-preview url=https://godoter.cn/assets/files/2022-01-06/1641447649-785628-image.png]

导出设置中勾选以下内容：

[upl-image-preview url=https://godoter.cn/assets/files/2022-01-06/1641447686-489526-image.png]

在代码中启用插件：

func _ready():
	if Engine.has_singleton("GodotUtils"):
		singleton = Engine.get_singleton("GodotUtils")
		singleton.connect("AndroidPhoneInfo",self,"_AndroidPhoneInfo")
		singleton.connect("OnTapLoginResult",self,"_OnTapLoginResult")
		singleton.connect("OnTapLoginAccessToken",self,"_OnTapLoginAccessToken")
		singleton.connect("OnTapMomentCallBack",self,"_OnTapMomentCallBack")

信号说明：

AndroidPhoneInfo 返回设备基础信息

OnTapLoginResult 调用Tap登录返回结果

OnTapLoginAccessToken 调用Tap 登录状态返回结果

OnTapMomentCallBack 当内嵌动态有提示时调用

方法说明：

获取设备基础信息

singleton.getMethods("getAndroidPhoneInfo")

提示框（参数0代表较短时间的提示框，1代表较长事件的提示框）：

singleton.showToast("这是一个来自Godot的提示",0) 

效果图：

[upl-image-preview url=https://godoter.cn/assets/files/2022-01-06/1641448006-25628-73cb08574c53f1b2348370485985532.jpg]

打开一个内置网页：

singleton.openWebView("https://godoter.cn")

效果图：

[upl-image-preview url=https://godoter.cn/assets/files/2022-01-06/1641448225-983191-95f0e7aadae141b3693a947cee24d23.jpg]

初始化TapTap SDK（需要自行去Tap开发者后台申请id与token）：

所有Tap相关操作都必须要在初始化之后再调用，初始化只需要一次就行

singleton.tapInit("client_id","client_token")

打开Tap登录界面：

singleton.getMethods("tapLogin")

效果图：

[upl-image-preview url=https://godoter.cn/assets/files/2022-01-06/1641449271-670667-e53ca1897c6a512f9d9b0f01e8235cf.jpg]

登录成功后返回登录信息：

[upl-image-preview url=https://godoter.cn/assets/files/2022-01-06/1641449288-434140-0a2874e5143b7a4efb2a73055e31ba6.jpg]

退出登录：

singleton.getMethods("tapLogin")

获取当前登录用户Token信息（必须是已经登录的情况下调用）：

singleton.getMethods("tapAccessToken")

效果图：

[upl-image-preview url=https://godoter.cn/assets/files/2022-01-06/1641449342-790941-85fe602ff9ae486682b23522aa2a3c9.jpg]

打开Tap内嵌动态：

singleton.getMethods("tapOpenMoment")

效果图：

[upl-image-preview url=https://godoter.cn/assets/files/2022-01-06/1641449373-699519-157545d4b8e162e163672a4d00ef2e7.jpg]

Tap统计发送自定义事件（参数一：事件名称，参数二：具体事件内容）：

singleton.tapTrackEvent("login",to_json({

		"user":"sakuya"

	}))

初始化SDK后自动启动Tap数据分析，数据分析可在开发者后台查看：

[upl-image-preview url=https://godoter.cn/assets/files/2022-01-06/1641449537-182885-image.png]
