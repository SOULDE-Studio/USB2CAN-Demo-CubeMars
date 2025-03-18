

# 简介
   本程序使用C++在Linux环境编写、运行，通过两个USB2CAN模块使Linux系统电脑拓展4路CAN总线，每条总线挂载3个CubeMars电机，程序可以以1000hz的频率控制共计12个CubeMars电机，适用于一般四足机器人控制底层。


# 前期准备
本程序需要与肥猫机器人公司USB2CAN模块配合使用，请准备好模块与模块说明书、模块SDK，`并按照说明书使用install.sh文件安装USB2CAN规则文件，或手动安装规则文件，安装方法：`
1. 进入项目目录下的can文件夹
```bash
cd USB2CAN-Demo-CubeMars/can
```
2. 复制规则文件usb_can.rules 到/etc/udev/rules.d/
```bash
sudo cp usb_can.rules /etc/udev/rules.d/
```
3. 运行下面的命令，使udev规则生效
```bash
sudo udevadm trigger
```

>CubeMars电机初始模式为伺服控制模式，本程序使用于运控模式，请提前使用CubeMars官方模块和上位机将电机模式切换为运控模式，模式切换之后，掉电之后，模式仍会保持运控模式，无需重复设置。


```USB转2路CAN模块购买地址：```
https://e.tb.cn/h.TBC18sl6EZKXUjL?tk=C5g5eLgyMf6HU071

```说明书以及SDK下载地址：```
https://pan.baidu.com/s/1EwYDNQ0jMKyTSvJEEcj6aw?pwd=10ob

```CubeMars电机购买地址：```
https://e.tb.cn/h.6ZLLkZPDLJqn9KD?tk=pA1jeJ5EowGtG-#22



# 安装
1. 克隆仓库到本地 :
```bash
git clone https://github.com/SOULDE-Studio/USB2CAN-Demo-CubeMars.git
```
2. 进入项目目录 :
```bash
cd USB2CAN-Demo-CubeMars
```
3. 编译项目 :
```bash
mkdir build
cd build
cmake ..
make
```
4. 运行项目 :
```bash
./can_code
```


# 注意事项
1. 本程序使用的两个USB2CAN模块其设备名称分别为USB2CAN0、USB2CAN1
2. 若还需要拓展多个USB2CAN模块，可在本程序基础上进行修改，一个电脑最多拓展4个模块即8路CAN总线。
3. 在同一模块的同一条CAN总线发送的控制命令间隔不应小于300us，可以交错发送不同CAN总线上的控制命令
4. 程序封装了电机数据结构体，只需要对结构体对象赋值再调用发送函数，即可控制电机，赋值数值范围请参考CubeMars电机说明书
5. 本程序使用CubeMars AK80-9KV100电机，如使用其他型号电机请修改头文件`include/Tangair_usb2can.h`参数。
6. 本程序主要控制函数为`CAN_TX_test_thread`
7. 经测试，对于单个电机，控制命令发送绝对时间间隔为248微秒时，有效带宽（即发送一帧控制命令，可收到一帧回复）达到最大3893.36赫兹，丢包率为3.1%

# 拓展
> 若想要以本项目开发四足机器人，可配合强化学习训练代码、强化学习部署代码使用，相关开源库地址如下：
> 
> ```isaaclab训练代码地址： ```https://github.com/fan-ziqi/robot_lab
> 
>  ```仿真、实物部署代码地址： ```https://github.com/fan-ziqi/rl_sar
> 
>  ```相关机器人展示视频链接：``` https://www.bilibili.com/video/BV17oPEeHEfM/?share_source=copy_web&vd_source=97170e52311d304767c925aed213e556


# 引用说明

Please cite the following if you use this code or parts of it:

```
@software{tangair2025USB2CAN-Demo-CubeMars,
  author = {tangair},
  title = {{USB2CAN-Demo-CubeMars: An  project based on USB2CAN and CubeMars motor.}},
  url = {https://github.com/SOULDE-Studio/USB2CAN-Demo-CubeMars.git},
  year = {2025}
}
```


