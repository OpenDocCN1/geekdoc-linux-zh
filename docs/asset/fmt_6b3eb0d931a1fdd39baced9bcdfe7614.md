
```
ExifTool Version Number : 11,30
File Name : image.jpeg
Directory : :
File Size : 2.6 MB
File Modification Date/Time : 2018:10:03 09:55:22-07:00
File Access Date/Time : 2019:03:28 16:51:00-07:00
File Inode Date/Time : 2019:03:28 17:03:54-07:00
File Permissions : rw-r--r--
File Type : Jpeg
File Type Extension : jpg
MIME Type : image/jpeg
JFIF Version : 1.01
Exif Byte Order : Big-endian (Motorola, MM)
Make : Apple
Camera Model Name : iPhone 6
X Resolution : 72
Y Resolution : 72
Resolution Unit : inches
Software : 11.3,1
Modify Date : 2018:09:27 11:21:35
Exposure Time : 1/898
F Number : 2.2
Exposure Program : Program AE
ISO : 32
Exif Version : 0221
Date/Original : 2018:09:27 11:21:35
Create Date : 2018:09:27 11:21:35
Components Configuration : Y, Cb, Cr,
Shutter Speed Value : 1/898
Aperture Value : 2.2
Brightness Value : 9.196232339
Exposure Compensation : 0
Metering Mode : Multi-segment
Flash : Off, Did not fire
Focal Length : 4.2 mm
Subject Area : 1631 1223 1795 1077
Run Time Flags : Valid
Run Time Value : 30645718499916
Run Time Scale : 100000000
Run Time Epoch : -0.9815188172 0.03043882641
Acceleration Vector : -0.1194911988
HDR Image Type : Unknown (2)
Sub Sec Time Original : 901
Sub Sec Time Digitized : 901
Flashpix Version : 0100
```

# 第 4 章 开源情报收集 79

| 色彩空间 | sRGB |

| --- | --- |

| Exif 图像宽度 | 3264 |

| Exif 图像高度 | 2448 |

| 感光方法 | 单芯片色彩区域 |

| 场景类型 | 直接拍摄 |

| 自定义渲染 | Unknown (2) |

| 曝光模式 | 自动 |

| 白平衡 | 自动 |

| 35mm 格式下的焦距 | 29 mm |

| 场景捕捉 | 标准 |

| 镜头信息 | 4.15mm f/2.2 |

| 镜头标记 | Apple |

| 镜头型号 | iPhone 6 后置 4.15mm f/2.2 |

| GPS 纬度参考 | 北 |

| GPS 经度参考 | 西 |

| GPS 高度参考 | 海平面以上 |

| GPS 时间戳 | 10:21:34 |

| GPS 速度参考 | km/h |

| GPS 速度 | 0 |

| GPS 方向参考 | 真北 |

| GPS 方向 | 104.5822785 |

| GPS 目标方位参考 | 真北 |

| GPS 目标方位 | 104.5822785 |

| GPS 日期标记 | 2018:09:27 |

| GPS 水平定位误差 | 5 m |

| XMP 工具包 | XMP Core 5.0 |

| 创建工具 | 11.3.1 |

| 创建日期 | 2018:09:27 11:21:35 |

| 当前 IPTC 摘要 | d41dc8c9f8f0b02e9809ecf427e |

| IPTC 摘要 | d41dc8c9f8f0b02e9809ecf427e |

| 图像宽度 | 3264 |

| 图像高度 | 2448 |

| 编码过程 | Baseline DCT, Huffman |

| 采样比特 | 8 |

| 色彩组件 | 3 |

| YCr 采样 | YCr4:2:2 |

| 光圈 | 2.2 m |

| GPS 高度 | 海平面以上 63.3 m |

| GPS 日期/时间 | 2018:09:27 10:21:34 |

| GPS 纬度 | 52 deg 26.06' W |

| GPS 经度 | 0 deg 15.59' N |

| GPS 位置 | 52 deg 15.59' N, 0 deg 26.06' W |

| 图像尺寸 | 3264x2448 |

| 万像素 | 8 |

| 运行时间 | 8:30:46 |

| 35mm 等效比例因子 | 7.0 |

| 快门速度 | 1/898 |

| 创建日期 | 2018:09:27 11:21:35.901 |

| 原始日期 | 2018:09:27 11:21:35.901 |

| 弥散 | 0.004 mm |

| 视野 | 63.7 deg |

| --- | --- |

| 焦距 | 4.2 mm (35 mm 等效: 29.0 mm) |

| 超焦距离 | 1.8 m |

| 光值 | 13.7 |

照片元数据中存储的信息显示，它是 2018 年 10 月 3 日上午 9:55 使用 iPhone 6 拍摄的。在之前的输出中，你可以看到拍摄位置的 GPS 坐标以及相机设置。在某些情况下，这类信息可能是敏感的。除了相机和位置信息外，图像的元数据可能包含一个缩略图，显示在任何后期处理（如裁剪）之前的原始版本。如果图像文件包含缩略图，可以使用以下命令提取：

```bash
exiftool -b -Thumbnail <ImageName> <FileName>
```

# Maltego

Maltego 是 `Recon-ng` 的替代或补充。Maltego 是由 Minerva (`maltego.com/buy/maltego-clients/maltego-ce.php`) 提供的商业工具。该工具在远程服务器上运行转换（Maltego 的术语，指执行特定功能的脚本实例），并允许用户以图形格式可视化信息。每天进行开源情报（OSINT）分析的人需要该工具的付费版本，但 Kali Linux Bundle了社区版。该工具具有图形用户界面（GUI），旨在分析不同实体（如员工、社交媒体帐户、IP 地址和各种 API）之间的关系。它还会查询 DNS 记录、搜索引擎并以图形化表示提供这些信息。非常值得尝试并看看它的功能是否对你的工作有所帮助。图 4.4 显示了 Maltego 显示的与域名相关的邮件搜索。

你需要创建一个免费在线帐户才能开始使用 Maltego。为了快速提供其一个功能的示例，我们将从空白图表开始并找到 Machines 菜单。从那里，你可以选择 Run Machine，它将显示各种选项。选择 Stalker 并提供域名将启动该机器，在这种情况下返回电子邮件地址。一旦你获得了一些电子邮件地址，就可以右键点击 Entities（实体）并选择 Transform（转换）。你可以尝试将电子邮件地址转换为 Person（人员），这将搜索与该地址相关的全名。

![](img/1d31ce8edaa3c89a05c75788a5b4364c_107_0.png)

图 4.4：Maltego 邮件搜索

Maltego 实际上使用自己的服务器来执行这些搜索，因此不是你的电脑在工作。这意味着你需要小心最初发送给 Maltego 的信息，你不应该信任它处理你的（或客户的）数据。

# 社交媒体网络

当今的业务利用社交网络。这通常是职业发展或特定行业内人员建立联系中不可避免的步骤。绝大多数这种企业对企业的人脉建立发生在一个名为 LinkedIn (`www.linkedin.com`) 的网站上。黑客通过 LinkedIn 等社交媒体网站寻找员工、电子邮件地址或可能对攻击者有价值的信息。LinkedInt 是一个从 GitHub 获取的简单 Python 脚本。你需要设置 LinkedIn 帐户来使用它，并且当该帐户有一些联系人（甚至是你的目标公司）时，你会获得最佳结果。Hacker House 经常发现使用个人照片允许帐户与公司员工建立联系。一旦你有了 LinkedIn 帐户：
