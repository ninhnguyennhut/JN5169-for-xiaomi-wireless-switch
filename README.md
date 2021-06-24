Pin connect

+ RESET -> VCC
+ ISP   -> GND




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
