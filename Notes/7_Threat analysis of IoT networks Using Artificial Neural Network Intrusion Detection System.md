# Threat analysis of IoT networks Using Artificial Neural Network Intrusion Detection System
# 基于人工神经网络入侵检测系统的物联网网络威胁分析

Elike Hodo, Xavier Bellekens, Andrew Hamilton, Pierre-Louis Dubouilh, 
Ephraim Iorkyase, Christos Tachtatzis and Robert Atkinson 
Department of Electronic & Electrical Engineering 
University of Strathclyde 
Glasgow, G1 1XW, UK 
E-mail :{ name.surname}@strath.ac.uk

## 摘要 
物联网（IoT）仍处于起步阶段，在医疗、物流跟踪、智能城市、汽车等多个产业领域引起了广泛关注。 然而作为范例，它容易受到一系列重大入侵威胁的影响。 本文提出了对物联网的威胁分析，并使用人工神经网络（ANN）来对抗这些威胁。 多级感知器是一种有监督的人工神经网络，使用互联网数据包跟踪进行训练，然后评估其阻止分布式拒绝服务（DDoS / DoS）攻击的能力。 本文重点介绍物联网中正常和威胁模式的分类。 ANN程序根据模拟的物联网网络进行验证。 实验结果表面该方法具有99.4％的准确率，并且可以成功检测到各种DDoS / DoS攻击。

## 关键词：
物联网，人工神经网络，拒绝服务，入侵检测系统和多级感知器

## 一、引言：

物联网（IoT）是一个分布式（传感器）节点，（云）服务器和软件的网络。这一范式允许在实时创建网络物理系统之间的直接交互平台时，能够感知和处理测量对象。这种方法可以提高数据生成和使用的效率，从而带来经济利益[1]。
 
思科公司的研究报告称，目前有100亿台设备联网，而世界人口超过70亿，预计到2020年将增加4%[2]。

对物联网范式的威胁正在上升;但是记录数据中的模式可以被分析以帮助预测威胁[3]。入侵者类型分为两类：1）外部入侵者 - 这些人属于网络外部，因此没有网络权限。它们通过发送恶意软件或通过利用漏洞访问系统来操作[4]。 2）内部入侵者 - 这些人拥有访问网络的权利和特权，但恶意滥用他们。这些类型的攻击包括更改重要数据内容或盗用机密数据。所有这些威胁都可以通过黑客进入计算机系统或通过远程访问网络来进行物理访问[4]。
 
IoT威胁可以分为四种类型[5]：1）拒绝服务（DoS） - 这种威胁通过引入无用或不需要的流量来拒绝或阻止用户的网络资源。2）恶意软件 - 攻击者使用可执行代码破坏物联网网络。他们可能收集敏感信息，或未经授权访问设备。攻击者可以利用设备上运行的固件中的缺陷并运行他们的软件来破坏物联网架构。 3）数据泄露 - 这是一种安全事件，从网络中检索敏感，受保护或机密数据。攻击者可以欺骗ARP数据包来监听网络上对等体之间的通信。 4）弱化周界 - 物联网网络设备目前没有考虑到普遍的安全性。网络安全机制并不经常出现在使网络成为威胁的脆弱网络中[5] [6]。
 
入侵检测系统(IDS)是一种用于监控网络和计算机系统的安全检测系统。自上世纪80年代以来，它就一直存在[7]。在KDD99数据集[8], [9],[10],[11]上使用人工神经网络入侵检测系统的前期工作和最近的研究表明，入侵检测具有良好的性能。

在本文中，ANN被用作离线IDS来收集和分析来自物联网网络各个部分的信息，并确定网络上的DoS攻击。
 
本文的其余部分安排如下：第二部分回顾了入侵检测系统。第三节介绍了人工神经网络算法的学习过程。第四节给出了网络架构的描述。最后第五节介绍结果分析，未来工作和结论在第六节中介绍。

## 二、入侵检测
一个IDS被战略性地放置在一个网络上，以检测威胁和监视数据包。IDS的功能包括提供有关威胁的信息，在检测到威胁时采取纠正步骤，并记录网络中所有事件的记录[12].
### A.	入侵检测分类
表I. HIDS和NIDS性能比较[13]

入侵检测系统可以分为两类[3]：
•基于主机的入侵检测系统（HIDS） - 这是基于软件的产品，安装在主机上，用于分析和监控系统应用文件和操作系统上的所有流量活动。 
•基于网络的IDS（NIDS） - 可在整个网络上找到这些IDS以通过网络捕获和分析数据包流。表I中显示了基于主机的ID和基于网络的IDS的性能比较。

### B.	入侵模式
入侵检测系统的设计可以有效检测和识别威胁。入侵归结为两种检测模式[14]：
•误用入侵 - 它与入侵者网络流量中的模式相匹配。误用检测系统的一个优点是能够检测所有已知的威胁[14]。 
•异常入侵 - 这是基于行为的入侵检测系统。它通过构建正在监测的系统概况来观察系统中正常模式的变化[14]，[4]。

### C.	入侵检测技术
基于入侵检测模式的入侵检测技术有多种类型。下面是对本文提出的包括ANN在内常用的描述。

•统计分析 - 这涉及将数据的当前趋势与预先确定的基线标准进行比较。它将数据的正常行为与随时间的偏差进行比较。该技术应用于异常检测系统[4], [15]。

•演化算法 - 这种技术创建了一个应用程序路径，它提供了正常的行为模型。这些应用程序被建模为通过根据不同条件对模型进行分类来检测正常行为，错误条件和企图入侵的条件[15]。
 
•协议验证 - 这是基于对协议字段及其行为进行全面检查的技术，与已建立的标准相比较。被认为违反了既定标准的数据被分类为可疑。这项技术在商业上取得了成功，系统，但缺点是对未指定的协议给予误报[15]。
 
•基于规则 - 状态转换分析技术将数据与签名进行比较。每个数据包在转换之后被应用到一个有限状态机，直到达到最终状态，从而检测到攻击[16]。
 
•人工神经网络 - 人工神经网络的神经元用于形成复杂的假设;越多的神经元，假设越复杂。评估假设是通过在反馈过程中设置输入节点完成的，并且事件流通过网络传播到输出，在那里它被归类为正常或被破坏。在此阶段，使用梯度下降以便通过反向传播过程将输出节点中的误差推回到网络中以便估计隐藏节点中的误差。因此可以计算成本函数的梯度[17] - [19]。神经网络系统通过训练来学习系统中创建的模式。

## 三、人工神经网络学习过程
人工神经网络有两个学习过程。
•监督学习过程:在监督学习过程中，神经网络提供了标记训练集，学习了从输入x到输出y的映射，给定了一组标记的输入输出对。其中，d为训练集，N为训练样本数，假设yi为某无限集的分类变量。
多层感知器(MLP)是一种使用监督学习过程训练的神经网络。MLP在[21]中用于检测基于离线分析方法的入侵。在另一种方法中，MLP在[22]中用于检测网络数据的入侵，并将其性能与自组织映射(SOM)进行比较。
•无监督的神经网络学习过程:在这个学习过程中，神经网络有一个输入d，这是一组无标记的数据，你要在数据中找到模式。SOM是一种使用无监督学习过程训练的神经网络，用来生成低维的、离散化的训练样本输入空间的表示。
 
在这项工作中，使用了如图1所示的具有三层前馈神经网络的MLP架构。该网络在每个隐藏层和输出层的神经元中都具有单极sigmoid传递函数。使用具有均方误差函数的随机学习算法。在图1中使用了标记为x1 …x 6的节点来表示神经网络的输入单位，其中标记为“+1”的圆被称为偏差单位。 ANN模型有六个输入单元（layer1），三个隐藏单元（layer2）和一个输出单元（layer13），其中l表示层。该网络采用前馈学习算法和后向学习算法进行训练。
 
图1三层人工神经网络
 
### A.	前馈学习算法
 
设sl表示不包括偏差单位的单位数。因此，我们做网络参数：（w,b）=(w1,b1,w2,b2),其中w ij表示与层l中单元j和层l+1中单元i之间的连接有关的参数。bli是与单元i在第1+ l层有关的偏差，因此从上面的模型中可以看出
 
令ai1表示单元在第1层的输出，对于i= 1，我们令aii = x1（表示第i个输入，ANNs模型将定义一个假设。
### B.	后向学习算法
这个学习过程经历了四个步骤，如下所示。 
•前馈学习算法计算网络中所有层的激活。 
•将l3中的out设置为计算输出中的误差项：
 

 
训练人工神经网络涉及采取梯度下降的重复步骤来降低成本函数J(w,b)。
## 四、实验情景
 
图2实验体系结构
 
物联网网络由5个节点传感器组成。其中四个节点充当客户端，一个充当服务器中继节点以用于数据分析目的。通过网络窃听来捕获流量，避免修改实时流量。服务器节点确认传感器节点发送的数据，并基于接收到的数据回复数据。这允许传感器节点调整其行为并对发生的事件做出反应，如图2（左）所示。
  
在本研究的背景下，攻击来自外部入侵者。攻击如图2(右)所示。攻击者只针对服务器节点，因为它是对传感器节点进行分析、记录和响应的。DoS攻击是使用单个主机执行的，发送超过1000万个包。当DDoS攻击时，多达3个主机发送超过1000万个数据包，每一个发送速度超过服务器节点。在DoS/DDoS攻击期间发送的包是由C中的自定义脚本编写的UDP包。

当服务器节点变得不响应时，传感器节点无法调整其行为，最终导致监控系统出现故障。

因此，对攻击的检测至关重要，可以让响应团队避免中断传感器网络并保证网络的稳定性。


## 五、结果与讨论
本节提供了对第四部分描述的人工神经网络入侵检测性能的评估。 网络接受了2313个样本的训练，经过496个样本和496个测试样本的验证。 表2显示了用于分类的样本数量。 表2  用于分类的样本数量
 
 
图3神经网络训练混淆矩阵。
 
图3显示了训练集、测试集、验证集和右下角的所有混淆矩阵（总体性能）的神经网络混淆矩阵图。 网络输出正确的响应值分为两类：真正（TP）和假正（FP）。 TP输出提供了正确分类的攻击措施，如绿色框中所示。 FP是正确分类的正常事件的度量，如红色框中所示。 神经网络模型在分类中显示99.4％的总体准确度。该模型表明，实现的ANN算法能够成功地检测到DDoS/DoS攻击对合法的IoT网络流量的攻击。此外，它还可以通过在攻击的早期警告响应团队，避免主要的网络中断，从而帮助提高网络的稳定性。

## 六、结论和未来工作
在本文中，我们提出了一种基于神经网络的物联网入侵检测方法来识别DDoS / DOS攻击。 该检测基于对正常和威胁模式进行分类。 人工神经网络模型验证了模拟物联网网络的准确性超过99％。 它能够成功地识别不同类型的攻击，并在真实和假阳性率方面表现出良好的表现。 对于未来的发展，应引入更多的攻击来测试我们的方法抵御攻击的可靠性并提高框架的准确性。 此外，我们将研究其他更深层次的神经网络，例如递归和卷积神经网络方法。

## REFERENCES
[1] “Internet of Things (IoT).” [Online]. Available:http://www.cisco.com/c/en/us/solutions/internet-ofthings/overview.html. [Accessed: 12-Jan-2016].
[2] D. Evans, “The Internet of Things - How the Next Evolution of the Internet is Changing Everything,” CISCO white Pap. ,no. April, pp. 1–11, 2011.
[3] SANS institute, “InfoSec Reading Room tu , Application of Neural Networks to Intrusion Detection,” 2001.<rt>
[4] J. Shun and H. a. Malki, “Network Intrusion Detection System Using Neural Networks,” 2008 Fourth Int. Conf. Nat. Comput., vol. 5, pp. 242–246, 2008.
[5] “Internet of Things: How Much are We Exposed to Cyber Threats? - InfoSec Resources.” [Online]. Available: http://resources.infosecinstitute.com/internet-things-muchexposed-cyber-threats/. [Accessed: 10-Dec-2015]. 
[6] X. Bellekens, A. Seeam, K. Nieradzinska, C. Tachtatzis, A. Cleary, R. Atkinson, and I. Andonovic, “Cyber-Physical- Security Model for Safety-Critical IoT Infrastructures.” Wireless World Research Forum Meeting 35 (WWRF35), Copenhagen, Danemark, 2015.
[7] S. Institute, “SANS InstituteInfoSec Reading Room tuevolution , The history and Evolution of Intrusion Detection,” 2001.
[8] N. T. T. Van and T. N. Thinh, “Accelerating Anomaly- Based IDS Using Neural Network on GPU,” in 2015 International Conference on Advanced Computing and Applications (ACOMP), 2015, pp. 67–74.
[9] C. Han, Y. Lv, D. Yang, and Y. Hao, “An intrusion detection system based on neural network,” in 2011 International Conference on Mechatronic Science, Electric Engineering and Computer (MEC), 2011, pp. 2018–2021.
[10] Z. Li, W. Sun, and L. Wang, “A neural network based distributed intrusion detection system on cloud platform,” in 2012 IEEE 2nd International Conference on Cloud Computing and Intelligence Systems, 2012, vol. 01, pp. 75– 79.
[11] V. Jaiganesh, P. Sumathi, and S. Mangayarkarasi, “An analysis of intrusion detection system using back propagation neural network,” in 2013 International Conference on Information Communication and Embedded Systems (ICICES), 2013, pp. 232–236.
[12] “What it is Network intrusion detection system? | COMBOFIX.” [Online]. Available: http://www.combofix.org/what-it-is-network-intrusiondetection- system.php. [Accessed: 10-Dec-2015].
[13] H. Kozushko, “Intrusion detection: Host-based and network based intrusion detection systems,” Sept., vol. 11, 2003.
[14] J. Mena, Investigative data mining for security and criminal detection. Amsterdam ; Boston, MA : Butterworth- Heinemann, 2003.
[15] T. Verwoerd and R. Hunt, Intrusion detection techniques and approaches, vol. 25, no. 15. 2002.
[16] X. J. A. Bellekens, C. Tachtatzis, R. C. Atkinson, C. Renfrew, and T. Kirkham, “A Highly-Efficient Memory- Compression Scheme for GPU-Accelerated Intrusion Detection Systems,” Proc. 7th Int. Conf. Secur. Inf. Networks - SIN ’14, pp. 302–309, 2014.
[17] M. A. Alsheikh, S. Lin, D. Niyato, and H.-P. Tan, “Machine Learning in Wireless Sensor Networks: Algorithms, Strategies, and Applications,” IEEE Commun. Surv. Tutorials, vol. 16, no. 4, pp. 1996–2018, 2014.
[18] K. A. Jalill, M. H. Kamarudin, and U. T. Mara, “Comparison of Machine Learning Algorithms Performance in Detecting Network Intrusion,” pp. 221–226, 2010.
[19] F. Gharibian and A. A. Ghorbani, “Comparative Study of Supervised Machine Learning Techniques for Intrusion Detection,” in Fifth Annual Conference on Communication Networks and Services Research (CNSR ’07), 2007, pp. 350–358.
[20] K. Murphy, “Machine learning: a probabilistic perspective,” Chance encounters: Probability in …, 2012. [Online]. Available: http://link.springer.com/chapter/10.1007/978-94- 011-3532-0_2. [Accessed: 06-Jan-2015].
[21] M. Moradi and M. Zulkernine, “A neural network based system for intrusion detection and classification of attacks,” Proc. 2004 IEEE Int. Conf. Adv. Intell. Syst. Appl., 2004.
[22] a Bivens and C. Palagiri, “Network-based intrusion detection using neural networks,” … Neural Networks, vol. 12, pp. 579–584, 2002.
