---
title: yolo多卡训练卡死(pytorch)
date: 2025-07-15 21:36:21
tags:
    - pytorch
    - nccl
    - yolo
headimg: '/img/2cuda.png'
---

*请忽略文章封面配图的带nvlink的多卡，实际情况是无nvlink，有nvlink的多卡该教程不奏效*

<!-- more -->

本人在2024年第一次使用RTX 4090 + TITAN RTX 双卡训练yolo时出现卡死的情况
（初始化阶段） 

经过大量检索找到了解决办法  
来源：[https://github.com/Megvii-BaseDetection/YOLOX/issues/1289#issuecomment-1409988436](https://github.com/Megvii-BaseDetection/YOLOX/issues/1289#issuecomment-1409988436)
### 仅允许IP套接字通信
训练前在终端输入：
```bash
export NCCL_LL_THRESHOLD=0
export NCCL_P2P_DISABLE=1
export NCCL_IB_DISABLE=1
```
也可以写入python脚本（使用os，问ai）
**NCCL_P2P_DISABLE** 变量禁用点对点 （P2P） 传输，该传输使用 NVLink 或 PCI 在 GPU 之间使用 CUDA 直接访问。  
**NCCL_IB_DISABLE** 变量禁用 NCCL 要使用的 IB/RoCE 传输。相反，NCCL 将回退到使用 IP 套接字。  

**解释**
对于分布式训练，子进程始终被初始化[dist.init_process_group](https://github.com/Megvii-BaseDetection/YOLOX/blob/f5331eaac5c03f73f59274522fe0507a030c5386/yolox/core/launch.py#L186-L190)由TCP 协议控制
因此，仅使用 IP 通信似乎是合理的。 

**警告**
NCCL_LL_THRESHOLD 通常设置为零。  
可能会影响模型性能。
[https://github.com/NVIDIA/nccl/issues/369#issue-678319427](https://github.com/NVIDIA/nccl/issues/369#issue-678319427)  

**建议**：多卡训练尽量显存相同，同时性能差距尽量小，否则影响速度和训练性能

-->end

>如果这帮助了你，可以对提出该解决方法的作者star or fllow [https://github.com/ZXYFrank](https://github.com/ZXYFrank)  
If this helps you, you can star or fllow the author who proposed the solution