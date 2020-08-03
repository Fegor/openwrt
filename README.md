编译命令如下:
-
1. 首先装好 Ubuntu 64bit，推荐  Ubuntu  18 LTS x64，打开控制面板-程序-启动或关闭windows程序-拉到最下面-选中适用于Linux的windows子系统，然后重启，再到windows store里搜索unbuntu，安装ubuntu18.

2. 打开ubuntu，可能会要求设置新的用户名和密码，设置即可。然后启动， 命令行输入 `sudo apt-get update` ，然后输入
`
sudo apt-get -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch python3.5 python2.7 unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint device-tree-compiler g++-multilib antlr3 gperf
`

3. `git clone -b dev-19.07 https://github.com/Lienol/openwrt op19` 命令下载好源代码，然后 `cd op19` 进入目录

4. `cd package`
   `git clone https://github.com/kenzok8/openwrt-packages.git`
       

6. ```bash
   ./scripts/feeds clean
   ./scripts/feeds update -a
   ./scripts/feeds install -a
   make menuconfig
   ```

//7. `make -j8 download V=s` 下载dl库（国内请尽量全局科学上网）

7. 上面的目的是获得一个.config文件，里面可以包含ssr和passwall。文件路径是C:\Users\用户名\AppData\Local\Packages\CanonicalGroupLimited.Ubuntu20.04onWindows_79rhkp1fndgsc\LocalState\rootfs\home\用户名\op19

8. 编辑workflow文件为lienol的源
REPO_URL: https://github.com/Lienol/openwrt
REPO_BRANCH: dev-19.07
（以Lienol OpenWrt源码为例分支dev-master 激进；dev-19.07 OpenWrt官方平稳版；dev-lean-lede lean的源码）。

9. 到https://p3terx.com/archives/build-openwrt-with-github-actions.html
（参考https://mianao.info/2020/05/05/%E7%BC%96%E8%AF%91%E6%9B%B4%E6%96%B0OpenWrt-PassWall%E5%92%8CSSR-plus%E6%8F%92%E4%BB%B6）
上传.config文件即开始编译，去actions里面查看进度。



//6. 输入 `make -j1 V=s` （-j1 后面是线程数。第一次编译推荐用单线程）即可开始编译你要的固件了。

//6. 编译完成后输出路径：op-19/bin/targets

你可以自由使用，但源码编译二次发布请注明我的 GitHub 仓库链接。谢谢合作！
 
 -----------------------------------------------------
 
My app source code: https://github.com/Lienol/openwrt-package

This is the buildsystem for the OpenWrt Linux distribution.

To build your own firmware you need a Linux, BSD or MacOSX system (case
sensitive filesystem required). Cygwin is unsupported because of the lack
of a case sensitive file system.

You need gcc, binutils, bzip2, flex, python, perl, make, find, grep, diff,
unzip, gawk, getopt, subversion, libz-dev and libc headers installed.

1. Run "./scripts/feeds update -a" to obtain all the latest package definitions
defined in feeds.conf / feeds.conf.default

2. Run "./scripts/feeds install -a" to install symlinks for all obtained
packages into package/feeds/

3. Run "make menuconfig" to select your preferred configuration for the
toolchain, target system & firmware packages.

4. Run "make" to build your firmware. This will download all sources, build
the cross-compile toolchain and then cross-compile the Linux kernel & all
chosen applications for your target system.

Sunshine!
	Your OpenWrt Community
	http://www.openwrt.org


