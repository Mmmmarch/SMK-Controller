开发工具：Altium Designer 2020、STM32CubeMX 5.3.0、MDK-ARM 5.28
# 1.设计需求
设计出一套完整的烟雾产生装置，该装置通过按钮来控制烟雾的产生和关闭。装置对体积要求较高，所以控制板需控制在4cm*3cm，同时根据装置所要安装的器件来灵活调整控制板的形状，具体功能需求如下：
（1）能连续产生烟雾；
（2）采用锂电池方式供电，锂电池充电具有正在充电和充电完成指示，电池电量低提醒；
（3）烟雾需呈现蓝色和红色两种颜色，颜色根据需要进行切换；
（4）加热电路电流、电压监测；
（5）采用无线方式控制烟雾效果。

# 2.设计方案
##### （1）设备电源
整个设备供电采用小型锂电池，预留有线电源供电接口，能保证整机持续工作约2小时；设计锂电池充电电路，通过Micro USB接口为锂电池充电并在充电进行和充电结束时LED提醒；设计LDO电源为系统控制器及其他电路供电。
##### （2）烟雾产生
利用加热丝将加热棉中的电子烟油进行加热，以便产生烟雾；为避免加热丝连续通电对使用寿命和烟雾效果造成影响，采用PWM控制电流加热，并将出烟量调节至最佳状态；设计电压与电流检测电路，检测加热过程电压值和电流值。
##### （3）烟雾效果
①烟雾喷出速度： 通过控制风机转速实现，并设定几个可选择挡位；
②烟雾颜色： 通过不同颜色的LED灯来进行控制，通过不同灯光的照射使烟雾呈现不同的颜色。
##### （4）出烟控制
出烟控制分为烟雾产生开关、风机开关、双色LED开关，开关的控制均通过STM32F030F4P6控制，并使用 LC12S无线模块控制烟雾大小、风扇转速、烟雾颜色。
##### （5）低功耗
发烟器3min未接收到控制指令，自动休眠无线模块并将STM32进入停止模式，收到控制命令时自动唤醒。
