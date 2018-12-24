---
layout: post
---
### 前言
其实制作`USB`启动盘的方法很多，譬如使用命令行，使用第三方工具。这个教程主要介绍使用命令行创建`USB`启动盘。因为这是目前我了解到的最稳妥、简单，而且没有兼容性问题的方法了。  
本教程使用 Yosemite 作为示例。

### 操作步骤

#### 1. 准备工作
1. 准备一个8G以上的`U`盘，确保里面的数据已经妥善备份好了(该过程会格式化全部数据)
2. 下载需要制作启动盘的正式版系统程序(可以从`AppStore`或者网盘下载)
3. 如果是从`AppStore`下载的，可能会自动运行，直接退出安装即可。
4. 如果是从网盘下载的，需要解压并将压缩包中的`Install OS X Yosemite.app`(或者`安装 OS X Yosemite.app`)移动到「应用程序」文件夹里面

#### 2. 格式化`U`盘
插入你的`U`盘，然后在「应用程序」-> 「实用工具」里面找到「磁盘工具」并打开，或者直接使用`Spotlight`搜索「磁盘工具」打开  
  
1. 在左方列表中找到`U`盘的名称并点击
2. 在右边顶部选择「分区」，然后在「分区布局」选择「1个分区」
3. 在分区信息中的「名称」输入`Test`(这个名称是自定义的，后面的命令会用到，保持一致即可)
4. 在「格式」中选择「`Mac OS` 扩展(日志式)」
5. 在「选项」中选择「`GUID`分区表」，然后点击「好」
6. 最后点击「应用」开始对U盘进行格式化

#### 3. 开始制作启动盘
再次确认`Install OS X Yosemite.app`在应用程序中

1. 在「应用程序」-> 「实用工具」中找到「终端」并打开，或者使用`Spotlight`搜索「终端」并打开
2. 赋值下面的命令，并粘贴到「终端」中运行

```
sudo /Applications/Install\ OS\ X\ Yosemite.app/Contents/Resources/createinstallmedia --volume /Volumes/Test --applicationpath /Applications/Install\ OS\ X\ Yosemite.app --nointeraction
```

3. 运行后，根据系统系统是输入管理员密码，接下来就等待系统制作就可以了。这时「终端」会陆续显示类似一下信息：

```
Erasing Disk: 0%... 10%... 20%... 30%...100%...
Copying installer files to disk...
Copy complete.
Making disk bootable...
Copying boot files...
Copy complete.
Done.
```

当你看到最后有 `Copy complete` 和 `Done`字样就表示启动盘已经制作完成了

#### 4. U盘启动安装系统的方法
当你插入制作完成的 `OS X Yosemite` `U`盘启动盘之后，桌面出现`Install OS X Yosemite`的盘符那么就表示启动盘是正常的了。那么怎样通过`USB`启动进行全新的系统安装呢？  
其实很简单，先在目标电脑上插上`U`盘，然后重启你的`Mac`，然后一直按住`option`(`alt`) 按键不放，直到屏幕显示多出一个`USB`启动盘的选项。
这时选择`U`盘的图标回车，即可通过`U`盘来安装`Yosemite`了！这时，你可以直接覆盖安装系统(升级)，也可以在磁盘工具里面格式化抹掉整个硬盘，或者重新分区等实现全新的干净的安装。