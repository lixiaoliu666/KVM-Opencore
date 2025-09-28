本项目源于https://github.com/thenickdude/KVM-Opencore/releases 他的V21版本，这个版本修复了直通独显卡900秒（20分钟）问题（其实他是没修复的，他的oc里面是没加-v参数的，他可能觉得解决了问题，觉得是蓝牙导致的，其实-v开启了一样出卡900秒或者20分钟才能进系统问题）。

This project is based on the V21 release of [thenickdude/KVM-Opencore](https://github.com/thenickdude/KVM-Opencore/releases). This version claims to fix the "900-second (20-minute) boot delay issue" caused by discrete GPU passthrough, but in reality, the problem persists. The OpenCore (OC) configuration in this release does not include the -v boot argument (verbose mode), which might have led the author to mistakenly assume the issue was resolved (potentially attributing it to Bluetooth-related causes). However, even with the -v parameter manually enabled, the system still experiences the same 900-second delay or 20-minute boot time before successfully entering macOS.

要支持amd免驱独显，我编辑他的config.plist在里面增加启动超时来开默认启动（比如3秒，config.plist->Misc->Boot->Timeout等待时间->设置为3秒左右,当然你也可以设置为其他值），以及加amd独显参数config.plist->NVRAM->7C436110-AB2A-4BBB-A880-FE41995C9F82->boot-args->增加 agdpmod=pikera

To support native AMD GPU compatibility, I edited the config.plist to configure a boot timeout value for enabling the default boot entry（such as 3s，config.plist->Misc->Boot->Timeout->input 3s）.and added amd gpu args  config.plist->NVRAM->7C436110-AB2A-4BBB-A880-FE41995C9F82->boot-args->added agdpmod=pikera

另外他的V21目前不支持6600免驱15系统（rx560可以免驱，6600老是点不亮），我和黑苹果屋经过测试，觉得解决办法是oc从0.9.9升级1.0.2，具体操作就是下载最新的oc1.0.2的空白配置，空白配置里面的acpi文件夹和kexts文件夹都是空的，也没有配置文件，把efi整个文件夹替换kvm-opencore的efi整个文件夹，就这样成功了，然后我用diskgenis软件把他做成了一个img文件，可以直接pve管理界面光驱iso那直接上传进去，以及在虚拟机中添加ide的0编号光驱（也可以sata的0编号光驱），直接选择加载这个img，并且设置这个光驱为默认开机选项！！不仅6600免驱点不亮问题解决了，重启连带win虚拟机死机问题也解决了，重启连带pve物理机死机问题也解决了，随便更新macos新版本也解决了。一声感叹，终于解决了这么多无聊问题。

Additionally, his V21 currently does not support the RX 6600 without a driver on macOS 15 (the RX 560 can work without a driver, but the RX 6600 always fails to light up). After testing with the imacos.top, we found that the solution is to upgrade OpenCore (OC) from version 0.9.9 to 1.0.2.
The specific operation is as follows: Download the latest blank configuration of OC 1.0.2. The "acpi" and "kexts" folders in the blank configuration are empty, and there is no configuration file. Replace the entire "efi" folder of kvm - opencore with this new "efi" folder. After that, it was successful.
Then, I used the DiskGenius software to create an img file, which can be directly uploaded in the optical drive ISO section of the PVE management interface. In the virtual machine, add an IDE optical drive with number 0 (you can also use a SATA optical drive with number 0), directly select and load this img file, and set this optical drive as the default boot option.
Not only was the problem of the RX 6600 failing to light up without a driver solved, but also the issues such as the Windows virtual machine crashing during restart and the PVE physical machine crashing during restart were resolved. The problem of updating to new macOS versions was also solved. I have to say, finally getting rid of so many annoying problems is really a relief.

如果你觉得可以，可以下载我Releases中的kvm-opencore1.0.2V21-131415amd.img直接使用就是

If you think it's feasible, you can download the kvm-opencore1.0.2V21-131415amd.img directly from my Releases section and use it right away.

详细使用可以访问b站我的文章：https://www.bilibili.com/opus/999921111571365906 oc去掉-v参数解决pve黑苹果重启关机导致pve物理机死机问题，提升运行稳定性

For detailed usage instructions, please visit my Bilibili article: https://www.bilibili.com/opus/999921111571365906. By removing the -v parameter in OC (OpenCore), the issue of PVE host machine crashes caused by Hackintosh reboots/shutdowns can be resolved, thereby enhancing operational stability.
## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=lixiaoliu666/KVM-Opencore&type=Date)](https://www.star-history.com/#lixiaoliu666/KVM-Opencore&Date)
