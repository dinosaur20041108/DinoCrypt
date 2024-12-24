# DinoCrypt

## 一、基本概述

DinoCrypt可能是一款专注于文件加密的软件，旨在为用户提供安全、便捷的文件保护服务。

## 二、核心功能

1. **文件加密**：DinoCrypt采用加密算法AES对文件进行加密，确保文件数据在存储和传输过程中的安全性。加密后的文件将变得不可读，只有拥有相应解密密钥的用户才能访问其内容。
2. **用户友好的界面**：为了降低使用难度，DinoCrypt可能设计有简洁直观的用户界面和便捷的操作方式。这使得用户无需具备专业的技术背景也能轻松上手，快速完成文件的加密和解密操作。

## 三、应用场景

DinoCrypt可能适用于多种场景，如个人文件保护、企业数据保密等。对于个人用户而言，它可以帮助保护个人隐私和敏感数据；对于企业用户而言，它则有助于确保商业机密和客户信息的安全性。


## 使用教程

加密恐龙是一个免费、开源的加密软件。此程序采用 [AES-256-GCM](https://www.w3.org/TR/WebCryptoAPI/#aes-gcm) 加密算法和[WebCryptoAPI](https://www.w3.org/TR/WebCryptoAPI/#aes-gcm) 。该软件源代码可以随时下载到本地电脑，离线运行.  

因为所有的加密和解密过程都在您的本地电脑运行，所以你会发现加密和解密的速度非常快，加密一个1Gb的文件仅仅需要10秒左右。  

操作步骤： 1. 上传一个本地文件 2. 输入密码 3.文件加密后，点击下载按钮，选择存储到您本地的电脑或者移动硬盘.

## 问答

##### 如果有一天你这个网站倒闭了，我到哪里去解密我的文件？

**完全不用担心.** 我们的软件不用链接互联网，本地点击运行文件夹里面的index.html文件即可.如果某一天该网站倒闭或者被某些国家的防火墙屏蔽，你只需要保存好该软件的离线源代码即可。

##### 这个软件免费吗?

**是的.** 加密恐龙是一个免费的离线加密软件。

##### 有mac/linux/windows的客户端吗?

没有，这个程序大小不到2M，您可以直接下载源代码到您的本地浏览器运行即可，为什么还需要安装客户端？不浪费您的硬盘空间吗？Ok，如果您还想仍然坚持使用客户端软件，可以到github上提issue

##### 有文件大小和类型限制吗?

没有，您可以加密任何格式的文件，例如zip、mp4、mp3、jpg等等。我们建议您先压缩您的所有文件到一个zip或者tar压缩包，然后加密这个压缩包，这样加密的速度更快

##### 这个软件安全吗?

当然，为什么不安全？这个加密软件采用 [AES-GCM](https://www.w3.org/TR/WebCryptoAPI/#aes-gcm) 算法.  
整个加密和解密的过程都在您本地的离线电脑运行. 服务器不存储任何数据，该软件的源代码也是100%开源的。打个比方，一个软件的源代码是开源的，就好像一道菜的制作方法和原材料是公开的，这样你就知道这道菜有没有毒，卫不卫生，能不能吃。

##### 我忘记了我的加密密码，我可以找回我的密码吗？

**不能，** 我们的服务器不存储任何数据, 我们也不存储任何用户资料，一旦您丢失了您的密码，您将无法解密您的文件。所以，我们强烈建议您务必保存好您自己设置的密码