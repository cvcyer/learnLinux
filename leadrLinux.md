###常用命令

`data`  时间

`wget `  下载 

`uname -a` 内核版本

`watch -n 1 uptime` 每一秒刷新查看系统负载

`free -m` 查看内存使用情况

`last` 查看系统所有登入记录

`history -c` 清空历史记录

`more` 查看文件，默认一页

`head -n 20` 查看文件前20行

`tail -n 20` 查看文件后20行

`cat tr.txt | tr [a-z] [A-Z]` 查看文件并肩里面小写转为大写

`wc`  统计文本呢内容  -l  行数 -w 单词数 -c 字节数

`cut` 剪切文本内容   -d: 以分号分割 -f1只看第一列

 `diff` 比较文本文件差异

`touch` 创建与修改文件时间  -m 修改更改时间 -a 修改访问时间  -d 同时修改两个时间 

`mkdir ` 创建文件夹  -m 775 默认权限 775    -p连续创建多层级目录

`cp` 复制文件   -r 递归复制目录    -i 询问是否覆盖

`rm` 删除文件   -r 目录  -f  忽略警告  -i  提示

`dd`文件拷贝或转换  if 输入文件 of输出文件 bs 每个块大小  count 块的个数



`useradd` 创建新用户

`passwd` 修改用户密码

`userdel` 删除用户

`usermod` 修改用户属性

`groupadd` 创建用户群组

`tar` 解压缩文件 tar czvf tets.tar.gz /etc   tar -xzvf tets.tar.gz -C ~/test  -C指定解压到文件夹下

`grep ` 指定搜索  -v 反选   grep /sbin/nologin /etc/passwd  找出系统中不允许登录的用户

`find` 查找文件  find 路径 条件 操作    find /etc -name "host*" -print  查找etc路径下host开头的文件

>重定向

`>`  标准输出重定向到文件 ， 清空原有内容

`命令2>文件` 错误输出重定向到文件

`>>` 追加

`<` 输入重定向   `命令<文件` 将文件作为命令标准输入

`*` 匹配多个

`?` 匹配任意一个字符

`[0-9]` 匹配范围内数字

`[abd]` 匹配abd中的任意字符

`alias`  alias 命令=别名 

`$PATH$` 查看$PATH 变量

`PATH=$PATH:/root/bin` 为path变量增加内容

`env` 查看所有环境变量

定义变量 WORKDIR=/home/workdir

`export WORKERDIR`  将WORKERDIR变量提升为全局变量

>vim编辑器

 u 撤销上一步操作

N 跳转到上一个搜索内容



>主机名、网卡信息

/etc/hostname  `修改主机名`

> `配置网卡:` vim修改文件 --> 逐步写入配置参数 --> 重启网卡`systemctl restart network`   **ip 掩码255.255.255.0 gateway网关 DNS一般和网关相同**



> **shell**

`接收参数`

$0 当前执行shell脚本程序名

$1  第一个参数

$#  参数数量

$? 判断上一条命令是否成功，成功为0，失败非0

[  ] 注意两边均有空格  ， 测试语句   -d 是否为目录  -e存在 -f文件

`at` 任务进程，安排自动任务 ， at 7:00         at -l  查看任务列表

`cron` 长期服务     `crontab` -l 查看计划任务列表 -r删除计划任务  -e创建编辑任务

`chattr` 设置文件隐藏权限

`lsattr` 查看隐藏文件

`setfacl`  增加或修改ALC规则  ALC 针对指定用户设置对文件权限

`getfacl` 显示文件的ALC规则



#### 存储结构与磁盘划分

>单扇区容量512bytes 。 
>
>第一扇区 : 主引导记录(446byte)+ 分区表   , 所以第一扇区还可以用记录4个分区信息
>
>4个分区信息为3主分区+1扩展分区   扩展分区中可以有无限个逻辑分区 -----> 所以主分区不能超过4个
>
>/dev/sda5  代表第一块硬盘的编号为5的逻辑分区

`mount` 挂载  `mount /dev/cdrom  /media/cdrom`   系统会自动判断挂载文件类型     -t 指定文件系统

开机自动挂载     /etc/fstab 文件下  `uuid 挂载目录 文件格式 权限类型 是否自检 优先级`

`fdisk` 管理磁盘

`mkfs` 格式化硬盘  mkfs.ext4 /dev/sdb 格式化sdb硬盘为ext4格式

`df` 查看挂载点与磁盘使用情况     -T 展示文件系统类型

>SWAP 交换分区 将一部分硬盘空间虚拟化为内存使用，相对于物理硬盘速度慢，且真实内存用完后进行调用



>RAID 磁盘冗余阵列  多个硬盘实现提高硬盘性能和吞吐量   0 1 5 10多种方式
>
>方案： `RAID0` 多个磁盘串联，一损俱损        `RAID1`另一块上是镜像 50%使用率 
>
>​             `RAID5` 数据分散存在每块盘中，每块盘均有其他盘的校验信息，可尝试修复
>
>​             `RAID10` 融合RAID0 RAID1 成本高

`mdadm` 配置磁盘阵列    需要安装

`sudo mdadm -Cv /dev/md0 -a yes -n 4 -l 10 /dev/sdb /dev/sdc /dev/sdd /dev/sde`      

> -C 创建 -v显示详细过程  /dev/md0 阵列名称  -a yes检查RAID名称  -n 硬盘个数 -l 指定RAID级别  最后写加入到阵列的设备名称

> -D 查看阵列信息 -S 停止阵列  -f 模拟设备损坏  -r移除设备

`mdadm /dev/md0 -f /dev/sde` 模拟/dev/sde 在阵列中损坏

`mdadm /dev/md0 -a /dev/sde` 将sde硬盘加上

>**设置冗余硬盘，磁盘阵列中有一块有问题后自动替换**

-x 设置备份磁盘个数

`sudo mdadm -Cv /dev/md1 -n 3 -a yes -l 5 -x 1 /dev/sdb /dev/sdc /dev/sdd /dev/sde `

创建RAID5磁盘阵列，3块使用，1块作为备份故障盘

