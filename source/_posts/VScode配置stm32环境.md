---
title: VScode配置STM32环境
date: 2024-07-5 03:00:23
tags:
    - VScode
    - Embedded IDE
headimg: '/img/vscodekokeil.png'
---

使用Embedded IDE在vscode上部署keil arm环境，一举解决keil开发难受的问题
vscode，爽！

<!-- more -->

<span style="font-size: x-large;">基于Embedded IDE在vscode上配置STM32环境</span>

前面配置了c51，当然少不了stm32嘿嘿

**话不多说直接开干**


还是使用EIDE与vscode，这里不过多赘述

<br>

### 打开EIDE安装扩展工具包
分别是cppcheck、GNU Arm Embedded Toolchain、OpenOCD

![image](../img/gju.png)
### 安装cortex-debug
>vscode插件

![image](../img/codex.png)

### 设置编译环境
>**第一步：打开EIDE扩展设置**

在vscode的扩展里头找到EIDE右键打开EIDE的扩展设置

![image](../img/kuoz.png)

>**第二步：在打开的设置中找到ARMCC5与ARMCC6两个框**

![image](../img/byi2.png)

>**第三步：将keil的ARM目录下的两个编译器路径填入**

打开keil的安装目录（qrm架构的），打开下面的ARM目录，可以看到前面两个文件夹分别是ARMCC与ARMCLANG

![image](../img/amrr.png)

>将它们的分别路径复制（右键有复制路径的选项），粘贴到刚刚打开的两个框中,最后就像这样

![image](../img/byi.png)

### 设置工具链（这一步可能已经不需要了）

按照图片打开工具链选择

![iamge](../img/gjul.png)

>选择kel目录下的TOOLS.INI

![image](../img/toools.png)
结束

### 新建或导入项目（导入可以导入keil项目）

打开项目之后有这些选项，我们导入芯片支持包

![iamge](../img/xp.png)

>第一个选项是联网下载，我们有离线包，选第二个选项
随后选择我们当时安装的pack包就好了

![image](../img/park.png)



构建配置选择默认，烧录配置按照我的来就好

![image](../img/stlin.png)

*别问为什么不选stlink，因为配置麻烦，而openocd支持stlink，其他默认就好了现在我们可以编译试试了*



**点击这两个都可以编译**

![image](../img/byss.png)

当你看到下面一堆绿色……

![image](../img/yd.png)

恭喜！！！编译成功，配置完成

**让我们一鼓作气试试烧录**

点击旁边这个看起来像下载的按钮，烧录！

![image](../img/slss.png)

当你看到你的stlink开始闪烁，并且出现以下的界面

![image](../img/slcg.png)
再次恭喜！！！烧录成功！！！

### 一些小tips
>不要使用中文文件名，会报错

有许多功能与界面对应着keil，如：
>添加包含的文件夹
{% tabs tab-id %}
<!-- tab EIDE -->

![image](../img/baohan.png)

<!-- endtab -->

<!-- tab keil -->

![image](../img/baohan2.png)

<!-- endtab -->
{% endtabs %}
>构建器选项
{% tabs tab-id %}
<!-- tab EIDE -->

![image](../img/gjian.png)

<!-- endtab -->

<!-- tab keil -->

![image](../img/gjian2.png)

<!-- endtab -->
{% endtabs %}