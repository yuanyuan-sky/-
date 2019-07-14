#1.Redis概述
-高性能键值对数据库，支持的键值数据类型：  
1. 字符串(String)

	最大能存储512MB
	set name "runoob"   键为name，对应的value值为runoob  
	get name     返回键值name对应的value值
2. 散列类型(hash):键值对集合

		HMSET myhash field1 "hello" field2 "world"   设置值  
		HGET myhash field1       返回"hello"  
		HGET myhash field2       返回"world"  
		每个hash可以存储40多亿个键值对
	
3. 列表类型(list):简单的**字符串**列表，按照插入顺序排序。可以添加一个元素到列表的头部（左边）或者尾部（右边）
		
		lpush runoob redis mongdb   在列表runoob中添加两个元素 redis、mongdb  		
		lpush runoob rabitmq  在列表runoob中添加一个元素rabitmq  
		lrange runoob 0 10     遍历runoob列表，输出rabitmq、mongdb、redis  
		每个列表可存储40多亿个元素


4. 集合类型(set) :String类型的无序集合

		添加一个String元素到key对应的set集合中，成功返回1，如果元素已存在集合中，返回0，如果key对应的set不存在则返回错误  
		sadd abc redis  
		sadd abc mongodb  
		sadd abc rabitmq  
		sadd abc rabitmq   
		smembers abc   输出集合abc中的值 redis、rabitmq、mongodb
		每个集合可存储40多亿个元素
5. zset有序集合类型(sorted set)：String类型元素的集合，且不允许重复的成员。  

		每个元素都会关联一个double类型的分数。通过分数来为集合中的成员进行从小到大的排序。
		zset的成员是唯一的，但分数却可以重复。
		添加元素到集合，元素在集合中已存在则更新对应的score  
		命令：zadd key score member  
		zadd gg 0 redis  
		zadd gg 5 mongodb  
		zadd gg 3 rabitmq
		zrangebyscore gg 0 100 遍历输出集合gg：redis、rabitmq、mongodb

#2.Redis的应用场景

1. 缓存
2. 任务队列
3. 网站访问统计
4. 应用排行榜
5. 数据过期处理
6. 分布式集群架构中的session分离

#3.命令
1. redis-cli。 该命令会连接本地的redis服务。
2. redsi-cli -h host -p port -a password。连接远程redis服务

		例：redis-cli -h 127.0.0.1 -p 6379 -a "mypass"
#4.key命令
1. del key。在key存在时删除key。返回被删除的key的数量
2. dump key。序列化给定key，并返回被序列化的值。如果key存在，返回序列化之后的值，key不存在返回nil
3. exists key。检查key是否存在。存在返回1，否则返回0
4. Expire key_name seconds。设置key的过期时间，key过期后将不再可用。单位以秒计。成功返回1，失败返回0.
5. Expireat key_name timestamp.为key设置过期时间，单位是时间戳。
6. keys pattern.查找所有符合给定模式（pattern）的key。

		keys abc*   查找所有以abc开头的key值  
		keys *      查找所有可使用的key
7. move key_name db_name。将当前数据库的key移动到给定的数据库db中.成功返回1，失败返回0

		move gg 1。将gg移动到数据库1  
		当key不存在或者目标数据库中已存在该key，则移动失败。
		
8. persist key 移除key的过期时间，key将保持永久。
9. pttl key 以毫秒为单位返回key的剩余的过期时间。
10. ttl key。 以秒为单位，返回给定key的剩余时间。
11. randomkey.从当前数据库中随机返回一个key。
12. rename key newkey。修改key的名称。

		若newkey已存在，则原来的newkey会被覆盖，即原来的newkey消失
13. renameNX key newkey。仅当newkey不存在时，将key改名为newkey
14. type key.返回key所存储的值的类型。

#字符串命令
1. set key value;设置给定key的值，若key已存在，则新key覆盖旧key，且无视类型。
2. get key;获取指定key的值，如果key不存在，则返回nil，如果key存储的不是String类型，则返回一个错误。
3. getrange key start end;获取key中字符串的子串

		set test "12345678"
		getrange test 3 6    返回4567；左右都闭合。
4. getset key value;用于设置指定key的值，并返回key的旧值。
	
		若可以不存在，则返回nil
		set ff "123"  
		getset ff "456"；返回123，且ff的值变为456
5. getbit key_name offect；key存储的字符串值，获取指定偏移量上的位（bit）
		
		set test a;  a所对应的二进制是01100001；
		getbit test 0;返回0；getbit test 1;返回1
6. setbit  key offset value;对key存储的字符串，设置或清除指定偏移量上的为（bit）

		setbit test 1 0;将test所存储的value值，对应的二进制编码的偏移量为1的位改为0
		即变成00000001
7. Mget key1[key2...];返回所有给定key的值。如果给定的key里，有某个key不存在，那么这个key返回nil
8. setEX key seconds value;将value关联到key，并将key的过期时间设置为seconds(以秒为单位)。
9. setNX key value;只有在key不存在时设置key的值。
10. setRange key offset value;用value覆写给定key所存储的字符串，从偏移量offset开始;返回修改后的长度

		set test abcdefghijk;
		setrange test 3 123456;
		get test;返回abc123456jk
11. strLen key;获取key所存储的字符串值得长度。当key存储的不是字符串时，返回一个错误。key不存在时返回0；
12. MSET key1 value1 key2 value2 ....同时设置一个或多个key-value
13. MsetNX key1 value1 key2 value2 ...同时设置一个或多个key-value，当且仅当所有给定的key都不存在。成功返回1，失败返回0
14. INCR key;将key中存储的数字值增1
15. INCRby key increment。将key所存储的值加上给定的增量值。若key不存在则先把key的值初始化为0，再加上增量。
16. INCRbyFloat key increment。将key所存储的值加上给定的浮点增量值。若key不存在则先把key的值初始化为0，再加上增量。
17. DECR。将key中存储的数字值减1
18. DECRby key decrement;将key中所存储的值减去给定的增量。
19. append key value。如果key已存在并且是一个字符串，append命令将指定的value追加到该key原来值的末尾。

#hash命令
1. Hset key field value。为哈希表中的字段赋值。如果哈希表不存在，一个新的哈希表被创建并进行赋值。若字段已经存在与哈希表中，旧值将被覆盖。
2. Hdel key field1[field2...]删除一个或多个哈希表字段。
3. Hexists key field;查看哈希表中，指定的字段是否存在。
4. Hget key field; 获取存储在哈希表中指定字段的值
5. HgetAll key;获取哈希表中指定key得所有字段和值.
6. HINCRby key field increment.为哈希表中的指定字段的整数值加上增量increment
7. HINCRbyFloat key field increment;为哈希表key中的指定字段的浮点数值加上增量increment。
8. Hkeys key。获取所有哈希表中的字段。
9. Hlen key。获取哈希表中字段的数量
10. HMget key field1[field2]。获取所有给定字段的值。
11. HMset key field1 value1[field2 value2]。同时将多个field-value对设置到哈希表key中。
12. HsetNX key field value。只有在字段field不存在时，设置哈希表字段的值。
13. Hvals key。获取哈希表中所有的值。
14. HSCAN key cursor。迭代哈希表中的键值对

#list命令
1. BLpop key1[key2] timeout.移出并获取列表的第一个元素，如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止。
2. BRpop key1[key2] timeout.移出并获取列表的最后一个元素，如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止。
3. BRpopLpush list1 another_list timeout.从列表中弹出第一个值，将弹出的元素插入到另一个列表中并返回它；如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止。
4. Lindex key_name index.通过索引获取列表中元素。也可以使用负数索引，-1表示最后一个。
5. Linsert key before|after pivot value;在列表的元素前或元素后插入元素。当元素不存在于列表中时，不执行任何操作。当列表不存在时，不执行任何操作。

		Linsert mylist before "tom" "jerry";
		在mylist的tom元素前添加一个jerry元素
6. LLen key;返回列表长度。
7. Lpop key；移出并获取列表的第一个元素。
8. Lpush key value1 [value2...]将一个或多个值插入到列表的头部
9. LpushX key value.将一个值插入到已存在的列表头部。
10. Lrange key start end. 获取列表中指定范围内的元素
11. Lrem key count value. 根据参数count的值，移除列表中与参数value相等的元素。
12. Lset key index value.通过索引来设置元素的值。即列表中原位置的元素被覆盖掉
13. Ltrim key start end .让列表只保留区间内的元素，不在指定区间之内的元素都将被删除。0代表第一个元素，-1代表最后一个元素。
14. Rpop。移除列表的最后一个元素，返回值为移除的元素。
15. RpopLpush key another_key.移除列表的最后一个元素，并将该元素添加到另一个列表并返回.
16. RPUSH key value1[value2].在列表中添加一个或多个值.
17. RPUSHX key value. 为已存在的列表添加值.

#set命令
1. sadd key member1[member].向集合添加一个或多个成员.
2. scard key.获取集合的成元素.
3. sdiff key1 [key2].返回给定所有集合的差集.差集的结果来自于第一个key.

		key1 ={a,b,c,d}
		key2 ={b,c,6,7}
		sdiff key1 key2;返回a,d
4. sdiffstore des_key key1...keyN;将key1到keyN的差集存储到des_key中,如果指定的集合key已存在,则会覆盖.即原来的des_key中的元素将不存在.
5. sinter key1 [key2...];返回所有给定集合的交集.
6. sinterstore dest_key ke1..keyN;将key1到keyN的交集存储在dest_key中,如果dest_key已存在,则将其覆盖.
7. sisMember key value.判断value是否是集合key的成员,是返回1,不是返回0
8. sMembers key;返回集合中的所有成员.
9. Smove source destination member;将member元素从集合source移动到destination集合.

		Smove是原子性操作.
		如果source集合不存在member元素,则Smove不执行任何操作.
		当distination集合已经包含source元素时,则Smove只是简单的将source集合中的member元素删除.
10. Spop key [count];移除集合key中的一个或多个随机元素,移除后会返回移除的元素
11. SrandMember key [count];返回集合中一个或多个随机元素.

		不提供count,返回1个随机元素
		提供count,返回1个数组
12. Srem key member1,member2...;移除集合中一个或多个成员元素.返回成功移除的元素的数量.
13. sunion key key1...keyN;返回给定集合的并集.
14. SUnionStore destination key key1...keyN.将给定集合的并集存储在指定的集合destination中.如果destination已经存在,则将其覆盖.
15. Sscan key cursor [MATCH pattern] [COUNT count];迭代集合中键的元素.

		myset{"hello","hi","bar"}
		Sscan mytest 0 match h*
		返回myset集合中的所有以h开头的元素

#有序集合(sorted set)命令
1. Zadd key score1 member1 [score2 member2];向有序集合添加一个或多个成员,或者更新已存在成员的分数.
2. Zcard key;获取有序集合的成员数.
3. Zcount key min max;获取在有序集合中指定区间分数的成员个数.
4. zINCRby key increment member;将集合key中member元素的分数加上增量increment
5. ZINTERSTORE destination numkeys key [key ...] [WEIGHTS weight [weight ...]] [AGGREGATE SUM|MIN|MAX]集合中,默认情况下,结果集中某个元素的分数值是给定集合下该成员分数值之和.
6. ZlexCount key min max;获取集合中指定字典区间内成员数量.
7. Zrange key start stop [withscores];返回有序集中,指定区间内的成员.0是第一个,-1是最后一个.成员位置按照分数递增来排序.
8. ZrangeByLex key min max [limit offset count];通过字典区间返回有序集合的成员.
9. ZrangeByScore key min max [WITHSCORE] [LIMIT offset count];返回有序集合中指定分数区间的成员列表.有序集成员按分数值递增次序排列.默认是左闭右闭.


		ZRANGEBYSCORE zset (1 5; 1<score<=5
		ZRANGEBYSCORE zset (1 (5;1<score<5
10. Zrank key member;返回有续集中指定成员的排名.其中有续集成员按分数值递增排序.
11. Zrem key member [member ...];移除有序集合中的一个或多个成员.返回成功移除的成员的数量
12. ZremrangeBylex key min max; 移除有序集合中给定的字典区间的所有成员。
13. ZremRangeByRank key start stop;移除有序集中，指定排名区间内的所有成员
14. ZremrangeByScore key min max;移除有序集中，指定分数区间内的所有成员。
15. Zrevrange key start stop [withscores];返回有序集中指定区间内的成员，成员的位置按数值递减来排序。
16. ZrevRangeByScore key max  min [WIthSCORES];返回有序集中指定分数区间内的成员，分数从高到底。
17. ZrecRank key member;返回member在有序集合中的排名；有序集合成员按分数值递减排序。排名从0开始
18. Zscore key member;返回有序集中member的分数值。如果member不是有序集的成员或者key不存在，返回nil;
19. Zunionstore destination numkeys key [key...] [weights weights [weights]] [aggregate sum|min|max];计算给定的一个或多个有序集的并集，其中key的数量必须以numkeys参数为指定，并将该并集存储到destination中；weights是为每个集合指定一个乘法因子，默认1；aggregate 是给出的集合中，相同成员的分数怎么处理，默认为sum；


		zset1={tom:200;jack:300;jerry:500}
		zset2={tom:300;marry:100;}
		zunionStore result 2 zset1 zset2 weightsc 1 3 aggregate max;
		结果result{tom:900,jack:300;jerry:500;marry:300};
		第一个集合成员都乘1，第二个集合成员都乘2，然后再求并集。对于都含有的成员tom，分数取最大的最为结果。
20. zscan key cursor [Match pattern] [Count count];遍历输出有序集合

#HyperLogLog
- 作用：计算输入的元素的基数。

		{1，2，5，7，9，5，7，8}
		基数集为{1，2，5，7，8，9}
		基数为：6
- 每个HyperLogLog键只需要12kb内存；
- HyperLogLog只会根据输入的元素来计算基数，而不会存储元素本身
###命令
1. pfadd key element [element...];添加指定元素到HyperLogLog中
2. pfcount key [key...];返回给定HyperLogLog的基数估算值。如果是多个，则返回基数之和。
3. pfmerge destkey sourcekey [sourcekey];将多个HyperLogLog合并成一个HyperLogLog，合并后的基数估算值是通过所有给定的HyperLogLog进行并集计算得出的


#发布订阅   


- 发送者（pub）发布消息，订阅者（sub）接受消息。
- redis客户端可以订阅任意数量的频道。


![avatar](..\imgs\111.jpg)  
 
![avatar](..\imgs\222.jpg)   
###命令
1. Psubscribe pattern [pattern...];订阅一个或者多个符合给定模式的频道
2. subscribe channel [channel ...];订阅给定的一个或多个频道的信息
3. publish channel message; 将消息发送到指定的频道。
4. unsubscribe channel [channel...];退订给定的一个或多个频道。
5. PUnsubscribe [pattern [pattern...]] ;退订所有给定模式的频道。
6. pubsub <subcommand> [argument[argument...]];查看订阅与发布系统状态。返回由活跃频道组成的列表。

#事务
###redis事务可以一次执行多个命令，并且带有以下两个重要的保证：
- 批量操作在发送EXEC命令前被放入队列缓存。
- 收到EXEC命令后进入事务执行，事务中任意命令执行失败，其余的命令依然被执行。
- 在事务执行过程，其他客户端提交的命令请求不会插入到事务执行命令序列中。

###一个事务开始到执行会经历一下三个阶段
1. 开始事务。
2. 命令入队。
3. 执行事务。

**单个Redis命令的执行是原子性的，但Redis没有在事务上加任何维持原子性的机制，所有Redis事务的执行并不是原子性的；中间某条指令的失败不会导致前面已做指令的回滚，也不会造成后续的指令不做**
###命令
1. multi;标记一个事务的开始。
2. exec;执行所有事务块内的命令。
3. discard;取消事务，放弃事务块内所有命令。
4. watch key [key...];监视一个或多个key，如果在事务执行前这些key被其它命令所改动，那么事务将被打断。
5. unwatch;取消watch命令对所有key的监视。

#连接命令
1. auth password;验证密码是否正确。
2. echo message；打印字符串。
3. ping；查看服务是否运行。
4. quit；关闭当前连接。
5. select index;切换到指定的数据库。

#服务器命令
1. BGREWriteAof;用于异步执行一个AOF（AppendOnly File）文件重写操作

		重写会创建一个当前AOF文件的体积优化版本，即使BGREWriteAof执行失败，也不会有任何数据丢失，因为旧的AOF文件在BGREWriteAof成功之前不会被修改。  
		在redis2.4开始，AOF重写有redis自行触发，BGREWriteAof仅仅用于手动触发重写操作。  
		什么是AOF：持久化记录服务器执行的所有写操作命令，并在服务器重新启动时，通过重新执行这些命令来还原数据集。
2. bgSave;在后台异步保存当前数据库的数据到磁盘。

		BGSAVE 命令执行之后立即返回 OK ，然后 Redis fork 出一个新子进程，原来的 Redis 进程(父进程)继续处理客户端请求，而子进程则负责将数据保存到磁盘，然后退出
3. client list;返回所有连接到服务器的客户端信息和统计数据。
4. client kill ip:port;关闭客户端连接。
5. client getname;获取连接的名称。
6. client pause timeout;在指定时间内终止运行来自客户端的命令。（毫秒计）
7. client setname connection-name;设置当前连接的名称。
8. cluster clots;获取集群节点的映射数组。
9. command；获取redis命令详情数组。
10. command count；获取redis命令总数；
11. command getkeys;获取给定命令的所有键。
12. time；返回当前服务器时间。
13. command info command-name[command-name ...]获取指定redis命令描述的数组。
14. config get parameter;获取指定配置参数的值。
15. config set parametet value;修改redis配置参数，无需重启。
16. config rewrite;将15步进行的配置文件的修改写到redis.conf文件。
17. config resetstat;重置info命令中的某些统计数据。
18. dbsize；返回当前数据库的key的数量。
19. debug object key；获取key的
20. debug segfault;让redis服务崩溃。
21. flushAll;删除所有数据库的所有key。
22. flushDB;删除当前数据的所有key。
23. Info；返回关于redis服务器的各种信息和统计数值。
24. lastSave；返回最后一次redis成功将数据保存到磁盘上的时间，以unix时间戳格式表示。
25. monitor;实时打印出redis服务器接收到的命令，调试用。
26. role;查看主从实例所属的角色，角色有master，slave,sentinel
27. save;执行一个同步保存操作，将当前redis实例的所有快照以RDB文件的形式保存到硬盘。
28. shutDown;异步保存数据到硬盘，并关闭服务器。
29. slaveOf host port;将当前服务器转变为指定服务器的从属服务器。

		如果当前服务器已经是某个主服务器的从属服务器，那么执行slaveOf host port 将使当前服务器停止对旧主服务器的同步，丢弃旧数据集，转而开始对新主服务器进行同步。  
		另外，对一个从属服务器执行命令slaveOf no one 将使得这个从属服务器关闭复制功能，并从从属服务器转变回主服务器，原来同步所得的数据集不会丢失。
30. slowlog；记录查询时间的日志系统。
31. sync；同步主从服务器。


#数据备份与恢复
###备份
- save;该命令将在redis安装目录中创建dump.rdb文件。
- bgsave;在后台备份文件。
###数据恢复
- 将备份文件移动到redis安装目录并启动服务即可。

#安全
- 设置密码config set requirepass 123456
- config get requirepass;获取密码
- auth pass 验证密码

#客户端命令
1. client list;返回连接到redis服务的客户端列表。
2. client setName;设置当前连接的名称。
3. client getname;获取当前连接的名称。
4. client pause 挂起客户端指针，指定挂起的时间以毫秒计。
5. client kill;关闭客户端连接。

#redis的持久化
1. RDB持久化：默认的，在指定的时间间隔内，将内存中的快照写入到磁盘内。

		优势：
2. AOF持久化：同步到日志文件中；需要手动配置
		
		同步策略：1，每修改就同步；2，每秒同步一次；3，不同步
		优势：更安全、
		缺点：效率低、文件大、
3. 无持久化：可以通过配置关闭redis的持久化功能。

