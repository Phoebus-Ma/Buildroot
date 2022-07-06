
---------------------------------------------------------------------

Buildroot用户手册

---------------------------------------------------------------------
---------------------------------------------------------------------

目录

 
I. 开始

- [1. 关于Buildroot](#chapter-1-关于buildroot)
- [2. 系统需求](#chapter-2-系统需求)

    - [2.1. 必选包](#21-必选包)
    - [2.2. 可选包](#22-可选包)

- [3. 获取Buildroot](#chapter-3-获取buildroot)
- [4. Buildroot快速开始](#chapter-4-buildroot快速开始)
- [5. 社区资源](#chapter-5-社区资源)

II. 用户指南

- [6. Buildroot配置](#chapter-6-buildroot配置)

    - [6.1. 交叉编译工具链](#61-交叉编译工具链)
    - [6.2. /dev 管理](#62-dev管理)
    - [6.3. init system](#63-init-system)

- [7. 配置其它组件](#chapter-7-配置其它组件)
- [8. Buildroot一般用法](#chapter-8-buildroot一般用法)

    - [8.1. make tips](#81-make-tips)
    - [8.2. 了解什么时候需要完全重建](#82-了解什么时候需要完全重建)
    - [8.3. 了解如何重新构建包](#83-了解如何重新构建包)
    - [8.4. 离线构建](#84-离线构建)
    - [8.5. Building out-of-tree](#85-building-out-of-tree)
    - [8.6. 环境变量](#86-环境变量)
    - [8.7. 有效地处理文件系统映像](#87-有效地处理文件系统映像)
    - [8.8. 包的详细信息](#88-包的详细信息)
    - [8.9. 绘制包之间的依赖关系图](#89-绘制包之间的依赖关系图)
    - [8.10. 绘制构建持续时间图](#810-绘制构建持续时间图)
    - [8.11. 绘制包对文件系统大小的贡献](#811-绘制包对文件系统大小的贡献)
    - [8.12. 顶层并行构建](#812-顶层并行构建)
    - [8.13. 与Eclipse集成](#813-与eclipse集成)
    - [8.14. 高级用法](#814-高级用法)

- [9. 具体项目的定制](#chapter-9-具体项目的定制)

    - [9.1. 推荐的目录结构](#91-推荐的目录结构)
    - [9.2. 将定制保持在Buildroot之外](#92-将定制保持在buildroot之外)
    - [9.3. 存储Buildroot配置](#93-存储buildroot配置)
    - [9.4. 存放其他组件的配置](#94-存放其他组件的配置)
    - [9.5. 定制生成的目标文件系统](#95-定制生成的目标文件系统)
    - [9.6. 添加自定义用户帐户](#96-添加自定义用户帐户)
    - [9.7. 创建映像后的自定义](#97-创建映像后的自定义)
    - [9.8. 添加特定项目的补丁](#98-添加特定项目的补丁)
    - [9.9. 添加特定项目包](#99-添加特定项目包)
    - [9.10. 存储特定于项目的自定义快速指南](#910-存储特定于项目的自定义的快速指南)

- [10. 在Buildroot中使用SELinux](#chapter-10-在buildroot中使用selinux)

    - [10.1. 启用SELinux支持](#101-启用selinux支持)
    - [10.2. SELinux策略调整](#102-selinux策略调整)

- [11. 常见问题及故障处理](#chapter-11-常见问题及故障处理)

    - [11.1. 启动网络后启动挂起...](#111-启动网络后启动挂起)
    - [11.2. 为什么目标上没有编译器?](#112-为什么目标上没有编译器)
    - [11.3. 为什么目标上没有开发文件?](#113-为什么目标上没有开发文件)
    - [11.4. 为什么没有目标的记录?](#114-为什么没有目标的记录)
    - [11.5. 为什么有些包在Buildroot配置菜单中不可见?](#115-为什么有些包在buildroot配置菜单中不可见)
    - [11.6. 为什么不使用目标目录作为chroot目录?](#116-为什么不使用目标目录作为chroot目录)
    - [11.7. 为什么Buildroot不生成二进制包(.deb, .ipkg...)?](#117-为什么buildroot不生成二进制包debipkg)
    - [11.8. 如何加快构建过程?](#118-如何加快构建过程)

- [12. 已知问题](#chapter-12-已知的问题)
- [13. 法律通知和许可](#chapter-13-法律通知和许可)

    - [13.1. 遵循开源许可协议](#131-遵循开源许可协议)
    - [13.2. 符合Buildroot许可证](#132-符合buildroot许可证)

- [14. Buildroot之外](#chapter-14-buildroot之外)

    - [14.1. 引导生成的映像](#141-引导生成的映像)
    - [14.2. Chroot](#142-chroot)

III. 开发人员指南

- [15. Buildroot是如何工作的](#chapter-15-buildroot是如何工作的)
- [16. 编程风格](#chapter-16-编程风格)

    - [16.1. Config.in文件](#161-configin文件)
    - [16.2. .mk文件](#162-mk文件)
    - [16.3. genimage.cfg文件](#163-genimagecfg文件)
    - [16.4. 文档](#164-文档)
    - [16.5. 支持脚本](#165-支持脚本)

- [17. 添加对特定开发板的支持](#chapter-17-添加对特定开发板的支持)
- [18. 为Buildroot添加新包](#chapter-18-为buildroot添加新包)

    - [18.1. Package目录](#181-package目录)
    - [18.2. Config文件](#182-config文件)
    - [18.3. .mk文件](#183-mk文件)
    - [18.4. .hash文件](#184-hash文件)
    - [18.5. SNNfoo启动脚本](#185-snnfoo启动脚本)
    - [18.6. 具有特定构建系统的包的基础结构](#186-具有特定构建系统的包的基础结构)
    - [18.7. autotools-based包基础架构](#187-autotools-based包基础架构)
    - [18.8. CMake-based包基础架构](#188-cmake-based包基础架构)
    - [18.9. Python包基础架构](#189-python包基础架构)
    - [18.10. LuaRocks-based包基础架构](#1810-luarocks-based包基础架构)
    - [18.11. Perl/CPAN包基础架构](#1811-perlcpan包基础架构)
    - [18.12. virtual包基础架构](#1812-virtual包基础架构)
    - [18.13. 包的基础架构使用kconfig配置文件](#1813-包的基础架构使用kconfig配置文件)
    - [18.14. rebar-based包基础架构](#1814-rebar-based包基础架构)
    - [18.15. Waf-based包基础架构](#1815-waf-based包基础架构)
    - [18.16. Meson-based包基础架构](#1816-meson-based包基础架构)
    - [18.17. Cargo-based包基础架构](#1817-cargo-based包基础架构)
    - [18.18. Go包基础架构](#1818-go包基础架构)
    - [18.19. QMake-based包基础架构](#1819-qmake-based包基础架构)
    - [18.20. 构建内核模块的包的基础设施](#1820-构建内核模块的包的基础设施)
    - [18.21. asciidoc文档的基础架构](#1821-asciidoc文档的基础架构)
    - [18.22. 特定于Linux内核包的基础结构](#1822-特定于linux内核包的基础结构)
    - [18.23. 各种构建步骤中可用的钩子](#1823-各种构建步骤中可用的钩子)
    - [18.24. 与包的Gettext集成和交互](#1824-与包的gettext集成和交互)
    - [18.25. 提示和技巧](#1825-提示和技巧)
    - [18.26. 结论](#1826-结论)

- [19. 为包打补丁](#chapter-19-为包打补丁)

    - [19.1. 提供补丁](#191-提供补丁)
    - [19.2. 如何应用补丁](#192-如何应用补丁)
    - [19.3. 软件包补丁的格式和许可](#193-软件包补丁的格式和许可)
    - [19.4. 集成在Web上找到的补丁](#194-集成在web上找到的补丁)

- [20. 下载基础设施](#chapter-20-下载基础设施)
- [21. 调试Buildroot](#chapter-21-调试buildroot)
- [22. 为Buildroot贡献](#chapter-22-为buildroot贡献)

    - [22.1. 复制、分析和修复bugs](#221-复制分析和修复bugs)
    - [22.2. 分析和修复自动构建失败](#222-分析和修复自动构建失败)
    - [22.3. 检查和测试补丁](#223-检查和测试补丁)
    - [22.4. 完成待办事项列表中的任务](#224-完成待办事项列表中的任务)
    - [22.5. 提交补丁](#225-提交补丁)
    - [22.6. 报告issue/bugs或获得帮助](#226-报告issuebugs或获得帮助)
    - [22.7. 使用运行时测试框架](#227-使用运行时测试框架)

- [23. DEVELOPERS文件和get-developers](#chapter-23-developers文件和get-developers)
- [24. Release工程](#chapter-24-release工程)

    - [24.1. Releases](#241-releases)
    - [24.2. Development](#242-development)

IV. 附录

- [25. Makedev语法文档](#chapter-25-makedev语法文档)
- [26. Makeusers语法文档](#chapter-26-makeusers语法文档)

    - [26.1. 关于自动UIDs和GIDs的警告](#261-关于自动uids和gids的警告)

- [27. 从较老的Buildroot版本中迁移](#chapter-27-从较老的buildroot版本中迁移)

    - [27.1. 一般方法](#271-一般方法)
    - [27.2. 迁移到2016.11](#272-迁移到201611)
    - [27.3. 迁移到2017.08](#273-迁移到201708)

例子清单

18.1. 配置脚本: divine包
18.2. 配置脚本: imagemagick包:


---------------------------------------------------------------------

---------------------------------------------------------------------

Buildroot 2022.02.3手册生成在2022-06-19 10:20:13 UTC从git版本fb3c633cf2

Buildroot手册是由Buildroot开发人员编写的.它是在GNU通用公共许可证版本2下授权的.
请参阅Buildroot中的复制
[http://git.buildroot.org/buildroot/tree/COPYING?id=fb3c633cf24188b2300426201d1fe5578ebbf972]
该许可证全文的来源.

Copyright © 2004-2020 The Buildroot developers

Part I 开始

目录

1. 关于Buildroot
2. 系统需求

    2.1. 必选包
    2.2. 可选包

3. 获取Buildroot
4. Buildroot快速开始
5. 社区资源

## Chapter 1 关于Buildroot

Buildroot是一种工具,它使用交叉编译来简化和自动化为嵌入式系统构建完整Linux系统的过程.

为了实现这一点,Buildroot能够为目标生成交叉编译工具链、根文件系统、Linux内核映像和引导加载程序.
可以独立地将Buildroot用于这些选项的任意组合(例如,您可以使用现有的交叉编译工具链,并使用Buildroot只构建根文件系统).

Buildroot主要适用于使用嵌入式系统的人.嵌入式系统通常使用的处理器不是每个人在自己的PC上使用的常规x86处理器.
它们可以是PowerPC处理器、MIPS处理器、ARM处理器等.

Buildroot支持多种处理器及其变体;它还为几种现成的板提供了默认配置.
除此之外,许多第三方项目都是基于,或者在Buildroot之上开发他们的BSP^[1]或者SDK^[2].


---------------------------------------------------------------------

^[1] BSP: Board Support Package

^[2] SDK: Software Development Kit

## Chapter 2 系统需求

Buildroot设计用于在Linux系统上运行.

虽然Buildroot本身将构建编译所需的大多数主机包,但预计某些标准的Linux实用程序已经安装在主机系统上.
下面您将看到强制性包和可选包的概述(注意包的名称在不同发行版之间可能有所不同).

### 2.1 必选包

  * Build tools:

      + which
      + sed
      + make (version 3.81 or any later)
      + binutils
      + build-essential (only for Debian based systems)
      + gcc (version 4.8 or any later)
      + g++ (version 4.8 or any later)
      + bash
      + patch
      + gzip
      + bzip2
      + perl (version 5.8.7 or any later)
      + tar
      + cpio
      + unzip
      + rsync
      + file (must be in /usr/bin/file)
      + bc
  * Source fetching tools:

      + wget

### 2.2 可选包

  * 推荐的依赖关系:

    Buildroot中的一些特性或实用程序(如法律信息或图形生成工具)具有额外的依赖关系.
    尽管对于简单的构建来说,它们不是强制性的,但仍然强烈建议使用它们:

      + python (version 2.7 or any later)
  * 配置接口依赖关系:

    对于这些库,您需要同时安装运行时数据和开发数据,这些数据在许多发行版中是单独打包的.
    开发包通常带有-dev或-devel后缀.

      + ncurses5 to use the menuconfig interface
      + qt5 to use the xconfig interface
      + glib2, gtk2 and glade2 to use the gconfig interface
  * 源抓取工具:

    在官方树中,大多数包源都是使用wget从ftp、http或https位置获取的.一些包只能通过版本控制系统使用.
    此外,Buildroot还能够通过其他工具(如rsync或scp)下载源代码(请参阅Chapter 20,下载基础设施以获取
    更多详细信息).如果您使用这些方法中的任何一种来启用软件包,那么您将需要在主机系统上安装相应的工具:

      + bazaar
      + cvs
      + git
      + mercurial
      + rsync
      + scp
      + sftp
      + subversion
  * 与Java相关的包,如果需要为目标系统构建Java类路径:

      + The javac compiler
      + The jar tool
  * 文档生成工具:

      + asciidoc, version 8.6.3 or higher
      + w3m
      + python with the argparse module (automatically present in
        2.7+ and 3.2+)
      + dblatex (required for the pdf manual only)
  * 图生成工具:

      + graphviz to use graph-depends and <pkg>-graph-depends
      + python-matplotlib to use graph-build

## Chapter 3 获取Buildroot

Buildroot每3个月发布一次,分别在2月、5月、8月和11月.版本号的格式为YYYY.比如2013.02、2014.08.

释放滚动版本在: http://buildroot.org/downloads/.

为了方便您,可以在Buildroot源代码树的support/misc/Vagrantfile中获得
Vagrantfile[https://www.vagrantup.com/] ,以快速设置一个虚拟机,并提供启动所需的依赖项.

如果您想在Linux或Mac Os X上设置一个隔离的构建根环境,请将这一行粘贴到终端上:

```console
curl -O https://buildroot.org/downloads/Vagrantfile; vagrant up
```

如果您使用的是Windows,请将此粘贴到您的powershell中:

```console
(new-object System.Net.WebClient).DownloadFile(
"https://buildroot.org/downloads/Vagrantfile","Vagrantfile");
vagrant up
```

如果希望继续开发,可以使用每日快照或克隆Git存储库.有关更多详细信息,
请参阅Buildroot网站的下载页面[http://buildroot.org/download].

## Chapter 4 Buildroot快速开始

重要的是:您可以并且应该像普通用户那样构建一切.不需要作为root用户来配置和使用Buildroot.
通过以普通用户的身份运行所有命令,您可以保护您的系统在编译和安装期间不受包行为不良的影响.

使用Buildroot的第一步是创建一个配置.Buildroot有一个很好的配置工具,类似于您可以在Linux内核
[http://www.kernel.org/]或BusyBox [http://www.busybox.net/]中找到的配置工具..

从buildroot目录运行

```console
$ make menuconfig
```

原来的curses-based配置器,或

```console
$ make nconfig
```

新的curses-based配置器,或

```console
$ make xconfig
```

Qt-based配置器,或

```console
$ make gconfig
```

GTK-based配置器.

所有这些“make”命令都需要构建一个配置实用程序(包括接口),因此您可能需要为配置实用程序使用的相关库
安装“开发”包.请参考Chapter 2,系统需求了解更多细节,特别是可选需求,以获得您喜欢的接口的依赖关系.

对于配置工具中的每个菜单项,您可以找到描述该项目的相关帮助.有关某些具体配置方面的详细信息,
请参考Chapter 6, Buildroot configuration.

一旦一切都配置好了,配置工具就会生成一个包含整个配置的.config文件.这个文件将由顶级Makefile读取.

要启动构建过程,只需运行即可:

```console
$ make
```

默认情况下,Buildroot不支持顶级并行构建,因此不需要运行make -jN.然而,对于顶级并行构建有实验性的支持,
参见8.12节,顶层并行构建.

make命令通常会执行以下步骤:

  * 下载源文件(根据需要);
  * 配置、构建和安装交叉编译工具链,或者直接导入外部工具链;
  * 配置、构建和安装选定的目标包;
  * 如果选择的话,构建内核映像;
  * 如果选择的话,构建一个引导加载程序映像;
  * 以选定的格式创建一个根文件系统.

Buildroot输出存储在单个目录output/中.这个目录包含几个子目录:

  * Images/ 存储所有映像(内核映像、引导加载器和根文件系统映像)的地方.
    这些是需要放在目标系统上的文件.
  * build/ 中构建的所有组件(这包括Buildroot在主机上所需的工具和为目标编译的包).
    这个目录包含每个组件的一个子目录.
  * Host/ 包含为主机构建的工具和目标工具链的sysroot.前者是为主机编译的工具的安装,
    这些工具是正确执行Buildroot所需的,包括交叉编译工具链.后者是一个类似于根文件系统层次结构的层次结构.
    它包含所有用户空间包的头和库,这些包提供并安装其他包使用的库.然而,这个目录并不打算成为目标的根文件系统:
    它包含许多开发文件、未删除的二进制文件和库,这使得它对于嵌入式系统来说太大了.
    这些开发文件用于编译依赖于其他库的目标库和应用程序.
  * Staging/ 是指向host/内部的目标工具链sysroot的符号链接,它的存在是为了向后兼容.
  * target/,它包含了目标的几乎完整的根文件系统:除了/dev/中的设备文件,所需的一切都存在
    (Buildroot 不能创建它们,因为Buildroot 不以root身份运行,不希望以root身份运行).
    此外,它没有有正确的权限(例如,busybox二进制文件的setuid).因此,不应该在目标上使用此目录.
    相反,您应该使用images/目录中构建的一个图像.如果需要根文件系统的解压缩映像来通过NFS引导,
    那么使用images/中生成的tarball映像并将其解压缩为根.与staging/相比,target/只包含运行所选目标应用程序
    所需的文件和库:开发文件(头文件等)不存在,二进制文件被剥离.

这些命令是make menuconfig|nconfig|gconfig|xconfig和make,
它们允许轻松、快速地生成符合您需求的图像,包含您启用的所有特性和应用程序.

关于“make”命令用法的更多细节在8.1节make tips中给出.

## Chapter 5 社区资源

与任何开源项目一样,Buildroot在社区内外都有不同的共享信息的方式.

如果您正在寻求一些帮助,希望了解Buildroot或为项目做出贡献,这些方法中的每一种都可能使您感兴趣.

邮件列表

    Buildroot有一个用于讨论和开发的邮件列表.它是Buildroot用户和开发人员交互的主要方法.

    只允许Buildroot邮件列表的订阅者向此列表发送邮件.您可以通过邮件列表信息页面
    [http://lists.buildroot.org/mailman/listinfo/buildroot]订阅.

    发送到邮件列表的邮件也可以在邮件列表档案中找到,可以通过
    Mailman [http://lists.buildroot.org/pipermail/buildroot]或
    lore.kernel.org[https://lore.kernel.org/buildroot/]获得.

IRC

    IRC频道#buildroot [irc://irc.oftc.net/#buildroot]托管在OFTC [https://www.oftc.net/WebChat/]上.
    这是一个问快速问题或讨论特定话题的有用的地方.

    在IRC上寻求帮助时,请使用代码共享网站(如https://paste.ack.tf/)分享相关日志或代码片段.

    请注意,对于某些问题,发送到邮件列表可能更好,因为它将接触到更多的人,包括开发人员和用户.

Bug tracker
    Buildroot中的bug可以通过邮件列表报告,或者通过Buildroot bug跟踪器
    [https://bugs.buildroot.org/buglist.cgi?product=buildroot]报告.
    在创建bug报告之前,请参阅第22.6节,报告issues/bugs或获取帮助.
Wiki
    Buildroot wiki页面[http://elinux.org/Buildroot]托管在eLinux [http://elinux.org] wiki上.
    它包含一些有用的链接,过去和即将发生的事件的概述,以及一个TODO列表.
Patchwork

    Patchwork是一个基于web的补丁跟踪系统,旨在促进对开源项目的贡献和管理.
    已发送到邮件列表的补丁会被系统“捕获”,并出现在网页上.任何引用补丁的评论也会被添加到补丁页面.
    有关Patchwork的更多信息,请参见http://jk.ozlabs.org/projects/patchwork/.

    Buildroot Patchwork网站主要供Buildroot维护人员使用,以确保错过补丁.它也被Buildroot补丁审稿人使用
    (参见第22.3.1节,从Patchwork应用补丁).然而,由于该网站在一个干净简洁的web界面中暴露了
    补丁及其相应的评论,它对所有Buildroot开发人员都很有用.

    Buildroot补丁管理界面可以在http://patchwork.buildroot.org上找到.

Part II 用户指南

目录

6. Buildroot配置

    6.1. 交叉编译工具链
    6.2. /dev 管理
    6.3. init system

7. 配置其它组件
8. Buildroot一般用法

    8.1. make tips
    8.2. 了解什么时候需要完全重建
    8.3. 了解如何重新构建包
    8.4. 离线构建
    8.5. Building out-of-tree
    8.6. 环境变量
    8.7. 有效地处理文件系统映像
    8.8. 包的详细信息
    8.9. 绘制包之间的依赖关系图
    8.10. 绘制构建持续时间图
    8.11. 绘制包对文件系统大小的贡献
    8.12. 顶层并行构建
    8.13. 与Eclipse集成
    8.14. 高级用法

9. 具体项目的定制

    9.1. 推荐的目录结构
    9.2. 将定制保持在Buildroot之外
    9.3. 存储Buildroot配置
    9.4. 存放其他组件的配置
    9.5. 定制生成的目标文件系统
    9.6. 添加自定义用户帐户
    9.7. 创建映像后的自定义
    9.8. 添加特定项目的补丁
    9.9. 添加特定项目包
    9.10. 存储特定于项目的自定义快速指南

10. 在Buildroot中使用SELinux

    10.1. 启用SELinux支持
    10.2. SELinux策略调整

11. 常见问题及故障处理

    11.1. 启动网络后启动挂起...
    11.2. 为什么目标上没有编译器?
    11.3. 为什么目标上没有开发文件?
    11.4. 为什么没有目标的记录?
    11.5. 为什么有些包在Buildroot配置菜单中不可见?
    11.6. 为什么不使用目标目录作为chroot目录?
    11.7. 为什么Buildroot不生成二进制包(.deb, .ipkg...)?
    11.8. 如何加快构建过程?

12. 已知问题
13. 法律通知和许可

    13.1. 遵循开源许可协议
    13.2. 符合Buildroot许可证

14. Buildroot之外

    14.1. 引导生成的映像
    14.2. Chroot

## Chapter 6 Buildroot配置

make *config中的所有配置选项都有一个帮助文本,提供关于该选项的详细信息.

make *config命令还提供了一个搜索工具.阅读不同的前端菜单中的帮助信息,了解如何使用它:

  * 在menuconfig中,搜索工具通过按 "/" 来调用;
  * 在xconfig中,按Ctrl + f调用搜索工具.

搜索结果显示匹配项的帮助消息.在menuconfig中,左列中的数字提供了对应条目的快捷方式.
只需输入这个数字就可以直接跳转到条目,或者在条目由于缺少依赖项而不可选的情况下跳转到包含的菜单.

尽管菜单结构和条目的帮助文本应该是充分不言自明的,但许多主题需要额外的解释,
而这些解释在帮助文本中不容易涉及,因此将在下面几节中讨论.

### 6.1 交叉编译工具链

编译工具链是允许您为系统编译代码的一组工具.它由一个编译器(在我们的例子中是gcc),二进制的utils,
如汇编器和链接器(在我们的例子中是binutils)和一个C标准库(例如GNU Libc 
[http://www.gnu.org/software/libc/libc.html], uClibc-ng [http://www.uclibc-ng.org/])组成.

安装在您的开发工作站上的系统当然已经有一个编译工具链,您可以使用它来编译在您的系统上运行的应用程序.
如果您使用的是PC,那么您的编译工具链在x86处理器上运行,并为x86处理器生成代码.在大多数Linux系统下,
编译工具链使用GNU libc (glibc)作为C标准库.这个编译工具链称为“主机编译工具链”.
运行它的机器和您工作的机器被称为"主机系统"^[3].

编译工具链由您的发行版提供,Buildroot与之无关(除了使用它构建交叉编译工具链和在开发主机上运行的其他工具之外).

如上所述,系统附带的编译工具链在上面运行,并为主机系统中的处理器生成代码.由于您的嵌入式系统具有不同的处理器,
因此需要一个交叉编译工具链—该编译工具链在您的主机系统上运行,但为您的目标系统(和目标处理器)生成代码.
例如,如果您的主机系统使用x86,而您的目标系统使用ARM,那么主机上的常规编译工具链在x86上运行并为x86生成代码,
而交叉编译工具链在x86上运行并为ARM生成代码.

Buildroot为交叉编译工具链提供了两种解决方案:

  * 内部工具链后端,在配置界面中称为Buildroot工具链.
  * 外部工具链后端,在配置接口中称为外部工具链.

使用Toolchain菜单中的Toolchain Type选项可以在这两种解决方案之间进行选择.
一旦选择了一个解决方案,就会出现许多配置选项,下面几节将详细介绍它们.

#### 6.1.1 内部工具链端

内部工具链后端是Buildroot在为目标嵌入式系统构建用户空间应用程序和库之前自己构建交叉编译工具链的后端.

后端支持几个C库:uClibc-ng [http://www.uclibc-ng.org], 
glibc [http://www.gnu.org/software/libc/libc.html]和musl [http://www.musl-libc.org].

一旦您选择了这个后端,就会出现许多选项.最重要的一些允许:

  * 更改用于构建工具链的Linux内核头文件的版本.这个项目值得做一些解释.在构建交叉编译工具链的过程中,
    正在构建C库.这个库提供用户空间应用程序和Linux内核之间的接口.为了知道如何与Linux内核“对话”,
    C库需要访问Linux内核头文件(即来自内核的.h文件),它定义了用户空间和内核之间的接口(系统调用,数据结构等).
    由于此接口是向后兼容的,因此用于构建工具链的Linux内核头文件的版本不需要与您打算在嵌入式系统上运行的
    Linux内核的版本完全匹配.它们只需要拥有与您打算运行的Linux内核版本相同或更老的版本.
    如果您使用的内核头文件比您在嵌入式系统上运行的Linux内核更新,那么C库可能使用的接口不是您的Linux内核提供的.
  * 更改GCC编译器、binutils和C库的版本.
  * 选择一些工具链选项(仅限uClibc):工具链是否应该具有RPC支持(主要用于NFS)、宽字符支持、
    区域设置支持(用于国际化)、c++支持或线程支持.根据您选择的选项,Buildroot菜单中可见的
    用户空间应用程序和库的数量会发生变化:许多应用程序和库需要启用某些工具链选项.当需要某个工具链
    选项来启用这些包时,大多数包都会显示注释.如果需要,您可以通过运行make uClibc -menuconfig
    来进一步细化uClibc配置.但是请注意,Buildroot中的所有包都针对Buildroot中绑定的默认uClibc配置进行测试:
    如果您通过从uClibc删除特性而偏离此配置,那么一些包可能不再构建.

值得注意的是,当这些选项中有一个选项被修改时,那么整个工具链和系统必须重建.第8.2节,了解何时全面重建是必要的.

此后台的优点:

  * 与Buildroot集成得很好
  * 快速,只构建必要的东西

此后台的缺点:

  * 在进行清理时需要重新构建工具链,这需要时间.如果您试图减少构建时间,请考虑使用External工具链后端.

#### 6.1.2 外部工具链后端

外部工具链后端允许使用现有的预构建的交叉编译工具链. Buildroot了解许多著名的交叉编译工具链
(从Linaro [http://www.linaro.org] for ARM, Sourcery CodeBench 
[http://www.mentor.com/embedded-software/sourcery-tools/sourcery-codebench/editions/lite-edition/]
for ARM, x86-64, PowerPC和MIPS,并能够自动下载它们,或者它可以指向一个定制的工具链,可以下载或本地安装.

然后,您有三种使用外部工具链的解决方案:

  * 使用预定义的外部工具链配置文件,并让Buildroot下载、提取和安装工具链.
    Buildroot已经知道一些CodeSourcery和Linaro工具链.只需从可用的工具链中选择工具链配置文件.
    这绝对是最简单的解决方案.
  * 使用预定义的外部工具链配置文件,但不需要让Buildroot下载并提取工具链,
    而是可以告诉Buildroot您的工具链已经安装在系统中的哪个位置.只需通过可用的工具链选择toolchain
    中的工具链配置文件,取消选择“自动下载工具链”,并在toolchain路径文本条目中填写交叉编译工具链的路径.
  * 使用完全自定义的外部工具链.这对于使用crosstool-NG或Buildroot本身生成的工具链特别有用.
    为此,在“工具链”列表中选择“自定义工具链”解决方案.您需要填充Toolchain路径、Toolchain前缀
    和External Toolchain C库选项.然后,您必须告诉Buildroot您的外部工具链支持什么.
    如果您的外部工具链使用glibc库,您只需要告诉您的工具链是否支持c++,以及它是否具有内置RPC支持.
    如果您的外部工具链使用uClibc库,那么您必须告诉Buildroot它是否支持RPC、宽字符、区域设置、程序调用、
    线程和c++.在执行的开始,Buildroot将告诉您所选选项是否与工具链配置不匹配.

我们的外部工具链支持已经通过CodeSourcery和Linaro的工具链、crosstool-NG [http://crosstool-ng.org]
生成的工具链以及Buildroot本身生成的工具链进行了测试.通常,所有支持sysroot特性的工具链都应该可以工作.
如果没有,请毫不犹豫地联系开发人员.

我们不支持由op固件或Yocto生成的工具链或SDK,因为这些工具链不是纯工具链(也就是说,只有编译器、binutils、C和c++库).
相反,这些工具链附带了一组非常大的预先编译的库和程序.因此,Buildroot不能导入工具链的sysroot,
因为它将包含数百兆字节的预编译库,这些库通常是由Buildroot构建的.

我们也不支持使用发行版工具链(即由你的发行版安装的gcc /binutils/C库)作为工具链来为目标构建软件.
这是因为你的发行版工具链不是一个“纯”的工具链(例如,只与C/ c++库),所以我们不能正确地导入它到Buildroot构建环境.
因此,即使您正在为x86或x86_64目标构建系统,也必须使用Buildroot或crosstool-NG生成交叉编译工具链.

如果您想为您的项目生成一个自定义工具链,可以作为Buildroot的一个外部工具链,我们的建议是用Buildroot本身构建
(参见第6.1.3节,构建一个具有Buildroot的外部工具链)或使用crosstoool-ng[http://crosstoool-ng.org].

这个后端的优点:

  * 允许使用众所周知且经过测试良好的交叉编译工具链.
  * 避免跨编译工具链的构建时间,在嵌入式Linux系统的整体构建时间中,这通常非常重要.

后端的缺点:

  * 如果您的预先构建的外部工具链有一个bug,可能很难从工具链供应商那里得到一个修复,
    除非您使用Buildroot或Crosstool-NG来构建您的外部工具链.

#### 6.1.3 使用Buildroot构建外部工具链

Buildroot内部工具链选项可用于创建外部工具链.
下面是构建内部工具链并将其打包以供Buildroot本身(或其他项目)重用的一系列步骤.

创建一个新的Buildroot配置,包含以下详细信息:

  * 为目标CPU架构选择适当的Target选项
  * 在“工具链”菜单中,保持“工具链”类型的Buildroot工具链的默认值,并根据需要配置工具链
  * 在“系统配置”菜单中,Init系统选择“None”,/bin/sh选择“None”
  * 在目标包菜单中,禁用BusyBox
  * 在Filesystem images菜单中,禁用tar根文件系统

然后,我们可以触发构建,并要求Buildroot生成SDK.这将方便地为我们生成一个包含工具链的tarball:

```console
make sdk
```

这将在$(O)/images中生成SDK tarball,其名称类似于arm-buildroot-linux-uclibcgnueabi_sdk-buildroot.tar.gz.
保存这个tarball,因为它现在是可以在其他Buildroot项目中作为外部工具链重用的工具链.

在其他的Buildroot项目中,在Toolchain菜单中:

  * “工具链类型”设置为“外部工具链”
  * “工具链”设置为“自定义工具链”
  * “工具链来源”设置为“需要下载安装的工具链”
  * “工具链URL”设置为 file:///path/to/your/sdk/tarball.tar.gz

6.1.3.1 外部工具链包装

当使用外部工具链时,Buildroot生成一个包装器程序,它透明地将适当的选项(根据配置)传递给外部工具链程序.
如果您需要调试这个包装器以准确地检查传递了哪些参数,您可以将环境变量BR2_DEBUG_WRAPPER设置为其中之一:

  * 0, 空或不设置:没有调试
  * 1: 在一行中跟踪所有参数
  * 2: 每行跟踪一个参数

### 6.2 /dev管理

在Linux系统中,/dev目录包含特殊的文件,称为设备文件,允许用户空间应用程序访问由Linux内核管理的硬件设备.
如果没有这些设备文件,您的用户空间应用程序将无法使用硬件设备,即使它们被Linux内核正确识别.

在系统配置、/dev管理,Buildroot提供了四种不同的解决方案来处理/dev目录:

  * 第一个解决方案是静态使用设备表.这是在Linux中处理设备文件的传统方法.使用这种方法,
    设备文件被持久地存储在根文件系统中(即,它们在重新启动时持续存在),当从系统中添加或删除硬件设备时,
    没有任何东西会自动创建和删除这些设备文件.因此,Buildroot使用一个设备表创建一组标准的设备文件,
    默认的设备表存储在Buildroot源代码中的system/device_table_dev.txt中.
    这个文件是在Buildroot生成最终的根文件系统映像时处理的,因此设备文件在output/target目录中不可见.
    BR2_ROOTFS_STATIC_DEVICE_TABLE选项允许更改Buildroot使用的默认设备表,或添加额外的设备表,
    以便Buildroot在构建期间创建额外的设备文件.因此,如果您使用这个方法,并且您的系统中缺少一个设备文件,
    您可以例如创建一个包含附加设备文件描述的board/<yourcompany>/<yourproject>/device_table_dev.txt文件,
    然后您可以将BR2_ROOTFS_STATIC_DEVICE_TABLE设置为system/device_table_dev.txt 
    board/<yourcompany>/<yourproject>/device_table_dev.txt.关于设备表文件格式的更多信息,
    请参见第25章,Makedev语法文档.
  * 第二个解决方案是动态使用devtmpfs.devtmpfs是在内核2.6.32中引入的Linux内核中的一个虚拟文件系统
    (如果您使用一个旧的内核,不可能使用此选项).当安装在/dev时,这个虚拟文件系统将自动使设备文件出现并消失,
    因为硬件设备被添加并从系统中删除.这个文件系统在重新设计中不是持久的:它是由内核动态填充的.
    使用devtmpfs需要启用以下内核配置选项:CONFIG_DEVTMPFS和CONFIG_DEVTMPFS_MOUNT.
    当Buildroot负责为嵌入式设备构建Linux内核时,它确保启用了这两个选项.但是,
    如果您在Buildroot之外构建Linux内核,那么您有责任启用这两个选项(如果您不这样做,您的Buildroot系统将不会启动).
  * 第三种解决方案是动态使用devtmpfs + mdev.这种方法还依赖于上面详细介绍的devtmpfs虚拟文件系统
    (因此在内核配置中启用CONFIG_DEVTMPFS和CONFIG_DEVTMPFS_MOUNT的要求仍然适用),
    但是在它的基础上添加了mdev用户空间实用程序.mdev是BusyBox的一个程序部分,每次添加或删除设备时,
    内核都会调用它.由于/etc/mdev.conf配置文件,可以对mdev进行配置,例如,设置设备文件的特定权限或所有权,
    在设备出现或消失时调用脚本或应用程序,等等.基本上,它允许用户空间对设备添加和删除事件做出反应.
    例如,Mdev可以用于在系统上出现设备时自动加载内核模块.如果您有需要固件的设备,Mdev也很重要,
    因为它将负责将固件内容推送到内核.Mdev是udev的一个轻量级实现(特性更少).
    有关mdev及其配置文件语法的详细信息,请参见http://git.busybox.net/busybox/tree/docs/mdev.txt.
  * 第四个解决方案是动态使用devtmpfs + eudev.这种方法也依赖于上面详细介绍的devtmpfs虚拟文件系统,
    但在其上添加了eudev用户空间守护进程.Eudev是一个在后台运行的守护进程,当系统添加或删除设备时,
    内核会调用它.它是比mdev更重量级的解决方案,但提供了更高的灵活性.eudev是udev的独立版本,
    udev是最初在大多数桌面Linux发行版中使用的用户空间守护进程,现在是Systemd的一部分.
    更多详细信息,请参见http://en.wikipedia.org/wiki/Udev.

Buildroot开发人员的建议是,首先使用devtmpfs唯一的解决方案,直到您有必要在设备被添加/删除设备时得到通知,
或者是否需要固件,在这种情况下,使用devtmpfs + mdev的情况通常是一个很好的解决方案.

注意,如果将systemd作为init系统,则由systemd提供的udev程序执行.

### 6.3 init system

init程序是内核启动的第一个用户空间程序(PID号为1),负责启动用户空间服务和程序
(例如:web服务器、图形应用程序、其他网络服务器等).

Buildroot允许使用三种不同类型的init系统,可以从系统配置、init系统中选择:

  * 第一个解决方案是BusyBox.在许多程序中,BusyBox实现了一个基本的init程序,
    这对于大多数嵌入式系统来说已经足够了.启用BR2_INIT_BUSYBOX将确保BusyBox构建
    并安装它的初始化程序.这是Buildroot中的默认解决方案.BusyBox初始化程序将在引导时
    读取/etc/inittab文件,以知道要做什么.该文件的语法可以在
    http://git.busybox.net/busybox/tree/examples/inittab中找到
    (注意BusyBox inittab语法是特殊的:不要使用Internet上随机的inittab文档来了解BusyBox inittab).
    Buildroot默认的“inittab”保存在“system/skeleton/etc/inittab”目录下.
    除了安装一些重要的文件系统之外,默认的inittab所做的主要工作是启动
    /etc/init.confd/rcS shell脚本,并启动一个getty程序(它提供一个登录提示).
  * 第二种解决方案是systemV.这个解决方案使用旧的传统sysvinit程序,
    打包在Buildroot package/sysvinit中.这是在大多数桌面Linux发行版中使用的解决方案,
    直到他们转向了最近的替代品,如Upstart或Systemd.sysvinit还可以使用inittab文件
    (它的语法与来自BusyBox的稍有不同).这个初始化解决方案安装的默认inittab位于包/sysvinit/inittab中.
  * 第三种解决方案是系统化.systemd是新一代的Linux init系统.它比传统的init程序做得
    更多:积极的并行化能力,使用套接字和D-Bus激活来启动服务,提供按需启动守护进程,
    使用Linux控制组跟踪进程,支持系统状态的快照和恢复等.systemd在相对复杂的嵌入式系统上很有用,
    例如需要D-Bus和服务之间通信的系统.值得注意的是systemd带来了相当多的大型依赖项:dbus、udev等.
    有关systemd的更多信息,请参见http://www.freedesktop.org/wiki/Software/systemd.

Buildroot开发人员推荐的解决方案是使用BusyBox init,
因为它对于大多数嵌入式系统来说已经足够了.Systemd可以用于更复杂的情况.


---------------------------------------------------------------------

^[3] 这个术语与GNU配置所使用的不同,在GNU配置中,主机是应用程序将在其上运行的机器(通常与目标相同).

## Chapter 7 配置其它组件

在尝试修改下面的任何组件之前,请确保已经配置了Buildroot本身,并启用了相应的包.

BusyBox

    如果已经有一个BusyBox配置文件,可以使用BR2_PACKAGE_BUSYBOX_CONFIG在
    Buildroot配置中直接指定该文件.否则,Buildroot将从默认的BusyBox配置文件启动.

    要对配置进行后续更改,请使用make BusyBox -menuconfig打开BusyBox配置编辑器.

    也可以通过环境变量指定BusyBox配置文件,但不推荐这样做.请参阅第8.6节,环境变量了解更多细节.

uClibc
    配置uClibc的方法与配置BusyBox的方法相同.指定现有配置文件的配置变量是BR2_UCLIBC_CONFIG.
    进行后续修改的命令是make uclibc-menuconfig.

Linux kernel

    如果已经有了内核配置文件,可以使用BR2_LINUX_KERNEL_USE_CUSTOM_CONFIG在Buildroot
    配置中直接指定该文件.

    如果您还没有内核配置文件,您可以使用BR2_LINUX_KERNEL_USE_DEFCONFIG在Buildroot配置中指定一个
    defconfig,或者使用BR2_LINUX_KERNEL_USE_CUSTOM_CONFIG创建一个空文件并指定它作为自定义配置文件.

    要对配置进行后续更改,请使用make Linux -menuconfig打开Linux配置编辑器.

Barebox
    Barebox的配置方法与Linux内核相同.对应的配置变量是BR2_TARGET_BAREBOX_USE_CUSTOM_CONFIG和
    BR2_TARGET_BAREBOX_USE_DEFCONFIG.要打开配置编辑器,请使用make barebox-menuconfig.

U-Boot
    U-Boot(版本2015.04或更新)的配置方法与Linux内核相同.对应的配置变量是BR2_TARGET_UBOOT_USE_CUSTOM_CONFIG
    和BR2_TARGET_UBOOT_USE_DEFCONFIG.要打开配置编辑器,使用make uboot-menuconfig.

## Chapter 8 Buildroot一般用法

### 8.1. make tips

这是一组帮助您充分利用Buildroot的技巧.

显示所有由make执行的命令:

```console
$ make V=1 <target>
```

显示defconfig的单板列表:

```console
$ make list-defconfigs
```

显示所有可用目标:

```console
$ make help
```

并不是所有的目标都是可用的,.config文件中的一些设置可能会隐藏一些目标:

  * busybox-menuconfig仅在启用busybox时有效;
  * Linux -menuconfig和Linux -savedefconfig只有在Linux开启的情况下才能工作;
  * uClibc -menuconfig仅在内部工具链后端选择uClibc C库时可用;
  * barebox-menuconfig和barebox-savedefconfig仅在启用barebox引导加载程序时工作.
  * uboot-menuconfig和uboot-savedefconfig只有在启用U-Boot引导加载程序
    且uboot构建系统设置为Kconfig时才能工作.

清除:当任何架构或工具链配置选项发生更改时,都需要显式清除.

删除所有构建产品(包括构建目录、主机、登台和目标树、映像和工具链):

```console
$ make clean
```

生成手册:当前的手册源位于docs/manual目录中.要生成手册:

```console
$ make manual-clean
$ make manual
```

手动输出将在output/docs/manual中生成.

注意

  * 构建文档需要一些工具(参见:第2.2节,可选包).

为新目标重置Buildroot:删除所有构建产品以及配置:

```console
$ make distclean
```

注意:如果启用了ccache,运行make clean或distclean不会清空Buildroot使用的编译器缓存.
要删除ccache,请参见8.14.3节,在Buildroot中使用ccache.

转储内部的make变量:可以转储已知要创建的变量及其值:

```console
$ make -s printvars VARS='VARIABLE1 VARIABLE2'
VARIABLE1=value_of_variable
VARIABLE2=value_of_variable
```

可以使用一些变量来调整输出:

  * VARS会将列表限制为名称匹配指定的make-patterns的变量-这个必须设置,否则不会打印
  * 如果QUOTED_VARS设置为YES,将单引号引用该值
  * RAW_VARS,如果设置为YES,将打印未展开的值

For example:

```console
$ make -s printvars VARS=BUSYBOX_%DEPENDENCIES
BUSYBOX_DEPENDENCIES=skeleton toolchain
BUSYBOX_FINAL_ALL_DEPENDENCIES=skeleton toolchain
BUSYBOX_FINAL_DEPENDENCIES=skeleton toolchain
BUSYBOX_FINAL_PATCH_DEPENDENCIES=
BUSYBOX_RDEPENDENCIES=ncurses util-linux
```

```console
$ make -s printvars VARS=BUSYBOX_%DEPENDENCIES QUOTED_VARS=YES
BUSYBOX_DEPENDENCIES='skeleton toolchain'
BUSYBOX_FINAL_ALL_DEPENDENCIES='skeleton toolchain'
BUSYBOX_FINAL_DEPENDENCIES='skeleton toolchain'
BUSYBOX_FINAL_PATCH_DEPENDENCIES=''
BUSYBOX_RDEPENDENCIES='ncurses util-linux'
```

```console
$ make -s printvars VARS=BUSYBOX_%DEPENDENCIES RAW_VARS=YES
BUSYBOX_DEPENDENCIES=skeleton toolchain
BUSYBOX_FINAL_ALL_DEPENDENCIES=$(sort $(BUSYBOX_FINAL_DEPENDENCIES) $(BUSYBOX_FINAL_PATCH_DEPENDENCIES))
BUSYBOX_FINAL_DEPENDENCIES=$(sort $(BUSYBOX_DEPENDENCIES))
BUSYBOX_FINAL_PATCH_DEPENDENCIES=$(sort $(BUSYBOX_PATCH_DEPENDENCIES))
BUSYBOX_RDEPENDENCIES=ncurses util-linux
```

例如,带引号的变量的输出可以在shell脚本中重用:

```console
$ eval $(make -s printvars VARS=BUSYBOX_DEPENDENCIES QUOTED_VARS=YES)
$ echo $BUSYBOX_DEPENDENCIES
skeleton toolchain
```

### 8.2 了解什么时候需要完全重建

当通过make menuconfig、make xconfig或其他配置工具更改系统配置时,
Buildroot不会试图检测应该重新构建系统的哪些部分.在某些情况下,
Buildroot应该重建整个系统,在某些情况下,只重建包的特定子集.
但是,以一种完全可靠的方式检测它是非常困难的,因此Buildroot的开发人员决定不尝试这样做.

相反,用户有责任知道何时需要完全重建.作为提示,这里有一些经验规则,可以帮助您理解如何使用Buildroot:

  * 当更改目标体系结构配置时,需要完全重新构建.例如,改变体系结构变体、二进制
    格式或浮点策略会对整个系统产生影响.
  * 当更改工具链配置时,通常需要完全重新构建.更改工具链配置通常涉及更改编译器
    版本、C库或其配置的类型,或其他一些基本配置项,这些更改会对整个系统产生影响.
  * 当向配置添加附加包时,不需要完全重新构建.Buildroot将检测到从未构建此包,并将构建它.
    但是,如果这个包是一个库,可以被已经构建的包有选择地使用,Buildroot将不会自动重新构建这些包.
    要么您知道应该重新构建哪些包,并且您可以手动重新构建它们,要么您应该进行完全的重新构建.
    例如,让我们假设您已经使用ctorrent包构建了一个系统,但没有使用openssl.您的系统可以工作,
    但是您意识到您希望在crtorrent中有SSL支持,因此您在Buildroot配置中启用了openssl包并重新启动构建.
    Buildroot会检测到应该构建openssl并且将会构建它,但它不会检测到应该重新构建crtorrent以从openssl中
    获益以添加openssl支持.您将要么做一个完整的重建,或重建crtorrent本身.
  * 当从配置中删除一个包时,Buildroot不会执行任何特殊操作.它不会从目标根文件系统或工具链sysroot中
    删除此包安装的文件.要清除此包,需要完全重新构建.但是,通常情况下,您并不需要立即删除这个包:
    您可以等到下一个午休时间再从头开始重新启动构建.
  * 当更改包的子选项时,不会自动重新生成包.在做出这样的更改之后,仅重建此包通常就足够了,
    除非启用包子选项向包添加了一些对已经构建的另一个包有用的特性.同样,Buildroot不跟踪包何时
    应该重新构建:一旦包被构建,它永远不会重新构建,除非明确地告诉它这样做.
  * 当对根文件系统框架进行更改时,需要完全重新构建.但是,当对根文件系统覆盖层进行更改时,
    进行后构建脚本或后图像脚本时,不需要完全重新构建:简单的make调用将考虑这些更改.
  * 当在FOO_DEPENDENCIES中列出的包被重新生成或删除时,包foo不会自动重新生成.
    例如,如果在FOO_DEPENDENCIES中使用FOO_DEPENDENCIES = bar列出了一个包栏,
    并且更改了这个包的配置,那么配置更改不会导致自动重新构建包foo.在这种情况下,
    您可能需要重新构建构建中的任何包,其中的参考条在它们的依赖项中,
    或者执行完全重新构建以确保任何依赖条的包是最新的.

一般来说,当您遇到构建错误,并且不确定所做的配置更改的潜在后果时,请进行完全的重新构建.
如果您得到相同的构建错误,那么您可以肯定该错误与包的部分重新构建无关,如果这个错误发生在
来自官方Buildroot的包上,请毫不犹豫地报告这个问题!随着您使用Buildroot的经验的发展,
您将逐步了解何时真正需要完整的重建,并且您将节省越来越多的时间.

作为参考,完全重建是通过运行实现的:

```console
$ make clean all
```

### 8.3 了解如何重新构建包

Buildroot用户最常见的问题之一是如何重新构建一个给定的包,
或者如何在不从头重新构建所有内容的情况下删除一个包.

如果不从头重新构建,则不支持删除包.这是因为Buildroot不跟踪哪个包在输出/staging和
输出/目标目录中安装了什么文件,或者根据另一个包的可用性,哪个包将以不同的方式编译.

从头重新构建单个包的最简单方法是在output/build中删除它的构建目录.然后,Buildroot将从头重新
提取、重新配置、重新编译和重新安装这个包.你可以用make <package>-dirclean命令要求buildroot这样做.

另一方面,如果您只想从包的编译步骤重新启动包的构建过程,您可以运行make <package>-rebuild.
它将重新启动包的编译和安装,但不是从头开始:它基本上是在包内重新执行make和make install,
因此它将只重建更改的文件.

如果希望从配置步骤重新启动包的构建过程,可以运行make <package>-reconfigure.
它将重新启动包的配置、编译和安装.

而<package>-rebuild表示<package>-重装和<package>-reconfigure表示<package>-rebuild,
这些目标和<package>只对该包执行操作,不要触发重新创建根文件系统映像.
如果需要重新创建根文件系统,应该另外运行make或make all.

在内部,Buildroot创建所谓的戳记文件来跟踪每个包已经完成了哪些构建步骤.它们存储在包构建目录中,
输出/build/<package>-<version>/,并命名为.stamp_<step-name>上面详细介绍的命令只是
简单地操作这些戳文件,以强制Buildroot重新启动包构建过程的一组特定步骤.

关于包专用的make目标的更多细节将在8.14.5节,包专用的make目标中解释.

### 8.4 离线构建

如果您打算做一个脱机构建,并且只是想要下载您之前在配置器
(menuconfig、nconfig、xconfig或gconfig)中选择的所有源,然后发布:

```console
$ make source
```

现在可以将dl目录的内容断开或复制到构建主机.

### 8.5 Building out-of-tree

默认情况下,Buildroot构建的所有东西都存储在Buildroot树的目录输出中.

Buildroot还支持使用类似于Linux内核的语法从树中构建.要使用它,添加O=<directory>到make命令行:

```console
$ make O=/tmp/build
```

Or:

```console
$ cd /tmp/build; make O=$PWD -C path/to/buildroot
```

所有输出文件将位于/tmp/build.如果O路径不存在,Buildroot将创建它.

注:O路径可以是一个绝对的或相对的路径,但如果它作为一个相对路径传递,
很重要的一点是,它被解释为相对于主Buildroot源目录,而不是当前工作目录.

当使用树的建造时,建造者.配置和临时文件也存储在输出目录中.
这意味着,只要使用唯一的输出目录,您就可以安全地运行多个构建,使用相同的源树.

为了方便使用,Buildroot在输出目录中生成一个Makefile包装器-所以在第一次运行之后,
您不再需要通过O=<...>和 -C <...>,只需运行(在输出目录中):

```console
$ make <target>
```

### 8.6 环境变量

当在环境中传递一些环境变量来创建或设置它们时,Buildroot也会执行这些变量:

  * HOSTCXX,主机c++编译器使用
  * HOSTCC, 宿主C编译器使用
  * UCLIBC_CONFIG_FILE=<path/to/.config>, uClibc配置文件的路径,如果正在构建内部工具链,
    则用于编译uClibc.注意,uClibc配置文件也可以从配置界面设置,因此可以通过Buildroot 
    .config文件;这是推荐的设置方式.
  * BUSYBOX_CONFIG_FILE=<path/to/.config>, BusyBox配置文件的路径.
    注意,BusyBox配置文件也可以从配置界面设置,因此可以通过Buildroot 
    .config文件;这是推荐的设置方式.
  * BR2_CCACHE_DIR来覆盖Buildroot在使用ccache时存储缓存文件的目录.
  * BR2_DL_DIR来覆盖Buildroot存储/检索下载文件的目录.注意,还可以从配置界面设置
    Buildroot下载目录,因此可以通过Buildroot .config文件进行设置.有关如何设置
    下载目录的详细信息,请参见8.14.4小节下载包的位置.
  * BR2_GRAPH_ALT,如果设置且非空,则在构建时图表中使用另一种颜色方案.
  * BR2_GRAPH_OUT设置生成图形的文件类型,可以是pdf(默认),也可以是png.
  * BR2_GRAPH_DEPS_OPTS将额外的选项传递给依赖图;请参阅8.9节,绘制包之间接受选项的依赖关系.
  * BR2_GRAPH_DOT_OPTS作为选项逐字传递给点实用程序,以绘制依赖关系图.
  * BR2_GRAPH_SIZE_OPTS将额外的选项传递给大小图;参见8.11节,
    绘制可接受选项的包对文件系统大小的贡献.

一个使用位于顶层目录和$HOME中的配置文件的示例:

```console
$ make UCLIBC_CONFIG_FILE=uClibc.config BUSYBOX_CONFIG_FILE=$HOME/bb.config
```

如果您想使用除默认gcc或g++以外的编译器在主机上构建helper-二进制文件,那么就这样做

```
$ make HOSTCXX=g++-4.3-HEAD HOSTCC=gcc-4.3-HEAD
```

### 8.7 有效地处理文件系统映像

文件系统映像可以变得相当大,这取决于您选择的文件系统、包的数量、是否提供了空闲空间.
然而,文件系统映像中的一些位置可能只是空的(例如,长期运行的0);这样的文件称为稀疏文件.

大多数工具可以有效地处理稀疏文件,并且只存储或写入稀疏文件中非空的部分.

例如:

  * tar接受-S选项,告诉它只存储稀疏文件的非零块:

      + tar cf archive.tar -S [files...] 将有效地存储稀疏文件在一个压缩
      + tar xf archive.tar -S 将有效地存储从压缩文件中提取的稀疏文件
  * cp accepts the --sparse=WHEN option (什么时候是自动的,从不还是总是):

      + cp --sparse=always source.file dest.file
      将使dest.file成为一个稀疏文件(如果源文件).文件有很长一段0

其他工具可能有类似的选择.请参阅各自的手册页.

如果需要存储文件系统映像(例如从一台机器传输到另一台机器),
或者需要发送映像(例如发送给Q&A团队),您可以使用稀疏文件.

但是请注意,当使用dd的稀疏模式时,将文件系统映像闪烁到设备可能会导致文件系统损坏
(例如,ext2文件系统的块位图可能被损坏;或者,如果您的文件系统中有稀疏文件,那么这些
部分在回读时可能不是全零).您应该只在构建机器上处理文件时使用稀疏文件,而不是在
将它们传输到将在目标上使用的实际设备时使用它们.

### 8.8 包的详细信息

Buildroot可以生成一个JSON简介,描述当前配置中启用的一组包,以及它们的依赖项、
许可证和其他元数据.这个JSON简介是使用show-info make目标生成的:

```console
make show-info
```

Buildroot还可以使用pkg-stats make target生成关于包的详细信息,如HTML和JSON输出.
这些细节包括已知的cve(安全漏洞)是否会影响当前配置中的包.它还显示这些包是否有更新的上游版本.

```console
make pkg-stats
```

### 8.9 绘制包之间的依赖关系图

Buildroot的工作之一是了解包之间的依赖关系,并确保它们以正确的顺序构建.
这些依赖关系有时会相当复杂,而且对于给定的系统,通常不容易理解Buildroot
为什么要在构建中引入这样或那样的包.

为了帮助理解依赖关系,从而更好地理解嵌入式Linux系统中不同组件的角色,
Buildroot能够生成依赖关系图.

要生成已编译的整个系统的依赖关系图,只需运行即可:

```console
make graph-depends
```

您将发现生成的图形在output/graphs/graph-depends.pdf.

如果您的系统非常大,依赖关系图可能太复杂,难以读取.因此,可以为一个给定的包生成依赖关系图:

```console
make <pkg>-graph-depends
```

您将发现生成的图形在output/graph/<pkg>-graph-depends.pdf.

注意,依赖关系图是使用Graphviz项目中的点工具生成的,必须在系统上安装该工具才能使用此特性.
在大多数发行版中,它以graphviz包的形式提供.

默认情况下,依赖关系图以PDF格式生成.但是,通过传递BR2_GRAPH_OUT环境变量,
可以切换到其他输出格式,如PNG、PostScript或SVG.支持dot工具-T选项支持的所有格式.

```console
BR2_GRAPH_OUT=svg make graph-depends
```

可以通过在BR2_GRAPH_DEPS_OPTS环境变量中设置选项来控制图依赖行为.可接受的选项有:

  * --depth N, -d N, 将依赖深度限制为N个级别.默认值0表示没有限制.
  * --stop-on PKG, -s PKG, PKG可以是一个实际的包名,一个glob,关键字virtual(在虚拟包上停止),
    或者关键字host(在主机包上停止).包仍然在图上,但是它的依赖项不在图上了.
  * --exclude PKG, -x PKG, like --stop-on, 但也从图中省略了PKG.
  * --transitive, --no-transitive, 绘制(或不绘制)传递依赖关系.默认值是不绘制传递依赖项.
  * --colors R,T,H, 用于绘制根包(R)、目标包(T)和主机包(H)的逗号分隔的颜色列表.
    默认为:浅蓝色、灰色、gainsboro.

```bash
BR2_GRAPH_DEPS_OPTS='-d 3 --no-transitive --colors=red,green,blue' make graph-depends
```

### 8.10 绘制构建持续时间图

当系统的构建需要很长时间时,了解哪些包的构建时间最长,
看看是否可以做些什么来加速构建,这有时是很有用的.为了帮助进行构建时间分析,
Buildroot收集每个包的每个步骤的构建时间,并允许从这些数据生成图表.

若要在生成后生成生成时间图,请运行:

```console
make graph-build
```

这将在输出/图形中生成一组文件:

  * build.hist-build.pdf, 每个包的构建时间的直方图,按构建顺序排列.
  * build.hist-duration.pdf, 每个包的构建时间的直方图,按持续时间排序(最长的优先).
  * build.hist-name.pdf, 每个包的构建时间直方图,按包名排序.
  * build.pie-packages.pdf, 每个包的构建时间的饼图.
  * build.pie-steps.pdf, 包构建过程的每一步所花费的全局时间的饼状图.

这个图形构建目标需要安装Python Matplotlib和Numpy库(在大多数发行版上是Python-Matplotlib和Python-Numpy),
如果你使用2.7以上的Python版本,也需要安装argparse模块(在大多数发行版上是Python-argparse).

默认情况下,图形的输出格式是PDF,但是可以使用BR2_GRAPH_OUT环境变量选择另一种格式.
唯一支持的其他格式是PNG:

```bash
BR2_GRAPH_OUT=png make graph-build
```

### 8.11 绘制包对文件系统大小的贡献

当目标系统增长时,了解每个Buildroot包对整个根文件系统大小的贡献大小有时很有用.
为了帮助进行这样的分析,Buildroot收集关于每个包安装的文件的数据,
并使用这些数据生成一个图表和详细描述不同包大小的CSV文件.

要在构建后生成这些数据,请运行:

```console
make graph-size
```

这将生成:

  * output/graphs/graph-size.pdf, 每个包对整个根文件系统大小的贡献的饼图.
  * output/graphs/package-size-stats.csv, 一个CSV文件,给出了每个包对整个根文件系统大小的贡献.
  * output/graphs/file-size-stats.csv, 一个CSV文件,它给出了每个已安装文件
    对其所属包的大小贡献,以及对整个文件系统大小的贡献.

这个图形大小的目标需要安装Python Matplotlib库(大多数发行版上是Python-Matplotlib),
如果您使用的Python版本高于2.7(大多数发行版上是Python -argparse),也需要安装argparse模块.

与持续时间图一样,支持BR2_GRAPH_OUT环境变量来调整输出文件格式.
关于这个环境变量的详细信息,请参见8.9节,绘制包之间的依赖关系.

另外,可以设置环境变量BR2_GRAPH_SIZE_OPTS来进一步控制生成的图.接受的选项:

  * --size-limit X, -l X, 将个人贡献低于X百分比的所有包分组到图中标记为Others的单个条目.
    默认情况下,X=0.01,这意味着每个贡献小于1%的包被分组在Others之下.接受的值在[0.0..1.0]范围内.
  * --iec, --binary, --si, --decimal, 使用IEC(二进制,1024次幂)或SI(十进制,1000次幂;默认)前缀.
  * --biggest-first, 按大小递减的顺序对包进行排序,而不是按大小递增的顺序.

请注意.收集的文件系统大小数据只有在完全清除重建之后才有意义.
在使用make图形大小之前,请务必运行make clean all.

要比较两个不同的Buildroot编译的根文件系统大小,例如在调整配置之后或切换到另一个Buildroot版本时,
请使用size-stats-compare脚本.它接受两个file-size-stats.csv文件(由make graph-size生成)作为输入.
有关更多细节,请参阅此脚本的帮助文本:

```bash
utils/size-stats-compare -h
```

### 8.12 顶层并行构建

请注意.本节讨论一个非常实验性的特性,该特性在一些普通情况下可以实现收支平衡.使用风险自负.

Buildroot一直能够在每个包的基础上使用并行构建:每个包都是由Buildroot使用make -jN
(或非基于make的构建系统的等效调用)构建的.并行度级别默认为cpu数量+1,
但可以使用BR2_JLEVEL配置选项进行调整.

然而,在2020.02之前,Buildroot一直在以一种连续的方式构建包:每个包一个接一个地构建,
包之间的构建没有并行化.截至2020.02,Buildroot对顶级并行构建提供了实验性支持,
通过并行构建没有依赖关系的包,可以显著节省构建时间.
然而,这个功能被标记为实验性的,在某些情况下是行不通的.

为了使用顶层并行构建,必须有一个:

 1. 在Buildroot配置中启用BR2_PER_PACKAGE_DIRECTORIES选项
 2. 启动Buildroot构建时使用make -jN

在内部,BR2_PER_PACKAGE_DIRECTORIES将启用一种称为每个包目录的机制,它将具有以下效果:

  * 与所有包通用的全局目标目录和全局主机目录不同,将使用每个包的目标目录和主机目录,
    分别为$(O)/per-package/<pkg>/target/和$(O)/per-package/<pkg>/host/.
    这些文件夹将从包依赖的相应文件夹中填充,在<pkg>构建.
    因此,编译器和所有其他工具将只能看到和访问由<pkg>.
  * 在构建的最后,将填充全局目标和主机目录,分别位于$(O)/target和$(O)/host中.
    这意味着在构建期间,这些文件夹将是空的,只有在构建的最后阶段才会填充它们.

### 8.13 与Eclipse集成

虽然一部分嵌入式Linux开发人员喜欢Vim或Emacs等经典文本编辑器和基于命令行的界面,
但许多其他嵌入式Linux开发人员喜欢更丰富的图形界面来完成他们的开发工作.
Eclipse是最流行的集成开发环境之一,为了简化Eclipse用户的开发工作,Buildroot集成了Eclipse.

我们与Eclipse的集成简化了构建在Buildroot系统上的应用程序和库的编译、远程执行和远程调试.
它没有将Buildroot配置和构建过程本身与Eclipse集成在一起.
因此,我们的Eclipse集成的典型使用模型是:

  * 用make menuconfig, make xconfig或任何其他配置界面来配置你的Buildroot系统.
  * 运行make来构建Buildroot系统.
  * 启动Eclipse来开发、执行和调试您自己的自定义应用程序和库,
    这些应用程序和库将依赖于Buildroot构建和安装的库.

在[https://github.com/mbats/eclipse-buildroot-bundle/wiki]
上详细介绍了Buildroot Eclipse集成安装过程和使用方法.

### 8.14 高级用法

#### 8.14.1 在Buildroot外使用生成的工具链

您可能希望为您的目标编译您自己的程序或其他没有在Buildroot中打包的软件.
为此,您可以使用Buildroot生成的工具链.

Buildroot生成的工具链默认位于输出/host/中.
使用它的最简单的方法是将输出/host/bin/添加到PATH环境变量,
然后使用ARCH-linux-gcc, ARCH-linux-objdump, ARCH-linux-ld等.

另外,Buildroot还可以通过运行make SDK命令将所有选定包的工具链和开发文件导出为SDK.
这将生成一个主机目录输出/host/内容的tarball,名为<TARGET-TUPLE>_sdk-builroot.tar.gz
(可以通过设置环境变量BR2_SDK_PREFIX来覆盖它),位于输出目录output/images/中.

然后,当应用程序开发人员希望开发尚未打包为Buildroot包的应用程序时,可以将这个tarball分发给他们.

在提取SDK tarball时,用户必须运行脚本relocate-sdk.sh(位于SDK的顶部目录),
以确保所有路径都更新为新的位置.

或者,如果您只是想准备SDK而不生成tarball(例如,因为您将只是移动主机目录,或将自己生成tarball),
Buildroot还允许您只使用make prepare-SDK来准备SDK,而不实际生成tarball.

为了方便起见,通过选择BR2_PACKAGE_HOST_ENVIRONMENT_SETUP选项,
可以在输出/host/中安装一个环境设置脚本,因此也可以安装在SDK中.这个脚本可以使用.
你的/sdk/path/environment-setup来导出许多环境变量,这些变量将帮助使用Buildroot sdk
交叉编译你的项目:path将包含sdk二进制文件,标准的自动工具变量将被定义为适当的值,
CONFIGURE_FLAGS将包含基本的./configure选项来交叉编译自动工具项目.它还提供了一些有用的命令.
但是请注意,一旦找到了这个脚本,环境的设置将只用于交叉编译,而不再用于本地编译.

#### 8.14.2 在Buildroot中使用gdb

Buildroot允许进行交叉调试,调试器在构建机器上运行,并与目标机上的gdbserver通信,以控制程序的执行.

为实现这一目标:

  * 如果您正在使用内部工具链(由Buildroot构建),您必须启用BR2_PACKAGE_HOST_GDB、
    BR2_PACKAGE_GDB和BR2_PACKAGE_GDB_SERVER.这将确保构建交叉gdb和gdbserver,
    并将gdbserver安装到目标上.
  * 如果您正在使用一个外部工具链,您应该启用BR2_TOOLCHAIN_EXTERNAL_GDB_SERVER_COPY,
    它将外部工具链中包含的gdbserver复制到目标.如果外部工具链没有跨gdb或gdbserver,
    也可以让Buildroot构建它们,方法是启用与内部工具链后端相同的选项.

现在,要开始调试一个名为foo的程序,您应该在目标上运行:

```console
gdbserver :2345 foo
```

这将导致gdbserver在TCP端口2345上侦听来自交叉gdb的连接.

然后,在主机上,应该使用以下命令行启动交叉gdb:

```console
<buildroot>/output/host/bin/<tuple>-gdb -ix <buildroot>/output/staging/usr/share/buildroot/gdbinit foo
```

当然,foo必须在当前目录中可用,用调试符号构建.通常,
您从构建foo的目录启动该命令(而不是从输出/target/开始,因为该目录中的二进制文件被剥离).

<buildroot>/output/staging/usr/share/buildroot/gdbinit文件将告诉交叉gdb在哪里找到目标的库.

最后,从交叉gdb连接到目标:

```console
(gdb) target remote <target ip address>:2345
```

#### 8.14.3 在Buildroot中使用ccache

Ccache [http://ccache.samba.org]是一个编译器缓存.它存储每个编译过程产生的目标文件,
并且能够通过使用预先存在的目标文件来跳过未来对相同源文件(使用相同的编译器和相同的参数)的编译.
当多次从头开始进行几乎相同的构建时,它可以很好地加快构建过程.

ccache支持集成在Buildroot中.你只需要在构建选项中启用编译器缓存.
这将自动构建ccache,并将其用于每个主机和目标编译.

缓存位于$HOME/.buildroot-ccache.它存储在Buildroot输出目录之外,
以便可以由单独的Buildroot构建共享.如果您想要删除缓存,只需删除这个目录.

通过运行make cache-stats,可以获得缓存的统计信息(大小、命中次数、未命中次数等).

make目标缓存选项和CCACHE_OPTIONS变量提供对ccache的更通用的访问.例如:

```bash
# set cache limit size
make CCACHE_OPTIONS="--max-size=5G" ccache-options

# zero statistics counters
make CCACHE_OPTIONS="--zero-stats" ccache-options
```

Ccache生成源文件和编译器选项的散列.如果编译器选项不同,则缓存的对象文件将不被使用.
但是,许多编译器选项都包含staging目录的绝对路径.因此,在不同的输出目录中构建将导致许多缓存丢失.

为了避免这个问题,buildroot有使用相对路径选项(BR2_CCACHE_USE_BASEDIR).
这将把指向输出目录内部的所有绝对路径重写为相对路径.因此,更改输出目录不再会导致缓存丢失.

相对路径的一个缺点是,它们最终也会成为目标文件中的相对路径.
因此,例如,调试器将不再找到该文件,除非您首先将cd切换到输出目录.

请参阅ccache手册的“在不同目录中编译”一节
[https://ccache.samba.org/manual.html#_compiling_in_different_directories],
了解关于重写绝对路径的更多细节.

#### 8.14.4 下载包的位置

Buildroot下载的各种tarball都存储在BR2_DL_DIR中,默认情况下是dl目录.
如果您希望保留Buildroot的完整版本(已知它与相关的tarball一起工作),
您可以创建这个目录的一个副本.这将允许您使用完全相同的版本重新生成工具链和目标文件系统.

如果您维护多个Buildroot树,那么最好有一个共享的下载位置.这可以通过将BR2_DL_DIR环境变量
指向一个目录来实现.如果设置了该选项,那么将覆盖Buildroot配置中的BR2_DL_DIR的值.
下面一行应该添加到<~/.bashrc>.

```bash
export BR2_DL_DIR=<shared download location>
```

还可以在.config文件中使用BR2_DL_DIR选项设置下载位置.
与.config文件中的大多数选项不同,该值被BR2_DL_DIR环境变量覆盖.

#### 8.14.5 包有关使目标

运行make <package>构建并安装特定的包及其依赖项.

对于依赖于Buildroot基础设施的包,有许多特殊的make目标,可以像这样独立调用它们:

```console
make <package>-<target>
```

包构建目标是(按照它们执行的顺序):

|command/target |Description                                                |
|-------------- | --------------------------------------------------------- |
|    source     |获取源代码(下载tarball,克隆源存储库,等等)                   |
|    depends    |生成并安装生成包所需的所有依赖项                              |
|    extract    |将源代码放在包构建目录中(提取tarball,复制源代码,等等)          |
|     patch     |应用补丁,如果有的话                                         |
|   configure   |如果有,请执行configure命令                                  |
|     build     |运行编译命令                                                |
|install-staging|目标包:如果需要,在暂存目录中运行包的安装                      |
|install-target |目标包:如果需要,在目标目录运行包的安装                        |
|    install    |目标包:运行之前的2条安装命令. 主机安装包:在主机目录下运行安装包  |

此外,还有一些其他有用的make目标:

|    command/target     |Description                                                                              |
|---------------------- | --------------------------------------------------------------------------------------- |
|     show-depends      |显示生成包所需的第一顺序依赖项                                                              |
|show-recursive-depends |递归地显示构建包所需的依赖项                                                                |
|     show-rdepends     |显示包(i)的一阶反向依赖项.e包直接依赖于它)                                                  |
|show-recursive-rdepends|递归地显示包的反向依赖关系(即直接或间接依赖它的包)                                            |
|     graph-depends     |在当前Buildroot配置的上下文中生成包的依赖关系图                                              |
|    graph-rdepends     |生成这个包反向依赖关系的图(即直接或间接依赖它的包)                                            |
|       dirclean        |删除整个包构建目录                                                                         |
|       reinstall       |重新运行安装命令                                                                           |
|        rebuild        |重新运行编译命令—只有在使用OVERRIDE_SRCDIR特性或直接在构建目录中修改文件时才有意义              |
|      reconfigure      |重新运行配置命令,然后重新构建—只有在使用OVERRIDE_SRCDIR特性或直接在构建目录中修改文件时才有意义 |

#### 8.14.6 在开发期间使用Buildroot

Buildroot的正常操作是下载一个tarball、解压它、配置、编译和安装在这个tarball中找到
的软件组件.在输出/build/<package>-<version>中提取源代码,这是一个临时目录:每当
使用make clean时,这个目录将被完全删除,并在下一次进行调用时重新创建.即使使用Git
或Subversion存储库作为包源代码的输入,Buildroot也会用它创建一个tarball,
然后像使用tarball时那样操作.

当Buildroot主要用作集成工具来构建和集成嵌入式Linux系统的所有组件时,
这种行为非常适合.但是,如果在开发系统的某些组件时使用Buildroot,
这种行为就不是很方便:相反,人们会希望对某个包的源代码做一个小更改,
并能够使用Buildroot快速重建系统.

直接在输出/构建/构建/<package>-<version>不是一个适当的解决方案,因为这个目录被删除了.

因此,Buildroot为这个用例提供了一个特定的机制:
<pkg>_OVERRIDE_SRCDIR机制.Buildroot读取一个覆盖文件,
该文件允许用户告诉Buildroot某些包的源位置.

覆盖文件的默认位置是$(CONFIG_DIR)/本地.通过BR2_PACKAGE_OVERRIDE_FILE配置选项
定义.$(CONFIG_DIR)是Buildroot的位置.配置文件,本地.mk在默认的情况下与.配置文件,这意味着:

  * 在树内构建的顶级Buildroot源目录中,当O=不使用时.
  * 在树下构建的树目录中即,当O = "使用".

如果需要不同的位置,那么可以通过BR2_PACKAGE_OVERRIDE_FILE配置选项来指定它.

在这个覆盖文件中,Buildroot希望找到表单的行:

```bash
<pkg1>_OVERRIDE_SRCDIR = /path/to/pkg1/sources
<pkg2>_OVERRIDE_SRCDIR = /path/to/pkg2/sources
```

For example:

```bash
LINUX_OVERRIDE_SRCDIR = /home/bob/linux/
BUSYBOX_OVERRIDE_SRCDIR = /home/bob/busybox/
```

当Buildroot发现对于一个给定的包,已经定义了<pkg>_OVERRIDE_SRCDIR时,
它将不再尝试下载、提取和修补该包.相反,它将直接使用指定目录中可用的源代码,
make clean不会触及该目录.这允许将Buildroot指向你自己的目录,可以由Git、Subversion
或任何其他版本控制系统管理.为了实现这一点,Buildroot将使用rsync将组件的源代码从指定
的<pkg>_OVERRIDE_SRCDIR复制到输出/build/<package>-custom/.

这种机制最好与make <pkg>-rebuild和make <pkg>-reconfigure目标一起使用.
一个make <pkg>-rebuild all序列将从<pkg>_OVERRIDE_SRCDIR rsync源代码
到输出/build/<package>-custom(多亏了rsync,只复制修改过的文件),
并仅重新启动这个包的构建过程.

在上面的linux包的示例中,开发人员可以让源代码更改/home/bob/linux然后运行:

```console
make linux-rebuild all
```

并在几秒钟内在输出/映像中获得更新的Linux内核映像.
类似地,可以对/home/bob/busybox中的BusyBox源代码进行更改:

```console
make busybox-rebuild all
```

输出/images中的根文件系统映像包含更新后的BusyBox.

大型项目的源代码树通常包含数百或数千个文件,这些文件在构建时并不需要,
但是使用rsync复制源代码的过程会变慢.可以选择定义
<pkg>_OVERRIDE_SRCDIR_RSYNC_EXCLUSIONS来跳过从源树中同步某些文件.
例如,当处理webkitgtk包时,下面的操作将从本地WebKit源代码树中排除测试和树内构建:

```bash
WEBKITGTK_OVERRIDE_SRCDIR = /home/bob/WebKit
WEBKITGTK_OVERRIDE_SRCDIR_RSYNC_EXCLUSIONS = \
        --exclude JSTests --exclude ManualTests --exclude PerformanceTests \
        --exclude WebDriverTests --exclude WebKitBuild --exclude WebKitLibraries \
        --exclude WebKit.xcworkspace --exclude Websites --exclude Examples
```

默认情况下,Buildroot会跳过VCS工件的同步(例如,.git和.svn目录).
有些包喜欢在构建期间使用这些VCS目录,例如用于自动确定版本信息的精确提交引用.
若要以降低速度为代价撤消此内置过滤,请将这些目录添加回去:

```bash
LINUX_OVERRIDE_SRCDIR_RSYNC_EXCLUSIONS = --include .git
```

## Chapter 9 具体项目的定制

对于给定的项目,您可能需要执行的典型操作是:

  * 配置Buildroot (包括构建选项和工具链、引导加载器、内核、包
    和文件系统映像类型选择)
  * 配置其它组件, 比如Linux kernel和BusyBox
  * 定制生成的目标文件系统

      + 在目标文件系统上添加或覆盖文件 (使用BR2_ROOTFS_OVERLAY)
      + 修改或删除目标文件系统上的文件 (使用BR2_ROOTFS_POST_BUILD_SCRIPT)
      + 在生成文件系统映像之前运行任意命令 (使用BR2_ROOTFS_POST_BUILD_SCRIPT)
      + 设置文件权限和所有权 (使用BR2_ROOTFS_DEVICE_TABLE)
      + 添加自定义设备节点 (使用BR2_ROOTFS_STATIC_DEVICE_TABLE)
  * 添加自定义用户帐户 (使用BR2_ROOTFS_USERS_TABLES)
  * 生成文件系统映像后运行任意命令 (使用BR2_ROOTFS_POST_IMAGE_SCRIPT)
  * 向一些包添加特定于项目的补丁 (使用BR2_GLOBAL_PATCH_DIR)
  * 添加特定项目包

关于此类项目特定自定义的重要注意事项:
请仔细考虑哪些更改确实是特定于项目的,哪些更改对项目之外的开发人员也有用.
Buildroot社区强烈推荐并鼓励对官方Buildroot项目的改进、包和板支持的上行.
当然,有时上游是不可能的,也不可取的,因为更改是高度特定的或专有的.

本章描述了如何在Buildroot中进行此类特定于项目的自定义,
以及如何以一种可重复构建相同映像的方式存储它们,即使在运行make clean之后.
通过遵循推荐的策略,您甚至可以使用相同的Buildroot树来构建多个不同的项目!

### 9.1 推荐的目录结构

在为项目定制Buildroot时,您将创建一个或多个项目特定的文件,这些文件需要存储在某个地方.
尽管这些文件中的大多数可以放置在任何位置,因为它们的路径要在Buildroot配置中指定,
但Buildroot开发人员建议使用本节中描述的特定目录结构.

与这个目录结构正交,您可以选择将这个结构本身放置在哪里:在Buildroot树中,
或者在它外面使用一个br2-external树.这两种选择都是有效的,选择取决于您.

+-- board/
|   +-- <company>/
|       +-- <boardname>/
|           +-- linux.config
|           +-- busybox.config
|           +-- <other configuration files>
|           +-- post_build.sh
|           +-- post_image.sh
|           +-- rootfs_overlay/
|           |   +-- etc/
|           |   +-- <some file>
|           +-- patches/
|               +-- foo/
|               |   +-- <some patch>
|               +-- libbar/
|                   +-- <some other patches>
|
+-- configs/
|   +-- <boardname>_defconfig
|
+-- package/
|   +-- <company>/
|       +-- Config.in (if not using a br2-external tree)
|       +-- <company>.mk (if not using a br2-external tree)
|       +-- package1/
|       |    +-- Config.in
|       |    +-- package1.mk
|       +-- package2/
|           +-- Config.in
|           +-- package2.mk
|
+-- Config.in (if using a br2-external tree)
+-- external.mk (if using a br2-external tree)
+-- external.desc (if using a br2-external tree)

上述文件的详细信息将在本章中进一步给出.

Note: 如果你选择将这个结构放置在Buildroot树之外,而是在br2-external树中,
<company>以及可能的<boardname>组件可能是多余的,可以忽略掉.

#### 9.1.1 实现分层定制

对于一个用户来说,有几个相关的项目在一定程度上需要相同的定制是很常见的.
与其为每个项目重复这些定制,不如建议使用分层定制方法,本节将对此进行解释.

几乎Buildroot中所有可用的定制方法,如构建后脚本和根文件系统覆盖,都接受以空格分隔的项列表.
指定的项总是按照从左到右的顺序处理.通过创建多个这样的项,一个用于普通定制,
另一个用于真正特定于项目的定制,您可以避免不必要的重复.每一层通常由board/<company>/
内部的单独目录体现.根据项目的不同,您甚至可以引入两个以上的层.

一个用户有两个定制层的示例目录结构:

+-- board/
    +-- <company>/
        +-- common/
        |   +-- post_build.sh
        |   +-- rootfs_overlay/
        |   |   +-- ...
        |   +-- patches/
        |       +-- ...
        |
        +-- fooboard/
            +-- linux.config
            +-- busybox.config
            +-- <other configuration files>
            +-- post_build.sh
            +-- rootfs_overlay/
            |   +-- ...
            +-- patches/
                +-- ...

例如,如果用户将BR2_GLOBAL_PATCH_DIR配置选项设置为:

```bash
BR2_GLOBAL_PATCH_DIR="board/<company>/common/patches board/<company>/fooboard/patches"
```

然后首先应用普通层的补丁,然后应用fooboard层的补丁.

### 9.2 将定制保持在Buildroot之外

正如在9.1节推荐的目录结构中已经简要提到的,您可以将特定于项目的自定义放置在两个位置:

  * 直接在Buildroot树中,通常使用版本控制系统中的分支来维护它们,
    这样就可以很容易地升级到新的Buildroot版本.
  * 在Buildroot树之外,使用br2外部机制.这种机制允许将包配方、
    板支持和配置文件保存在Buildroot树之外,同时仍然将它们很好地集成到构建逻辑中.
    我们称这个位置为br2-external树.本节解释如何使用br2-external机制,
    以及在br2-external树中提供什么.

通过将BR2_EXTERNAL make变量设置为要使用的br2-external树的路径,
可以告诉Buildroot使用一个或多个br2-external树.它可以传递给任何Buildroot make调用.
它会自动保存在隐藏的.br2-external文件中.Mk文件.因此,不需要在每次进行调用时传递BR2_EXTERNAL.
但是,它可以在任何时候通过传递新值来更改,也可以通过传递空值来删除.

Note. 到br2-external树的路径可以是绝对的,也可以是相对的.如果它作为相对路径传递,
一定要注意它是相对于主Buildroot源目录解释的,而不是相对于Buildroot输出目录.

Note: 如果使用Buildroot 2016.11之前的br2-external tree,
您需要转换它,然后才能使用它与Buildroot 2016.11向前.
请参阅第27.2节,迁移到2016.11来获取帮助.

一些例子:

```console
buildroot/ $ make BR2_EXTERNAL=/path/to/foo menuconfig
```

从现在开始,将使用/path/to/foo br2-external树的定义:

```console
buildroot/ $ make
buildroot/ $ make legal-info
```

我们可以在任何时候切换到另一个br2-external树:

```console
buildroot/ $ make BR2_EXTERNAL=/where/we/have/bar xconfig
```

我们还可以使用多个br2外部树:

```console
buildroot/ $ make BR2_EXTERNAL=/path/to/foo:/where/we/have/bar menuconfig
```

或禁用任何br2外部树的使用:

```console
buildroot/ $ make BR2_EXTERNAL= xconfig
```

#### 9.2.1 br2-external tree的布局

一个br2-external树必须至少包含这三个文件,以下章节将对此进行描述:

  * external.desc
  * external.mk
  * Config.in

除了这些强制文件之外,在br2-external树中可能还存在额外的可选内容,
比如config /或provider /目录.它们也将在接下来的章节中进行描述.

后面还将描述一个完整的示例br2-external树布局.

9.2.1.1 external.desc文件

该文件描述了br2-external树:该br2-external树的名称和描述.

该文件的格式是基于行的,每行以一个关键字开头,后面是冒号和一个或多个空格,
后面是分配给该关键字的值.目前有两个关键词被认可:

  * Name(强制)定义了br2-external树的名称.该名称必须只使用集合[A-Za-z0-9_]中的ASCII字符;
    禁止使用其他字符.Buildroot将变量BR2_EXTERNAL_$(NAME)_PATH设置为br2-external树的绝对路径,
    以便您可以使用它来引用您的br2-external树.这个变量在Kconfig中都是可用的,
    所以您可以使用它来生成Kconfig文件(见下文)和Makefile,这样您就可以使用它来包含
    其他Makefile(见下文)或引用br2-external树中的其他文件(如数据文件).

    Note: 因为可以同时使用多个br2-external树,Buildroot使用这个名称为每个树生成变量.
    这个名称用于标识你的br2-external树,所以尽量用一个真正描述你的br2-external树的名称,
    以便它相对唯一,这样它就不会与另一个br2-external树的另一个名称冲突,
    特别是如果你计划以某种方式与第三方共享你的br2-external树或使用第三方的br2-external树.

  * 可选的Desc为br2-external树提供了简短的描述.它应该适合一行,主要是自由形式(见下文),
    并在显示br2-external树的信息时使用(例如,在defconfig文件列表上方,或作为
    menuconfig中的提示符);因此,它应该相对简短(40个字符可能是一个不错的上限).
    这个描述可以在BR2_EXTERNAL_$(NAME)_DESC变量中找到.

名称和相应的BR2_EXTERNAL_$(NAME)_PATH变量的示例:

  * FOO â†’ BR2_EXTERNAL_FOO_PATH
  * BAR_42 â†’ BR2_EXTERNAL_BAR_42_PATH

在下面的示例中,假定名称设置为BAR_42.

Note: BR2_EXTERNAL_$(NAME)_PATH和BR2_EXTERNAL_$(NAME)_DESC都可以在Kconfig文件
和Makefiles文件中找到.它们也被导出到环境中,以便在构建后、映像后和fakeroot脚本中可用.

9.2.1.2 Config.in和external.mk

这些文件(可能每个都是空的)可以用来定义包的配方(例如foo/Config,
foo/foo.mk之类的包捆绑在Buildroot本身)或其他自定义配置选项或make逻辑.

Buildroot自动包含Config.in在每个br2-external树中使其出现在顶级配置菜单中,
并包括外部.每个br2外部树的Mk,以及makefile逻辑的其余部分.

它的主要用途是存储包配方.推荐的方法是编写一个Config.in在文件中:

```bash
source "$BR2_EXTERNAL_BAR_42_PATH/package/package1/Config.in"
source "$BR2_EXTERNAL_BAR_42_PATH/package/package2/Config.in"
```

然后,有一个external.mk文件:

```bash
include $(sort $(wildcard $(BR2_EXTERNAL_BAR_42_PATH)/package/*/*.mk))
```

然后在$(BR2_EXTERNAL_BAR_42_PATH)/package/package1和
$(BR2_EXTERNAL_BAR_42_PATH)/package/package2中创建正常的Buildroot包配方,
如第十八章中所述,向Buildroot添加新包.如果愿意,
还可以将名为<boardname>并对上述路径进行相应调整.

您还可以在Config中定义自定义配置选项.In和custom在"external.mk"中创建逻辑.

9.2.1.3 configs/文件夹

可以将Buildroot defconfig存储在br2-external树的config子目录中.
Buildroot将自动在make list-defconfig的输出中显示它们,并允许使用普通的
make <name>_defconfig命令来加载它们.它们将在make list-defconfigs输出中可见,
位于External configs标签下方,该标签包含定义它们的br2-external树的名称.

Note: 如果一个defconfig文件存在于多个br2-external树中,
那么将使用最后一个br2-external树中的一个.
因此,可以重写Buildroot或另一个br2-external树中绑定的defconfig.

9.2.1.4 provides/文件夹

对于某些包,Buildroot提供了两种(或更多)与api兼容的此类包实现的选择.
例如,可以选择libjpeg或jpeg-turbo;在openssl和libressl之间有一个;
有一个可以选择已知的、预先配置的工具链.

通过提供一组定义这些选项的文件,br2-external可以扩展这些选项:

  * provides/toolchains.in 定义预先配置的工具链,然后将在工具链选择中列出;
  * provides/jpeg.in 定义替代libjpeg实现;
  * provides/openssl.in 定义替代openssl实现;
  * provides/skeleton.in 定义替代框架实现;
  * provides/init.in 定义替代的初始化系统实现,这可以用来选择初始化的默认框架.

9.2.1.5 Free-form content

可以将所有与单板相关的配置文件存储在那里,例如内核配置、根文件系统覆盖
或Buildroot允许设置位置的任何其他配置文件(通过使用R2_EXTERNAL_$(NAME)_PATH变量).
例如,您可以如下所示设置全局补丁目录、rootfs覆盖和内核配置文件的路径
(例如,通过运行make menuconfig并填写这些选项):

```bash
BR2_GLOBAL_PATCH_DIR=$(BR2_EXTERNAL_BAR_42_PATH)/patches/
BR2_ROOTFS_OVERLAY=$(BR2_EXTERNAL_BAR_42_PATH)/board/<boardname>/overlay/
BR2_LINUX_KERNEL_CUSTOM_CONFIG_FILE=$(BR2_EXTERNAL_BAR_42_PATH)/board/<boardname>/kernel.config
```

9.2.1.6 额外的Linux内核扩展

附加的Linux内核扩展(参见第18.22.2节,Linux -kernel-extensions)
可以通过将它们存储在br2-external树的根目录Linux/目录中来添加.

9.2.1.7 示例布局

下面是一个使用了br2-external所有特性的示例布局(示例内容显示在上面的文件中,
当它与解释br2-external树相关时;当然,这完全是为了说明而编造的):

```console
/path/to/br2-ext-tree/
  |- external.desc
  |     |name: BAR_42
  |     |desc: Example br2-external tree
  |     `----
  |
  |- Config.in
  |     |source "$BR2_EXTERNAL_BAR_42_PATH/toolchain/toolchain-external-mine/Config.in.options"
  |     |source "$BR2_EXTERNAL_BAR_42_PATH/package/pkg-1/Config.in"
  |     |source "$BR2_EXTERNAL_BAR_42_PATH/package/pkg-2/Config.in"
  |     |source "$BR2_EXTERNAL_BAR_42_PATH/package/my-jpeg/Config.in"
  |     |
  |     |config BAR_42_FLASH_ADDR
  |     |    hex "my-board flash address"
  |     |    default 0x10AD
  |     `----
  |
  |- external.mk
  |     |include $(sort $(wildcard $(BR2_EXTERNAL_BAR_42_PATH)/package/*/*.mk))
  |     |include $(sort $(wildcard $(BR2_EXTERNAL_BAR_42_PATH)/toolchain/*/*.mk))
  |     |
  |     |flash-my-board:
  |     |    $(BR2_EXTERNAL_BAR_42_PATH)/board/my-board/flash-image \
  |     |        --image $(BINARIES_DIR)/image.bin \
  |     |        --address $(BAR_42_FLASH_ADDR)
  |     `----
  |
  |- package/pkg-1/Config.in
  |     |config BR2_PACKAGE_PKG_1
  |     |    bool "pkg-1"
  |     |    help
  |     |      Some help about pkg-1
  |     `----
  |- package/pkg-1/pkg-1.hash
  |- package/pkg-1/pkg-1.mk
  |     |PKG_1_VERSION = 1.2.3
  |     |PKG_1_SITE = /some/where/to/get/pkg-1
  |     |PKG_1_LICENSE = blabla
  |     |
  |     |define PKG_1_INSTALL_INIT_SYSV
  |     |    $(INSTALL) -D -m 0755 $(PKG_1_PKGDIR)/S99my-daemon \
  |     |                          $(TARGET_DIR)/etc/init.d/S99my-daemon
  |     |endef
  |     |
  |     |$(eval $(autotools-package))
  |     `----
  |- package/pkg-1/S99my-daemon
  |
  |- package/pkg-2/Config.in
  |- package/pkg-2/pkg-2.hash
  |- package/pkg-2/pkg-2.mk
  |
  |- provides/jpeg.in
  |     |config BR2_PACKAGE_MY_JPEG
  |     |    bool "my-jpeg"
  |     `----
  |- package/my-jpeg/Config.in
  |     |config BR2_PACKAGE_PROVIDES_JPEG
  |     |    default "my-jpeg" if BR2_PACKAGE_MY_JPEG
  |     `----
  |- package/my-jpeg/my-jpeg.mk
  |     |# This is a normal package .mk file
  |     |MY_JPEG_VERSION = 1.2.3
  |     |MY_JPEG_SITE = https://example.net/some/place
  |     |MY_JPEG_PROVIDES = jpeg
  |     |$(eval $(autotools-package))
  |     `----
  |
  |- provides/init.in
  |     |config BR2_INIT_MINE
  |     |    bool "my custom init"
  |     |    select BR2_PACKAGE_MY_INIT
  |     |    select BR2_PACKAGE_SKELETON_INIT_MINE if BR2_ROOTFS_SKELETON_DEFAULT
  |     `----
  |
  |- provides/skeleton.in
  |     |config BR2_ROOTFS_SKELETON_MINE
  |     |    bool "my custom skeleton"
  |     |    select BR2_PACKAGE_SKELETON_MINE
  |     `----
  |- package/skeleton-mine/Config.in
  |     |config BR2_PACKAGE_SKELETON_MINE
  |     |    bool
  |     |    select BR2_PACKAGE_HAS_SKELETON
  |     |
  |     |config BR2_PACKAGE_PROVIDES_SKELETON
  |     |    default "skeleton-mine" if BR2_PACKAGE_SKELETON_MINE
  |     `----
  |- package/skeleton-mine/skeleton-mine.mk
  |     |SKELETON_MINE_ADD_TOOLCHAIN_DEPENDENCY = NO
  |     |SKELETON_MINE_ADD_SKELETON_DEPENDENCY = NO
  |     |SKELETON_MINE_PROVIDES = skeleton
  |     |SKELETON_MINE_INSTALL_STAGING = YES
  |     |$(eval $(generic-package))
  |     `----
  |
  |- provides/toolchains.in
  |     |config BR2_TOOLCHAIN_EXTERNAL_MINE
  |     |    bool "my custom toolchain"
  |     |    depends on BR2_some_arch
  |     |    select BR2_INSTALL_LIBSTDCPP
  |     `----
  |- toolchain/toolchain-external-mine/Config.in.options
  |     |if BR2_TOOLCHAIN_EXTERNAL_MINE
  |     |config BR2_TOOLCHAIN_EXTERNAL_PREFIX
  |     |    default "arch-mine-linux-gnu"
  |     |config BR2_PACKAGE_PROVIDES_TOOLCHAIN_EXTERNAL
  |     |    default "toolchain-external-mine"
  |     |endif
  |     `----
  |- toolchain/toolchain-external-mine/toolchain-external-mine.mk
  |     |TOOLCHAIN_EXTERNAL_MINE_SITE = https://example.net/some/place
  |     |TOOLCHAIN_EXTERNAL_MINE_SOURCE = my-toolchain.tar.gz
  |     |$(eval $(toolchain-external-package))
  |     `----
  |
  |- linux/Config.ext.in
  |     |config BR2_LINUX_KERNEL_EXT_EXAMPLE_DRIVER
  |     |    bool "example-external-driver"
  |     |    help
  |     |      Example external driver
  |     |---
  |- linux/linux-ext-example-driver.mk
  |
  |- configs/my-board_defconfig
  |     |BR2_GLOBAL_PATCH_DIR="$(BR2_EXTERNAL_BAR_42_PATH)/patches/"
  |     |BR2_ROOTFS_OVERLAY="$(BR2_EXTERNAL_BAR_42_PATH)/board/my-board/overlay/"
  |     |BR2_ROOTFS_POST_IMAGE_SCRIPT="$(BR2_EXTERNAL_BAR_42_PATH)/board/my-board/post-image.sh"
  |     |BR2_LINUX_KERNEL_CUSTOM_CONFIG_FILE="$(BR2_EXTERNAL_BAR_42_PATH)/board/my-board/kernel.config"
  |     `----
  |
  |- patches/linux/0001-some-change.patch
  |- patches/linux/0002-some-other-change.patch
  |- patches/busybox/0001-fix-something.patch
  |
  |- board/my-board/kernel.config
  |- board/my-board/overlay/var/www/index.html
  |- board/my-board/overlay/var/www/my.css
  |- board/my-board/flash-image
  `- board/my-board/post-image.sh
        |#!/bin/sh
        |generate-my-binary-image \
        |    --root ${BINARIES_DIR}/rootfs.tar \
        |    --kernel ${BINARIES_DIR}/zImage \
        |    --dtb ${BINARIES_DIR}/my-board.dtb \
        |    --output ${BINARIES_DIR}/image.bin
        `----
```

然后在menuconfig中可以看到br2-external树(扩展了布局):

```console
External options  --->
    *** Example br2-external tree (in /path/to/br2-ext-tree/)
    [ ] pkg-1
    [ ] pkg-2
    (0x10AD) my-board flash address
```

如果你使用多个br2-external树,它看起来会像这样(展开布局,
第二个名为FOO_27,但在external.desc中没有desc:字段):

```console
External options  --->
    Example br2-external tree  --->
        *** Example br2-external tree (in /path/to/br2-ext-tree)
        [ ] pkg-1
        [ ] pkg-2
        (0x10AD) my-board flash address
    FOO_27  --->
        *** FOO_27 (in /path/to/another-br2-ext)
        [ ] foo
        [ ] bar
```

此外,jpeg提供程序将在jpeg选项中可见:

```console
Target packages  --->
    Libraries  --->
        Graphics  --->
            [*] jpeg support
                jpeg variant ()  --->
                    ( ) jpeg
                    ( ) jpeg-turbo
                        *** jpeg from: Example br2-external tree ***
                    (X) my-jpeg
                        *** jpeg from: FOO_27 ***
                    ( ) another-jpeg
```

工具链也是如此:

```console
Toolchain  --->
    Toolchain ()  --->
        ( ) Custom toolchain
            *** Toolchains from: Example br2-external tree ***
        (X) my custom toolchain
```

Note. toolchain/toolchain-external-mine/Config.in.选项不会出现在“工具链”菜单中.
它们必须显式地包含在br2-external的顶层Config.in,因此将出现在“外部选项”菜单中.

### 9.3 存储Buildroot配置

可以使用make savedefconfig命令存储Buildroot配置.

这将通过删除使用默认值的配置选项来删除Buildroot配置.
结果存储在一个名为defconfig的文件中.如果你想把它保存到另一个地方,
在Buildroot配置本身中改变BR2_DEFCONFIG选项,或者用
make savedefconfig BR2_DEFCONFIG=<path-to-defconfig>.

建议存储该defconfig的位置是configs/<boardname>_defconfig.
如果您遵循这个建议,配置将在make帮助中列出,并且可以通过运行
make <boardname>_defconfig再次进行设置.

或者,您可以将文件复制到任何其他位置,并使用
make defconfig BR2_DEFCONFIG=<path-to-defconfig-file>.

### 9.4 存放其他组件的配置

BusyBox、Linux内核、Barebox、U-Boot和uClibc的配置文件如果更改,也应该存储在一起.
对于这些组件,存在一个Buildroot配置选项来指向一个输入配置文件,例如
BR2_LINUX_KERNEL_CUSTOM_CONFIG_FILE.要存储它们的配置,
请将这些配置选项设置为您希望保存配置文件的路径,然后使用下面描述的helper目标来实际存储配置.

如9.1节推荐的目录结构中所述,存储这些配置文件的推荐路径是
board/<company>/<boardname>/foo.config.

确保在更改BR2_LINUX_KERNEL_CUSTOM_CONFIG_FILE等选项之前创建一个配置文件.
否则,Buildroot将尝试访问这个还不存在的配置文件,并将失败.
你可以通过运行make linux-menuconfig等来创建配置文件.

Buildroot提供了一些帮助器目标,使配置文件的保存更容易.

  * make linux-update-defconfig将linux配置保存到BR2_LINUX_KERNEL_CUSTOM_CONFIG_FILE
    指定的路径.它通过删除默认值来简化配置文件.但是,这只适用于2.6.33之后的内核.
    对于早期的内核,请使用make linux-update-config.
  * make busybox-update-config将busybox配置保存到BR2_PACKAGE_BUSYBOX_CONFIG指定的路径.
  * make uClibc -update-config保存uClibc配置到BR2_UCLIBC_CONFIG指定的路径.
  * make barebox-update-defconfig将barebox配置保存到
    BR2_TARGET_BAREBOX_CUSTOM_CONFIG_FILE指定的路径.
  * make uboot-update-defconfig保存U-Boot配置到
    BR2_TARGET_UBOOT_CUSTOM_CONFIG_FILE指定的路径.
  * 对于at91bootstrap3,不存在helper,所以必须手动将配置文件复制到
    BR2_TARGET_AT91BOOTSTRAP3_CUSTOM_CONFIG_FILE.

### 9.5 定制生成的目标文件系统

除了通过make *config更改配置之外,还有一些其他方法可以定制生成的目标文件系统.

推荐的两种方法是根文件系统覆盖和构建后脚本,它们可以共存.

```bash
Root filesystem overlays (BR2_ROOTFS_OVERLAY)

    A filesystem overlay is a tree of files that is copied directly
    over the target filesystem after it has been built. To enable
    this feature, set config option BR2_ROOTFS_OVERLAY (in the System
    configuration menu) to the root of the overlay. You can even
    specify multiple overlays, space-separated. If you specify a
    relative path, it will be relative to the root of the Buildroot
    tree. Hidden directories of version control systems, like .git,
    .svn, .hg, etc., files called .empty and files ending in ~ are
    excluded from the copy.

    When BR2_ROOTFS_MERGED_USR is enabled, then the overlay must not
    contain the /bin, /lib or /sbin directories, as Buildroot will
    create them as symbolic links to the relevant folders in /usr. In
    such a situation, should the overlay have any programs or
    libraries, they should be placed in /usr/bin, /usr/sbin and /usr/
    lib.

    As shown in Section 9.1, Recommended directory structure, the
    recommended path for this overlay is board/<company>/<boardname>/
    rootfs-overlay.

Post-build scripts (BR2_ROOTFS_POST_BUILD_SCRIPT)

    Post-build scripts are shell scripts called after Buildroot
    builds all the selected software, but before the rootfs images
    are assembled. To enable this feature, specify a space-separated
    list of post-build scripts in config option
    BR2_ROOTFS_POST_BUILD_SCRIPT (in the System configuration menu).
    If you specify a relative path, it will be relative to the root
    of the Buildroot tree.

    Using post-build scripts, you can remove or modify any file in
    your target filesystem. You should, however, use this feature
    with care. Whenever you find that a certain package generates
    wrong or unneeded files, you should fix that package rather than
    work around it with some post-build cleanup scripts.

    As shown in Section 9.1, Recommended directory structure, the
    recommended path for this script is board/<company>/<boardname>/
    post_build.sh.

    The post-build scripts are run with the main Buildroot tree as
    current working directory. The path to the target filesystem is
    passed as the first argument to each script. If the config option
    BR2_ROOTFS_POST_SCRIPT_ARGS is not empty, these arguments will be
    passed to the script too. All the scripts will be passed the
    exact same set of arguments, it is not possible to pass different
    sets of arguments to each script.

    In addition, you may also use these environment variables:

      + BR2_CONFIG: the path to the Buildroot .config file
      + CONFIG_DIR: the directory containing the .config file, and
        therefore the top-level Buildroot Makefile to use (which is
        correct for both in-tree and out-of-tree builds)
      + HOST_DIR, STAGING_DIR, TARGET_DIR: see Section 18.6.2,
        generic-package reference
      + BUILD_DIR: the directory where packages are extracted and
        built
      + BINARIES_DIR: the place where all binary files (aka images)
        are stored
      + BASE_DIR: the base output directory
```

下面将描述另外三种定制目标文件系统的方法,但不推荐使用它们.

```console
Direct modification of the target filesystem

    For temporary modifications, you can modify the target filesystem
    directly and rebuild the image. The target filesystem is
    available under output/target/. After making your changes, run
    make to rebuild the target filesystem image.

    This method allows you to do anything to the target filesystem,
    but if you need to clean your Buildroot tree using make clean,
    these changes will be lost. Such cleaning is necessary in several
    cases, refer to Section 8.2, Understanding when a full rebuild
    is necessary for details. This solution is therefore only useful
    for quick tests: changes do not survive the make clean command.
    Once you have validated your changes, you should make sure that
    they will persist after a make clean, using a root filesystem
    overlay or a post-build script.

Custom target skeleton (BR2_ROOTFS_SKELETON_CUSTOM)

    The root filesystem image is created from a target skeleton, on
    top of which all packages install their files. The skeleton is
    copied to the target directory output/target before any package
    is built and installed. The default target skeleton provides the
    standard Unix filesystem layout and some basic init scripts and
    configuration files.

    If the default skeleton (available under system/skeleton) does
    not match your needs, you would typically use a root filesystem
    overlay or post-build script to adapt it. However, if the default
    skeleton is entirely different than what you need, using a custom
    skeleton may be more suitable.

    To enable this feature, enable config option
    BR2_ROOTFS_SKELETON_CUSTOM and set
    BR2_ROOTFS_SKELETON_CUSTOM_PATH to the path of your custom
    skeleton. Both options are available in the System configuration
    menu. If you specify a relative path, it will be relative to the
    root of the Buildroot tree.

    Custom skeletons don't need to contain the /bin, /lib or /sbin
    directories, since they are created automatically during the
    build. When BR2_ROOTFS_MERGED_USR is enabled, then the custom
    skeleton must not contain the /bin, /lib or /sbin directories, as
    Buildroot will create them as symbolic links to the relevant
    folders in /usr. In such a situation, should the skeleton have
    any programs or libraries, they should be placed in /usr/bin, /
    usr/sbin and /usr/lib.

    This method is not recommended because it duplicates the entire
    skeleton, which prevents taking advantage of the fixes or
    improvements brought to the default skeleton in later Buildroot
    releases.

Post-fakeroot scripts (BR2_ROOTFS_POST_FAKEROOT_SCRIPT)

    When aggregating the final images, some parts of the process
    requires root rights: creating device nodes in /dev, setting
    permissions or ownership to files and directories To avoid
    requiring actual root rights, Buildroot uses fakeroot to simulate
    root rights. This is not a complete substitute for actually being
    root, but is enough for what Buildroot needs.

    Post-fakeroot scripts are shell scripts that are called at the 
    end of the fakeroot phase, right before the filesystem image
    generator is called. As such, they are called in the fakeroot
    context.

    Post-fakeroot scripts can be useful in case you need to tweak the
    filesystem to do modifications that are usually only available to
    the root user.

    Note: It is recommended to use the existing mechanisms to set
    file permissions or create entries in /dev (see Section 9.5.1,
    Setting file permissions and ownership and adding custom devices
    nodes) or to create users (see Section 9.6, Adding custom user
    accounts)

    Note: The difference between post-build scripts (above) and
    fakeroot scripts, is that post-build scripts are not called in
    the fakeroot context.

    Note: Using fakeroot is not an absolute substitute for actually
    being root. fakeroot only ever fakes the file access rights and
    types (regular, block-or-char device) and uid/gid; these are
    emulated in-memory.
```

#### 9.5.1 设置文件权限和归属,添加自定义设备节点

有时,需要在文件或设备节点上设置特定的权限或所有权.
例如,某些文件可能需要由root所有者.由于后构建脚本不作为根运行,
否则您不能在这里进行这些更改,除非您在后构建脚本中使用了一个显式的fakeroot.

相反,Buildroot提供了对所谓的权限表的支持.要使用此特性,
请将配置选项BR2_ROOTFS_DEVICE_TABLE设置为一个由空格分隔的权限表列表,
即遵循makedev语法的常规文本文件.

如果你使用的是静态设备表(即不使用devtmpfs, mdev,或(e)udev),
那么你可以使用相同的语法在所谓的设备表中添加设备节点.要使用此特性,
请将配置选项BR2_ROOTFS_STATIC_DEVICE_TABLE设置为以空格分隔的设备表列表.

如9.1节所示,推荐的目录结构,这些文件的推荐位置是board/<company>/<boardname>/.

需要注意的是,如果特定的权限或设备节点与特定的应用程序相关,
你应该在包的mk文件中设置变量FOO_PERMISSIONS和FOO_DEVICES(参见第18.6.2节,通用包引用).

### 9.6 添加自定义用户帐户

有时需要在目标系统中添加特定的用户.为了满足这一需求,Buildroot提供了对所谓的用户表的支持.
要使用此特性,请将配置选项BR2_ROOTFS_USERS_TABLES设置为一个由空格分隔的用户表列表,
即遵循makeusers语法的常规文本文件.

如9.1节所示,推荐的目录结构,这些文件的推荐位置是board/<company>/<boardname>/.

需要注意的是,如果自定义用户与特定的应用程序相关,
则应该在包的.mk文件中设置变量FOO_USERS(参见第18.6.2节,泛型包引用).

### 9.7 创建映像后的自定义

虽然构建后脚本(第9.5节,定制生成的目标文件系统)是在构建文件系统映像、
内核和引导加载程序之前运行的,但可以在创建所有映像之后使用构建后脚本执行一些特定的操作.

例如,可以使用映像后脚本在NFS服务器导出的位置自动提取根文件系统tarball,
或者创建一个捆绑根文件系统和内核映像的特殊固件映像,或者项目所需的任何其他自定义操作.

要启用该特性,请在配置选项BR2_ROOTFS_POST_IMAGE_SCRIPT(在系统配置菜单中)
中指定一个以空格分隔的后映像脚本列表.如果您指定一个相对路径,它将相对于Buildroot树的根.

就像后期构建脚本一样,后期映像脚本以主Buildroot树作为当前工作目录运行.
图像输出目录的路径作为每个脚本的第一个参数传递.如果配置选项BR2_ROOTFS_POST_SCRIPT_ARGS
不是空的,这些参数也将被传递给脚本.所有脚本都将传递完全相同的参数集,
不可能向每个脚本传递不同的参数集.

同样,就像构建后脚本一样,脚本可以访问环境变量BR2_CONFIG、HOST_DIR、
STAGING_DIR、TARGET_DIR、BUILD_DIR、BINARIES_DIR、CONFIG_DIR和BASE_DIR.

后映像脚本将作为执行Buildroot的用户执行,该用户通常不应该是根用户.因此,这些脚本
中任何需要root权限的操作都需要特殊处理(使用fakeroot或sudo),这是脚本开发人员的工作.

### 9.8 添加特定项目的补丁

有时,在Buildroot中提供的补丁基础上对包应用额外的补丁是很有用的.
例如,这可能用于支持项目中的自定义特性,或者在开发新体系结构时.

BR2_GLOBAL_PATCH_DIR配置选项可用于指定一个或多个包含包补丁的目录的以空格分隔的列表.

对于特定包<packagename>的特定版本<packageversion>,
补丁从BR2_GLOBAL_PATCH_DIR应用如下:

 1. 对于每个目录 - <global-patch-dir> - 存在于BR2_GLOBAL_PATCH_DIR中,
    一个<package-patch-dir>将被确定如下:

      + <global-patch-dir>/<packagename>/<packageversion>/ 如果目录存在.
      + 否则, <global-patch-dir>/<packagename> 如果目录存在.
 2. 然后补丁将从<package-patch-dir>如下:

      + 如果包目录下存在系列文件,则根据系列文件应用补丁;
      + 否则,匹配“*”的补丁文件.补丁按字母顺序应用.因此,为了确保它们以正确的顺序应用,
        强烈建议将补丁文件命名为:<number>-<description>.patch, <number>指的是申请顺序.

补丁对一个包的应用请参见19.2补丁的应用.

BR2_GLOBAL_PATCH_DIR选项是为包指定自定义补丁目录的首选方法.
它可以用来为buildroot中的任何包指定补丁目录.它也应该用于替代自定义补丁目录选项,
这些选项对于U-Boot和Barebox这样的包是可用的.
通过这样做,它将允许用户从一个顶级目录管理他们的补丁.

BR2_GLOBAL_PATCH_DIR作为指定自定义补丁的首选方法的例外是BR2_LINUX_KERNEL_PATCH.
应该使用BR2_LINUX_KERNEL_PATCH来指定可通过URL获得的内核补丁.
注意:BR2_LINUX_KERNEL_PATCH指定在BR2_GLOBAL_PATCH_DIR中可用的补丁之后应用的内核补丁,
因为它是在Linux包的后补丁钩子中完成的.

### 9.9 添加特定项目包

通常,任何新包都应该直接添加到包目录中,并提交给Buildroot上游项目.
如何向Buildroot中添加包在第18章,向Buildroot中添加新包中有详细的解释,
这里不再赘述.但是,您的项目可能需要一些不能上流的专有包.
本节将解释如何将此类项目特定的包保存在项目特定的目录中.

如9.1节所示,推荐的目录结构,项目特定包的推荐位置是package/<company>/.
如果你使用的是br2-external树特性(请参阅9.2节,将定制放在Buildroot之外),
建议将它们放在你的br2-external树中名为package/的子目录中.

但是,除非我们执行一些额外的步骤,否则Buildroot不会知道这个位置的包.
正如在第18章“向Buildroot添加新包”中所解释的,Buildroot中的一个包基本上由两个
文件组成:一个.mk文件(描述如何构建包)和一个Config.conf文件.文件中(描述此包的配置选项).

Buildroot将自动在包目录的第一级子目录中包含.mk文件(使用模式package/*/*.mk).
如果我们想要Buildroot包含来自更深层子目录(如package/<company>/package1/)的.mk文件,
那么我们只需在包含这些额外的.mk文件的一级子目录中添加一个.mk文件.
因此,创建一个文件包/<company>/<company>mkwith以下内容
(假设在package/<company>/下面只有一个额外的目录级别):

```bash
include $(sort $(wildcard package/<company>/*/*.mk))
```

配置.在文件中创建一个package/<company>/Config.in.其中包括配置.
在所有包的文件中.必须提供一个详尽的列表,因为在kconfig的源命令中不支持通配符.例如:

```bash
source "package/<company>/package1/Config.in"
source "package/<company>/package2/Config.in"
```

包含这个新文件package/<company>/Config.in.在从package/Config.in,
最好是在公司特定的菜单中,以便更容易地与未来的Buildroot版本合并.

如果使用一个br2-external树,请参考章节9.2,保持Buildroot之外的自定义来了解如何填充这些文件.

### 9.10 存储特定于项目的自定义的快速指南

在本章的前面,已经描述了进行项目特定定制的不同方法.
本节现在将通过提供如何存储特定于项目的自定义的分步说明来总结所有这些内容.
显然,可以跳过与项目无关的步骤.

 1. make menuconfig配置工具链、软件包和内核.
 2. make linux-menuconfig 要更新内核配置,与busybox、uclibc等其他配置类似.
 3. mkdir -p board/<manufacturer>/<boardname>
 4. 将以下选项设置为board/<manufacturer>/<boardname>/
    <package>.config (只要它们是相关的):

      + BR2_LINUX_KERNEL_CUSTOM_CONFIG_FILE
      + BR2_PACKAGE_BUSYBOX_CONFIG
      + BR2_UCLIBC_CONFIG
      + BR2_TARGET_AT91BOOTSTRAP3_CUSTOM_CONFIG_FILE
      + BR2_TARGET_BAREBOX_CUSTOM_CONFIG_FILE
      + BR2_TARGET_UBOOT_CUSTOM_CONFIG_FILE
 5. 写入配置文件:

      + make linux-update-defconfig
      + make busybox-update-config
      + make uclibc-update-config
      + cp <output>/build/at91bootstrap3-*/.config board/
        <manufacturer>/<boardname>/at91bootstrap3.config
      + make barebox-update-defconfig
      + make uboot-update-defconfig
 6. 创建board/<manufacturer>/<boardname>/rootfs-overlay/ and fill
    it with additional files you need on your rootfs, e.g. board/
    <manufacturer>/<boardname>/rootfs-overlay/etc/inittab. Set
    BR2_ROOTFS_OVERLAY to board/<manufacturer>/<boardname>/
    rootfs-overlay.
 7. 创建post-build脚本board/<manufacturer>/<boardname>/
    post_build.sh. Set BR2_ROOTFS_POST_BUILD_SCRIPT to board/
    <manufacturer>/<boardname>/post_build.sh
 8. 如果必须设置额外的setuid权限或必须创建设备节点, 创建board/<manufacturer>/<boardname>/
    device_table.txt and add that path to BR2_ROOTFS_DEVICE_TABLE.
 9. 如果必须创建额外的用户帐户,创建board/<manufacturer>/<boardname>/users_table.txt
    并将该路径添加到BR2_ROOTFS_USERS_TABLES.
10. 向某些包添加自定义补丁, 设置
    BR2_GLOBAL_PATCH_DIR to board/<manufacturer>/<boardname>/patches/
    and add your patches for each package in a subdirectory named
    after the package. Each patch should be called <packagename>-
    <num>-<description>.patch.
11. 特别是对于Linux内核,还存在BR2_LINUX_KERNEL_PATCH选项,其主要优点是它还可以
    从URL下载补丁.如果您不需要它,首选BR2_GLOBAL_PATCH_DIR.U-Boot, Barebox, 
    at91bootstrap和at91bootstrap3也有单独的选项,但它们没有提供任何比
    BR2_GLOBAL_PATCH_DIR的优势,可能会在未来被删除.
12. 如果您需要添加特定于项目的包, 创建package/<manufacturer>/
    and place your packages in that directory. Create
    an overall <manufacturer>.mk file that includes the .mk files of
    all your packages. Create an overall Config.in file that sources
    the Config.in files of all your packages. Include this Config.in
    file from Buildroot's package/Config.in file.
13. make savedefconfig 保存buildroot配置.
14. cp defconfig configs/<boardname>_defconfig

## Chapter 10 在Buildroot中使用SELinux

SELinux [https://selinuxproject.org]是一个执行访问控制策略的Linux内核安全模块.
除了传统的文件权限和访问控制列表外,SELinux还允许为用户或进程编写规则,
以访问资源的特定功能(文件、套接字).

SELinux有三种操作模式:

  * Disabled: the policy is not applied
  * Permissive: the policy is applied, and non-authorized actions are
    simply logged. This mode is often used for troubleshooting
    SELinux issues.
  * Enforcing: the policy is applied, and non-authorized actions are
    denied

In Buildroot the mode of operation is controlled by the
BR2_PACKAGE_REFPOLICY_POLICY_STATE_* configuration options. The Linux
kernel also has various configuration options that affect how SELinux
is enabled (see security/selinux/Kconfig in the Linux kernel
sources).

By default in Buildroot the SELinux policy is provided by the
upstream refpolicy [https://github.com/SELinuxProject/refpolicy]
project, enabled with BR2_PACKAGE_REFPOLICY.

### 10.1 启用SELinux支持

要在Buildroot生成的系统中正确支持SELinux,必须启用以下配置选项:

  * BR2_PACKAGE_LIBSELINUX
  * BR2_PACKAGE_REFPOLICY

In addition, your filesystem image format must support extended
attributes.

### 10.2 SELinux策略调整

SELinux重新策略包含可以在构建时启用或禁用的模块.每个模块提供许多SELinux规则.
在Buildroot中,默认情况下禁用非基础模块,并提供了几种启用此类模块的方法:

  * Packages can enable a list of SELinux modules within the
    refpolicy using the <packagename>_SELINUX_MODULES variable.
  * Packages can provide additional SELinux modules by putting them
    (.fc, .if and .te files) in package/<packagename>/selinux/.
  * Extra SELinux modules can be added in directories pointed by the
    BR2_REFPOLICY_EXTRA_MODULES_DIRS configuration option.
  * Additional modules in the refpolicy can be enabled if listed in
    the BR2_REFPOLICY_EXTRA_MODULES_DEPENDENCIES configuration
    option.

Buildroot also allows to completely override the refpolicy. This
allows to provide a full custom policy designed specifically for a
given system. When going this way, all of the above mechanisms are
disabled: no extra SElinux module is added to the policy, and all the
available modules within the custom policy are enabled and built into
the final binary policy. The custom policy must be a fork of the
official refpolicy [https://github.com/SELinuxProject/refpolicy].

In order to fully override the refpolicy the following configuration
variables have to be set:

  * BR2_PACKAGE_REFPOLICY_CUSTOM_GIT
  * BR2_PACKAGE_REFPOLICY_CUSTOM_REPO_URL
  * BR2_PACKAGE_REFPOLICY_CUSTOM_REPO_VERSION

## Chapter 11 常见问题及故障处理

### 11.1 启动网络后启动挂起...

如果启动过程在以下消息之后挂起(消息不一定完全相似,取决于所选的包列表):

```console
Freeing init memory: 3972K
Initializing random number generator... done.
Starting network...
Starting dropbear sshd: generating rsa key... generating dsa key... OK
```

then it means that your system is running, but didn't start a shell
on the serial console. In order to have the system start a shell on
your serial console, you have to go into the Buildroot configuration,
in System configuration, modify Run a getty (login prompt) after boot
and set the appropriate port and baud rate in the getty options
submenu. This will automatically tune the /etc/inittab file of the
generated system so that a shell starts on the correct serial port.

### 11.2 为什么目标上没有编译器?

已经决定从Buildroot-2012.11版本开始停止对目标上本地编译器的支持,因为:

  * this feature was neither maintained nor tested, and often broken;
  * this feature was only available for Buildroot toolchains;
  * Buildroot mostly targets small or very small target hardware with
    limited resource onboard (CPU, ram, mass-storage), for which
    compiling on the target does not make much sense;
  * Buildroot aims at easing the cross-compilation, making native
    compilation on the target unnecessary.

If you need a compiler on your target anyway, then Buildroot is not
suitable for your purpose. In such case, you need a real distribution
and you should opt for something like:

  * openembedded [http://www.openembedded.org]
  * yocto [https://www.yoctoproject.org]
  * Debian [https://www.debian.org/ports/]
  * Fedora [https://fedoraproject.org/wiki/Architectures]
  * openSUSE ARM [http://en.opensuse.org/Portal:ARM]
  * Arch Linux ARM [http://archlinuxarm.org]
  * â€¦

### 11.3 为什么目标上没有开发文件?

由于目标上没有可用的编译器(参见11.2节,为什么目标上没有编译器?),
所以用头文件或静态库浪费空间是没有意义的.

因此,自Buildroot-2012.11版本以来,这些文件总是从目标中删除.

### 11.4 为什么没有目标的记录?

因为Buildroot主要针对的是机载资源有限的小型或非常小的目标硬件(CPU、ram、大容量存储),
所以浪费文档数据的空间是没有意义的.

如果您无论如何都需要目标上的文档数据,那么Buildroot不适合您的目的,
您应该寻找一个真正的发行版(参见:11.2节,为什么目标上没有编译器?).

### 11.5 为什么有些包在Buildroot配置菜单中不可见?

如果一个包存在于Buildroot树中,但没有出现在配置菜单中,
这很可能意味着包的一些依赖项没有得到满足.

To know more about the dependencies of a package, search for the
package symbol in the config menu (see Section 8.1, make tips).

Then, you may have to recursively enable several options (which
correspond to the unmet dependencies) to finally be able to select
the package.

If the package is not visible due to some unmet toolchain options,
then you should certainly run a full rebuild (see Section 8.1, make
tips for more explanations).

### 11.6 为什么不使用目标目录作为chroot目录?

There are plenty of reasons to not use the target directory a chroot
one, among these:

  * file ownerships, modes and permissions are not correctly set in
    the target directory;
  * device nodes are not created in the target directory.

For these reasons, commands run through chroot, using the target
directory as the new root, will most likely fail.

If you want to run the target filesystem inside a chroot, or as an
NFS root, then use the tarball image generated in images/ and extract
it as root.

### 11.7 为什么Buildroot不生成二进制包(.deb,.ipkg...)?

Buildroot列表中经常讨论的一个特性是“包管理”这个通用主题.
总的来说,这个想法是添加一些关于哪个Buildroot包安装什么文件的跟踪,目标是:

  * being able to remove files installed by a package when this
    package gets unselected from the menuconfig;
  * being able to generate binary packages (ipk or other format) that
    can be installed on the target without re-generating a new root
    filesystem image.

In general, most people think it is easy to do: just track which
package installed what and remove it when the package is unselected.
However, it is much more complicated than that:

  * It is not only about the target/ directory, but also the sysroot
    in host/<tuple>/sysroot and the host/ directory itself. All files
    installed in those directories by various packages must be
    tracked.
  * When a package is unselected from the configuration, it is not
    sufficient to remove just the files it installed. One must also
    remove all its reverse dependencies (i.e. packages relying on it)
    and rebuild all those packages. For example, package A depends
    optionally on the OpenSSL library. Both are selected, and
    Buildroot is built. Package A is built with crypto support using
    OpenSSL. Later on, OpenSSL gets unselected from the
    configuration, but package A remains (since OpenSSL is an
    optional dependency, this is possible.) If only OpenSSL files are
    removed, then the files installed by package A are broken: they
    use a library that is no longer present on the target. Although
    this is technically doable, it adds a lot of complexity to
    Buildroot, which goes against the simplicity we try to stick to.
  * In addition to the previous problem, there is the case where the
    optional dependency is not even known to Buildroot. For example,
    package A in version 1.0 never used OpenSSL, but in version 2.0
    it automatically uses OpenSSL if available. If the Buildroot .mk
    file hasn't been updated to take this into account, then package
    A will not be part of the reverse dependencies of OpenSSL and
    will not be removed and rebuilt when OpenSSL is removed. For
    sure, the .mk file of package A should be fixed to mention this
    optional dependency, but in the mean time, you can have
    non-reproducible behaviors.
  * The request is to also allow changes in the menuconfig to be
    applied on the output directory without having to rebuild
    everything from scratch. However, this is very difficult to
    achieve in a reliable way: what happens when the suboptions of a
    package are changed (we would have to detect this, and rebuild
    the package from scratch and potentially all its reverse
    dependencies), what happens if toolchain options are changed,
    etc. At the moment, what Buildroot does is clear and simple so
    its behaviour is very reliable and it is easy to support users.
    If configuration changes done in menuconfig are applied after the
    next make, then it has to work correctly and properly in all
    situations, and not have some bizarre corner cases. The risk is
    to get bug reports like "I have enabled package A, B and C, then
    ran make, then disabled package C and enabled package D and ran
    make, then re-enabled package C and enabled package E and then
    there is a build failure". Or worse "I did some configuration,
    then built, then did some changes, built, some more changes,
    built, some more changes, built, and now it fails, but I don't
    remember all the changes I did and in which order". This will be
    impossible to support.

For all these reasons, the conclusion is that adding tracking of
installed files to remove them when the package is unselected, or to
generate a repository of binary packages, is something that is very
hard to achieve reliably and will add a lot of complexity.

On this matter, the Buildroot developers make this position
statement:

  * Buildroot strives to make it easy to generate a root filesystem
    (hence the name, by the way.) That is what we want to make
    Buildroot good at: building root filesystems.
  * Buildroot is not meant to be a distribution (or rather, a
    distribution generator.) It is the opinion of most Buildroot
    developers that this is not a goal we should pursue. We believe
    that there are other tools better suited to generate a distro
    than Buildroot is. For example, Open Embedded [http://
    openembedded.org/], or openWRT [https://openwrt.org/], are such
    tools.
  * We prefer to push Buildroot in a direction that makes it easy (or
    even easier) to generate complete root filesystems. This is what
    makes Buildroot stands out in the crowd (among other things, of
    course!)
  * We believe that for most embedded Linux systems, binary packages
    are not necessary, and potentially harmful. When binary packages
    are used, it means that the system can be partially upgraded,
    which creates an enormous number of possible combinations of
    package versions that should be tested before doing the upgrade
    on the embedded device. On the other hand, by doing complete
    system upgrades by upgrading the entire root filesystem image at
    once, the image deployed to the embedded system is guaranteed to
    really be the one that has been tested and validated.

### 11.8 如何加快构建过程?

由于Buildroot经常需要对整个系统进行完整的重新构建,这可能会很长,
所以我们在下面提供了一些提示,以帮助减少构建时间:

  * Use a pre-built external toolchain instead of the default
    Buildroot internal toolchain. By using a pre-built Linaro
    toolchain (on ARM) or a Sourcery CodeBench toolchain (for ARM,
    x86, x86-64, MIPS, etc.), you will save the build time of the
    toolchain at each complete rebuild, approximately 15 to 20
    minutes. Note that temporarily using an external toolchain does
    not prevent you to switch back to an internal toolchain (that may
    provide a higher level of customization) once the rest of your
    system is working;
  * Use the ccache compiler cache (see: Section 8.14.3, Using ccache
    in Buildroot);
  * Learn about rebuilding only the few packages you actually care
    about (see Section 8.3, Understanding how to rebuild packages),
    but beware that sometimes full rebuilds are anyway necessary (see
    Section 8.2, Understanding when a full rebuild is necessary);
  * Make sure you are not using a virtual machine for the Linux
    system used to run Buildroot. Most of the virtual machine
    technologies are known to cause a significant performance impact
    on I/O, which is really important for building source code;
  * Make sure that you're using only local files: do not attempt to
    do a build over NFS, which significantly slows down the build.
    Having the Buildroot download folder available locally also helps
    a bit.
  * Buy new hardware. SSDs and lots of RAM are key to speeding up the
    builds.
  * Experiment with top-level parallel build, see Section 8.12,
    Top-level parallel build.

## Chapter 12 已知的问题

  * It is not possible to pass extra linker options via
    BR2_TARGET_LDFLAGS if such options contain a $ sign. For example,
    the following is known to break: BR2_TARGET_LDFLAGS="-Wl,-rpath=
    '$ORIGIN/../lib'"
  * The libffi package is not supported on the SuperH 2, nds32, and
    ARMv7-M architectures.
  * The prboom package triggers a compiler failure with the SuperH 4
    compiler from Sourcery CodeBench, version 2012.09.

## Chapter 13 法律通知和许可

### 13.1 遵循开源许可协议

构建droot(工具链、根系统、内核、引导加载器)的所有最终产品都包含开源软件,在各种许可证下发布.

使用开源软件可以让您自由地构建丰富的嵌入式系统,从广泛的软件包中进行选择,
但也强加了一些您必须知道和遵守的义务.有些许可要求您在产品文档中发布许可文本.
另一些则要求您将软件的源代码重新分发给那些接收您的产品的人.

每个许可证的确切要求都记录在每个包中,遵守这些要求是您(或您的法律办公室)的责任.
为了方便您,Buildroot可以为您收集一些您可能需要的材料.要生成这个材料,
在你用make menuconfig、make xconfig或make gconfig配置了Buildroot之后,运行:

```console
make legal-info
```

Buildroot将在输出目录legal-info/子目录下收集与法律相关的材料.你会发现:

  * A README file, that summarizes the produced material and contains
    warnings about material that Buildroot could not produce.
  * buildroot.config: this is the Buildroot configuration file that
    is usually produced with make menuconfig, and which is necessary
    to reproduce the build.
  * The source code for all packages; this is saved in the sources/
    and host-sources/ subdirectories for target and host packages
    respectively. The source code for packages that set <PKG>
    _REDISTRIBUTE = NO will not be saved. Patches that were applied
    are also saved, along with a file named series that lists the
    patches in the order they were applied. Patches are under the
    same license as the files that they modify. Note: Buildroot
    applies additional patches to Libtool scripts of autotools-based
    packages. These patches can be found under support/libtool in the
    Buildroot source and, due to technical limitations, are not saved
    with the package sources. You may need to collect them manually.
  * A manifest file (one for host and one for target packages)
    listing the configured packages, their version, license and
    related information. Some of this information might not be
    defined in Buildroot; such items are marked as "unknown".
  * The license texts of all packages, in the licenses/ and
    host-licenses/ subdirectories for target and host packages
    respectively. If the license file(s) are not defined in
    Buildroot, the file is not produced and a warning in the README
    indicates this.

请注意,Buildroot的法律信息特性的目的是生成与软件包许可的法律合规性有关的所有材料.
Buildroot不会试图生产你必须以某种方式公开的确切材料.当然,生产的材料比严格遵守法律所需要的要多.
例如,它为在类似bsd的许可证下发布的包生成源代码,您不需要以源代码的形式重新发布这些包.

此外,由于技术上的限制,Buildroot不会生成您将会或可能需要的一些材料,
例如一些外部工具链的工具链源代码和Buildroot源代码本身.
当您运行make legal-info时,Buildroot会在README文件中产生警告,告知您无法保存的相关材料.

最后,请记住,make legal-info的输出基于每个包配方中的声明性语句.
Buildroot的开发人员会尽他们最大的努力使这些声明式语句尽可能准确.
然而,很有可能这些陈述性的陈述并不都是完全准确或详尽的.
您(或您的法律部门)必须检查make legal-info的输出,然后再将其用作您自己的遵从性交付.
请参阅位于Buildroot发行版根目录的拷贝文件中的NO WARRANTY条款(第11和12条).

### 13.2 符合Buildroot许可证

Buildroot本身是一个开源软件,在GNU通用公共许可证下发布,版本2 
[http://www.gnu.org/licenses/old-licenses/gpl-2.0.html]
或(根据您的选择)任何更高的版本,除了下面详细介绍的包补丁.然而,作为一个构建系统,
它通常不是最终产品的一部分:如果您为一个设备开发根文件系统、内核、引导加载程序或工具链,
Buildroot的代码只会出现在开发机器上,而不会出现在设备存储中.

Nevertheless, the general view of the Buildroot developers is that
you should release the Buildroot source code along with the source
code of other packages when releasing a product that contains
GPL-licensed software. This is because the GNU GPL [http://
www.gnu.org/licenses/old-licenses/gpl-2.0.html] defines the "complete
source code" for an executable work as "all the source code for all
modules it contains, plus any associated interface definition files,
plus the scripts used to control compilation and installation of the
executable". Buildroot is part of the scripts used to control
compilation and installation of the executable, and as such it is
considered part of the material that must be redistributed.

Keep in mind that this is only the Buildroot developers' opinion, and
you should consult your legal department or lawyer in case of any
doubt.

#### 13.2.1 补丁包

Buildroot还打包了补丁文件,这些补丁文件应用于各种包的源代码.
这些补丁不包括在Buildroot的许可证中.相反,它们受到应用补丁的软件的许可证的保护.
当上述软件在多个许可证下可用时,Buildroot补丁只在公开可访问的许可证下提供.

See Chapter 19, Patching a package for the technical details.

## Chapter 14 Buildroot之外

### 14.1 引导生成的映像

#### 14.1.1 NFS boot

要实现nfs引导,请在filesystem images菜单中启用tar根文件系统.

After a complete build, just run the following commands to setup the
NFS-root directory:

sudo tar -xavf /path/to/output_dir/rootfs.tar -C /path/to/nfs_root_dir

Remember to add this path to /etc/exports.

Then, you can execute a NFS-boot from your target.

#### 14.1.2 Live CD

要构建活动CD映像,请在Filesystem images菜单中启用iso映像选项.
注意,这个选项仅在x86和x86-64架构上可用,并且如果您使用Buildroot构建内核的话.

You can build a live CD image with either IsoLinux, Grub or Grub 2 as
a bootloader, but only Isolinux supports making this image usable
both as a live CD and live USB (through the Build hybrid image
option).

You can test your live CD image using QEMU:

qemu-system-i386 -cdrom output/images/rootfs.iso9660

Or use it as a hard-drive image if it is a hybrid ISO:

qemu-system-i386 -hda output/images/rootfs.iso9660

It can be easily flashed to a USB drive with dd:

dd if=output/images/rootfs.iso9660 of=/dev/sdb

### 14.2 Chroot

如果你想在生成的映像中使用chroot,那么有一些事情你应该知道:

  * you should setup the new root from the tar root filesystem image;
  * either the selected target architecture is compatible with your
    host machine, or you should use some qemu-* binary and correctly
    set it within the binfmt properties to be able to run the
    binaries built for the target on your host machine;
  * Buildroot does not currently provide host-qemu and binfmt
    correctly built and set for that kind of use.

Part III. 开发人员指南

目录

15. Buildroot是如何工作的
16. 编程风格

    16.1. Config.in文件
    16.2. .mk文件
    16.3. genimage.cfg文件
    16.4. 文档
    16.5. 支持脚本

17. 添加对特定开发板的支持
18. 为Buildroot添加新包

    18.1. Package目录
    18.2. Config文件
    18.3. .mk文件
    18.4. .hash文件
    18.5. SNNfoo启动脚本
    18.6. 具有特定构建系统的包的基础结构
    18.7. autotools-based包基础架构
    18.8. CMake-based包基础架构
    18.9. Python包基础架构
    18.10. LuaRocks-based包基础架构
    18.11. Perl/CPAN包基础架构
    18.12. virtual包基础架构
    18.13. 包的基础架构使用kconfig配置文件
    18.14. rebar-based包基础架构
    18.15. Waf-based包基础架构
    18.16. Meson-based包基础架构
    18.17. Cargo-based包基础架构
    18.18. Go包基础架构
    18.19. QMake-based包基础架构
    18.20. 构建内核模块的包的基础设施
    18.21. asciidoc文档的基础架构
    18.22. 特定于Linux内核包的基础结构
    18.23. 各种构建步骤中可用的钩子
    18.24. 与包的Gettext集成和交互
    18.25. 提示和技巧
    18.26. 结论

19. 为包打补丁

    19.1. 提供补丁
    19.2. 如何应用补丁
    19.3. 软件包补丁的格式和许可
    19.4. 集成在Web上找到的补丁

20. 下载基础设施
21. 调试Buildroot
22. 为Buildroot贡献

    22.1. 复制、分析和修复bugs
    22.2. 分析和修复自动构建失败
    22.3. 检查和测试补丁
    22.4. 完成待办事项列表中的任务
    22.5. 提交补丁
    22.6. 报告issue/bugs或获得帮助
    22.7. 使用运行时测试框架

23. DEVELOPERS文件和get-developers
24. Release工程

    24.1. Releases
    24.2. Development

## Chapter 15 Buildroot是如何工作的

如上所述,Buildroot基本上是一组通过正确选项下载、配置和编译软件的makefile.
它还包括各种软件包的补丁——主要是跨编译工具链(gcc、binutils和uClibc).

基本上每个软件包都有一个Makefile,它们以.mk扩展名命名.makefile被分成许多不同的部分.

  * The toolchain/ directory contains the Makefiles and associated
    files for all software related to the cross-compilation
    toolchain: binutils, gcc, gdb, kernel-headers and uClibc.
  * The arch/ directory contains the definitions for all the
    processor architectures that are supported by Buildroot.
  * The package/ directory contains the Makefiles and associated
    files for all user-space tools and libraries that Buildroot can
    compile and add to the target root filesystem. There is one
    sub-directory per package.
  * The linux/ directory contains the Makefiles and associated files
    for the Linux kernel.
  * The boot/ directory contains the Makefiles and associated files
    for the bootloaders supported by Buildroot.
  * The system/ directory contains support for system integration,
    e.g. the target filesystem skeleton and the selection of an init
    system.
  * The fs/ directory contains the Makefiles and associated files for
    software related to the generation of the target root filesystem
    image.

每个目录至少包含2个文件:

  * something.mk is the Makefile that downloads, configures, compiles
    and installs the package something.
  * Config.in is a part of the configuration tool description file.
    It describes the options related to the package.

主Makefile执行以下步骤(一旦配置完成):

  * 在输出目录中创建所有输出目录:staging、target、build等
    (默认情况下,输出/可以使用O=指定另一个值)
  * 生成工具链目标.当使用内部工具链时,这意味着生成交叉编译的工具链.
    当使用外部工具链时,这意味着检查外部工具链的特性并将其导入到Buildroot环境中.
  * 生成targets变量中列出的所有目标.这个变量由所有独立组件的makefile填充.
    生成这些目标将触发编译用户空间包(库、程序)、内核、引导加载程序和生成根
    文件系统映像,具体取决于配置.

## Chapter 16 编程风格

总的来说,这些编码风格规则可以帮助您在Buildroot中添加新文件或重构现有文件.

If you slightly modify some existing file, the important thing is to
keep the consistency of the whole file, so you can:

  * either follow the potentially deprecated coding style used in
    this file,
  * or entirely rework it in order to make it comply with these
    rules.

### 16.1 Config.in文件

Config.in文件包含几乎所有在Buildroot中可配置的条目.

An entry has the following pattern:

```bash
config BR2_PACKAGE_LIBFOO
        bool "libfoo"
        depends on BR2_PACKAGE_LIBBAZ
        select BR2_PACKAGE_LIBBAR
        help
          This is a comment that explains what libfoo is. The help text
          should be wrapped.

          http://foosoftware.org/libfoo/
```

  * The bool, depends on, select and help lines are indented with one
    tab.
  * The help text itself should be indented with one tab and two
    spaces.
  * The help text should be wrapped to fit 72 columns, where tab
    counts for 8, so 62 characters in the text itself.

Config.in在文件中,配置工具用于Buildroot的配置工具,这是常规的Kconfig.有关Kconfig语言的进一步细节,
请参阅http://kernel.org/doc/Documentation/kbuild/kconfig-language.txt.

### 16.2 .mk文件

  * Header: 该文件以一个头文件开始.它包含模块名,最好是小写,
    用80个散列组成的分隔符括起来.标题后必须有空行:

    ################################################################################
    #
    # libfoo
    #
    ################################################################################

  * Assignment: use = preceded and followed by one space:

```bash
    LIBFOO_VERSION = 1.0
    LIBFOO_CONF_OPTS += --without-python-support

    Do not align the = signs.
```

  * Indentation: use tab only:

```bash
    define LIBFOO_REMOVE_DOC
            $(RM) -fr $(TARGET_DIR)/usr/share/libfoo/doc \
                    $(TARGET_DIR)/usr/share/man/man3/libfoo*
    endef

    Note that commands inside a define block should always start with
    a tab, so make recognizes them as commands.
```

  * Optional dependency:

      + Prefer multi-line syntax.

        YES:

```bash
        ifeq ($(BR2_PACKAGE_PYTHON3),y)
        LIBFOO_CONF_OPTS += --with-python-support
        LIBFOO_DEPENDENCIES += python3
        else
        LIBFOO_CONF_OPTS += --without-python-support
        endif
```

        NO:

```bash
        LIBFOO_CONF_OPTS += --with$(if $(BR2_PACKAGE_PYTHON3),,out)-python-support
        LIBFOO_DEPENDENCIES += $(if $(BR2_PACKAGE_PYTHON3),python3,)
```

      + Keep configure options and dependencies close together.
  * Optional hooks: keep hook definition and assignment together in
    one if block.

    YES:

```bash
    ifneq ($(BR2_LIBFOO_INSTALL_DATA),y)
    define LIBFOO_REMOVE_DATA
            $(RM) -fr $(TARGET_DIR)/usr/share/libfoo/data
    endef
    LIBFOO_POST_INSTALL_TARGET_HOOKS += LIBFOO_REMOVE_DATA
    endif
```

    NO:

```bash
    define LIBFOO_REMOVE_DATA
            $(RM) -fr $(TARGET_DIR)/usr/share/libfoo/data
    endef

    ifneq ($(BR2_LIBFOO_INSTALL_DATA),y)
    LIBFOO_POST_INSTALL_TARGET_HOOKS += LIBFOO_REMOVE_DATA
    endif
```

### 16.3 genimage.cfg文件

genimage.cfg文件包含输出图像布局,genimage实用程序使用它来创建最终的.img文件.

An example follows:

```bash
image efi-part.vfat {
        vfat {
                file EFI {
                        image = "efi-part/EFI"
                }

                file Image {
                        image = "Image"
                }
        }

        size = 32M
}

image sdimage.img {
        hdimage {
        }

        partition u-boot {
                image = "efi-part.vfat"
                offset = 8K
        }

        partition root {
                image = "rootfs.ext2"
                size = 512M
        }
}
```

  * Every section(i.e. hdimage, vfat etc.), partition must be
    indented with one tab.
  * Every file or other subnode must be indented with two tabs.
  * Every node(section, partition, file, subnode) must have an open
    curly bracket on the same line of the node's name, while the
    closing one must be on a newline and after it a newline must be
    added except for the last one node. Same goes for its option, for
    example option size =.
  * Every option(i.e. image, offset, size) must have the = assignment
    one space from it and one space from the value specified.
  * Filename must at least begin with genimage prefix and have the
    .cfg extension to be easy to recognize.
  * Allowed notations for offset and size options are: G, M, K (not
    k). If it's not possible to express a precise byte count with
    notations above then use hexadecimal 0x prefix or, as last
    chance, the byte count. In comments instead use GB, MB, KB (not
    kb) in place of G, M, K.

genimage.cfg文件是genimage工具的输入,在Buildroot中使用该工具生成最终的图像文件
(即.sdcard.img).有关genimage语言的更多详细信息,请参阅
[https://github.com/pengutronix/genimage/blob/master/README.rst].

### 16.4 文档

该文档使用asciidoc格式[https://asciidoc-py.github.io/].

有关asciidoc语法的更多详细信息,请参考
[https://asciidoc-py.github.io/userguide.html].

### 16.5 支持脚本

support/和utils/目录中的一些脚本是用Python编写的,
应该遵循PEP8 Python代码风格指南[https://www.python.org/dev/peps/pep-0008/].

## Chapter 17 添加对特定开发板的支持

Buildroot包含几个公开可用的硬件板的基本配置,这样一个板的用户就可以轻松地
构建一个已知可以工作的系统.也欢迎您在Buildroot中添加对其他板的支持.

To do so, you need to create a normal Buildroot configuration that
builds a basic system for the hardware: (internal) toolchain, kernel,
bootloader, filesystem and a simple BusyBox-only userspace. No
specific package should be selected: the configuration should be as
minimal as possible, and should only build a working basic BusyBox
system for the target platform. You can of course use more
complicated configurations for your internal projects, but the
Buildroot project will only integrate basic board configurations.
This is because package selections are highly application-specific.

Once you have a known working configuration, run make savedefconfig.
This will generate a minimal defconfig file at the root of the
Buildroot source tree. Move this file into the configs/ directory,
and rename it <boardname>_defconfig. If the configuration is a bit
more complicated, it is nice to manually reformat it and separate it
into sections, with a comment before each section. Typical sections
are Architecture, Toolchain options (typically just linux headers
version), Firmware, Bootloader, Kernel, and Filesystem.

Always use fixed versions or commit hashes for the different
components, not the "latest" version. For example, set
BR2_LINUX_KERNEL_CUSTOM_VERSION=y and
BR2_LINUX_KERNEL_CUSTOM_VERSION_VALUE to the kernel version you
tested with.

建议尽可能多地使用Linux内核和引导加载程序的上游版本,并尽可能多地使用默认内核和引导加载程序配置.
如果它们对你的董事会不正确,或者不存在默认值,我们鼓励你发送修复到相应的上游项目.

However, in the mean time, you may want to store kernel or bootloader
configuration or patches specific to your target platform. To do so,
create a directory board/<manufacturer> and a subdirectory board/
<manufacturer>/<boardname>. You can then store your patches and
configurations in these directories, and reference them from the main
Buildroot configuration. Refer to Chapter 9, Project-specific
customization for more details.

Before submitting patches for new boards it is recommended to test it
by building it using latest gitlab-CI docker container. To do this
use utils/docker-run script and inside it issue these commands:

```console
$ make +<boardname>_defconfig+
$ make
```

## Chapter 18 为Buildroot添加新包

本节将介绍如何将新的包(用户空间库或应用程序)集成到Buildroot中.
它还展示了如何集成现有的包,这是修复问题或调优它们的配置所需要的.

当你添加一个新的包时,一定要在各种条件下测试它(参见第18.25.3节,
如何测试你的包),并检查它的编码风格(参见第18.25.2节,如何检查编码风格).

### 18.1 Package目录

首先,在软件包目录下为软件创建一个目录,例如libfoo.

Some packages have been grouped by topic in a sub-directory: x11r7,
qt5 and gstreamer. If your package fits in one of these categories,
then create your package directory in these. New subdirectories are
discouraged, however.

### 18.2 Config文件

要在配置工具中显示包,您需要在包目录中创建一个Config文件.
有两种类型:Config.in和Config.in.host.

#### 18.2.1 Config.in文件

对于在目标上使用的包,创建一个名为Config.in的文件.该文件将包含与我们
的libfoo软件相关的选项描述,这些将被使用并显示在配置工具中.它应该包含:

```bash
config BR2_PACKAGE_LIBFOO
        bool "libfoo"
        help
          This is a comment that explains what libfoo is. The help text
          should be wrapped.

          http://foosoftware.org/libfoo/
```

关于配置选项的bool行、帮助行和其他元数据信息必须用一个选项卡缩进.
帮助文本本身应该用一个制表符和两个空格缩进,行应该换行以容纳72列,其中制表符
计数为8,因此文本本身有62个字符.帮助文本必须在空行之后提到项目的上游URL.

作为Buildroot特有的约定,属性的顺序如下:

 1. The type of option: bool, string with the prompt
 2. If needed, the default value(s)
 3. Any dependencies on the target in depends on form
 4. Any dependencies on the toolchain in depends on form
 5. Any dependencies on other packages in depends on form
 6. Any dependency of the select form
 7. The help keyword and help text.

You can add other sub-options into a if BR2_PACKAGE_LIBFOO endif
statement to configure particular things in your software. You can
look at examples in other packages. The syntax of the Config.in file
is the same as the one for the kernel Kconfig file. The documentation
for this syntax is available at http://kernel.org/doc/Documentation/
kbuild/kconfig-language.txt

Finally you have to add your new libfoo/Config.in to package/
Config.in (or in a category subdirectory if you decided to put your
package in one of the existing categories). The files included there
are sorted alphabetically per category and are NOT supposed to
contain anything but the bare name of the package.

source "package/libfoo/Config.in"

#### 18.2.2 Config.in.host文件

还需要为主机系统构建一些包.这里有两个选择:

  * The host package is only required to satisfy build-time
    dependencies of one or more target packages. In this case, add
    host-foo to the target package's BAR_DEPENDENCIES variable. No
    Config.in.host file should be created.
  * The host package should be explicitly selectable by the user from
    the configuration menu. In this case, create a Config.in.host
    file for that host package:

    config BR2_PACKAGE_HOST_FOO
            bool "host foo"
            help
              This is a comment that explains what foo for the host is.

              http://foosoftware.org/foo/

    The same coding style and options as for the Config.in file are
    valid.

    Finally you have to add your new libfoo/Config.in.host to package
    /Config.in.host. The files included there are sorted
    alphabetically and are NOT supposed to contain anything but the 
    bare name of the package.

    source "package/foo/Config.in.host"

    The host package will then be available from the Host utilities
    menu.

#### 18.2.3 Choosing depends on or select

Config.in在您的包的文件中还必须确保依赖项是启用的.通常,Buildroot使用以下规则:

  * Use a select type of dependency for dependencies on libraries.
    These dependencies are generally not obvious and it therefore
    make sense to have the kconfig system ensure that the
    dependencies are selected. For example, the libgtk2 package uses
    select BR2_PACKAGE_LIBGLIB2 to make sure this library is also
    enabled. The select keyword expresses the dependency with a
    backward semantic.
  * Use a depends on type of dependency when the user really needs to
    be aware of the dependency. Typically, Buildroot uses this type
    of dependency for dependencies on target architecture, MMU
    support and toolchain options (see Section 18.2.4, Dependencies
    on target and toolchain options), or for dependencies on "big"
    things, such as the X.org system. The depends on keyword
    expresses the dependency with a forward semantic.

Note. The current problem with the kconfig language is that these two
dependency semantics are not internally linked. Therefore, it may be
possible to select a package, whom one of its dependencies/
requirement is not met.

An example illustrates both the usage of select and depends on.

```bash
config BR2_PACKAGE_RRDTOOL
        bool "rrdtool"
        depends on BR2_USE_WCHAR
        select BR2_PACKAGE_FREETYPE
        select BR2_PACKAGE_LIBART
        select BR2_PACKAGE_LIBPNG
        select BR2_PACKAGE_ZLIB
        help
          RRDtool is the OpenSource industry standard, high performance
          data logging and graphing system for time series data.

          http://oss.oetiker.ch/rrdtool/

comment "rrdtool needs a toolchain w/ wchar"
        depends on !BR2_USE_WCHAR

Note that these two dependency types are only transitive with the
dependencies of the same kind.

This means, in the following example:

config BR2_PACKAGE_A
        bool "Package A"

config BR2_PACKAGE_B
        bool "Package B"
        depends on BR2_PACKAGE_A

config BR2_PACKAGE_C
        bool "Package C"
        depends on BR2_PACKAGE_B

config BR2_PACKAGE_D
        bool "Package D"
        select BR2_PACKAGE_B

config BR2_PACKAGE_E
        bool "Package E"
        select BR2_PACKAGE_D

  * Selecting Package C will be visible if Package B has been
    selected, which in turn is only visible if Package A has been
    selected.
  * Selecting Package E will select Package D, which will select
    Package B, it will not check for the dependencies of Package B,
    so it will not select Package A.
  * Since Package B is selected but Package A is not, this violates
    the dependency of Package B on Package A. Therefore, in such a
    situation, the transitive dependency has to be added explicitly:

config BR2_PACKAGE_D
        bool "Package D"
        depends on BR2_PACKAGE_A
        select BR2_PACKAGE_B

config BR2_PACKAGE_E
        bool "Package E"
        depends on BR2_PACKAGE_A
        select BR2_PACKAGE_D
```

Overall, for package library dependencies, select should be
preferred.

Note that such dependencies will ensure that the dependency option is
also enabled, but not necessarily built before your package. To do
so, the dependency also needs to be expressed in the .mk file of the
package.

Further formatting details: see the coding style.

#### 18.2.4 Dependencies on target and toolchain options

Many packages depend on certain options of the toolchain: the choice
of C library, C++ support, thread support, RPC support, wchar
support, or dynamic library support. Some packages can only be built
on certain target architectures, or if an MMU is available in the
processor.

这些依赖关系必须在Config中使用适当的depends语句来表示.在文件中.此外,对于工具链选项的依赖关系,
当选项未启用时,应该显示一条注释,以便用户知道为什么包不可用.对目标架构或MMU支持的依赖不应该在
注释中显示:因为用户不太可能自由地选择另一个目标,所以显式地显示这些依赖没有什么意义.

只有在满足工具链选项依赖关系时,配置选项本身是可见的,该注释才应该是可见的.这意味着包的所有其他
依赖项(包括对目标体系结构和MMU支持的依赖项)必须在注释定义上重复.为了清晰起见,这些非工具链选项
的depends语句应该与工具链选项的depends语句分开.如果在同一个文件(通常是主包)中有一个配置选项的依赖,
最好使用全局的If构造 endif,而不是在注释和其他配置选项上重复依赖语句.

The general format of a dependency comment for package foo is:

foo needs a toolchain w/ featA, featB, featC

for example:

mpd needs a toolchain w/ C++, threads, wchar

or

crda needs a toolchain w/ threads

Note that this text is kept brief on purpose, so that it will fit on
a 80-character terminal.

本节的其余部分列举了不同的目标和工具链选项、要依赖的相应配置符号,以及注释中要使用的文本.

  * Target architecture

      + Dependency symbol: BR2_powerpc, BR2_mips, (see arch/
        Config.in)
      + Comment string: no comment to be added
  * MMU support

      + Dependency symbol: BR2_USE_MMU
      + Comment string: no comment to be added
  * Gcc _sync* built-ins used for atomic operations. They are
    available in variants operating on 1 byte, 2 bytes, 4 bytes and 8
    bytes. Since different architectures support atomic operations on
    different sizes, one dependency symbol is available for each
    size:

      + Dependency symbol: BR2_TOOLCHAIN_HAS_SYNC_1 for 1 byte,
        BR2_TOOLCHAIN_HAS_SYNC_2 for 2 bytes,
        BR2_TOOLCHAIN_HAS_SYNC_4 for 4 bytes,
        BR2_TOOLCHAIN_HAS_SYNC_8 for 8 bytes.
      + Comment string: no comment to be added
  * Gcc _atomic* built-ins used for atomic operations.

      + Dependency symbol: BR2_TOOLCHAIN_HAS_ATOMIC.
      + Comment string: no comment to be added
  * Kernel headers

      + Dependency symbol: BR2_TOOLCHAIN_HEADERS_AT_LEAST_X_Y,
        (replace X_Y with the proper version, see toolchain/
        Config.in)
      + Comment string: headers >= X.Y and/or headers <= X.Y (replace
        X.Y with the proper version)
  * GCC version

      + Dependency symbol: BR2_TOOLCHAIN_GCC_AT_LEAST_X_Y, (replace
        X_Y with the proper version, see toolchain/Config.in)
      + Comment string: gcc >= X.Y and/or gcc <= X.Y (replace X.Y
        with the proper version)
  * Host GCC version

      + Dependency symbol: BR2_HOST_GCC_AT_LEAST_X_Y, (replace X_Y
        with the proper version, see Config.in)
      + Comment string: no comment to be added
      + Note that it is usually not the package itself that has a
        minimum host GCC version, but rather a host-package on which
        it depends.
  * C library

      + Dependency symbol: BR2_TOOLCHAIN_USES_GLIBC,
        BR2_TOOLCHAIN_USES_MUSL, BR2_TOOLCHAIN_USES_UCLIBC
      + Comment string: for the C library, a slightly different
        comment text is used: foo needs a glibc toolchain, or foo
        needs a glibc toolchain w/ C++
  * C++ support

      + Dependency symbol: BR2_INSTALL_LIBSTDCPP
      + Comment string: C++
  * D support

      + Dependency symbol: BR2_TOOLCHAIN_HAS_DLANG
      + Comment string: Dlang
  * Fortran support

      + Dependency symbol: BR2_TOOLCHAIN_HAS_FORTRAN
      + Comment string: fortran
  * thread support

      + Dependency symbol: BR2_TOOLCHAIN_HAS_THREADS
      + Comment string: threads (unless
        BR2_TOOLCHAIN_HAS_THREADS_NPTL is also needed, in which case,
        specifying only NPTL is sufficient)
  * NPTL thread support

      + Dependency symbol: BR2_TOOLCHAIN_HAS_THREADS_NPTL
      + Comment string: NPTL
  * RPC support

      + Dependency symbol: BR2_TOOLCHAIN_HAS_NATIVE_RPC
      + Comment string: RPC
  * wchar support

      + Dependency symbol: BR2_USE_WCHAR
      + Comment string: wchar
  * dynamic library

      + Dependency symbol: !BR2_STATIC_LIBS
      + Comment string: dynamic library

#### 18.2.5 Dependencies on a Linux kernel built by buildroot

Some packages need a Linux kernel to be built by buildroot. These are
typically kernel modules or firmware. A comment should be added in
the Config.in file to express this dependency, similar to
dependencies on toolchain options. The general format is:

foo needs a Linux kernel to be built

If there is a dependency on both toolchain options and the Linux
kernel, use this format:

foo needs a toolchain w/ featA, featB, featC and a Linux kernel to be built

#### 18.2.6 Dependencies on udev /dev management

If a package needs udev /dev management, it should depend on symbol
BR2_PACKAGE_HAS_UDEV, and the following comment should be added:

foo needs udev /dev management

If there is a dependency on both toolchain options and udev /dev
management, use this format:

foo needs udev /dev management and a toolchain w/ featA, featB, featC

#### 18.2.7. Dependencies on features provided by virtual packages

Some features can be provided by more than one package, such as the
openGL libraries.

See Section 18.12, Infrastructure for virtual packages for more on
the virtual packages.

### 18.3 .mk文件

Finally, here's the hardest part. Create a file named libfoo.mk. It
describes how the package should be downloaded, configured, built,
installed, etc.

Depending on the package type, the .mk file must be written in a
different way, using different infrastructures:

  * Makefiles for generic packages (not using autotools or CMake):
    These are based on an infrastructure similar to the one used for
    autotools-based packages, but require a little more work from the
    developer. They specify what should be done for the
    configuration, compilation and installation of the package. This
    infrastructure must be used for all packages that do not use the
    autotools as their build system. In the future, other specialized
    infrastructures might be written for other build systems. We
    cover them through in a tutorial and a reference.
  * Makefiles for autotools-based software (autoconf, automake,
    etc.): We provide a dedicated infrastructure for such packages,
    since autotools is a very common build system. This
    infrastructure must be used for new packages that rely on the
    autotools as their build system. We cover them through a tutorial
    and reference.
  * Makefiles for cmake-based software: We provide a dedicated
    infrastructure for such packages, as CMake is a more and more
    commonly used build system and has a standardized behaviour. This
    infrastructure must be used for new packages that rely on CMake.
    We cover them through a tutorial and reference.
  * Makefiles for Python modules: We have a dedicated infrastructure
    for Python modules that use either the distutils or the
    setuptools mechanism. We cover them through a tutorial and a
    reference.
  * Makefiles for Lua modules: We have a dedicated infrastructure for
    Lua modules available through the LuaRocks web site. We cover
    them through a tutorial and a reference.

Further formatting details: see the writing rules.

### 18.4 .hash文件

When possible, you must add a third file, named libfoo.hash, that
contains the hashes of the downloaded files for the libfoo package.
The only reason for not adding a .hash file is when hash checking is
not possible due to how the package is downloaded.

When a package has a version selection choice, then the hash file may
be stored in a subdirectory named after the version, e.g. package/
libfoo/1.2.3/libfoo.hash. This is especially important if the
different versions have different licensing terms, but they are
stored in the same file. Otherwise, the hash file should stay in the
package's directory.

The hashes stored in that file are used to validate the integrity of
the downloaded files and of the license files.

The format of this file is one line for each file for which to check
the hash, each line with the following three fields separated by two
spaces:

  * the type of hash, one of:

      + md5, sha1, sha224, sha256, sha384, sha512
  * the hash of the file:

      + for md5, 32 hexadecimal characters
      + for sha1, 40 hexadecimal characters
      + for sha224, 56 hexadecimal characters
      + for sha256, 64 hexadecimal characters
      + for sha384, 96 hexadecimal characters
      + for sha512, 128 hexadecimal characters
  * the name of the file:

      + for a source archive: the basename of the file, without any
        directory component,
      + for a license file: the path as it appears in
        FOO_LICENSE_FILES.

Lines starting with a # sign are considered comments, and ignored.
Empty lines are ignored.

There can be more than one hash for a single file, each on its own
line. In this case, all hashes must match.

Note. Ideally, the hashes stored in this file should match the hashes
published by upstream, e.g. on their website, in the e-mail
announcement If upstream provides more than one type of hash (e.g.
sha1 and sha512), then it is best to add all those hashes in the
.hash file. If upstream does not provide any hash, or only provides
an md5 hash, then compute at least one strong hash yourself
(preferably sha256, but not md5), and mention this in a comment line
above the hashes.

Note. The hashes for license files are used to detect a license
change when a package version is bumped. The hashes are checked
during the make legal-info target run. For a package with multiple
versions (like Qt5), create the hash file in a subdirectory
<packageversion> of that package (see also Section 19.2, How patches
are applied).

The example below defines a sha1 and a sha256 published by upstream
for the main libfoo-1.2.3.tar.bz2 tarball, an md5 from upstream and a
locally-computed sha256 hashes for a binary blob, a sha256 for a
downloaded patch, and an archive with no hash:

# Hashes from: http://www.foosoftware.org/download/libfoo-1.2.3.tar.bz2.{sha1,sha256}:
sha1  486fb55c3efa71148fe07895fd713ea3a5ae343a  libfoo-1.2.3.tar.bz2
sha256  efc8103cc3bcb06bda6a781532d12701eb081ad83e8f90004b39ab81b65d4369  libfoo-1.2.3.tar.bz2

# md5 from: http://www.foosoftware.org/download/libfoo-1.2.3.tar.bz2.md5, sha256 locally computed:
md5  2d608f3c318c6b7557d551a5a09314f03452f1a1  libfoo-data.bin
sha256  01ba4719c80b6fe911b091a7c05124b64eeece964e09c058ef8f9805daca546b  libfoo-data.bin

# Locally computed:
sha256  ff52101fb90bbfc3fe9475e425688c660f46216d7e751c4bbdb1dc85cdccacb9  libfoo-fix-blabla.patch

# Hash for license files:
sha256  a45a845012742796534f7e91fe623262ccfb99460a2bd04015bd28d66fba95b8  COPYING
sha256  01b1f9f2c8ee648a7a596a1abe8aa4ed7899b1c9e5551bda06da6e422b04aa55  doc/COPYING.LGPL

If the .hash file is present, and it contains one or more hashes for
a downloaded file, the hash(es) computed by Buildroot (after
download) must match the hash(es) stored in the .hash file. If one or
more hashes do not match, Buildroot considers this an error, deletes
the downloaded file, and aborts.

If the .hash file is present, but it does not contain a hash for a
downloaded file, Buildroot considers this an error and aborts.
However, the downloaded file is left in the download directory since
this typically indicates that the .hash file is wrong but the
downloaded file is probably OK.

Hashes are currently checked for files fetched from http/ftp servers,
Git repositories, files copied using scp and local files. Hashes are
not checked for other version control systems (such as Subversion,
CVS, etc.) because Buildroot currently does not generate reproducible
tarballs when source code is fetched from such version control
systems.

Hashes should only be added in .hash files for files that are
guaranteed to be stable. For example, patches auto-generated by
Github are not guaranteed to be stable, and therefore their hashes
can change over time. Such patches should not be downloaded, and
instead be added locally to the package folder.

If the .hash file is missing, then no check is done at all.

### 18.5 SNNfoo启动脚本

Packages that provide a system daemon usually need to be started
somehow at boot. Buildroot comes with support for several init
systems, some are considered tier one (see Section 6.3, init system
), while others are also available but do not have the same level of
integration. Ideally, all packages providing a system daemon should
provide a start script for BusyBox/SysV init and a systemd unit file.

For consistency, the start script must follow the style and
composition as shown in the reference: package/busybox/S01syslogd. An
annotated example of this style is shown below. There is no specific
coding style for systemd unit files, but if a package comes with its
own unit file, that is preferred over a buildroot specific one, if it
is compatible with buildroot.

The name of the start script is composed of the SNN and the daemon
name. The NN is the start order number which needs to be carefully
chosen. For example, a program that requires networking to be up
should not start before S40network. The scripts are started in
alphabetical order, so S01syslogd starts before S01watchdogd, and
S02sysctl start thereafter.

```bash
01: #!/bin/sh
02:
03: DAEMON="syslogd"
04: PIDFILE="/var/run/$DAEMON.pid"
05:
06: SYSLOGD_ARGS=""
07:
08: # shellcheck source=/dev/null
09: [ -r "/etc/default/$DAEMON" ] && . "/etc/default/$DAEMON"
10:
11: # BusyBox' syslogd does not create a pidfile, so pass "-n" in the command line
12: # and use "-m" to instruct start-stop-daemon to create one.
13: start() {
14:     printf 'Starting %s: ' "$DAEMON"
15:     # shellcheck disable=SC2086 # we need the word splitting
16:     start-stop-daemon -b -m -S -q -p "$PIDFILE" -x "/sbin/$DAEMON" \
17:             -- -n $SYSLOGD_ARGS
18:     status=$?
19:     if [ "$status" -eq 0 ]; then
20:             echo "OK"
21:     else
22:             echo "FAIL"
23:     fi
24:     return "$status"
25: }
26:
27: stop() {
28:     printf 'Stopping %s: ' "$DAEMON"
29:     start-stop-daemon -K -q -p "$PIDFILE"
30:     status=$?
31:     if [ "$status" -eq 0 ]; then
32:             rm -f "$PIDFILE"
33:             echo "OK"
34:     else
35:             echo "FAIL"
36:     fi
37:     return "$status"
38: }
39:
40: restart() {
41:     stop
42:     sleep 1
43:     start
44: }
45:
46: case "$1" in
47:     start|stop|restart)
48:             "$1";;
49:     reload)
50:             # Restart, since there is no true "reload" feature.
51:             restart;;
52:     *)
53:             echo "Usage: $0 {start|stop|restart|reload}"
54:             exit 1
55: esac
```

Note: programs that support reloading their configuration in some
fashion (SIGHUP) should provide a reload() function similar to stop
(). The start-stop-daemon supports -K -s HUP for this. It is
recommended to always append -x "/sbin/$DAEMON" to all the
start-stop-daemon commands to ensure signals are set to a PID that
matches $DAEMON.

Both start scripts and unit files can source command line arguments
from /etc/default/foo, in general, if such a file does not exist it
should not block the start of the daemon, unless there is some site
specirfic command line argument the daemon requires to start. For
start scripts a FOO_ARGS="-s -o -m -e -args" can be defined to a
default value in and the user can override this from /etc/default/
foo.

### 18.6 具有特定构建系统的包的基础结构

By packages with specific build systems we mean all the packages
whose build system is not one of the standard ones, such as autotools
or CMake. This typically includes packages whose build system is
based on hand-written Makefiles or shell scripts.

#### 18.6.1 generic-package tutorial

```bash
01: ################################################################################
02: #
03: # libfoo
04: #
05: ################################################################################
06:
07: LIBFOO_VERSION = 1.0
08: LIBFOO_SOURCE = libfoo-$(LIBFOO_VERSION).tar.gz
09: LIBFOO_SITE = http://www.foosoftware.org/download
10: LIBFOO_LICENSE = GPL-3.0+
11: LIBFOO_LICENSE_FILES = COPYING
12: LIBFOO_INSTALL_STAGING = YES
13: LIBFOO_CONFIG_SCRIPTS = libfoo-config
14: LIBFOO_DEPENDENCIES = host-libaaa libbbb
15:
16: define LIBFOO_BUILD_CMDS
17:     $(MAKE) $(TARGET_CONFIGURE_OPTS) -C $(@D) all
18: endef
19:
20: define LIBFOO_INSTALL_STAGING_CMDS
21:     $(INSTALL) -D -m 0755 $(@D)/libfoo.a $(STAGING_DIR)/usr/lib/libfoo.a
22:     $(INSTALL) -D -m 0644 $(@D)/foo.h $(STAGING_DIR)/usr/include/foo.h
23:     $(INSTALL) -D -m 0755 $(@D)/libfoo.so* $(STAGING_DIR)/usr/lib
24: endef
25:
26: define LIBFOO_INSTALL_TARGET_CMDS
27:     $(INSTALL) -D -m 0755 $(@D)/libfoo.so* $(TARGET_DIR)/usr/lib
28:     $(INSTALL) -d -m 0755 $(TARGET_DIR)/etc/foo.d
29: endef
30:
31: define LIBFOO_USERS
32:     foo -1 libfoo -1 * - - - LibFoo daemon
33: endef
34:
35: define LIBFOO_DEVICES
36:     /dev/foo c 666 0 0 42 0 - - -
37: endef
38:
39: define LIBFOO_PERMISSIONS
40:     /bin/foo f 4755 foo libfoo - - - - -
41: endef
42:
43: $(eval $(generic-package))
```

The Makefile begins on line 7 to 11 with metadata information: the
version of the package (LIBFOO_VERSION), the name of the tarball
containing the package (LIBFOO_SOURCE) (xz-ed tarball recommended)
the Internet location at which the tarball can be downloaded from
(LIBFOO_SITE), the license (LIBFOO_LICENSE) and file with the license
text (LIBFOO_LICENSE_FILES). All variables must start with the same
prefix, LIBFOO_ in this case. This prefix is always the uppercased
version of the package name (see below to understand where the
package name is defined).

在第12行,我们指定这个包希望在登台空间中安装一些东西.库通常需要这样做,
因为它们必须在登台空间中安装头文件和其他开发文件.
这将确保LIBFOO_INSTALL_STAGING_CMDS变量中列出的命令将被执行.

On line 13, we specify that there is some fixing to be done to some
of the libfoo-config files that were installed during
LIBFOO_INSTALL_STAGING_CMDS phase. These *-config files are
executable shell script files that are located in $(STAGING_DIR)/usr/
bin directory and are executed by other 3rd party packages to find
out the location and the linking flags of this particular package.

The problem is that all these *-config files by default give wrong,
host system linking flags that are unsuitable for cross-compiling.

For example: -I/usr/include instead of -I$(STAGING_DIR)/usr/include
or: -L/usr/lib instead of -L$(STAGING_DIR)/usr/lib

So some sed magic is done to these scripts to make them give correct
flags. The argument to be given to LIBFOO_CONFIG_SCRIPTS is the file
name(s) of the shell script(s) needing fixing. All these names are
relative to $(STAGING_DIR)/usr/bin and if needed multiple names can
be given.

In addition, the scripts listed in LIBFOO_CONFIG_SCRIPTS are removed
from $(TARGET_DIR)/usr/bin, since they are not needed on the target.

Example 18.1 Config script: divine package

Package divine installs shell script $(STAGING_DIR)/usr/bin/
divine-config.

So its fixup would be:

```bash
DIVINE_CONFIG_SCRIPTS = divine-config
```

Example 18.2 Config script: imagemagick package:

Package imagemagick installs the following scripts: $(STAGING_DIR)/
usr/bin/{Magick,Magick++,MagickCore,MagickWand,Wand}-config

So it's fixup would be:

```bash
IMAGEMAGICK_CONFIG_SCRIPTS = \
   Magick-config Magick++-config \
   MagickCore-config MagickWand-config Wand-config
```

On line 14, we specify the list of dependencies this package relies
on. These dependencies are listed in terms of lower-case package
names, which can be packages for the target (without the host-
prefix) or packages for the host (with the host-) prefix). Buildroot
will ensure that all these packages are built and installed before
the current package starts its configuration.

The rest of the Makefile, lines 16..29, defines what should be done
at the different steps of the package configuration, compilation and
installation. LIBFOO_BUILD_CMDS tells what steps should be performed
to build the package. LIBFOO_INSTALL_STAGING_CMDS tells what steps
should be performed to install the package in the staging space.
LIBFOO_INSTALL_TARGET_CMDS tells what steps should be performed to
install the package in the target space.

所有这些步骤都依赖于$(@D)变量,该变量包含解压包源代码的目录.

On lines 31..33, we define a user that is used by this package (e.g.
to run a daemon as non-root) (LIBFOO_USERS).

On line 35..37, we define a device-node file used by this package
(LIBFOO_DEVICES).

On line 39..41, we define the permissions to set to specific files
installed by this package (LIBFOO_PERMISSIONS).

最后,在第43行,我们调用了generic-package函数,该函数根据前面定义的
变量生成使包工作所需的所有Makefile代码.

#### 18.6.2 generic-package reference

There are two variants of the generic target. The generic-package
macro is used for packages to be cross-compiled for the target. The
host-generic-package macro is used for host packages, natively
compiled for the host. It is possible to call both of them in a
single .mk file: once to create the rules to generate a target
package and once to create the rules to generate a host package:

```console
$(eval $(generic-package))
$(eval $(host-generic-package))
```

This might be useful if the compilation of the target package
requires some tools to be installed on the host. If the package name
is libfoo, then the name of the package for the target is also
libfoo, while the name of the package for the host is host-libfoo.
These names should be used in the DEPENDENCIES variables of other
packages, if they depend on libfoo or host-libfoo.

The call to the generic-package and/or host-generic-package macro 
must be at the end of the .mk file, after all variable definitions.
The call to host-generic-package must be after the call to
generic-package, if any.

For the target package, the generic-package uses the variables
defined by the .mk file and prefixed by the uppercased package name:
LIBFOO_*. host-generic-package uses the HOST_LIBFOO_* variables. For 
some variables, if the HOST_LIBFOO_ prefixed variable doesn't exist,
the package infrastructure uses the corresponding variable prefixed
by LIBFOO_. This is done for variables that are likely to have the
same value for both the target and host packages. See below for
details.

The list of variables that can be set in a .mk file to give metadata
information is (assuming the package name is libfoo) :

  * LIBFOO_VERSION, mandatory, must contain the version of the
    package. Note that if HOST_LIBFOO_VERSION doesn't exist, it is
    assumed to be the same as LIBFOO_VERSION. It can also be a
    revision number or a tag for packages that are fetched directly
    from their version control system. Examples:

      + a version for a release tarball: LIBFOO_VERSION = 0.1.2
      + a sha1 for a git tree: LIBFOO_VERSION =
        cb9d6aa9429e838f0e54faa3d455bcbab5eef057
      + a tag for a git tree LIBFOO_VERSION = v0.1.2

        Note: Using a branch name as FOO_VERSION is not supported,
        because it does not and can not work as people would expect
        it should:

         1. due to local caching, Buildroot will not re-fetch the
            repository, so people who expect to be able to follow the
            remote repository would be quite surprised and
            disappointed;
         2. because two builds can never be perfectly simultaneous,
            and because the remote repository may get new commits on
            the branch anytime, two users, using the same Buildroot
            tree and building the same configuration, may get
            different source, thus rendering the build non
            reproducible, and people would be quite surprised and
            disappointed.
  * LIBFOO_SOURCE may contain the name of the tarball of the package,
    which Buildroot will use to download the tarball from
    LIBFOO_SITE. If HOST_LIBFOO_SOURCE is not specified, it defaults
    to LIBFOO_SOURCE. If none are specified, then the value is
    assumed to be libfoo-$(LIBFOO_VERSION).tar.gz. Example:
    LIBFOO_SOURCE = foobar-$(LIBFOO_VERSION).tar.bz2
  * LIBFOO_PATCH may contain a space-separated list of patch file
    names, that Buildroot will download and apply to the package
    source code. If an entry contains ://, then Buildroot will assume
    it is a full URL and download the patch from this location.
    Otherwise, Buildroot will assume that the patch should be
    downloaded from LIBFOO_SITE. If HOST_LIBFOO_PATCH is not
    specified, it defaults to LIBFOO_PATCH. Note that patches that
    are included in Buildroot itself use a different mechanism: all
    files of the form *.patch present in the package directory inside
    Buildroot will be applied to the package after extraction (see
    patching a package). Finally, patches listed in the LIBFOO_PATCH
    variable are applied before the patches stored in the Buildroot
    package directory.
  * LIBFOO_SITE provides the location of the package, which can be a
    URL or a local filesystem path. HTTP, FTP and SCP are supported
    URL types for retrieving package tarballs. In these cases don't
    include a trailing slash: it will be added by Buildroot between
    the directory and the filename as appropriate. Git, Subversion,
    Mercurial, and Bazaar are supported URL types for retrieving
    packages directly from source code management systems. There is a
    helper function to make it easier to download source tarballs
    from GitHub (refer to Section 18.25.4, How to add a package from
    GitHub for details). A filesystem path may be used to specify
    either a tarball or a directory containing the package source
    code. See LIBFOO_SITE_METHOD below for more details on how
    retrieval works. Note that SCP URLs should be of the form scp://
    [user@]host:filepath, and that filepath is relative to the user's
    home directory, so you may want to prepend the path with a slash
    for absolute paths: scp://[user@]host:/absolutepath. The same
    goes for SFTP URLs. If HOST_LIBFOO_SITE is not specified, it
    defaults to LIBFOO_SITE. Examples: LIBFOO_SITE=http://
    www.libfoosoftware.org/libfoo LIBFOO_SITE=http://svn.xiph.org/
    trunk/Tremor LIBFOO_SITE=/opt/software/libfoo.tar.gz LIBFOO_SITE=
    $(TOPDIR)/../src/libfoo
  * LIBFOO_DL_OPTS is a space-separated list of additional options to
    pass to the downloader. Useful for retrieving documents with
    server-side checking for user logins and passwords, or to use a
    proxy. All download methods valid for LIBFOO_SITE_METHOD are
    supported; valid options depend on the download method (consult
    the man page for the respective download utilities).
  * LIBFOO_EXTRA_DOWNLOADS is a space-separated list of additional
    files that Buildroot should download. If an entry contains ://
    then Buildroot will assume it is a complete URL and will download
    the file using this URL. Otherwise, Buildroot will assume the
    file to be downloaded is located at LIBFOO_SITE. Buildroot will
    not do anything with those additional files, except download
    them: it will be up to the package recipe to use them from $
    (LIBFOO_DL_DIR).
  * LIBFOO_SITE_METHOD determines the method used to fetch or copy
    the package source code. In many cases, Buildroot guesses the
    method from the contents of LIBFOO_SITE and setting
    LIBFOO_SITE_METHOD is unnecessary. When HOST_LIBFOO_SITE_METHOD
    is not specified, it defaults to the value of LIBFOO_SITE_METHOD.
    The possible values of LIBFOO_SITE_METHOD are:

      + wget for normal FTP/HTTP downloads of tarballs. Used by
        default when LIBFOO_SITE begins with http://, https:// or
        ftp://.
      + scp for downloads of tarballs over SSH with scp. Used by
        default when LIBFOO_SITE begins with scp://.
      + sftp for downloads of tarballs over SSH with sftp. Used by
        default when LIBFOO_SITE begins with sftp://.
      + svn for retrieving source code from a Subversion repository.
        Used by default when LIBFOO_SITE begins with svn://. When a
        http:// Subversion repository URL is specified in
        LIBFOO_SITE, one must specify LIBFOO_SITE_METHOD=svn.
        Buildroot performs a checkout which is preserved as a tarball
        in the download cache; subsequent builds use the tarball
        instead of performing another checkout.
      + cvs for retrieving source code from a CVS repository. Used by
        default when LIBFOO_SITE begins with cvs://. The downloaded
        source code is cached as with the svn method. Anonymous
        pserver mode is assumed otherwise explicitly defined on
        LIBFOO_SITE. Both LIBFOO_SITE=cvs://libfoo.net:/cvsroot/
        libfoo and LIBFOO_SITE=cvs://:ext:libfoo.net:/cvsroot/libfoo
        are accepted, on the former anonymous pserver access mode is
        assumed. LIBFOO_SITE must contain the source URL as well as
        the remote repository directory. The module is the package
        name. LIBFOO_VERSION is mandatory and must be a tag, a
        branch, or a date (e.g. "2014-10-20", "2014-10-20 13:45",
        "2014-10-20 13:45+01" see "man cvs" for further details).
      + git for retrieving source code from a Git repository. Used by
        default when LIBFOO_SITE begins with git://. The downloaded
        source code is cached as with the svn method.
      + hg for retrieving source code from a Mercurial repository.
        One must specify LIBFOO_SITE_METHOD=hg when LIBFOO_SITE
        contains a Mercurial repository URL. The downloaded source
        code is cached as with the svn method.
      + bzr for retrieving source code from a Bazaar repository. Used
        by default when LIBFOO_SITE begins with bzr://. The
        downloaded source code is cached as with the svn method.
      + file for a local tarball. One should use this when
        LIBFOO_SITE specifies a package tarball as a local filename.
        Useful for software that isn't available publicly or in
        version control.
      + local for a local source code directory. One should use this
        when LIBFOO_SITE specifies a local directory path containing
        the package source code. Buildroot copies the contents of the
        source directory into the package's build directory. Note
        that for local packages, no patches are applied. If you need
        to still patch the source code, use LIBFOO_POST_RSYNC_HOOKS,
        see Section 18.23.1, Using the POST_RSYNC hook.
  * LIBFOO_GIT_SUBMODULES can be set to YES to create an archive with
    the git submodules in the repository. This is only available for
    packages downloaded with git (i.e. when LIBFOO_SITE_METHOD=git).
    Note that we try not to use such git submodules when they contain
    bundled libraries, in which case we prefer to use those libraries
    from their own package.
  * LIBFOO_GIT_LFS should be set to YES if the Git repository uses
    Git LFS to store large files out of band. This is only available
    for packages downloaded with git (i.e. when LIBFOO_SITE_METHOD=
    git).
  * LIBFOO_STRIP_COMPONENTS is the number of leading components
    (directories) that tar must strip from file names on extraction.
    The tarball for most packages has one leading component named "
    <pkg-name>-<pkg-version>", thus Buildroot passes
    --strip-components=1 to tar to remove it. For non-standard
    packages that don't have this component, or that have more than
    one leading component to strip, set this variable with the value
    to be passed to tar. Default: 1.
  * LIBFOO_EXCLUDES is a space-separated list of patterns to exclude
    when extracting the archive. Each item from that list is passed
    as a tar's --exclude option. By default, empty.
  * LIBFOO_DEPENDENCIES lists the dependencies (in terms of package
    name) that are required for the current target package to
    compile. These dependencies are guaranteed to be compiled and
    installed before the configuration of the current package starts.
    However, modifications to configuration of these dependencies
    will not force a rebuild of the current package. In a similar
    way, HOST_LIBFOO_DEPENDENCIES lists the dependencies for the
    current host package.
  * LIBFOO_EXTRACT_DEPENDENCIES lists the dependencies (in terms of
    package name) that are required for the current target package to
    be extracted. These dependencies are guaranteed to be compiled
    and installed before the extract step of the current package
    starts. This is only used internally by the package
    infrastructure, and should typically not be used directly by
    packages.
  * LIBFOO_PATCH_DEPENDENCIES lists the dependencies (in terms of
    package name) that are required for the current package to be
    patched. These dependencies are guaranteed to be extracted and
    patched (but not necessarily built) before the current package is
    patched. In a similar way, HOST_LIBFOO_PATCH_DEPENDENCIES lists
    the dependencies for the current host package. This is seldom
    used; usually, LIBFOO_DEPENDENCIES is what you really want to
    use.
  * LIBFOO_PROVIDES lists all the virtual packages libfoo is an
    implementation of. See Section 18.12, Infrastructure for virtual
    packages.
  * LIBFOO_INSTALL_STAGING can be set to YES or NO (default). If set
    to YES, then the commands in the LIBFOO_INSTALL_STAGING_CMDS
    variables are executed to install the package into the staging
    directory.
  * LIBFOO_INSTALL_TARGET can be set to YES (default) or NO. If set
    to YES, then the commands in the LIBFOO_INSTALL_TARGET_CMDS
    variables are executed to install the package into the target
    directory.
  * LIBFOO_INSTALL_IMAGES can be set to YES or NO (default). If set
    to YES, then the commands in the LIBFOO_INSTALL_IMAGES_CMDS
    variable are executed to install the package into the images
    directory.
  * LIBFOO_CONFIG_SCRIPTS lists the names of the files in $
    (STAGING_DIR)/usr/bin that need some special fixing to make them
    cross-compiling friendly. Multiple file names separated by space
    can be given and all are relative to $(STAGING_DIR)/usr/bin. The
    files listed in LIBFOO_CONFIG_SCRIPTS are also removed from $
    (TARGET_DIR)/usr/bin since they are not needed on the target.
  * LIBFOO_DEVICES lists the device files to be created by Buildroot
    when using the static device table. The syntax to use is the
    makedevs one. You can find some documentation for this syntax in
    the Chapter 25, Makedev syntax documentation. This variable is
    optional.
  * LIBFOO_PERMISSIONS lists the changes of permissions to be done at
    the end of the build process. The syntax is once again the
    makedevs one. You can find some documentation for this syntax in
    the Chapter 25, Makedev syntax documentation. This variable is
    optional.
  * LIBFOO_USERS lists the users to create for this package, if it
    installs a program you want to run as a specific user (e.g. as a
    daemon, or as a cron-job). The syntax is similar in spirit to the
    makedevs one, and is described in the Chapter 26, Makeusers
    syntax documentation. This variable is optional.
  * LIBFOO_LICENSE defines the license (or licenses) under which the
    package is released. This name will appear in the manifest file
    produced by make legal-info. If the license appears in the SPDX
    License List [https://spdx.org/licenses/], use the SPDX short
    identifier to make the manifest file uniform. Otherwise, describe
    the license in a precise and concise way, avoiding ambiguous
    names such as BSD which actually name a family of licenses. This
    variable is optional. If it is not defined, unknown will appear
    in the license field of the manifest file for this package. The
    expected format for this variable must comply with the following
    rules:

      + If different parts of the package are released under
        different licenses, then comma separate licenses (e.g.
        LIBFOO_LICENSE = GPL-2.0+, LGPL-2.1+). If there is clear
        distinction between which component is licensed under what
        license, then annotate the license with that component,
        between parenthesis (e.g. LIBFOO_LICENSE = GPL-2.0+
        (programs), LGPL-2.1+ (libraries)).
      + If some licenses are conditioned on a sub-option being
        enabled, append the conditional licenses with a comma (e.g.:
        FOO_LICENSE += , GPL-2.0+ (programs)); the infrastructure
        will internally remove the space before the comma.
      + If the package is dual licensed, then separate licenses with
        the or keyword (e.g. LIBFOO_LICENSE = AFL-2.1 or GPL-2.0+).
  * LIBFOO_LICENSE_FILES is a space-separated list of files in the
    package tarball that contain the license(s) under which the
    package is released. make legal-info copies all of these files in
    the legal-info directory. See Chapter 13, Legal notice and
    licensing for more information. This variable is optional. If it
    is not defined, a warning will be produced to let you know, and
    not saved will appear in the license files field of the manifest
    file for this package.
  * LIBFOO_ACTUAL_SOURCE_TARBALL only applies to packages whose
    LIBFOO_SITE / LIBFOO_SOURCE pair points to an archive that does
    not actually contain source code, but binary code. This a very
    uncommon case, only known to apply to external toolchains which
    come already compiled, although theoretically it might apply to
    other packages. In such cases a separate tarball is usually
    available with the actual source code. Set
    LIBFOO_ACTUAL_SOURCE_TARBALL to the name of the actual source
    code archive and Buildroot will download it and use it when you
    run make legal-info to collect legally-relevant material. Note
    this file will not be downloaded during regular builds nor by
    make source.
  * LIBFOO_ACTUAL_SOURCE_SITE provides the location of the actual
    source tarball. The default value is LIBFOO_SITE, so you don't
    need to set this variable if the binary and source archives are
    hosted on the same directory. If LIBFOO_ACTUAL_SOURCE_TARBALL is
    not set, it doesn't make sense to define
    LIBFOO_ACTUAL_SOURCE_SITE.
  * LIBFOO_REDISTRIBUTE can be set to YES (default) or NO to indicate
    if the package source code is allowed to be redistributed. Set it
    to NO for non-opensource packages: Buildroot will not save the
    source code for this package when collecting the legal-info.
  * LIBFOO_FLAT_STACKSIZE defines the stack size of an application
    built into the FLAT binary format. The application stack size on
    the NOMMU architecture processors cann't be enlarged at run time.
    The default stack size for the FLAT binary format is only 4k
    bytes. If the application consumes more stack, append the
    required number here.
  * LIBFOO_BIN_ARCH_EXCLUDE is a space-separated list of paths
    (relative to the target directory) to ignore when checking that
    the package installs correctly cross-compiled binaries. You
    seldom need to set this variable, unless the package installs
    binary blobs outside the default locations, /lib/firmware, /usr/
    lib/firmware, /lib/modules, /usr/lib/modules, and /usr/share,
    which are automatically excluded.
  * LIBFOO_IGNORE_CVES is a space-separated list of CVEs that tells
    Buildroot CVE tracking tools which CVEs should be ignored for
    this package. This is typically used when the CVE is fixed by a
    patch in the package, or when the CVE for some reason does not
    affect the Buildroot package. A Makefile comment must always
    precede the addition of a CVE to this variable. Example:

```bash
# 0001-fix-cve-2020-12345.patch
LIBFOO_IGNORE_CVES += CVE-2020-12345
# only when built with libbaz, which Buildroot doesn't support
LIBFOO_IGNORE_CVES += CVE-2020-54321
```

  * LIBFOO_CPE_ID_* variables is a set of variables that allows the
    package to define its CPE identifier [https://nvd.nist.gov/
    products/cpe]. The available variables are:

      + LIBFOO_CPE_ID_PREFIX, specifies the prefix of the CPE
        identifier, i.e the first three fields. When not defined, the
        default value is cpe:2.3:a.
      + LIBFOO_CPE_ID_VENDOR, specifies the vendor part of the CPE
        identifier. When not defined, the default value is <pkgname>
        _project.
      + LIBFOO_CPE_ID_PRODUCT, specifies the product part of the CPE
        identifier. When not defined, the default value is <pkgname>.
      + LIBFOO_CPE_ID_VERSION, specifies the version part of the CPE
        identifier. When not defined the default value is $
        (LIBFOO_VERSION).
      + LIBFOO_CPE_ID_UPDATE specifies the update part of the CPE
        identifier. When not defined the default value is *.

    If any of those variables is defined, then the generic package
    infrastructure assumes the package provides valid CPE
    information. In this case, the generic package infrastructure
    will define LIBFOO_CPE_ID.

    For a host package, if its LIBFOO_CPE_ID_* variables are not
    defined, it inherits the value of those variables from the
    corresponding target package.

定义这些变量的建议方法是使用以下语法:

```bash
LIBFOO_VERSION = 2.32
```

现在,变量定义在构建过程的不同步骤中应该执行什么.

  * LIBFOO_EXTRACT_CMDS lists the actions to be performed to extract
    the package. This is generally not needed as tarballs are
    automatically handled by Buildroot. However, if the package uses
    a non-standard archive format, such as a ZIP or RAR file, or has
    a tarball with a non-standard organization, this variable allows
    to override the package infrastructure default behavior.
  * LIBFOO_CONFIGURE_CMDS lists the actions to be performed to
    configure the package before its compilation.
  * LIBFOO_BUILD_CMDS lists the actions to be performed to compile
    the package.
  * HOST_LIBFOO_INSTALL_CMDS lists the actions to be performed to
    install the package, when the package is a host package. The
    package must install its files to the directory given by $
    (HOST_DIR). All files, including development files such as
    headers should be installed, since other packages might be
    compiled on top of this package.
  * LIBFOO_INSTALL_TARGET_CMDS lists the actions to be performed to
    install the package to the target directory, when the package is
    a target package. The package must install its files to the
    directory given by $(TARGET_DIR). Only the files required for 
    execution of the package have to be installed. Header files,
    static libraries and documentation will be removed again when the
    target filesystem is finalized.
  * LIBFOO_INSTALL_STAGING_CMDS lists the actions to be performed to
    install the package to the staging directory, when the package is
    a target package. The package must install its files to the
    directory given by $(STAGING_DIR). All development files should
    be installed, since they might be needed to compile other
    packages.
  * LIBFOO_INSTALL_IMAGES_CMDS lists the actions to be performed to
    install the package to the images directory, when the package is
    a target package. The package must install its files to the
    directory given by $(BINARIES_DIR). Only files that are binary
    images (aka images) that do not belong in the TARGET_DIR but are
    necessary for booting the board should be placed here. For
    example, a package should utilize this step if it has binaries
    which would be similar to the kernel image, bootloader or root
    filesystem images.
  * LIBFOO_INSTALL_INIT_SYSV, LIBFOO_INSTALL_INIT_OPENRC and
    LIBFOO_INSTALL_INIT_SYSTEMD list the actions to install init
    scripts either for the systemV-like init systems (busybox,
    sysvinit, etc.), openrc or for the systemd units. These commands
    will be run only when the relevant init system is installed (i.e.
    if systemd is selected as the init system in the configuration,
    only LIBFOO_INSTALL_INIT_SYSTEMD will be run). The only exception
    is when openrc is chosen as init system and
    LIBFOO_INSTALL_INIT_OPENRC has not been set, in such situation
    LIBFOO_INSTALL_INIT_SYSV will be called, since openrc supports
    sysv init scripts. When systemd is used as the init system,
    buildroot will automatically enable all services using the
    systemctl preset-all command in the final phase of image
    building. You can add preset files to prevent a particular unit
    from being automatically enabled by buildroot.
  * LIBFOO_HELP_CMDS lists the actions to print the package help,
    which is included to the main make help output. These commands
    can print anything in any format. This is seldom used, as
    packages rarely have custom rules. Do not use this variable,
    unless you really know that you need to print help.
  * LIBFOO_LINUX_CONFIG_FIXUPS lists the Linux kernel configuration
    options that are needed to build and use this package, and
    without which the package is fundamentally broken. This shall be
    a set of calls to one of the kconfig tweaking option:
    KCONFIG_ENABLE_OPT, KCONFIG_DISABLE_OPT, or KCONFIG_SET_OPT. This
    is seldom used, as package usually have no strict requirements on
    the kernel options.

The preferred way to define these variables is:

```bash
define LIBFOO_CONFIGURE_CMDS
        action 1
        action 2
        action 3
endef
```

In the action definitions, you can use the following variables:

  * $(LIBFOO_PKGDIR) contains the path to the directory containing
    the libfoo.mk and Config.in files. This variable is useful when
    it is necessary to install a file bundled in Buildroot, like a
    runtime configuration file, a splashscreen image
  * $(@D), which contains the directory in which the package source
    code has been uncompressed.
  * $(LIBFOO_DL_DIR) contains the path to the directory where all the
    downloads made by Buildroot for libfoo are stored in.
  * $(TARGET_CC), $(TARGET_LD), etc. to get the target
    cross-compilation utilities
  * $(TARGET_CROSS) to get the cross-compilation toolchain prefix
  * Of course the $(HOST_DIR), $(STAGING_DIR) and $(TARGET_DIR)
    variables to install the packages properly. Those variables point
    to the global host, staging and target directories, unless 
    per-package directory support is used, in which case they point
    to the current package host, staging and target directories. In
    both cases, it doesn't make any difference from the package point
    of view: it should simply use HOST_DIR, STAGING_DIR and
    TARGET_DIR. See Section 8.12, Top-level parallel build for more
    details about per-package directory support.

最后,您还可以使用钩子.有关更多信息,请参阅第18.23节,各种构建步骤中可用的钩子.

### 18.7 autotools-based包基础架构

#### 18.7.1 autotools-package教程

首先,让我们通过一个示例来了解如何为基于自动工具的包编写.mk文件:

```bash
01: ################################################################################
02: #
03: # libfoo
04: #
05: ################################################################################
06:
07: LIBFOO_VERSION = 1.0
08: LIBFOO_SOURCE = libfoo-$(LIBFOO_VERSION).tar.gz
09: LIBFOO_SITE = http://www.foosoftware.org/download
10: LIBFOO_INSTALL_STAGING = YES
11: LIBFOO_INSTALL_TARGET = NO
12: LIBFOO_CONF_OPTS = --disable-shared
13: LIBFOO_DEPENDENCIES = libglib2 host-pkgconf
14:
15: $(eval $(autotools-package))
```

在第7行,我们声明了包的版本.

在第8行和第9行,我们声明了tarball的名称(推荐使用xz-ed的tarball)和
该tarball在Web上的位置.Buildroot将从这个位置自动下载压缩文件.

在第10行,我们告诉Buildroot将包安装到临时目录.staging目录位于
output/staging/中,它是安装所有包的目录,包括它们的开发文件等.默认情况下,
包不会安装到暂存目录,因为通常只需要在暂存目录中安装库:需要它们的开发文件来
编译依赖于它们的其他库或应用程序.同样在默认情况下,当启用临时安装时,
使用make install命令将包安装在此位置.

在第11行,我们告诉Buildroot不要将包安装到目标目录.这个目录包含将成为在目标上
运行的根文件系统的内容.对于纯静态库,没有必要将它们安装在目标目录中,因为它们
在运行时不会被使用.默认情况下,目标安装是启用的;将这个变量设置为NO几乎是不需要的.
同样在默认情况下,使用make install命令将包安装在此位置.

在第12行,我们告诉Buildroot传递一个自定义配置选项,
该选项将在配置和构建包之前传递给./configure脚本.

在第13行,我们声明了依赖项,以便在包的构建过程开始之前构建它们.

最后,在第15行,我们调用autotools-package宏,
该宏生成所有允许构建包的Makefile规则.

#### 18.7.2 autotools-package reference

The main macro of the autotools package infrastructure is
autotools-package. It is similar to the generic-package macro. The
ability to have target and host packages is also available, with the
host-autotools-package macro.

Just like the generic infrastructure, the autotools infrastructure
works by defining a number of variables before calling the
autotools-package macro.

First, all the package metadata information variables that exist in
the generic infrastructure also exist in the autotools
infrastructure: LIBFOO_VERSION, LIBFOO_SOURCE, LIBFOO_PATCH,
LIBFOO_SITE, LIBFOO_SUBDIR, LIBFOO_DEPENDENCIES,
LIBFOO_INSTALL_STAGING, LIBFOO_INSTALL_TARGET.

A few additional variables, specific to the autotools infrastructure,
can also be defined. Many of them are only useful in very specific
cases, typical packages will therefore only use a few of them.

  * LIBFOO_SUBDIR may contain the name of a subdirectory inside the
    package that contains the configure script. This is useful, if
    for example, the main configure script is not at the root of the
    tree extracted by the tarball. If HOST_LIBFOO_SUBDIR is not
    specified, it defaults to LIBFOO_SUBDIR.
  * LIBFOO_CONF_ENV, to specify additional environment variables to
    pass to the configure script. By default, empty.
  * LIBFOO_CONF_OPTS, to specify additional configure options to pass
    to the configure script. By default, empty.
  * LIBFOO_MAKE, to specify an alternate make command. This is
    typically useful when parallel make is enabled in the
    configuration (using BR2_JLEVEL) but that this feature should be
    disabled for the given package, for one reason or another. By
    default, set to $(MAKE). If parallel building is not supported by
    the package, then it should be set to LIBFOO_MAKE=$(MAKE1).
  * LIBFOO_MAKE_ENV, to specify additional environment variables to
    pass to make in the build step. These are passed before the make
    command. By default, empty.
  * LIBFOO_MAKE_OPTS, to specify additional variables to pass to make
    in the build step. These are passed after the make command. By
    default, empty.
  * LIBFOO_AUTORECONF, tells whether the package should be
    autoreconfigured or not (i.e. if the configure script and
    Makefile.in files should be re-generated by re-running autoconf,
    automake, libtool, etc.). Valid values are YES and NO. By
    default, the value is NO
  * LIBFOO_AUTORECONF_ENV, to specify additional environment
    variables to pass to the autoreconf program if LIBFOO_AUTORECONF=
    YES. These are passed in the environment of the autoreconf
    command. By default, empty.
  * LIBFOO_AUTORECONF_OPTS to specify additional options passed to
    the autoreconf program if LIBFOO_AUTORECONF=YES. By default,
    empty.
  * LIBFOO_GETTEXTIZE, tells whether the package should be
    gettextized or not (i.e. if the package uses a different gettext
    version than Buildroot provides, and it is needed to run 
    gettextize.) Only valid when LIBFOO_AUTORECONF=YES. Valid values
    are YES and NO. The default is NO.
  * LIBFOO_GETTEXTIZE_OPTS, to specify additional options passed to
    the gettextize program, if LIBFOO_GETTEXTIZE=YES. You may use
    that if, for example, the .po files are not located in the
    standard place (i.e. in po/ at the root of the package.) By
    default, -f.
  * LIBFOO_LIBTOOL_PATCH tells whether the Buildroot patch to fix
    libtool cross-compilation issues should be applied or not. Valid
    values are YES and NO. By default, the value is YES
  * LIBFOO_INSTALL_STAGING_OPTS contains the make options used to
    install the package to the staging directory. By default, the
    value is DESTDIR=$(STAGING_DIR) install, which is correct for
    most autotools packages. It is still possible to override it.
  * LIBFOO_INSTALL_TARGET_OPTS contains the make options used to
    install the package to the target directory. By default, the
    value is DESTDIR=$(TARGET_DIR) install. The default value is
    correct for most autotools packages, but it is still possible to
    override it if needed.

With the autotools infrastructure, all the steps required to build
and install the packages are already defined, and they generally work
well for most autotools-based packages. However, when required, it is
still possible to customize what is done in any particular step:

  * By adding a post-operation hook (after extract, patch, configure,
    build or install). See Section 18.23, Hooks available in the
    various build steps for details.
  * By overriding one of the steps. For example, even if the
    autotools infrastructure is used, if the package .mk file defines
    its own LIBFOO_CONFIGURE_CMDS variable, it will be used instead
    of the default autotools one. However, using this method should
    be restricted to very specific cases. Do not use it in the
    general case.

### 18.8 CMake-based包基础架构

#### 18.8.1 cmake-package教程

First, let's see how to write a .mk file for a CMake-based package,
with an example :

```bash
01: ################################################################################
02: #
03: # libfoo
04: #
05: ################################################################################
06:
07: LIBFOO_VERSION = 1.0
08: LIBFOO_SOURCE = libfoo-$(LIBFOO_VERSION).tar.gz
09: LIBFOO_SITE = http://www.foosoftware.org/download
10: LIBFOO_INSTALL_STAGING = YES
11: LIBFOO_INSTALL_TARGET = NO
12: LIBFOO_CONF_OPTS = -DBUILD_DEMOS=ON
13: LIBFOO_DEPENDENCIES = libglib2 host-pkgconf
14:
15: $(eval $(cmake-package))
```

在第7行,我们声明了包的版本.

On line 8 and 9, we declare the name of the tarball (xz-ed tarball
recommended) and the location of the tarball on the Web. Buildroot
will automatically download the tarball from this location.

On line 10, we tell Buildroot to install the package to the staging
directory. The staging directory, located in output/staging/ is the
directory where all the packages are installed, including their
development files, etc. By default, packages are not installed to the
staging directory, since usually, only libraries need to be installed
in the staging directory: their development files are needed to
compile other libraries or applications depending on them. Also by
default, when staging installation is enabled, packages are installed
in this location using the make install command.

On line 11, we tell Buildroot to not install the package to the
target directory. This directory contains what will become the root
filesystem running on the target. For purely static libraries, it is
not necessary to install them in the target directory because they
will not be used at runtime. By default, target installation is
enabled; setting this variable to NO is almost never needed. Also by
default, packages are installed in this location using the make
install command.

在第12行,我们告诉Buildroot在配置包时将自定义选项传递给CMake.

On line 13, we declare our dependencies, so that they are built
before the build process of our package starts.

Finally, on line line 15, we invoke the cmake-package macro that
generates all the Makefile rules that actually allows the package to
be built.

#### 18.8.2 cmake-package reference

The main macro of the CMake package infrastructure is cmake-package.
It is similar to the generic-package macro. The ability to have
target and host packages is also available, with the
host-cmake-package macro.

就像通用的基础架构一样,CMake基础架构的工作方式是在调用cmake-package宏之前定义许多变量.

First, all the package metadata information variables that exist in
the generic infrastructure also exist in the CMake infrastructure:
LIBFOO_VERSION, LIBFOO_SOURCE, LIBFOO_PATCH, LIBFOO_SITE,
LIBFOO_SUBDIR, LIBFOO_DEPENDENCIES, LIBFOO_INSTALL_STAGING,
LIBFOO_INSTALL_TARGET.

A few additional variables, specific to the CMake infrastructure, can
also be defined. Many of them are only useful in very specific cases,
typical packages will therefore only use a few of them.

  * LIBFOO_SUBDIR may contain the name of a subdirectory inside the
    package that contains the main CMakeLists.txt file. This is
    useful, if for example, the main CMakeLists.txt file is not at
    the root of the tree extracted by the tarball. If
    HOST_LIBFOO_SUBDIR is not specified, it defaults to
    LIBFOO_SUBDIR.
  * LIBFOO_CONF_ENV, to specify additional environment variables to
    pass to CMake. By default, empty.
  * LIBFOO_CONF_OPTS, to specify additional configure options to pass
    to CMake. By default, empty. A number of common CMake options are
    set by the cmake-package infrastructure; so it is normally not
    necessary to set them in the package's *.mk file unless you want
    to override them:

      + CMAKE_BUILD_TYPE is driven by BR2_ENABLE_RUNTIME_DEBUG;
      + CMAKE_INSTALL_PREFIX;
      + BUILD_SHARED_LIBS is driven by BR2_STATIC_LIBS;
      + BUILD_DOC, BUILD_DOCS are disabled;
      + BUILD_EXAMPLE, BUILD_EXAMPLES are disabled;
      + BUILD_TEST, BUILD_TESTS, BUILD_TESTING are disabled.
  * LIBFOO_SUPPORTS_IN_SOURCE_BUILD = NO should be set when the
    package cannot be built inside the source tree but needs a
    separate build directory.
  * LIBFOO_MAKE, to specify an alternate make command. This is
    typically useful when parallel make is enabled in the
    configuration (using BR2_JLEVEL) but that this feature should be
    disabled for the given package, for one reason or another. By
    default, set to $(MAKE). If parallel building is not supported by
    the package, then it should be set to LIBFOO_MAKE=$(MAKE1).
  * LIBFOO_MAKE_ENV, to specify additional environment variables to
    pass to make in the build step. These are passed before the make
    command. By default, empty.
  * LIBFOO_MAKE_OPTS, to specify additional variables to pass to make
    in the build step. These are passed after the make command. By
    default, empty.
  * LIBFOO_INSTALL_OPTS contains the make options used to install the
    package to the host directory. By default, the value is install,
    which is correct for most CMake packages. It is still possible to
    override it.
  * LIBFOO_INSTALL_STAGING_OPTS contains the make options used to
    install the package to the staging directory. By default, the
    value is DESTDIR=$(STAGING_DIR) install/fast, which is correct
    for most CMake packages. It is still possible to override it.
  * LIBFOO_INSTALL_TARGET_OPTS contains the make options used to
    install the package to the target directory. By default, the
    value is DESTDIR=$(TARGET_DIR) install/fast. The default value is
    correct for most CMake packages, but it is still possible to
    override it if needed.

With the CMake infrastructure, all the steps required to build and
install the packages are already defined, and they generally work
well for most CMake-based packages. However, when required, it is
still possible to customize what is done in any particular step:

  * By adding a post-operation hook (after extract, patch, configure,
    build or install). See Section 18.23, Hooks available in the
    various build steps for details.
  * By overriding one of the steps. For example, even if the CMake
    infrastructure is used, if the package .mk file defines its own
    LIBFOO_CONFIGURE_CMDS variable, it will be used instead of the
    default CMake one. However, using this method should be
    restricted to very specific cases. Do not use it in the general
    case.

### 18.9 Python包基础架构

This infrastructure applies to Python packages that use the standard
Python setuptools mechanism as their build system, generally
recognizable by the usage of a setup.py script.

#### 18.9.1 python-package教程

First, let's see how to write a .mk file for a Python package, with
an example :

```bash
01: ################################################################################
02: #
03: # python-foo
04: #
05: ################################################################################
06:
07: PYTHON_FOO_VERSION = 1.0
08: PYTHON_FOO_SOURCE = python-foo-$(PYTHON_FOO_VERSION).tar.xz
09: PYTHON_FOO_SITE = http://www.foosoftware.org/download
10: PYTHON_FOO_LICENSE = BSD-3-Clause
11: PYTHON_FOO_LICENSE_FILES = LICENSE
12: PYTHON_FOO_ENV = SOME_VAR=1
13: PYTHON_FOO_DEPENDENCIES = libmad
14: PYTHON_FOO_SETUP_TYPE = distutils
15:
16: $(eval $(python-package))
```

On line 7, we declare the version of the package.

On line 8 and 9, we declare the name of the tarball (xz-ed tarball
recommended) and the location of the tarball on the Web. Buildroot
will automatically download the tarball from this location.

On line 10 and 11, we give licensing details about the package (its
license on line 10, and the file containing the license text on line
11).

On line 12, we tell Buildroot to pass custom options to the Python
setup.py script when it is configuring the package.

On line 13, we declare our dependencies, so that they are built
before the build process of our package starts.

On line 14, we declare the specific Python build system being used.
In this case the distutils Python build system is used. The two
supported ones are distutils and setuptools.

Finally, on line 16, we invoke the python-package macro that
generates all the Makefile rules that actually allow the package to
be built.

#### 18.9.2 python-package reference

As a policy, packages that merely provide Python modules should all
be named python-<something> in Buildroot. Other packages that use the
Python build system, but are not Python modules, can freely choose
their name (existing examples in Buildroot are scons and supervisor).

The main macro of the Python package infrastructure is
python-package. It is similar to the generic-package macro. It is
also possible to create Python host packages with the
host-python-package macro.

Just like the generic infrastructure, the Python infrastructure works
by defining a number of variables before calling the python-package
or host-python-package macros.

All the package metadata information variables that exist in the
generic package infrastructure also exist in the Python
infrastructure: PYTHON_FOO_VERSION, PYTHON_FOO_SOURCE,
PYTHON_FOO_PATCH, PYTHON_FOO_SITE, PYTHON_FOO_SUBDIR,
PYTHON_FOO_DEPENDENCIES, PYTHON_FOO_LICENSE,
PYTHON_FOO_LICENSE_FILES, PYTHON_FOO_INSTALL_STAGING, etc.

Note that:

  * It is not necessary to add python or host-python in the
    PYTHON_FOO_DEPENDENCIES variable of a package, since these basic
    dependencies are automatically added as needed by the Python
    package infrastructure.
  * Similarly, it is not needed to add host-setuptools to
    PYTHON_FOO_DEPENDENCIES for setuptools-based packages, since it's
    automatically added by the Python infrastructure as needed.

One variable specific to the Python infrastructure is mandatory:

  * PYTHON_FOO_SETUP_TYPE, to define which Python build system is
    used by the package. The two supported values are distutils and
    setuptools. If you don't know which one is used in your package,
    look at the setup.py file in your package source code, and see
    whether it imports things from the distutils module or the
    setuptools module.

A few additional variables, specific to the Python infrastructure,
can optionally be defined, depending on the package's needs. Many of
them are only useful in very specific cases, typical packages will
therefore only use a few of them, or none.

  * PYTHON_FOO_SUBDIR may contain the name of a subdirectory inside
    the package that contains the main setup.py file. This is useful,
    if for example, the main setup.py file is not at the root of the
    tree extracted by the tarball. If HOST_PYTHON_FOO_SUBDIR is not
    specified, it defaults to PYTHON_FOO_SUBDIR.
  * PYTHON_FOO_ENV, to specify additional environment variables to
    pass to the Python setup.py script (for both the build and
    install steps). Note that the infrastructure is automatically
    passing several standard variables, defined in
    PKG_PYTHON_DISTUTILS_ENV (for distutils target packages),
    HOST_PKG_PYTHON_DISTUTILS_ENV (for distutils host packages),
    PKG_PYTHON_SETUPTOOLS_ENV (for setuptools target packages) and
    HOST_PKG_PYTHON_SETUPTOOLS_ENV (for setuptools host packages).
  * PYTHON_FOO_BUILD_OPTS, to specify additional options to pass to
    the Python setup.py script during the build step. For target
    distutils packages, the PKG_PYTHON_DISTUTILS_BUILD_OPTS options
    are already passed automatically by the infrastructure.
  * PYTHON_FOO_INSTALL_TARGET_OPTS, PYTHON_FOO_INSTALL_STAGING_OPTS,
    HOST_PYTHON_FOO_INSTALL_OPTS to specify additional options to
    pass to the Python setup.py script during the target installation
    step, the staging installation step or the host installation,
    respectively. Note that the infrastructure is automatically
    passing some options, defined in
    PKG_PYTHON_DISTUTILS_INSTALL_TARGET_OPTS or
    PKG_PYTHON_DISTUTILS_INSTALL_STAGING_OPTS (for target distutils
    packages), HOST_PKG_PYTHON_DISTUTILS_INSTALL_OPTS (for host
    distutils packages), PKG_PYTHON_SETUPTOOLS_INSTALL_TARGET_OPTS or
    PKG_PYTHON_SETUPTOOLS_INSTALL_STAGING_OPTS (for target setuptools
    packages) and HOST_PKG_PYTHON_SETUPTOOLS_INSTALL_OPTS (for host
    setuptools packages).

With the Python infrastructure, all the steps required to build and
install the packages are already defined, and they generally work
well for most Python-based packages. However, when required, it is
still possible to customize what is done in any particular step:

  * By adding a post-operation hook (after extract, patch, configure,
    build or install). See Section 18.23, Hooks available in the
    various build steps for details.
  * By overriding one of the steps. For example, even if the Python
    infrastructure is used, if the package .mk file defines its own
    PYTHON_FOO_BUILD_CMDS variable, it will be used instead of the
    default Python one. However, using this method should be
    restricted to very specific cases. Do not use it in the general
    case.

#### 18.9.3 Generating a python-package from a PyPI repository

If the Python package for which you would like to create a Buildroot
package is available on PyPI, you may want to use the scanpypi tool
located in utils/ to automate the process.

You can find the list of existing PyPI packages here [https://
pypi.python.org].

scanpypi requires Python's setuptools package to be installed on your
host.

When at the root of your buildroot directory just do :

```console
utils/scanpypi foo bar -o package
```

This will generate packages python-foo and python-bar in the package
folder if they exist on https://pypi.python.org.

找到外部python模块菜单并将你的包插入其中.记住,菜单中的项目应该按字母顺序排列.

Please keep in mind that you'll most likely have to manually check
the package for any mistakes as there are things that cannot be
guessed by the generator (e.g. dependencies on any of the python core
modules such as BR2_PACKAGE_PYTHON_ZLIB). Also, please take note that
the license and license files are guessed and must be checked. You
also need to manually add the package to the package/Config.in file.

If your Buildroot package is not in the official Buildroot tree but
in a br2-external tree, use the -o flag as follows:

```console
utils/scanpypi foo bar -o other_package_dir
```

This will generate packages python-foo and python-bar in the
other_package_directory instead of package.

Option -h will list the available options:

```console
utils/scanpypi -h
```

#### 18.9.4 python-package CFFI backend

C Foreign Function Interface for Python (CFFI) provides a convenient
and reliable way to call compiled C code from Python using interface
declarations written in C. Python packages relying on this backend
can be identified by the appearance of a cffi dependency in the
install_requires field of their setup.py file.

Such a package should:

  * add python-cffi as a runtime dependency in order to install the
    compiled C library wrapper on the target. This is achieved by
    adding select BR2_PACKAGE_PYTHON_CFFI to the package Config.in.

```bash
config BR2_PACKAGE_PYTHON_FOO
        bool "python-foo"
        select BR2_PACKAGE_PYTHON_CFFI # runtime
```

  * add host-python-cffi as a build-time dependency in order to
    cross-compile the C wrapper. This is achieved by adding
    host-python-cffi to the PYTHON_FOO_DEPENDENCIES variable.

```bash
################################################################################
#
# python-foo
#
################################################################################

...

PYTHON_FOO_DEPENDENCIES = host-python-cffi

$(eval $(python-package))
```

### 18.10 LuaRocks-based包基础架构

#### 18.10.1 luarocks-package教程

First, let's see how to write a .mk file for a LuaRocks-based
package, with an example :

```bash
01: ################################################################################
02: #
03: # lua-foo
04: #
05: ################################################################################
06:
07: LUA_FOO_VERSION = 1.0.2-1
08: LUA_FOO_NAME_UPSTREAM = foo
09: LUA_FOO_DEPENDENCIES = bar
10:
11: LUA_FOO_BUILD_OPTS += BAR_INCDIR=$(STAGING_DIR)/usr/include
12: LUA_FOO_BUILD_OPTS += BAR_LIBDIR=$(STAGING_DIR)/usr/lib
13: LUA_FOO_LICENSE = luaFoo license
14: LUA_FOO_LICENSE_FILES = $(LUA_FOO_SUBDIR)/COPYING
15:
16: $(eval $(luarocks-package))
```

On line 7, we declare the version of the package (the same as in the
rockspec, which is the concatenation of the upstream version and the
rockspec revision, separated by a hyphen -).

On line 8, we declare that the package is called "foo" on LuaRocks.
In Buildroot, we give Lua-related packages a name that starts with
"lua", so the Buildroot name is different from the upstream name.
LUA_FOO_NAME_UPSTREAM makes the link between the two names.

On line 9, we declare our dependencies against native libraries, so
that they are built before the build process of our package starts.

On lines 11-12, we tell Buildroot to pass custom options to LuaRocks
when it is building the package.

On lines 13-14, we specify the licensing terms for the package.

Finally, on line 16, we invoke the luarocks-package macro that
generates all the Makefile rules that actually allows the package to
be built.

Most of these details can be retrieved from the rock and rockspec.
So, this file and the Config.in file can be generated by running the
command luarocks buildroot foo lua-foo in the Buildroot directory.
This command runs a specific Buildroot addon of luarocks that will
automatically generate a Buildroot package. The result must still be
manually inspected and possibly modified.

  * The package/Config.in file has to be updated manually to include
    the generated Config.in files.

#### 18.10.2 luarocks-package reference

LuaRocks is a deployment and management system for Lua modules, and
supports various build.type: builtin, make and cmake. In the context
of Buildroot, the luarocks-package infrastructure only supports the
builtin mode. LuaRocks packages that use the make or cmake build
mechanisms should instead be packaged using the generic-package and
cmake-package infrastructures in Buildroot, respectively.

The main macro of the LuaRocks package infrastructure is
luarocks-package: like generic-package it works by defining a number
of variables providing metadata information about the package, and
then calling luarocks-package.

Just like the generic infrastructure, the LuaRocks infrastructure
works by defining a number of variables before calling the
luarocks-package macro.

First, all the package metadata information variables that exist in
the generic infrastructure also exist in the LuaRocks infrastructure:
LUA_FOO_VERSION, LUA_FOO_SOURCE, LUA_FOO_SITE, LUA_FOO_DEPENDENCIES,
LUA_FOO_LICENSE, LUA_FOO_LICENSE_FILES.

Two of them are populated by the LuaRocks infrastructure (for the
download step). If your package is not hosted on the LuaRocks mirror
$(BR2_LUAROCKS_MIRROR), you can override them:

  * LUA_FOO_SITE, which defaults to $(BR2_LUAROCKS_MIRROR)
  * LUA_FOO_SOURCE, which defaults to $(lowercase
    LUA_FOO_NAME_UPSTREAM)-$(LUA_FOO_VERSION).src.rock

A few additional variables, specific to the LuaRocks infrastructure,
are also defined. They can be overridden in specific cases.

  * LUA_FOO_NAME_UPSTREAM, which defaults to lua-foo, i.e. the
    Buildroot package name
  * LUA_FOO_ROCKSPEC, which defaults to $(lowercase
    LUA_FOO_NAME_UPSTREAM)-$(LUA_FOO_VERSION).rockspec
  * LUA_FOO_SUBDIR, which defaults to $(LUA_FOO_NAME_UPSTREAM)-$
    (LUA_FOO_VERSION_WITHOUT_ROCKSPEC_REVISION)
  * LUA_FOO_BUILD_OPTS contains additional build options for the
    luarocks build call.

### 18.11 Perl/CPAN包基础架构

#### 18.11.1 perl-package教程

First, let's see how to write a .mk file for a Perl/CPAN package,
with an example :

```bash
01: ################################################################################
02: #
03: # perl-foo-bar
04: #
05: ################################################################################
06:
07: PERL_FOO_BAR_VERSION = 0.02
08: PERL_FOO_BAR_SOURCE = Foo-Bar-$(PERL_FOO_BAR_VERSION).tar.gz
09: PERL_FOO_BAR_SITE = $(BR2_CPAN_MIRROR)/authors/id/M/MO/MONGER
10: PERL_FOO_BAR_DEPENDENCIES = perl-strictures
11: PERL_FOO_BAR_LICENSE = Artistic or GPL-1.0+
12: PERL_FOO_BAR_LICENSE_FILES = LICENSE
13: PERL_FOO_BAR_DISTNAME = Foo-Bar
14:
15: $(eval $(perl-package))
```

在第7行,我们声明了包的版本.

在第8行和第9行中,我们声明了压缩包的名称和压缩包在CPAN服务器上的位置.
Buildroot将从这个位置自动下载压缩文件.

在第10行,我们声明了依赖项,以便在包的构建过程开始之前构建它们.

On line 11 and 12, we give licensing details about the package (its
license on line 11, and the file containing the license text on line
12).

On line 13, the name of the distribution as needed by the script
utils/scancpan (in order to regenerate/upgrade these package files).

最后,在第15行,我们调用perl-package宏,该宏生成实际允许构建包的所有Makefile规则.

Most of these data can be retrieved from https://metacpan.org/. So,
this file and the Config.in can be generated by running the script
utils/scancpan Foo-Bar in the Buildroot directory (or in a
br2-external tree). This script creates a Config.in file and
foo-bar.mk file for the requested package, and also recursively for
all dependencies specified by CPAN. You should still manually edit
the result. In particular, the following things should be checked.

  * If the perl module links with a shared library that is provided
    by another (non-perl) package, this dependency is not added
    automatically. It has to be added manually to
    PERL_FOO_BAR_DEPENDENCIES.
  * The package/Config.in file has to be updated manually to include
    the generated Config.in files. As a hint, the scancpan script
    prints out the required source "â€¦" statements, sorted
    alphabetically.

#### 18.11.2 perl-package reference

As a policy, packages that provide Perl/CPAN modules should all be
named perl-<something> in Buildroot.

This infrastructure handles various Perl build systems :
ExtUtils-MakeMaker (EUMM), Module-Build (MB) and Module-Build-Tiny.
Build.PL is preferred by default when a package provides a
Makefile.PL and a Build.PL.

The main macro of the Perl/CPAN package infrastructure is
perl-package. It is similar to the generic-package macro. The ability
to have target and host packages is also available, with the
host-perl-package macro.

Just like the generic infrastructure, the Perl/CPAN infrastructure
works by defining a number of variables before calling the
perl-package macro.

First, all the package metadata information variables that exist in
the generic infrastructure also exist in the Perl/CPAN
infrastructure: PERL_FOO_VERSION, PERL_FOO_SOURCE, PERL_FOO_PATCH,
PERL_FOO_SITE, PERL_FOO_SUBDIR, PERL_FOO_DEPENDENCIES,
PERL_FOO_INSTALL_TARGET.

Note that setting PERL_FOO_INSTALL_STAGING to YES has no effect
unless a PERL_FOO_INSTALL_STAGING_CMDS variable is defined. The perl
infrastructure doesn't define these commands since Perl modules
generally don't need to be installed to the staging directory.

A few additional variables, specific to the Perl/CPAN infrastructure,
can also be defined. Many of them are only useful in very specific
cases, typical packages will therefore only use a few of them.

  * PERL_FOO_PREFER_INSTALLER/HOST_PERL_FOO_PREFER_INSTALLER,
    specifies the preferred installation method. Possible values are
    EUMM (for Makefile.PL based installation using
    ExtUtils-MakeMaker) and MB (for Build.PL based installation using
    Module-Build). This variable is only used when the package
    provides both installation methods.
  * PERL_FOO_CONF_ENV/HOST_PERL_FOO_CONF_ENV, to specify additional
    environment variables to pass to the perl Makefile.PL or perl
    Build.PL. By default, empty.
  * PERL_FOO_CONF_OPTS/HOST_PERL_FOO_CONF_OPTS, to specify additional
    configure options to pass to the perl Makefile.PL or perl
    Build.PL. By default, empty.
  * PERL_FOO_BUILD_OPTS/HOST_PERL_FOO_BUILD_OPTS, to specify
    additional options to pass to make pure_all or perl Build build
    in the build step. By default, empty.
  * PERL_FOO_INSTALL_TARGET_OPTS, to specify additional options to
    pass to make pure_install or perl Build install in the install
    step. By default, empty.
  * HOST_PERL_FOO_INSTALL_OPTS, to specify additional options to pass
    to make pure_install or perl Build install in the install step.
    By default, empty.

### 18.12 virtual包基础架构

在Buildroot中,虚拟包的功能是由一个或多个包提供的,这些包被称为提供程序.
虚拟包管理是一种可扩展的机制,允许用户选择rootfs中使用的提供者.

例如,OpenGL ES是一个用于嵌入式系统上的2D和3D图形的API.对于全赢科技Sunxi
和德州仪器OMAP35xx平台,这个API的实现是不同的.所以libgles将会是一个虚拟包,
而sunxi-mali-utgard和ti-gfx将会是提供商.

#### 18.12.1 virtual-package tutorial

In the following example, we will explain how to add a new virtual
package (something-virtual) and a provider for it (some-provider).

First, let's create the virtual package.

#### 18.12.2 Virtual package's Config.in file

The Config.in file of virtual package something-virtual should
contain:

```bash
01: config BR2_PACKAGE_HAS_SOMETHING_VIRTUAL
02:     bool
03:
04: config BR2_PACKAGE_PROVIDES_SOMETHING_VIRTUAL
05:     depends on BR2_PACKAGE_HAS_SOMETHING_VIRTUAL
06:     string
```

In this file, we declare two options,
BR2_PACKAGE_HAS_SOMETHING_VIRTUAL and
BR2_PACKAGE_PROVIDES_SOMETHING_VIRTUAL, whose values will be used by
the providers.

#### 18.12.3 Virtual package's .mk file

The .mk for the virtual package should just evaluate the
virtual-package macro:

```bash
01: ################################################################################
02: #
03: # something-virtual
04: #
05: ################################################################################
06:
07: $(eval $(virtual-package))
```

The ability to have target and host packages is also available, with
the host-virtual-package macro.

#### 18.12.4 Provider's Config.in file

When adding a package as a provider, only the Config.in file requires
some modifications.

The Config.in file of the package some-provider, which provides the
functionalities of something-virtual, should contain:

```bash
01: config BR2_PACKAGE_SOME_PROVIDER
02:     bool "some-provider"
03:     select BR2_PACKAGE_HAS_SOMETHING_VIRTUAL
04:     help
05:       This is a comment that explains what some-provider is.
06:
07:       http://foosoftware.org/some-provider/
08:
09: if BR2_PACKAGE_SOME_PROVIDER
10: config BR2_PACKAGE_PROVIDES_SOMETHING_VIRTUAL
11:     default "some-provider"
12: endif
```

On line 3, we select BR2_PACKAGE_HAS_SOMETHING_VIRTUAL, and on line
11, we set the value of BR2_PACKAGE_PROVIDES_SOMETHING_VIRTUAL to the
name of the provider, but only if it is selected.

#### 18.12.5 Provider's .mk file

The .mk file should also declare an additional variable
SOME_PROVIDER_PROVIDES to contain the names of all the virtual
packages it is an implementation of:

```bash
01: SOME_PROVIDER_PROVIDES = something-virtual
```

Of course, do not forget to add the proper build and runtime
dependencies for this package!

#### 18.12.6 Notes on depending on a virtual package

When adding a package that requires a certain FEATURE provided by a
virtual package, you have to use depends on BR2_PACKAGE_HAS_FEATURE,
like so:

```bash
config BR2_PACKAGE_HAS_FEATURE
    bool

config BR2_PACKAGE_FOO
    bool "foo"
    depends on BR2_PACKAGE_HAS_FEATURE
```

#### 18.12.7 Notes on depending on a specific provider

If your package really requires a specific provider, then you'll have
to make your package depends on this provider; you can not select a
provider.

Let's take an example with two providers for a FEATURE:

```bash
config BR2_PACKAGE_HAS_FEATURE
    bool

config BR2_PACKAGE_FOO
    bool "foo"
    select BR2_PACKAGE_HAS_FEATURE

config BR2_PACKAGE_BAR
    bool "bar"
    select BR2_PACKAGE_HAS_FEATURE
```

And you are adding a package that needs FEATURE as provided by foo,
but not as provided by bar.

如果您使用select BR2_PACKAGE_FOO,那么用户仍然可以在菜单配置中选择BR2_PACKAGE_BAR.
这将导致配置不一致,因此同一特性的两个提供者将同时启用,
一个由用户显式设置,另一个由您的选择隐式设置.

Instead, you have to use depends on BR2_PACKAGE_FOO, which avoids any
implicit configuration inconsistency.

### 18.13 包的基础架构使用kconfig配置文件

A popular way for a software package to handle user-specified
configuration is kconfig. Among others, it is used by the Linux
kernel, Busybox, and Buildroot itself. The presence of a .config file
and a menuconfig target are two well-known symptoms of kconfig being
used.

Buildroot features an infrastructure for packages that use kconfig
for their configuration. This infrastructure provides the necessary
logic to expose the package's menuconfig target as foo-menuconfig in
Buildroot, and to handle the copying back and forth of the
configuration file in a correct way.

The kconfig-package infrastructure is based on the generic-package
infrastructure. All variables supported by generic-package are
available in kconfig-package as well. See Section 18.6.2,
generic-package reference for more details.

In order to use the kconfig-package infrastructure for a Buildroot
package, the minimally required lines in the .mk file, in addition to
the variables required by the generic-package infrastructure, are:

FOO_KCONFIG_FILE = reference-to-source-configuration-file

```bash
$(eval $(kconfig-package))
```

This snippet creates the following make targets:

  * foo-menuconfig, which calls the package's menuconfig target
  * foo-update-config, which copies the configuration back to the
    source configuration file. It is not possible to use this target
    when fragment files are set.
  * foo-update-defconfig, which copies the configuration back to the
    source configuration file. The configuration file will only list
    the options that differ from the default values. It is not
    possible to use this target when fragment files are set.
  * foo-diff-config, which outputs the differences between the
    current configuration and the one defined in the Buildroot
    configuration for this kconfig package. The output is useful to
    identify the configuration changes that may have to be propagated
    to configuration fragments for example.

and ensures that the source configuration file is copied to the build
directory at the right moment.

There are two options to specify a configuration file to use, either
FOO_KCONFIG_FILE (as in the example, above) or FOO_KCONFIG_DEFCONFIG.
It is mandatory to provide either, but not both:

  * FOO_KCONFIG_FILE specifies the path to a defconfig or full-config
    file to be used to configure the package.
  * FOO_KCONFIG_DEFCONFIG specifies the defconfig make rule to call
    to configure the package.

In addition to these minimally required lines, several optional
variables can be set to suit the needs of the package under
consideration:

  * FOO_KCONFIG_EDITORS: a space-separated list of kconfig editors to
    support, for example menuconfig xconfig. By default, menuconfig.
  * FOO_KCONFIG_FRAGMENT_FILES: a space-separated list of
    configuration fragment files that are merged to the main
    configuration file. Fragment files are typically used when there
    is a desire to stay in sync with an upstream (def)config file,
    with some minor modifications.
  * FOO_KCONFIG_OPTS: extra options to pass when calling the kconfig
    editors. This may need to include $(FOO_MAKE_OPTS), for example.
    By default, empty.
  * FOO_KCONFIG_FIXUP_CMDS: a list of shell commands needed to fixup
    the configuration file after copying it or running a kconfig
    editor. Such commands may be needed to ensure a configuration
    consistent with other configuration of Buildroot, for example. By
    default, empty.
  * FOO_KCONFIG_DOTCONFIG: path (with filename) of the .config file,
    relative to the package source tree. The default, .config, should
    be well suited for all packages that use the standard kconfig
    infrastructure as inherited from the Linux kernel; some packages
    use a derivative of kconfig that use a different location.
  * FOO_KCONFIG_DEPENDENCIES: the list of packages (most probably,
    host packages) that need to be built before this package's
    kconfig is interpreted. Seldom used. By default, empty.
  * FOO_KCONFIG_SUPPORTS_DEFCONFIG: whether the package's kconfig
    system supports using defconfig files; few packages do not. By
    default, YES.

### 18.14 rebar-based包基础架构

#### 18.14.1 rebar-package教程

First, let's see how to write a .mk file for a rebar-based package,
with an example :

```bash
01: ################################################################################
02: #
03: # erlang-foobar
04: #
05: ################################################################################
06:
07: ERLANG_FOOBAR_VERSION = 1.0
08: ERLANG_FOOBAR_SOURCE = erlang-foobar-$(ERLANG_FOOBAR_VERSION).tar.xz
09: ERLANG_FOOBAR_SITE = http://www.foosoftware.org/download
10: ERLANG_FOOBAR_DEPENDENCIES = host-libaaa libbbb
11:
12: $(eval $(rebar-package))
```

On line 7, we declare the version of the package.

On line 8 and 9, we declare the name of the tarball (xz-ed tarball
recommended) and the location of the tarball on the Web. Buildroot
will automatically download the tarball from this location.

On line 10, we declare our dependencies, so that they are built
before the build process of our package starts.

Finally, on line 12, we invoke the rebar-package macro that generates
all the Makefile rules that actually allows the package to be built.

18.14.2 rebar-package reference

The main macro of the rebar package infrastructure is rebar-package.
It is similar to the generic-package macro. The ability to have host
packages is also available, with the host-rebar-package macro.

Just like the generic infrastructure, the rebar infrastructure works
by defining a number of variables before calling the rebar-package
macro.

First, all the package metadata information variables that exist in
the generic infrastructure also exist in the rebar infrastructure:
ERLANG_FOOBAR_VERSION, ERLANG_FOOBAR_SOURCE, ERLANG_FOOBAR_PATCH,
ERLANG_FOOBAR_SITE, ERLANG_FOOBAR_SUBDIR, ERLANG_FOOBAR_DEPENDENCIES,
ERLANG_FOOBAR_INSTALL_STAGING, ERLANG_FOOBAR_INSTALL_TARGET,
ERLANG_FOOBAR_LICENSE and ERLANG_FOOBAR_LICENSE_FILES.

还可以定义一些特定于钢筋基础设施的额外变量.它们中的许多只在非常特定的
情况下有用,因此典型的包只会使用其中的一些.

  * ERLANG_FOOBAR_USE_AUTOCONF, to specify that the package uses 
    autoconf at the configuration step. When a package sets this
    variable to YES, the autotools infrastructure is used.

    Note. You can also use some of the variables from the autotools
    infrastructure: ERLANG_FOOBAR_CONF_ENV, ERLANG_FOOBAR_CONF_OPTS,
    ERLANG_FOOBAR_AUTORECONF, ERLANG_FOOBAR_AUTORECONF_ENV and
    ERLANG_FOOBAR_AUTORECONF_OPTS.

  * ERLANG_FOOBAR_USE_BUNDLED_REBAR, to specify that the package has
    a bundled version of rebar and that it shall be used. Valid
    values are YES or NO (the default).

    Note. If the package bundles a rebar utility, but can use the
    generic one that Buildroot provides, just say NO (i.e., do not
    specify this variable). Only set if it is mandatory to use the 
    rebar utility bundled in this package.

  * ERLANG_FOOBAR_REBAR_ENV, to specify additional environment
    variables to pass to the rebar utility.
  * ERLANG_FOOBAR_KEEP_DEPENDENCIES, to keep the dependencies
    described in the rebar.config file. Valid values are YES or NO
    (the default). Unless this variable is set to YES, the rebar
    infrastructure removes such dependencies in a post-patch hook to
    ensure rebar does not download nor compile them.

With the rebar infrastructure, all the steps required to build and
install the packages are already defined, and they generally work
well for most rebar-based packages. However, when required, it is
still possible to customize what is done in any particular step:

  * By adding a post-operation hook (after extract, patch, configure,
    build or install). See Section 18.23, Hooks available in the
    various build steps for details.
  * By overriding one of the steps. For example, even if the rebar
    infrastructure is used, if the package .mk file defines its own
    ERLANG_FOOBAR_BUILD_CMDS variable, it will be used instead of the
    default rebar one. However, using this method should be
    restricted to very specific cases. Do not use it in the general
    case.

### 18.15 Waf-based包基础架构

#### 18.15.1 waf-package tutorial

First, let's see how to write a .mk file for a Waf-based package,
with an example :

```bash
01: ################################################################################
02: #
03: # libfoo
04: #
05: ################################################################################
06:
07: LIBFOO_VERSION = 1.0
08: LIBFOO_SOURCE = libfoo-$(LIBFOO_VERSION).tar.gz
09: LIBFOO_SITE = http://www.foosoftware.org/download
10: LIBFOO_CONF_OPTS = --enable-bar --disable-baz
11: LIBFOO_DEPENDENCIES = bar
12:
13: $(eval $(waf-package))
```

On line 7, we declare the version of the package.

On line 8 and 9, we declare the name of the tarball (xz-ed tarball
recommended) and the location of the tarball on the Web. Buildroot
will automatically download the tarball from this location.

On line 10, we tell Buildroot what options to enable for libfoo.

On line 11, we tell Buildroot the dependencies of libfoo.

Finally, on line line 13, we invoke the waf-package macro that
generates all the Makefile rules that actually allows the package to
be built.

#### 18.15.2 waf-package reference

The main macro of the Waf package infrastructure is waf-package. It
is similar to the generic-package macro.

Just like the generic infrastructure, the Waf infrastructure works by
defining a number of variables before calling the waf-package macro.

First, all the package metadata information variables that exist in
the generic infrastructure also exist in the Waf infrastructure:
LIBFOO_VERSION, LIBFOO_SOURCE, LIBFOO_PATCH, LIBFOO_SITE,
LIBFOO_SUBDIR, LIBFOO_DEPENDENCIES, LIBFOO_INSTALL_STAGING,
LIBFOO_INSTALL_TARGET.

An additional variable, specific to the Waf infrastructure, can also
be defined.

  * LIBFOO_SUBDIR may contain the name of a subdirectory inside the
    package that contains the main wscript file. This is useful, if
    for example, the main wscript file is not at the root of the tree
    extracted by the tarball. If HOST_LIBFOO_SUBDIR is not specified,
    it defaults to LIBFOO_SUBDIR.
  * LIBFOO_NEEDS_EXTERNAL_WAF can be set to YES or NO to tell
    Buildroot to use the bundled waf executable. If set to NO, the
    default, then Buildroot will use the waf executable provided in
    the package source tree; if set to YES, then Buildroot will
    download, install waf as a host tool and use it to build the
    package.
  * LIBFOO_WAF_OPTS, to specify additional options to pass to the waf
    script at every step of the package build process: configure,
    build and installation. By default, empty.
  * LIBFOO_CONF_OPTS, to specify additional options to pass to the
    waf script for the configuration step. By default, empty.
  * LIBFOO_BUILD_OPTS, to specify additional options to pass to the
    waf script during the build step. By default, empty.
  * LIBFOO_INSTALL_STAGING_OPTS, to specify additional options to
    pass to the waf script during the staging installation step. By
    default, empty.
  * LIBFOO_INSTALL_TARGET_OPTS, to specify additional options to pass
    to the waf script during the target installation step. By
    default, empty.

### 18.16 Meson-based包基础架构

#### 18.16.1 meson-package tutorial

Meson [http://mesonbuild.com] is an open source build system meant to
be both extremely fast, and, even more importantly, as user friendly
as possible. It uses Ninja [https://ninja-build.org] as a companion
tool to perform the actual build operations.

Let's see how to write a .mk file for a Meson-based package, with an
example:

```bash
01: ################################################################################
02: #
03: # foo
04: #
05: ################################################################################
06:
07: FOO_VERSION = 1.0
08: FOO_SOURCE = foo-$(FOO_VERSION).tar.gz
09: FOO_SITE = http://www.foosoftware.org/download
10: FOO_LICENSE = GPL-3.0+
11: FOO_LICENSE_FILES = COPYING
12: FOO_INSTALL_STAGING = YES
13:
14: FOO_DEPENDENCIES = host-pkgconf bar
15:
16: ifeq ($(BR2_PACKAGE_BAZ),y)
17: FOO_CONF_OPTS += -Dbaz=true
18: FOO_DEPENDENCIES += baz
19: else
20: FOO_CONF_OPTS += -Dbaz=false
21: endif
22:
23: $(eval $(meson-package))
```

The Makefile starts with the definition of the standard variables for
package declaration (lines 7 to 11).

On line line 23, we invoke the meson-package macro that generates all
the Makefile rules that actually allows the package to be built.

In the example, host-pkgconf and bar are declared as dependencies in
FOO_DEPENDENCIES at line 14 because the Meson build file of foo uses
pkg-config to determine the compilation flags and libraries of
package bar.

Note that it is not necessary to add host-meson in the
FOO_DEPENDENCIES variable of a package, since this basic dependency
is automatically added as needed by the Meson package infrastructure.

If the "baz" package is selected, then support for the "baz" feature
in "foo" is activated by adding -Dbaz=true to FOO_CONF_OPTS at line
17, as specified in the meson_options.txt file in "foo" source tree.
The "baz" package is also added to FOO_DEPENDENCIES. Note that the
support for baz is explicitly disabled at line 20, if the package is
not selected.

To sum it up, to add a new meson-based package, the Makefile example
can be copied verbatim then edited to replace all occurences of FOO
with the uppercase name of the new package and update the values of
the standard variables.

#### 18.16.2 meson-package reference

meson package基础结构的主要宏是meson-package.它类似于generic-package宏.
通过host-meson-package宏,还可以使用目标包和主机包.

Just like the generic infrastructure, the Meson infrastructure works
by defining a number of variables before calling the meson-package
macro.

First, all the package metadata information variables that exist in
the generic infrastructure also exist in the Meson infrastructure:
FOO_VERSION, FOO_SOURCE, FOO_PATCH, FOO_SITE, FOO_SUBDIR,
FOO_DEPENDENCIES, FOO_INSTALL_STAGING, FOO_INSTALL_TARGET.

A few additional variables, specific to the Meson infrastructure, can
also be defined. Many of them are only useful in very specific cases,
typical packages will therefore only use a few of them.

  * FOO_SUBDIR may contain the name of a subdirectory inside the
    package that contains the main meson.build file. This is useful,
    if for example, the main meson.build file is not at the root of
    the tree extracted by the tarball. If HOST_FOO_SUBDIR is not
    specified, it defaults to FOO_SUBDIR.
  * FOO_CONF_ENV, to specify additional environment variables to pass
    to meson for the configuration step. By default, empty.
  * FOO_CONF_OPTS, to specify additional options to pass to meson for
    the configuration step. By default, empty.
  * FOO_CFLAGS, to specify compiler arguments added to the package
    specific cross-compile.conf file c_args property. By default, the
    value of TARGET_CFLAGS.
  * FOO_CXXFLAGS, to specify compiler arguments added to the package
    specific cross-compile.conf file cpp_args property. By default,
    the value of TARGET_CXXFLAGS.
  * FOO_LDFLAGS, to specify compiler arguments added to the package
    specific cross-compile.conf file c_link_args and cpp_link_args
    properties. By default, the value of TARGET_LDFLAGS.
  * FOO_MESON_EXTRA_BINARIES, to specify a space-separated list of
    programs to add to the [binaries] section of the meson
    cross-compilation.conf configuration file. The format is
    program-name='/path/to/program', with no space around the = sign,
    and with the path of the program between single quotes. By
    default, empty. Note that Buildroot already sets the correct
    values for c, cpp, ar, strip, and pkgconfig.
  * FOO_MESON_EXTRA_PROPERTIES, to specify a space-separated list of
    properties to add to the [properties] section of the meson
    cross-compilation.conf configuration file. The format is
    property-name=<value> with no space around the = sign, and with
    single quotes around string values. By default, empty. Note that
    Buildroot already sets values for needs_exe_wrapper, c_args,
    c_link_args, cpp_args, cpp_link_args, sys_root, and
    pkg_config_libdir.
  * FOO_NINJA_ENV, to specify additional environment variables to
    pass to ninja, meson companion tool in charge of the build
    operations. By default, empty.
  * FOO_NINJA_OPTS, to specify a space-separated list of targets to
    build. By default, empty, to build the default target(s).

### 18.17 Cargo-based包基础架构

Cargo is the package manager for the Rust programming language. It
allows the user to build programs or libraries written in Rust, but
it also downloads and manages their dependencies, to ensure
repeatable builds. Cargo packages are called "crates".

#### 18.17.1 cargo-package教程

The Config.in file of Cargo-based package foo should contain:

```bash
01: config BR2_PACKAGE_FOO
02:     bool "foo"
03:     depends on BR2_PACKAGE_HOST_RUSTC_TARGET_ARCH_SUPPORTS
04:     select BR2_PACKAGE_HOST_RUSTC
05:     help
06:       This is a comment that explains what foo is.
07:
08:       http://foosoftware.org/foo/
```

And the .mk file for this package should contain:

```bash
01: ################################################################################
02: #
03: # foo
04: #
05: ################################################################################
06:
07: FOO_VERSION = 1.0
08: FOO_SOURCE = foo-$(FOO_VERSION).tar.gz
09: FOO_SITE = http://www.foosoftware.org/download
10: FOO_LICENSE = GPL-3.0+
11: FOO_LICENSE_FILES = COPYING
12:
13: $(eval $(cargo-package))
```

The Makefile starts with the definition of the standard variables for
package declaration (lines 7 to 11).

As seen in line 13, it is based on the cargo-package infrastructure.
Cargo will be invoked automatically by this infrastructure to build
and install the package.

It is still possible to define custom build commands or install
commands (i.e. with FOO_BUILD_CMDS and FOO_INSTALL_TARGET_CMDS).
Those will then replace the commands from the cargo infrastructure.

#### 18.17.2 cargo-package reference

The main macros for the Cargo package infrastructure are
cargo-package for target packages and host-cargo-package for host
packages.

Just like the generic infrastructure, the Cargo infrastructure works
by defining a number of variables before calling the cargo-package or
host-cargo-package macros.

First, all the package metadata information variables that exist in
the generic infrastructure also exist in the Cargo infrastructure:
FOO_VERSION, FOO_SOURCE, FOO_PATCH, FOO_SITE, FOO_DEPENDENCIES,
FOO_LICENSE, FOO_LICENSE_FILES, etc.

A few additional variables, specific to the Cargo infrastructure, can
also be defined. Many of them are only useful in very specific cases,
typical packages will therefore only use a few of them.

  * FOO_SUBDIR may contain the name of a subdirectory inside the
    package that contains the Cargo.toml file. This is useful, if for
    example, it is not at the root of the tree extracted by the
    tarball. If HOST_FOO_SUBDIR is not specified, it defaults to
    FOO_SUBDIR.
  * FOO_CARGO_ENV can be used to pass additional variables in the
    environment of cargo invocations. It used at both build and
    installation time
  * FOO_CARGO_BUILD_OPTS can be used to pass additional options to
    cargo at build time.
  * FOO_CARGO_INSTALL_OPTS can be used to pass additional options to
    cargo at install time.

A crate can depend on other libraries from crates.io or git
repositories, listed in its Cargo.toml file. Buildroot automatically
takes care of downloading such dependencies as part of the download
step of packages that use the cargo-package infrastructure. Such
dependencies are then kept together with the package source code in
the tarball cached in Buildroot's DL_DIR, and therefore the hash of
the package's tarball includes such dependencies.

This mechanism ensures that any change in the dependencies will be
detected, and allows the build to be performed completely offline.

### 18.18 Go包基础架构

This infrastructure applies to Go packages that use the standard
build system and use bundled dependencies.

#### 18.18.1 golang-package教程

First, let's see how to write a .mk file for a go package, with an
example :

```bash
01: ################################################################################
02: #
03: # foo
04: #
05: ################################################################################
06:
07: FOO_VERSION = 1.0
08: FOO_SITE = $(call github,bar,foo,$(FOO_VERSION))
09: FOO_LICENSE = BSD-3-Clause
10: FOO_LICENSE_FILES = LICENSE
11:
12: $(eval $(golang-package))
```

On line 7, we declare the version of the package.

On line 8, we declare the upstream location of the package, here
fetched from Github, since a large number of Go packages are hosted
on Github.

On line 9 and 10, we give licensing details about the package.

Finally, on line 12, we invoke the golang-package macro that
generates all the Makefile rules that actually allow the package to
be built.

#### 18.18.2 golang-package reference

In their Config.in file, packages using the golang-package
infrastructure should depend on
BR2_PACKAGE_HOST_GO_TARGET_ARCH_SUPPORTS because Buildroot will
automatically add a dependency on host-go to such packages. If you
need CGO support in your package, you must add a dependency on
BR2_PACKAGE_HOST_GO_TARGET_CGO_LINKING_SUPPORTS.

The main macro of the Go package infrastructure is golang-package. It
is similar to the generic-package macro. The ability to build host
packages is also available, with the host-golang-package macro. Host
packages built by host-golang-package macro should depend on
BR2_PACKAGE_HOST_GO_HOST_ARCH_SUPPORTS.

Just like the generic infrastructure, the Go infrastructure works by
defining a number of variables before calling the golang-package.

All the package metadata information variables that exist in the
generic package infrastructure also exist in the Go infrastructure:
FOO_VERSION, FOO_SOURCE, FOO_PATCH, FOO_SITE, FOO_SUBDIR,
FOO_DEPENDENCIES, FOO_LICENSE, FOO_LICENSE_FILES,
FOO_INSTALL_STAGING, etc.

Note that it is not necessary to add host-go in the FOO_DEPENDENCIES
variable of a package, since this basic dependency is automatically
added as needed by the Go package infrastructure.

A few additional variables, specific to the Go infrastructure, can
optionally be defined, depending on the package's needs. Many of them
are only useful in very specific cases, typical packages will
therefore only use a few of them, or none.

  * The package must specify its Go module name in the FOO_GOMOD
    variable. If not specified, it defaults to URL-domain/
    1st-part-of-URL/2nd-part-of-URL, e.g FOO_GOMOD will take the
    value github.com/bar/foo for a package that specifies FOO_SITE =
    $(call github,bar,foo,$(FOO_VERSION)). The Go package
    infrastructure will automatically generate a minimal go.mod file
    in the package source tree if it doesn't exist.
  * FOO_LDFLAGS and FOO_TAGS can be used to pass respectively the
    LDFLAGS or the TAGS to the go build command.
  * FOO_BUILD_TARGETS can be used to pass the list of targets that
    should be built. If FOO_BUILD_TARGETS is not specified, it
    defaults to .. We then have two cases:

      + FOO_BUILD_TARGETS is .. In this case, we assume only one
        binary will be produced, and that by default we name it after
        the package name. If that is not appropriate, the name of the
        produced binary can be overridden using FOO_BIN_NAME.
      + FOO_BUILD_TARGETS is not .. In this case, we iterate over the
        values to build each target, and for each produced a binary
        that is the non-directory component of the target. For
        example if FOO_BUILD_TARGETS = cmd/docker cmd/dockerd the
        binaries produced are docker and dockerd.
  * FOO_INSTALL_BINS can be used to pass the list of binaries that
    should be installed in /usr/bin on the target. If
    FOO_INSTALL_BINS is not specified, it defaults to the lower-case
    name of package.

With the Go infrastructure, all the steps required to build and
install the packages are already defined, and they generally work
well for most Go-based packages. However, when required, it is still
possible to customize what is done in any particular step:

  * By adding a post-operation hook (after extract, patch, configure,
    build or install). See Section 18.23, Hooks available in the
    various build steps for details.
  * By overriding one of the steps. For example, even if the Go
    infrastructure is used, if the package .mk file defines its own
    FOO_BUILD_CMDS variable, it will be used instead of the default
    Go one. However, using this method should be restricted to very
    specific cases. Do not use it in the general case.

A Go package can depend on other Go modules, listed in its go.mod
file. Buildroot automatically takes care of downloading such
dependencies as part of the download step of packages that use the
golang-package infrastructure. Such dependencies are then kept
together with the package source code in the tarball cached in
Buildroot's DL_DIR, and therefore the hash of the package's tarball
includes such dependencies.

This mechanism ensures that any change in the dependencies will be
detected, and allows the build to be performed completely offline.

### 18.19 QMake-based包基础架构

#### 18.19.1 qmake-package教程

First, let's see how to write a .mk file for a QMake-based package,
with an example :

```bash
01: ################################################################################
02: #
03: # libfoo
04: #
05: ################################################################################
06:
07: LIBFOO_VERSION = 1.0
08: LIBFOO_SOURCE = libfoo-$(LIBFOO_VERSION).tar.gz
09: LIBFOO_SITE = http://www.foosoftware.org/download
10: LIBFOO_CONF_OPTS = QT_CONFIG+=bar QT_CONFIG-=baz
11: LIBFOO_DEPENDENCIES = bar
12:
13: $(eval $(qmake-package))
```

On line 7, we declare the version of the package.

On line 8 and 9, we declare the name of the tarball (xz-ed tarball
recommended) and the location of the tarball on the Web. Buildroot
will automatically download the tarball from this location.

On line 10, we tell Buildroot what options to enable for libfoo.

On line 11, we tell Buildroot the dependencies of libfoo.

Finally, on line line 13, we invoke the qmake-package macro that
generates all the Makefile rules that actually allows the package to
be built.

#### 18.19.2 qmake-package reference

The main macro of the QMake package infrastructure is qmake-package.
It is similar to the generic-package macro.

Just like the generic infrastructure, the QMake infrastructure works
by defining a number of variables before calling the qmake-package
macro.

First, all the package metadata information variables that exist in
the generic infrastructure also exist in the QMake infrastructure:
LIBFOO_VERSION, LIBFOO_SOURCE, LIBFOO_PATCH, LIBFOO_SITE,
LIBFOO_SUBDIR, LIBFOO_DEPENDENCIES, LIBFOO_INSTALL_STAGING,
LIBFOO_INSTALL_TARGET.

An additional variable, specific to the QMake infrastructure, can
also be defined.

  * LIBFOO_CONF_ENV, to specify additional environment variables to
    pass to the qmake script for the configuration step. By default,
    empty.
  * LIBFOO_CONF_OPTS, to specify additional options to pass to the
    qmake script for the configuration step. By default, empty.
  * LIBFOO_MAKE_ENV, to specify additional environment variables to
    the make command during the build and install steps. By default,
    empty.
  * LIBFOO_MAKE_OPTS, to specify additional targets to pass to the
    make command during the build step. By default, empty.
  * LIBFOO_INSTALL_STAGING_OPTS, to specify additional targets to
    pass to the make command during the staging installation step. By
    default, install.
  * LIBFOO_INSTALL_TARGET_OPTS, to specify additional targets to pass
    to the make command during the target installation step. By
    default, install.
  * LIBFOO_SYNC_QT_HEADERS, to run syncqt.pl before qmake. Some
    packages need this to have a properly populated include directory
    before running the build.

### 18.20 构建内核模块的包的基础设施

Buildroot offers a helper infrastructure to make it easy to write
packages that build and install Linux kernel modules. Some packages
only contain a kernel module, other packages contain programs and
libraries in addition to kernel modules. Buildroot's helper
infrastructure supports either case.

#### 18.20.1 kernel-module tutorial

Let's start with an example on how to prepare a simple package that
only builds a kernel module, and no other component:

```bash
01: ################################################################################
02: #
03: # foo
04: #
05: ################################################################################
06:
07: FOO_VERSION = 1.2.3
08: FOO_SOURCE = foo-$(FOO_VERSION).tar.xz
09: FOO_SITE = http://www.foosoftware.org/download
10: FOO_LICENSE = GPL-2.0
11: FOO_LICENSE_FILES = COPYING
12:
13: $(eval $(kernel-module))
14: $(eval $(generic-package))
```

Lines 7-11 define the usual meta-data to specify the version, archive
name, remote URI where to find the package source, licensing
information.

On line 13, we invoke the kernel-module helper infrastructure, that
generates all the appropriate Makefile rules and variables to build
that kernel module.

Finally, on line 14, we invoke the generic-package infrastructure.

The dependency on linux is automatically added, so it is not needed
to specify it in FOO_DEPENDENCIES.

What you may have noticed is that, unlike other package
infrastructures, we explicitly invoke a second infrastructure. This
allows a package to build a kernel module, but also, if needed, use
any one of other package infrastructures to build normal userland
components (libraries, executables). Using the kernel-module
infrastructure on its own is not sufficient; another package
infrastructure must be used.

Let's look at a more complex example:

```bash
01: ################################################################################
02: #
03: # foo
04: #
05: ################################################################################
06:
07: FOO_VERSION = 1.2.3
08: FOO_SOURCE = foo-$(FOO_VERSION).tar.xz
09: FOO_SITE = http://www.foosoftware.org/download
10: FOO_LICENSE = GPL-2.0
11: FOO_LICENSE_FILES = COPYING
12:
13: FOO_MODULE_SUBDIRS = driver/base
14: FOO_MODULE_MAKE_OPTS = KVERSION=$(LINUX_VERSION_PROBED)
15:
16: ifeq ($(BR2_PACKAGE_LIBBAR),y)
17: FOO_DEPENDENCIES += libbar
18: FOO_CONF_OPTS += --enable-bar
19: FOO_MODULE_SUBDIRS += driver/bar
20: else
21: FOO_CONF_OPTS += --disable-bar
22: endif
23:
24: $(eval $(kernel-module))
26: $(eval $(autotools-package))
```

Here, we see that we have an autotools-based package, that also
builds the kernel module located in sub-directory driver/base and, if
libbar is enabled, the kernel module located in sub-directory driver/
bar, and defines the variable KVERSION to be passed to the Linux
buildsystem when building the module(s).

#### 18.20.2 kernel-module reference

The main macro for the kernel module infrastructure is kernel-module.
Unlike other package infrastructures, it is not stand-alone, and
requires any of the other *-package macros be called after it.

The kernel-module macro defines post-build and post-target-install
hooks to build the kernel modules. If the package's .mk needs access
to the built kernel modules, it should do so in a post-build hook, 
registered after the call to kernel-module. Similarly, if the
package's .mk needs access to the kernel module after it has been
installed, it should do so in a post-install hook, registered after
the call to kernel-module. Here's an example:

```bash
$(eval $(kernel-module))

define FOO_DO_STUFF_WITH_KERNEL_MODULE
    # Do something with it...
endef
FOO_POST_BUILD_HOOKS += FOO_DO_STUFF_WITH_KERNEL_MODULE

$(eval $(generic-package))
```

Finally, unlike the other package infrastructures, there is no
host-kernel-module variant to build a host kernel module.

The following additional variables can optionally be defined to
further configure the build of the kernel module:

  * FOO_MODULE_SUBDIRS may be set to one or more sub-directories
    (relative to the package source top-directory) where the kernel
    module sources are. If empty or not set, the sources for the
    kernel module(s) are considered to be located at the top of the
    package source tree.
  * FOO_MODULE_MAKE_OPTS may be set to contain extra variable
    definitions to pass to the Linux buildsystem.

You may also reference (but you may not set!) those variables:

  * LINUX_DIR contains the path to where the Linux kernel has been
    extracted and built.
  * LINUX_VERSION contains the version string as configured by the
    user.
  * LINUX_VERSION_PROBED contains the real version string of the
    kernel, retrieved with running make -C $(LINUX_DIR) kernelrelease
  * KERNEL_ARCH contains the name of the current architecture, like
    arm, mips

### 18.21 asciidoc文档的基础架构

The Buildroot manual, which you are currently reading, is entirely
written using the AsciiDoc [http://asciidoc.org/] mark-up syntax. The
manual is then rendered to many formats:

  * html
  * split-html
  * pdf
  * epub
  * text

Although Buildroot only contains one document written in AsciiDoc,
there is, as for packages, an infrastructure for rendering documents
using the AsciiDoc syntax.

Also as for packages, the AsciiDoc infrastructure is available from a
br2-external tree. This allows documentation for a br2-external tree
to match the Buildroot documentation, as it will be rendered to the
same formats and use the same layout and theme.

#### 18.21.1 asciidoc-document tutorial

Whereas package infrastructures are suffixed with -package, the
document infrastructures are suffixed with -document. So, the
AsciiDoc infrastructure is named asciidoc-document.

Here is an example to render a simple AsciiDoc document.

```bash
01: ################################################################################
02: #
03: # foo-document
04: #
05: ################################################################################
06:
07: FOO_SOURCES = $(sort $(wildcard $(FOO_DOCDIR)/*))
08: $(eval $(call asciidoc-document))
```

On line 7, the Makefile declares what the sources of the document
are. Currently, it is expected that the document's sources are only
local; Buildroot will not attempt to download anything to render a
document. Thus, you must indicate where the sources are. Usually, the
string above is sufficient for a document with no sub-directory
structure.

On line 8, we call the asciidoc-document function, which generates
all the Makefile code necessary to render the document.

#### 18.21.2 asciidoc-document reference

The list of variables that can be set in a .mk file to give metadata
information is (assuming the document name is foo) :

  * FOO_SOURCES, mandatory, defines the source files for the
    document.
  * FOO_RESOURCES, optional, may contain a space-separated list of
    paths to one or more directories containing so-called resources
    (like CSS or images). By default, empty.
  * FOO_DEPENDENCIES, optional, the list of packages (most probably,
    host-packages) that must be built before building this document.

There are also additional hooks (see Section 18.23, Hooks available
in the various build steps for general information on hooks), that a
document may set to define extra actions to be done at various steps:

  * FOO_POST_RSYNC_HOOKS to run additional commands after the sources
    have been copied by Buildroot. This can for example be used to
    generate part of the manual with information extracted from the
    tree. As an example, Buildroot uses this hook to generate the
    tables in the appendices.
  * FOO_CHECK_DEPENDENCIES_HOOKS to run additional tests on required
    components to generate the document. In AsciiDoc, it is possible
    to call filters, that is, programs that will parse an AsciiDoc
    block and render it appropriately (e.g. ditaa [http://
    ditaa.sourceforge.net/] or aafigure [https://pythonhosted.org/
    aafigure/]).
  * FOO_CHECK_DEPENDENCIES_<FMT>_HOOKS, to run additional tests for
    the specified format <FMT> (see the list of rendered formats,
    above).

Buildroot设置以下变量,可以在上面的定义中使用:

  * $(FOO_DOCDIR), similar to $(FOO_PKGDIR), contains the path to the
    directory containing foo.mk. It can be used to refer to the
    document sources, and can be used in the hooks, especially the
    post-rsync hook if parts of the documentation needs to be
    generated.
  * $(@D), as for traditional packages, contains the path to the
    directory where the document will be copied and built.

下面是一个使用了所有变量和所有钩子的完整示例:

```bash
01: ################################################################################
02: #
03: # foo-document
04: #
05: ################################################################################
06:
07: FOO_SOURCES = $(sort $(wildcard $(FOO_DOCDIR)/*))
08: FOO_RESOURCES = $(sort $(wildcard $(FOO_DOCDIR)/ressources))
09:
10: define FOO_GEN_EXTRA_DOC
11:     /path/to/generate-script --outdir=$(@D)
12: endef
13: FOO_POST_RSYNC_HOOKS += FOO_GEN_EXTRA_DOC
14:
15: define FOO_CHECK_MY_PROG
16:     if ! which my-prog >/dev/null 2>&1; then \
17:         echo "You need my-prog to generate the foo document"; \
18:         exit 1; \
19:     fi
20: endef
21: FOO_CHECK_DEPENDENCIES_HOOKS += FOO_CHECK_MY_PROG
22:
23: define FOO_CHECK_MY_OTHER_PROG
24:     if ! which my-other-prog >/dev/null 2>&1; then \
25:         echo "You need my-other-prog to generate the foo document as PDF"; \
26:         exit 1; \
27:     fi
28: endef
29: FOO_CHECK_DEPENDENCIES_PDF_HOOKS += FOO_CHECK_MY_OTHER_PROG
30:
31: $(eval $(call asciidoc-document))
```

### 18.22 特定于Linux内核包的基础结构

The Linux kernel package can use some specific infrastructures based
on package hooks for building Linux kernel tools or/and building
Linux kernel extensions.

#### 18.22.1 linux-kernel-tools

Buildroot offers a helper infrastructure to build some userspace
tools for the target available within the Linux kernel sources. Since
their source code is part of the kernel source code, a special
package, linux-tools, exists and re-uses the sources of the Linux
kernel that runs on the target.

Let's look at an example of a Linux tool. For a new Linux tool named
foo, create a new menu entry in the existing package/linux-tools/
Config.in. This file will contain the option descriptions related to
each kernel tool that will be used and displayed in the configuration
tool. It would basically look like:

```bash
01: config BR2_PACKAGE_LINUX_TOOLS_FOO
02:     bool "foo"
03:     select BR2_PACKAGE_LINUX_TOOLS
04:     help
05:       This is a comment that explains what foo kernel tool is.
06:
07:       http://foosoftware.org/foo/
```

The name of the option starts with the prefix
BR2_PACKAGE_LINUX_TOOLS_, followed by the uppercase name of the tool
(like is done for packages).

Note. Unlike other packages, the linux-tools package options appear
in the linux kernel menu, under the Linux Kernel Tools sub-menu, not
under the Target packages main menu.

Then for each linux tool, add a new .mk.in file named package/
linux-tools/linux-tool-foo.mk.in. It would basically look like:

```bash
01: ################################################################################
02: #
03: # foo
04: #
05: ################################################################################
06:
07: LINUX_TOOLS += foo
08:
09: FOO_DEPENDENCIES = libbbb
10:
11: define FOO_BUILD_CMDS
12:     $(TARGET_MAKE_ENV) $(MAKE) -C $(LINUX_DIR)/tools foo
13: endef
14:
15: define FOO_INSTALL_STAGING_CMDS
16:     $(TARGET_MAKE_ENV) $(MAKE) -C $(LINUX_DIR)/tools \
17:             DESTDIR=$(STAGING_DIR) \
18:             foo_install
19: endef
20:
21: define FOO_INSTALL_TARGET_CMDS
22:     $(TARGET_MAKE_ENV) $(MAKE) -C $(LINUX_DIR)/tools \
23:             DESTDIR=$(TARGET_DIR) \
24:             foo_install
25: endef
```

在第7行,我们将Linux工具foo注册到可用的Linux工具列表中.

On line 9, we specify the list of dependencies this tool relies on.
These dependencies are added to the Linux package dependencies list
only when the foo tool is selected.

The rest of the Makefile, lines 11-25 defines what should be done at
the different steps of the Linux tool build process like for a
generic package. They will actually be used only when the foo tool is
selected. The only supported commands are _BUILD_CMDS,
_INSTALL_STAGING_CMDS and _INSTALL_TARGET_CMDS.

Note. One must not call $(eval $(generic-package)) or any other
package infrastructure! Linux tools are not packages by themselves,
they are part of the linux-tools package.

#### 18.22.2 linux-kernel-extensions

Some packages provide new features that require the Linux kernel tree
to be modified. This can be in the form of patches to be applied on
the kernel tree, or in the form of new files to be added to the tree.
The Buildroot's Linux kernel extensions infrastructure provides a
simple solution to automatically do this, just after the kernel
sources are extracted and before the kernel patches are applied.
Examples of extensions packaged using this mechanism are the
real-time extensions Xenomai and RTAI, as well as the set of
out-of-tree LCD screens drivers fbtft.

Let's look at an example on how to add a new Linux extension foo.

First, create the package foo that provides the extension: this
package is a standard package; see the previous chapters on how to
create such a package. This package is in charge of downloading the
sources archive, checking the hash, defining the licence informations
and building user space tools if any.

Then create the Linux extension proper: create a new menu entry in
the existing linux/Config.ext.in. This file contains the option
descriptions related to each kernel extension that will be used and
displayed in the configuration tool. It would basically look like:

```bash
01: config BR2_LINUX_KERNEL_EXT_FOO
02:     bool "foo"
03:     help
04:       This is a comment that explains what foo kernel extension is.
05:
06:       http://foosoftware.org/foo/
```

Then for each linux extension, add a new .mk file named linux/
linux-ext-foo.mk. It should basically contain:

```bash
01: ################################################################################
02: #
03: # foo
04: #
05: ################################################################################
06:
07: LINUX_EXTENSIONS += foo
08:
09: define FOO_PREPARE_KERNEL
10:     $(FOO_DIR)/prepare-kernel-tree.sh --linux-dir=$(@D)
11: endef
```

在第7行,我们将Linux扩展foo添加到可用的Linux扩展列表中.

On line 9-11, we define what should be done by the extension to
modify the Linux kernel tree; this is specific to the linux extension
and can use the variables defined by the foo package, like: $
(FOO_DIR) or $(FOO_VERSION) as well as all the Linux variables,
like: $(LINUX_VERSION) or $(LINUX_VERSION_PROBED), $(KERNEL_ARCH)
See the definition of those kernel variables.

### 18.23 各种构建步骤中可用的钩子

The generic infrastructure (and as a result also the derived
autotools and cmake infrastructures) allow packages to specify hooks.
These define further actions to perform after existing steps. Most
hooks aren't really useful for generic packages, since the .mk file
already has full control over the actions performed in each step of
the package construction.

The following hook points are available:

  * LIBFOO_PRE_DOWNLOAD_HOOKS
  * LIBFOO_POST_DOWNLOAD_HOOKS
  * LIBFOO_PRE_EXTRACT_HOOKS
  * LIBFOO_POST_EXTRACT_HOOKS
  * LIBFOO_PRE_RSYNC_HOOKS
  * LIBFOO_POST_RSYNC_HOOKS
  * LIBFOO_PRE_PATCH_HOOKS
  * LIBFOO_POST_PATCH_HOOKS
  * LIBFOO_PRE_CONFIGURE_HOOKS
  * LIBFOO_POST_CONFIGURE_HOOKS
  * LIBFOO_PRE_BUILD_HOOKS
  * LIBFOO_POST_BUILD_HOOKS
  * LIBFOO_PRE_INSTALL_HOOKS (for host packages only)
  * LIBFOO_POST_INSTALL_HOOKS (for host packages only)
  * LIBFOO_PRE_INSTALL_STAGING_HOOKS (for target packages only)
  * LIBFOO_POST_INSTALL_STAGING_HOOKS (for target packages only)
  * LIBFOO_PRE_INSTALL_TARGET_HOOKS (for target packages only)
  * LIBFOO_POST_INSTALL_TARGET_HOOKS (for target packages only)
  * LIBFOO_PRE_INSTALL_IMAGES_HOOKS
  * LIBFOO_POST_INSTALL_IMAGES_HOOKS
  * LIBFOO_PRE_LEGAL_INFO_HOOKS
  * LIBFOO_POST_LEGAL_INFO_HOOKS
  * LIBFOO_TARGET_FINALIZE_HOOKS

These variables are lists of variable names containing actions to be
performed at this hook point. This allows several hooks to be
registered at a given hook point. Here is an example:

```bash
define LIBFOO_POST_PATCH_FIXUP
        action1
        action2
endef

LIBFOO_POST_PATCH_HOOKS += LIBFOO_POST_PATCH_FIXUP
```

#### 18.23.1 Using the POST_RSYNC hook

The POST_RSYNC hook is run only for packages that use a local source,
either through the local site method or the OVERRIDE_SRCDIR
mechanism. In this case, package sources are copied using rsync from
the local location into the buildroot build directory. The rsync
command does not copy all files from the source directory, though.
Files belonging to a version control system, like the directories
.git, .hg, etc. are not copied. For most packages this is sufficient,
but a given package can perform additional actions using the
POST_RSYNC hook.

In principle, the hook can contain any command you want. One specific
use case, though, is the intentional copying of the version control
directory using rsync. The rsync command you use in the hook can,
among others, use the following variables:

  * $(SRCDIR): the path to the overridden source directory
  * $(@D): the path to the build directory

18.23.2 Target-finalize hook

Packages may also register hooks in LIBFOO_TARGET_FINALIZE_HOOKS.
These hooks are run after all packages are built, but before the
filesystem images are generated. They are seldom used, and your
package probably do not need them.

### 18.24 与包的Gettext集成和交互

Many packages that support internationalization use the gettext
library. Dependencies for this library are fairly complicated and
therefore, deserve some explanation.

The glibc C library integrates a full-blown implementation of gettext
, supporting translation. Native Language Support is therefore
built-in in glibc.

On the other hand, the uClibc and musl C libraries only provide a
stub implementation of the gettext functionality, which allows to
compile libraries and programs using gettext functions, but without
providing the translation capabilities of a full-blown gettext
implementation. With such C libraries, if real Native Language
Support is necessary, it can be provided by the libintl library of
the gettext package.

Due to this, and in order to make sure that Native Language Support
is properly handled, packages in Buildroot that can use NLS support
should:

 1. Ensure NLS support is enabled when BR2_SYSTEM_ENABLE_NLS=y. This
    is done automatically for autotools packages and therefore should
    only be done for packages using other package infrastructures.
 2. Add $(TARGET_NLS_DEPENDENCIES) to the package <pkg>_DEPENDENCIES
    variable. This addition should be done unconditionally: the value
    of this variable is automatically adjusted by the core
    infrastructure to contain the relevant list of packages. If NLS
    support is disabled, this variable is empty. If NLS support is
    enabled, this variable contains host-gettext so that tools needed
    to compile translation files are available on the host. In
    addition, if uClibc or musl are used, this variable also contains
    gettext in order to get the full-blown gettext implementation.
 3. If needed, add $(TARGET_NLS_LIBS) to the linker flags, so that
    the package gets linked with libintl. This is generally not
    needed with autotools packages as they usually detect
    automatically that they should link with libintl. However,
    packages using other build systems, or problematic
    autotools-based packages may need this. $(TARGET_NLS_LIBS) should
    be added unconditionally to the linker flags, as the core
    automatically makes it empty or defined to -lintl depending on
    the configuration.

No changes should be made to the Config.in file to support NLS.

Finally, certain packages need some gettext utilities on the target,
such as the gettext program itself, which allows to retrieve
translated strings, from the command line. In such a case, the
package should:

  * use select BR2_PACKAGE_GETTEXT in their Config.in file,
    indicating in a comment above that it's a runtime dependency
    only.
  * not add any gettext dependency in the DEPENDENCIES variable of
    their .mk file.

### 18.25 提示和技巧

#### 18.25.1 Package name, config entry name and makefile variable
relationship

In Buildroot, there is some relationship between:

  * the package name, which is the package directory name (and the
    name of the *.mk file);
  * the config entry name that is declared in the Config.in file;
  * the makefile variable prefix.

It is mandatory to maintain consistency between these elements, using
the following rules:

  * the package directory and the *.mk name are the package name
    itself (e.g.: package/foo-bar_boo/foo-bar_boo.mk);
  * the make target name is the package name itself (e.g.:
    foo-bar_boo);
  * the config entry is the upper case package name with . and -
    characters substituted with _, prefixed with BR2_PACKAGE_ (e.g.:
    BR2_PACKAGE_FOO_BAR_BOO);
  * the *.mk file variable prefix is the upper case package name with
    . and - characters substituted with _ (e.g.:
    FOO_BAR_BOO_VERSION).

#### 18.25.2 How to check the coding style

Buildroot provides a script in utils/check-package that checks new or
changed files for coding style. It is not a complete language
validator, but it catches many common mistakes. It is meant to run in
the actual files you created or modified, before creating the patch
for submission.

This script can be used for packages, filesystem makefiles, Config.in
files, etc. It does not check the files defining the package
infrastructures and some other files containing similar common code.

To use it, run the check-package script, by telling which files you
created or changed:

```console
$ ./utils/check-package package/new-package/*
```

If you have the utils directory in your path you can also run:

```console
$ cd package/new-package/
$ check-package *
```

The tool can also be used for packages in a br2-external:

```console
$ check-package -b /path/to/br2-ext-tree/package/my-package/*
```

#### 18.25.3 How to test your package

一旦添加了新包,在各种条件下测试它是很重要的:它是为所有架构构建的吗?
它是用不同的C库构建的吗?它需要线程吗,NPTL?等等

Buildroot runs autobuilders [http://autobuild.buildroot.org/] which
continuously test random configurations. However, these only build
the master branch of the git tree, and your new fancy package is not
yet there.

Buildroot provides a script in utils/test-pkg that uses the same base
configurations as used by the autobuilders so you can test your
package in the same conditions.

First, create a config snippet that contains all the necessary
options needed to enable your package, but without any architecture
or toolchain option. For example, let's create a config snippet that
just enables libcurl, without any TLS backend:

```console
$ cat libcurl.config
BR2_PACKAGE_LIBCURL=y
```

If your package needs more configuration options, you can add them to
the config snippet. For example, here's how you would test libcurl
with openssl as a TLS backend and the curl program:

```console
$ cat libcurl.config
BR2_PACKAGE_LIBCURL=y
BR2_PACKAGE_LIBCURL_CURL=y
BR2_PACKAGE_OPENSSL=y
```

Then run the test-pkg script, by telling it what config snippet to
use and what package to test:

```console
$ ./utils/test-pkg -c libcurl.config -p libcurl
```

By default, test-pkg will build your package against a subset of the
toolchains used by the autobuilders, which has been selected by the
Buildroot developers as being the most useful and representative
subset. If you want to test all toolchains, pass the -a option. Note
that in any case, internal toolchains are excluded as they take too
long to build.

The output lists all toolchains that are tested and the corresponding
result (excerpt, results are fake):

```console
$ ./utils/test-pkg -c libcurl.config -p libcurl
                armv5-ctng-linux-gnueabi [ 1/11]: OK
              armv7-ctng-linux-gnueabihf [ 2/11]: OK
                        br-aarch64-glibc [ 3/11]: SKIPPED
                           br-arcle-hs38 [ 4/11]: SKIPPED
                            br-arm-basic [ 5/11]: FAILED
                  br-arm-cortex-a9-glibc [ 6/11]: OK
                   br-arm-cortex-a9-musl [ 7/11]: FAILED
                   br-arm-cortex-m4-full [ 8/11]: OK
                             br-arm-full [ 9/11]: OK
                    br-arm-full-nothread [10/11]: FAILED
                      br-arm-full-static [11/11]: OK
11 builds, 2 skipped, 2 build failed, 1 legal-info failed
```

The results mean:

  * OK: the build was successful.
  * SKIPPED: one or more configuration options listed in the config
    snippet were not present in the final configuration. This is due
    to options having dependencies not satisfied by the toolchain,
    such as for example a package that depends on BR2_USE_MMU with a
    noMMU toolchain. The missing options are reported in
    missing.config in the output build directory (~/br-test-pkg/
    TOOLCHAIN_NAME/ by default).
  * FAILED: the build failed. Inspect the logfile file in the output
    build directory to see what went wrong:

      + the actual build failed,
      + the legal-info failed,
      + one of the preliminary steps (downloading the config file,
        applying the configuration, running dirclean for the package)
        failed.

When there are failures, you can just re-run the script with the same
options (after you fixed your package); the script will attempt to
re-build the package specified with -p for all toolchains, without
the need to re-build all the dependencies of that package.

The test-pkg script accepts a few options, for which you can get some
help by running:

```console
$ ./utils/test-pkg -h
```

#### 18.25.4 How to add a package from GitHub

Packages on GitHub often don't have a download area with release
tarballs. However, it is possible to download tarballs directly from
the repository on GitHub. As GitHub is known to have changed download
mechanisms in the past, the github helper function should be used as
shown below.

```bash
# Use a tag or a full commit ID
FOO_VERSION = 1.0
FOO_SITE = $(call github,<user>,<package>,v$(FOO_VERSION))
```

Notes

  * The FOO_VERSION can either be a tag or a commit ID.
  * The tarball name generated by github matches the default one from
    Buildroot (e.g.:
    foo-f6fb6654af62045239caed5950bc6c7971965e60.tar.gz), so it is
    not necessary to specify it in the .mk file.
  * When using a commit ID as version, you should use the full 40 hex
    characters.
  * When the tag contains a prefix such as v in v1.0, then the
    VERSION variable should contain just 1.0, and the v should be
    added directly in the SITE variable, as illustrated above. This
    ensures that the VERSION variable value can be used to match
    against release-monitoring.org [http://www.release-monitoring.org
    /] results.

If the package you wish to add does have a release section on GitHub,
the maintainer may have uploaded a release tarball, or the release
may just point to the automatically generated tarball from the git
tag. If there is a release tarball uploaded by the maintainer, we
prefer to use that since it may be slightly different (e.g. it
contains a configure script so we don't need to do AUTORECONF).

You can see on the release page if it's an uploaded tarball or a git
tag:

  * If it looks like the image above then it was uploaded by the
    maintainer and you should use that link (in that example: 
    mongrel2-v1.9.2.tar.bz2) to specify FOO_SITE, and not use the 
    github helper.
  * On the other hand, if there's is only the "Source code" link,
    then it's an automatically generated tarball and you should use
    the github helper function.

18.25.5 How to add a package from Gitlab

In a similar way to the github macro described in Section 18.25.4,
How to add a package from GitHub, Buildroot also provides the
gitlab macro to download from Gitlab repositories. It can be used to
download auto-generated tarballs produced by Gitlab, either for
specific tags or commits:

```bash
# Use a tag or a full commit ID
FOO_VERSION = 1.0
FOO_SITE = $(call gitlab,<user>,<package>,v$(FOO_VERSION))
```

By default, it will use a .tar.gz tarball, but Gitlab also provides
.tar.bz2 tarballs, so by adding a <pkg>_SOURCE variable, this
.tar.bz2 tarball can be used:

```bash
# Use a tag or a full commit ID
FOO_VERSION = 1.0
FOO_SITE = $(call gitlab,<user>,<package>,v$(FOO_VERSION))
FOO_SOURCE = foo-$(FOO_VERSION).tar.bz2
```

If there is a specific tarball uploaded by the upstream developers in
https://gitlab.com/<project>/releases/, do not use this macro, but
rather use directly the link to the tarball.

### 18.26 结论

As you can see, adding a software package to Buildroot is simply a
matter of writing a Makefile using an existing example and modifying
it according to the compilation process required by the package.

If you package software that might be useful for other people, don't
forget to send a patch to the Buildroot mailing list (see
Section 22.5, Submitting patches)!

## Chapter 19 为包打补丁

在集成新包或更新现有包时,可能需要对软件源代码打补丁,以便在Buildroot中进行交叉构建.

Buildroot offers an infrastructure to automatically handle this
during the builds. It supports three ways of applying patch sets:
downloaded patches, patches supplied within buildroot and patches
located in a user-defined global patch directory.

### 19.1 提供补丁

#### 19.1.1 Downloaded

If it is necessary to apply a patch that is available for download,
then add it to the <packagename>_PATCH variable. If an entry contains
://, then Buildroot will assume it is a full URL and download the
patch from this location. Otherwise, Buildroot will assume that the
patch should be downloaded from <packagename>_SITE. It can be a
single patch, or a tarball containing a patch series.

Like for all downloads, a hash should be added to the
<packagename>.hash file.

This method is typically used for packages from Debian.

#### 19.1.2 Within Buildroot

Most patches are provided within Buildroot, in the package directory;
these typically aim to fix cross-compilation, libc support, or other
such issues.

These patch files should be named <number>-<description>.patch.

Notes

  * The patch files coming with Buildroot should not contain any
    package version reference in their filename.
  * The field <number> in the patch file name refers to the apply
    order, and shall start at 1; It is preferred to pad the number
    with zeros up to 4 digits, like git-format-patch does. E.g.:
    0001-foobar-the-buz.patch
  * Previously, it was mandatory for patches to be prefixed with the
    name of the package, like <package>-<number>-<description>.patch,
    but that is no longer the case. Existing packages will be fixed
    as time passes. Do not prefix patches with the package name.
  * Previously, a series file, as used by quilt, could also be added
    in the package directory. In that case, the series file defines
    the patch application order. This is deprecated, and will be
    removed in the future. Do not use a series file.

#### 19.1.3 Global patch directory

The BR2_GLOBAL_PATCH_DIR configuration file option can be used to
specify a space separated list of one or more directories containing
global package patches. See Section 9.8, Adding project-specific
patches for details.

### 19.2 如何应用补丁

 1. Run the <packagename>_PRE_PATCH_HOOKS commands if defined;
 2. Cleanup the build directory, removing any existing *.rej files;
 3. If <packagename>_PATCH is defined, then patches from these
    tarballs are applied;
 4. If there are some *.patch files in the package's Buildroot
    directory or in a package subdirectory named <packageversion>,
    then:

      + If a series file exists in the package directory, then
        patches are applied according to the series file;
      + Otherwise, patch files matching *.patch are applied in
        alphabetical order. So, to ensure they are applied in the
        right order, it is highly recommended to name the patch files
        like this: <number>-<description>.patch, where <number>
        refers to the apply order.
 5. If BR2_GLOBAL_PATCH_DIR is defined, the directories will be
    enumerated in the order they are specified. The patches are
    applied as described in the previous step.
 6. Run the <packagename>_POST_PATCH_HOOKS commands if defined.

If something goes wrong in the steps 3 or 4, then the build fails.

### 19.3 软件包补丁的格式和许可

Patches are released under the same license as the software they
apply to (see Section 13.2, Complying with the Buildroot license).

A message explaining what the patch does, and why it is needed,
should be added in the header commentary of the patch.

You should add a Signed-off-by statement in the header of the each
patch to help with keeping track of the changes and to certify that
the patch is released under the same license as the software that is
modified.

If the software is under version control, it is recommended to use
the upstream SCM software to generate the patch set.

Otherwise, concatenate the header with the output of the diff -purN
package-version.orig/ package-version/ command.

If you update an existing patch (e.g. when bumping the package
version), make sure the existing From header and Signed-off-by tags
are not removed, but do update the rest of the patch comment when
appropriate.

At the end, the patch should look like:

```bash
configure.ac: add C++ support test

Signed-off-by: John Doe <john.doe@noname.org>

--- configure.ac.orig
+++ configure.ac
@@ -40,2 +40,12 @@

AC_PROG_MAKE_SET
+
+AC_CACHE_CHECK([whether the C++ compiler works],
+               [rw_cv_prog_cxx_works],
+               [AC_LANG_PUSH([C++])
+                AC_LINK_IFELSE([AC_LANG_PROGRAM([], [])],
+                               [rw_cv_prog_cxx_works=yes],
+                               [rw_cv_prog_cxx_works=no])
+                AC_LANG_POP([C++])])
+
+AM_CONDITIONAL([CXX_WORKS], [test "x$rw_cv_prog_cxx_works" = "xyes"])
```

### 19.4 集成在Web上找到的补丁

When integrating a patch of which you are not the author, you have to
add a few things in the header of the patch itself.

Depending on whether the patch has been obtained from the project
repository itself, or from somewhere on the web, add one of the
following tags:

Backported from: <some commit id>

or

Fetch from: <some url>

It is also sensible to add a few words about any changes to the patch
that may have been necessary.

## Chapter 20 下载基础设施

TODO

## Chapter 21 调试Buildroot

It is possible to instrument the steps Buildroot does when building
packages. Define the variable BR2_INSTRUMENTATION_SCRIPTS to contain
the path of one or more scripts (or other executables), in a
space-separated list, you want called before and after each step. The
scripts are called in sequence, with three parameters:

  * start or end to denote the start (resp. the end) of a step;
  * the name of the step about to be started, or which just ended;
  * the name of the package.

For example :

make BR2_INSTRUMENTATION_SCRIPTS="/path/to/my/script1 /path/to/my/script2"

The list of steps is:

  * extract
  * patch
  * configure
  * build
  * install-host, when a host-package is installed in $(HOST_DIR)
  * install-target, when a target-package is installed in $
    (TARGET_DIR)
  * install-staging, when a target-package is installed in $
    (STAGING_DIR)
  * install-image, when a target-package installs files in $
    (BINARIES_DIR)

The script has access to the following variables:

  * BR2_CONFIG: the path to the Buildroot .config file
  * HOST_DIR, STAGING_DIR, TARGET_DIR: see Section 18.6.2,
    generic-package reference
  * BUILD_DIR: the directory where packages are extracted and built
  * BINARIES_DIR: the place where all binary files (aka images) are
    stored
  * BASE_DIR: the base output directory

## Chapter 22 为Buildroot贡献

There are many ways in which you can contribute to Buildroot:
analyzing and fixing bugs, analyzing and fixing package build
failures detected by the autobuilders, testing and reviewing patches
sent by other developers, working on the items in our TODO list and
sending your own improvements to Buildroot or its manual. The
following sections give a little more detail on each of these items.

If you are interested in contributing to Buildroot, the first thing
you should do is to subscribe to the Buildroot mailing list. This
list is the main way of interacting with other Buildroot developers
and to send contributions to. If you aren't subscribed yet, then
refer to Chapter 5, Community resources for the subscription link.

If you are going to touch the code, it is highly recommended to use a
git repository of Buildroot, rather than starting from an extracted
source code tarball. Git is the easiest way to develop from and
directly send your patches to the mailing list. Refer to Chapter 3, 
Getting Buildroot for more information on obtaining a Buildroot git
tree.

### 22.1. 复制、分析和修复bugs

A first way of contributing is to have a look at the open bug reports
in the Buildroot bug tracker [https://bugs.buildroot.org/buglist.cgi?
product=buildroot]. As we strive to keep the bug count as small as
possible, all help in reproducing, analyzing and fixing reported bugs
is more than welcome. Don't hesitate to add a comment to bug reports
reporting your findings, even if you don't yet see the full picture.

### 22.2 分析和修复自动构建失败

Buildroot自动生成器是一组基于随机配置持续运行Buildroot构建的构建机器.
这适用于Buildroot支持的所有架构,使用各种工具链和随机选择的包.
对于Buildroot上的大型提交活动,这些自动构建程序在提交后非常早地检测问题方面有很大的帮助.

All build results are available at http://autobuild.buildroot.org,
statistics are at http://autobuild.buildroot.org/stats.php. Every
day, an overview of all failed packages is sent to the mailing list.

Detecting problems is great, but obviously these problems have to be
fixed as well. Your contribution is very welcome here! There are
basically two things that can be done:

  * Analyzing the problems. The daily summary mails do not contain
    details about the actual failures: in order to see what's going
    on you have to open the build log and check the last output.
    Having someone doing this for all packages in the mail is very
    useful for other developers, as they can make a quick initial
    analysis based on this output alone.
  * Fixing a problem. When fixing autobuild failures, you should
    follow these steps:

     1. Check if you can reproduce the problem by building with the
        same configuration. You can do this manually, or use the
        br-reproduce-build [http://git.buildroot.org/buildroot-test/
        tree/utils/br-reproduce-build] script that will automatically
        clone a Buildroot git repository, checkout the correct
        revision, download and set the right configuration, and start
        the build.
     2. Analyze the problem and create a fix.
     3. Verify that the problem is really fixed by starting from a
        clean Buildroot tree and only applying your fix.
     4. Send the fix to the Buildroot mailing list (see Section 22.5,
        Submitting patches). In case you created a patch against
        the package sources, you should also send the patch upstream
        so that the problem will be fixed in a later release, and the
        patch in Buildroot can be removed. In the commit message of a
        patch fixing an autobuild failure, add a reference to the
        build result directory, as follows:

Fixes: http://autobuild.buildroot.org/results/51000a9d4656afe9e0ea6f07b9f8ed374c2e4069

### 22.3 检查和测试补丁

With the amount of patches sent to the mailing list each day, the
maintainer has a very hard job to judge which patches are ready to
apply and which ones aren't. Contributors can greatly help here by
reviewing and testing these patches.

In the review process, do not hesitate to respond to patch
submissions for remarks, suggestions or anything that will help
everyone to understand the patches and make them better. Please use
internet style replies in plain text emails when responding to patch
submissions.

To indicate approval of a patch, there are three formal tags that
keep track of this approval. To add your tag to a patch, reply to it
with the approval tag below the original author's Signed-off-by line.
These tags will be picked up automatically by patchwork (see
Section 22.3.1, Applying Patches from Patchwork) and will be part
of the commit log when the patch is accepted.

Tested-by
    Indicates that the patch has been tested successfully. You are
    encouraged to specify what kind of testing you performed
    (compile-test on architecture X and Y, runtime test on target A,
    ). This additional information helps other testers and the
    maintainer.
Reviewed-by
    Indicates that you code-reviewed the patch and did your best in
    spotting problems, but you are not sufficiently familiar with the
    area touched to provide an Acked-by tag. This means that there
    may be remaining problems in the patch that would be spotted by
    someone with more experience in that area. Should such problems
    be detected, your Reviewed-by tag remains appropriate and you
    cannot be blamed.
Acked-by
    Indicates that you code-reviewed the patch and you are familiar
    enough with the area touched to feel that the patch can be
    committed as-is (no additional changes required). In case it
    later turns out that something is wrong with the patch, your
    Acked-by could be considered inappropriate. The difference
    between Acked-by and Reviewed-by is thus mainly that you are
    prepared to take the blame on Acked patches, but not on Reviewed
    ones.

If you reviewed a patch and have comments on it, you should simply
reply to the patch stating these comments, without providing a
Reviewed-by or Acked-by tag. These tags should only be provided if
you judge the patch to be good as it is.

It is important to note that neither Reviewed-by nor Acked-by imply
that testing has been performed. To indicate that you both reviewed
and tested the patch, provide two separate tags (Reviewed/Acked-by
and Tested-by).

Note also that any developer can provide Tested/Reviewed/Acked-by
tags, without exception, and we encourage everyone to do this.
Buildroot does not have a defined group of core developers, it just
so happens that some developers are more active than others. The
maintainer will value tags according to the track record of their
submitter. Tags provided by a regular contributor will naturally be
trusted more than tags provided by a newcomer. As you provide tags
more regularly, your trustworthiness (in the eyes of the maintainer)
will go up, but any tag provided is valuable.

Buildroot's Patchwork website can be used to pull in patches for
testing purposes. Please see Section 22.3.1, Applying Patches from
Patchwork for more information on using Buildroot's Patchwork
website to apply patches.

#### 22.3.1 Applying Patches from Patchwork

The main use of Buildroot's Patchwork website for a developer is for
pulling in patches into their local git repository for testing
purposes.

When browsing patches in the patchwork management interface, an mbox
link is provided at the top of the page. Copy this link address and
run the following commands:

```console
$ git checkout -b <test-branch-name>
$ wget -O - <mbox-url> | git am
```

Another option for applying patches is to create a bundle. A bundle
is a set of patches that you can group together using the patchwork
interface. Once the bundle is created and the bundle is made public,
you can copy the mbox link for the bundle and apply the bundle using
the above commands.

### 22.4 完成待办事项列表中的任务

If you want to contribute to Buildroot but don't know where to start,
and you don't like any of the above topics, you can always work on
items from the Buildroot TODO list [http://elinux.org/Buildroot#
Todo_list]. Don't hesitate to discuss an item first on the mailing
list or on IRC. Do edit the wiki to indicate when you start working
on an item, so we avoid duplicate efforts.

### 22.5 提交补丁

Note

请不要给错误附加补丁,而是发送到邮件列表.

If you made some changes to Buildroot and you would like to
contribute them to the Buildroot project, proceed as follows.

#### 22.5.1 The formatting of a patch

We expect patches to be formatted in a specific way. This is
necessary to make it easy to review patches, to be able to apply them
easily to the git repository, to make it easy to find back in the
history how and why things have changed, and to make it possible to
use git bisect to locate the origin of a problem.

First of all, it is essential that the patch has a good commit
message. The commit message should start with a separate line with a
brief summary of the change, prefixed by the area touched by the
patch. A few examples of good commit titles:

  * package/linuxptp: bump version to 2.0
  * configs/imx23evk: bump Linux version to 4.19
  * package/pkg-generic: postpone evaluation of dependency conditions
  * boot/uboot: needs host-{flex,bison}
  * support/testing: add python-ubjson tests

The description that follows the prefix should start with a lower
case letter (i.e "bump", "needs", "postpone", "add" in the above
examples).

其次,提交消息的正文应该描述为什么需要进行此更改,如果有必要,还应该详细说明如何
进行更改.在编写提交消息时,要考虑评审人员将如何阅读它,但也要考虑几年以后当您
再次看到这个更改时将如何阅读它.

第三,补丁本身应该只做一个更改,但要完全更改.两个不相关或弱相关的更改通常应该在
两个独立的补丁中完成.这通常意味着一个补丁只影响一个包.如果几个更改是相关的,通常
仍然可以将它们分割成小补丁,并以特定的顺序应用它们.小补丁更容易检查,并且通常更容易
理解为什么要进行更改.但是,每个补丁必须是完整的.当只应用第一个而不应用第二个补丁时,
不允许构建被破坏.这对于以后使用git bisect是必要的.

Of course, while you're doing your development, you're probably going
back and forth between packages, and certainly not committing things
immediately in a way that is clean enough for submission. So most
developers rewrite the history of commits to produce a clean set of
commits that is appropriate for submission. To do this, you need to
use interactive rebasing. You can learn about it in the Pro Git book
[https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History].
Sometimes, it is even easier to discard you history with git reset
--soft origin/master and select individual changes with git add -i or
git add -p.

Finally, the patch should be signed off. This is done by adding
Signed-off-by: Your Real Name <> at the end of the commit message.
git commit -s does that for you, if configured properly. The
Signed-off-by tag means that you publish the patch under the
Buildroot license (i.e. GPL-2.0+, except for package patches, which
have the upstream license), and that you are allowed to do so. See
the Developer Certificate of Origin [http://developercertificate.org
/] for details.

When adding new packages, you should submit every package in a
separate patch. This patch should have the update to package/
Config.in, the package Config.in file, the .mk file, the .hash file,
any init script, and all package patches. If the package has many
sub-options, these are sometimes better added as separate follow-up
patches. The summary line should be something like <packagename>: new
package. The body of the commit message can be empty for simple
packages, or it can contain the description of the package (like the
Config.in help text). If anything special has to be done to build the
package, this should also be explained explicitly in the commit
message body.

When you bump a package to a new version, you should also submit a
separate patch for each package. Don't forget to update the .hash
file, or add it if it doesn't exist yet. Also don't forget to check
if the _LICENSE and _LICENSE_FILES are still valid. The summary line
should be something like <packagename>: bump to version <new
version>. If the new version only contains security updates compared
to the existing one, the summary should be <packagename>: security
bump to version <new version> and the commit message body should show
the CVE numbers that are fixed. If some package patches can be
removed in the new version, it should be explained explicitly why
they can be removed, preferably with the upstream commit ID. Also any
other required changes should be explained explicitly, like configure
options that no longer exist or are no longer needed.

If you are interested in getting notified of build failures and of
further changes in the packages you added or modified, please add
yourself to the DEVELOPERS file. This should be done in the same
patch creating or modifying the package. See the DEVELOPERS file for
more information.

Buildroot提供了一个方便的工具来检查你创建或修改的文件中常见的编码风格错误,
称为check-package(参见第18.25.2节,如何检查编码风格以获取更多信息).

#### 22.5.2 Preparing a patch series

Starting from the changes committed in your local git view, rebase
your development branch on top of the upstream tree before generating
a patch set. To do so, run:

```console
$ git fetch --all --tags
$ git rebase origin/master
```

Now, you are ready to generate then submit your patch set.

To generate it, run:

```console
$ git format-patch -M -n -s -o outgoing origin/master
```

This will generate patch files in the outgoing subdirectory,
automatically adding the Signed-off-by line.

Once patch files are generated, you can review/edit the commit
message before submitting them, using your favorite text editor.

Buildroot provides a handy tool to know to whom your patches should
be sent, called get-developers (see Chapter 23, DEVELOPERS file and
get-developers for more information). This tool reads your patches
and outputs the appropriate git send-email command to use:

```console
$ ./utils/get-developers outgoing/*
```

Use the output of get-developers to send your patches:

```console
$ git send-email --to buildroot@buildroot.org --cc bob --cc alice outgoing/*
```

Alternatively, get-developers -e can be used directly with the
--cc-cmd argument to git send-email to automatically CC the affected
developers:

```console
$ git send-email --to buildroot@buildroot.org \
      --cc-cmd './utils/get-developers -e' origin/master
```

git can be configured to automatically do this out of the box with:

```console
$ git config sendemail.to buildroot@buildroot.org
$ git config sendemail.ccCmd "$(pwd)/utils/get-developers -e"
```

And then just do:

```console
$ git send-email origin/master
```
注意,git应该配置为使用您的邮件帐户.配置git参见man git-send-email或谷歌搜索它.

If you do not use git send-email, make sure posted patches are not
line-wrapped, otherwise they cannot easily be applied. In such a
case, fix your e-mail client, or better yet, learn to use git
send-email.

#### 22.5.3 Cover letter

If you want to present the whole patch set in a separate mail, add
--cover-letter to the git format-patch command (see man
git-format-patch for further information). This will generate a
template for an introduction e-mail to your patch series.

A cover letter may be useful to introduce the changes you propose in
the following cases:

  * large number of commits in the series;
  * deep impact of the changes in the rest of the project;
  * RFC ^[4];
  * whenever you feel it will help presenting your work, your
    choices, the review process, etc.

#### 22.5.4 Patches for maintenance branches

When fixing bugs on a maintenance branch, bugs should be fixed on the
master branch first. The commit log for such a patch may then contain
a post-commit note specifying what branches are affected:

package/foo: fix stuff

Signed-off-by: Your Real Name <your@email.address>
---
Backport to: 2020.02.x, 2020.05.x
(2020.08.x not affected as the version was bumped)

Those changes will then be backported by a maintainer to the affected
branches.

However, some bugs may apply only to a specific release, for example
because it is using an older version of a package. In that case,
patches should be based off the maintenance branch, and the patch
subject prefix must include the maintenance branch name (for example
"[PATCH 2020.02.x]"). This can be done with the git format-patch flag
--subject-prefix:

```console
$ git format-patch --subject-prefix "PATCH 2020.02.x" \
    -M -s -o outgoing origin/2020.02.x
```

然后用git send-email发送补丁,如上所述.

#### 22.5.5 Patch revision changelog

When improvements are requested, the new revision of each commit
should include a changelog of the modifications between each
submission. Note that when your patch series is introduced by a cover
letter, an overall changelog may be added to the cover letter in
addition to the changelog in the individual commits. The best thing
to rework a patch series is by interactive rebasing: git rebase -i
origin/master. Consult the git manual for more information.

When added to the individual commits, this changelog is added when
editing the commit message. Below the Signed-off-by section, add ---
and your changelog.

Although the changelog will be visible for the reviewers in the mail
thread, as well as in patchwork [http://patchwork.buildroot.org], git
will automatically ignores lines below --- when the patch will be
merged. This is the intended behavior: the changelog is not meant to
be preserved forever in the git history of the project.

Hereafter the recommended layout:

Patch title: short explanation, max 72 chars

A paragraph that explains the problem, and how it manifests itself. If
the problem is complex, it is OK to add more paragraphs. All paragraphs
should be wrapped at 72 characters.

A paragraph that explains the root cause of the problem. Again, more
than one paragraph is OK.

Finally, one or more paragraphs that explain how the problem is solved.
Don't hesitate to explain complex solutions in detail.

Signed-off-by: John DOE <john.doe@example.net>

---
Changes v2 -> v3:
  - foo bar  (suggested by Jane)
  - bar buz

Changes v1 -> v2:
  - alpha bravo  (suggested by John)
  - charly delta

Any patch revision should include the version number. The version
number is simply composed of the letter v followed by an integer
greater or equal to two (i.e. "PATCH v2", "PATCH v3").

This can be easily handled with git format-patch by using the option
--subject-prefix:

```console
$ git format-patch --subject-prefix "PATCH v4" \
    -M -s -o outgoing origin/master
```

Since git version 1.8.1, you can also use -v <n> (where <n> is the
version number):

```console
$ git format-patch -v4 -M -s -o outgoing origin/master
```

When you provide a new version of a patch, please mark the old one as
superseded in patchwork [http://patchwork.buildroot.org]. You need to
create an account on patchwork [http://patchwork.buildroot.org] to be
able to modify the status of your patches. Note that you can only
change the status of patches you submitted yourself, which means the
email address you register in patchwork [http://
patchwork.buildroot.org] should match the one you use for sending
patches to the mailing list.

You can also add the --in-reply-to <message-id> option when
submitting a patch to the mailing list. The id of the mail to reply
to can be found under the "Message Id" tag on patchwork [http://
patchwork.buildroot.org]. The advantage of in-reply-to is that
patchwork will automatically mark the previous version of the patch
as superseded.

### 22.6 报告issue/bugs或获得帮助

Before reporting any issue, please check in the mailing list archive
whether someone has already reported and/or fixed a similar problem.

However you choose to report bugs or get help, either by opening a
bug in the bug tracker or by sending a mail to the mailing list,
there are a number of details to provide in order to help people
reproduce and find a solution to the issue.

Try to think as if you were trying to help someone else; in that
case, what would you need?

Here is a short list of details to provide in such case:

  * host machine (OS/release)
  * version of Buildroot
  * target for which the build fails
  * package(s) for which the build fails
  * the command that fails and its output
  * any information you think that may be relevant

Additionally, you should add the .config file (or if you know how, a
defconfig; see Section 9.3, Storing the Buildroot configuration).

If some of these details are too large, do not hesitate to use a
pastebin service. Note that not all available pastebin services will
preserve Unix-style line terminators when downloading raw pastes.
Following pastebin services are known to work correctly: - https://
gist.github.com/ - http://code.bulix.org/

### 22.7 使用运行时测试框架

Buildroot includes a run-time testing framework built upon Python
scripting and QEMU runtime execution. The goals of the framework are
the following:

  * build a well defined Buildroot configuration
  * optionally, verify some properties of the build output
  * optionally, boot the build results under Qemu, and verify that a
    given feature is working as expected

The entry point to use the runtime tests framework is the support/
testing/run-tests tool, which has a series of options documented in
the tool's help -h description. Some common options include setting
the download folder, the output folder, keeping build output, and for
multiple test cases, you can set the JLEVEL for each.

Here is an example walk through of running a test case.

  * For a first step, let us see what all the test case options are.
    The test cases can be listed by executing support/testing/
    run-tests -l. These tests can all be run individually during test
    development from the console. Both one at a time and selectively
    as a group of a subset of tests.

```console
$ support/testing/run-tests -l
List of tests
test_run (tests.utils.test_check_package.TestCheckPackage)
test_run (tests.toolchain.test_external.TestExternalToolchainBuildrootMusl) ... ok
test_run (tests.toolchain.test_external.TestExternalToolchainBuildrootuClibc) ... ok
test_run (tests.toolchain.test_external.TestExternalToolchainCCache) ... ok
test_run (tests.toolchain.test_external.TestExternalToolchainCtngMusl) ... ok
test_run (tests.toolchain.test_external.TestExternalToolchainLinaroArm) ... ok
test_run (tests.toolchain.test_external.TestExternalToolchainSourceryArmv4) ... ok
test_run (tests.toolchain.test_external.TestExternalToolchainSourceryArmv5) ... ok
test_run (tests.toolchain.test_external.TestExternalToolchainSourceryArmv7) ... ok
[snip]
test_run (tests.init.test_systemd.TestInitSystemSystemdRoFull) ... ok
test_run (tests.init.test_systemd.TestInitSystemSystemdRoIfupdown) ... ok
test_run (tests.init.test_systemd.TestInitSystemSystemdRoNetworkd) ... ok
test_run (tests.init.test_systemd.TestInitSystemSystemdRwFull) ... ok
test_run (tests.init.test_systemd.TestInitSystemSystemdRwIfupdown) ... ok
test_run (tests.init.test_systemd.TestInitSystemSystemdRwNetworkd) ... ok
test_run (tests.init.test_busybox.TestInitSystemBusyboxRo) ... ok
test_run (tests.init.test_busybox.TestInitSystemBusyboxRoNet) ... ok
test_run (tests.init.test_busybox.TestInitSystemBusyboxRw) ... ok
test_run (tests.init.test_busybox.TestInitSystemBusyboxRwNet) ... ok

Ran 157 tests in 0.021s

OK
```

  * Then, to run one test case:

```console
$ support/testing/run-tests -d dl -o output_folder -k tests.init.test_busybox.TestInitSystemBusyboxRw
15:03:26 TestInitSystemBusyboxRw                  Starting
15:03:28 TestInitSystemBusyboxRw                  Building
15:08:18 TestInitSystemBusyboxRw                  Building done
15:08:27 TestInitSystemBusyboxRw                  Cleaning up
.
Ran 1 test in 301.140s

OK
```

The standard output indicates if the test is successful or not. By
default, the output folder for the test is deleted automatically
unless the option -k is passed to keep the output directory.

#### 22.7.1 Creating a test case

Within the Buildroot repository, the testing framework is organized
at the top level in support/testing/ by folders of conf, infra and
tests. All the test cases live under the tests folder and are
organized in various folders representing the category of test.

The best way to get familiar with how to create a test case is to
look at a few of the basic file system support/testing/tests/fs/ and
init support/testing/tests/init/ test scripts. Those tests give good
examples of a basic tests that include both checking the build
results, and doing runtime tests. There are other more advanced cases
that use things like nested br2-external folders to provide skeletons
and additional packages.

Creating a basic test case involves:

  * Defining a test class that inherits from infra.basetest.BRTest
  * Defining the config member of the test class, to the Buildroot
    configuration to build for this test case. It can optionally rely
    on configuration snippets provided by the runtime test
    infrastructure: infra.basetest.BASIC_TOOLCHAIN_CONFIG to get a
    basic architecture/toolchain configuration, and
    infra.basetest.MINIMAL_CONFIG to not build any filesystem. The
    advantage of using infra.basetest.BASIC_TOOLCHAIN_CONFIG is that
    a matching Linux kernel image is provided, which allows to boot
    the resulting image in Qemu without having to build a Linux
    kernel image as part of the test case, therefore significant
    decreasing the build time required for the test case.
  * Implementing a def test_run(self): function to implement the
    actual tests to run after the build has completed. They may be
    tests that verify the build output, by running command on the
    host using the run_cmd_on_host() helper function. Or they may
    boot the generated system in Qemu using the Emulator object
    available as self.emulator in the test case. For example
    self.emulator.boot() allows to boot the system in Qemu,
    self.emulator.login() allows to login, self.emulator.run() allows
    to run shell commands inside Qemu.

在创建测试脚本之后,将自己添加到developer文件中,以成为测试用例的维护者.

#### 2.7.2 Debugging a test case

当一个测试用例运行时,output_folder将包含以下内容:

```console
$ ls output_folder/
TestInitSystemBusyboxRw/
TestInitSystemBusyboxRw-build.log
TestInitSystemBusyboxRw-run.log
```

TestInitSystemBusyboxRw/ is the Buildroot output directory, and it is
preserved only if the -k option is passed.

TestInitSystemBusyboxRw-build.log is the log of the Buildroot build.

TestInitSystemBusyboxRw-run.log is the log of the Qemu boot and test.
This file will only exist if the build was successful and the test
case involves booting under Qemu.

If you want to manually run Qemu to do manual tests of the build
result, the first few lines of TestInitSystemBusyboxRw-run.log
contain the Qemu command line to use.

You can also make modifications to the current sources inside the
output_folder (e.g. for debug purposes) and rerun the standard
Buildroot make targets (in order to regenerate the complete image
with the new modifications) and then rerun the test.

#### 22.7.3 Runtime tests and Gitlab CI

All runtime tests are regularly executed by Buildroot Gitlab CI
infrastructure, see .gitlab.yml and https://gitlab.com/buildroot.org/
buildroot/-/jobs.

You can also use Gitlab CI to test your new test cases, or verify
that existing tests continue to work after making changes in
Buildroot.

In order to achieve this, you need to create a fork of the Buildroot
project on Gitlab, and be able to push branches to your Buildroot
fork on Gitlab.

The name of the branch that you push will determine if a Gitlab CI
pipeline will be triggered or not, and for which test cases.

In the examples below, the <name> component of the branch name is an
arbitrary string you choose.

  * To trigger all run-test test case jobs, push a branch that ends
    with -runtime-tests:

```console
$ git push gitlab HEAD:<name>-runtime-tests
```
  * To trigger one or several test case jobs, push a branch that ends
    with the complete test case name
    (tests.init.test_busybox.TestInitSystemBusyboxRo) or with the
    name of a category of tests (tests.init.test_busybox):

```console
$ git push gitlab HEAD:<name>-<test case name>
```

Example to run one test:

```console
$ git push gitlab HEAD:foo-tests.init.test_busybox.TestInitSystemBusyboxRo
```

Examples to run several tests part of the same group:

```console
$ git push gitlab HEAD:foo-tests.init.test_busybox
$ git push gitlab HEAD:foo-tests.init
```

---------------------------------------------------------------------

^[4] RFC: (Request for comments) change proposal

## Chapter 23 DEVELOPERS文件和get-developers

主Buildroot目录包含一个名为developer的文件,该文件列出了涉及Buildroot各个
领域的开发人员.多亏了这个文件,get-developers工具允许这样做:

  * Calculate the list of developers to whom patches should be sent,
    by parsing the patches and matching the modified files with the
    relevant developers. See Section 22.5, Submitting patches for
    details.
  * Find which developers are taking care of a given architecture or
    package, so that they can be notified when a build failure occurs
    on this architecture or package. This is done in interaction with
    Buildroot autobuild infrastructure.

我们要求开发人员在Buildroot中添加新包、新板或通常的新功能,在developer文件中注册自己.
例如,我们希望开发人员贡献一个新包时,在他的补丁中包含对developer文件的适当修改.

The DEVELOPERS file format is documented in detail inside the file
itself.

The get-developers tool, located in utils/ allows to use the
DEVELOPERS file for various tasks:

  * When passing one or several patches as command line argument,
    get-developers will return the appropriate git send-email
    command. If the -e option is passed, only the email addresses are
    printed in a format suitable for git send-email --cc-cmd.
  * When using the -a <arch> command line option, get-developers will
    return the list of developers in charge of the given
    architecture.
  * When using the -p <package> command line option, get-developers
    will return the list of developers in charge of the given
    package.
  * When using the -c command line option, get-developers will look
    at all files under version control in the Buildroot repository,
    and list the ones that are not handled by any developer. The
    purpose of this option is to help completing the DEVELOPERS file.
  * When using without any arguments, it validates the integrity of
    the DEVELOPERS file and will note WARNINGS for items that don't
    match.

## Chapter 24 Release工程

### 24.1. Releases

Buildroot项目每季度发布一次,每月发布一次bug修复版本.
每年发布的第一个版本是一个长期支持版本LTS.

  * Quarterly releases: 2020.02, 2020.05, 2020.08, and 2020.11
  * Bugfix releases: 2020.02.1, 2020.02.2
  * LTS releases: 2020.02, 2021.02

Releases are supported until the first bugfix release of the next
release, e.g., 2020.05.x is EOL when 2020.08.1 is released.

LTS releases are supported until the first bugfix release of the next
LTS, e.g., 2020.02.x is supported until 2021.02.1 is released.

### 24.2 Development

每个发布周期包括两个月的主分支开发和发布前一个月的稳定.
在此阶段,没有向主控添加新特性,只添加了错误修复.

稳定阶段从标记-rc1开始,直到发布之前,每周都会标记另一个候选发布版本.

为了在稳定阶段处理新特性和版本变化,可以为这些特性创建下一个分支.一旦完成了当前版本,
下一个分支将合并到主版本中,下一个版本的开发周期将继续在主版本中进行.

Part IV. Appendix

目录

25. Makedev语法文档
26. Makeusers语法文档

    26.1. 关于自动UIDs和GIDs的警告

27. 从较老的Buildroot版本中迁移

    27.1. 一般方法
    27.2. 迁移到2016.11
    27.3. 迁移到2017.08

## Chapter 25 Makedev语法文档

makedev语法在Buildroot的多个地方被用于定义权限更改,或者创建哪些设备文件以及如何创建它们,以避免调用mknod.

此语法来自makedev实用程序,在package/makedevs/README文件中可以找到更完整的文档.

它采用空格分隔字段列表的形式,每行一个文件;字段是:

+--------------------------------------------------+
|name|type|mode|uid|gid|major|minor|start|inc|count|
+--------------------------------------------------+

There are a few non-trivial blocks:

  * name is the path to the file you want to create/modify
  * type is the type of the file, being one of:

      + f: a regular file
      + d: a directory
      + r: a directory recursively
      + c: a character device file
      + b: a block device file
      + p: a named pipe
  * mode are the usual permissions settings (only numerical values
    are allowed)
  * uid and gid are the UID and GID to set on this file; can be
    either numerical values or actual names
  * major and minor are here for device files, set to - for other
    files
  * start, inc and count are for when you want to create a batch of
    files, and can be reduced to a loop, beginning at start,
    incrementing its counter by inc until it reaches count

Let say you want to change the permissions of a given file; using
this syntax, you will need to write:

```bash
/usr/bin/foo f 755 0 0 - - - - -
/usr/bin/bar f 755 root root - - - - -
/data/buz f 644 buz-user buz-group - - - - -
```

Alternatively, if you want to change owner/permission of a directory
recursively, you can write (to set UID to foo, GID to bar and access
rights to rwxr-x--- for the directory /usr/share/myapp and all files
and directories below it):

```bash
/usr/share/myapp r 750 foo bar - - - - -
```

On the other hand, if you want to create the device file /dev/hda and
the corresponding 15 files for the partitions, you will need for /dev
/hda:

```bash
/dev/hda b 640 root root 3 0 0 0 -
```

and then for device files corresponding to the partitions of /dev/
hda, /dev/hdaX, X ranging from 1 to 15:

```bash
/dev/hda b 640 root root 3 1 1 1 15
```

Extended attributes are supported if
BR2_ROOTFS_DEVICE_TABLE_SUPPORTS_EXTENDED_ATTRIBUTES is enabled. This
is done by adding a line starting with |xattr after the line
describing the file. Right now, only capability is supported as
extended attribute.

+------------------+
||xattr|capability |
+------------------+

  * |xattr is a "flag" that indicate an extended attribute
  * capability is a capability to add to the previous file

If you want to add the capability cap_sys_admin to the binary foo,
you will write :

```bash
/usr/bin/foo f 755 root root - - - - -
|xattr cap_sys_admin+eip
```

You can add several capabilities to a file by using several |xattr
lines. If you want to add the capability cap_sys_admin and
cap_net_admin to the binary foo, you will write :

```bash
/usr/bin/foo f 755 root root - - - - -
|xattr cap_sys_admin+eip
|xattr cap_net_admin+eip
```

## Chapter 26 Makeusers语法文档

The syntax to create users is inspired by the makedev syntax, above,
but is specific to Buildroot.

The syntax for adding a user is a space-separated list of fields, one
user per line; the fields are:

+---------------------------------------------------------+
|username|uid|group|gid|password|home|shell|groups|comment|
+---------------------------------------------------------+

Where:

  * username is the desired user name (aka login name) for the user.
    It can not be root, and must be unique. If set to -, then just a
    group will be created.
  * uid is the desired UID for the user. It must be unique, and not
    0. If set to -1 or -2, then a unique UID will be computed by
    Buildroot, with -1 denoting a system UID from [100â€¦999] and -2
    denoting a user UID from [1000â€¦1999].
  * group is the desired name for the user's main group. It can not
    be root. If the group does not exist, it will be created.
  * gid is the desired GID for the user's main group. It must be
    unique, and not 0. If set to -1 or -2, and the group does not
    already exist, then a unique GID will be computed by Buildroot,
    with -1 denoting a system GID from [100â€¦999] and -2 denoting a
    user GID from [1000â€¦1999].
  * password is the crypt(3)-encoded password. If prefixed with !,
    then login is disabled. If prefixed with =, then it is
    interpreted as clear-text, and will be crypt-encoded (using MD5).
    If prefixed with !=, then the password will be crypt-encoded
    (using MD5) and login will be disabled. If set to *, then login
    is not allowed. If set to -, then no password value will be set.
  * home is the desired home directory for the user. If set to -, no
    home directory will be created, and the user's home will be /.
    Explicitly setting home to / is not allowed.
  * shell is the desired shell for the user. If set to -, then /bin/
    false is set as the user's shell.
  * groups is the comma-separated list of additional groups the user
    should be part of. If set to -, then the user will be a member of
    no additional group. Missing groups will be created with an
    arbitrary gid.
  * comment (aka GECOS [https://en.wikipedia.org/wiki/Gecos_field]
    field) is an almost-free-form text.

There are a few restrictions on the content of each field:

  * except for comment, all fields are mandatory.
  * except for comment, fields may not contain spaces.
  * no field may contain a colon (:).

If home is not -, then the home directory, and all files below, will
belong to the user and its main group.

Examples:

foo -1 bar -1 !=blabla /home/foo /bin/sh alpha,bravo Foo user

This will create this user:

  * username (aka login name) is: foo
  * uid is computed by Buildroot
  * main group is: bar
  * main group gid is computed by Buildroot
  * clear-text password is: blabla, will be crypt(3)-encoded, and
    login is disabled.
  * home is: /home/foo
  * shell is: /bin/sh
  * foo is also a member of groups: alpha and bravo
  * comment is: Foo user

test 8000 wheel -1 = - /bin/sh - Test user

This will create this user:

  * username (aka login name) is: test
  * uid is : 8000
  * main group is: wheel
  * main group gid is computed by Buildroot, and will use the value
    defined in the rootfs skeleton
  * password is empty (aka no password).
  * home is / but will not belong to test
  * shell is: /bin/sh
  * test is not a member of any additional groups
  * comment is: Test user

### 26.1 关于自动UIDs和GIDs的警告

当更新buildroot或在配置中添加或删除包时,自动uid和gid可能会被更改.
如果持久文件是用该用户或组创建的,这可能会出现问题:升级后,它们会突然有不同的所有者.

因此,建议保留自动id.这可以通过添加一个具有生成的id的users表来完成.
它只需要对实际创建持久文件的uid这样做,例如数据库.

## Chapter 27 从较老的Buildroot版本中迁移

有些版本引入了向后不兼容性.本节解释这些不兼容性,并针对每个不兼容性说明如何完成迁移.

### 27.1 一般方法

要从旧的Buildroot版本迁移,请执行以下步骤.

 1. For all your configurations, do a build in the old Buildroot
    environment. Run make graph-size. Save graphs/file-size-stats.csv
    in a different location. Run make clean to remove the rest.
 2. Review the specific migration notes below and make the required
    adaptations to external packages and custom build scripts.
 3. Update Buildroot.
 4. Run make menuconfig starting from the existing .config.
 5. If anything is enabled in the Legacy menu, check its help text,
    unselect it, and save the configuration.
 6. For more details, review the git commit messages for the packages
    that you need. Change into the packages directory and run git log
    <old version>..â€‰â€”â€‰<your packages>.
 7. Build in the new Buildroot environment.
 8. Fix build issues in external packages (usually due to updated
    dependencies).
 9. Run make graph-size.
10. Compare the new file-size-stats.csv with the original one, to
    check if no required files have disappeared and if no new big
    unneeded files have appeared.
11. For configuration (and other) files in a custom overlay that
    overwrite files created by Buildroot, check if there are changes
    in the Buildroot-generated file that need to be propagated to
    your custom file.

### 27.2 迁移到2016.11

在Buildroot 2016.11之前,一次只能使用一个br2-external树.随着Buildroot 2016.11
出现了同时使用多个的可能性(详细信息,参见章节9.2,保持Buildroot之外的自定义).

然而,这意味着较旧的br2外部树不能按原样使用.需要做一些小更改:向br2-external树添加一个名称.

这只需要几个步骤就可以很容易地完成:

  * 首先,在br2-external树的根处创建一个名为external.desc的新文件,
    用一行定义br2-external树的名称:

```console
    $ echo 'name: NAME_OF_YOUR_TREE' >external.desc
```

    Note. 在选择名称时要小心:它必须是唯一的,并且只能使用集合[a- za -z0-9_]中的ASCII字符.

  * 然后,用新变量更改br2-external树中出现的每一个BR2_EXTERNAL:

```console
    $ find . -type f | xargs sed -i 's/BR2_EXTERNAL/BR2_EXTERNAL_NAME_OF_YOUR_TREE_PATH/g'
```

现在,您的br2-external tree可以在Buildroot 2016.11之后使用.

Note: 这一改变使得您的br2-external树在2016.11之前与Buildroot不兼容.

### 27.3 迁移到2017.08

在Buildroot 2017.08之前,主机包被安装
在$(HOST_DIR)/usr (with e.g. the autotools' --prefix=$(HOST_DIR)/usr).
使用Buildroot 2017.08,它们现在直接安装在$(HOST_DIR).

每当一个包安装一个与$(HOST_DIR)/lib中的库链接的可执行文件时,它必须有一个RPATH指向该目录.

指向$(HOST_DIR)/usr/lib的RPATH不再被接受.
