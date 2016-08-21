title: centos7修改ssh默认端口号
date: 2016-05-25 09:29:06
tags: [centos,centos7,linux]
---
## step1 修改/etc/ssh/sshd_config
`vim /etc/ssh/sshd_config`
#Port 22         //这行去掉#号
Port 8722      //下面添加这一行
<!-- more -->
## step2 修改SELinux
使用以下命令查看当前SElinux 允许的ssh端口：
`semanage port -l | grep ssh`

添加8722端口到 SELinux
`semanage port -a -t ssh_port_t -p tcp 8722`

然后确认一下是否添加进去
`semanage port -l | grep ssh`
如果成功会输出
`ssh_port_t                    tcp    8722, 22`

## step3 重启ssh
`systemctl restart sshd.service`
