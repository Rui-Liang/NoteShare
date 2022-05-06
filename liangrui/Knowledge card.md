
```ad-note
title:# **TIFF与BigTiff**
collapse: close
&emsp;&emsp;&emsp;&emsp; TIFF（Tag Image File Format，标签图像文件格式）是一种广泛使用的多图像存档文件格式，可以存储多张2D图像，每个像素也可以是1、2或4字节（称位深度或SizeP），它们线性排列在被称为IFD的维度（称I维度）上，每个IFD类似于视频的一“帧”，除了像素数值以外还包含高度（Y维度）、宽度（X维度）等元数据信息，每一项元数据被称为一个标签。TIFF规范规定了每个IFD都必须包含的，所谓必需标签，以及一些可选包含的标签。
&emsp;&emsp;&emsp;&emsp; 经典的TIFF格式存在无法处理>4㎇文件的问题。BigTiff是TIFF格式的变体，解决了4㎇限制的问题。

```ad-note
title:# **OME-TIFF**
collapse: close
&emsp;&emsp;&emsp;&emsp; 但是，很多时候，高、宽、IFD，这3个维度并不足以满足我们的需求，于是出现了OME（Open Microscopy Environment，开放显微镜环境）-TIFF扩展格式，将I维度扩展为C, Z, T三个维度：
&emsp;&emsp;&emsp;&emsp; **C**，Channel，颜色通道。这里指的不是常见的RGB颜色通道，而是拍摄设备所支持的同时工作的记录设备。这些设备往往可以记录不同波长的光信号，包括但不限于RGB，甚至还包括非光学信号。
&emsp;&emsp;&emsp;&emsp; **Z**，深度层级。许多拍摄设备可以对拍摄对象进行多层深度扫描拍摄，形成立体图像，因此需要增加一个Z维度。
&emsp;&emsp;&emsp;&emsp; **T**，Time，时间轴。
&emsp;&emsp;&emsp;&emsp; 这样，OME-TIFF实际上是具有XYCZT这5个维度的图像文件。为了与TIFF格式兼容，它利用了TIFF格式里可选的ImageDescription标签。OME-TIFF规定，在完全满足TIFF规范的基础上，首个IFD的ImageDescription标签变为必需标签。这个标签在TIFF规范中可以是任意的字符串，OME则规范了这个字符串必须为特定的OME-XML格式元数据，用于记录XYCZT各维度尺寸信息，各通道颜色（ChannelColor），各维度在存储空间中的线性排列顺序（DimensionOrder，谁为高维谁为低维），单个像素值的数据类型（PixelType），以及拍摄设备相关的元数据信息。

```

^187640

```ad-note
title: # **DICOM**
collapse: close

&emsp;&emsp;&emsp;&emsp; 医学数字图像通讯协议 （Digital Imaging and Communications in Medicine，DICOM）是广泛应用于放射医疗领域（X射线、CT、核磁共振、超声等）的医学图像国际标准，是医学成像设备中部署最广泛的标准之一。
		
&emsp;&emsp;&emsp;&emsp; 这一标准是美国放射联合会和美国国家电子制 造商协会联合制定的，目的是为了解决由于医疗设备厂 家不同带来的通讯困难等问题。现在国际通用的 DICOM 标准是 3.0 版本，于 1993 年正式发布。
		
&emsp;&emsp;&emsp;&emsp; DICOM 标准详细规定了传输医学影像及其相关信息的 交换方法和交换格式。DICOM 的文件组织是按照患者、研究、序列和图像四个层次进行的。在 DICOM 文件中最 基本的单元是数据元素。DICOM 数据元素主要由四部分组成 ：标签、数据描述、数据长度和数据域。DICOM 中 对应的所有数据元素都可以通过标签来唯一标识，DICOM 中人为将标签分为两个部分：组号和元素。标签和元素的 对应关系可以通过查阅标准来描述。数据描述用以说明数 据对应的类型，数据长度指明数据的字节数，数据域则包含了该数据元素的数据。

![[Pasted image 20220301212758.png]]


```

^042415

```ad-note
title: # **fMRI时间序列**
collapse: closed

&emsp;&emsp;&emsp;&emsp; fMRI是四维的时间序列，也就是在一段时间内不同时间点上的三维图像。那么，只要提取出某一个体素在全部时间上的数据也就得到了这个体素的时间序列。这个时间序列也就代表着这个体素之内血氧水平随时间的变化，也就反映了功能的表现。

```

# H.26x那些事
```ad-note
title: # **变换系数(Transform Coefficients)**
collapse: closed

&emsp;&emsp;变换系数是图像像素信息在变换域中的具体体现。变换系数的大小直接反映图像亮度和能量的整体分布，包含图像纹理和边缘的细节。

&emsp;&emsp;HEVC是基于块进行编码的，其中又可以分为编码单元 (CU)、预测单元(PU)和变换单元(Tu)，其中TU的有关处理涉及大量信息，在视频编码过程中占有重要的作用。在经过一系列的预测、变换(使用具有固定变换矩阵的离散余弦变换（DCT）和离散正弦变换（DST）来计算预测误差残差的变换系数)和量化等处理之后，TU中的变换系数具有非常显著的特点，即数据向左上角高度集中，也就是每个变换单元中只在左上角有少量的非零系数，其他位置的系数大部分都为零,==这种方法可能会导致图像细节的丢失和视觉对比度不足==。
```

^e14a58

```ad-note
title: # **量化参数(quantization parameter)**
collapse: closed
&emsp;&emsp;H.26x的关键技术是码率控制，即在传输带宽受限的情况下，使 H.26x获得较好的重建视频质量。码率控制主要包括设定量化参数(Quantization Parameter，QP)和比特数分配两部分。较小的 QP 值会导致较高的重建视频质量和较低的压缩率，反之亦然。
```

^18ce74

```ad-note
title: # **帧内预测(intra prediction mode)**
collapse: closed

&emsp;&emsp;帧内预测是H.26x编码中用来提升帧内编码压缩效率的编码工具,它通过计算和比较多种帧内预测模式下的宏块率失真代价,并选择最优的帧内预测模式来充分消除图像信号的空间冗余,提升视频信号帧内编码的压缩效率,但多种帧内预测模式下的宏块率失真代价计算使帧内编码运算量成倍增长,阻碍了其实际应用。
```

^fb3cce
```ad-note
title: # **BDBR & BDPSNR**
collapse: closed
&emsp;&emsp;在视频的处理过程中， 常常利用 BD-BitRate(BDBR) 与 BD-PSNR(BDPSNR) 来衡量方法的好坏。它提供的是利用新方法得到的视频相对于原来的方法在码率和PSNR上的变化情况。一般来说，码率降低，PSNR增大，能够说明新方法具有较好的性能。然而，会出现这样一种情况， 即码率相对于原来的方法有所降低，但是PSNR即视频的质量却降低了，在这种情况下想要衡量方法的好坏，就需要利用BDBR和DBPSNR.
	
&emsp;&emsp;Bjøntegaard delta bit rate (BDBR) 表示了在同样的客观质量下，两种方法的码率节省情况(Rate/distortion curves 画一条水平线)

&emsp;Bjøntegaard delta peak signal-to-noise rate (BD-PSNR)表示了在给定的同等码率下，两种方法的PSNR-Y的差异(Rate/distortion curves 画一条垂直线)。
```

^ac2721
