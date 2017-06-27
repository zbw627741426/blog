---
title: ArchLinux安装教程
---

## 安装前准备
使用VirtualBox安装，一定要**固定空间**大小，选择默认8G就可以了。

## 设置键盘和字体
键盘配置文件在 `/usr/share/kbd/keymaps/i386/**` `load-keys`设置
查看键盘配置文件，还有Emacs配置，**占个坑**留待以后详查。

字体配置文件在 `/usr/share/kbd/consolefont/**` `set-font`设置  

## 查看启动模式boot mode

启动模式有两种：`BISO`和`UEFI`。
`UEFI`: Unified Extensible Firmware Interface 可改写ROM
`system-boot` is a simple UEFI manager tool.  And the configure file is in /sys/firmware/efi/efivars if is UEFI.
`BIOS`: Basic Input/Output System 不可改写ROM
我的电脑LENOVE G470 是后者。

## 配置网络

通常来说，wire有线连接系统会自动配置好。[Network Configure](https://wiki.archlinux.org/index.php/Network_configuration#Device_driver)
wireless[无线配置](https://wiki.archlinux.org/index.php/Wireless_network_configuration)

## 系统时钟
`timedatectl` 此工具可以用来显示设置时间、时区、开启网络时间（同步时间）。
当然了，能实现某一功能的软件多的是，`date`也可以实现，还有其他的。但是工作原理都是一样的，以**设置时区**为例：
`/usr/share/zoneinfo/**/**`存储着位于各个时区的大城市，比如中国是`/usr/share/zoneinfo/Asia/Shanghai`, 这是一个二进制文件Binary File， 想要设置时区，先建立一个`/etc/localtime` 二进制文件，在建立一个sysbolic link 指向`/usr/share/zoneinfo/Asia/Shanghai`。
网络时钟同步： timedatectl set-ntp [bool]  
此工具既可以设置系统时钟也可以设置RTC(real-time clock)或者叫hardware clock，反正就是指主板时钟，由可充电纽扣电池供电，即便后关机还继续运行。
`timedatectl set-local-rtc [bool]` `on`: local time `off` universal time 设置RTC是使用UTC（世界协调时Coordinated Universal Time）还是CST（中国标准时China Standard Time），可见要先设置好时区，建议RTC使用UTC。
`hwclock`获取或设置RTC。

## 分区 partition

1. 分区表
多数情况下一块硬盘要分成一个或一个以上分区，也就是建立分区表，除SWAP分区外，必须格式化后才能进行数据读取access。
DISKLABEL TYPE (不知道怎么翻译，就是指分区表的类型）主要有两种： MBR GPT。
MBR(Master Boot Record):
- The MBR is not located in a partition; it is located at a first sector（扇区） of the device (physical offset 0), preceding（先于） the first partition.   
- 分成Primary和Extended两种形式，Extended包含有一个至无限多个Logical分区。
- 最多有三个Primary分区，先要分更多区，需要把一个分区变为Extended分区，在这个Extended分区内建立一个至多个Logical分区。
- 只有Primary分区可以引导启动。
- 最早由MSDOS引进，也称DOS Partition table  

GPT(GUID Partition table)是UEFI的一部分，可以继承MBR，使用GUID(Global Unique identifier）方式来定义分区。

选择： 对于新式电脑，主板支持UEFI，使用GPT,否则使用MBR。

也可以不进行分区，直接使用一块硬盘（注意：一块硬盘只分成一个分区也叫分区），可以使用[Btrfs](https://wiki.archlinux.org/index.php/Btrfs)。过后再了解。

2. 进行分区
   1. 建立分区表
      推荐使用`fdisk`或者`parted`。都是dialogue-driven(对话驱动）模式，参考着帮助文件，很简单就可以完成分区任务，此处不需累述。
      首先，建立DISKLABEL TYPE ,MBT就是DOS。o 建立DOS 类型分区表，w 写分区表。
      然后，n 新建分区，p 指定格式。还有序号、类型、大小根据对话来分配。
   2. 格式化分区
      格式化的意思是给分区指定文件系统，ext2、ext4、fat32等。In computing, a file system (or filesystem) is used to control how data is stored and retrieved. Without a file system, information placed in a storage medium would be one large body of data with no way to tell where one piece of information stops and the next begins. By separating the data into pieces and giving each piece a name, the information is easily isolated and identified.   
      mkfs.ext4 /dev/sda1 指定ext4格式 mkfs.ntfs 指定ntfs格式

## 挂载分区
mount /dev/sda1 /mnt
mount /dev/sda2 /mnt/home
此处挂载分区的目的是，将后续需要安装的包下载到分区中。

## 安装软件
`pacstrap`会读取`/etc/pacman.d/mirrorlist`列表，先修改此配置文件，选择163的镜像，`pacstrap /mnt base`会安装base package group。

## 分区表写进配置文件

`genfstab -U /mnt >> /mnt/etc/fstab`
到下一步chroot之前，都是运行在LiveCD环境中，在这个环境中，给正式系统分了区，分别设置了文件系统（ext4），下载了base package grop，[这里](https://www.archlinux.org/groups/x86_64/base/)查看group包含的软件和内核。现在把正式系统的分区表写进正式系统的配置文件中，LiveCD就可以退出，以后用不到了。也就是说LiveCD相当于系统安装程序，除了更复杂一些。

## chroot
Chroot is an operation that changes the apparent root directory for the current running process and their children. A program that is run in such a modified environment cannot access files and commands outside that environmental directory tree. This modified environment is called a chroot jail.
就是说，将整个运行环境从LiveCD切换至正式系统中去，是修复不能自己启动的系统常用方法。
The bash script **arch-chroot** is part of the arch-install-scripts package. Before it runs /usr/bin/chroot, the script mounts api filesystems like /proc and makes /etc/resolv.conf available from the chroot.
`arch-chroot /mnt`

## 设置时间 时区 本地化 主机名 网络 root账户密码

参考[这里](https://wiki.archlinux.org/index.php/Installation_guide#Time_zone),知识点在前面已经讲过。
root密码要设置的复杂一些，不然虽然能设置成功，但是重启后登录密码不正确。不知道什么原因。

## 安装GRUB启动引导

`pacman -S grub` 安装GRUB2软件
`grub-install --target=i386-pc /dev/sdx` 安装GRUB到需要引导的硬盘
`grub-mkconfig -o /boot/grub/grub.cfg` 创建配置文件，写到/boot/grub/grub.cfg中。
