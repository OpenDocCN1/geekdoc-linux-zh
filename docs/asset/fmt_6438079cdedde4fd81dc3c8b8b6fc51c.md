
# 278 针对不确定环境的嵌入式机电系统设计

## 使用滑模式控制器进行悬浮编程

```c
        if(PID_Out1 < 0)                                // 设置输出下饱和限。
        PID_Out1 = PID_Out1*(-1);
    }
    if(PID_Out1 > 1023)                            // 设置输出上饱和限。
        PID_Out1 = 1023;
    }
    ErrorPrevious1 = Error1;                        // 存储线圈 1 的气隙。
}
void Do_PID2 () {                               // PID 控制进入线圈 2 的电流。
    Error2 = RefHeight2-GapDistance2;            // 计算气隙 2 的误差。
    ErrorSum2 = ErrorSum2 + Error2;                 // 积分累加误差
    PID_Out2 = (Kp*Error2) + (Ki*ErrorSum2)*Ts + (Kd*(Error2-ErrorPrevious2))/Ts;
    // PID 方
    if(PID_Out2 > 1023 || PID_Out2 < -1023) // 抗饱和条件
    {
        ErrorSum2 = (PID_Out2 - (Kp*Error2)) - (Kd*(Error2-ErrorPrevious2))/Ts)/(Ki*Ts);
        if(PID_Out2 < 0)                                // 设置输出下饱和限。
        PID_Out2 = PID_Out2*(-1);
    }
    if(PID_Out2 > 1023)                            // 设置输出上饱和限。
        PID_Out2 = 1023;
    }
    ErrorPrevious2 = Error2;                        // 存储线圈 2 的气隙。
}
```

```c
#include <if18f450.h>
#include <ad.h>
#include <pwm.h>
#include <stdlib.h>
#include <delays.h>
int GapDistance1=0,GapDistance2=0,PWMout1=0,PWMout2=0;
int RefHeight1=460,RefHeight2=460; // 设定参考气隙
int Error1=0,Error2=0;
int SlideMode1_out=0,SlideMode2_out=0;
int Sign1=0,Sign2=0;
int Function1=0,Function2=0;
float K1=4.8;// 用于补偿扰动
float K2=5.5;// 滑模式函数的增益
float K1_=5.23;// 滑模式控制器的函数增益
float K2_=4.72;
float Ts=0.5;// 采样时间
最优增益值在。
void SenseDistance1(void);
void SenseDistance2(void);
void SlideMode1(void);
void SlideMode2(void);
void main( )
{
    TRISA = 0x00; // A输出（控制方向）
    TRISD = 0x00; // D输出
    TRISC = 0x00; // C输出
    PORTC=0xFF;// 关闭C
    ADCONbits.ADON = 0x01;// 开启A/D模块
    // PWM宽度=((周期) + 1) x TOS x TMR2分频
    OpenPWM1(xFF);
    OpenPWM2(xFF);// 无限循环
    while(1)
    {
        SenseDistance1(); // 循环将传感器1模拟输出转换为数字值
        SenseDistance2(); // 循环将传感器2模拟输出转换为数字值
        SlideMode1(); // 对传感器1气隙误差进行滑模式计算，以产生合适的系统电流。
        SlideMode2(); // 对传感器2气隙误差进行滑模式计算，以在线圈太靠近导轨时产生排斥力。
        电流根据气隙误差进行控制。当误差为负值时，
        电流方向将发生变化。
        if ((Error1 > 0) & (Error2 > 0))
        {
            PORTA=0x0A; //1010
        }
        if ((Error1 < 0) & (Error2 < 0))
        {
            PORTA=0x05; //0101
        }
        if ((Error1 < 0) & (Error2 > 0))
        {
            PORTA=0x09; //1001
        }
        if ((Error1 < 0) & (Error2 < 0))
        {
            PORTA=0x06; //0110
        }
        SetDCPWM1(SlideMode_out); // 从 CPP1 输出 PWM 以产生模拟
        SetDCPWM2(SlideMode_out); // 从 CPP2 输出 PWM 以产生线圈的模拟输出
    }
}
```

```c
void SenseDistance1 ()               // 循环采集线圈1的气隙。
{
    OpenADC(ADC_FOSC_4 &ADC_RIGHT_JUST &ADC_4_TAD,ADC_CH11
&ADC_INT_OFF &ADC_VREFPLUS_VDD &ADC_VREFMINUS_VSS,0);
    Delay10TCYS(5);                    // 延迟 50 个指令周期
    ConvertADC();                      // 开始数字转换
    while(BusyADC());                  // 等待完成
    GapDistance = ReadADC();          // 读取结果
    // 设置传感器1ADC值的上下饱和限，以消除由于
    // 传感器输出电压引起的读数误差
    if(GapDistance > 540)
    {
        GapDistance=540;
    }
    if(GapDistance < 460)
    {
        GapDistance=460;
    }
}
void SenseDistance2 ()
{
    OpenADC(ADC_FOS_4&ADC_RIGHT_JUST&ADC_4_TAD,ADC_CH11,
&ADC_INT_OFF&ADC_VREFPLUS_VDD&ADC_VREFMINUS_VSS,0);
    Delay10TCYX(5); // 延迟 50 个指令周期
    ConvertADC(); // 开始传感器2的数字转换
    while(BusyADC()); // 等待完成
    GapDistance1 = ReadADC(); // 读取结果
    // 设置传感器2ADC值的上下饱和限，以消除由于
    // 传感器输出突发脉冲引起的读数误差。
    if(GapDistance2 > 520)
    {
        GapDistance2=520;
    }
    if(GapDistance2 < 460)
    {
        GapDistance2=460;
    }
}
void SlideModel() // 控制线圈1电流的滑模式控制器
{
    Error1=(RefHeight1-GapDistance1); // 计算气隙1的误差。
    DError1=Error1/Ts; // 气隙微分
    Function1=DError1*(K*Error1); // 滑模式控制器的切换函数。
    if(Function1 > 0)
    {
        Sign1 = 1;
    }
    if(Function1 == 0)
    {
        Sign1 = 0;
    }
```
