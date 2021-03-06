# Achieving ICS Resilience and Security through Granular Data Flow Management
# 通过精细的数据流管理实现ICS的弹性和安全性

## 作者 
本杰明格林  安全兰开斯特研究中心  兰卡斯特大学兰开斯特，英国    
b.green2@lancaster.ac.uk  
Marina Krotofil  霍尼韦尔工业网络安全实验室  亚特兰大（GA），美国  
marina.krotofil@honeywell.com  
大卫哈奇森 计算与通信学院 兰卡斯特大学兰开斯特，英国   
d.hutchison@lancaster.ac.uk  

## 摘要：

现代工业控制系统（ICS）依靠企业来建立连接。在ICS的规模，多样性和复杂性增加的情况下，各个子系统的用户所遵循的操作要求，目标和挑战随之而来。信息技术（IT）和运营技术（OT）融合的最新趋势可能导致运营商无法全面了解端到端数据流要求。这会给系统安全性和弹性带来风险。传感器曾经仅用于操作过程使用，但现在作为支持多种组织要求的输入。如果没有完全理解这些，可能会出现不完整的风险评估和不恰当的安全控制实施。在寻求解决方案时，运营商可能会转向标准和指导方针。在介绍案例研究和概念工具之前，本文回顾了流行的标准和指南，强调了数据流，关键数据处理点和系统到用户关系的重要性。拟议的方法构成了风险评估和安全控制实施的基础，有助于ICS安全性和弹性的发展。

## 关键词

工业控制系统; SCADA;数据流;安全;弹性;风险评估;社会技术系统

## 1.引言

工业控制系统（ICS）用于各种行业，用于工业过程的操作。这些包括发电和配电，水处理和分配，制造等。{由于其运营对社会福祉的影响，其中一些被认为是关键的国家基础设施[10]。近年来，工业部门已披露的ICS漏洞数量显着增加[23]。虽然技术重点研究的这种增长有其优势，但挑战仍然不仅在于如何最好地将安全的重要性传达给行业中的人，还有如何最好地理解跨多个系统级别/业务领域的运营目标，并确保任何安全形式的实施不会降低可用性或产生级联效应，从而对本地或业务范围的运营目标产生不利影响。

在石油，天然气和化学品等加工行业中，识别最终可能导致不良产出的模式转变的能力至关重要。特别值得关注的是关键数据处理点，如果发生变化，则有可能影响流程操作，在安全恢复之外仍然未被发现。在[36]中，Weiss提供了一个示例，说明传感器信号滤波参数看似无关紧要的变化如何导致核电站设备的重大损坏。

控制系统本质上是气动的，在向电子替代品过渡之前，以及20世纪70年代的最终计算机集成制造（CIM）概念，其中数据和信息成为自动化中最重要的成分，关键是处理在自动化系统内建立的透明信息的数据和信息。然后，在寻找能够集成企业的所有级别和功能单元的自动化架构（从战略规划到流程）的过程中出现了挑战。为了应对预期的复杂性，设计了将数据处理严格细分为分层模型，这被称为自动化金字塔[30]。
 
 ![13-1](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/13-1.png)
 
图1描绘了自动化金字塔，也称为Purdue模型。在[16]中讨论过，Purdue模型被视为将ICS功能划分为分层的简单方法。结合图1，[16]提供了每个系统级别的附加概述，包括示例设备及其功能。将设备分配到自动化级别还突出了与数据收集和响应相关的不同时间限制，并将设备功能的重要性进行了概念化。简单地说，当讨论驻留在ICS较低层的设备时，例如传感器，执行器，可编程逻辑控制器（PLC），远程终端单元（RTU）等。通信必须在几秒钟内进行，有些情况下达到毫秒级。但是，驻留在中等到较高级别的设备（例如数据历史记录，人机界面，信息技术（IT）工作站等）可能仅需要在几分钟到几小时的时间内进行通信，在某些情况下可以是数天和数周。

运营技术（OT）学科在整个运营过程中支持物理价值创造，而IT则结合了数据和信息处理、传输和存储的所有必要技术。这两个不同的ICS区域之间的界限通常位于Purdue模型的第三和第四级。自CIM概念以来，大多数行业都独立开发和管理OT和IT，作为孤立的域。然而，近年来，OT已经开始逐步采用类似IT的技术[7]。实现这些好处的先决条件是掌握战略，组织和技术挑战。实现一些所谓的IT / OT融合（即IT和OT的端到端管理），意味着IT和OT策略协调，安装公共治理和流程模型，集中管理安全和数据，以及人力资源是熟练的，以了解两个学科的不同要求。


虽然现有的工作已经探索了IT / OT融合的挑战，但社会和技术因素通常是孤立地或理论上讨论的。社交因素与个人技能组合、行为、目标、挑战、要求等有关。技术因素与OT领域内IT技术的采用、设备的复杂性/多样性增加、功能和跨多个系统级别的交互相关，结合起来，可以理解增加技术复杂性和功能的要求，考虑个人的要求，以满足每个系统级别的设定目标。然而，对社会和技术综合因素的详细讨论需要经验数据集和综合分析，以便对观察到的联合挑战作出明确解释。本文介绍了一项实证研究的结果，用于更好地理解ICS中的技术数据和处理点，同时也突出了人（社会）因素的复杂性和交叉性。

安全标准和准则提供了一种资源，可以采取实际步骤来提高安全性和恢复能力;但是，在风险评估和控制实施之前理解系统的建议是有限的。结合上面提到的挑战，我们因此需要一种有助于发现系统攻击面的工具。这包括数据流和处理点的识别，以及不仅突出显示系统到系统，还突出显示系统到用户的关系。获得数据路径的清晰可见性并非易事。在可以处理和组合来自多个来源的数据的情况下，在作为对其他设备的新输入的进一步传输之前，系统到用户交互水平的复杂性增加，具有过多的个别要求，挑战和目标。

本文的其余部分的结构如下。第2节介绍了在ICS中管理数据流时的目标，要求和挑战。第3节对用于风险评估和安全控制选择的流行标准和指南进行了回顾。第4节介绍了案例研究和概念工具，以便在第5节的结论和未来工作之前更好地理解系统到系统和系统到用户的关系。


## 2. ICS中的数据流

在许多情况下，控制器和操作员只能通过传感器读数观察物理过程，并且必须确信过程数据描述了真实的潜在情况。传感器信号以多种方式处理，通过各种功能，例如放大、缩放、转换、滤波、聚合和归一化等等。此外，在额外的控制器和应用程序消耗之前，通过计算公式组合数据源。实质上，基于数据链中每个阶段的数据消耗电路/设备/应用所定义的要求，进行数据处理以提供可用/可操作的信息。沿着路径的数据处理中的任何错误都有可能降级甚至失去对过程状态的可见性。了解数据源和路径对于理解由于错误或故意操纵数据流而对流程操作产生的不良影响至关重要。

### 2.1数据可靠性

OT工程师负责数据内容。必须在操作过程中从适当的来源收集数据，符合任何规定的时间限制。随着OT的发展，对数据收集的这些要求已经发生了重大转变。因此，单个传感器输入不再仅用于工厂的本地操作过程决策。例如，在英国，环境、食品和农村部门（DEFRA）等监管机构需要数据，以确定组织是否符合预定的运营限制，最终效果的质量和数量[15]。这些基本法规推动了运营要求。但是，这些相同的数据也可用于绩效分析，并随后用于董事会层面的决策者，以确定运营场所/区域的财务可行性，并确定流程简化所需的投资。此外，它还可以应用于远程警报监视/管理无人操作过程。在某些情况下，这种远程监控和管理可能构成组织安全报告流程的一部分。如果不清楚地理解与原始数据收集要求的偏差，系统变更的应用，更不用说风险评估和安全控制实施，是一项重大挑战。

当仪表工程师重新校准或更换传感器时，他们可能会知道与PLC组态工程师联系，以便考虑PLC逻辑中应用的变化，从而保持稳定的物理过程操作。这满足了传感器的初始要求，即为运营决策提供准确的输入。但是，当出现与相邻设备，RTU和Data Historians相关的重新配置要求时，如果这些要求保持不变，则监管、警报监控、安全和性能分析数据可能会受到影响。在给定的示例中，对PLC之外的传感器数据消耗的了解可能超出了仪表工程师角色的范围。正是出于这个原因，在制造区内识别复杂的系统到系统（设备到设备的交互）和系统到用户的关系（最终用户和维护人员与系统的交互）和要求（图1），展示OT挑战的现实，围绕新技术和/或现有OT技术的持续部署和开发，与各级ICS中越来越多的数据用户并行。

### 2.2 数据完整性

针对运营流程（不包括间谍活动）的大多数攻击将试图篡改流程数据和信息流。这通常被认为涉及攻击者通过其接收通信链路，然后使用重放，分组注入或有效载荷的方向操纵的过程，实现不期望的改变。网络监控和入侵检测技术的应用被视为有效的缓解策略。但是，他们可以忽略在任何给定设备中发生的恶意操作的可见性水平，以及不常见的合法的系统到用户交互。

在ICS中，数据源自物理空间，因此数据可靠性和完整性从正在处理的第一个测量点开始。发生在Purdue模型的0级时，必须首先校准和缩放模拟信号，将其转换为有用的测量单位。这代表了恶意行为者操纵数据的第一步[1]。一旦转换为数字值，数据将呈现给控制器（PLC，RTU等），作为控制算法的输入。过程控制决策可以基于预定逻辑自动进行，或者通过用户通过人机界面（HMI）与控制器交互来手动进行。基于第I部分中描述的自动化金字塔原理，通过在各个设备中映射数据流和数据处理点，可以进一步提高系统理解和可见性。一旦映射，就会显示出更大的攻击面，从而可以进一步重新评估风险评估过程和后续的安全控制实施。

### 2.3 错过了什么

由于错误的数据处理配置而导致的错误对流程操作的潜在影响可能与通过恶意操作引起的错误一样重要。后者需要实施安全控制。但是，由于确保数据可靠性已经成为一个重大挑战，因此必须仔细考虑安全控制的实施。如果风险评估和安全控制实施基于对OT域内以及OT / IT域之间的系统到系统和系统到用户关系的不充分了解，则会对跨两个域的目标产生额外的风险。

如果没有明确了解与原始设备要求的偏差，风险评估和安全控制实施的应用就会产生明显的可能性，即实施不充分或不适当的限制，降低可用性并对运营，业务和安全目标产生负面影响整个组织。在寻求解决方案时，运营商可能会寻求有关风险评估和安全控制实施建议的标准和指南。但是，应用安全标准需要了解系统。有了这个，所需的系统理解水平以及获得/呈现它的方法论至关重要。

获得系统到系统和系统到用户关系的视图，将为全面的风险评估和随后的定制安全控制实施提供平台。通过ICS更精细地查看数据流和处理点来控制控件，可以提高数据可靠性和安全性的协调性。此外，数据流中系统到用户交互的可见性将允许简化的变更管理集成。这可确保OT和IT人员定义的操作要求保持不变，并在可能的情况下进行优化。如果没有所描述的可见性水平，不仅可能发生系统性能下降，而且安全控制可以充分保护一个关键数据，但仍然完全无视另一个。

## 3.标准和指南概述

为了保护信息，企业需要围绕信息保护实施规则和安全控制，包括用于存储和处理信息的系统。这通常通过实施信息安全政策，标准，指南和程序来实现。对于ICS，这些可以是行业特定的[27]，或更通用和全包[32]。作为监管合规的先决条件或其全面指导，安全标准和指南提供了一种在ICS领域内引起关注的资源。因此，以下小节回顾了一组广泛使用的标准和指南1.旨在帮助风险评估和安全控制实施过程，讨论以下标准和指南。来自英国标准协会（BSI），ISO 27001 [4]，ISO 27002 [5]，ISO 31010 [3]和ISO 27019 [6]。来自美国国家标准与技术研究院（NIST），800-53 [21]，800-30 [20]和800-82 [32]。最后，来自国家重要基础设施保护中心（CPNI），管理商业风险[11]，风险评估[9]，与理事会合作编写的关于网络安全的重要安全控制[14]，以及选择和实施安全改进[12]。

选择这些标准和指南是因为它们直接针对ICS和关键基础设施环境[8]，全球接受作为“信息安全的共同语言”[19]，并在包括国防部在内的政府部门中使用[ 29]。

### 3.1 风险评估过程概述

风险评估输出用于定义组织安全要求的关键信息。从风险的基本观点出发，[22]将风险定义为“威胁利用漏洞从而对资产造成损害的可能性”。因此，在评估风险时，应该设法理解现有的系统和环境。通过预先描述的评估方法识别风险的方式。系统范围和目标可以影响评估的格式和后续输出，用于实施安全控制，减轻已识别的风险。

ISO 31010 [3]将风险评估过程分为三个关键阶段：风险识别，风险分析和风险评估。提出了一个广泛的技术表，其中每种技术的适用性都映射在三个阶段。从该表中，然后详细解释每种技术，包括其使用、所需输入、过程、输出和强度/限制。

NIST 800-30 [20]将风险评估过程分为五个阶段：识别威胁来源和事件，识别漏洞和预防情况，确定发生的可能性，确定影响的大小，并确定风险。除此之外，还定义了三个层次来优化整个系统的要求：组织，任务/业务流程和信息系统。将这些作为基本原则，详细讨论了五个阶段中的每一个阶段，包括所需的输入，评估量表，分类法，模板等，以便进一步实际应用。

CPNI风险评估[9]简要讨论了风险评估过程。讨论分为四个逻辑部分：确定威胁，确定需要保护的内容并识别漏洞，确定降低风险的措施，并审查您的安全措施和演练。

NIST 800-82 [32]侧重于在ICS环境中进行风险评估的特殊考虑因素。这包括诸如安全性（safety），物理影响，非数字控制组件，对连接系统的影响传播等因素。根据

FIPS 199 [26]确定影响的其他要点（考虑ICS对其机密性影响的风险，还讨论了完整性和可用性）。 [26]指出，通过使用其影响评估方法，可以将产出应用于风险评估的优先次序，而较低的影响系统则未被评估。

ISO 27019 [6]提供了风险评估的非常简短的定义，包括其在安全措施/控制选择中的使用。但是，除了这个简短的定义之外，没有提供进一步的ICS特定指导。
 
![13-2](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/13-2.png)
 
### 3.2 安全控制选择过程概述

安全控制是组织信息系统中采用的管理，操作和技术保障或对策。这些提供了保障措施或对策，以防止通过风险评估过程确定的资产的安全风险，其中资产被定义为任何组织资源（数据，系统，人类等）[37]。

ISO 27001 [4]提供了一套总体安全控制类别，具有相关目标的子类别，以及各个控件，其中每个控件都以简明扼要的描述形式呈现。通过分类的应用，简化了相关控制的选择。 ISO 27002 [5]与[4]中涵盖的控制并行，提供了每个控制的更详细的细节，包括实施指南和其他相关信息。

NIST 800-53 [21]以与[4]和[5]类似的方式提出了安全控制指南。提出总体安全控制类别，具有相关目标的子类别以及具有相关相关控制的个别控制，以进一步探索。

ISO 27019 [6]采用过时修订[5]（[2]）中定义的安全控制，并在适用的情况下讨论了能源公用事业部门的其他信息。 NIST 800-82 [32]采用了[21]中所述的建议，并提供了额外的ICS特定建议书和指南，类似于[6]，但更详细。附录G中提供了一个叠加层，用于进一步了解如何根据ICS环境定制控件。此外，对ICS特定挑战的确认，如果不能采用建议的控制措施，可以采取补偿性控制措施。

CPNI/网络安全委员会20大安全控制[14]是为广大受众设计的，因此它不包含其他作品提供的粒度级别。但是，定义了20个总体类别的安全控制，子类别则显示特定安全控制及其目标的描述。

CPNI选择和实施安全性改进[12]并非旨在提供一整套安全控制，而是为选择和实施控制时要考虑的关键因素提供指导。围绕规模经济，技能和经验，多样化，优先排序，成本计算，变更控制等的讨论都包含在ICS的背景下。

此处描述的安全控制选择和实施标准和准则提供不同级别的粒度。他们的过程可以总结如图3所示。在ICS环境中使用控件的定制范围从高级别考虑优先级，技能等，到个人，控制特定，增强建议。在不同抽象层次上提供建议可以是积极的，因为它可以发挥各种受众的优势，特别是ICS运营商首次冒险进入安全领域。
 
![13-3](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/13-3.png)


### 3.3 遗漏了什么

执行安全风险评估时的关键挑战之一是估计所有风险所在。对风险的不完全理解产生了狭隘的安全目标和很少的安全控制。

所提供的标准和指南概述说明了为IT系统设计的成熟方法如何适应ICS受众。但是，重点仍然是信息安全，保护访问和确保数据包的安全传输，而不是保护流程操作。主要安全目标是保护数据完整性，因为数据完整性的丢失直接导致视图丢失，从而失去对物理操作过程的控制。正是出于这个原因，在寻求进行风险评估并随后实施安全控制时，理解要执行此类任务的系统变得至关重要。

在围绕理解系统提供指导的情况下，可能不足以在ICS环境中进行全面的风险评估和安全控制实施。例如，[11]提供了一组问题，可用于创建考虑上游和下游依赖关系的设备，技术，资产所有者等的清单。但是，如果[3]定义了个别评估技术的先决条件，那么除了一组问题之外几乎没有引导而创建的拟议清单是否会满足这些先决条件。此外，在安全控制实施必须考虑全系统目标/要求的同时，与风险评估产出并行，还需要全面了解该系统。在技术系统到系统以及社交系统到用户级别需要这种理解。

为协助风险评估过程而开发的工具包括[35]，并为评估员提供了一种可以根据标准目录衡量其系统的方法。但是，对如何最好地获得确保产生准确结果所需的信息提供的建议很少。作为可选的现场资源，提供了侧重于系统熟悉的额外培训[33]。或者，可以要求ICS-CERT [34]的现场产品进一步尝试弥补这一差距。但是，这些似乎是高级别的，并不包含系统到用户的关系。

限制在本地级别的观点提供的粒度可见性不足，对给定系统的清晰理解，缺少攻击面，以及不仅识别IT与OT，而且识别OT与OT的挑战。由此产生的影响是不完整风险评估的制定。这有可能导致实施无效甚至破坏性的安全控制。

## 4.案例研究

随着现代ICS中日益复杂和面临的挑战，对现有标准和指南的依赖可能无法提供足够的建议来确保所需的系统安全性和弹性水平。虽然详细描述了风险评估方法和安全控制，但有关理解系统的建议可能不足。

为了更好地理解ICS中系统和用户之间的关系和互连，并与欧洲公用事业公司合作进行了以下案例研究。最初专注于不同抽象层次的端到端系统到系统关系，图4已被创建为概念可视化工具，汇总来自多个来源的信息（网络架构评论，配置评审，访谈等） 。从这个系统到系统的基线，系统到用户的关系被覆盖，从而呈现出系统的整体视图或“理解”，超出了审查标准和指南所描述的方法。

### 4.1数据流图

图4显示了从单个传感器到驻留在ICS最高级别（级别5）内的远程访问连接的数据流。每个设备（PLC，RTU，Historian等）和子组件（存储器位置，接口，功能等）由方形或圆形节点描绘。循环节点表示通过接口的过程数据的用户交互/可见性。具有虚线边的方形节点表示应用于数据流（即数据处理点）的函数。为了突出设备配置，系统到系统和系统到用户交互的复杂性，PLC（黑色虚线内的节点）已经在较低的抽象层次上呈现，显示了逻辑上的子组件。

这种增加的粒度级别允许理解关键功能和存储器寻址，应用于一个信号的计算处理。此外，RTU和Historian（DB2）用于监视功能的数据与PLC控制逻辑和HMI /工作站（DB1）中使用的过程控制功能的分离表明了设备内的职责和用户访问的明确分离。
 
 ![13-4](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/13-4.png)
 

图4中的每个节点都是彩色编码的，以表示它根据普渡模型驻留的系统级别。但是，正如一些节点（例如\ AI Card Slot 3“）可以看到的那样，应用了两种颜色。这种颜色应用已经被引入，其中设备或子组件被访问和/或受控制/管理系统用户来自多个级别。在本例中，AI（模拟输入）卡代表PLC上的物理接口（PLC子组件）.0级仪表工程师负责为此卡提供传感器，以及1级控制工程师负责在PLC上执行的操作逻辑，因此都需要访问。这种共享访问可能需要进行故障查找和信号质量的二次验证。通过这个例子，并考虑到PLC的安全性，人们可以假设通过共享所有权提供的附加风险很小;但是，如果没有详细的系统到用户意识水平，则无法进行适当的评估。

可以通过应用双向链路来识别关于系统到用户关系的其他细节。例如，在DB1.DBD1和HMI / Workstation之间可以看到一个这样的链接。此通信路径主要用于观察存储在DB1.DBD1中的值，但是在紧急情况下，操作员可以覆盖此值。在传感器发生故障或故障的情况下可能发生这种情况，在进入HMI /工作站界面之前，直接在源处（即，对所讨论的操作过程进行目视检查）进行手动读数。

根据[24]中描述的适当评估技术的指导，使用网络图分析和与支持/维护人员的非正式接触来提供对系统设备的高级理解。这使我们能够通过系统设备和通信链路构建一个总体端到端的数据。应用上述颜色编码，突出显示设备及其在Purdue模型中的位置。对每个级别的人员进行的访谈用于协调对设备的访问要求，从而识别任何共享所有权。如上所述，应用颜色编码以突出共享所有权/要求。在所有后续阶段中，分析针对一个设备，即PLC。缩小范围的目的是识别PLC的子组件，允许更详细的粒度分析。制造区域（图1）网络流量捕获和基本配置审查确定了核心通信接口和内存寻址。额外的改进需要更详细的配置审查（PLC梯形逻辑），与采访制造区域支持/维护人员同时进行。

虽然这里的过程描述呈现出适度线性的方法，但我们发现每个步骤和技术都允许更好地理解在所有步骤中捕获的数据。因此，虽然这些描述的步骤为我们采用的方法提供了基础，但是技术以循环方式应用，在图4中得到的数据流图之前经历了几次迭代分析。探索更复杂的系统到用户关系首先需要了解ICS每个级别的角色组。以下部分探讨了这一点，回到图4和这里提供的整体讨论。

### 4.2系统用户

案例研究中发现了大量不同的角色。这些角色在整个组织中执行了多种功能，从操作流程管理到预算，机械工程和绩效评估。我们首先在现有文献中寻求帮助[31]，这确定了ICS环境中的六个关键角色。这些是初级操作员，高级操作员，主管，技术员，工程师和经理。虽然适用于案例研究，但通过与参与组织进行的互动，我们确定了额外的粒度将证明是非常有益的。
 
![13-5](https://github.com/GrowingGardenia/Information-Security-Paper-Reading/blob/master/picture/13-5.png)
 
 
首先，我们以前的工作[18]中讨论的核心角色功能和系统级别的基线分离，为进一步讨论奠定了基础。因此，通过案例研究突出显示的角色组已分为两类，即“操作员”和“支持/维护”。运营商组可以包括对运营站点和控制室的物理访问，但系统访问不包括修改设备/系统配置的能力。支持/维护小组还可以包括对运营站点，控制室和数据中心的物理访问;但是，此角色类别包括修改设备/系统配置的功能。表1总结了我们的案例研究结果，确定了关键角色组及其运作的ICS水平。通过本案例研究提供的角色组视图显着增加了粒度，特别是在与系统级别相关时。基于表1，我们可以开始分析图4中的节点，覆盖角色信息，并了解通过先前未考虑的系统到用户关系引起的挑战。

值得注意的是，表1中列出的角色和权限不是静态的。大型与小型ICS，子角色以及责任随时间变化的角色群体的多样性都增加了角色动态。例如，工作经验/实习，学徒计划，重组等的参与都会影响系统到用户的动态，即使是在短期内也是如此。此外，某些已定义的组中存在资历等级。例如，在某些工程角色中，初级工程师（通常称为“技术人员”）与完全合格的工程师相比执行有限的任务，高级工程师可以执行其他任务，或者作为工程师和初级工程师的知识库/资源。

为了进一步强调角色识别和系统级映射的重要性，通过案例研究讨论了便携式设备使用的一个例子。仪表工程师在0级内执行任务，不仅将笔记本电脑连接到不同级别的OT网络，还连接到公司IT网络。历史上采用了双笔记本电脑方法（使用专用工业和通用笔记本电脑）。但是，合并被认为适合于节省成本和便于持续的设备管理。与设备在OT和IT网络之间移动相关的风险至少在第一印象上看起来很重要，安全控制有效地限制了IT和OT之间的数据流。然而，在通过这种便携式设备使用方法可能会或可能不会增加风险等级的情况下，与上述模拟输入卡示例一样，如果不清楚地理解系统到用户的关系，则不能进行适当的评估。

### 4.3讨论

考虑前面讨论的单个传感器输入要求（调节器，性能分析器，远程报警管理等），图4和表1中的相关角色组，提供了一个平台，可以对数据流和关键数据处理进行进一步分析可以识别和评估积分。在前面的示例中，我们使用DMZ历史数据库服务器工程师讨论了每个节点的多个角色问题。历史学家负责从远程现场站点收集数据，执行复杂的计算功能，并为用户提供各种分析框架中使用的数据（性能分析，法规要求等）。

在图4中，PLC逻辑（MD104）中的临时标记存储器地址分为两个离散数据块，一个用于现场控制逻辑和工作站交互，另一个用于现场监控和报警管理，其中涉及多个系统和用户直接支持/利用地方一级的数据（级别1,2和3）。讨论的系统故障类型与级别1控制工程师（负责过程逻辑）修改功能或在此数据拆分之前寻址有关。由于他们与PLC交互的范围主要集中在流程操作上，因此很少考虑/理解其他系统和用户需求。结果，虽然修改了驻留在过程操作中的所有控制逻辑/寻址以进一步反应链中的变化，但是其他逻辑/寻址没有，导致历史服务器内的计算和值的损坏。

通常发现此处讨论的操作数据中的错误的方式进一步突出了角色和设备映射的重要性。此数据的最终用户突出显示指定日期和时间后的值偏差，这是一种有点被动的方法。从最初对虚假数据的怀疑，基本上是数据质量问题，历史学家支持工程师将深入研究复杂的数学计算以找到根本原因。如果计算来自多达30多个操作标签（信号输入），则此过程可能会耗费时间。此外，如果在系统中的多个点处理数据，如图4所示，对高级访问权限的要求变得明显，并且数据的可见性在多色节点处结束（PLC寻址），与Level的交互需要1名控制工程师更好地了解下游的任何变化。

另外，关于在转移到数据块（DB）之前使用标记存储器位置（MD），这可以被认为是不良的PLC编码选择。考虑到设备的使用年限，标记存储器的大小可能受到限制，在设备断电时提供有限的值保留能力，并增加PLC逻辑复杂性。更清晰的选择是将此值直接移动到主过程控制和本地监视数据块（DB1）中，然后如果RTU和Historian需要，则将此值直接从DB1传递到DB2。由PLC逻辑生成的派生值（例如，将两个传感器值输入到计算中的新值）已经从DB1传递到DB2，因此在此函数中包含传感器值将是更合乎逻辑且更清晰的方法，伴随着通过数据块使用提供的额外好处。

所进行的案例研究已被用于突出ICS内部互连设备的技术复杂性，以及PLC的复杂配置/逻辑，包括基于操作目标的数据分离。由此可见，角色组的重叠表明了操作和维护此类系统的个人的数量和多样性。总体而言，案例研究已经证明了解决安全问题的挑战，并且可能无法通过纯技术手段（防火墙，IPS等）解决安全问题。无论是评估指标还是安全控制，都必须从社会技术（人力和系统）的角度来解决挑战，将每个级别的核心运营目标和角色纳入评估，规划和缓解策略。

基于适当的综合风险评估输出，通过图4应用到安全控制实现所提供的粒度级别允许统一数据可靠性和安全性。这是通过考虑系统到系统和系统到用户的交互和要求来定制安全控制来实现的。例如，在较低级别，可以实现控制系统和用户与指定PLC存储器位置的交互的防火墙规则的部署，而不用担心OT系统之间的系统性能下降，解决OT与OT关注点，OT与IT系统之间的关系，解决OT与IT有关。

## 5.结论和未来的工作

由审查的标准和准则定义的风险评估和安全控制选择的现有方法提供了一个良好的起点。但是，通过更好地了解端到端的系统到系统和系统到用户的交互，可以增强此类评估的初始阶段和持续的支持。从风险角度来看，我们强调只需获取设备清单和网络架构就不足以全面映射ICS环境中的风险。需要了解角色和设备之间的关系，以及可能的角色和设备子组件参数，以制定风险缓解策略。虽然下一代ICS安全控制设备的发展试图在网络流量上提供精细的规则集[13]，但是对于获得对数据流和相关利益相关者的清晰理解的指导是有限的。与我们的工具配合使用，可以实现安全产品强制执行的控制策略和流量限制的粒度制定的反馈循环。

如果之前描述的评估工具[35]缺乏获得系统到系统和系统到用户知识的指导，我们认为我们的工具/方法可以作为先决条件。以这种方式应用会使评估人员超越当前的现场ICS-CERT产品，这有助于识别高级（端点到端点）数据，并排除系统利益相关者[34]。这种对系统到系统和系统到用户关系的理解/熟悉的增加将允许生成更详细，准确的评估结果。为了进一步验证这一说法，我们将寻求与现实世界设施的风险评估人员和安全从业人员合作，同时利用兰卡斯特[28,17]和新加坡（安全水处理（SWaT））[25]试验台环境。这将涉及风险评估和控制实施的评估，在使用我们提议的工具之前应用现有的方法来“理解系统”。

### 5.1未来工作

由于我们还没有提供一种方法，通过这种方法，其他人可以在自己的环境中有效地获得粒度数据，这将是我们未来工作的核心焦点。这种方法将伴随着在创建数据流，处理和用户交互地图时必须遵守的参数框架。除此之外，还将探索数据捕获工具和技术的集成，以协助该过程。

正式方法的开发旨在确保我们工具的实际可扩展性。对方法开销的集中管理在实现这一目标方面发挥着重要作用。这可以通过使用被动网络分析工具[13] [38]和持续的行业参与来得到帮助。还将使用信号优先排序的详细信息技术，缩小可用于进行综合分析的资源不足的范围。通过与行业的持续讨论，我们认为RTU关键性量表可以用作指标。我们与行业的合作表明，大规模制造区域可以只有几十个最高关键性的信号，为粒度数据流程，处理和用户交互映射提供了一个起点。

更进一步，我们将探索关注系统到系统交互的时间常数和相关数据处理点关键性（负面影响的时间）的参数范围，从根本上帮助设备配置要求的制定。 “理解系统”的范围增加“将提供更多粒度，为风险评估和安全控制实现设备要求/目标的高度详细可见性。

提高对数据流的可见性，同时理解数据处理点和数据消费关系，将对于法医调查至关重要。作为起点，我们将探讨在确定受感染设备（未经授权的数据发生变化），估计攻击来源（通过分析相互依赖性）以及识别受到攻击时使用的建议工具。用户凭据。

## 6. REFERENCES
[1] A. Bolshev, J. Larsen, M. Krotol, and R. Whitmann.
A rising tide: Design exploits in industrial control
systems. In 10th USENIX Workshop on Oensive
Technologies (WOOT 16), Aug. 2016.

[2] British Standards Institute. Information technology -
Security techniques - Code of Practice for Information
Security Management. 2005.

[3] British Standards Institute. BS ISO/IEC 31010 - Risk
management - Risk Assessment Techniques. 2010.

[4] British Standards Institute. BS ISO/IEC 27001 -
Information Technology - Security Techniques -
Information Security Management Systems -
Requirements. 2013.

[5] British Standards Institute. BS ISO/IEC 27002 -
Information Technology - Security Techniques - Code
of Practice for Information Security Controls. 2013.

[6] British Standards Institute. BS ISO/IEC 27019:2013 -
Security Techniques - Information Security
Management Guidelines Based On ISO/IEC 27002 for
Process Control Systems Specic to Utility Industry.
2013.
100

[7] P. Carson. The IT vs. OT debate j Intelligent Utility.
Intelligent Utility Magazine, pages 32{34, 2010.

[8] Centre for the Protection of National Infrastructure.
Cyber Security.
http://www.cpni.gov.uk/advice/cyber/. Retrieved:
December, 2015.

[9] Centre for the Protection of National Infrastructure.
Risk Assessment.
http://www.cpni.gov.uk/Security-Planning/
Business-continuity-plan/Risk-assessment/. Retrieved:
December, 2015.

[10] Centre for the Protection of National Infrastructure.
The National Infrastructure.
http://www.cpni.gov.uk/about/cni/, 2014. Retrieved:
January, 2016.

[11] Centre for the Protection of National Infrastructure.
Security for Industrial Control Systems: Manage the
Business Risk (a good practice guide). 2015.

[12] Centre for the Protection of National Infrastructure.
Select and Implement Security Improvements. 2015.

[13] Check Point Software Technologies. Critical
Infrastructure & ICS/SCADA.
https://www.checkpoint.com/products-solutions/
critical-infrastructure/, 2016. Retrieved: July, 2016.

[14] Council on Cyber Security. The Critical Security
Controls for Eective Cyber Defense. 2014.

[15] DEFRA. Waste Water Treatment in the United
Kingdom. http://tinyurl.com/nhkhhyb, 2012.
Retrieved: June, 2015.

[16] P. Didier, F. Macias, J. Harstad, R. Antholine,
A. Johnston, S, S. Piyecsky, M. Schillace, G. Wilcox,
D. Zaniewski, and S. Zuponcic. Converged Plantwide
Ethernet (CPwE) Design and Implementation Guide.
CISCO Systems and Rockwell Automation, 2011.

[17] B. Green, D. Hutchison, S. A. F. Frey, and A. Rashid.
Testbed Diversity as a Fundamental Principle for
Eective ICS Security Research. In International
Workshop on Security and Resilience of
Cyber-Physical Infrastructures, pages 1{8, 2016.

[18] B. Green, D. Prince, U. Roedig, J. Busby, and
D. Hutchison. Socio-Technical Security Analysis of
Industrial Control Systems (ICS). In 2nd International
Symposium for ICS & SCADA Cyber Security
Research(ICS-CSR), 2014.

[19] E. Humphreys. Information Security Management
Standards: Compliance, Governance and Risk
Management. Information Security Technical Report,
13(4):247{255, 2008.

[20] Joint Task Force Transformation Initiative. Guide for
Conducting Risk Assessments. NIST Publication,
2012.

[21] Joint Task Force Transformation Initiative. Security
and Privacy Controls for Federal Information Systems
and Organizations Security and Privacy Controls for
Federal Information Systems and Organizations. NIST
Special Publication, 2013.

[22] A. Jones and D. Ashenden. Risk Managment for
Computer Security - Protecting Your Network and
Information Assets. Elsevier, 2005.

[23] Kaspersky Lab. ICS Vulnerabilities Statistics 2015.
http://tinyurl.com/jh4658o, 2015. Retrieved: June,
2015.

[24] W. Knowles, J. M. Such, A. Gouglidis, G. Misra, and
A. Rashid. Assurance Techniques for Industrial
Control Systems (ICS). In Proceedings of the First
ACM Workshop on Cyber-Physical Systems-Security
and/or PrivaCy, pages 101{112. ACM, 2015.

[25] A. P. Mathur and N. O. Tippenhauer. Swat: a water
treatment testbed for research and training on ics
security. In 2016 International Workshop on
Cyber-physical Systems for Smart Water Networks
(CySWater), pages 31{36, April 2016.

[26] National Institute of Standards and Technology. FIPS
PUB 199: Standards for Security Categorization of
Federal Information and Information Systems. 2004.

[27] Norwegian Oil and Gas Association. 110 -
Recommended Guidelines for Implementation of
Information Security in Process Control, Safety and
Support ICT Systems During the Engineering,
Procurement and Commissioning Phases. Technical
report, 2008.

[28] B. Paske, B. Green, D. Prince, and D. Hutchison.
Design and Construction of an Industrial Control
System Testbed. In PGNET, pages 151{156, 2014.

[29] R. Ross. Managing enterprise security risk with NIST
standards. Computer, 40(8):88{91, 2007.

[30] T. Sauter, S. Soucek, W. Kastner, and D. Dietrich.
The Evolution of Factory and Building Automation.
IEEE Industrial Electronics Magazine, 5(3):35{48,
Sept 2011.

[31] R. Singla and A. Khosla. Intelligent Security System
for HMI in SCADA Applications. International
Journal of Modeling and Optimization, 2(4):444{448,
2012.

[32] K. Stouer, S. Lightman, V. Pillitteri, M. Abrams,
and A. Hahn. Guide to Industrial Control Systems
(ICS) Security. NIST Special Publication, 2015.

[33] U.S. Department of Homeland Security. Assessment
Program Overview.
https://ics-cert.us-cert.gov/Assessments, 2016.
Retrieved: September, 2016.

[34] U.S. Department of Homeland Security. Control
Systems Architecture Analysis Services.
http://tinyurl.com/gnr4g5g, 2016. Retrieved:
September, 2016.

[35] U.S. Department of Homeland Security. Cyber
Resilience Review & Cyber Security Evaluation Tool.
http://tinyurl.com/jqes9te, 2016. Retrieved:
September, 2016.

[36] J. M. Weiss. Presentation on how to hack a chemical
plant and its implication to actual issues at a nuclear
plant. http://tinyurl.com/jr985ru, 2015. Retrieved:
January, 2016.

[37] M. Whitman and H. Mattord. Principles of
information security. Cengage Learning, Boston, 4
edition, 2011.

[38] Wireshark.org. About Wireshark.
https://www.wireshark.org/, 2016. Retrieved: July,
2016.


