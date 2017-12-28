#include <Servo.h>
int motorL1=6; //左边轮子
int motorL2=5;
int motorR1=9; //右边轮子
int motorR2=11;
Servo s; //超声波转向舵机
int trig=4; //发射信号
int echo=2; //接收信号
unsigned int S; //距离存储
void setup() {
Serial.begin(9600); //设置波特率
pinMode(trig,OUTPUT); //设置引脚模式
pinMode(echo,INPUT);
pinMode(motorL1,OUTPUT);
pinMode(motorL2,OUTPUT);
pinMode(motorR1,OUTPUT);
pinMode(motorR2,OUTPUT);
pinMode(12,OUTPUT);
s.attach(3); //定义舵机所用引脚
s.write(90); //初始化舵机角度
delay(1000); //开机延时
}
void loop() { //主函数
s.write(90); //舵机中位
range(); //执行测距函数
if(S<10){ //判断障碍物距离，距离太近
back(); //后退
}
if(S<=20&&S>10){ //距离中等
turn(); //运行转向判断函数
}
if(S>20){ //距离充足
line(); //运行直行函数
}
}
void turn(){ //判断转向函数
lull(); //停止所用电机
s.write(170); //舵机转到170度既左边（角度与安装方式有关）
delay(500); //留时间给舵机转向
range(); //运行测距函数
s.write(90); //测距完成，舵机回到中位
delay(600); //留时间给舵机转向
if (S>10) {L();} //判断左边障碍物距离，如果距离充足,运行左转
else {
s.write(10); //否则，舵机转动到10度，测右边距离
delay(600);
range(); //测距
s.write(90); //中位
delay(600);}
if(S>10){ R();
} //右转
else{ back();} //判断右边距离，距离充足右转否则后退
//判断随机数
} //否则后退，并随机转向void range(){ //测距函数
digitalWrite(trig,LOW); //测距
delayMicroseconds(2); //延时2微秒
digitalWrite(trig,HIGH);
delayMicroseconds(20);
digitalWrite(trig,LOW);
int distance = pulseIn(echo,HIGH); //读取高电平时间
distance = (distance/58); //按照公式计算
S = distance; //把值赋给S
Serial.println(S); //向串口发送S的值，可以在显示器上显示距离
}
void line(){
digitalWrite(motorR1,HIGH); //启动所有电机向前
digitalWrite(motorL1,HIGH);
digitalWrite(motorR2,LOW);
digitalWrite(motorL2,LOW);
}void L(){
digitalWrite(motorL1,LOW);
digitalWrite(motorR2,LOW);
analogWrite(motorL2,100);
analogWrite(motorR1,100);
delay(200);
lull(); //暂停所有电机
}
void R(){
digitalWrite(motorL2,LOW);
digitalWrite(motorR1,LOW);
analogWrite(motorL1,100);
analogWrite(motorR2,100);
delay(200);
lull();
}
void back()//后退
{
digitalWrite(motorL1,LOW);
digitalWrite(motorR1,LOW);
analogWrite(motorL2,100);
analogWrite(motorR2,100);
delay(200);
}void lull(){
digitalWrite(motorL1,LOW);
digitalWrite(motorL2,LOW);
digitalWrite(motorR1,LOW);
digitalWrite(motorR2,LOW);
}
