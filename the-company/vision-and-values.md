---
cover: >-
  https://images.unsplash.com/photo-1552664730-d307ca884978?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=2970&q=80
coverY: 0
---

# Window 10

## 安装

{% hint style="info" %}
**现在的电脑都没有光驱等设备。一般都是通过UEFI方式启动安装系统。window系统的启动盘需要在window环境制作才能正常启动并安装。**
{% endhint %}

制作安装启动盘（该方法来之于网络，制作的盘可以启动，但是不能正确安装，中断在找不到可用于安装的硬盘或复制后无法启动windows而继续）

准备工作

* U盘 不小于16G
* Windows 10 ISO 镜像 微软官网下载 https://www.microsoft.com/en-gb/software-download/windows10ISO
*

#### 步骤1

使用diskutil命令确定你的USB盘在哪个驱动器上

```shell
#diskutil list
/dev/disk0(internal, physical):
#:       TYPE NAME           SIZE      IDENTIFIER
0: GUID_partition_scheme     *1.0TB    disk0
1: 
.
.
/dev/disk2(external, physical):
#:      TYPE NAME            SIZE      IDENTIFIER 
0: FDisk_partition_scheme    *31.4GB  disk2   
```

第七行的/dev/disk2就是我的U盘在电脑中的地址，不同的机器可能不一样。



#### 步骤2

格式化 U盘

```
#diskutil eraseDisk MS-DOS "WIN10" GPT /dev/disk2
Started erase on disk2
Unmounting disk
.
.
Finished erase on disk2
```

注意：对于某些硬件，你可能需要使用MBR格式分区，MBR格式最大只支持2TB的硬盘。把命令中的GPT改为 MBR制作出来的就是支持MBR格式的启动分区。

#### 步骤3

打开下载的Win10\_21H2\_Chinese(Simplified)\_x64.iso文件，会挂载处一个文件目录，MacOS 一般在/Volumes下,像这样/Volumes/CCCOMA\_X64FRE\_ZH-CN\_DV9。

#### 步骤4

复制Windows 10 ISO到 U盘

**2020 年 4 月更新：**Windows 10 ISO 中的一个文件 - install.wim - 现在太大而无法复制到 FAT-32 格式的 USB 驱动器。所以我会告诉你如何单独复制它。

首先运行此命令以复制除该文件之外的所有内容：

rsync -vha --exclude=sources/install.wim /Volumes/CCCOMA\_X64FRE\_ZH-CN\_DV9/\* /Volumes/WIN10rsync -vha --exclude=sources/install.wim /Volumes/CCCOMA\_X64FRE\_ZH-CN\_DV9/\* /Volumes/WIN10

然后使用 Homebrew 使用此终端命令安装名为 wimlib 的工具：

brew install wimlib

然后继续创建你要将文件写入的目录：

mkdir /Volumes/WIN10/sources

然后运行这个命令。请注意，此过程可能需要几个小时，在完成之前你可能会看到 0% 的进度。不要中止它。它将使用 wimlib 将 install.wim 文件拆分为 2 个小于 4 GB 的文件（我在以下命令中使用 3.8 GB），然后将它们复制到你的 USB：

wimlib-imagex split /Volumes/CCCOMA\_X64FRE\_ZH-CN\_DV9/sources/install.wim /Volumes/WIN10/sources/install.swm 3800

制作完成，可以用它启动，并安装windows 10了。

步骤6

## 配置

{% hint style="info" %}
****
{% endhint %}

### 打开openssh服务

设置->应用和功能->可选功能->添加功能->OpenSSH服务

运行->services.msc->OpenSSH服务->鼠标右键->启动

```
netstat -nat #查看
net start sshd #命令行启动
net user root 123456 /add #增加用户
net user root 123456 /active #激活用户
ssh localhost #连接测试
```

### 任务计划

```
schtasks /run /tn mytask # 启动任务
schtasks /end /tn mytask # 终止任务
```

## 操作

```
tasklist # 查看任务列表
takslist /fi "imagename eq myapp*" # 查找 myapp
taskkill /mi myapp                 # 关闭 myapp进程
taskkill /pid 33423                # 关闭 33423进程
taskkill /fi my*                   # 关闭 my 开头的全部进程
```
