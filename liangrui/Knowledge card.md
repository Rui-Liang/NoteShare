
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


