# 破解Ubuntu Linux SSH服务

## 实验环境

Ubuntu  10.10.10.14/24

![1698645813277](D:\作业\网络攻防项目\破解Ubuntu Linux SSH服务\img\1.png)

Kali  10.10.10.15/24

![1698645876060](D:\作业\网络攻防项目\破解Ubuntu Linux SSH服务\img\2.png)

## 破解步骤

#### 1.加载Kali-Linux虚拟机，利用Nmap对目标10.10.10.14进行端口扫描

nmap -v -A -Pn 10.10.10.14

![1698646075124](D:\作业\网络攻防项目\破解Ubuntu Linux SSH服务\img\3.png)

#### 2.打开另一个新的命令窗口，输入ssh 用户名@IP地址,任意输入密码，提示访问被阻止。多次尝试，账户不会被锁定，满足暴力破解条件

![1698646367058](D:\作业\网络攻防项目\破解Ubuntu Linux SSH服务\img\4.png)

#### 3.使用Metasploit中的ssh_login模块进行破解，打开Kali系统终端,输入msfconsole

![1698646524474](D:\作业\网络攻防项目\破解Ubuntu Linux SSH服务\img\5.png)

#### 4.输入search ssh_login,搜索ssh_login,显示搜索到ssh_login模块

![1698646641296](D:\作业\网络攻防项目\破解Ubuntu Linux SSH服务\img\6.png)

#### 5.输入use auxiliary/scanner/ssh/ssh_login,加载ssh_login模块

![1698646705976](D:\作业\网络攻防项目\破解Ubuntu Linux SSH服务\img\7.png)

#### 6.输入show options,显示ssh_login模块参数

RHOSTS:目标主机IP地址

PASS_FILE:暴力破解密码字典存放路径

USERNAME:指定暴力破解使用的用户名

STOP_ON_SUCCESS:设置破解出密码后立即停止暴力破解

![1698646879664](D:\作业\网络攻防项目\破解Ubuntu Linux SSH服务\img\8.png)

#### 7.设置暴力破解目标主机的相关参数

![1698647858821](D:\作业\网络攻防项目\破解Ubuntu Linux SSH服务\img\9.png)

#### 8.成功获取密码，且破解出用户的UID GID 属于哪些组、操作系统的发行版本号和内核版本号

![1698648018638](D:\作业\网络攻防项目\破解Ubuntu Linux SSH服务\img\10.png)

#### 9.打开终端输入ssh 用户名@IP地址,并输入破解的密码,登录服务器

![1698648185373](D:\作业\网络攻防项目\破解Ubuntu Linux SSH服务\img\11.png)

#### 10.输入命令，查看服务器相关信息

ls -l

![1698648367788](D:\作业\网络攻防项目\破解Ubuntu Linux SSH服务\img\12.png)

## 添加Tcp_wrappers防御

#### 1.修改/etc/hosts.allow文件

![1698648790052](D:\作业\网络攻防项目\破解Ubuntu Linux SSH服务\img\13.png)

##### 修改/etc/hosts.deny

![1698648966339](D:\作业\网络攻防项目\破解Ubuntu Linux SSH服务\img\14.png)

#### 2.允许10.10.10.14的计算机登录SSH服务器，禁止10.10.10.15的计算机登录SSH服务器

##### 编辑文件/etc/hosts.allow,允许10.10.10.14的计算机登录Linux服务器

![1698650848006](D:\作业\网络攻防项目\破解Ubuntu Linux SSH服务\img\15.png)

##### 编辑文件/etc/hosts.deny,禁止10.10.10.15的计算机登录Linux服务器

![1698650882549](D:\作业\网络攻防项目\破解Ubuntu Linux SSH服务\img\16.png)

##### 编辑文件/etc/hosts.allow 和 /etc/hosts.deny完成后，需要重新启动SSHD服务

![1698651624834](D:\作业\网络攻防项目\破解Ubuntu Linux SSH服务\img\17.png)

##### 在客户端Kali使用exploit开始攻击，不能获取SSH服务器的密码

