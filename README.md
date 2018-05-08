<blockquote>写在前面的话，几周前完成的安装，真是段痛苦的经历，大学御用的笔记本崩了，不想再拆机买配件修了，直接入了一台小米pro低配版，8G+256G

macos真的是太好用，已经回不去windows10了，之所以还装了win10，是因为没事还要打打游戏啊

以前用御用asus笔记本装过ubuntu16和win10双系统，但是驱动支持不好(主要是手势操作)，太难用

也有可能现在改善了，其实现在win10的手势也不错了，但比起mac还是差一截

适合用一定装系统经验的人安装，因为遇到各种各样的问题。</blockquote>
<blockquote>新电脑推荐先装macos再装win10，因为mac需要的引导分区大于200M，而预装的win10家庭版的引导分区只有100M。

所以我直接干掉了预装的win10，装完mac之后再装win10专业版。

并且这样不用一个u盘即写入mac镜像，又写入pe工具箱，还得调整u盘分区特别麻烦。</blockquote>
<h1>装备工作</h1>
<ol>
 	<li>mac镜像，<a href="https://mirrors.dtops.cc/iso/MAC%20OS/%E9%BB%91%E6%9E%9C%E5%B0%8F%E5%85%B5/macOS%20High%20Sierra%2010.13.3%2817D47%29%20Installer%20with%20Clover%204391.dmg" target="_blank" rel="noopener">迅雷下载链接</a>，<a href="https://pan.baidu.com/s/1bqmWMLp">百度云</a>https://pan.baidu.com/s/1bqmWMLp，密码：7pu8</li>
 	<li>8G及以上U盘，做pe推荐<a href="http://www.wepe.com.cn/download.html">微PE</a></li>
 	<li>EFI文件<a href="https://github.com/kkyv/XiaoMIPro/blob/master/efi.zip">efi.zip</a></li>
 	<li>TransMac软件<a href="https://github.com/kkyv/XiaoMIPro/blob/master/tmsetup_10-3.exe">tmsetup_10-3.exe</a></li>
</ol>
<h2>用TransMac克隆镜像到U盘</h2>
<p style="padding-left: 60px;">下载安装transmac，然后写入镜像到u盘就好了，很简单</p>
<p style="padding-left: 60px;"><img class="size-medium wp-image-87 alignleft" src="http://123.207.110.218/wp-content/uploads/2018/05/TransMac1-300x221.png" alt="" width="300" height="221" /></p>
&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;
<h2>修改BIOS，从U盘启动</h2>
由于小米bios默认开启了安全认证，无法加载其他的uefi启动，也就是需要关闭才能从u盘启动

先设置bios密码才能关掉认证，
<p style="padding-left: 30px;"><code>开机F2--》BIOS--》Security--》Set Supervisor Password--》输入密码--》确认</code></p>
<p style="padding-left: 30px;"><code>然后：Security--》Secure Boot Mode--》选择Disable--》F10保存退出</code></p>
从U盘启动：
<p style="padding-left: 30px;"><code>开机F10--》BIOS--》BootManger--》选择EFI USB Device</code></p>
进入后：
<img class="size-medium wp-image-88 alignleft" src="http://123.207.110.218/wp-content/uploads/2018/05/XiaoMiCloverboot-300x225.png" alt="" width="300" height="225" />

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

只有一个图标，选择进入系统
<h2>安装MacOS</h2>
之后可以看到选择语言界面：选择<code>简体中文</code>进入到：实用工具界面

<img class="size-medium wp-image-92 alignleft" src="http://123.207.110.218/wp-content/uploads/2018/05/ParallelsPicture0-300x225.png" alt="" width="300" height="225" />

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

选择实用工具--》选择显示所设备

<img class="size-medium wp-image-93 alignleft" src="http://123.207.110.218/wp-content/uploads/2018/05/WX20180508-135611-300x198.png" alt="" width="300" height="198" />

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

选择自带的硬盘--》抹掉（全盘抹掉的好处会自动生成200m的esp引导分区）

<img class="size-medium wp-image-94 alignleft" src="http://123.207.110.218/wp-content/uploads/2018/05/WX20180508-140136-300x197.png" alt="" width="300" height="197" />

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

完成后退出<code>磁盘工具</code>，选择<code>安装MacOs</code>，基本就是无脑下一步下一步下一步

不要设置的尽量不设置，像登陆appid之类的以后用到再登陆，但是设置用户名密码是必须的，得设置

完成之后就可以进入到MacOS的界面了，很激动有没有，但还剩最后一步
<h2>把EFI拷贝到磁盘的EFI引导启动</h2>
Mac使用挂载的方式加载分区，因为EFI是隐藏的，所以需要命令来挂载EFI分区

首先找到终端，然后使用<code>diskutil</code>命令，<code>diskutil list</code>查看所有的磁盘分区

<img class="size-medium wp-image-95 alignleft" src="http://123.207.110.218/wp-content/uploads/2018/05/WX20180508-141431-300x193.png" alt="" width="300" height="193" />

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

然后可以看到256G的磁盘的efi分区为<code>disk0s1</code>，再用<code>diskutil mount disk0s1</code>挂载efi分区（名字加）

就能够在访达（文件管理）里面操作efi分区了，删除efi文件夹，拷贝下载的efi到分区

下载的efi文件夹里面有<code>BOOT</code>和<code>CLOVER</code>文件夹

<img class="size-medium wp-image-96 alignleft" src="http://123.207.110.218/wp-content/uploads/2018/05/WX20180508-141822-300x190.png" alt="" width="300" height="190" />

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

这样，MacOS的安装就完成了，

&nbsp;

安装Windows待续。。。
