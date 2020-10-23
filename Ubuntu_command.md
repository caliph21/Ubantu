# 一.恢复Grub引导:
U_disk start:  
Ctrl+Shift+t,open Terminal.  
'<
ubuntu@ubuntu:~$ sudo su  
root@ubuntu:/home/ubuntu# fdisk -l  
root@ubuntu:/home/ubuntu# mount /dev/sda /mnt  
root@ubuntu:/home/ubuntu# grub-install --boot-directory=/mnt /dev/sda  
Installing for i386-pc platform.  
grub-install: error: failed to get canonical path of `/cow'.  

`/cow' Wrong:install 'boot-repair' repair boot:  
ubuntu@ubuntu:~$ df  
ubuntu@ubuntu:~$ sudo add-apt-repository ppa:yannubuntu/boot-repair && sudo apt-get update  
ubuntu@ubuntu:~$ sudo apt-get install -y boot-repair  
ubuntu@ubuntu:~$ boot-repair  >'
>>
select:Recommended repair...waitting...Create a Bootinfo summary(r).This may  require several mintutes....waitting.....restart...

> 在迁移后的Ubuntu下重装Grub  
进入Ubuntu，在Ubuntu系统下执行操作:  
sudo update-grub   
sudo grub-install /dev/sda  
>>>  
root@California:~# update-grub  
Sourcing file `/etc/default/grub'  
Sourcing file `/etc/default/grub.d/init-select.cfg'  
正在生成 grub 配置文件 ...  
找到 Linux 镜像：/boot/vmlinuz-5.4.0-52-generic  
找到 initrd 镜像：/boot/initrd.img-5.4.0-52-generic  
找到 Linux 镜像：/boot/vmlinuz-5.4.0-42-generic  
找到 initrd 镜像：/boot/initrd.img-5.4.0-42-generic  
Found memtest86+ image: /memtest86+.elf  
Found memtest86+ image: /memtest86+.bin  
完成  
root@California:~# grub-install /dev/sda  
正在为 i386-pc 平台进行安装。   
安装完成。没有报告错误。  
root@California:~# reboot  

# 二.主文件夹改成英文:    
语言改英文，重起，使用新本文档，语言改中文，重起，使用旧版本文档，勾选下次不再提示。  

# 三.垃圾文件清理  
Ubuntu Linux与Windows系统不同，Ubuntu Linux不会产生无用垃圾文件，但是在升级缓存中，Ubuntu Linux不会自动删除这些文件，今天就来说说这些垃圾文件清理方法。  
 一、删除缓存  
1，非常有用的清理命令：  
sudo apt-get autoclean                 清理旧版本的软件缓存  
sudo apt-get clean                     清理所有软件缓存  
sudo apt-get autoremove              删除系统不再使用的孤立软件  
这三个命令主要清理升级缓存以及无用包的。  

2，清理opera firefox的缓存文件：  
ls ~/.opera/cache4
ls ~/.mozilla/firefox/*.default/Cache  

3，清理Linux下孤立的包：  
图形界面下我们可以用：gtkorphan  
sudo apt-get install gtkorphan -y  
终端命令下我们可以用：deborphan  
sudo apt-get install deborphan -y  

4，卸载：tracker  
这个东西一般我只要安装ubuntu就会第一删掉tracker 他不仅会产生大量的cache文件而且还会影响开机速度。所以在新得利里面删掉就行。  
附录：  
包管理的临时文件目录:  
包在  
/var/cache/apt/archives  
没有下载完的在  
/var/cache/apt/archives/partial  

  二、删除软件  
ubuntu软件的删除一般用“ubuntu软件中心”或“新立得”就能搞定，但有时用命令似乎更快更好～～  
sudo apt-get remove --purge 软件名
sudo apt-get autoremove        删除系统不再使用的孤立软件  
sudo apt-get autoclean         清理旧版本的软件缓存  
dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P    清除残余的配置文件保证干净。  

  三、删除多余内核  
1，首先要使用这个命令查看当前Ubuntu系统使用的内核  
uname -a  

  2，再查看所有内核  
dpkg --get-selections|grep linux  
有image的就是内核文件  
  3，最后小心翼翼地删除吧  
sudo apt-get remove linux-image-2.6.32-22-generic  
ps：linux-image-xxxxxx-generic     就是要删除的内核版本  
还有
linux-headers-xxxxxx  
linux-headers-xxxxxx-generic     总之中间有“xxxxxx”那段的旧内核都能删，注意一般选内核号较小的删
内核删除，释放空间了，应该能释放130－140M空间。  

最后不要忘了看看当前内核：uname -a  
附录：  
包管理的临时文件目录:  
包在  
/var/cache/apt/archives  
没有下载完的在  
/var/cache/apt/archives/partial   


# 四、Ubuntu修改默认键盘布局的方法  

当初安装Ubuntu的时候选了键盘布局为英国的键盘布局（爱尔兰键盘），打代码的时候‘#’打成了一个类似‘£’的符号，‘|’打成了’~’。  

方法1：  
重启无效:>  
命令：sudo dpkg-reconfigure keyboard-configuration，使用这个命令后会出现非常人性化的伪图形界面供我们设置。  
然后选择步骤>>>> 按TAB选择》确定  
1.选择‘通用104键’---Generic 104-key PC  
2.英语（美国）English (US)  
3.键盘布局默认  
4.无组合键  
5.确保ubuntu右上角键盘的显示为“键盘-英语（美国）”，如果不是则点击设置为英语（美国）  

maya@California:~$ sudo dpkg-reconfigure keyboard-configuration  
Your console font configuration will be updated the next time your system  
boots. If you want to update it now, run 'setupcon' from a virtual console.  
update-initramfs: deferring update (trigger activated)  
正在处理用于 initramfs-tools (0.136ubuntu6.3) 的触发器 ...  
update-initramfs: Generating /boot/initrd.img-5.4.0-52-generic  
I: The initramfs will attempt to resume from /dev/sda5  
I: (UUID=925510db-1454-4e19-8f91-7e91a3910997)  
I: Set the RESUME variable to override this.  
 

> 方法2（有效）：  
设置>区域与语言>输入源（选择键盘布局或输入法）>-删除所有输入法>+添加英语（美国）+添加中文输入法，查看，完成  
%sudo ALL=(ALL:ALL) NOPASSWD: ALL  


# 五、Ubuntu出现无法定位软件包，更换源：  
解决办法很简单，更换另一个源就行了。一般建议是使用国内的源。  
1.在修改source.list前，最好先备份一份  
执行备份命令  
sudo cp /etc/apt/sources.list /etc/apt/sources.list.old  

2.执行命令打开sources.list文件：  
sudo vim /etc/apt/sources.list  
 
将下边的阿里源复制进去，然后点击保存关闭。  

清华源  

    deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted universe multiverse
    # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted universe multiverse
    deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse
    # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse
    deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse
    # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse
    deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security main restricted universe multiverse
    # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security main restricted universe multiverse

其他源：  
阿里源  

    deb http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse  
    deb http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse  
    deb http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse  
    deb http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse  
    deb http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse  
    deb-src http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse  
    deb-src http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse  
    deb-src http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse  
    deb-src http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse  
    deb-src http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse

网易源  

    deb http://mirrors.163.com/ubuntu/ wily main restricted universe multiverse
    deb http://mirrors.163.com/ubuntu/ wily-security main restricted universe multiverse
    deb http://mirrors.163.com/ubuntu/ wily-updates main restricted universe multiverse
    deb http://mirrors.163.com/ubuntu/ wily-proposed main restricted universe multiverse
    deb http://mirrors.163.com/ubuntu/ wily-backports main restricted universe multiverse
    deb-src http://mirrors.163.com/ubuntu/ wily main restricted universe multiverse
    deb-src http://mirrors.163.com/ubuntu/ wily-security main restricted universe multiverse
    deb-src http://mirrors.163.com/ubuntu/ wily-updates main restricted universe multiverse
    deb-src http://mirrors.163.com/ubuntu/ wily-proposed main restricted universe multiverse
    deb-src http://mirrors.163.com/ubuntu/ wily-backports main restricted universe multiverse


更新源
sudo apt-get update
   
更新软件
 sudo apt-get upgrade

卸载不需要了de软件包
sudo apt autoremove
下列软件包是自动安装的并且现在不需要了：
  libfprint-2-tod1
使用'sudo apt autoremove'来卸载它(它们)

# -->系统 软件安装与更新 失败 解决：  
1.更新阿里源：  
maya@California:/etc/apt$ sudo gedit sources.list  
sudo apt-get update  
sudo apt-get install -f  
您希望继续执行吗？ [Y/n] y  
2.软件安装与更新-换anli源-》重试更新  

# 六、you-get与pip安装：  
# 一、you-get:  
maya@California:~$ pip3 install you-get  
Collecting you-get  
  Downloading you_get-0.4.1456-py3-none-any.whl (217 kB)  
     |████████████████████████████████| 217 kB 23 kB/s   
Installing collected packages: you-get  
  WARNING: The script you-get is installed in '/home/maya/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.  
Successfully installed you-get-0.4.1456  

maya@California:~$ pip install you-get  
Defaulting to user installation because normal site-packages is not writeable  
Requirement already satisfied: you-get in /home/maya/.local/lib/python3.8/site-packages (0.4.1456)  

maya@California:~$ you-get  
you-get：未找到命令  

>>>+sudo:  
maya@California:~$ sudo pip install you-get  
Collecting you-get  
  Downloading you_get-0.4.1456-py3-none-any.whl (217 kB)  
     |████████████████████████████████| 217 kB 105 kB/s   
Installing collected packages: you-get  
Successfully installed you-get-0.4.1456  

maya@California:~$ you-get -V   
you-get: version 0.4.1456, a tiny downloader that scrapes the web.  

### >>>you-get命令详解：  
    

    获得下载资源的信息，使用-i参数,i代表info资源信息  
    1.you-get -i 【资源地址,http/https】，然后download-with命令下载对应的格式  
# 先使用you-get -i 【资源地址】   
maya@California:~$ you-get -i https://www.bilibili.com/video/BV1Pf4y1z7Rt  
site:                Bilibili  
title:               【叠纸新作】次世代3D恋爱动作手游《恋与深空》实机画面PV  
streams:             # Available quality and codecs  
    [ DASH ] ____________________________________  
    - format:        dash-flv  
      container:     mp4  
      quality:       高清 1080P  
      size:          35.4 MiB (37167283 bytes)  
    # download-with: you-get --format=dash-flv [URL]  

# 切换路径，然后再下载视频：  
maya@California:~$ cd ~/Downloads  
maya@California:~/Downloads$ you-get --format=dash-flv https://www.bilibili.com/video/BV1Pf4y1z7Rt  

# 指定文件夹：  #   
maya@California:~$ you-get -o ~/Desktop/恋与空 --format=dash-flv https://www.bilibili.com/video/BV1Pf4y1z7Rt  

# 设置自定义路径及文件名 # 
maya@California:~$ you-get -o ~/Desktop -O sky --format=dash-flv480 https://www.bilibili.com/video/BV1pz4y1o7ek  
    
#》》》批量下载B站的教程视频

贴上我需要下载的地址：https://www.bilibili.com/video/av71335007  
批量下载命令：  
you-get --playlist -o D:\docker教程 --format=flv https://www.bilibili.com/video/av71335007   

  
# 二、pip正确安装:
重新安装 pip 但不是通过 apt-get 而是通过 python -m  
因为我用的是 python3 ，所以我执行的命令为：  
'<
maya@California:~$ sudo python3 -m pip install --upgrade --force-reinstall pip  
Collecting pip  
  Downloading pip-20.2.4-py2.py3-none-any.whl (1.5 MB)  
     |████████████████████████████████| 1.5 MB 8.9 kB/s   
Installing collected packages: pip  
maya@California:~$ pip -V  
pip 20.2.4 from /usr/local/lib/python3.8/dist-packages/pip (python 3.8)  >'

成功安装 python3 对应的 pip ，并且修改 pip 指定为 python3 的包管理工具。此时执行 pip -V  


#七、>>>>ubuntu20.4安装最新版ffmpeg4.3以上版本详细流程
第一步：下载资源包  
官方链接如下：https://ffmpeg.org/download.html   
ffmpeg-4.3.1.tar.gz  

第二步：依次运行以下命令  
1、对资源包进行解压  
tar -zxvf ffmpeg-4.3.1.tar.gz  
2、进入资源包文件夹目录  
cd ffmpeg-4.3.1/  
3、建立文件夹build  
mkdir build  
4、进入build文件夹  
cd ./build  
5、安装yasm  
sudo apt-get install yasm  
6、运行配置文件  
../configure  
maya@California:~/Downloads/ffmpeg-4.3.1/build$ ../configure  
nasm/yasm not found or too old. Use --disable-x86asm for a crippled build.  

***maya@California:~/Downloads/ffmpeg-4.3.1/build$ ../configure --disable-x86asm  
7、编译(这个过程耗时比较久，耐心等待一下)  
make  
8、安装  
sudo make install  
9、运行下面语句出现这个界面说明安装成功(如果没有出现，重启电脑试试)  
ffmpeg -version  
maya@California:~/Downloads/ffmpeg-4.3.1/build$ ffmpeg -version  
ffmpeg version 4.3.1 Copyright (c) 2000-2020 the FFmpeg developers  
built with gcc 9 (Ubuntu 9.3.0-17ubuntu1~20.04)  
成功～  
再you-get 视频就能合并拉！  
参考：https://blog.csdn.net/my_name_is_learn/article/details/107408551  

maya@California:~/Downloads/ffmpeg-4.3.1/build$ you-get -o ~/Desktop/恋与空 --format=dash-flv https://www.bilibili.com/video/BV1Pf4y1z7Rt  
site:                Bilibili  
title:               【叠纸新作】次世代3D恋爱动作手游《恋与深空》实机画面PV  
stream:   
    - format:        dash-flv  
      container:     mp4  
      quality:       高清 1080P  
      size:          35.4 MiB (37167283 bytes)  
    # download-with: you-get --format=dash-flv [URL]  

Downloading 【叠纸新作】次世代3D恋爱动作手游《恋与深空》实机画面PV.mp4 ...  
 100% ( 35.4/ 35.4MB) ├████████████████████████████████████████┤[2/2]   12 MB/s  
Merging video parts... Merged into 【叠纸新作】次世代3D恋爱动作手游《恋与深空》实机画面PV.mp4  

Downloading 【叠纸新作】次世代3D恋爱动作手游《恋与深空》实机画面PV.cmt.xml ...  


#八、火狐安装flash

一、一般选择选者.tar.gz包  
二、 下载后解压：  
tar -zxvf flash_player_npapi_linux.x86_64.tar.gz  
maya@California:~/Downloads$ tar -zxvf flash_player_npapi_linux.x86_64.tar.gz  libflashplayer.so  
三、拷贝到火狐插件目录：  
sudo cp libflashplayer.so /usr/lib/firefox-addons/plugins/  
如果报目录不存在错误，说明火狐安装目录不是这个，看具体情况。  
maya@California:~/Downloads$ sudo cp libflashplayer.so /usr/lib/firefox-addons/plugins/  
maya@California:~/Downloads$ sudo cp -r usr/* /usr  
maya@California:~/Downloads$   
  运行了 #-->系统 软件安装与更新 失败 解决：  
火狐浏览器莫名其妙的可以播放视频了，即可。  

#九、安装pycharm2020.2.2及激活，见https://blog.csdn.net/caliph21/article/details/109096929
#九、git/github
maya@California:~$ mkdir myGithub  
maya@California:~$ cd myGithub  
maya@California:~/myGithub$ git init  
Command 'git' not found, but can be installed with:  
sudo apt install git  
maya@California:~/myGithub$ sudo apt install git  
maya@California:~/myGithub$ git init  
已初始化空的 Git 仓库于 /home/maya/myGithub/.git/  
save file:
maya@California:~/myGithub$ cp ~/Desktop/Ubuntu_command.md ~/myGithub  














