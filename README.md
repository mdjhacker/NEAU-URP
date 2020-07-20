# NEAU-URP自助脚本

* 测试环境
  * Windows10Pro 2004 v19041.329
  * Windows7SP2
  * Python 3.5.0 32/64-bit
  * VScode
* 依赖包
  * requests
    * get
    * post
    * session
    * exceptions
  * re
    * complie
  * random
    * sample

### 免责声明
* 如您使用了该脚本，则视为您同意和遵守【免责声明】及其他相关条款的声明，且同意在使用时已获取校方同意，遵守相关校规校纪和法律法规。
* 该脚本仅用于社团教学演示与交流学习，请勿将该脚本用于正常教学选课等，不符合学校校规校纪和相关法律法规的场合！如有因此造成的各种后果，本人概不负责！
* 该脚本仅为个人学习测试使用，如因使用脚本造成的错选，漏选，意外退课及其他各种因非正常选课流程操作所导致的情况，本人概不负责！
* 该脚本允许二次开发和直接转载，但应当注明出处，本人不对二次开发后脚本的各种问题负责！

### 注意事项  
* 使用前建议核对运行目录，本程序会在当前目录生成导出文件
* 本人在尝试完成验证码自动识别模块时调用过多个API，例如百度和腾讯的普通OCR及高精度OCR。但是由于测试过程中发现依然容易出现识别不正确的情况，最终采用<b><i>肉眼识别</i></b>的方式手动输入验证码/doge
* ~~别问为什么不用机器学习啥的识别验证码，问就是懒~~
* 关于多线程这个，由于python默认解释器具有GIL锁，多核单线程的假“多线程”我也懒得写了，虽然确实可以优化，但是，嗯，不写了

### UPDATE V2.1 (2020.7.20)
* 功能新增
  * 【验证码】
    * 新增【看不清】选项，在输入验证码时输入 0 即可刷新验证码
    * 在验证码输入后 <b>删除</b> 验证码文件，避免多次登录时造成的验证码混淆
  * 【文件】
    * 文件夹检测与创建功能，免去了因为不存在指定文件夹造成的无法正常读写文件
  * 【重新获取CSS】
    * 在登陆后的菜单列表中增加重获CSS功能，避免因登陆时默认获取CSS失败造成的网页显示无表格
* BUG修复
  * 现在可以正确处理由于CSS获取时超时或其他连接原因造成的异常
  * 现在可以在无法获取到当前账户名时给予正确的返回和提示了
* 综合改善
  * 由requests导入exceptions改为由requests.exceptions导入各种具体模块
  * 各种常量统一移动到文件最前端
  * 新增<b>CONNECTION_TIME_OUT</b>和<b>READ_TIME_OUT</b>两个选项，用于在较差的网络环境下直接修改超时选项
  * 优化input输入提示

### UPDATE V2.0 (2020.7.17)
* 功能新增
  * 增加了【抢课模式】（此项功能不予公开，望谅解）
  * 增加了当前教务处账号【名字校验】功能，可用于当前cookie有效校验和有效期快速刷新
  * 完善了【成绩总表】功能，可以输出<b><i>成绩总表html</b></i>和<b><i>不及格成绩总表html</b></i>
* 综合改善
  * 增加了对网站CSS的获取
    * 在成功登录VPN时获取CSS，并写入本地文件
    * 利用获取到的CSS对成绩表HTML和课表HTML渲染，将其格式化，便于查看相应信息
  * 修改默认导出文件存储路径为 <b>./export/*</b> ，如有需要可手动更改文件目录
  * 修改了文件输出提示
  * 新增2.0版本的功能特性示例
  * 修改个别变量名
  * 修改换行缩进形式为空格符
* 下个版本更新计划
  * 优化代码逻辑结构
  * （可能做成多文件模组导入版，但是可能懒得写成多文件）

### UPDATE V1.2 (2020.7.15)
* 功能提升 && BUG修复
  * 选课查询时增加课序号查询，从而修复了由于课程号过多（如体育课）导致的无法正常选课和无法正常读取选课结果页面信息的bug
* 综合改善
  * 增加了选课查询params的备注说明
  * 保留了部分debug代码，方便各位读取和修改
* 下个版本更新计划
  * 预计增加当前账户名提示功能
  * 预计增加“发大水（洪水）”攻击版抢课功能
  
### UPDATE V1.1 (2020.7.13)
* GIT新增
  * 新增代码运行样例txt文件
* 功能新增
  * 增加了超时提示功能
  * 现在可以在单次运行中不重启程序选择端口了（如有已登录账户需先退出当前账户）
* BUG修复
  * 修复了多个账户切换时会导致判断为多次密码输入错误，致使意外退出的bug
  * 修复了对服务器页面<b><500 Servlet Exception></b>但是<b>HTTP 200</b>的错误情况无法正确响应的bug
* 综合改善
  * 改善了验证码读取刷新的逻辑结构，现在会在用户输入用户名后尝试获取验证码，如无法正常获取直接报超时错误，避免因验证码刷新不及时或无法获取导致的读写问题
  * 将 <b><i>选课结果.html</i></b> 和 <b><i>yzm.jpg</i></b> 的默认生成目录设为"./"，也可在代码中手动修改
  * 将import改为from ... import ... 的形式，便于pyinstaller编译，缩小编译后exe文件体积

自己上手写的一个教务系统自助选课、退课、查课表、查成绩（暂未完善）的脚本，疫情期间依赖于vpn.neau.edu.cn接入校园网，疫情结束后会给出校园网的对应接口版本

现release.py版本全程采用键入方式获取各种所需数据，后续会逐步完善各个功能和逻辑结构，并实现文本读取版本

如有问题，欢迎提出issue！