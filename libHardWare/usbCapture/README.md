# UsbCapture

## 一、简要说明

UsbCapture封装相机操作，提供__usb免驱UVC协议相机__（ov2710相机）在linux系统下的驱动与使用。该相机模块驱动基于__v4l2库__ （linux自带）和__OpenCV__库。其中v4l2用于读取采集的图片数据，opencv用于显示图片。该模块作为RMdemo一个组件进行开发。

* 本模块参考了__Robomaster2016 DJI开源代码__ 。

### a.运行环境：

* ubuntu 16.04
* opencv 3.0

### b.三个版本

__普通usbcapture版本:__

* 没有帧延迟，即获取的图片为最新的。
* 可实时调整相机参数：分辨率，曝光时间，增益，对比度，白平衡，色彩饱和度，伽玛值，亮度值等。

__多线程usbcapture版本:__

* 单独线程采集图片。
* 每次读取的图片皆为最新的，所以如果连续图像采集，会出现等待时间。
* 可实时调整相机参数：分辨率，曝光时间，增益，对比度，白平衡，色彩饱和度，伽玛值，亮度值等。
* 接口松动引起的断线重连

__基于opencv多线程usbcapture版本：__

- 单独线程采集图片。
- 每次读取的图片皆为最新的，所以如果连续图像采集，会出现等待时间。
- 三个版本中，延迟最低
- 可实时调整相机参数：分辨率
- 接口松动引起的断线重连

### c.其他说明

__兼容性：__

* 3个版本的使用API统一，即基本相同，向下兼容。

__可能出现的问题：__

* 打开相机后，可能会出现前面几张读取错误，或读取到黑屏图片。（不超过10张），通过初始化给予延时，读取几张图片废弃，后续将正常。
* 相机拔插可能会导致相机号的变化，可以采用udev固定相机设备路径方法解决。

## 二、基本使用

创建

```c++
UsbCapture　cap;
```

初始化

```c++
/** 相机初始化函数(不包括相机参数初始化)
　* @param:std::string videoPath,相机设备名
  *  @param: int width,相机分辨率的宽度值。
  *  @param: int height,相机分辨率的高度值。
  *  @return: int ,错误码，0代表无错误。
  */
int init(std::string videoPath,int width,int heigh);
```

获取图片

```c++
/** 图片获取函数
 *  @param: Mat &img,　Mat类的引用，目标图像存放。
 *  @return: int ,错误码，0代表无错误。
 */
int getImg(Mat &img);
```

### 详细API

* 参考注释

## 三、版权及许可证

uestc robomaster2018

- gezp email:1350824033@qq.com

UsbCapture is provided under the [GPL-v3](COPYING).

