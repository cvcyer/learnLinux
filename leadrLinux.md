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

**shell**

