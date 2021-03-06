# Motion Primitives-based Path Planning for Fast and Agile Exploration using Aerial Robots

基于运动基元的路径规划，用于使用空中机器人进行快速敏捷的探索


## 摘要

本文提出了一种新的路径规划策略，用于使用空中机器人进行快速，敏捷的探索。 尽管微型航空器的耐用性有限，但为满足挑战性和密闭环境的大规模探索的综合需求，拟议的规划师使用运动原语来识别可搜索的路径，以搜索配置空间，同时利用小型航空器的动态飞行特性 机器人。 利用有效的环境体积表示法，规划器提供了无碰撞且未来安全的快速路径，可最大化预期的勘探收益并确保在未知环境中连续快速导航。 新方法已在与地下勘探有关的一系列部署中进行了现场验证，特别是在内华达州北部的现代和废弃地下矿井中，使用了一个0.55m宽的耐碰撞飞行机器人进行勘探，速度高达2m / s 导航段的宽度小至0.8m。

---

## 引言

自主机器人探索和绘制未知环境的研究正在扩展到越来越多的应用领域。 推进机器人可以用作探险家的前沿[1-4]，第一反应[5,6]和检查员[7,8]，特别是空中车辆，目前被用于许多民用和军事应用。 然而，尽管在该领域取得了前所未有的进展，并提出了各种各样的勘探路径规划方法[9-17]，但正如实验所证明的那样，目前自主勘探的最新技术仅限于相当低速的保守任务，因为机器人试图保证安全导航和同时优化选择后续勘探移动，因为它们具有实时机载定位和绘图能力。 然而，低速探索不允许充分利用小型飞行机器人的敏捷性，并禁止大规模探索，因为它们的电池寿命有限。

出于上述原因，这项工作提出了一种基于运动原语的探索路径规划器（MBPlanner），该规划器提供了特别适合于空中机器人系统的快速灵活的路径。 通过依靠基于运动原语的随机搜索策略，该新方法固有地对飞行器的动力学进行了计算，因此可以在自主探测任务期间实现敏捷的动态轨迹。 另外，与大多数现有方法（包括作者的先前工作[13，15-17]）相比，考虑的可允许路径在每个选定路径的最后一个顶点都不假设悬停条件（零速度），相反， 考虑可以以任何最终速度结尾的路径，只要可以识别出减速和停止动作，如果需要，可以在将来使机器人达到安全的无碰撞配置。 因此，采样路径针对敏捷性导航进行了优化，因此有潜力最大化机器人系统的探索时间，特别是对于受其机载电池限制的微型飞行器（MAV）。 然后，仅在未知区域的边界范围内，针对每个候选允许路径评估其勘探增益，并选择并执行针对安全性进行了优化的最佳解决方案，同时重复整个过程。 为了进一步支持快速灵活的探索过程，将贡献的计划方法与在线体积表示方法[18]结合在一起，该方法固有地提供了欧几里得符号距离场计算，因此有助于快速评估每个候选者的无碰撞特性 边缘。

通过实验评估了所提出的快速灵活的勘探路径规划方法，重点是可以同时具有非常大的规模和非常狭窄的地下环境，因此需要有效的勘探和敏捷机动。 更具体地说，现场测试结果来自内华达州北部的一系列地下矿山环境。 将这项研究与新颖的耐碰撞空中机器人设计相结合，我们在受限的环境中推动了快速，敏捷探索的前沿。 实际上，在评估所有可能的加速路径后，即使是“万不得已的安全性”这一非常严格的约束条件，也可以在某个实验中放宽，从而可以了解在狭窄环境中自主飞行机器人的探索和制图的局限性。


本文的其余部分安排如下。


第二节概述了相关工作，第三节概述了问题。 第四节详细介绍了拟议的方法。 第五节详细介绍了评估研究，随后在第六节中得出了结论。

---

## 相关工作

机器人在未知环境中的探索吸引了研究界的兴趣，多年来，人们提出了许多针对探索路径规划问题的方法[9-12]。 历史上已经通过基于边界的方法来解决未知空间的体积挖掘问题[10]，其中路径规划算法的目标是主动引导机器人向其传感器范围的边界发展。 同样，也采用了基于采样的方法，其目的是对环境的“最佳视图” [9，13]进行采样，以最大程度地了解未知空间。 在这一领域，最近的努力集中在多目标计划[14-16]，其中计划的路径同时或以级联方式针对多个目标进行了优化。 着重于大规模探索，[17]中的工作提出了一种基于图的本地搜索，并结合了全局重新规划架构，以将机器人重新定位为先前在大规模地下拓扑中发现的边界。 同样，还提出了涉及多个机器人团队进行探索的路径规划范式[19，20]。 然而，尽管已经通过多种技术解决了未知环境中机器人探索的一般性问题，但当前的最新技术尚未提出促进敏捷和快速部署的方法和系统，特别是在 大规模和狭窄的环境，这一事实与快速自主飞行的已知进展相矛盾[21-23]。 出于上述原因，并意识到以下事实：特别是对于微型飞行器，在电池有限的情况下，探索的速度直接转化为探索的深度，在这项工作中，我们强调敏捷路径规划策略，以便在大型和窄型同时进行快速探索 环境。 作为理想的现场验证活动，我们在地下勘探和制图的背景下演示了这项工作，其中机器人完全自主运行，无需任何人工干预。


---





---