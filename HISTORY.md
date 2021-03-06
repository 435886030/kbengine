###v0.7.0

	2015/11/25

	新增与改善：
		邮件重置密码完善
		更新API文档
		抽象化interfaces，interfaces使用python进行扩展
		loginapp支持脚本了,可扩展脚本做类似登陆排队功能和控制账号的登陆等行为
		deregisterFileDescriptor改名为deregisterReadFileDescriptor
		proxy在destroy后及时通知客户端被服务器踢出
		支持让某个baseapp、cellapp不参与负载均衡（KBEngine.setAppFlags、KBEngine.getAppFlags）
		增加新的API：Entity.getRandomPoints用于随机获取目的坐标点周围navigate可到达的指定数量的坐标点（可用于NPC随机移动，掉落物品坐标计算等）。
		
	BUG修正：
		修正loginapp的http回调端口返回页面时乱码现象
		修正:一个entity属性设成BOOL（也就是UINT8），然后退出服务器，改成了INT8，重起服务器以后，数据表不会变bug(#263)
		修正在服务器上不存在某实体的时候，客户端请求实体方法可能造成crash
		防止APP在退出时有日志没有同步完（同步到logger）。



###v0.6.21

	2015/10/26

	新增与改善：
		将原有的CLIENYT_TYPE_PC拆分成CLIENYT_TYPE_WIN、CLIENYT_TYPE_LlINUX、CLIENYT_TYPE_MAC
		Entitydef的摘要检查不再与客户端类型绑定在一起，如果客户端提交了摘要则检查，没有提交则客户端对自己的协议正确性负责（如果客户端严格从服务器远程导入协议，理论上不会有问题）
		标准化一些协议名称



###v0.6.20

	2015/10/23

	新增与改善：
		增加新的API：Entity.addYawRotator
		更新API文档
		vs2010项目升级到vs2013
		实体容器类属性标脏机制(#259)
		addSpaceGeometryMapping参数调整可指定参数加载navmesh到某个layer下(#240)
		调整数据库查询接口，更好的支持不同形式的数据库扩展

	BUG修正：
		修正email激活邮件乱码问题
		修正指定FIXED_DICT类型存档字段不对的问题(#255)
		修正dbmgr多次与interfaces连接的问题
		修正moveToPoint的参数distance大于0时当实体距离目的地小于distance时实体会忘相反的地方行走



###v0.6.1

	2015/6/1

	新增与改善：
		数据库所有系统主键ID改为uint64类型
		增加服务端切换地图时回调onEnterSpace/onLeaveSpace
		当客户端请求获得服务端协议时，将属性flags也下发到客户端，用于属性类型的判断
		一些结构调整

	BUG修正：
		修正某种情况下实体销毁并未通知客户端销毁的问题
		修正某些情况下teleport后，客户端没有改变实体位置



###v0.6.0

	2015/5/3

	新增与改善：
		Websocket FRC6544协议通讯完善
		cluster_controller.py（集群控制）、installer.py（安装助手）工具完善
		assets默认不包含scripts/client目录，避免不必要的误会(移动到OGRE例子脚本目录中)
		更新API文档
		一些结构调整

	BUG修正：
		修正bots程序退出时crash问题
		修正在进程繁忙状态下有时不能很好的安全关服
		修正FixedDict引用未释放问题



###v0.5.0

	2015/4/18

	新增与改善：
		优化部分代码结构
		增加新的API（getClientDatas），用于在脚本中读取客户端登陆时所附带的数据
		增加API，getAoiRadius、getAoiHystArea
		统一向服务端同步方向的顺序是roll、pitch、yaw
		bots增加entryScriptFile配置 

	BUG修正：
		Cellapp上的Exposed方法，第一个参数得到的并非是调用者的ID
		修正BASE_AND_CLIENT类属性在客户端实体创建之后才同步过来
		修复客户端注册账号时上报的数据过长导致dbmgr出错的问题



###v0.4.20

	2015/3/13

	新增与改善：
		优化部分代码结构
		增加logger处理速度
		API文档更新

	BUG修正：
		修正windows下genUUID64可能不正确的问题
		修正bots在某些条件下导致日志缓存没有释放的问题



###v0.4.10

	2015/2/10

	新增与改善：

	    实体自动加载功能（用法见API手册，baseapp中writeToDB部分）
	    onBaseAppReady、onReadyForLogin回调函数参数调整，改为bool（是否为第一个启动的baseapp）
	    增加进程启动参数 --gus，详见：http://www.kbengine.org/cn/docs/startup_shutdown.html
	    删除进程启动参数--grouporder与--globalorder，该值由程序内部自动产生，通过环境变量在脚本中可以获得KBE_COMPONENTID、KBE_BOOTIDX_GLOBAL、KBE_BOOTIDX_GROUP
	    API文档完善

	BUG修正：

	    修正teleport后ghost消息错乱问题
	    修正teleport后pitch错误的问题



###v0.4.0

	2015/1/23

        新增与完善：

		网络模块优化（主要针对send以及一些结构方面）
		增加对TCP发送窗口的配置，以便对一些情况进行控制
		负载均衡模块调整（Cellapp在大量动态副本创建时能更好的均衡负载）
		消息跟踪模块调整
		
	BUG修正：
		
		修正EntityDef，可能在一些情况下def改变后MD5并未变化的问题
		修正Cellapp初始化时执行其他进程要求的任务产生的错误
		修正DBMgr如果宕了，interfaces与logger进程等自动关闭



###v0.3.0
	
	2014/12/30

	新增与完善：

	    完善API文档
	    GUIConsole增加log搜索与过滤等功能
	    完善cluster_controller了
	    完善了installer功能
	    billingsystem改名interfaces、kbmachine改名为machine、messagelog改名为logger
	    增加默认的项目资产目录"assets"，如果没有配置环境变量引擎将自动从根目录寻找该资产目录
	    原本的demo资产目录被迁移到独立的项目中，在具体的demo中使用git submodule获得
	    其他若干小完善

	BUG修正：

	    修正BASE_AND_CLIENT等类型被修改后没有同步到客户端的问题
	    修正CLIENT_TYPE_MOBILE类型要求判断entitydef的错误
	    修正实体跳转场景后ghost机制带来的消息错乱问题



###v0.2.15

	2014/12/6

	新增与改善：
	    脚本层字符串属性序列化到流优化， 可以减少一次内存拷贝
	    增强GUIConsole的探测功能
	    对部分代码结构进行调整

	BUG修正：
	    修正AOI极端情况下一些状态错乱的问题
	    globalorderid等应该使用int32类型目前int8， 这样会限制理论的进程数量
	    避免在目录下没有log4j.log时提示错误信息

