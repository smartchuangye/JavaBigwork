## 各种包名详细介绍：
1. libs 包： 存放着需要用到的jar包，包括一下内容：
        （1）JDBC的驱动 ---》 mysql...
        （2）Apache公司的jar包，用来发送手机验证码（阿里云），以及发送短信验证码用到的jar包
        （3）Commons工具包对应的jar包

2. main 包：存放着主界面相关的类
        （1）UIFrame 类，注册登录界面

3. javabean 包： 封装了很多javabean对象，用来存储对象到数据库
        （1）User 类，对应数据库 bigwork中的user表，用来存放用户个人信息

4. jdbc 包：各种与JDBC相关操作的类，用来将数据存储到数据库
        （1）JDBCUtil 类，封装的基本操作的 工具类
        （2）

db.properties ---》 资源文件： 用来存储jdbc连接的基本信息，如用户名，密码等

待解决问题：
-----》    试题的删除             OK
----->      试题的编辑           OK
----->      AddSubjectToPaper       第146行，解决更新数据到数据库的过程   没毛病啊
                                    2019年11月30日19:30:23     测试发现还是有毛病滴，等待修改
                                    2019年11月30日19:41:23     已经解决，原因是：“ Data too long for column 'subjectTitle' at row 10”
                                                            将 subjectTitle 字段的类型改成 text 就行，可以存64kb

----》 考试管理界面：正在开发中，
        需求：发布考试，删除考试，统计考试信息（例如得分，平均分，每一题的错误率，以及参加考试的人数）-----》 管理员
                进行考试，考试结束之后可以查看成绩，查看哪些题目错了（这里主要以选择题为主）        ---》 学生
                
        需要完成的UI界面：   0.考试管理的主界面             OK
                            1. 预览试卷的 ui 界面，                 
                            2.学生进行答题的界面                 OK
                            3.发布考试的界面           OK
                            4.统计考试信息的界面
                            
              new  bug ---》 考试界面的按钮切换存在问题   2019年12月1日11:08:04    
                             mainUI界面切换之后选择表格中的一行选不到    2019年12月1日11:08:38
                             
             2019年12月2日22:41:33     增加了将学生的考试结果存储到数据库里面的功能，抛弃了 javabean 的使用，彻底使用工具类
                        待更改： 考试结束之后，用户可查看自己的考试结果   
             2019年12月3日14:16:50   上面的已经完成
             
2019年12月3日14:17:02      剩下带完成的功能：
            1. 人脸识别功能
            2.在选项卡之间切换之后不能继续选中表格中的某一行的BUG       --》 ok 2019年12月3日17:41:03
            3.已经考完了一次考试，下次继续开始考试时需要提示用户的功能
            4. 用户分为管理员和普通学生的功能
        2019年12月3日17:40:01          已经修改第2个BUG，实现方法：保证每个表格，表格模型，滚动面板只有唯一的一个对象（类似单例模式）
        2019年12月3日18:06:50         再次测试git提交,每次提交都要显示时间
        2019年12月3日22:32:13      
                完成人脸识别，在孙大佬的帮助下。思路：看了github上其他人的调用百度API接口例子，发现它的版本是V2版的，走了很多坑。最后在孙大佬的帮助下，顺利完成了。
                就是利用     列表 + Map     的存储方式存储数据，然后调用方法转换成为 Json 格式，然后调用对应的方法就行了。
                即 ArrayList(HashMap(String, String))   ，有2张图片，所以ArrayList里面应该有2个HashMap1的对象，每个对象通过Key-value的方式存放参数。
                github 参考项目地址：https://github.com/yigechaojivip/facematch-springmvc  
                不过没多大用处，因为他写的是V2版本，现在全面升级到V3版本了
    2019年12月4日14:43:00      
        昨天已经完成了人脸识别功能，今天完成 用户分为管理员和普通学生 部分，将用户登录注册界面和主界面关联起来
    2019年12月4日19:48:03  
        关联这些界面遇到新问题，发现密码没有用 MD5加密（加盐加密处理），所以首先得解决这个问题
        UserJDBC 待完成，功能：检测输入密码是否正确，还有用户点击发送验证码时检测该手机号或邮箱号是否注册，如果未注册，提示
2019年12月5日08:54:57  
    还要增加一个学生管理的界面，可以查看到所有注册登录过的学生，管理员可以查看学生的基本信息，例如考试信息
2019年12月5日16:58:54
    完成了人脸识别功能
2019年12月5日17:03:22
    下面要完成的功能，增加学生管理
2019年12月5日22:37:47
     尝试使用 
2019年12月8日14:07:03
    自己买了个云服务器，将数据库放到了服务器上，然后重构了一下代码  云服务器IP：101.132.147.111
2019年12月11日14:47:29
    需要新增一个学生管理的界面   --> 2019年12月14日13:17:58     完成了
2019年12月14日14:21:00 
    新增需求：
    （1）可以将表格中的数据导出 Excel 表格
    （2）新增 “成绩查询” 界面，学生只能查看本人的成绩，管理员（林凯）可以查看所有学生的成绩
 