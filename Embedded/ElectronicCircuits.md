# 常见电路

## 1. NPN与PNP三极管电路
<p align="center">
<img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/NPN-PNP.png" height="200"> 
</p>

- **电流方向区别**
  - **NPN：** 用B-E的电流（IB）控制C—E的电流（IC），E极电位最低，且正常放大时通常C极电位最高，即：VC>VB>VE
  - **PNP：** 用E-B的电流（IB）控制E—C的电流（IC），E极电位最高，且正常放大时通常C极电位最低，即：VC<VB<VE 
- **电压区别**
  - **NPN：** 基极B高电压，集电极C与发射极E短路。基极B低电压，集电极C与发射极E开路，也就是不工作。
  - **PNP：** 基极B高电压，集电极C与发射极E开路，也就是不工作。基极B低电位，集电极C与发射极E短路。
- **用法**
  - **NPN：** 当基极B用高电平控制时，我们通常用NPN，（通常应用于E级接GND）
  - **PNP：** 当基极B用低电平控制时，我们通常用PNP，（通常应用于E级接VCC）