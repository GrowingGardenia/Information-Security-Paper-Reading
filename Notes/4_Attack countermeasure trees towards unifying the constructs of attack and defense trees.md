# ACT : Towards unifying the constructs of attack and defense trees
# 攻击对策树的构造
Arpan Roy, Dong Seong Kim and Kishor S. Trivedi,
Department of Electrical & Computer Engineering, Duke University, Durham, NC 27708, USA.

## 摘要
攻击树（AT）是安全分析中广泛使用的非状态空间模型之一。 AT的基本形式没有考虑防御机制。已经开发了防御树（DT）来使用诸如攻击成本，安全投资成本，攻击回报率（ROA）和投资回报率（ROI）等措施来调查防御机制的效果。但是，DT仅将防御机制置于叶节点处，并且相应的ROI / ROA分析不包含攻击的概率。在攻击响应树（ART）中，攻击和响应都被捕获，但ART受到状态空间爆炸问题的困扰，因为ART的解决方案是通过状态空间模型获得的。在本文中，我们提出了一种新的攻击树模式，称为攻击对抗树（ACT），它避免了状态空间模型的生成和解决，并考虑到攻击以及对策（以检测和缓解事件的形式）。在ACT中，检测和缓解不仅允许在叶节点而且也允许在中间节点处，同时在其分析中避免状态空间爆炸问题。我们使用三个案例研究（ACT针对BGP攻击，ACT针对SCADA攻击以及ACT针对恶意内部攻击）研究了将对策纳入ACT的结果。
版权2011 John Wiley＆Sons，Ltd.

##  关键词: 
攻击树，非状态空间模型，缩小曲线，攻击返回，投资回报。

## 1.介绍:
迈向安全建模的第一步涉及到设计一个可扩展的模型[1,2]，以帮助量化安全性[3]的关键属性，如攻击造成的损失[4,5]或者执行安全对策所产生的收益[ 6]。这不仅有助于系统的概率风险分析（PRA），而且还有助于决定计划的哪些安全投资部分应该优先。在这种情况下最简单的模型类型是攻击树（AT）[7,2]。但是，AT的基本形式不包括防御机制。防御树（DT）[8,9]在AT中包含防御机制。但是，它只在叶节点放置防御机制。使用DT的投资回报率（ROI）和攻击回报率（ROA）分析不包含攻击概率。在攻击响应树（ARTs）[10]中，攻击和响应都在任意节点捕获，但ART作为一种解决方案由于使用部分可观察马尔可夫决策过程（POMDP）而遭受状态空间爆炸问题（或者庞大问题）[11]。
在本文中，我们提出了一种称为攻击对策树（ACT）的新型攻击树模型。我们的贡献总结如下。在ACT中，
	防御机制可以放置在树的任何节点上，而不仅仅放在叶节点上，
	攻击场景的生成和分析以及攻击对策场景都是使用缩略图自动生成的，
	概率分析（使用诸如攻击和安全投资成本，Birnbaum重要性度量，系统风险，攻击影响，ROI和ROA等措施）以综合方式进行（如图1所示），
![4-1](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-1.png) 
图1.使用ACT进行分析
	利用结构和Birnbaum重要性措施优先考虑攻击事件和对策
	采用三种案例研究（ACT针对BGP攻击，ACT针对SCADA攻击，ACT针对恶意内部攻击），证明了将对策纳入ACT的结果[10]。
我们在SHARPE（(Symbolic Hierarchical Automated Reliability and Performance Evaluator，符号分级自动化可靠性和性能评估器）[12,13]软件包中实施了ACT模块。
本文的其余部分组织如下。 相关工作在第2节中介绍。第3.1节中定义了一些基本术语。 ACT的基本模型在3.2节中介绍。 第3.3节描述了使用ACT的定性和概率分析。 第4部分介绍了ACT模块在SHARPE中的实现。在第5节中，我们通过分析案例研究（BGP攻击[14]，SCADA攻击[15]和恶意内部攻击[16]）来演示ACT的效用。 最后，我们在第6部分结束该论文。

## 2.相关工作
Weiss的威胁逻辑树[17]和Amoroso的威胁树[18]标志着使用决策树来描述攻击的开始。 Schneier开发了基本的攻击树（AT）形式[2]，其中PGP AT用于说明AT的应用。 Moore[7]通过引入攻击场景和攻击配置文件扩展了Schneier的AT。 Mauw et.al [19]为AT开发了一种替代形式，其目标是与所有缩略图相关联。当应用于复杂的案例研究时，AT常常变得庞大而笨拙。因此，Daley [20]提出了一种分层的方法来对攻击树节点进行功能划分。由于攻击和故障都会导致系统故障，Fovino et.al [21]通过开发一个称为扩展故障树（EFT）的图理论模型将攻击集成到故障树结构中[21]。但是，这些AT并未考虑到防御机制。为了在AT中融入防御机制，Bistarelli等[8]使用防御树（DT）并应用博弈论来找到最具成本效益的对策。 Edge et.al [22]提出了保护树（PT），它们只关注防御机制而不管攻击。 Zonouz et.al [10]提出了包含攻击和响应的攻击响应树（ARTs），但是使用状态空间模型（部分可观察的随机博弈模型）来找到一组最佳的对策。因此，他们的模型受到状态空间爆炸的影响。我们提出的ACT为安全分析提供了一种简单而紧凑的方法，利用了上述模型的好处，同时避免了状态空间爆炸问题。

## 3.攻击对抗树
### 3.1. 准备
![4-2](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-2.png) 
A_k  一次袭击事件
D_k  一个检测事件
M_k  一个缓解事件
〖CM〗_k  是一种对策
ACT = {V，ψ，E}（V：ACT中所有顶点的集合，ψ：ACT中的所有门的集合，E：ACT中的所有边的集合）
其中V = {∀k，v_k：v_k∈{A_j} || v_k∈{D_i} || v_k∈{M_l}}其中A1，A2，...，D1，D2，...，M1，M2，...是ACT的事件，ψ= {∀k，k：k∈{AND，OR，k-of-n门}}，E = {∀k，e_k：e_k∈（ψ_i，ψ_j）|| e_k∈（v_i，v_j）}并且X =（xA1xA2 ... xD1xD2 ... xM1xM2 ...）是一个ACT的状态向量，其中x_Ak，x_Dk，x_Mk是分别与事件Ak，Dk，Mk相关联的布尔值变量。
ф(X)  ACT的结构功能
〖PA〗_k  发生攻击事件Ak的概率
〖PD〗_kpDk   检测事件Dk成功的概率
〖PM〗_kpMk  缓解事件成功的概率Mk
P_goal   在ACT目标下Pgoal攻击成功的概率
PUD   ACT目标未检测到的pUD概率
PDUM   检测ACT目标到但未发起攻击的概率
I_(A_k)^ST   攻击事件Ak的结构重要性度量
I_(A_k)^B   Birnbaum对攻击事件Ak的重要度量
i_Ak   攻击事件Ak的影响
I_goal   影响ACT的目标节点
〖cA〗_k  攻击事件Ak的开销
C_attacker   ACT的目标节点上的攻击者攻击成本
c_(〖CM〗_k )  对抗CMK的安全投资成本

### 3.2.  ACT的形式
在这一小节中，介绍了ACT的基本形式。在ACT中，存在三种不同类别的事件：攻击事件（例如，安装击键记录器），检测事件（例如，检测击键记录器）和缓解事件（例如，移除击键记录器）。图2（a）显示了一个简单的ACT攻击事件。在目标节点成功攻击的概率的相应表达式如下式所示。
P_goal=pA (1)
![4-3](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-3.png) 
图2.（a）一次攻击事件的ACT，（b）一次攻击和一次检测事件的ACT，（c）一次攻击和多次检测事件的ACT，（d）一次攻击，一次检测和一次缓解事件的ACT ，（e）一次攻击，多次检测和一次缓解事件的ACT，（f）一次攻击，一次检测和多次缓解事件的ACT，（g）一次攻击的ACT，m次检测和n次缓解事件，以及（h）ACT一次攻击和多对检测和缓解事件

在图2（b）中，使用了一个攻击事件和一个检测机制。成功的未被发现的攻击的概率的对应表达式是：
P_goal=pA(1-pD)  (2)
图2（c）是图2（b）的扩展，其中n个检测机制用于检测一个攻击事件。相应的Pgoal是：
Pgoal = pA（1-pD1）（1-pD2）...（1-pDn）（3）
在仅有检测的ACT中，缓解被认为是完美的，即它们以概率1（或pM = 1）减轻。但是，如果缓解措施不完善（即0≤pM<1），除了检测机制之外，缓解技术可用于ACT。图2（d）显示了一个ACT有一个攻击事件，一个检测事件和一个缓解事件。式（4）是攻击成功的概率的对应表达式，即未检测到攻击或检测到但未释放攻击（D代表检测事件，M代表缓解事件）。
Pgoal = pA（1-pD + pD（1-pM））= pA（1-pD×pM））（4）
事实上，如果需要，这个概率可以分成两部分：未检测到的攻击的概率pUD = pA（1-pD）以及检测到但未发起攻击的概率pDUM = pApD（1-pM）。
图2（e）显示了一个ACT有一个攻击事件，n个检测事件和一个缓解事件，并且成功攻击概率的相应等式在式（5）。对于图2（e）中的ACT，未检测到攻击的相应概率PUD=pA∏_(i=1)^n▒〖(1-〖pD〗_i)〗为，并且检测到攻击但未释放的相应概率为PDUM=pA(1-∏_(i=1)^n▒〖(1-〖pD〗_i)×(1-pM))〗。
![4-4](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-4.png) 
图2（f）显示了一个ACT，其中包含一个攻击事件，一个检测事件和n个缓解事件。式（6）给出了相应的成功攻击概率。对于图2（f）中的ACT，未检测到攻击的相应概率为pUD = pA（1 - pD），并且检测到攻击但未释放的相应概率为PDUM=pApD∏_(i=1)^n▒〖(1-〖pM〗_i)〗。
![4-5](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-5.png)
图2（g）显示了一个ACT，其中包含一个攻击事件，m个检测事件和n个缓解事件。式（7）给出了相应的成功攻击概率。
![4-6](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-6.png)

表I.攻击成功概率的公式
![4-7](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-7.png)
图2（h）显示了一个ACT有一个攻击事件和n对检测和缓解事件。引发缓解的性质取决于检测到的入侵的性质。式（8）显示了Pgoal的相应表达式。未检测到攻击的相应概率为PUD=pA∏_(i=1)^n▒〖(1-〖pD〗_i)〗，并且检测到但未释放攻击的相应概率为PDUM=pApD∏_(i=1)^n▒〖(1-〖pD〗_i 〖×pM〗_i)〗-pA∏_(i=1)^n▒〖(1-〖pD〗_i)〗
![4-8](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-8.png)
除AND和OR门之外，ACT还允许k-outof-n门（具有相同或不同的输入）。表I列举了ACT中AND，OR门和k-n门输出概率的公式。


### 3.3. 使用ACT进行安全分析
在本节中，我们将使用ACT进行定性分析和定量分析。
#### 3.3.1. 定性分析
使用ACT的定性分析为我们提供了最小化和结构重要性度量。
![4-9](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-9.png)
##### Mincut（最小切入点）分析。
在AT和ACT中，顶级事件都与所有缩略图的集合相关联。 AT的Mincut表示攻击场景[23]，而ACT的则表示攻击对策场景。我们给出了一个用于BGP攻击的例子[14]（图3中所示的“重置BGP会话”）及其相应的ACT与对策[24]（如图4所示）。其中，所采用的对策包括路由跟踪 [25]作为欺骗TCP重置消息和序列号随机化检测机制之一[24]作为相应的缓解技术。 ACT中的顶（或goal）事件也可以表示为叶节点事件的布尔函数-（Φ（X））。在等式（9），-Φ（X）给出了图3中AT的互补布尔结构函数，其中X是ACT的状态向量，xAi是布尔变量，当事件Ai发生时xAi = 1，否则xAi = 0。图3中AT的最小切换为：{（A111，A12），（A1121，A12），（A1122，A12），（A1223，A12），（A2）}。
-Φ（X）= xA111xA12 + xA1121xA12 + xA1122xA12 + xA1123xA12 + xA2 （9）
图4中ACT的最小切入点（攻击对策场景）为{（A111，-CM1，A12，-CM12），（A1121，-CM1，A12，-CM12），（A1122，-CM1，A12，-CM12），（A1123，-CM1，A12，-CM12），（A2，-CM2）}（其中-CM1 =（-D1M1），-CM12 =（-D12M12），-CM2 = （-D2M2））。 5个切入点中的每一个代表事件的组合，每个事件的发生都会导致攻击成功。例如mincut（A1122，-CM1，A12，-CM12）表示如果攻击事件A1122和A12都发生，并且对策CM1和CM12都失败，则攻击成功，从最小切点（A1122，-CM1，A12，-CM12）中，我们也观察到攻击事件事件（A1122，A12）由对策CM1或CM12中的任何一种所覆盖，我们在3.3.2节中使用了切入点来开发ACT的成本和影响分析方法，在未来的工作中，切入点也将用于找到为ACT设定的最佳对策。
##### 结构重要性度量分析。
确定ACT中最关键的事件很重要。为了达到这个目标，可以使用结构重要性度量[26]。 Boland等人首次提出了基于结构重要性对系统组件进行排序的概念[27]。结构重要性测量[28]用于ACT具有等概率事件，即我们仅提供ACT，但攻击概率（针对攻击事件）和检测/缓解（针对检测/缓解事件）未知。给定一个ACT，可以建立其布尔结构函数（Φ（X））。攻击成功时-Φ（X）= 1，攻击失败时-Φ（X）= 0。考虑两种状态向量：
X =（xA1 xA2 ... xAk-1 xAk xAk + 1 ... xAn）
X'=（xA1 xA2 ... xAk-1 xAk （-xAk + 1 ）... xAn）
ACT中的攻击事件（Ak）的结构重要性度量被定义为状态向量的归一化计数，其中该分量与布尔结构函数相关。等式（1）中显示了IST Ak的相应表达式（10）。
![4-10](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-10.png)
当发生与攻击事件相关的布尔值时，攻击事件（Ak）被认为与特定状态向量X相关，Ak将-Φ（X）的值从1变为0.换句话说，Ak与状态向量X如果(-Φ（X）Ak) –(- Φ（X'）Ak )= 1。一旦确定了系统中最关键的事件，就可以对其进行修补，或者可以强制执行组件的适当检测和缓解。

#### 3.3.2. 概率分析
![4-11](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-11.png)
在第3.2节中讨论了ACT中成功攻击概率的计算。对于ACT，可以计算出成功攻击的概率，该概率可以进一步分解为未检测到攻击的概率以及检测到但未释放攻击的概率。当提供诸如攻击概率，成本等参数值时，可以使用ACT进行概率（或定量）分析。使用ACT的定量分析可以从两个不同的角度来看：攻击者的观点和防御者（或安全分析师）的观点。攻击成本和ROA等措施反映了攻击者的视角，而安全投资成本，风险，影响和投资回报率代表防守者的视角。
##### 成本计算。
在ACT中，成本可能有两种类型：攻击成本和安全投资成本。使用表II [29]中的表达式计算ACT（Cattacker）中没有重复事件的攻击成本。在ACT中，攻击的成本是与门的输入事件的成本的总和，而它是用于或门的输入事件的成本的最小值。 k-n门的攻击成本是k门成本最低的输入事件的总和。对于包含一个或多个重复事件的ACT（如图5所示），我们使用一个简单的过程来计算攻击成本。
 SHARPE [13]可以用来生成ACT的最小切割。最小切割的攻击成本可以由最小切割中每个攻击事件的攻击成本总和给出。选择成本最低的Mincut的攻击成本作为ACT的攻击成本。在图5的情况下，ACT切入点是{（A1，A2），A3}，因此对应的Cattacker = min {cA1 + cA2，cA3}。在OR门的情况下，我们采用“恐慌方法”计算输出端的Cattacker，这意味着在OR门的不同输入事件中，我们选择要传播的攻击代价的最小值。我们这样做是因为攻击者的能力和偏好不能事先知道，并且攻击者被认为是最好的出路（即最低成本攻击）。出于同样的原因，我们选择最小成本mincut，同时计算具有重复事件的ACT的Cattacker。
![4-12](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-12.png)
ACT的安全投资成本是通过总结ACT中反制措施的安全投资成本来计算的。同样使用ACT，可以根据攻击者的资源约束（例如攻击成本）构建可行的攻击场景集合。在SecurITree [30] AT分析工具中称为AT的“基于能力的修剪”。如果提供总攻击成本作为攻击者的资源约束，则可以确定攻击者可以成功利用其资源（成本）约束的一小部分切入点（或攻击情景的子集）。
##### 影响计算。
在ACT中，我们使用与每个攻击事件相关的影响[31]的确切值，而不是追求用于影响计算的缩放方法（例如，以1-10的比例进行标准化）。即使对策不直接影响影响价值，对策也会降低影响的预期价值。表2总结了不重复事件的ACT中不同门的冲击计算。如果ACT中存在重复事件，我们将遵循与成本计算中使用的过程类似的过程。我们首先找到ACT的缩影。 mincut的影响是mincut中攻击事件的影响值的总和。具有最高影响值的最小切割的影响被选为ACT的影响。例如，对于图5（a）中的ACT，由于最小切割是{（A1，A2），A3}，Igoal = max {iA1 + iA2，iA3}。在OR门的情况下，我们再次假定在输出端计算Igoal的最坏情况，这意味着在OR门的不同输入事件中，我们选择要传播的影响的最大值。我们这样做是因为攻击者的能力和偏好不能事先知道，安全分析人员必须做好准备以应对最糟糕的后果（即最大影响攻击）。出于同样的原因，我们在计算具有重复事件的ACT的Igoal时选择最大影响最小切割。
![4-13](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-13.png)
##### Birnbaum重要性度量。
当ACT节点的攻击/防御概率已知时，Birnbaum重要性度量[32]（也称为故障树的“可靠性重要性度量”）用于优先防御机制来抵制攻击事件。攻击事件的Birbaum重要性度量表示在Ak上ACT节点的攻击概率发生微小变化所导致的目标攻击概率的变化。 Birnbaum对攻击事件Ak的重要性度量定义如下：
![4-14](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-14.png)
SHARPE可以用来计算I_(A_k)^B。
![4-15](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-15.png)
##### 风险计算。
在ACT的背景下，风险可以指两种不同的措施，即（i）对攻击者有风险[33]和（ii）对系统的风险[34]。攻击者的原子攻击风险是指检测到原子攻击的概率[33]。 AttackTree + AT分析工具[35]将此类风险称为攻击者的“接受风险”。由于我们在3.2节讨论Pgoal计算中原子攻击的检测概率，本小节中我们讨论了系统的风险。系统风险是指系统对特定攻击场景的风险。在这方面，需要考虑两个措施。一个是攻击场景可以给系统带来的伤害量（Igoal），另一个是攻击成功的概率（Pgoal）。结合这两者，系统的风险可以被定义为影响的预期值。 ACTs的系统风险表述是：
Risksys = Pgoal×Igoal（12）
在没有任何对策的ACT中，CMi的应用导致包含攻击事件Ak（CMi的应用点）的ACT节点的输出概率减小△pAkCMi（例如，结合CMi可能导致图2中的ACT节点（ a）成为图2（d）中的ACT节点）。在ACT中，对策CMi的风险降低（△RiskCMi）可由下式给出：
△RiskCMi = Riskwithout CMi − Riskwith CMi = Igoal × (Pgoalwithout CMi − Pgoalwith CMi )  (13)
其中Pgoalwith CMi是具有对策的ACT的Pgoal。Pgoalwithout CMi是没有对策CMi的ACT的Pgoal。类似地，对于包含对策集SCM的ACT，对策集SCM的风险降低（△RiskSCM）可以由下式给出：
△RiskSCM = Riskwithout SCM − Riskwith SCM = Igoal × (Pgoalwithout SCM − Pgoalwith SCM ) (14) 
##### ROA和ROI计算。
为了量化攻击者和防御者之间的竞争性质，经济学领域的两个度量标准已经适用于安全情景。攻击回报率（ROA）[8,9]是一个指标，旨在衡量特定攻击对攻击者的好处。与攻击成本不同，ROA随着特定对策的应用而改变。 ROA [4]被定义为：
![4-16](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-16.png)
接下来我们讨论投资回报率（ROI）的量化[6]。 ROICMi的基本定义是通过实施CMi获得的利润（从而表明该对策的效率）。反制措施的投资回报CMi是ACT攻击的影响，由CMi引起的ACT目标攻击概率（△PgoalCMi）下降和CMi安全投资成本（cCMi）的函数。根据Sonnenreich对投资回报的定义[6]，在ACT的背景下，我们有：
![4-17](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-17.png)
请注意，ROICMi≥-1。

## 4.实施
我们使用SHARPE [13]评估ACT。我们在SHARPE中实现了一个自动描述和评估ACT的模块。为了计算ACT的攻击概率，最小切割，结构和Birnbaum重要性度量，我们只需使用已有的算法来求解SHARPE中的故障树。我们添加了相关算法（在3.3.2节中进行了介绍），以计算ACT中的成本，影响和风险。 ROA和ROI计算是通过定义SHARPE输入文件中的函数完成的。
## 5.举例
为了分析ACT，我们使用图4的BGP ACT [14]，图7的SCADA ACT [10]和图8的恶意内部攻击ACT（ACT）作为案例研究。 SCADA ACT的两个重要特征是：（i）只包含攻击和缓解事件;（ii）所有缩减范围未被所提供的缓解技术所覆盖。 [16]中提出了ACT的恶意内部攻击（MI ACT）的基本结构。我们通过添加来自其他来源的更低级别的子树来构建此结构（例如，在MI ACT中，从[36]获得恶意用户（图8中的节点A4）的'提升'攻击的子树）。 MI ACT有攻击，检测和缓解事件。但是，在MI ACT中，所有的最小切割都不在所提供的对策范围内。
图6（a）显示了结构重要性度量的变化，图6（c）显示了由于实施对策CMi，BGP ACT中攻击事件Ai的Birnbaum重要性度量的变化。从图6（c）和图6（d）中可以看出，Pgoal的最大降低是由于实施与具有最高值I_(A_k)^B的攻击事件相关的对策而引起的。例如，在没有防御的BGP ACT（或BGP AT）中，攻击事件A1（'发送RESET消息'）的IB值最高，导致首先执行CM1（'Traceroute'）。 Pgoal的相应减少量（如图6（c）所示）是目前所有对策的最大值。因此，针对具有较高I_(A_k)^B值的攻击事件（Ai）应采取对策措施（CMi）的优先次序。类似地，我们可以从图6（a）和图6（b）中观察到，实施具有更高I_(A_k)^B的对策应该被优先考虑。
所有三种ACT的对应节点的输入参数值如表3所示，所有三种ACT的攻击节点的输入参数值如表4所示。
![4-18](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-18.png)
![4-19](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-19.png)
图9（a）显示了BGP ACT（有和没有对策），图9（b）显示了Pgoal的SCADA ACT（有和没有对策），图9（c）显示了Pgoal的MI ACT（有和没有对策） ACT中所有叶子节点的攻击值的概率在[0,1]范围内一起变化。从图9（a）我们发现，BGP ACT的Pgoal值随着检测机制的结合而降低（Pgoal = PUD）。在ACT中只有检测机制，缓解措施被认为是完美的，即它们以概率1工作。因此，通过在BGP ACT中引入缓解措施（不完善的缓解措施），Pgoal会增加（Pgoal = PUD + PDUM）。 SCADA ACT只有攻击和缓解事件。这里假定检测是完美的，即，所有pDi = 1的Pgoal = PUD + PDUM。
从图9（b）中，我们发现Pgoal随SCADA ACT中的缓解措施而减少。类似地，从图9（c）我们发现MI ACT的Pgoal值随着检测机制的结合而降低，然后随着缓解措施（不完全缓解措施）的结合而增加。
![4-20](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-20.png)
图10（a）显示了BGP ACT（有和没有对策）的系统风险（Risksys），其叶节点（pA1123）的攻击概率一起在[0,1]范围内变化，叶节点A1123（iA1123 ）在0-3×105 $范围内均匀变化。观察到Risksys随着检测机制的结合而减少（假设完美缓解），然后随着ACT中缓解措施的结合而增加。图10（b）显示SCADA ACT的Risksys（有和没有对策），叶节点pS1和pG1的攻击概率一起在[0,1]范围内变化，叶节点IS1和IG1的影响值一起变化范围0-3×105 $。观察Risksys在SCADA ACT中采用对策（缓解措施）后会降低的表面。图10（c）显示MI ACT（有和没有对策）的系统风险（Risksys），在叶节点（pA31）处的攻击概率一起在[0,1]范围内变化，叶节点A31（iA31 ）在0-3×105 $范围内均匀变化。从表面上看，对于BGP，SCADA和MI ACT，Risksys随着叶节点处攻击值的概率而增加。它也与相应的ACT的Igoal值成正比。
![4-21](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-21.png)
系统中不同组件的Risksys也可以使用其ACT进行比较。图11（a）显示了针对SCADA ACT的Risksys针对攻击概率值（从0到1一致范围）以及发生器节点G1，G2和G3的影响值（均匀范围从0-2×105 $），而图11（ b）显示了针对SCADA ACT的Risksys针对攻击概率值（范围从0到1一致）以及传感器节点S1，S2和S3的影响值（均匀范围从0-2×105 $）。从表面看，传感器的风险要高于发电机。
![4-22](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-22.png)
图12（a）显示了BGP ACT（有和没有对策）的ROA，叶节点A1123的攻击代价在0-200 $范围内一致地变化，并且叶节点A1123的攻击影响值在0-3× 105 $。与Risksys一样，BGP ACT的ROA随着检测机制的结合而降低，然后随着ACT中的缓解技术（不完全缓解）的结合而增加。图12（b）显示了SCADA ACT（有和没有对策）的ROA，叶节点S1和G1的攻击代价一起在0-200 $范围内变化，叶节点S1和G1的冲击值一起变化在范围0-3×105 $。 SCADA ACT的ROA随着对策的并入而下降。图12（c）示出了MI ACT的ACT（有和没有对策）的ROA，叶节点A31的攻击成本在0-200 $范围内均匀变化，并且叶节点A31的攻击影响值在0-3× 105 $。从表面我们可以看到，对于BGP，SCADA和MI ACT，ROA值与Igoal值成正比，与相应ACT的Cattacker值成反比。
图13（a）显示了BGP ACT的Pgoal，图13（b）显示了SCADA ACT的Pgoal值，图13（c）显示了ACT对所有对策有效的概率（pCMi）在[0,1]范围内一起变化。对于BGP，SCADA和MI ACT，可以看出Pgoal随着pCMi的增加而下降。此外，CM1和CM12对BGP ACT的Pgoal具有相同的效果，并且它们的图重叠。
![4-23](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/4-23.png)
图14（a）显示了BGP ACT中每种对策的ROI，图14（b）显示了SCADA ACT的对策（开关HMI）和（重启G3）的ROI，图14（c）显示了MI ACT中每种对策的ROI对策的安全投资成本（cCMi）在0-100 $范围内均匀变化，相应的pCMi在[0,1]范围内均匀变化。对于所有对策，我们观察到对于pCMi = 0，ROI = -1。从图14（a）可以看出，来自CM2的ROI超过了CM1或CM12。这使安全分析师能够优先考虑在BGP ACT中实施CM2。对于SCADA ACT，冬季（重启G3）的ROI超过（开关HMI）的ROI。与MI ACT类似，CM412的投资回报率超过了CM12和CM123的投资回报率，没有这些，就没有什么可以说话的。
## 6.结论
在本文中，我们提出了攻击对策树（ACT），这是一种非状态空间模型，它允许我们对系统的安全性进行定性和概率分析。我们考虑到攻击和对策（以检测机制和缓解技术的形式）。检测和缓解不仅可以放置在叶节点，而且可以放置在任何中间节点。在结构和Birnbaum重要性措施的帮助下，可以优先考虑ACT中的事件。采用三种案例研究（ACT针对BGP攻击，ACT针对SCADA攻击，ACT针对恶意内部攻击），展示了将对策纳入ACT的效果。在未来的工作中，我们将探讨如何在非状态空间ACT中使用ACT来快速有效地计算大型系统的最佳防御策略，其中使用单目标和多目标优化，给定一定的安全限制（例如，安全投资成本，投资回报率）模型，同时继续避免状态空间爆炸问题。
## 7.相关工作
作者想感谢Dong Seong Kim博士对这一主题材料的深刻回顾。
## 致谢
本研究得到美国国家科学基金会NSF-CNS-08-31325的资助。
## REFERENCES
1. Ortalo R, Deswarte Y, Kaˆaniche M. Experimenting with quantitative evaluation tools for monitoring operational security. IEEE Trans. on Software Engineering 1999; 25(5):633–650.<br>
2. Schneier B. Secrets and Lies: Digital Security in a Networked World. John Wiley and Sons Inc., New York, NY, USA, 2000.<br>
3. Trivedi KS, Kim DS, Roy A,Medhi D. Dependabilityand security models. Proc. DRCN, IEEE, 2009; 11–20.<br>
4. Cremonini M, Martini P. Evaluating information security investments from attackers perspective: theReturn-On-Attack (ROA). Proc. Fourth Workshop on the Economics of Information Security, 2005.<br>
5. Kearney P, Br¨ugger L. A risk-driven security analysis method and modelling language. BT Technology J.2007; 25(1):141–153.<br>
6. Sonnenreich W, Albanese J, Stout B. Return On Security Investment (ROSI): A Practical Quantitative Model. J. of Research and Practice in Information Technology 2006; 38(1):45–56.<br>
7. Moore AP, Ellison RJ, Linger RC. Attack Modeling for Information Security and Survivability.CMU/SEI-2001-TN-001 2001; .<br>
8. Bistarelli S, Aglio MD, Peretti P. Strategic Games on Defense Trees. LNCS 2007; 4691:1–15.<br>
9. Bistarelli S, Peretti P, Trubitsyna I. Defense trees for economic evaluation of security investments. Proc. ARES, 2006; 8–15.<br>
10. Zonouz SA, Khurana H, Sanders WH, Yardley TM.RRE: A Game-Theoretic Intrusion Response and Recovery Engine. Proc. DSN, 2009; 439–448.<br>
11. Sondik E. The optimal control of partially observable Markov processes. PhD Thesis, Stanford Univ.Electronics Labs 1971.<br>
12. Sahner R, Trivedi KS, Puliafito A. Performance and reliability analysis of computer systems: an example-based approach using the SHARPE software package. Kluwer Academic, Norwell,Massachusetts, USA, 1999.<br>
13. Trivedi KS, Sahner R. Sharpe at the age of twenty two. ACM SIGMETRICS Perf. Eval. Review 2009;36(4):52–57.<br>
14. Convery S, Cook D, Franz M. An Attack Tree for the Border Gateway Protocol. Cisco Internet draft 2002;.<br>
15. Baker GH, Berg A. Supervisory Control and Data Acquisition (SCADA) Systems. The Critical Infrastructure Protection Report 1.6 2002; .<br>
16. Butts J, Mills R, Baldwin R. Developing an insider threat model using functional decomposition. Computer Network Security 2005; LNCS(3685):412–417.<br>
17. Weiss JD. A System Security Engineering Process.Proc. of the 14th National Computer Security Conf.,1991.<br>
18. Amoroso EG. Fundamentals of Computer Security Technology. Prentice-Hall Inc., Upper Saddle River, NJ, USA, 1994.<br>
19. Mauw S, Oostdijk M. Foundations of Attack Trees. LNCS 2006; 3935:186–198.
20. Daley K, Larson R, Dawkins J. A Structural Framework for Modeling Multi-stage Network Attacks. Proc. ICPPW, 2002; 1530–1536.<br>
21. Fovino IN, Masera M, Cian AD. Integrating Cyber Attacks Within Fault Trees. Reliability Engineering & System Safety 2009; 94(9):1394–1402.<br>
22. Edge KS. A Framework for Analyzing andMitigating the Vulnerabilities of Complex Systems via Attack and Protection Trees. PhD Thesis, Air Force Institute of Technology 2007.<br>
23. Gan Z, Tang J, Wu P, Varadharajan V. A Novel Security Risk Evaluation for Information Systems.Proc. FCST, 2007; 67–73.<br>
24. Kuhn R, Sriram K, Montgomery D. Border gateway protocol security: Recommendations of the national institute of standards and technology. NIST Special Publication 800-54 2007; .<br>
25. Hu X, Mao ZM. Accurate real-time identification of IP prefix hijacking. Proc. IEEE S & P, 2007; 3–17.<br>
26. Meng FC. Comparing the importance of system components by some structural characteristics. IEEE Trans. on Reliability 1996; 45(1):59–65.<br>
27. Boland PJ, Proschan F, Tong YL. Optimal arrangement of components via pairwise rearrangements. Naval Research Logistics 1989; 36(6):807–815.<br>
28. Fricks RM, Trivedi KS. Importance analysis with Markov chains. Proc. Reliability and Maintainability Symp., IEEE, 2003; 89–95.<br>
29. Nicol DM, Sanders WH, Trivedi KS. Model-based evaluation: From dependability to security. IEEE Trans. on Dependable and Secure Computing 2004; 1(1):48–65.<br>
30. Technologies A. Securitree. http://www.amenaza.com/software.php 2002.<br>
31. Olzak T. A Practical Approach to Threat Modeling.Technical Report, Erudio Security, LLC 2006.<br>
32. Birnbaum ZW. On The Importance of Different Components in a Multicomponent System. Multivariate Analysis - II, Krishnaiah PR (ed.), Academic Press, New York, NY, USA, 1969; 581–592.<br>
33. Higuero MV, Unzilla JJ, Jacob E, Saiz P, Aguado M,Luengo D. Application of’attack trees’ in security analysis of digital contents e-commerce protocols with copyright protection. Proc. CCST, 2005; 57–60.<br>
34. Lathrop S, Hill J, Surdu J. Modeling Network Attacks. Proc. 12th Conf. Behavior Representation in Modeling and Simulation, 2003; 401–407.<br>
35. Software I. Attacktree+. http://www.isographsoftware.com/atpover.htm 2007.<br>
36. Tidwell T, Larson R, Fitch K, Hale J. Modeling internet attacks. Proceedings of the 2001 IEEE Workshop on Information Assurance and security,vol. 59, IEEE, 2001.<br>


