# NXP JN5169 zigbee 3.0 protocol stack source code for Xiaomi 39 yuan wireless switch (also supports green rice wireless switch upgrade version)
-All kinds of JS are welcome to plagiarize

#### Remarks
-Aiming at Xiaomi's 39 yuan wireless switch, the code implementation on the NXP JN5169 platform can realize the multicast sending of signals after the button is pressed, instead of the official firmware, it can only be realized to the gateway (short address 0x0000) Send the report attribute unicast command, so that you must rely on the gateway to control other devices, and the multicast method can be separated from the gateway
-Based on DimmerSwitch sample project development
-Working in end device mode, the sleep power consumption after entering the network is 1.3uA, the working power consumption is relatively high, the network power consumption is about ten milliamperes, the multicast sending command is about 2 milliamperes, and the deep sleep current is 0.2uA
-After entering the network, the default wake-up period is the number of minutes defined by ZED_TIMEOUT_2048_MIN, because the original sample code calls ZPS_bAplAfSetEndDeviceTimeout(ZED_TIMEOUT_16384_MIN) to set the maximum child aging timeout, which is in line with the child aging characteristics. After two years of actual measurement, the power consumption is indeed very low. A CR2032 battery can last about one year
-The LED is connected to the DIO11 pin, pull it high and turn it off, pull it low to light up
-The function key in the middle of the board is connected to the DIO16 DIO17 pin, which is triggered by the falling edge. It is not clear why the same key is connected to DIO16 and DIO17 through two 1K resistors. It stands to reason that one is enough
-The network distribution button is connected to DIO0, triggering on the falling edge
-The multicast address can be configured through instructions and written into PDM to save, and the multicast address can be read automatically after power-on again
-During the network access phase, all channels try to enter the network by steering, if it fails, go directly to deep sleep
-Multicast address can be configured through BASIC cluster
-Long press the network configuration button for more than 5s, the LED starts to flash 6 times quickly, automatically exit the network and re-steering into the network, after the successful network access, the LED flashes 3 times
-The coordinator is powered off and the rejoin fails, then it enters deep sleep
-Endpoint parameter configuration, [app.zpscfg editing method reference](https://blog.csdn.net/code_style/article/details/90487512)
-Private protocol has been supported, the code is in sdk\JN-SW-4170\Components\ZCL\Clusters\Private, you can choose to use the private protocol report attribute and gateway to achieve linkage control

#### Xiaomi 39 yuan wireless switch hardware line sequence diagram
-![pic](https://img-blog.csdnimg.cn/20190527165744956.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NvZG4,color_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NvZG4F,size
-The so-called upgraded version of Green Rice Switch is the same chip used in Xiaomi's 39 yuan wireless switch, even the buttons and the LED indicator line sequence are exactly the same, but the shell is different
#### Lvmi wireless switch (upgraded version) hardware line sequence diagram
![pic](pic0.png)

#### Branch
-master wireless switch (Millet 39 yuan wireless switch white round, green rice wireless switch upgrade version)
-lvmi_wxkg green rice wireless switch (86 panel wall mounted, including 1 button, 2 button, 3 button)

#### Known issues
-None

#### How to compile
-import project to BeyondStudio
![pic](how2build_0.png)

-select Active "DimmerSwitch,JN5169,DR1199" configuration in properties of project
![pic](how2build_1.png)

#### Programming method
-Enter the ISP mode first (the ISP pin is grounded, and RESET can be entered at the same time)
```
JN51xxProgrammer.exe -s COM7 -P115200 --eraseflash=full -f C:\NXP\bstudio_nxp\Application\JN-AN-1219-Zigbee-3-0-Controller-and-Switch\DimmerSwitch\Build\DimmerSwitch_JN5169_DR1199.bin
```

![pic](https://am.zdmimg.com/201603/10/56e1344deed61.jpg_e680.jpg)
![pic](https://am.zdmimg.com/201609/25/57e74c058d09f.jpg_e600.jpg)

-Upgraded version of Lumi wireless switch
![pic](pic3.jpg)

-Upgraded version of Lumi wireless switch
![pic](pic1.jpg)

-Upgraded version of Lumi wireless switch
![pic](pic2.jpg) 


# NXP JN5169 zigbee 3.0 协议栈source code for 小米39元无线开关(同时支持绿米无线开关升级版)
- 欢迎各种JS前来抄袭

#### 备注
- 针对小米39元无线开关，在NXP JN5169平台的代码实现，在按键按下之后能够实现组播的方式向外发送信号，而不是官方自带的固件，只能实现向网关(短地址0x0000)发送report attribute单播指令，这样就必须依赖网关才能实现对其他设备的控制,组播的方式可以脱离网关
- 基于DimmerSwitch示例工程开发
- 工作在end device模式，入网后休眠功耗1.3uA，工作功耗比较高，入网功耗大概十几毫安，组播发送指令2毫安左右，深度休眠电流0.2uA
- 入网之后默认唤醒周期为ZED_TIMEOUT_2048_MIN定义的分钟数，因为原来的示例代码调用了ZPS_bAplAfSetEndDeviceTimeout(ZED_TIMEOUT_16384_MIN)设置的是最大的child aging超时时间，符合child aging特性，经过两年实测，功耗的确很低，一颗CR2032电池可以续航一年左右
- LED连接的是DIO11引脚，拉高灭，拉低亮
- 板子中间功能键连接的是DIO16 DIO17引脚，下降沿触发，这里不清楚为什么同一个按键，通过两个1K电阻分别连接到DIO16和DIO17上，按理说一个足够了
- 配网按钮连接的是DIO0，下降沿触发
- 可以通过指令配置组播的地址，并写入PDM保存，重新上电自动读取组播地址
- 入网阶段所有信道尝试steering入网，如果失败，直接进入深度休眠
- 通过BASIC cluster可以配置组播地址
- 长按网络配置按钮超过5s，LED开始快速闪烁6次，自动退网并重新steering入网，入网成功之后，LED长闪烁3次
- 协调器断电，导致rejoin失败，则进入深度休眠
- endpoint参数配置，[app.zpscfg编辑方法参考](https://blog.csdn.net/code_style/article/details/90487512)
- 已支持私有协议，代码在sdk\JN-SW-4170\Components\ZCL\Clusters\Private，可以选择使用私有协议report attribute和网关实现联动控制

#### 小米39元无线开关硬件线序图
- ![pic](https://img-blog.csdnimg.cn/20190527165744956.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NvZGVfc3R5bGU=,size_16,color_FFFFFF,t_70)
- 所谓绿米开关升级版，和小米39元无线开关用的同一款芯片，连按键，LED指示灯线序都一模一样，只是外壳不一样
#### 绿米无线开关(升级版)硬件线序图
![pic](pic0.png)

#### 分支
- master 无线开关(小米39元无线开关白色圆形，绿米无线开关升级版)
- lvmi_wxkg 绿米无线开关(86面板贴墙式，包含1键，2键，3键)

#### 已知问题
- 无

#### 如何编译
- import project to BeyondStudio 
![pic](how2build_0.png)

- select Active "DimmerSwitch,JN5169,DR1199" configuration in properties of project
![pic](how2build_1.png)

#### 烧写方法
- 先进入ISP模式(ISP引脚接地，同时RESET复位即可进入)
```
JN51xxProgrammer.exe -s COM7 -P115200 --eraseflash=full -f C:\NXP\bstudio_nxp\Application\JN-AN-1219-Zigbee-3-0-Controller-and-Switch\DimmerSwitch\Build\DimmerSwitch_JN5169_DR1199.bin
```

![pic](https://am.zdmimg.com/201603/10/56e1344deed61.jpg_e680.jpg)
![pic](https://am.zdmimg.com/201609/25/57e74c058d09f.jpg_e600.jpg)

- 绿米无线开关升级版 
![pic](pic3.jpg)

- 绿米无线开关升级版
![pic](pic1.jpg)

- 绿米无线开关升级版
![pic](pic2.jpg)
