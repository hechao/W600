# 常见问题

## 基础概念篇

### W600是什么？

　　W600是联盛德新一代支持多接口、多协议的无线局域网802.11n（1T1R）低功耗WLAN SoC 芯片。芯片内置 Cortex-M3 CPU处理器和Flash，集成射频收发前端RFTransceiver，CMOSPA功率放大器，基带处理器/媒体访问控制，集成电源管理电路，支持丰富的外围接口，支持多种加解密协议。W600提供给客户的二次开发空间更大、芯片外围电路器件更少、开发更简便，性价比更优势。

### W601和W600有什么区别？

W601和W600同属于联盛德W600系列WiFi芯片，主要区别如下：

| 属性   | W600      | W601      |
| ------ | --------- | --------- |
| 封装   | QFN32 5*5 | QFN68 7*7 |
| 可用IO | 17        | 48        |
| ADC    | 无        | 8个       |
| LCD    | 无        | 1个       |
| I2S    | 无MCLK    | 完整      |

### 联盛德与星通智联是什么关系？

　　联盛德是W600的芯片设计和生产厂商，星通智联是联盛德的芯片代理商和方案供应商。

### TW-01, TW-02是什么？

　　TW01\~TW-03是由深圳市星通智联科技有限公司研发生产的 W600系列模组，在W600芯片的基础上，完善了外围器件布局和天线优化，并在设计时考虑兼容市面上已有模组，方便大家替换测试。

### T-Cloud是什么？

　　T-Cloud 是星通智联提供的全球智能云服务，配合TW系列模组，有诸多成熟的PCBA 方案。

### W600 必须要借助远程服务器才能开发吗？

　　这个根据您的需求来定，若您只需要局域网就可以满足产品需求，那么无需服务器，同样可以使用W600 进行开发。

### 如何基于 T-Cloud 开发产品？

　　T-Cloud 暂时不开放，如您需要使用，可通过[support@thingsturn.com](mailto:support@thingsturn.com)联系我司，后期我们会开放透传固件，可外接MCU实现任意定制功能。

### 如何购买W600模组和测试板？

　　星通智联官方淘宝店铺：http://shop.thingsturn.com，强烈建议新手购买TB-01 开发板。

### 我该选择哪个型号的W600模组？

　　模组硬件之间的差异主要是封装区别，您可以根据需求自行选择，若有疑问，可联系我们。

### 我该选择AT开发还是SDK开发？

SDK方法：

*   优势：让系统成本最少,体积最小
*   劣势：新手需要一个礼拜到半个月的时间去熟悉代码的研读

AT方法：

*   优势：只需要知道几条AT指令即可用外部单片机实现网络通讯！开发速度快。
*   劣势：增加了外置CPU成本

您可以依此评估自己适合哪种方案。

### 开发中，遇到问题如何寻求帮助？

-   若您是企业用户，我们会专门委派一名工程师负责贵司的对接；
-   若您是个人用户，您可以在论坛发帖，或发邮件到
    <support@thingsturn.com>，我们也会有专门的工程师去处理。

## 硬件连接篇

### W600 最小系统如何搭建

　　W600外围极其简单，可参考我们给出的模组原理图。

### W600 有几个 UART？

　　W600 有 2 个 完整的 UART，速率最高为 2Mbps。AT 固件默认使用串口 0进行指令控制，串口 1 作日志打印。

### GPIO 可以直接连 5V 吗？

　　不可以！！！GPIO 最高只能承受3.6V。必须需要通过电平转换电路，否则会造成 GPIO 永久性损坏。

### W600 电压电流需求？

　　W600 的数字部分的电压范围是 1.8V \~ 3.3V, 模拟部分的工作电压是 3.0V\~ 3.6V，最低 3.0V。模拟电源峰值 350 mA，数字电源峰值 200 mA。

### 设计 W600 的供电时，需要注意哪些问题？

请注意如下几点：

1.  如果是使用 LDO 变压，请确保输入电压和输出电压要足够大。
2.  电源端去耦电容器必须接近 W600 摆放，等效电阻要足够低。
3.  W600 不能直连 5V 电压。
4.  如果是通过 DC-DC 给 W600 供电，必要时要加上 LC 滤波电路。

### W600 上电时电流很大，是什么原因？

　　W600 的 RF 和数字电路具有极高的集成度。上电后，RF自校准会需要大电流。模拟部分电路最大的极限电路可能达到 500mA；数字电路部分最大电流 达到 200 mA。一般的操作，平均电流在 100 mA左右。因此，W600 需要供电能达到 500 mA，才能保证不会有瞬间压降。

### 可以使用锂电池或者 2 节 AA 纽扣电池直接给 W600 供电吗？

　　理论上，2 节 AA 纽扣电池可以给 W600供电。但锂电池放电时压降比较大，不适合直接给 W600 供电。W600 的 RF电路会受温度及电压浮动影响。不推荐不加任何校准的电源直接给 W600供电。推荐使用 DC-DC 或者 LDO 给 W600 供电。

### W600 的 RAM 是怎么划分的？

整个RAM空间为 288 KB，当前的RAM空间划分:

|     分类      |  起始地址  | 大小（K Byte） |
| :-----------: | :--------: | :------------: |
|   可用空间    | 0x20000000 |      240       |
| Wi-Fi使用空间 | 0x2003C000 |       48       |

### W600 的 Flash 是如何分配的？

内置 Flash 总容量为 1M Bytes，具体分配方式如下

|     分类      | 起始地址  | 大小（K Byte） |
| :-----------: | :-------: | :------------: |
|   系统参数    | 0x8000000 |       8        |
| 二级BOOT区域  | 0x8002000 |       32       |
|   IMAGE1头    | 0x800A000 |       4        |
|   IMAGE2头    | 0x800B000 |       4        |
|   参数1区域   | 0x800C000 |       4        |
|   参数2区域   | 0x800D000 |       4        |
| IMAGE运行区域 | 0x800E000 |      450       |
| IMAGE升级区域 | 0x807E800 |      450       |
|   用户区域    | 0x80EF000 |       64       |

