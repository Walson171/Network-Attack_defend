# FTP服务

## 实验环境

kali  192.168.40.128

![image-20231023140930089](D:\作业\网络攻防项目\FTP服务\img\1.png)

Winser2000  192.168.40.137

![image-20231023142919178](D:\作业\网络攻防项目\FTP服务\img\2.png)

## 破解步骤

#### 1.打开kali 利用nmap扫描Winser2000 输入nmap 192.168.40.137

![image-20231023142844006](D:\作业\网络攻防项目\FTP服务\img\3.png)

#### 2.打开一个新的窗口连接ftp测试任意账户密码，检测是否会在密码多次错误的情况下锁定用户

![image-20231023144605934](D:\作业\网络攻防项目\FTP服务\img\4.png)

#### 3.打开Kali输入msfconsole

![image-20231023144745586](D:\作业\网络攻防项目\FTP服务\img\5.png)

#### 4.输入search ftp_login搜索ftp_login模块

![image-20231023144848093](D:\作业\网络攻防项目\FTP服务\img\6.png)

#### 5.输入use auxiliary/scanner/ftp/ftp_login加载ftp_login模块

![7](D:\作业\网络攻防项目\FTP服务\img\7.png)

#### 6.输入show options查看模块的参数

RHOSTS  目标主机IP地址

PASS_FILE  暴力破解密码字典存放路径

USERNAME  指定暴力破解使用的用户名

STOP_ON_SUCCESS  设置破解出密码后立即停止暴力破解

![image-20231023145329949](D:\作业\网络攻防项目\FTP服务\img\8.png)

#### 7.设置密码字典/也可以使用superdic生成字典

![image-20231023145549917](D:\作业\网络攻防项目\FTP服务\img\9.png)

![image-20231023150551704](D:\作业\网络攻防项目\FTP服务\img\13.png)

#### 8.设置暴力破解目标主机FTP的相关参数

![image-20231023145849204](D:\作业\网络攻防项目\FTP服务\img\10.png)

#### 9.输入exploit开始攻击成功获取administrator的密码为abc123

![image-20231023145949028](D:\作业\网络攻防项目\FTP服务\img\11.png)

#### 10.尝试登陆FTP打开kali输入ftp 192.168.40.137 输入获取的账户 密码

![image-20231023150227818](D:\作业\网络攻防项目\FTP服务\img\12.png)

## 防御步骤

#### 对于Winser的服务器 在管理工具下设置Internet服务管理器 选择默认的ftp站点属性 “目录安全性”选项卡下添加拒绝访问的Kali Linux系统的IP地址   192.168.40.128

![image-20231023151617091](D:\作业\网络攻防项目\FTP服务\img\14.png)

#### 不能正确获取密码

![image-20231023152636035](D:\作业\网络攻防项目\FTP服务\img\15.png)



