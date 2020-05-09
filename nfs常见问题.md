## 挂载特定版本
```
mount -t nfs -o vers=4.0 55.55.57.118:/data/opm /mnt/opm
```

## nfs client mount failure

    [root@node94 mnt]# mount -t nfs 172.25.84.190:/NAS/CAPFS/data/nfs nas_nfs
    mount: wrong fs type, bad option, bad superblock on 172.25.84.190:/NAS/CAPFS/data/nfs,
       missing codepage or helper program, or other error
       (for several filesystems (e.g. nfs, cifs) you might
       need a /sbin/mount.<type> helper program)

       In some cases useful info is found in syslog - try
       dmesg | tail or so.

## nfs client mount success

    [root@node94 mnt]# mount -t nfs 172.25.84.93:/NAS/CAPFS/data/nfs nas_nfs

## 怎么用iso安装nfs客户端

1. 上传CentOS.iso镜像
2. 创建/mnt/cdrom目录后运行 mount -t iso9660 CentOS.iso /mnt/cdrom 将镜挂载到/mnt/cdrom目录
3. 备份/etc/yum.repos .d/CentOS-Base.repo文件并修改原文件中的[base]部分为如下：

          [base]
          name=CentOS-$releasever - Base
          baseurl=file:///mnt/cdrom
          gpgcheck=1
          gpgkey=file:///mnt/cdrom/RPM-GPG-KEY-CentOS-7

4.将其他分段禁止掉:

          enabled=0
          
5.yum install nfs-utils安装客户端

## nfs共享怎么看

     showmount -e

## nfs配置文件在哪里

    /etc/exports.d/

## nfs挂载命令

    mount -t nfs 192.168.0.22:/share/nfs /mnt/nfs
    
## nfs 客户端是否 direct io

nfs客户端可以缓存数据后发给 nfsd，此时每个报文大小是1M，否则根据应用下发的大小，比如vdbench 先设置 64k 大小下发。

## rwx/u

在nfs客户端上，touch file 后mode为 644，在nfs服务器目录下为 644

## rwx/ugo

在nfs客户端上，touch file 后mode为 777，在nfs服务器目录下为 644

## NAS机头查看export 出去的共享目录

   exportfs -v
   
其实 showmount -e 也能看到export出下的目录，不过好像信息没有 exportfs -v全

## 没有 export出去的目录，在nfs客户端也能mount，但是是readonly

在4.0 以上的版本中，不是export出去的目录也能在nfs 客户端上挂载，只是为read only。
