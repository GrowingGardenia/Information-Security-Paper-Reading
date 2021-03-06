# 论文摘要：ACT: Attack Countermeasure Trees for Information Assurance Analysis
# 信息保证性分析的攻击对策树
## 介绍

在对信息安全威胁建模时，研究者对状态空间模型有了更多的使用，重要的实例包括文献9中提出的部分可见的随机游戏模型。这些状态空间模型的缺点是他们可能遭受状态空间爆炸。我们在模型防御方面的方法使得一个帮助避免这个问题的组合模型起作用。我们基于对攻击模型和对策模型特性的组合提出了一种命名为攻击对策树（ACT）的攻击树模型。ACT让人们可以：（１）不仅在防御树的叶子节点，而是在树的任何节点设置检测和缓解形式的防御机制（２）从使用切分模型的ACT中自动生成攻击方案（３）用一个各自联系紧密的方式来进行可能性分析（例如，攻击的可能性，攻击和信息安全投资开销，攻击的影响，系统风险，攻击收益（ROA），投资收益（ROI））（４）使用比基于方法的状态空间模型开销更小的方法从防御机制池中选择一个最优化对策集（５）对树中重复性和非重复性的事件进行分析。为了评估其用途，我们在SHARPE中建议了一个合适的算法和工具在ACT模型。我们使用一个实际的实例研究（BGP　攻击）来证明ACT的实用性。

## 攻击对策树
![1-1](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/1-1.png)  
 
图１　攻击对策树：（ａ）一个攻击事件（ｂ）一个攻击和一个检测事件（ｃ）一个攻击和多个检测事件（ｄ）一个攻击、一个检测、和一个缓解事件（ｅ）多个检测和多个缓解事件
在攻击对策树中，我们可以有三种不同类型的事件：攻击事件（例如：安装一个按键记录器），检测事件（例如：检测按键记录器），和缓解事件（例如：缓解案件记录器）。图１（ａ）－（ｅ）代表了不同类型的ACT节点，相关攻击可能性等式见公式１－公式５，其中，ｐｇｏａｌ是攻击目标成功的可能性。在情况５中，缓解方法被触发的特征依赖于入侵检查的特性。假设检测能同时发生。
 ![1-2](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/1-2.png)  
在一个攻击对策树中与门、或门和k-out-of-n门的输出可能性枚举在表１中。
表１　攻击成功可能性的计算公式
 ![1-3](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/1-3.png)  
注：k-out-of-n门（表决门）假定(C1,C2,...,Cn)是按照开销增长的顺序排列的，(I1,I2,...,In)是按照开销下降的顺序排列的。

## 攻击对策树分析
攻击对策树分析可以是定性分析或可能性分析。
定性分析。攻击对策树的定性分析使用切分模型研究不同的攻击方案和使用重要性测量（IM　 importance measures）研究相关的攻击、检测、和缓解事件重要性。切分模型帮助枚举攻击对策树中的能够使攻击成功的各种最小的攻击事件组合。重要性测量（IM）在定义系统的关键部件时重要的。关键部件的检测／缓解事件可以被赋予更高的优先权。当攻击对策树节点中的攻击、检测和缓解的可能性未知时我们考虑结构重要性（I_(A_ｋ)^ST）。当攻击对策树节点的攻击或防御可能性已知时，使用Birnbaum importance measure（I_(A_ｋ)^BT）。我们在敏感度分析集ROI、ROA的计算过程中使用I_(A_ｋ)^BT。
可能性分析。攻击花费或ROA的度量反映攻击者的观点尽管投资花销、风险、重要性、和ROI代表了防御的攻击者观点。“攻击的花销和重要性”被　Schneier作为分析攻击树的测量【７】。在攻击对策树中，花销有两种类型：攻击花销和信息安全投资花销。在没有重复事件的攻击对策树中，我们使用表１中的公式来计算攻击花销和对该门的重要性。当在攻击对策树中有一个或多个事件重复时，我们使用Rauzy’s的算法来构造攻击对策树相应的二叉决定图（BDD）。我们选定攻击对策树中攻击开销中最低的切分模型的开销作为攻击对策树的开销，选定最高攻击影响的切分模块的影响作为攻击对策树的影响。信息安全投资开销通过计算防御设备的开销之和来获得。风险计算（风险概率估计）由风险的概率和影响计算，因为系统风险通过风险的概率和影响的积给出。例如：预设的影响值。ROA 和ROI量化攻击和防御间的竞争特点。ROA是一个量化从一个特定的攻击中获得的收获的测量。与攻击开销不同的是，防御设备的ROA随着防御设备的申请顺序而改变。ROI是通过防御方执行的k^th防御设备获得的收益。对于一个攻击对策树，ROI根据公式6给出，其中δp_goal （k），I_goal和C_(D_k )随p_goal、攻击成功的影响和依次执行防御机制的开销变化。
 ![1-4](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/1-4.png)  

## 实现和最优化对策选择
### A、实现
我们已经用SHARPE完成了对攻击对策树的风险开销、影响的分析。ROA和ROI的计算可以通过在SHARPE中定义函数完成。我们可能也计算在攻击者资源有限（攻击开销有限制）的情况下可行的攻击方案（切分模型）。图２ａ展示了在重置安全网管阶段的攻击对策树中ROI如何随着安全投资开销和攻击的影响变化。
 ![1-5](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/1-5.png)  
图２　（ａ）BGP攻击时攻击对策树中ROI随攻击影响和安全投资开销和的变化（b）运行时间随树的尺寸大小的变化
### B、最优化对策选择
给出一个系统的攻击对策树，实施整个对策集合中的一个覆盖尽可能多的攻击事件的最有效开销的子集是通常可取的。然后问题减少为在每个切分模型中找出对策集合（C‘）中包含至少一个对策的最小的可能的集合。表２中给出了一种解决这个问题的贪心算法，我们在一个MATLAB的工具箱里实现了所有的最优化算法。表２中的算法直接减少了覆盖优化算法的集合。运行时间＝（在攻击对策树中的攻击事件总数）＊（攻击对策树中的防御装置的总数）＊最小值（攻击事件的数量，防御装置的数量）＝O(mn*min(m,n))(say) = worst case O(m3)（当ｍ＝ｎ时是最糟的情况，例如给每个攻击事件加入一个对应的对策）。随着树的尺寸的增长，优化时间（ｙ轴）随树的节点数（ｘ轴）的变化被画在了图２ｂ。从我们的分析中发现一个系统防御对策的优化集合利用我们的攻击对策树的优化特征与使用攻击响应树相比可以通过相对少的时间获得。
 
## 结论
我们展示了攻击对策树不仅能让我们基于组合模型进行定性和概率分析，也提供给我们了在大型系统中计算最优化防御策略的的方法。
## 参考文献
[1] Z. W. Birnbaum. On The Importance of Different Components in a　Multicomponent System. Technical report, Washington University Seattle　Lab of Statistical Research, 1968.<br>
[2] S. Bistarelli, M. D. Aglio, and P. Peretti. Strategic Games on Defense　Trees. LNCS, 4691:1–15, 2007.<br>
[3] S. Convery, D. Cook, and M. Franz. An Attack Tree for the Border　Gateway Protocol. Cisco Internet draft 2002.<br>
[4] T. H. Cormen, C. E. Leiserson, R. L. Rivest, and C. Stein. Introduction　to Algorithms. MIT press, 2001.<br>
[5] A. P. Moore, R. J. Ellison, and R. C. Linger. Attack modeling for　information security and survivability. CMU/SEI-2001-TN-001, 2001.<br>
[6] A. Rauzy. New Algorithms for Fault Tree Analysis. Reliability Engineering　& System Safety, 40(3):203–211, 1993.<br>
[7] B. Schneier. Secrets and Lies: Digital Security in a Networked World.　John Wiley and Sons, Inc. New York, NY, USA, 2000.<br>
[8] K. S. Trivedi and R. Sahner. Sharpe at the age of twenty two. ACM　SIGMETRICS Perf. Eval. Review, 36(4):52–57, 2009.<br>
[9] S. A. Zonouz, H. Khurana, W. H. Sanders, and T. M. Yardley. RRE: A　Game-Theoretic Intrusion Response and Recovery Engine. In Proc. DSN,　2009.
