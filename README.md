# NWU-ipmi-病理图像组生存手册

[TOC]

## 服务器使用手册

### Linux 常用命令

* 路径 cd ls

* 文件：mkdir touch cat vim
* 权限： chmod  chown
* 查看显卡使用情况： nvidia-smi 、watch -n 1 nvidia-smi（实时监控显卡状态）
* [详细]([Linux 命令大全 | 菜鸟教程 (runoob.com)](https://www.runoob.com/linux/linux-command-manual.html))

### 安装ubuntu系统

如果拿到学长学姐服务器，安装系统前务必询问学长学姐是否有资料需要保存，及时机器目前处于无法开机状态，也可以使用试用模式保存硬盘文件。

需要准备：4G以上u盘、[ubuntu镜像安装包](https://cn.ubuntu.com/download/server/step1)、[软碟通](https://cn.ultraiso.net/xiazai.html)

流程：下载ubuntu镜像安装包(推荐非最新版本)——>使用软碟通制作启动U盘——>在主机中安装 [安装参考](https://www.zhihu.com/tardis/zm/art/379049774?source_id=1005)

# 硬盘挂载

linux下的硬盘使用与windows使用硬盘逻辑区别很大。首先默认安装系统的盘称为系统盘，它会被挂载在根目录"/"下，可以使用"df -h" 查看硬盘的挂载情况，使用"fdisk -l"查看分区情况。 假如有一块新的硬盘要被使用，流程为：设置好分区——> 创建好需要挂载的目录——>使用mount临时挂载、修改/etc/fstab文件开机自动挂载。[参考教程](https://blog.csdn.net/weixin_44578029/article/details/118464216)

设置分区格式化硬盘推荐使用系统自带的工具磁盘进行操作。

### 安装驱动

* 安装驱动前，确保gcc和make已经被安装。

* 为什么安装好的驱动，某次重启后就掉了？

安装好驱动后需要固定ubuntu的内核版本，否则使用apt update会自动升级内核，导致内核和驱动版本不匹配。[内核固定方法参考](https://blog.csdn.net/maohule/article/details/107370788)

* 为什么安装好驱动后，什么都没有运行，使用nvidia-smi却看到有进程占用显存？

如果没有打开核显输出，并正确配合显示输出和安装驱动，就会使用独显显示输出。这样会在跑大型模型时出现显示时延变大，图形化界面死机的情况。正确安装驱动流程大致为：完全卸载原有驱动——> 进入tty命令行界面并关闭图形化显示服务——>使用下载好的[安装包](https://www.nvidia.cn/Download/index.aspx?lang=cn)（推荐）或ppa仓库安装驱动——>配置显示器输出，最后重启。[具体方法参考](https://gist.github.com/wangruohui/bc7b9f424e3d5deb0c0b8bba990b1bc5) [关闭图形化界面参考](https://www.jianshu.com/p/36dcf5185f01))

* 安装好驱动配置核显输出后，有可能会出现花屏现象解决方案：[参考教程](https://zhuanlan.zhihu.com/p/439088148?utm_campaign=shareopn&utm_medium=social&utm_oi=1119270340852854784&utm_psn=1640407976681816064&utm_source=wechat_session)

### ssh远程使用服务器

使用公共服务器，多人无法同时使用向日葵远程桌面，所以需要用到ssh。

使用流程：在ubuntu主机中安装好anaconda（[安装参考及使用教程](https://blog.csdn.net/m0_50117360/article/details/108403586)），创建需要使用的虚拟环境——>在自己电脑上安装Pycharm**专业版**配置ssh连接使用服务器[参考教程](https://blog.csdn.net/sdkjkfk/article/details/108202094))。





## 学习路线

| 内容            | 学习参考                                                     | 备注                                                         |
| --------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 常用指标        | [ROC,AUC](https://www.bilibili.com/video/BV1wz4y197LU/?spm_id_from=333.788.recommend_more_video.-1&vd_source=a589ab38fbe0cdb7bab7ac68fb414f0a)   [Acc, Precision,Recall,F1](https://www.bilibili.com/video/BV1vt4y117Zz/?spm_id_from=333.999.0.0&vd_source=a589ab38fbe0cdb7bab7ac68fb414f0a) | 言简意赅，清晰明了                                           |
| Inception_v3    | 文献： [Rethinking the Inception Architecture for Computer Vision.](https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Szegedy_Rethinking_the_Inception_CVPR_2016_paper.pdf) | GoogLeNet的主要网络结构                                      |
| DeepLabv3       | 文献：[Rethinking Atrous Convolution for Semantic Image Segmentation.](https://arxiv.org/abs/1706.05587)  [b站霹雳吧啦Wz.](https://www.bilibili.com/video/BV1Jb4y1q7j7/?spm_id_from=333.337.search-card.all.click&vd_source=a589ab38fbe0cdb7bab7ac68fb414f0a) |                                                              |
| YOLOv1-v3       | [b站同济子豪兄. YOLOv1 YOLOv2 ](https://space.bilibili.com/1900783) | YOLO系列学习建议学完v1直接学v7                               |
| Transformer     | [B站李沐](https://www.bilibili.com/video/BV1pu411o7BE/?spm_id_from=333.999.0.0) | 学长给的论文中有，视频结合论文                               |
| Vitransformer   | [B站李沐](https://www.bilibili.com/video/BV15P4y137jb/?spm_id_from=333.999.0.0&vd_source=e2b27549479cf820a4b63da8210be1e2) | 学长给的论文中有，视频结合论文                               |
| SwinTransformer | [B站李沐](https://www.bilibili.com/video/BV13L4y1475U/?spm_id_from=333.999.0.0&vd_source=e2b27549479cf820a4b63da8210be1e2) | 学长给的论文中有，视频结合论文                               |
| Mask R-CNN      | B站霹雳吧啦Wz（Faster R-CNN）--》[B站FPN](https://www.bilibili.com/video/BV1dh411U7D9/?spm_id_from=333.788.recommend_more_video.1)--》[B站FCN](https://www.bilibili.com/video/BV1J3411C7zd/?spm_id_from=333.999.0.0)--》[B站霹雳（Mask R-CNN）](https://www.bilibili.com/video/BV1ZY411774T/?spm_id_from=333.999.0.0) | 根据第二列视频顺序观看，再结合论文                           |
| YOLOV7          | [github项目](https://github.com/WongKinYiu/yolov7) [B站自由时有船](https://space.bilibili.com/1420484560) | 建议先看论文再看视频，论文github项目中有                     |
| GNN             | [GNN](https://www.bilibili.com/video/BV1iT4y1d7zP/?spm_id_from=333.337.search-card.all.click)、[GCN](https://www.bilibili.com/video/BV18U4y1x7gi/?spm_id_from=333.337.search-card.all.click) | 关于GNN/GCN的基础知识                                        |
| nnU-Net         | [b站](https://www.bilibili.com/video/BV1iN411d7wz/?spm_id_from=333.337.search-card.all.click&vd_source=a589ab38fbe0cdb7bab7ac68fb414f0a) | 别人的论文汇报和大佬的追问                                   |
| P2PNet          | [论文解读1](https://www.jiqizhixin.com/articles/2021-10-05-9)、[论文解读2](https://zhuanlan.zhihu.com/p/443685614) |                                                              |
| 多实例          | [文献1](https://sci-hub.wf/10.1016/B978-0-12-816176-0.00027-2)  [文献2](https://openaccess.thecvf.com/content/CVPR2021/html/Li_Dual-Stream_Multiple_Instance_Learning_Network_for_Whole_Slide_Image_Classification_CVPR_2021_paper.html) | 目前尚未找到很好的介绍多实例的中文教程。 文献1是对多实例的综述 |





## 实用工具

优秀可靠的工具一定不是免费的，付费使用工具一定是最便捷可靠的方法。

* [clash](https://github.com/Dreamacro/clash) : This is a powerful scientific internet tool that requires subscription purchased on other platforms. By importing the subscription into the tool, you can achieve scientific internet access. It has a traffic detection function. If you access external websites, it will use a proxy. By default, it will not use a proxy to access domestic websites such as Baidu. This is where it is superior to v2ray and shadowrocket. In fact, you don't need to understand how it works, just use it simply. [Thunder](https://58sd.net/#/knowledge) is a proxy purchasing platform that I often use. Although I have put its tutorial here, it is not my recommendation to you, because there must be cheaper, more stable and faster platforms. If you find any, please open an issue and let me know. Thanks.
* [chatgpt](https://chat.openai.com/) : 无需多言。 [注册使用教程](https://www.youtube.com/watch?v=NWJeRBMpsx8)
* [typore](https://typora.io/) ：这是一款好用的Markdown和latex写作工具，支持导出word,pdf等各种格式。[markdown基本语法教程](https://markdown.com.cn/basic-syntax/) [latex公式手册](https://www.cnblogs.com/1024th/p/11623258.html)
* [IDM](https://www.internetdownloadmanager.com/) : 下载管理器，可以集成在浏览器中，支持动态分段下载。

* [kfb文件转svs(windows)](https://github.com/WilmerWang/SLFCD/releases/tag/0.0.1) : 官方工具，可以结合脚本实现批文件转换。

* [APEX](https://github.com/NVIDIA/apex) :  这是一个NVIDIA的官方工具， 它提供一些工具和技术加速模型的训练，或者使用FP16精度来计算模型从而降低显存消耗。首先需要判断[显卡是否支持FP16](https://blog.csdn.net/u011119817/article/details/120055088), 然后[安装官方工具](https://zhuanlan.zhihu.com/p/320402663)。该工具对python、pytorch、cuda、cudnn的版本都有要求，且安装会碰到各种棘手问题。

* [rsync](https://www.ruanyifeng.com/blog/2020/08/rsync.html): 这是一个用于在服务器与服务器之间传输数据的工具，在校园网内网中主机间传输可达100M/s。
