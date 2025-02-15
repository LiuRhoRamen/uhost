{{indexmenu_n>20}}

# 磁盘

## 查看硬盘分区

登陆云主机后，使用fdisk -l命令查看云主机的硬盘分区（Ubuntu中需要root权限）。

![image](/images/udisk_use1.png)

    系统盘：/dev/vda
    
    数据盘1：/dev/vdb
    
    数据盘2：/dev/vdc

## 系统盘扩容

本地盘和云盘目前采用不同的后台扩容模式。

选择本地盘扩容后，无需进入主机额外操作，但等待时间较长，可能达到30分钟；选择云盘扩容后，需要登陆云主机进行一系列操作。

### 本地盘

除去北京A机房，本地普通盘均支持在主机创建成功后，扩容系统盘到100G。

具体步骤：

1.  **为了防止系统盘文件系统有部分损坏，导致重启后无法开机，建议您先制作镜像，再执行扩容相关操作**
2.  选择“更改配置”-\> “更改磁盘容量” -\> 系统盘
3.  注意：本地盘的扩容模式系统盘扩容时间较长，扩容到100G可能需要关机等待30分钟。请确认。
4.  开始扩容。
5.  等待扩容结束，主机进入关机状态。

### 云硬盘

#### Linux

**为了防止系统盘文件系统有部分损坏，导致重启后无法开机，建议您先制作镜像，再执行扩容相关操作**

**步骤1：安装growpart**

CentOS：

    yum install -y epel-release
    yum install -y cloud-utils

Ubuntu：

    sudo apt-get install cloud-initramfs-growroot

**步骤2：扩容块设备并重启**

    growpart /dev/vda 1
    reboot

**步骤3：扩容文件系统**

虚拟机重启后执行:

``` 
resize2fs /dev/vda1 (ext4文件系统)
xfs_growfs /dev/vda1 (xfs文件系统)

```

**步骤4：确认**

查看是否扩容完成：

``` 
df -TH

```

#### Windows

在“计算机管理”中选择扩展卷，即可完成扩容。具体操作步骤如下：

![](/images/guide/sysdisk_step1.jpg)

![](/images/guide/sysdisk_step2.jpg)

![](/images/guide/sysdisk_step3.jpg)

![](/images/guide/sysdisk_step4.jpg)

![](/images/guide/sysdisk_step5.jpg)

![](/images/guide/sysdisk_step6.jpg)

![](/images/guide/sysdisk_step7.jpg)

![](/images/guide/sysdisk_step8.jpg)

## 数据盘扩容

### Step1 控制台操作

#### 磁盘类型：本地磁盘

![](/images/reconfig.png)

对于本地盘的磁盘扩容，在控制台，选择“更改配置”，关机升级后，重新开机，在主机内执行下述操作。

#### 磁盘类型：云硬盘

对于云硬盘（UDisk）的磁盘扩容，请先在主机内部完成卸载操作。

    mount -l //查看当前卷，假设/dev/vdb为云盘
    umount /dev/vdb
    fsck.ext4 /dev/vdb

然后在控制台选中磁盘，执行卸载操作：

![image](/images/udisk_del1.png)

在云硬盘控制面板完成扩容，并重新挂载，在主机内执行下述Step 2步骤的操作：

### Step2 命令行操作

#### 对于有数据盘扩容的主机

##### Linux操作系统

关机升级后，需在云主机内做如下操作：

    //查看数据盘的文件系统类型（升级操作需要针对ext4和xfs两种文件系统采取不同的操作）//
    df -ihT

![image](/images/ext4.png)

![image](/images/xfs.png)

    //针对ext4文件格式的操作系统（如CentOS6）：//
    umount /dev/vdb
    e2fsck -f /dev/vdb
    resize2fs /dev/vdb
    mount /dev/vdb /data

    //针对xfs文件格式的操作系统（如CentOS7）//
    umount /dev/vdb
    xfs_repair /dev/vdb
    mount /dev/vdb /data
    xfs_growfs /data

##### Windows操作系统

在主机上操作，cmd中输入diskpart.exe，list volume，选择要扩展大小的逻辑卷，输入要扩展大小extend
\[size=n\]， 或extend将所有未分配大小扩展到选择的逻辑卷

![image](/images/disk_extend.png)

#### 对于升级之前无数据盘的主机

（限本地磁盘）

##### Linux操作系统

升级后，需在云主机内做如下操作：

可选择ext4或xfs两种文件系统格式来格式化数据盘

将数据盘设置为ext4文件格式（CentOS6的默认文件系统格式）：

``` 
mkfs -t ext4 /dev/vdb 
mount /dev/vdb /data/

```

编辑/etc/fstab，将对应配置写入fatab

``` 
/dev/vdb   /data  ext4  defaults,noatime 0 0


```

将数据盘设置为xfs格式（CentOS7的默认文件系统格式）：

    mkfs.xfs /dev/vdb
    mount -t xfs /dev/vdb /data

编辑/etc/fstab，加入如下内容

    /dev/vdb /data xfs defaults,noatime 0 0

##### Windows操作系统

在主机上操作，cmd中输入diskpart.exe

1）输入list disk，select disk n (请根据实际情况，填写n的具体数值），选中数据盘。

2）输入create partition primary，创建分区。

3）输入list volume，可看到创建的卷。输入format fs=ntfs quick 进行分区

4）输入assign。分配驱动器号。

5）输入exit退出。系统中已可看到已创建的磁盘。

![image](/images/create_new_disk.png)

## 挂载云硬盘

在云主机详情界面-\>绑定-\>云硬盘-\>挂载，进行挂载操作。

    mkdir /udisk
    mount /dev/vdc /udisk
    df -h

## 卸载云硬盘

### Step 1 系统内卸载云盘

Linux操作系统：

    umount /dev/vdc

Windows操作系统：

首先在磁盘管理器中选中云磁盘，右键选择“脱机”。

![image](/images/udisk_windows_1.png)

然后在设备管理器中选中云硬盘，右键点击“卸载”。

![image](/images/udisk_windows_2.png)

这两个操作相当于在Windows系统中对云硬盘进行了dismount操作。

如果只有一个C盘，此时第二个便是云硬盘，建议在扩容前对云硬盘进行备份（如快照和克隆）。

在控制台云硬盘列表页选择需要扩容的云硬盘，将其卸载。这时云硬盘状态会从“已挂载”变为“可用”。

### Step 2 控制台操作

在云主机详情界面-\>绑定-\>云硬盘-\>找到指定磁盘-\>卸载，进行卸载操作。

**注意事项：系统盘无法被卸载。**

## 本地磁盘“缩容”

控制台不支持本地磁盘的“缩容”。但可以通过以下步骤变相实现“缩容”。**请注意，此操作会完全抹去数据，请先进行数据备份后操作！！！**

### Step 1 删除本地盘

首先进入系统内部进行卸载操作，操作步骤：

Linux操作系统：

    umount /dev/vdc

Windows操作系统：

首先在磁盘管理器中选中云磁盘，右键选择“脱机”。

![image](/images/udisk_windows_1.png)

然后在设备管理器中选中云硬盘，右键点击“卸载”。

![image](/images/udisk_windows_2.png)

在系统内完成卸载后，请在控制台选择 指定主机-\>详情-\>磁盘与恢复-\>删除本地盘。

    注意：本地盘的删除需要关机进行。

![](/images/guide/jietu20181227-174630.jpg)

### Step 2 添加本地盘

请在控制台选择 指定主机-\>详情-\>磁盘与恢复-\>新建本地盘，选择适合大小。

![](/images/guide/jietu20181227-174714.jpg)

新建后，请进入主机内部进行如下操作：

**Linux操作系统：**

升级后，需在云主机内做如下操作：

可选择ext4或xfs两种文件系统格式来格式化数据盘

将数据盘设置为ext4文件格式（CentOS6的默认文件系统格式）：

``` 
mkfs -t ext4 /dev/vdb 
mount /dev/vdb /data/

```

编辑/etc/fstab，将对应配置写入fatab

``` 
/dev/vdb   /data  ext4  defaults,noatime 0 0


```

将数据盘设置为xfs格式（CentOS7的默认文件系统格式）：

    mkfs.xfs /dev/vdb
    mount -t xfs /dev/vdb /data

编辑/etc/fstab，加入如下内容

    /dev/vdb /data xfs defaults,noatime 0 0

**Windows操作系统：**

在主机上操作，cmd中输入diskpart.exe

1）输入list disk，select disk n (请根据实际情况，填写n的具体数值），选中数据盘。

2）输入create partition primary，创建分区。

3）输入list volume，可看到创建的卷。输入format fs=ntfs quick 进行分区

4）输入assign。分配驱动器号。

5）输入exit退出。系统中已可看到已创建的磁盘。

![image](/images/create_new_disk.png)

同理，云盘亦不支持直接“缩容”，但可以在卸载后新建容量较小的云盘，直接挂载。
