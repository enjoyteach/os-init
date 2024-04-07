# os-init
搭建适合自己的linux系统，包含安装与软件（所有软件及镜像均来自官方网站，切勿所以下载非官方镜像小心菊花被开）

# 系统安装 -ubuntu22.04
采用ubuntu22.04是因为他是LTS（长期技术支持版本，另外今年会发布24.04LTS安装应该会有不同）

# 软件安装方式介绍 

1. snap安装方式（ubuntu自带）
   
 优点：这玩意说白了就是模仿macos的安装方式，所有的文件都独立在一个文件夹中，无需解决软件间的依赖问题，所有依赖都提前准备好了，独立性和通用性没得说，非常适合桌面用户，但是不太适合于服务器！

 缺点：占用体积较大，可能消耗更多资源（桌面用户不在乎）
 
## 常用命令：
      
查看snap安装软件：
`sudo snap list`

在应用商店中查找snap：
`sudo snap find <软件包名>`

安装Snap软件：
`sudo snap install <snap软件包名>`

更新Snap软件：
`sudo snap refresh <snap软件包名>`

更新所有的snap软件包：
`sudo snap refresh all`

Snap还原到以前安装的版本：
`sudo snap revert <snap软件包名>`

卸载snap软件：
`sudo snap remove <snap软件包名>`

---

2. deb文件安装
   
dpkg 是“Debian Packager ”的简写。为 “Debian” 专门开发的套件管理系统，方便软件的安装、更新及移除。可以理解为类似window的安装文件exe或者msi文件。不过用着个安装的话软件的程序可能分布在不同的目录，删除使用命令别直接删除
deb安装文件的后缀是deb，使用dpkg命令进行安装与卸载操作


使用dpkg -i   *.deb 的时候出现依赖没有安装

使用apt-get -f -y install  解决依赖问题后再执行dpkg安装deb包

## 常用命令：


安装.deb格式的软件包文件。  `dpkg -i <软件包路径>`

用于删除软件包保留配置。    `dpkg -r <软件包名>`

用于删除软件包不保留配置。   `dpkg -P <软件包名>`

列出指定软件包的内容        `dpkg -c <软件包名>`

提取指定软件包的安装信息。    `dpkg -l <软件包名>`

已安装软件包的文件清单        `dpkg -L <软件包名>`

已安装软件包的详细信息        `dpkg -s <软件包名>`

已安装软件包的包含关系        `dpkg -S <软件包名>`

---

3. apt&apt-get安装

这俩玩意差不多的东西，apt就是个高级的apt-get 用法一样，安装的时候类似于window的软件商店，直接在apt的官方源安装软件，来源可靠安全，安装的时候也能自动解决依赖问题（软件依赖可能冲突需要额外操作）

## 常用命令（必须sodu执行）：

更新软件包索引        `apt update`

升级软件包版本        `apt upgrade`

完全升级              `apt full-upgrade`

安装软件包            `apt install <软件名>`

移除软件包            `apt remove <软件名>`

自动移除未使用的包      `apt autoremove`

显示软件包            `apt list`

搜索包                `apt search`

查看包信息             `apt show`

其他与安装关系不大的未列出

---

4. docker安装
   
docker安装方式就是容器安装方式，完全不污染系统环境，不过需要对docker熟悉才方便使用，类似于虚拟机，但是原理可不是虚拟机那样，你可以理解为一个系统中抽取几个进程安装一个最小化的linux系统，然后在这个最小化的系统中安装你需要的软件。因为本来软件就需要进程来执行，只不过这次是在进程中加了一个托盘（即最小linux系统）托住了软件，既能方便的安装软件（无环境污染），又能安全运行（类似隔绝真实系统，侵入也只是个托盘）

docker命令不在此出列出，我们使用软件或者ui面板操作（废话，新手能直接用起来docker还看我这破文章）

我们选择使用1panel的安装面板（因为我有本地搭建web环境与数据库的需求，用这个最好，因为里面有store商店，如果你只是用docker安装软件，用docker官网的软件也可以）

---

5. appimage软件安装

这个安装方式是个好东西，什么命令也不用执行，什么操作也不需要安装，他是一个完全独立的软件，可以直接放在任何的linux系统中直接运行。不需要了直接删除文件软件就删除干净了。

唯一的缺点：这个东西不能直接放在dock（就是ubunt的那个大任务栏）中

---
   
6. 编译安装

当你看到这里的话，实际上已经不适合你了，因为软件的编译安装已经是最后的办法了使用软件的源代码对当前系统的硬件直接编译生成系统可以使用的软件。但是这个开源软件的最后一道防线，一般服务器可能用的较多或者开发者打包软件使用。

安装的具体步骤：

```
.$ tar zxvf XXXX.tar.gz (or tar jxvf XXXX.tar.bz2)  #解压缩软件源码包

.$ cd XXXX  #进入源码文件夹

.$ ./configure  #编译相关的准备工作 查看环境是否符合要求  ./configure –prefix=/opt/XXX 可以设置安装目录

.$ make  #make会根据Makefile中的规则调用相应的编译器 生成文件

.# make install  # 真正的安装过程 可能需要管理员权限，即sudo执行

```
---

# 1panel的安装

github地址：https://github.com/1Panel-dev/1Panel

安装命令：`curl -sSL https://resource.fit2cloud.com/1panel/package/quick_start.sh -o quick_start.sh && sudo bash quick_start.sh`

安装过程中会提示设置安装位置：默认为/opt
安装过程中会提示设置设置端口：随意设置（1-65535） 尽量不要使用低端口（1-1024）也不要和其他端口冲突
安装过程中会提示设置后台用户名：随便写（不写就随即生成）
安装过程中会提示设置后台密码：随便写（不写就随即生成）

安装完成后会提示web后台入口：

`http://目标服务器 IP 地址:目标端口/安全入口`



# 本地软件安装与卸载

1. 流程图软件-draw.io （snap安装-开源）
   安装命令：`snap install drawio`
   
   biu的一下就安装完毕了（不想写命令可以在ubuntu software中直接搜索下载）

2. 开发软件-vscode （deb安装-开源）https://github.com/microsoft/vscode

   github上只有源码，没有deb包，需要从vscode官网进入下载(别下rpm那是centos系列的)   https://code.visualstudio.com/
   
   安装命令：dpkg -i  deb文件
   
   友情提示，需要进入deb文件位置或者dpkg -i 把文件拖进取都性

3. 下载软件-motrix(开源deb或appimage) https://github.com/agalwood/Motrix

   github提供了appimage文件，官网提供多类型，包含deb、snap等  https://motrix.app/download （官网）
      
   snap安装： `snap install motrix`
   
   deb安装： `sudo dpkg -i Motrix_1.8.19_amd64.deb`  #这里下载的版本是1.8.19  amd64表示CPU架构是X86 
   
   appimage安装:  进入文件所在目录，运行 

   `chmod +x Motrix-1.8.19.AppImage`  #增加执行权限appimage文件需要先给运行权限
   
   `./Motrix-1.8.19.AppImage`         #运行程序
   
5. 办公软件-wps(deb安装-开源软件)
   

6. 脑图软件-freeplane（snap安装-开源）https://github.com/freeplane/freeplane

   snap安装：`snap install freeplane`  #ubuntu server商店也有   

7. 绘图软件-kolourpaint（snap安装-开源）https://github.com/KDE/kolourpaint

   snap安装：`snap install kolourpaint`  #ubuntu server商店也有  

8. 动态壁纸软件-fantascene-dynamic-wallpaper（）https://github.com/enjoyteach/fantascene-dynamic-wallpaper

   官方提供的下载地址：https://software.opensuse.org//download.html?project=home%3Aliuminghang&package=fantascene-dynamic-wallpaper  #readme中书写的

   下载符合系统的deb安装包：fantascene-dynamic-wallpaper_1.6.4-1_amd64.deb

   deb安装：`dpkg -i fantascene-dynamic-wallpaper_1.6.4-1_amd64.deb`  #请确定已经在文件所在的目录下
   
10. 动态壁纸软件-komorebi（deb安装 - 开源）  https://github.com/cheesecakeufo/komorebi

      下载最新版komorebi：

       deb安装： sudo dpkg -i komorebi.deb

    本软件在22.04上有问题无法打开设置页面，不过没关系。。可以进入配置文件直接改  修改下  ~/.Komorebi.prop 的文件即可：


   ```
   [KomorebiProperties]
   WallpaperName=foggy_sunny_mountain   这个就是设置的壁纸名（不是文件名，是使用creater创建的）
   TimeTwentyFour=true
   ShowDesktopIcons=true
   EnableVideoWallpapers=true
   ````
   生成的壁纸保存在`/System/Resources/Komorebi` 之下，这下面就是creater创建的壁纸名 文件夹格式存在

12. 浏览器-chromium/chrome(snap/deb安装-开源)

    chromium是chrome的现行版，可以理解为新技术的测试基地，完全开源，不包含google组件大礼包，但是不会自动更新。
    
    snap安装:`snap install chromium`

    chrome谷歌浏览器，无需介绍

    下载deb安装包：https://www.google.cn/chrome/index.html

    deb安装：`sudo dpkg -i google-chrome-stable_current_amd64.deb` #请确定已经在文件所在的目录下
    
13. 虚拟机-VirtualBox(deb安装-开源)

    下载地址：https://www.virtualbox.org/wiki/Linux_Downloads

    deb安装：  `sudo dpkg -i virtualbox-7.0_7.0.14-161095~Ubuntu~jammy_amd64.deb` #请确定已经在文件所在的目录下

    snap安装：   `snap install  virtualbox`
    
14. 安卓虚拟机-Genymotion(bin安装-闭源)

      该软件可以在任何平台运行，但是软件是基于虚拟机VirtualBox，所以电脑中需要提前安装VirtualBox，软件可以模拟任何版本的android系统，并且分辨率品牌等都可以设置，适合开发者使用。

       该软件是基于x86版本设计的所以arm架构的软件无法运行，需要安装转换工具便可以随意运行。转换软件地址：https://github.com/m9rco/Genymotion_ARM_Translation/tree/master/package (根据版本自行下载)
    
   安装：

      1. 到官网下载对应版本的镜像文件：https://www.genymotion.com/product-desktop/download/  我们下载linux的.BIN文件

      2. 修改软件执行权限  ` chmod u+x genymotion-3.6.0-linux_x64.bin`

      3. 安装并制定安装路径 ` sudo ./genymotion-3.6.0-linux_x64.bin -d /opt`  出现提示按y同意

      4. 此时可以点击软件图表进入软件了（软件使用此处不做详解）

      5. 解决arm架构的软件安装问题：

         下载Genymotion_ARM_Translation ： https://github.com/m9rco/Genymotion_ARM_Translation/blob/master/package/Genymotion-ARM-Translation_for_9.0.zip 【注意：千万别复制链接，点下载按钮，我下在的安卓9转换，根据自己的需要下载版本】

         将下载的文件直接拖进Genymotion已经打开的安卓虚拟机窗口就行了。然后就可以使用arm架构的app！

         如果拖进提示复制到/sdcard/Download  说明没有成功执行转换工具，则需要使用adb连接虚拟机  执行` adb shell  /system/bin/flash-archive.sh /sdcard/Download/Genymotion-ARM-Translation_for_9.0.zip`

         adb如果执行报错，则说明电脑没有安装安卓SDK与tools。 安装SDK和tools操作连接

         安装完成继续执行命令理论上还可能报错：(这是因为Genymotion的设置未使用本地安装的SDK)

            ...
         
            [ERROR][unzip_archive_in_extract_dir] unzip failed: /sdcard/Download/Genymotion-

            ARM-Translation.zip
            
            {Result:KO};

            解决方法：1.打开Genymotion 2.进入设置 3.选择ADB选项 4.设置为 Use custom android SDK tools 5.点击BROWSE 选中本地安装的SDK目录

14. 大飞机-V2rayX (snap安装-开源)

    snap安装：`snap install V2rayX`
         
15.视频播放-Vlc

   snap安装：`snap install vlc`

         
15.音视频剪辑-Kdenlive

   snap安装：`snap install Kdenlive`


16.数据库管理-dbeaver  https://github.com/dbeaver/dbeaver

17 网络工具-网络工具

   snap安装：`snap install 网络工具`

18 markdown软件-notable

 snap安装：`snap install notable`

19. ssh管理-snowflake

snap安装：`snap install snowflake`

21. 系统清理 - bleachbit

snap安装：`snap install bleachbit`

22.系统备份-timeshift


apt安装：`sudo  apt  install timeshift`

23.音乐聚合-musicfree  https://github.com/maotoumao/MusicFreeDesktop



24.视频聚合-zyplayer   https://github.com/Hiram-Wong/ZyPlayer/releases



25.录制退流-obs

# 系统备份还原

