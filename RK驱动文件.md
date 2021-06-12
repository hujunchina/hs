# CAMERA驱动文件

<<<<<<< HEAD
## 1、sensor驱动成功

### 1.1log查看sensor驱动匹配到

dmesg | grep gc2053

rockchip-mipi-dphy-rx ff4b8000.csi-dphy: match m01_f_gc2053 3-0037:bus type 4

1.2
=======
## 1、电压

![img](IMG/%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16217694488073.png)

0ms，1ms，2ms是指供电顺序，DOVDD先供电，DVDD等1ms再供电，AVDD等DVDD供电结束，等待2ms再供电。

sensor工作期间，一直上电；等你将sensor退出的时候，在反过来下电；针对嵌入式设备，一般没有下电要求，但是像手机这种，会有要求。

sc2310:模拟电压AVDD2.8v，数字电压DOVDD1.8v，数字电压也是GPIO口的电压，应与I2C电压一致

，否则I2C通信不上；核工作电压DVDD1.5v；

### 1.1DTS&sensor驱动

sensor驱动中函数：static const struct i2c_device_id sc2310_match_id[] = {

  { "smartsens,sc2310", 0 },

  { },

};

dts中compatible = "smartsens,sc2310";需要与驱动中字符串保持一致，否则驱动中的probe函数调用不到；

remote-endpoint = <&mipi_ucam_out1>;是指sensor端的port名；data-lanes = <1 2>;mipi的lane数；

#### 1.1.1多sensor注册：

sensor0->csi_dphy0->csi2->vicap->isp0->ispp0

sensor1->csi_dphy1->isp1->ispp1

#### 1.1.2 I2C地址

reg = <0x30>; //sensor I2C设备地址，7位；若sensor的data sheet中写8位，需要右移一位，因为最后一位是读和写。sc2310的sensor数据手册写的sensor id是7位表示，0X30；GC2053数据手册的sensor id是8位表示，0x6e，需要右移一位，I2C地址为0X3f；OV9732数据手册中的sensor的i2c地址为6c和10；

## 2、驱动文件

### 2.1 I2C协议

struct i2c_client {

  unsigned short flags;    /* div., see below   */

  unsigned short addr;    /* chip address - NOTE: 7bit  */

​          /* addresses are stored in the */

​          /* _LOWER_ 7 bits    */

  char name[I2C_NAME_SIZE];

  struct i2c_adapter *adapter;  /* the adapter we sit on  */

  struct device dev;   /* the device structure   */

  int init_irq;      /* irq set at initialization  */

  int irq;      /* irq issued by device   */

  struct list_head detected;

### 2.2获取RK定义的私有资源

  ret = of_property_read_u32(node, RKMODULE_CAMERA_MODULE_INDEX,

​          &sc2310->module_index);

  ret |= of_property_read_string(node, RKMODULE_CAMERA_MODULE_FACING,

​            &sc2310->module_facing);

  ret |= of_property_read_string(node, RKMODULE_CAMERA_MODULE_NAME,

​            &sc2310->module_name);

  ret |= of_property_read_string(node, RKMODULE_CAMERA_LENS_NAME,

​            &sc2310->len_name);

### 2.3枚举支持的初始化列表

sc2310->cfg_num = ARRAY_SIZE(supported_modes);

### 2.4时钟

xvclk用于接收CPU 输出的24 MHz 的工作时钟，sensor内部产生的帧同步信号VSYNC、行同步信号HREF、像素时钟信号PCLK 等3 个时钟信号传入ARM 芯片中， 用于控制图像采集。每一个VSYN C 脉冲表示一帧图像数据采集的开始， HREF 的高电平则表示采集一行图像数据， 图像传感器按从左到右的顺序在每个PCLK脉冲过程中依次采集一个字节的数据， 直到一帧图像数据全部采集完成

sc2310->xvclk = devm_clk_get(dev, "xvclk");

  if (IS_ERR(sc2310->xvclk)) {

​    dev_err(dev, "Failed to get xvclk\n");

​    return -EINVAL;

  }









>>>>>>> a1e857e6d1743f10c00675bb18cbd824288e8266
