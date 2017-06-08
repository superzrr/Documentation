#EOS.IO技术白皮书

**草稿: 2017/6/5**

**概要:** EOS.IO软件引进了一个新的区块链架构,用来设计增强去中心化应用的垂直和水平扩容.通过创建一种类似于操作系统, 程序可在其上构建.软件提供帐户 认证 数据库 异步通讯和跨数以百计的CPU核心或者集群的计划.最终的技术是一种区块链架构,可以拓展到每秒处理百万级事务,降低用户费用,允许快速和简单的去中心化应用的部署.

版权归属 @ 2017 block.one

无需授权, 在非商业用途或为教育目的,使用人可以使用\重生或分发本白皮书的所有内容(而非用于收费或商业用途) 引用时请注明出处和版权.

**声明:** 本EOS.IO草案技术白皮书只用于信息目的, block.one不保证本白皮书结论精准无误. 在任何情况下,本白皮书内容只可以原样提供, 不作任何跟作品有关的任何表述或担保,明示或暗示.不表述不担保的情况包括且不限于以下内容:(i) 商用性 适用于某些目的 不侵权(ii) 本白皮书的内容无差错 不适用任何目的(iii) 此内容不侵犯第三方权力.否认所有担保.对本白皮书的任何不恰当使用\引用或对任何信息的引申,如造成损害,block.com及录属机构不负有任何责任.即使有被提醒此类损害的可能性.
任何情况下, 因此白皮书所引起的任何直接的\间接的\特殊的\继发的损害,block.one及其所属机构不向任何个人\公司负责.


#背景

区块链技术在2008年伴随着比特币而为人所知,从此,公司和开发者们一直致力推广该技术,希望能在一个单独的区块链平台上支持更多的应用.

然而大量的区块链平台激烈竞争,以支持各种功能的去中心应用,特定区块链应用,比如BitShares去中心交易(2014) Steem社会媒体平台(2016)对区块链的使用越来越重,日活用户数以万计, 为此,上述应用已将性能提升到每秒支持数千笔交易,并将等待时间降低至1.5秒,消除费用,将用户体验提升至与当前已有去中心化服务相当的水平.

现有的区块链平台承担着大量的费用和有限的计算容量,这些都将限制区块链的广泛使用.

#区块链应用必备条件

为了能广泛应用,基于区块链的应用所需的平台要有足够的灵活性,并满足以下需求:

##能支持百万级用户

类似于Ebay Uber AirBnb这样的分布式商业应用需要的区块链技术可以满足千万级日活用户的处理.在特定情况下,有些应用只会在达到海量用户的时候才开启工作,因而,处理海量用户是平台最重要的能力之一.

##免费使用

应用开发者通常希望可以给用户提供免费服务.不是所有用户都需要付费,或者可以通过服务创收.能向用户提供免费服务的区块链平台会赢得更多应用的青睐.这样,开发者和商业才能提供更有效率的货币策略.

##易于升级及BUG修复

创建基于应用的区块链商业需要有灵活性,通过新的功能特性来强化他们的应用.
不管怎样的应用都会有bug,即使测试验证时使用了最严格的手段,平台要够强大,当bug发生时可以及时修复.

##低等待时间

好的用户体验等待时间一般不能超过数秒就需要得到应用的反馈. 如果等待时间越长,用户体验就越糟糕,这时区块链应用与非区块链上同类应用的相对优势就会荡然无存.

##序列性能

有一些应用因为序列依赖步骤(Sequentially dependent steps),就是无法用并行算法实现.比如交易类应用需要有足够的序列性能来处理高容量, 因此有快速的序列性能也是平台所必需的.

##并发性能

大规模应用需要利用多个CPU和计算机实现负载均衡

##一致意见算法(DPOS)

EOS.IO software utilizes the only decentralized consensus algorithm capable of meeting the performance requirements of applications on the blockchain, [Delegated Proof of Stake (DPOS)](https://steemit.com/dpos/@dantheman/dpos-consensus-algorithm-this-missing-white-paper). Under this algorithm, those who hold tokens on a blockchain may select block producers through a continuous approval voting system and anyone may choose to participate in block production and will be given an opportunity to produce blocks proportional to the total votes they have received relative to all other producers. For private blockchains the management will use the tokens to add and remove IT staff.


The EOS.IO software enables blocks to be produced exactly every 3 seconds and exactly one producer is authorized to produce a block at any given point in time. If the block is not produced at the scheduled time then the block for that time slot is skipped.  When one or more blocks are skipped, there is a 6 or more second gap in the blockchain.

Using the EOS.IO software blocks are produced in rounds of 21. At the start of each round 21 unique block producers are chosen. The top 20 by total approval are automatically chosen every round and the last producer is chosen proportional to their number of votes relative to other producers. The selected producers are shuffled using a pseudorandom number derived from the block time.  This shuffling is done to ensure that all producers maintain balanced connectivity to all other producers.

If a producer misses a block and has not produced any block within the last 24 hours they are removed from consideration until they notify the blockchain of their intention to start producing blocks again. This ensures the network operates smoothly by minimizing the number of blocks missed by not scheduling those who are proven to be unreliable.

Under normal conditions a DPOS blockchain does not experience any forks because the block producers cooperate to produce blocks rather than compete.  In the event there is a fork, consensus will automatically switch to the longest chain. This metric works because the rate at which blocks are added to a blockchain chain fork is directly correlated to the percentage of block producers that share the same consensus. In other words, a blockchain fork with more producers on it will grow in length faster than one with fewer producers.  Furthermore, no block producer should be producing blocks on two forks at the same time. If a block producer is caught doing this then such block producer will likely be voted out. Cryptographic evidence of such double-production may also be used to automatically remove abusers.

    事务确认
    事务证据桩(Transaction as Proof of Stake)
帐户
    信息和顾问
    基于许可管理的角色
        命名的许可级别
        命名的消息顾问群组
        许可映射
        许可评估
            缺省许可群组
            并发的许可评估
    使用强制延迟的信息
    被偷key的恢复

#应用确定化的并发执行
    沟通等待时间最小化
    只能读的信息顾问
    多帐号的原子化事务
    区块链状态的局部评估
    主观的最佳效果规划
#令牌模式和资源使用
    主客观的测量方法
    收件人付费
    委托性能
    事务成本和令牌价值分离
    状态存储成本
    区块回报
    社区收益应用
#统治
    帐户冻结
    改变帐户代码
    章程
    协议&章程的升级
        应急变化
#脚本&虚拟机
    已定义的消息结构
    已定义的数据库结构
    认证与应用相分离
    虚拟机独立的架构
        网络组装
        以太坊虚拟机(EVM)    
#内部区块链沟通
    轻客户端认可的Merkle证据
    内部链沟通的等待时间
    完整性证据
#结论
