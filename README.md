# 查看手机串口号

## 新增手机

[查看操作文档](https://www.cnblogs.com/fnng/p/8486863.html)

新增加手机时,需要连接usb线查询手机终端串口号码, 安装手机自动化测试软件

    python -m uiautomator2 init
    
## 查看串口号

安装完成后,手机上出现 **uiautomator** App, 点击进入, 查看 **IDENTIFY**, 显示中 **SERIAL** 为当前设备**串口号**


# 新增支付宝


## 查询已有设备

登录本地服务器 ***192.168.8.100(kyty)***,  使用终端进入文件目录 ***~/py-appium/db***, 执行命令

    sqlite3 app.ls
    
进入sqlite3 命令行

    select * from devices;
    
查询列出当前所有设备, 结果返回数据项以 "**|**" 分隔, 分别为 

    设备串口号|设备ip|支付宝账号|设备名称|连接方式|使用状态
    
**连接方式**: 0: usb接线连接, 1: 无线连接, 

**使用状态**: 0: 连接正常, 1: 停止连接
   
## 新增手机

**在登录新支付宝前先停止程序状态**

在**sqlite3** 命令行中执行SQL:
    
    INSERT INTO devices (deviceName, deviceIp, deviceAccount, phoneName, connectType, status, pwd) VALUES ('手机串口号', '手机ip地址, '支付宝账号', '手机名称(备注)', 0, 1, null);
    
程序根据新增状态来 **启动/停止** 当前手机

## 修改手机

**在登录新支付宝前先停止程序状态**

之前账号不使用, 更换新账号时, 只需要修改当前设备的支付宝账号和使用状态就可以

在**sqlite3** 命令行中执行SQL:

    update devices set deviceAccount='支付宝账号', status=程序状态 where deviceName='设备串口号';
