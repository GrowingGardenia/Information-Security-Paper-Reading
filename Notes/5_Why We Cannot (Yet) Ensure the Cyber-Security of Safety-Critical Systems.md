# Why We Cannot (Yet) Ensure the Cyber-Security of Safety-Critical Systems
# 为什么我们不能确保安全关键系统的网络安全
Chris Johnson1 <br>
University of Glasgow <br>
Glasgow, UK

## 摘要：
安全关键系统的网络安全性正在不断增加。包括Linux在内的Commercial Off Shelf（COTS）软件，航空，航海，铁路和发电基础设施的专业VOIP应用和基于卫星的增强系统的引入已经造成了常见的漏洞。因此，现在有更多的人拥有识别和利用安全关键系统漏洞所需的技术技能。这是第一次有可能出现跨模式攻击，导致未来的“网络风暴”。公私伙伴关系未能建立关键安全应用的网络安全，加剧了这种情况。财政危机阻止了政府吸引并保留有能力的监管机构在安全和网络安全的交叉点。特别是，我们认为安全（safety）和安全性(security)之间的表面相似性导致安全(security)策略无法在安全(safety)关键系统中实施。现有的基于官方的安全标准，例如ISO27k系列，不能轻易地与IEC61508或ISO26262等标准集成。诸如IEC 62443之类的混合标准缺乏可信的验证。迫切需要超越高层次的政策，解决威胁安全关键系统网络安全的更为详细的工程挑战。特别是，我们考虑网络安全(security)问题如何破坏传统形式的安全工程(safety)，例如通过使传统形式的风险评估失效。我们还总结了安全（safety）问题阻碍传统网络安全(security)机制（包括入侵检测系统）部署的方式。

## 1.引言
安全关键系统(safety)的网络安全(security)的威胁越来越大。部分原因是由于在国家关键基础设施供应链中整合了少量商业现货（COTS）产品。在前几代中，关键基础设施往往依赖于定制系统，这些定制系统在不同行业中未被重复使用（Johnson，2015）。目前，安全相关应用中的COTS组件包括但不限于Linux，VOIP和卫星/地面增强系统（SBAS），如北美的WAAS和欧洲的EGNOS。越来越多的潜在攻击者具有破坏运输，能源分配，食品和水行业等安全相关应用的技术知识。
同时，我们看到新一代恐怖主义威胁的兴起，类似于民族国家的半稳定政权。这些政权可以在其境内获得训练有素的工程师和工艺设备。类似国家的恐怖主义政权已经成为网络安全方面的专家，部分原因在于西方政府实施的政策。警方和情报机构拒绝让他们接触传统的社交媒体。这些机制的回应是发展加密技术和使用源自于深或暗网络的技术的点对点网络。这使得恐怖主义组织将强大的政治，宗教和意识形态动机与已经出售零日漏洞利用，恶意软件库和rootkit的半商业黑客联系起来。
这篇论文的一个关键主题是，政府和私营企业都没有采取必要的行动，以维持我们对网络犯罪和恐怖主义国家日益增长的威胁的防御。公私合作伙伴关系未能提供监管指导和适当的审计机制。财政危机阻止了许多安全监管机构招募和留住在网络安全和安全应用方面拥有足够专业知识的人员。安全和网络安全（safety 和security）之间的文化和组织障碍加剧了这一点。对传统网络安全有着深入了解的人也需要一段时间才能了解出现的问题，例如在核工业或航空工业中。当网络安全技术不能简单地从更传统的基于办公室的系统转移到安全关键环境时，这一点很重要。

政治和组织障碍也有助于解释我们在确保国家关键基础设施方面进展有限。出现这些障碍是因为不同的监管机构负责国家数据网络的网络安全以及特定行业的安全。在英国，OFCOM，国家基础设施保护中心和民航局或核监管局之间的区别就说明了这一点。在美国，联邦通信委员会，国土安全部和联邦航空管理局或核管理委员会之间也有类似的区别，不要忘记美国国家标准与技术研究院（NIST）作为负责联邦的机构联邦信息安全管理法案（FISMA）内的网络安全规定，或者其他地方和国家组织的东道国也可能被列为利益相关者。这些组织和政治区别造成了重大的实际后果。公司通常不了解他们在国家和国际机构（包括计算机紧急响应小组（CERTS），警察，情报和关键基础设施组织以及电信和行业监管机构）对网络事件的报告义务。当安全和安全之间（safety 和 security）的表面相似性导致制定了不适当的政策，而这些政策不能通过现有的工程实践来维持时，这种情况就更加复杂了。以下几页主要关注两类关注点。首先，在某些情况下，网络安全问题会破坏现有的安全做法：
•在系统可能遭受协调和恶意攻击的情况下，常规安全风险评估无法持续;
•现有的安全管理系统对网络安全提供了有限的支持，尤其是在这两个领域的事件报告和根本原因分析方面存在差异;
•网络安全问题挑战了许多现有的与安全相关的软件工程技术，例如，使用软件多样性和Nversion编程会导致供应链的扩展，不可能安全也很难做到。
当安全问题使现有的网络安全技术的应用复杂化时，第二个问题就出现了：
•常规入侵检测系统的局限性。在复杂的遗留系统中，白名单列举的许可过程不容易被应用，并且在有效的、安全相关的过程被拒绝必要的资源时存在危险。与此相反，由于上一节中提到的在安全相关系统中出现的网络事件报告失败，恶意软件的黑名单列表并不起作用;
•传统取证技术的局限性。现有的支持往往侧重于与互联网协议相关的系统，而不是使用非常不同的可编程逻辑控制器（PLC）和协议的工业监控和数据采集（SCADA）基础架构。进一步的担忧源于决定立即隔离开一个受损系统时出现的竞争风险 。
•传统法医技术的局限性。现有的支持往往侧重于与互联网协议相关的系统，而不是使用非常不同的可编程逻辑控制器（PLC）和协议的工业监控和数据采集（SCADA）基础架构。进一步的担忧来自于在决定立即隔离一个被破坏的系统时产生的相互竞争的风险，即在一个潜在的不安全的状态下离开应用程序，或者在关闭之前继续运行，但有可能会覆盖重要的证据;
•传统的网络安全政策对SCADA系统的限制。对于控制系统而言，在许多设备没有联网的情况下，常规安全补丁策略的实现可能会增加而不是减少潜在的漏洞。

## 2.网络安全中安全关键技术的失效。
引言部分指出，我们没有准备好迎接支持许多安全关键行业的COTS基础设施面临的越来越多的威胁。后面的部分将解释为什么现有的网络安全技术(security)难以应用于安全相关(safety)的领域。相反，这一节解释了为什么安全技术常常受到网络安全问题的影响。

### 2.1网络威胁破坏安全风险评估（Cyber-threats Undermine Safety Risk Assessments）
欧洲网络和信息安全局（ENISA，2006）和欧洲空中交通管理组织（EUROCONTROL，2006）主张使用安全管理概念来支持关键基础设施的网络安全（Johnson，2015）。在传统应用中，安全管理系统使用事件报告和其他形式的运行监控来确定实施的系统是否满足从初始风险评估中获得的安全要求。如果出现新的危险形式，或者如果系统未能充分缓解已识别的风险，则需要进一步开发。换句话说，风险评估，设计和运营，监测和事件报告形成良性循环。
 安全管理系统的这些组件也为信息安全管理系统提供了基础。风险评估有助于识别威胁和漏洞。适当的设计和操作程序有助于确保威胁得到缓解。事件报告和审计提供必要的反馈信息，以便在出现新威胁时修正最初的风险评估，并确定在哪些情况下操作不能满足最初风险评估的要求。理论上，使用类似的概念应该支持安全和信息安全管理系统的整合。不幸的是，这些表面上的相似之处掩盖了许多不同之处，这些差异破坏了将安全管理系统的优点转移到安全领域的尝试，显示出缺乏工程专业知识和操作经验，这些已经引导了许多先前的指导（Johnson，2015a）。例如，一个有智慧的对手的存在削弱了传统安全评估中的独立性假设。混合攻击的时间与常规组件故障的时间一致。同样，如果识别出一种形式的网络攻击的症状，那么很有可能系统在其他方面受到了损害。
网络安全问题以其他方式破坏了现有的安全工程实践。他们不仅挑战风险评估的概率组成部分，网络威胁也会破坏与安全有关的后果评估。其中一个原因是我们对新形式的高级持续性威胁的经验有限，例如状态机可以改变Stuxnet的行为，或者使用命令和控制服务器来隐藏来自入侵检测系统的Duqu。这使得预测未来攻击模式的潜在结果变得非常危险。关键基础设施的不断增长的相互连接导致隐藏的相互依赖性。也有人担心“网络风暴”，即单个攻击会导致许多不同的基础设施——例如，当关键系统运行在同一版本的Linux下，或者多个服务依赖于来自同一卫星基础设施的定时信息时。
如果我们有一系列的工具和技术，可以将传统的安全风险评估和网络威胁分析结合起来，那么这些警告都不重要。故障树与攻击树具有表面相似性，但底层语义不同。结果是，许多组织最终形成了无法在安全与安全之间转移课程的并行系统。有一些明显的例外(Pietre-Cambacedes和Bouissou 2010, Johnson, 2015)。然而，很少有关于安全与安全（safety 和 security）的综合方法的已发表的案例研究，甚至对于这些工具在不同行业普遍使用的一致性不甚了解。

### 2.2网络威胁挑战安全事件报告。
多年来，在安全关键行业建立了强烈的事件报告文化。相比之下，很少有公司拥有相同的安全报告文化。其中一个原因是，报道安全(safety)问题的员工通常受到“不受责备”或“与之相称”的环境保护。相反，违反安全(security)规定会引发对其他雇员的纪律处分或法律行动。安全(security)政策和实践之间的不匹配可能会破坏一种新生的报告文化。管理层暗中支持许多安全(security)违规行为，例如承包商使用USB设备，因为他们急于维持运营。这样的事件很少被报道。
许多公司不愿向计算机应急响应小组(CERTs)、监管机构或行业协会报告事件。失去控制和对外部机构的依赖也会损害知识产权，调查人员必须熟悉商业敏感信息，以便诊断攻击的原因。关于跨越国界信息交换的网络安全事件也存在政治上的担忧，甚至对其他友好国家也是如此。
 进一步的障碍阻止使用事件报告来支持安全和网络安全。经验教训的应用确保安全建议尽可能广泛地传播。目的是避免潜在事故再次发生。但是，披露关于网络事件的信息可能会鼓励未来的攻击。它可能会破坏市场信心，可能触发监管行动和诉讼。
虽然有完善的安全问题报告机制，但在欧洲和北美的一系列“地盘战”中，网络事件报道已被破坏。对许多公司来说，它可以清楚报告应该发送给美国联邦航空管理局或核管理委员会等行业监管机构，以便向安全机构（如国土安全部或美国CERT）发送报告或电信监管机构负责整理关于更广泛的网络安全问题的信息，例如联邦通信委员会。在某些情况下，一个事件必须报告给多个机构。例如，在英国，必须向国家行业安全监管机构报告具有安全相关后果的网络攻击，并可能向国家犯罪局，国家网络犯罪部门，GOVCERT，英国信息专员以及通过在网络事件响应（CIR）或网络安全事件响应计划（CSIR）下注册的提供商来保护国家重要基础设施的CESG /中心。 

### 2.3网络安全破坏了安全关键的发展（Cyber-security Undermines Safety-Critical Development）
安全与安全（safety and security）之间的紧张关系跨越了工程生命周期，从风险评估到详细的开发实践。例如，冗余通常用于增加关键系统的可靠性如果一个组件发生故障，则备份可以保持操作。然而，这在没有一定多样性的软件相关系统中提供了很少的好处。相同代码的两个冗余版本可能包含相同的错误，因此也会以同样的方式失败，即使它们提供的数据略有不同。因此，n版本编程技术依赖于使用两个或多个承包商来开发同一个程序的多个版本。如果一个失败了，另一个就不会。使用不同的供应链有助于确保两个程序不共享常见的错误，假设它们的需求是正确的。
不幸的是，软件多样性为安全管理带来了迫在眉睫的问题。最终用户必须确保两个或多个不同的供应链 - 换句话说，冗余的多样性打开了多条路径，通过这些路径，可以将受损代码集成到安全关键系统中。客户必须审核多个分包商，以确保他们符合约定的网络安全要求。在安全关键软件开发中很少考虑这些安全问题。客户几乎没有保证供应商审核员工，阻止不受信任来源的代码的引入等。 
元层面（meta-level）的观点是，安全与网络安全（safety and security）的结合揭示了一系列的紧张关系，只有通过整合才能解决。如果没有这一点，我们就不能假定这两个孤立的社区将为本文所确定的问题提供可行的解决办法。例如，少数安全（safety）关键的公司现在在他们自己的组织内提供不同的供应链。换句话说，他们将为客户提供两个软件，每个软件执行非常相似的功能，但保证他们是由不同的团队使用不同的开发方法来实现的。这简化了供应链，但依赖于一系列创新的软件管理和开发实践。这种做法是否足够强大，足以解决当冗余软件来自同一供应商时产生的自然安全问题，还有待观察。

## 3.安全技术在网络安全中的失败(The Failures of Safety Techniques in Cyber-Security)
上一节指出，由于安全技术经常受到网络安全问题的影响，因此迫切需要集成的工具和专门知识。相比之下，以下段落认为现有的网络安全策略不能很容易地应用于安全相关的领域。我们着重于三个例子:
1.传统的入侵检测系统破坏了复杂应用的安全性;
2.其次，传统办公系统的现有取证指导将导致安全关键系统的寿命缩短;
3.最后，许多SCADA环境的气隙架构破坏了现有的安全管理原则。
### 3.1安全问题限制了网络入侵检测系统(Safety Concerns Limit Cyber-Intrusion Detection Systems)
NIST（2012）主张在关键应用程序中使用几种不同的入侵检测系统（IDS）。这在IDS可能错误地阻止安全相关应用程序中的关键过程时引起了重大关注。入侵检测主要有两种方法。黑名单依赖于检测恶意软件的特征。白名单将在随后的章节中讨论，依赖于认可批准的代码。
大多数黑名单IDS旨在保护基于办公室的系统。恶意软件的特征和症状是通过一系列机制（包括蜜罐（Spitzner，2002））报告的事件证据编制的，也可以通过向主要安全公司进行保密报告。第2.2节总结了阻碍安全关键系统中网络事件信息交换的障碍。除非我们能够识别恶意软件特征，这些特征表明对工业控制系统日益增长的威胁，否则尝试开发黑名单IDS将为SCADA应用提供非常有限的保护（Naedele，2007）。
为了保护系统，一旦识别出恶意软件签名，更新黑名单就很重要。但是，这在安全相关的应用中产生了问题，因为在软件修改之前需要进行详尽的测试。上传损坏的黑名单也可能导致检测系统的失败，从而导致与安全相关的过程产生连锁反应。在确定新签名后，安全工程师将面临在更新黑名单的竞争性要求和确保新签名不会破坏应用程序安全性的要求之间的困难决策。
与黑名单相比，白名单IDS确保只有经批准的程序才能执行。他们描绘和报告任何偏离“正常行为”的情况。这可以通过创建所有软件应用程序的散列摘要来实现。如果可执行文件的哈希不匹配列表中的任何内容，则会触发安全事件。同样重要的是防止未经授权的用户更改显示哪些文件可以被执行的列表。

白名单为安全关键应用程序提供好处。确定“正常流程”的重点消除了不断更新恶意软件签名的需要。白名单提供一些针对零日攻击的保护 - 即使攻击的签名未知，恶意代码也不会包含在已批准的散列列表中。但是，这种方法的应用引起了一些担忧。例如，跨多个控制系统实例的同一次攻击将同时导致大量分布式安全事件。这些可能会压倒组织的及时响应能力，也可能由非恶意原因触发。软件更新没有反映在白名单上的变化会导致大量的误报。安全关键流程可能会被拒绝计算资源。因此，在所有软件安装过程中，工作人员和分包商都必须遵守约定的安全更新程序。在一些安全关键的应用程序中，这是相对简单的 - 例如在长期存在的SCADA系统中，PLC上的软件更新相对较少。在其他情况下，比如空中交通管理，每个分包商都有知识产权方面的问题，可能很难确定什么是和什么不是“正常过程”。

数据二极管确保信息只能在一个方向上传播;例如，从光纤电缆的一个方向上移除发送和接收收发器。它们可以被使用，这样流程数据只从操作区域流向业务系统，反之亦然。这些设备还可以将IDS与关键进程隔离开来。数据的单向流动减少了对检测系统将对应用程序安全产生不利影响的担忧。不幸的是，更高水平的监测会导致越来越多的误报。这可能会破坏网络态势感知，当运营商错误地停止他们担心已经受到威胁的应用程序时，可能会导致拒绝服务。相反，提高IDS容忍度阈值会增加错过肯定的可能性。在安全关键的系统中，这导致了IDS的过度容错配置允许公司继续在关键应用程序中使用恶意软件进行操作的可能性。在传统的基于办公室的系统中，机器学习技术已经成功地部署了威胁可视化技术，将自动入侵检测与人工决策集成在一起。还需要进一步的工作来确定这些方法是否也能适用于解决在安全关键系统中破坏网络环境意识的假阳性/假阴性问题。
### 3.2空气间隙系统的安全性破坏了网络策略（Safety in Air Gapped Systems Undermines Cyber Policies）
大多数现有的网络安全工具和技术专注于基于传统IP堆栈的分布式体系结构。相反，许多与安全相关的应用依赖于计算设备，例如甚至从局域网隔离的PLC。监视和控制应用程序的行为可能在十年内不会改变。设备与任何网络之间的“空隙”可提高安全关键型应用的网络安全性，因为它限制了远程攻击的机会。然而，“空隙”也限制了使用黑名单IDS的机会。对于系统管理员来说，没有一种简单的方法可以自动更新带有恶意软件签名的节点。操作员必须在整个工厂的每个隔离设备上手动安装任何更新。这导致了一个悖论。任何攻击者都很难破坏独立的PLC，除非它被挂钩到其他设备 - 例如安装补丁或更新IDS。这些更新越频繁出现，交叉污染的风险就越大。因此，安全关键型系统的系统管理人员通常故意忽视传统的网络安全建议，宁愿将未隔离的设备留在原位。其他问题限制了白名单在气隙系统中的应用。如果没有网络访问，工程师可能需要几周或几个月才能详细检查日志，以便记录远程设备上的感染。
### 3.3安全问题破坏了传统的网络取证（Safety Concerns Undermine Conventional Cyber-Forensics）
详细的指导方针涵盖了网络安全事件的取证分析。例如，美国司法部（2004年，2008年）建议法医调查人员必须保留“证据链”：
•“立即保护所有电子设备，包括个人或便携式设备。
•确保没有未经授权的人员在犯罪现场使用任何电子设备。 
•拒绝任何未经授权的人提供帮助或技术援助。 
•从犯罪现场或收集证据的邻近地区移除所有人员。 
•确保任何电子设备的状态不变。 
• 停！如果计算机或电子设备已关闭，请将其关闭“。
这些原则支持基于办公系统的网络取证。它们还说明了将现有安全措施集成到安全关键系统的问题。很难想象，任何一个调查机构如何能立即确保“所有电子设备”分布在一个折衷的过程控制系统中，或者如何列举所有连接到现代国家空中交通管理系统的设备。许多安全关键的公司都有最低限度的访问控制政策，因此对于那些在犯罪现场完全授权使用这些设备的外部机构来说，并不总是很清楚。通常情况下，有很强的外围接入形式——只有员工和授权的分包商才能进入设备或机房，但一旦进入设备或机房，他们就会对机架和网络组件进行访问。这与金融机构，甚至是web服务提供商形成了强烈的对比，在这种情况下，可以使用细粒度的访问控制策略来阻止软件工程师访问机房。在拥挤的空中交通管制中心或核控制室中，将“所有人从犯罪现场”移除可能是灾难性的。在这种情况下，操作、工程和安全管理必须在应急行动中进行合作，包括网络攻击的后果。“如果电脑或电子设备已关闭，请将电脑或电子设备关闭”以防止使用冗余保护系统。

司法部的准则旨在通过敦促调查人员关闭任何受损系统来保存证据。持续的操作可能会覆盖有价值的数据，或者使攻击者能够掩盖系统受到攻击的方式。然而，立即隔离安全关键系统可能危及公众和运营商的生命。启动回退系统可以降低此风险，直到应用程序达到安全状态。但是，这会增加交叉污染的风险。换句话说，在工程师和调查人员不可能知道最初传播攻击的机制时，停止主要应用程序以保存取证数据可能会导致二次系统的感染。如果没有某种形式的整合，业务人员、高级管理人员和调查机构就无法平衡应用程序的安全、交叉污染的可能性和法律要求，以保存在攻击后起诉所需的证据。 
## 4.结论和进一步的工作
我们面临着越来越多的对安全关键系统的网络威胁。像国家一样的恐怖组织拥有大量的资金和工程资源。对安全关键系统的威胁也来自恶意软件的商业市场，通过黑暗/深度网络的点对点网络，那些缺乏开发它们所需技术技能的人可以购买零日漏洞。与此同时，我们的漏洞正在增加 - 通过将包括Linux，IP语音（VOIP）和基于卫星的增强系统等COTS应用整合到安全关键应用中。为加强网络安全而建立的公私合作伙伴关系，在解决这些问题方面收效甚微，部分原因是由于财政危机和组织障碍导致我们没有能够胜任安全关键应用网络安全的监管机构。
安全和安全（safety and security）之间表面上的相似性导致了不能使用现有工程技术的政策的发展。在网络攻击之后，对于安全问题的独特关注使我们不能简单地利用现有的基于办公室的系统的指导。在取证调查过程中，我们不能立即隔离安全相关的过程，也不会危及依靠关键基础设施的人员的生命。同样，如果这些应用程序可能会阻止关键进程，或者更新恶意软件签名无意中破坏了与安全相关的系统，我们就无法重用传统入侵检测系统。
还有很多领域需要进一步开展工作，包括对安全关键系统中的网络事件进行因果分析。系统性因素有助于创建事件或事故可能破坏应用程序安全性的环境。相反，安全调查倾向于更多地关注有意或无意的违规行为。这种关注安全事件的直接人为原因类似于十多年前以安全相关报告为特征的“完美方法”（Johnson，2003）。因此，我们可能期望安全调查的重点在未来转向系统性因素。为了实现这一点，我们似乎需要新一代的根本原因分析技术。大多数现有的方法在安全相关事件之后使用反事实推理。建议是通过确定原因而得出的，如果这些原因被阻止，那么事件就不会发生。这种推理不容易适用于网络攻击。如果敌人发起多个同时进行的攻击，其中一些没有被发现，那么就很难认为安全事件会被阻止。

## References 
 
ENISA, (2006), Risk Management: Implementation principles and Inventories for Risk Management/Risk Assessment methods and tools, Conducted by the Technical Department of ENISA, Section Risk Management, Heraklion, Greece, June 2006. <br>
EUROCONTROL (2006), Safety Case Development Manual, Technical report DAP/SSH/091, Brussels, Belgium.  <br>
Naedele, M. (2007), Addressing IT Security for Critical Control Systems, Proceedings of the 40th Hawaii International Conference on System Sciences, IEEE Computer Society.  <br>
Johnson, C.W., (2003), Failure in Safety-Critical Systems: A Handbook of Accident and Incident Reporting, University of Glasgow Press, Glasgow, Scotland, ISBN 0-85261-784-4, available in in electronic form.  <br>
Johnson, C.W., (2015), Contrasting Approaches to Incident Reporting in the Development of Security and Safety-Critical Software.  In F. Koorneef and C. van Gulijk (eds.), SAFECOMP 2015, Springer Verlag, Heidelberg, Germany, 400-409, LNCS 9337, ISBN 978-3-319-24254-5.  <br>
Johnson, C.W., (2015a), Barriers to the Use of Intrusion Detection Systems in Safety-Critical Applications.  In F. Koorneef and C. van Gulijk (eds.), SAFECOMP 2015, Springer Verlag, Heidelberg, Germany, 375-384, LNCS 9337, ISBN 978-3-319-24254-5.   <br>
Piètre-Cambacédès, L. and Bouissou, M., (2010), Modelling Safety and Security Interdependencies with BDMP (Boolean logic Driven Markov Processes). IEEE International Conference on Systems Man and Cybernetics (SMC), 10-13 Oct. 2010, 2852 – 2861.  <br>
Spitzner, L. (2002), Honeypots tracking hackers. Addison-Wesley. pp. 68–70. ISBN 0-32110895-7.  <br>
U.S. Department of Justice (2004), Forensic Examination of Digital Evidence: A Guide for Law Enforcement.   <br>
U.S. Department of Justice (2008), Office of Justice Programs, Electronic Crime Scene Investigation: A Guide for First Responders, Second Edition, Washington DC, 2008. http://www.nij.gov/publications/ecrime-guide-219941/  <br>
U.S. National Institute of Standards and Technology (NIST, 2012), Computer Security Incident Handling Guide (Draft), Special Publication 800-61 Revision 2 (Draft), Gaithersburg, Maryland.
