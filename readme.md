#功能支持
##1.用户操作
- 微信用户首次浏览创建用户资料，篱笆币+10，每日首次登陆篱笆币+1
- 用户认证：用户填写用户信息完成认证 
  - 类型分类：1, '高校学生' 2, '北京大学' 3, '清华大学' 4, '社会人' 5, '未认证
  - 认证操作：
  	在校学生:邮箱、学生证、校园卡、录取通知书截图
	毕业校友：毕业证、学位证截图
	社会人士：手机号
- 用户权限：
 - 已认证：
 	浏览任务列表、话题列表、活动列表；
	按照关键字搜索任务列表、话题列表、活动列表；
	浏览任务内容、话题内容、活动内容，查看相关信息；
	发布任务、话题、活动
	任务、话题、活动报名、点赞、留言、分享
	本人发布任务、话题、活动查看、删除
	获取最新评论
	编辑个人资料
	匿名评论
	清北校园帮忙
	兴趣交友
	校园活动
 - 未认证：
 	浏览任务列表、话题列表、活动列表；
	按照关键字搜索任务列表、话题列表、活动列表；
	浏览任务内容、话题内容、活动内容，查看相关信息；
	发布任务，每次发表篱笆币-2.篱笆币>0可以发布
	任务、话题、活动报名、点赞、留言、分享
	本人发布任务查看、删除
	获取最新评论
	编辑个人资料
- 任务
	- 任务类型：找人帮忙、二手交易、职业资源 、交友情感、其他任务
	- 标题、描述、图片、有效期、任务赏金
	- 联系方式：微信号、手机、email
- 话题
	- 话题内容
	- 图片
	- 语音
	- 匿名发布
- 活动
	- 活动标题
	- 活动日期、开始时间、结束时间、活动地点
	- 活动描述
	- 活动图片
	- 联系方式：微信号、手机、email
- 篱笆币
	- 首次关注小程序的用户，自动获得10枚“篱笆币”
	- 每日登陆的用户，可以获得1枚“篱笆币”
	- 通过认证的用户每次发布消息(任务/话题/活动)可获得“2枚篱笆币”，分享转发消息(任务/话题/活动)至其他好友、微信群，奖励1枚“篱笆币”
	- 完成用户认证的用户，赠送10枚“篱笆币”
	- 未认证的用户，只能发布任务, 每次发布消耗2枚“篱笆币”
##2.管理员操作
- User管理
- MissionReward管理
- Activity管理
- Topic管理
##3.微信公众号相关
- 每日定时推送模板
	每天21:00向认证用户推送‘服务状态通知’ 模板，向非认证用户推送模板信息"用户认证状态提醒" 模板
	每天9：00向非认证用户推送模板信息"用户认证状态提醒" 模板
- 公众号菜单设置
- 公众号消息
	处理订阅、文本、其他消息
#后端接口
- required(func)
- OauthToken(request)
- get_list(request, obj)
- item_op(request, obj, obj_id)
- create_item(request, obj)
- profile(request)
- get_qiniu_token(request)
- get_news(request)
- invite_code(request)
- cert(request, cert_type)
- get_my_pub(request)
- get_my_favor(request)
- get_topic_rank(request)
- get_participants(request, id)
- get_favor_user(request, id)
- send_id_code(request)
- verify_id_code(request)
- verify_wx_push(request)
- post_formId(request)
- wxpa_menu_config(request)
- wxpa_reply(request):
#数据库列表
## User
                id, AutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')),
                nickName, CharField(blank=True, max_length=40, verbose_name='昵称')),
                gender, PositiveSmallIntegerField(choices=[(1, '男'), (2, '女')], default=1, verbose_name='性别')),
                avatarUrl, URLField(default='', verbose_name='头像')),
                authType, PositiveIntegerField(choices=[(1, '高校学生'), (2, '北京大学'), (3, '清华大学'), (4, '社会人'), (5, '未认证')], default=5, verbose_name='认证类型')),
                certImgUrl1, URLField(blank=True, null=True, verbose_name='认证图片一URL')),
                certImgUrl2, URLField(blank=True, null=True, verbose_name='认证图片二URL')),
                certImgUrl3, URLField(blank=True, null=True, verbose_name='认证图片三URL')),
                identifyState, PositiveIntegerField(choices=[(1, '未认证'), (2, '认证中'), (3, '已认证')], default=1, verbose_name='认证状态')),
                openId, CharField(default='', max_length=40, verbose_name='微信openID')),
                onlineTime, DateTimeField(auto_now_add=True, verbose_name='在线时间')),
                lastView, DateTimeField(auto_now_add=True, verbose_name='上次查看消息时间')),
                inviteCode, CharField(blank=True, max_length=50, verbose_name='邀请码')),
                realName, CharField(blank=True, max_length=20, verbose_name='真实姓名')),
                school, CharField(blank=True, max_length=40, verbose_name='学校名称')),
                admissionYear, CharField(blank=True, max_length=20, verbose_name='入学年份')),
                birthDay, CharField(blank=True, max_length=40, verbose_name='生日')),
                education, PositiveIntegerField(choices=[(1, '本科'), (2, '硕士'), (3, '博士'), (4, '专科'), (5, '其他')], default=5, verbose_name='目前学历')),
                signature, CharField(blank=True, max_length=100, verbose_name='个性签名')),
                cert_type, PositiveIntegerField(choices=[(1, '在校学生'), (2, '毕业校友'), (3, '社会人士')], default=1, verbose_name='认证类型')),
                location, CharField(blank=True, max_length=100, verbose_name='现居住地')),
                hometown, CharField(blank=True, max_length=100, verbose_name='家乡')),
                occupation, CharField(blank=True, max_length=30, verbose_name='职业')),
                state, PositiveIntegerField(choices=[(1, '单身'), (2, '有对象'), (3, '已婚'), (4, '离异')], default=1, verbose_name='情感状态')),
                id_code, CharField(blank=True, max_length=10, null=True, verbose_name='手机验证码')),
                liba_credit, PositiveIntegerField(default=10, verbose_name='篱笆积分')),
                mobile, CharField(blank=True, max_length=15, null=True, verbose_name='手机号')),
                session_key, CharField(max_length=24, null=True, verbose_name='session_key')),
                last_tmpl_push, DateTimeField(null=True, verbose_name='上一次推送时间')),

## MissionReward
                id, AutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')),
                mission_type, PositiveIntegerField(choices=[(0, '全部'), (1, '找人帮忙'), (2, '二手交易'), (3, '职业资源'), (4, '交友情感'), (5, '其他')], verbose_name='任务类型')),
                title, CharField(max_length=50, verbose_name='任务标题')),
                content, TextField(null=True, verbose_name='任务内容')),
                imgs, CharField(blank=True, max_length=2048, verbose_name='活动图片')),
                create_at, DateTimeField(auto_now_add=True, verbose_name='任务创建时间')),
                money, PositiveIntegerField(default=0, verbose_name='金钱悬赏')),
                reward, CharField(blank=True, max_length=50, verbose_name='其他悬赏')),
                views, PositiveIntegerField(default=0, verbose_name='被查看数')),
                shares, PositiveIntegerField(default=0, verbose_name='被分享数')),
                is_active, BooleanField(default=True, verbose_name='是否上线')),
                contact_type, PositiveIntegerField(choices=[(0, '微信'), (1, '电话'), (2, '邮箱'), (3, 'QQ')], default='wx', verbose_name='联系渠道')),
                contact, CharField(max_length=200, null=True, verbose_name='联系方式')),
                contact_views, PositiveIntegerField(default=0, verbose_name='联系方式点击量')),
                priority, PositiveIntegerField(default=0, verbose_name='优先级')),
                longitude, FloatField(blank=True, null=True, verbose_name='经度')),
                latitude, FloatField(blank=True, null=True, verbose_name='纬度')),
                campus, CharField(default='qing_bei_help', max_length=50, verbose_name='学校名')),
                likes, PositiveIntegerField(default=0, verbose_name='点赞数')),
                resolved, BooleanField(default=False, verbose_name='是否已解决')),
                anonymous, BooleanField(default=False, verbose_name='是否匿名')),
                expiry, DateTimeField(default=datetime.datetime(2021, 8, 7, 18, 52, 15, 850398), verbose_name='有效期限')),
                wxa_code, URLField(default='', verbose_name='小程序码图片URL')),

## Topic
                id, AutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')),
                content, TextField(blank=True, null=True, verbose_name='内容')),
                create_at, DateTimeField(auto_now_add=True, verbose_name='话题创建时间')),
                imgs, CharField(blank=True, max_length=2048, verbose_name='活动图片')),
                wave, URLField(blank=True, default='', verbose_name='声音文件地址')),
                shares, PositiveIntegerField(default=0, verbose_name='分享数')),
                views, PositiveIntegerField(default=0, verbose_name='查看数')),
                campus, CharField(default='qing_bei_help', max_length=40, verbose_name='学校')),
                is_active, BooleanField(default=True, verbose_name='是否显示')),
                priority, PositiveIntegerField(default=0, verbose_name='优先级')),
                likes, PositiveIntegerField(default=0, verbose_name='点赞数')),
                anonymous, BooleanField(default=False, verbose_name='是否匿名')),
                wxa_code, URLField(default='', verbose_name='小程序码图片URL')),
## Activity
                id, AutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')),
                title, CharField(max_length=50, verbose_name='活动标题')),
                start_time, CharField(blank=True, max_length=50, verbose_name='活动开始时间')),
                end_time, CharField(blank=True, max_length=50, verbose_name='活动结束时间')),
                activity_place, CharField(blank=True, default='在那遥远的地方', max_length=50, verbose_name='活动地点')),
                content, TextField(blank=True, null=True, verbose_name='活动内容')),
                imgs, CharField(blank=True, max_length=2048, verbose_name='活动图片')),
                views, PositiveIntegerField(default=0, verbose_name='活动查看数')),
                shares, PositiveIntegerField(default=0, verbose_name='活动分享数')),
                create_at, DateTimeField(auto_now_add=True, verbose_name='创建时间')),
                is_active, BooleanField(default=True, verbose_name='是否显示')),
                priority, PositiveIntegerField(default=0, verbose_name='优先级')),
                campus, CharField(default='qing_bei_help', max_length=50, verbose_name='学校名')),
                contact, CharField(blank=True, max_length=50, verbose_name='联系方式')),
                contact_type, PositiveIntegerField(choices=[(0, '微信'), (1, '电话'), (2, '邮箱'), (3, 'QQ')], default='wx', verbose_name='联系渠道')),
                contact_views, PositiveIntegerField(default=0, verbose_name='联系方式点击量')),
                longitude, FloatField(blank=True, null=True, verbose_name='经度')),
                latitude, FloatField(blank=True, null=True, verbose_name='纬度')),
                likes, PositiveIntegerField(default=0, verbose_name='点赞数')),
                anonymous, BooleanField(default=False, verbose_name='是否匿名')),
                wxa_code, URLField(default='', verbose_name='小程序码图片URL')),
## Comment
                id, AutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')),
                content, TextField(verbose_name='评论内容')),
                create_at, DateTimeField(auto_now_add=True, verbose_name='创建时间')),
                is_active, BooleanField(default=True, verbose_name='是否显示')),
                priority, PositiveIntegerField(default=0, verbose_name='优先级')),
                likes, PositiveIntegerField(default=0, verbose_name='点赞数')),
                anonymous, BooleanField(default=False, verbose_name='是否匿名')),
                activity, ForeignKey(null=True, on_delete=django.db.models.deletion.CASCADE, related_name='comment', to='qbhelp.Activity', verbose_name='所在活动')),
## CommentChildren
                id, AutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')),
                content, TextField(verbose_name='评论内容')),
                create_at, DateTimeField(auto_now_add=True, verbose_name='创建时间')),
                likes, PositiveIntegerField(default=0, verbose_name='点赞数')),
                is_active, BooleanField(default=True, verbose_name='是否显示')),
                priority, PositiveIntegerField(default=0, verbose_name='优先级')),
                anonymous, BooleanField(default=False, verbose_name='是否匿名')),
## FormId
                id, AutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')),
                form_id, CharField(max_length=100, verbose_name='formId内容')),
                create_at, DateTimeField(auto_now_add=True, verbose_name='创建时间')),
                tmpl_scope, PositiveSmallIntegerField(choices=[(0, '可用于所有推送'), (1, '服务状态通知'), (2, '用户认证提醒'), (3, '用户留言提醒'), (4, '活动参加提醒')], default=0, verbose_name='使用范围')),
## OAuth2Client
                id, AutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')),
                client_id, CharField(max_length=20, verbose_name='客户端id')),
                account_id, CharField(max_length=20, verbose_name='账户id')),
                secret, CharField(max_length=40, verbose_name='秘钥')),
                create_time, DateTimeField(auto_now_add=True, verbose_name='创建时间')),
                scope, CharField(max_length=40, verbose_name='授权范围')),
## ShareRecord
                id, AutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')),
                user_id, IntegerField(default=0, verbose_name='User id')),
                openGId, CharField(default='', max_length=40, verbose_name='微信openGId')),
                object_type, PositiveIntegerField(choices=[(0, 'other'), (1, 'mission'), (2, 'activity'), (3, 'topic')], default=0, verbose_name='消息类型')),
                object_id, IntegerField(default=0, verbose_name='消息ID')),
                create_at, DateTimeField(auto_now_add=True, verbose_name='创建时间')),
 
