# raft-study
#### 分布式协议raft

1. raft 动画演示: http://thesecretlivesofdata.com/raft  
   一个解释比较好的网站: http://www.jdon.com/artichect/raft.html

2. CAP: C 一致性, A 可用性, P 容错性. 只能三选二,并不能保证全部,需要更具场景进行取舍.

3. raft 协议重要的角色:  
Leader: 领导者  
Candidate: 侯选者  
Follower: 跟随者(平民)  

4. raft协议中重要的超时机制.  
Election timeout: 每次的都需要在150 ~ 300 ms之间随机的生成一个随机数,作为超时设置数. 这个很重要,注意是"每次,随机",这些词汇.  
Heartbeat timeout: 心跳检测.

5. votes > N/2 + 1, vote of itself  
N/2 +1 就超过半数，代表大多数了

#### 问题清单
* 一个节点怎么成为一个candidate?  
引用某个游戏公司有关一个游戏的开篇话,"开局,都是平民", 即,初始时,所有的节点都是follower,根据Election timeout,而这个超时,每一个节点都是在150 ~ 300ms之间,随机生成的,所以超时值都不一样,因此总有一个节点成为Candidate, 发出邀请,让其它节点投自己,已经投过票的节点,不允许再投票.

* 一个candidate怎么成为一个leader?  
一个candidate搜集足够的votes >( N/2 + 1) 就成为当前的leader,

* candidate出现僵局怎么办?怎么打破?  
出现两个candidate,超时追加赛的方式,直至新生成一个candidate.

* 节点共识不一致怎么办?  
回滚

* 通信交互实现?  
commit ok  
ack机制  


#### 相关词汇
splite view:candidate出现僵局,所出现的状态  

view:类似现实生活中的领导选举一样,产生新领导时,生成新的一个世界格局,状态,成为一个视图  



