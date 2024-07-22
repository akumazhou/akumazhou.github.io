# Windows自动登录




## 一.设置自动登录的方法

找到运行窗口后输入control userpasswords2或者netplwiz代码并按下回车键

{{< image src="./20231012042328133.jpg" >}}

在跳转界面中点击用户属性一览，如下图所示取消对用户名密码输入的勾选

{{< image src="./20231012042328412.jpg" >}}

点击保存后即可看到系统已经设置为自动登录效果

{{< image src="./20231012042328442.jpg" >}}



## 二.没有“使用本计算机,用户必须输入用户名和密码”选项的解决办法

　　要实现Win10自动登录，通常办法是按win+r，输入netplwiz或是control userpasswords2 回车，调出用户帐号界面，把“要使用本计算机，用户必须输入用户名和密码”前面的勾去掉，输入帐号密码。

　　但有些电脑，会出现“要使用本计算机，用户必须输入用户名和密码”选项不见的情况

{{< image src="./c77e1d05534f00d51c92cee9870e67b1feead79c.png@!web-article-pic.webp" >}}

　　解决方法，桌面新建文本文件，输入以下文字

Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\PasswordLess\Device];

"DevicePasswordLessBuildVersion"=dword:00000002

"DevicePasswordLessBuildVersion"=dword:00000000

　　然后另存为“恢复.reg”，双击，点“是”确认(注意扩展名不是txt)

{{< image src="./776710a9479ff4e01bfa258b51e8f694bfcb48f1.png@!web-article-pic.webp" >}}



　　也可以按按win+r，输入regedit，回车，然后在注册表中修改相应的值，其原始值是2，改为0即可。

{{< image src="./564cdcba569c21fb0103120d0302fb9394f531b0.png@1256w_888h_!web-article-pic.webp" >}} 






