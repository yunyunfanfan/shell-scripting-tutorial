# Linux 命令速查表（中文版）

这是一份面向日常学习和运维实践的 Linux 常用命令速查表。内容覆盖用户信息、文件目录、权限、网络、软件包、磁盘、系统信息、文件搜索、SSH 和 Vi/Vim。

## 目录

| 序号 | 主题 |
| --- | --- |
| 1 | [用户信息](#用户信息) |
| 2 | [文件和目录命令](#文件和目录命令) |
| 3 | [文件权限](#文件权限) |
| 4 | [网络](#网络) |
| 5 | [安装软件包](#安装软件包) |
| 6 | [磁盘使用情况](#磁盘使用情况) |
| 7 | [系统和硬件信息](#系统和硬件信息) |
| 8 | [搜索文件](#搜索文件) |
| 9 | [SSH](#ssh) |
| 10 | [Vi/Vim 命令](#vivim-命令) |

## 用户信息

### `who`

查看当前登录到系统的用户。如果不带任何选项，会显示登录用户名、终端、登录时间以及远程主机信息。

```bash
who
```

示例输出：

```text
pavankumar :0 2024-01-01 01:21 (:0)
```

### `whoami`

显示当前终端会话对应的用户名。

```bash
whoami
```

### `id`

显示当前用户的 UID、GID 以及所属用户组。

```bash
id
```

示例输出：

```text
uid=1000(sj) gid=1000(sj) groups=1000(sj),4(adm),27(sudo)
```

### `groups`

显示当前用户所属的所有用户组。

```bash
groups
```

也可以查看指定用户：

```bash
groups username
```

### `finger`

查看当前登录用户的详细信息，例如登录时间、终端、空闲时间、家目录、默认 shell 等。

```bash
finger
```

很多 Linux 发行版默认不安装该命令，可以手动安装：

```bash
sudo apt install finger
```

### `users`

显示当前登录系统的所有用户名。

```bash
users
```

### `grep`

可以从 `/etc/passwd` 中查找某个用户的账户信息。

```bash
grep -i username /etc/passwd
```

示例：

```bash
grep -i sj /etc/passwd
```

### `w`

显示当前登录用户，以及每个用户正在执行的操作。

```bash
w
```

也可以查看指定用户：

```bash
w username
```

### `last` 和 `lastb`

显示系统最近登录记录。`last` 查看成功登录记录，`lastb` 查看失败登录记录。

```bash
last
last username
lastb
```

### `lastlog`

查看所有用户或指定用户最近一次登录信息。

```bash
lastlog
lastlog -u username
```

[返回顶部](#目录)

## 文件和目录命令

### `pwd`

打印当前工作目录的绝对路径。

```bash
pwd
```

示例输出：

```text
/home/pavankumar/Desktop/Linux
```

### `ls`

列出文件和目录。

```bash
ls
ls [选项] [目录]
```

常用示例：

```bash
ls
ls -ltr
ls ~
```

常用选项：

```text
-a  显示所有文件，包括隐藏文件
-R  递归列出子目录
-r  反向排序
-t  按最后修改时间排序
-S  按文件大小排序
-l  使用长格式显示
-1  每行显示一个文件
-m  使用逗号分隔输出
-Q  给文件名加引号
```

### `mkdir`

创建目录。

```bash
mkdir ubuntu
```

使用 `-p` 可以一次创建多级目录：

```bash
mkdir -p dir1/dir2/dir3
```

### `rmdir`

删除空目录。相比 `rm -r`，它更适合删除确定为空的目录。

```bash
rmdir FolderName
rmdir FolderName1 FolderName2 FolderName3
```

删除多级空目录：

```bash
rmdir -p a/b/c
```

忽略非空目录导致的失败：

```bash
rmdir FolderName --ignore-fail-on-non-empty
```

### `rm`

删除文件、目录、符号链接等对象。使用该命令要格外谨慎。

```bash
rm file_name
rm -f file_name
rm -r myDir
rm -rf myDir
```

说明：

```text
-f  强制删除，不提示确认
-r  递归删除目录及其内容
-rf 强制递归删除，危险操作，确认路径后再执行
```

### `touch`

创建空文件，或修改文件的访问时间和修改时间。

```bash
touch file_name
touch file1 file2 file3
touch -a file_name
touch -m file_name
touch -r source_file target_file
touch -t 1911010000 file_name
```

说明：

```text
-a  修改访问时间
-m  修改内容修改时间
-r  使用另一个文件的时间戳
-t  指定时间戳
```

### `cat`

创建文件、查看文件内容、拼接文件，并可将输出重定向到终端或文件。

```bash
cat [选项] [文件]...
```

创建文件：

```bash
cat > file_name1.txt
Hello, Linux!
```

输入完成后按 `Ctrl+D` 结束。

查看文件内容：

```bash
cat file_name1.txt
cat file_name1.txt file_name2.txt
```

分页查看长文件：

```bash
cat file_name1.txt | more
cat file_name1.txt | less
```

[返回顶部](#目录)

## 文件权限

Linux 是多用户操作系统，需要通过权限机制控制用户对文件和目录的访问。

### 所有者

每个文件或目录通常涉及三类对象：

```text
user   文件所有者
group  文件所属用户组
other  系统中的其他用户
```

### 权限类型

```text
r  read，读取权限
w  write，写入权限
x  execute，执行权限
-  没有对应权限
```

对文件来说：

```text
r  可以读取文件内容
w  可以修改文件内容
x  可以执行该文件
```

对目录来说：

```text
r  可以列出目录内容
w  可以在目录中创建、删除、重命名文件
x  可以进入该目录
```

### `chmod`

修改文件或目录权限。

```bash
chmod [权限] file
```

#### 数字模式

权限可以用三位八进制数字表示：

| 权限 | 数字 | 符号 |
| --- | --- | --- |
| 无权限 | 0 | `---` |
| 执行 | 1 | `--x` |
| 写入 | 2 | `-w-` |
| 写入 + 执行 | 3 | `-wx` |
| 读取 | 4 | `r--` |
| 读取 + 执行 | 5 | `r-x` |
| 读取 + 写入 | 6 | `rw-` |
| 读取 + 写入 + 执行 | 7 | `rwx` |

示例：

```bash
chmod 764 test.txt
```

含义：

```text
7  所有者：读、写、执行
6  用户组：读、写
4  其他用户：只读
```

#### 符号模式

对象：

```text
u  user，所有者
g  group，用户组
o  other，其他用户
a  all，所有人
```

操作符：

```text
+  添加权限
-  移除权限
=  设置为指定权限
```

示例：

```bash
chmod u+x script.sh
chmod g-w test.txt
chmod o=r test.txt
chmod a-rwx secret.txt
```

### `chown`

修改文件或目录的所有者和所属用户组。

```bash
chown user filename
chown user:group filename
```

示例：

```bash
chown john test.txt
chown john:admin test.txt
```

### `chgrp`

只修改文件或目录的所属用户组。

```bash
chgrp group_name filename
```

示例：

```bash
sudo chgrp Administrator test.txt
```

[返回顶部](#目录)

## 网络

### 显示网络信息

`ifconfig` 可以显示网卡、IP 地址等网络信息。部分新系统默认使用 `ip` 命令。

```bash
ifconfig -a
ip addr show
```

### 测试远程连接

使用 `ping` 向远程主机发送测试包。

```bash
ping 172.16.1.222
ping example.com
```

### 查看本机 IP 地址

```bash
hostname -I
ip addr show
```

### 查看监听端口

```bash
netstat -pnltu
```

如果系统没有 `netstat`，可以使用：

```bash
ss -pnltu
```

### 查询域名信息

`whois` 可以查询域名所有者、注册信息、域名服务器等信息。

```bash
whois google.com
```

[返回顶部](#目录)

## 安装软件包

不同 Linux 发行版使用不同包管理器。原文示例主要使用 `yum`，常见于 CentOS、RHEL、Rocky Linux、AlmaLinux。

### 使用 `yum` 安装软件包

```bash
sudo yum install package_name
```

查看软件包信息：

```bash
yum info package_name
```

卸载软件包：

```bash
sudo yum remove package_name
```

### 从本地 RPM 文件安装

```bash
sudo rpm -i package_name.rpm
```

### 从源码安装

```bash
tar zxvf sourcecode.tar.gz
cd sourcecode
./configure
make
sudo make install
```

### Debian/Ubuntu 常用命令

如果你使用 Ubuntu、Debian 或 WSL Ubuntu，更常用的是 `apt`：

```bash
sudo apt update
sudo apt install package_name
sudo apt remove package_name
apt show package_name
```

[返回顶部](#目录)

## 磁盘使用情况

### `du`

查看文件和目录占用的磁盘空间。

```bash
du [选项] [文件或目录]
```

查看 `/home` 目录树的空间占用：

```bash
du /home/
```

以人类可读格式显示：

```bash
du -h /home/
```

查看目录总占用：

```bash
du -sh /home/
```

查看所有文件和目录：

```bash
du -ah /home/
```

限制显示深度：

```bash
du -ah --max-depth 2 /home/
```

排除指定模式的文件：

```bash
du -ah --exclude="*.txt" /home/
```

查看帮助：

```bash
du --help
```

[返回顶部](#目录)

## 系统和硬件信息

### `uname`

显示系统信息。

```bash
uname -a
```

常用选项：

```bash
uname -s   # 内核名称
uname -r   # 内核版本
uname -m   # 机器架构
uname -o   # 操作系统
```

[返回顶部](#目录)

## 搜索文件

### `grep`

在文件中搜索匹配指定模式的文本。

```bash
grep pattern files
```

常用选项：

```text
-i  忽略大小写
-r  递归搜索目录
-v  反向匹配，显示不匹配的行
```

示例：

```bash
grep "^hello" test.txt
grep -i "hELLo" test.txt
grep -r "TODO" .
```

### `find`

按文件名、目录名、时间、所有者、权限等条件搜索文件和目录，并可对搜索结果执行操作。

按名称搜索：

```bash
find ./directory_name -name file_name
```

示例：

```bash
find ./test -name test.txt
```

按模式搜索：

```bash
find ./test -name "*.txt"
```

搜索后执行命令：

```bash
find ./test -name test.txt -exec rm -i {} \;
```

搜索空文件或空目录：

```bash
find ./directory_name -empty
```

按权限搜索：

```bash
find ./directory_name -perm 664
```

在多个文件中搜索文本：

```bash
find ./ -type f -name "*.txt" -exec grep "World" {} \;
```

### `whereis`

查找命令对应的二进制文件、源码文件和 man 手册位置。

```bash
whereis command_name
```

示例：

```bash
whereis netstat
```

### `locate`

按文件名快速查找文件。它通过数据库搜索，通常比 `find` 更快，但结果依赖数据库是否及时更新。

```bash
locate "*.txt" -n 10
```

如果找不到新文件，可以先更新数据库：

```bash
sudo updatedb
```

[返回顶部](#目录)

## SSH

SSH（Secure Shell）是一种网络协议，用于在两台系统之间建立安全的远程连接。

### 连接远程主机

使用主机名或 IP 地址连接：

```bash
ssh 192.111.66.100
ssh test.remoteserver.com
```

指定用户名：

```bash
ssh username@hostname_or_ip
```

示例：

```bash
ssh john@192.0.0.22
ssh john@test.remoteserver.com
```

指定端口：

```bash
ssh hostname_or_ip -p port_number
```

示例：

```bash
ssh test.remoteserver.com -p 3322
```

### 生成 SSH 密钥

生成公钥和私钥，用于免密登录或 GitHub SSH 认证。

```bash
ssh-keygen -t rsa
```

更推荐的新算法：

```bash
ssh-keygen -t ed25519
```

### 复制公钥到服务器

```bash
ssh-copy-id username@hostname_or_ip
```

### 通过 SSH 远程复制文件

`scp` 可以通过 SSH 协议安全复制文件。

```bash
scp fileName user@remotehost:destinationPath
```

示例：

```bash
scp test.txt test@10.0.0.64:/home/john/Desktop
```

### 编辑 SSH 服务配置

```bash
sudo vim /etc/ssh/sshd_config
```

### 在远程服务器执行命令

```bash
ssh test.remoteserver.com mkdir NewDirectoryName
```

### 重启 SSH 服务

修改 SSH 配置后通常需要重启服务。

```bash
sudo systemctl restart ssh
sudo systemctl restart sshd
```

[返回顶部](#目录)

## Vi/Vim 命令

Vi 是 Unix 早期流行的文本编辑器。Vim 是 Vi IMproved 的缩写，是 Vi 的增强版本，常用于命令行中编辑配置文件和脚本。常见替代编辑器还包括 Nano、Emacs、Joe 等。

Vim 主要有两种常见模式：

```text
普通模式 / 命令模式：移动光标、删除、复制、保存等
插入模式：输入文本
```

### 打开文件

创建新文件或打开已有文件：

```bash
vi filename
vim filename
```

基本流程：

1. 执行 `vi first.txt` 打开文件。
2. 按 `i` 进入插入模式。
3. 输入 `Hello World!`。
4. 按 `Esc` 回到普通模式。
5. 输入 `:wq` 保存并退出。

### 光标移动

方向移动：

```text
h  左移
j  下移
k  上移
l  右移
```

按单词跳转：

```text
w  跳到下一个单词开头
W  跳到下一个 WORD 开头
e  跳到当前或下一个单词结尾
E  跳到当前或下一个 WORD 结尾
b  跳到前一个单词开头
B  跳到前一个 WORD 开头
```

行内跳转：

```text
^       跳到当前行开头的第一个非空字符
$       跳到当前行末尾
Enter   跳到下一行开头
```

屏幕位置：

```text
Backspace  光标左移一个字符
Spacebar   光标右移一个字符
H          跳到屏幕顶部
M          跳到屏幕中部
L          跳到屏幕底部
```

翻页和滚动：

```text
Ctrl+f  向前翻一整页
Ctrl+b  向后翻一整页
Ctrl+d  向前翻半页
Ctrl+u  向后翻半页
```

### 插入文本

从普通模式进入插入模式：

```text
i    在光标左侧插入
I    在当前行开头插入
a    在光标右侧追加
A    在当前行末尾追加
o    在当前行下方新开一行
O    在当前行上方新开一行
Esc  退出插入模式，回到普通模式
```

### 修改文本

```text
cw  修改光标右侧的一个单词或部分单词
cc  修改整行
C   从光标位置修改到行尾
```

### 删除文本

```text
x   删除光标所在字符
X   删除光标前一个字符
dw  删除一个单词
dd  删除整行
```

### 复制、剪切和粘贴

普通模式下，`y` 表示复制，`d` 表示剪切或删除，`p` 表示粘贴。

复制：

```text
yy   复制整行
3yy  从当前行开始复制 3 行
yaw  复制一个单词，包含后面的空白
yiw  复制一个单词，不包含后面的空白
y$   从光标复制到行尾
y^   从光标复制到行首
ytx  复制到字符 x 之前，不包含 x
yfx  复制到字符 x，包含 x
```

剪切：

```text
dd   剪切整行
3dd  从当前行开始剪切 3 行
d$   从光标剪切到行尾
d^   从光标剪切到行首
```

粘贴：

```text
p    粘贴到光标之后
P    粘贴到光标之前
```

### 可视模式

先选择文本，再执行复制、剪切、粘贴等操作。

```text
v       按字符选择
V       按整行选择
Ctrl+v  按块选择
y       复制选中内容
d       剪切或删除选中内容
p       粘贴
```

### 保存和退出

```text
:w    保存文件，但不退出
:wq   保存并退出
:wq!  强制保存并退出
:q    退出；如果文件有修改会失败
:q!   不保存修改，强制退出
```

[返回顶部](#目录)

## 返回主页

- [中文 README](../README_Ch.md)
- [英文原版速查表](Linux-cheat-sheet.md)
