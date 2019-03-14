其实本身我对CocoaPods就半知半解的，但是好在网上的教程都讲解得很是详尽，所以当出现如下的问题时我还没有很慌张。


1、提示更新

![](https://raw.githubusercontent.com/bw4uf/bw4uf.github.io/master/_posts/CocoaPods更新出错及解决方案pics/reminder.png)

2、找不到gem，直接404了

![](https://raw.githubusercontent.com/bw4uf/bw4uf.github.io/master/_posts/CocoaPods更新出错及解决方案pics/install.png)

3、访问文件也是404

![](https://raw.githubusercontent.com/bw4uf/bw4uf.github.io/master/_posts/CocoaPods更新出错及解决方案pics/404.png)

4、访问[ruby.taobao.org](https://ruby.taobao.org)的时候，有了重大发现：原来是淘宝把HTTP协议改成了HTTPS协议，才导致了原先的问题。

![](https://raw.githubusercontent.com/bw4uf/bw4uf.github.io/master/_posts/CocoaPods更新出错及解决方案pics/taobao.png)

5、这里的curl方法是朋友教我的，差距就这么显现出来了，所以还是要多多学习啊。

![](https://raw.githubusercontent.com/bw4uf/bw4uf.github.io/master/_posts/CocoaPods更新出错及解决方案pics/success.png)

6、搞定，更到了0.39.0版本。

![](https://raw.githubusercontent.com/bw4uf/bw4uf.github.io/master/_posts/CocoaPods更新出错及解决方案pics/done.png)


感谢朋友[@小龙同学](https://github.com/longkai)的帮助!
