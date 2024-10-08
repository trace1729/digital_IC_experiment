# 实验3（重要）MOSFET的宽长比
“他尽力两手挝过道：“忒粗忒长些！再短细些方可用。”说毕，那宝贝就短了几尺，细了一围。悟空又颠一颠道：“再细些更好！”那宝贝真个又细了几分。悟空十分欢喜，拿出海藏看时，原来两头是两个金箍，中间乃一段乌铁；紧挨箍有镌成的一行字，唤做“如意金箍棒”，重一万三千五百斤。”

——《西游记》，吴承恩

MOSFET的宽长比（W/L），是我们数字集成电路设计师最关心的设计参数，改变W/L是电路设计师最常用的手段，可以说，一个电路的能否正确运行，一看电路拓扑结构，二看晶体管的W/L（晶体管的宽长比W/L也简称为晶体管的尺寸）。
## 3.1.再回首，MOSFET的结构
首先，让我们来重新复习一下MOSFET的结构图 1，对于NMOS来说，电流从D流到S。我们注意一下导电沟道，我们可以看到，实际上导电沟道是一个长方体（不考虑沟道长度调制效应等的理想情况），其长度就是图中的L，宽度就是图中的W。
我们不妨再回想一下中学时候的物理知识：**电阻的横截面积越大，电阻越小**。那么我们这里的导电沟道是不是也可以当作一个电阻呢？如果我们将W增加，就相当于增加了这个“电阻”的横截面积，那沟道的等效阻值就应该减小。

![](./图片/图片%201.png)

图 1 MOSFET物理结构示意图
问题时间：有些同学可能会问：“为什么我们不可以增加沟道的高度（厚度）？也相当于增加了横截面积。”
这是因为沟道的厚度是由制造工艺决定的，我们电路设计师是无法改变的，我们只能改变晶体管的宽度W和长度L。
由此可见，在沟道长度L不变的情况下，当我们增加晶体管的宽度W，相当于增加了晶体管的W/L，进而减小了沟道等效电阻。这表明在相同的驱动电压下，晶体管中的电流增加了，因此驱动负载的能力就提高了。
## 3.2.改变反相器的W/L
我们这里再次使用反相器作为实验对象，我们分别将晶体管的W/L设置为1，2，5（其中L设置为180nm），观察其驱动1pF电容负载的结果。如何更改MOSFET的宽度W和长度L呢？请读者自行STFW。
实验结果如下：

![](./图片/图片%202.png)

图 2 W/L=1时输出结果

![](./图片/图片%203.png)	

图 3 W/L=2时输出结果	

![](./图片/图片%204.png)

图 4 W/L=5时输出结果

可以看到，随着我们增加晶体管的W/L，输出结果逐渐从三角波变成了方波。其实从RC电路的角度也很好理解，其本质就是R减小，因此时间常数减小。
代价是什么呢？
虽然我们已经看到了增加W/L可以大幅改善驱动能力，可惜天下没有免费的午餐，增大W/L也带来的一些问题。

1. **芯片的成本与芯片的面积成4次方关系**，那么如果我们把每一个晶体管的尺寸（宽长比）都增大5倍，那么意味着芯片的成本会增加625倍！显然，你的老板不会接受这样的情况。

2. 从制造工艺的角度出发，W/L不可能无限制的增加。这是因为晶体管的宽度W存在一个最大值（由每个工厂的工艺决定），长度L存在最小值（一般就是这个工艺节点的特征尺寸，例如0.25um工艺的L最小就为0.25um）。
   
## 3.3.NMOS和PMOS完全对称吗
我们说CMOS工艺就是一对互补的晶体管，直观上我们会认为，NMOS和PMOS是完全对称的。理想很丰满，但是现实很骨感，从上面我们自己定义的晶体管模型中我们发现，PMOS的跨导Kp只有NMOS的跨导Kp的1/3，也就是说，PMOS的栅极电压对漏极电流的控制能力只有NMOS的1/3。因此，为了保证NMOS和PMOS尽可能的对称，我们通常会把PMOS的尺寸（W/L）设计的比NMOS大3倍，以此来弥补PMOS由于工艺原因导致的跨导较小。
## 3.4.动手实验内容
1 更改反相器PMOS和NMOS的W/L为不同值后，再次仿真反相器的电压传输特性曲线（VTC），使得输出的曲线尽可能对称。