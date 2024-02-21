---
title: m3u8与mp4的互相转化
date: 2024-02-22 01:02:22
tags:
---

## 什么是m3u8？
:::info
正常来说，我们的视频格式都是mp4，但是mp4并不适合网络传播，在线播放视频将会十分困难，m3u8的出现改变了这一切，M3U8 是一种常用的视频流媒体播放列表格式，它使用分片（Chunk）的方式将视频内容切分成多个小片段，以便在网络上进行传输和播放。下面是关于 M3U8 分片原理的简要讲解：
:::

1. 原始视频切片：首先，将原始视频文件切分成短小的视频片段。这些片段通常是几秒钟到几十秒钟的长度，并且以.ts（Transport Stream）为扩展名。切片的目的是为了提供更好的网络传输和流媒体播放体验。
2. 生成 M3U8 播放列表：在切片完成后，生成一个 M3U8 播放列表文件。这个文件是一个文本文件，其中包含了视频片段的信息和顺序。M3U8 播放列表使用标准的文本格式，可以在任何文本编辑器中打开和查看。
3. 分片的索引和时长：M3U8 播放列表中的每个片段都有一个唯一的 URL，用于指定该片段的位置和访问方式。此外，每个片段还包含了其时长信息，以便播放器可以准确地控制和显示视频的进度。
4. 自适应码率：M3U8 还支持自适应码率（Adaptive Bitrate）功能。在自适应码率中，同一段视频会根据用户的网络带宽和设备性能，提供多个不同分辨率和比特率的版本。播放器可以根据当前的网络状况，选择适合的视频分辨率和比特率进行播放，以提供最佳的观看体验。
5. 动态加载和播放：当用户开始播放 M3U8 文件时，播放器会根据 M3U8 播放列表中的信息，动态加载视频片段并按照顺序播放。播放器会根据每个片段的时长和码率，自动控制缓冲和下载速度，以确保连续的播放和流畅的体验。
:::info
一言以蔽之，m3u8是一种视频格式，它的出现使网络视频传播变得非常流畅
:::
## 为什么mp4格式不适合网络传播？

1.  文件大小：MP4 文件通常相对较大，特别是对于高分辨率和高比特率的视频来说。这导    致在网络传输过程中需要更长的时间和更大的带宽来下载和播放。对于用户来说，下载大  型的 MP4 文件可能需要等待时间较长，尤其是在网络连接较慢的情况下。
2. 缓冲和加载时间：由于 MP4 文件的大小，播放器在开始播放之前需要先下载一部分视频内容进行缓冲。这意味着用户可能需要等待一段时间才能开始观看视频，特别是对于较长的视频来说。在网络不稳定或带宽有限的情况下，缓冲和加载时间可能会更长。
3.  不适应网络波动：MP4 文件通常需要完全下载后才能开始播放。这意味着如果网络连接中断或不稳定，用户可能无法顺利播放视频。在网络传输过程中，如果发生网络波动或中断，用户可能需要重新下载整个视频文件或等待缓冲重新开始。
:::info
总的来说，MP4 文件适合本地播放和存储，而对于网络传播和流媒体播放，使用专门的流媒体格式如 M3U8 更为合适，可以提供更好的用户体验和适应性。
:::
## m3u8与mp4可以互相转化吗？
可以!!
但是需要通过一些工具，如FFmpeg等，接下来将会有一个详细的教程告诉大家怎么将m3u8转化成mp4.

- 以腾讯课堂视频下载为例
### 1.获取工具包

- share.gdmuna.com
### 2.获取腾讯课堂视频
  第一步：登录到下载器

- 在浏览器登录自己的腾讯课堂账号，随后右键点击检查打开控制台，输入document.cookie,复制结果

![s6.jpg](https://cdn.nlark.com/yuque/0/2023/jpeg/34408084/1691420246520-0292320a-4dd3-43a2-b9a5-a53333332645.jpeg#averageHue=%23d1d1cb&clientId=uc70ebef9-0448-4&from=ui&id=u08dbef8c&originHeight=1341&originWidth=2238&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=309927&status=done&style=none&taskId=u2cfda94a-cd42-4152-9695-b20e5f741b0&title=)

- 使用记事本打开这个文件

![s1.5.png](https://cdn.nlark.com/yuque/0/2023/png/34408084/1691420330243-21094b43-5ead-40f0-9965-821c26cdf234.png#averageHue=%23fdfcfb&clientId=uc70ebef9-0448-4&from=ui&id=ubfa0da07&originHeight=821&originWidth=1136&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=43571&status=done&style=none&taskId=u58cf7a75-223b-47fe-8360-2f57d717d0d&title=)

- 在这个地方把刚刚复制的cookie粘贴进去

![s2.png](https://cdn.nlark.com/yuque/0/2023/png/34408084/1691420415049-1ad2a294-3473-4547-b871-4e6473f83e77.png#averageHue=%23f4f3f2&clientId=uc70ebef9-0448-4&from=ui&id=ua8894b6e&originHeight=968&originWidth=1680&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=88197&status=done&style=none&taskId=u059453e1-012d-4c8e-b4e6-bfb5e65b6af&title=)
![s9.png](https://cdn.nlark.com/yuque/0/2023/png/34408084/1691420472142-d2ee31ff-b117-4c94-aa6a-37aca45e6c60.png#averageHue=%23eeebe9&clientId=uc70ebef9-0448-4&from=ui&id=u8aedc023&originHeight=968&originWidth=1680&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=111499&status=done&style=none&taskId=ubbd134ae-02e1-4b5e-a470-64a29eb49ab&title=)

- 打开这个软件

![s0.png](https://cdn.nlark.com/yuque/0/2023/png/34408084/1691419719275-b5414c75-929f-4586-aa6f-133b9fe1000b.png#averageHue=%23fdfcfb&clientId=uc70ebef9-0448-4&from=ui&id=vZsau&originHeight=821&originWidth=1136&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=43264&status=done&style=none&taskId=u15f9748d-3fc7-420f-b10c-ae098af9c03&title=)

- 输入login查看登录状态

![s35.png](https://cdn.nlark.com/yuque/0/2023/png/34408084/1691420638863-d3f2aac5-19af-43f4-9cbf-fb777cde4a5b.png#averageHue=%23111111&clientId=uc70ebef9-0448-4&from=ui&id=u5142afa5&originHeight=966&originWidth=1752&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=53167&status=done&style=none&taskId=u318d08a2-302f-41b4-8d8c-0bc678b6aef&title=)

- 获取腾讯课堂的cid，复制这串数字

![s4.png](https://cdn.nlark.com/yuque/0/2023/png/34408084/1691420704138-aefcc808-40c6-492e-bd99-a9fe54994732.png#averageHue=%2392876c&clientId=uc70ebef9-0448-4&from=ui&id=u0e32744f&originHeight=1352&originWidth=2240&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=486263&status=done&style=none&taskId=u2d159473-1f37-4210-af42-523fd98e00d&title=)

- 回到控制台，输入tree -c <cid>

![ss.png](https://cdn.nlark.com/yuque/0/2023/png/34408084/1691420898222-dea8a948-0e26-47b1-9119-f691a5cbd672.png#averageHue=%23161616&clientId=uc70ebef9-0448-4&from=ui&id=ud89ad0a9&originHeight=966&originWidth=1752&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=124091&status=done&style=none&taskId=u72167bdc-3758-4db9-8cca-97e6150f05d&title=)

- 选择要下载的视频，输入d 编号 下载，一般来说，编号1就是下载全部

![微信截图_20230807230942.png](https://cdn.nlark.com/yuque/0/2023/png/34408084/1691421007250-feff8fe9-20fa-4eba-ac7f-91d97ec704f3.png#averageHue=%23181818&clientId=uc70ebef9-0448-4&from=ui&id=u21891735&originHeight=966&originWidth=1752&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=108433&status=done&style=none&taskId=u87870165-e296-4c3c-b29d-8e0be8d74fe&title=)
![ssss.png](https://cdn.nlark.com/yuque/0/2023/png/34408084/1691421097873-e397dc62-32ab-426f-a20b-b7cdc25ea9ab.png#averageHue=%23111111&clientId=uc70ebef9-0448-4&from=ui&id=ueaa16aec&originHeight=966&originWidth=1752&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=30780&status=done&style=none&taskId=u9904fc99-c613-4827-8db5-e19c825276a&title=)

- 下载好之后存放在这个文件夹中，是m3u8格式

![微信截图_20230807231238.png](https://cdn.nlark.com/yuque/0/2023/png/34408084/1691421210307-67034468-3f5a-4338-848f-62d2ca68e670.png#averageHue=%23fdfcfc&clientId=uc70ebef9-0448-4&from=ui&id=ued58f19f&originHeight=821&originWidth=1136&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=37531&status=done&style=none&taskId=uebfc9ebd-6361-4079-9b24-5fd0628a410&title=)
### 3.转化成mp4

- 点击上面的download文件夹，直到打开m3u8文件

![微信截图_20230807231557.png](https://cdn.nlark.com/yuque/0/2023/png/34408084/1691421480642-4e86e8c1-0841-468d-8851-80a27b01e234.png#averageHue=%23faf8f8&clientId=uc70ebef9-0448-4&from=ui&id=u073b5e50&originHeight=1083&originWidth=1398&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=93749&status=done&style=none&taskId=u108f3d3b-7413-42ca-beaa-910111c9046&title=)

- 打开并且右键这个文件复制文件路径（必须要这个文件）

![微信图片编辑_20230807231656.jpg](https://cdn.nlark.com/yuque/0/2023/jpeg/34408084/1691421548037-787fc49a-be0e-47dc-955f-9681831233e3.jpeg#averageHue=%23ebe8df&clientId=uc70ebef9-0448-4&from=ui&id=u806d3839&originHeight=1055&originWidth=1349&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=178950&status=done&style=none&taskId=u2be4ac2e-3d69-438c-a0bd-cd7fbc9373b&title=)

- 打开这个软件

![微信截图_20230807232014.png](https://cdn.nlark.com/yuque/0/2023/png/34408084/1691421687061-b09a7b38-af69-42a6-af2d-5f6a36693654.png#averageHue=%23fdfcfc&clientId=uc70ebef9-0448-4&from=ui&id=uccc12101&originHeight=821&originWidth=1136&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=38105&status=done&style=none&taskId=u3593959c-d279-4b8d-a7a0-717014efb05&title=)

- 把刚刚复制的路径粘贴到这里面，然后点击go

![7232346.png](https://cdn.nlark.com/yuque/0/2023/png/34408084/1691421873899-662db8a7-c0d7-4091-9ba0-b974abf0f562.png#averageHue=%23323337&clientId=uc70ebef9-0448-4&from=ui&id=ub1ca03dc&originHeight=918&originWidth=630&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=55662&status=done&style=none&taskId=u271f1603-cdc3-4f04-96fa-2b14d6f6742&title=)

- 然后就会开始下载

![微信截图_20230807232449.png](https://cdn.nlark.com/yuque/0/2023/png/34408084/1691421924091-69d12e43-3a26-45a4-b818-1cf48655ac12.png#averageHue=%23141414&clientId=uc70ebef9-0448-4&from=ui&id=u44b9339e&originHeight=966&originWidth=1752&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=116432&status=done&style=none&taskId=u5114bdfb-d492-478a-8692-99dad8dfaab&title=)

- 下载完之后，会有一个文件夹

![微信截图_20230807232701.png](https://cdn.nlark.com/yuque/0/2023/png/34408084/1691422109723-6066e43f-cb6e-4a25-9a4c-25de0c69645f.png#averageHue=%23fdfcfb&clientId=uc70ebef9-0448-4&from=ui&id=u88c9b0a3&originHeight=821&originWidth=1136&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=42888&status=done&style=none&taskId=u28d8658d-7440-4a98-979a-796de6a7030&title=)

- 打开之后就有mp4文件了！！！

![微信截图_20230807232730.png](https://cdn.nlark.com/yuque/0/2023/png/34408084/1691422159084-ffa4bb01-9b5e-4dff-824f-3017c559be46.png#averageHue=%23f9f8f7&clientId=uc70ebef9-0448-4&from=ui&id=u2eea4295&originHeight=1083&originWidth=1398&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=115895&status=done&style=none&taskId=u6cc82b72-a097-4ce5-a418-8d5658af158&title=)
## 免责声明
本文仅供学习和研究目的，提供有关特定主题的信息和指导。请注意以下重点强调的免责声明，以确保您理解并遵守本文的使用目的。

1. 仅供学习研究：本文的目的是为读者提供学习和研究特定主题的参考资料。它不应被视为专业建议、指导或解决方案的替代品。读者在使用本文中的任何内容时，应自行评估其适用性，并在必要时寻求专业意见。
2. 个人责任：本文中的任何建议、指导或观点仅代表作者个人的意见和观点，并不代表本平台或任何其他组织或个人的立场。读者在根据本文的内容进行任何行动或决策时，应自行承担个人责任，并对其结果负责。
3. 第三方内容和链接：本文可能包含指向第三方网站、资源或内容的链接。这些链接仅为方便读者提供，并不构成对这些第三方内容的认可、推荐或担保。我们对这些第三方内容的准确性、安全性和合法性不承担任何责任。
4. 免责声明的适用范围：本免责声明适用于本文的所有内容，包括文字、图像、链接和其他形式的信息。本文的阅读和使用即视为您已接受本免责声明，并同意自行承担使用本文内容所产生的风险和责任。
