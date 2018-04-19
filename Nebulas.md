# Nebulas

Nebulas，基于价值尺度的区块链操作系统及搜索引擎。

### 背景：

当前区块链，一方面无法满足大规模商业应用的扩容性，另外一方面存在价值尺度缺失，各个区块链项目五花八门，技术角度不一，吸引人群有差异，宣传力度也不一致，没有一个统一的价值尺度来衡量这些区块链项目。

### 星云链的目标

- 建立一个适用于所有开发者并且被不断完善的区块链操作系统。
- 基于这样一个区块链操作系统汇聚大量的智能合约程序，为有区块链技术需求的用户提供搜索服务。其中Nebulas制定诸多机制，保证其自主升级和完善。

主要内容包含：

- 定义价值尺度的星云指数 Nebulas Rank(NR)，通过综合考虑链中各个账户的流动性及传播性，如果这个NR真做起来了，那么就像淘宝刷单一样，如何防止作弊？
- 支持核心协议和智能合约链上升级的星云原力 Nebulas Force（NF），帮助星云链自身及其身上的应用实现自我进化，动态适应社区或市场变化，开发者通过星云链构建更丰富的应用，并进行快速迭代。如果Nebulas不仅仅做一个区块链的搜索引擎，还要做一个公链平台，那要重点放在共识算法上。如果底层的共识算法不安全，TPS做不上去，帮助开发者那是扯淡了。
- 开发者激励协议 Developer Incentive Protocol（DIP），就是用自己的财政支持优秀开发者咯，其实只要你公链足够优秀，开发者自然会跟公链相互促进的。
- 贡献度证明共识算法Proof of Devotion（PoD），快速，不可逆和公平性，不知道PoD为何物。
- 去中心化应用的搜索引擎，这个要看这个引擎是中心化的还是去中心化的，如果是中心化的，那么已有的引擎再次开发难度不大。如果是像智能合约一样，去中心化的实现了搜索引擎的整个算法，那这点确实不错。

### 星云链设计原则

- 公正的排名算法

NR确实有比较大的商业潜力，但如何对抗人性中的弱点才是亮点。如果搞出一个不错的指数，但抵不住人性的恶，分分钟被作弊薅羊毛了，这个指数有还不如没有。

- 区块链系统及应用的自我进化

将星云链上的应用简单理解成智能合约，这些智能合约是链上数据的一部分，通过链上数据的追加实现基础协议的升级。这个说法很有问题，升级智能合约是大家都想的，但如何达成共识来升级呢？星云链通过在智能合约底层存储支持状态变量可跨合约访问的设计，完成智能合约的升级，这一句感觉有点玄乎呢？

- 生态系统

PoD算法，利用NR的价值尺度评估出对生态贡献度较高的账户，平等赋予记账资格。如果NR是可以人为参与影响，那么遏制记账权被垄断就很难说得过去。


### Nebulas Rank

NR是其他算法的基础部分，三重价值尺度：

- 流动性
 交易的频次和规模，这个就完全可以造假

- 传播性
 资产流动的广度和深度，也完全可以造假
 
- 互操作性
 信息间的互操作，具体这些操作是什么？

其实说了这么多，就是按照对每个帐号地址进行统一价值尺度的图计算处理。然而现在的图计算是中心化的计算，基本都是采用分布式计算，比如Spark来计算，这个NR的计算难道也要用贵公司的服务器来跑？

#### 抵抗作弊

作弊手法：

- 环形记账
- 提高出度
- 搞群控
- 蹭热点

NR弱化作弊的机制：

- 滑动时间窗T，就是看你表现不是一两条，短期内作弊效果不明显呗，长期作弊的好处也相对长期有效
- 环形攻击，就你们几个瘪三在那转来转去，当然可以让其边的强度信息降低
- 算法还考虑“币龄”，可以拖慢作弊者的交易速度，但也是说只要有耐心作弊，效果更好
- 为了获得最大的“激励值”，账户需要在当前周期内转出金额多于收入，或者只转出少于收入一半的金额，就是说要么账户资产流出，要么资产流入，怎么就会搞群控的时候，出现什么账户的储蓄效应呢？
- 取最大弱联通分支，伪造的独立分支会被视为噪声而过滤清除。就是说那些搞群控的都是二傻，搞一些没有“人脉“的节点给自己做独立分支，恐怕那些搞群控的就会钻你这个空子，让自己的节点比那些真正的中心节点更加显得中心。
- 蹭热点，对低入度的节点评分偏向“保守”，就是说你从交易平台这样的中心节点，取点小钱，人家没把你放在眼里。但人家既然搞作弊，当然要真刀真枪干啊，蹭热点又不是说不花成本。


这个NR说这么多，就是简单考量地址的热度，这个跟整个项目的热度也不是绝对的对应关系。比特币转账成本这么高，让它在钱包里呆着好了，或者直接在交易平台呆着好了，但其他交易费低的就不是这样。要用一个统一的数值来衡量所有的项目，难度还是很大。至少这个NR设计看不出有这个能力。

这些基础的疑问，如果Nebulas不出来解答，白皮书下面部分是没必要看了。


OK，星云链团队第一时间给出了他们的答案，对团队效率表示赞赏。


""""""""""""""""""""""""start""""""""""""""""""""""""

Thanks for your comments. Let's focus on your questions about Nebulas Rank.

- Simple answer

	Cheating could be mitigated by mechanism design.

​

- More details(tr;dl)

	- With regards to the computation of nebulas rank, it is designed to be allowed to run on every full node, which will produce the same output, given the agreed block chain data as the input. So if any node is not willing to compute the rank itself, it could fetch the data from somewhere else, as the rank value could be verified at any time.
 	- About cheating on ranking, it is also the main concern of Nebulas Rank.
		- First, from the prospective of incentive mechanism, Nebulas Rank is some kind of better metric than the "stake" for POS. The intuition is that POS encourages agents to own more token but not to spend any. But in order to encourage the system to develop, the owner of account should have the ability to create more liquidity, etc.(we could call it contribution). So a ranking algorithm should care about the local information of a node, such as 1-hop one, i.e. degree centrality, and \inf-hop one, i.e. centrality of page rank family.
		- Second, unfortunately, degree centrality is not hard to improve in transaction network. So the "unforgeable power", i.e. stake, of an account should also be considered by ranking algorithm. In my personal opinion, in the worse case with all accounts try hard to transfer to each other and acts "normally", the ranking based incentive mechanism would be no worse than POS. So it is safe enough as long as POS-based consensus is safe. For example, by incorporating coinage factor, a wealthy and active account might earn "slow money" by Nebulas Ranks, but a wealthy and lazy account could earn quick money. However, a wealthy and lazy account should be ranked low by NR. [0,2,5 pt in your last argument paragraph]
		-Third, with the above two points, the ranking algorithm faces a trade-off between stake and contribution. The main promise is, to raise its rank, an adversary must hold quite an amount of wealth in the system, and it must be influential enough and the benefit of cheating should bounded by a concave function. Besides that, more processing method makes it harder to cheat. For example, by encouragement function, an adversary has to preserve half of the income in the account each time, which reducee its influence exponentially. [3 pt in your last argument paragraph]
		- As for other preprocessing methods, they could also mitigate some common cheating effect. Of course, it is not the main reason that NR could resist cheating. However, they are simple but effective according to the Ethereum transaction network analysis. [1, 4 pt in your last argument paragraph]
		- The last but most important point, we are working on a better version of NR, using cooperative game theory. With the new design, all concern above should be resolve by more rigorous theorem. Sybil attack on ranking could be mitigated by the mechanism itself. Let's release more detail after peer review. And you are welcome to contribute to it :)
		- By the way, cheating, or shua dan, is believed to be well resolved by mechanism design. For example, you could refer to recsys'16 .

""""""""""""""""""""""""over""""""""""""""""""""""""

- 首先回答了计算不是中心化计算，而是每个节点都参与计算，输入是给定的链上块数据，输出是统一的输出，如果有哪个节点不想计算，也可以自己去验证计算。既然说到计算，当然还是有疑问，对于一个区块链项目，有些数据是需要上链的，但是还有很多数据是不上链的，比如一个很大的文件，不方便上链，可能保存在IPFS系统里面，链上只保存这份数据的Hash值，那在你们的计算框架里，只拿到这个hash值，但很明显，这份没有上链的数据的重要程度是没法考据的。总之意思是没有上链的数据也是区块链项目的衡量价值尺度之一，如果只考量上链数据，只是工程上可行性比较大，而在算法设计上偷懒了。

- 然后围绕如何防作弊展开讨论Nebulas Rank

	- 站在PoS角度，只要持有，就有代表权或者投票权，这样你可以批评这些节点没有让所持有的代币（财富）流动起来发挥其价值，NR需要考量其流动性。但这也要从哪个角度去看问题，罗马元老院的元老们握有大量财富，也拥有所有的投票权，你可以轻易批评这些世袭的老家伙们没有让财富发挥流动性价值，但如果在我看来，正是因为有元老院才防止了无数的凯撒想当皇帝，元老院就是帝国的稳定器，其价值是毋庸置疑的。说这么多，就是想反驳你的立论：为了鼓励系统发展，拥有者应该去创造流动性。系统发展是需要流动性，但持币者作出贡献的方式有很多种，长期持有就是最大的支持。
	- "slow money"和"quick money"要如何理解呢？是转账频次快慢，还是地址新旧？感觉还是无法避免作弊。
	- 解释清楚了储蓄效应，如果每次转账不保持一半以上的币，其影响因子在算法里面是指数级下降。这样对于那些搞群控的当然是不利的。在一个整体来看，就无法实现帕累托改进。比如一个帐号想提高自己的NR，拉来一批小帐号，就在那伪造这个帐号的中心效应，如果确实将这个帐号的权重提高了，但其他小帐号的权重降低了，总体来看无法实现帕累托改进。
	- 新版本的算法本身能规避女巫攻击。感觉精妙的算法并不能抵挡住人性的贪婪，这个贪婪包括追求利益，薅羊毛，也包括要搞出一个NR，当然这个算是好的“贪婪”。是否可以引入AI呢？你们创始团队可能有google背景，但可能对google过去的技术有了解，对于page rank的经典算法是非常熟悉的，但现在基于document之间距离的计算，价值尺度的计算，防作弊的深度学习，每一个都是AI的好课题，星云链是计算层，也有自己的EVM之类的，底层存储可以有IPFS，决策层完全可以引入AI技术。


再看看他们团队是如何回复的：


""""""""""""""""""""""""start""""""""""""""""""""""""

- With regards to the data off-blockchain and AI-based rank, it depends... Overall, the metrics for a blockchain system should not be unique: different applications should adopt their own defined ones. Initially, Nebulas Rank is well suited for incentive mechanism, where on-chain data and deterministic algorithm works well enough. In the future, various ranking algorithm, including those incorporating off-chain data and AI-based strategy, should be good to be applied in different scenarios.

- When it comes to which one is better for an economy system: not spending tokens v.s. creating liquidity. Personally I support the latter while the first one is not a bad idea, either. However, of course, this question could be tested by people's practice.

- In the white paper version of ranking algorithm, slowing down is a method to mitigate cheating, not to remove cheating. To prevent cheating, or to mitigate it more, other methods are adopted.

- In the case where one big account gets high rank while others gets low rank seems not bad: the cheater is punished in this case. The concept of Pareto Optimality might not be appropriately used here: the objective of the system is liquidity, etc., not the reward to block committers.

""""""""""""""""""""""""over""""""""""""""""""""""""
