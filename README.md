# jdata

jdata联通赛top11特征分析及详细代码（含注释）

#这是我第二次参加数据挖掘类比赛，新手成长中，回头想想，当初有很多细节没做好，所以也附带了赛后反思优化

#比赛链接  https://jdata.jd.com/html/detail.html?id=3

### 特征工程

#初始特征

对于train testa testb 分别有三个特征表：sms.txt(短信) voice.txt（通话）  wa.txt（网址）

#### sms 表

##### `opp_num`

这个是匿名特征，当时直接删掉没用，想想真后悔，其实稍加处理下，应该可以稍微提分的，比如说对出现频次最多的n个号码进行统计，应该可以作为风险用户的强特

的，后悔！！


##### `opp_head`

根据vid和opp_head做group_by聚类处理，统计每个用户对于不同开头号码的短信情况

赛后反思：其实可以知道里面有国际电话和国内电话，并且有不同运营商的信息，可以对其进一步处理的



##### `opp_len`

 根据vid和opp_len做group_by聚类处理，统计每个用户对于不同开头号码的短信情况


##### `start_time`
由于这个是时间戳特征，所以对其进行了数字化处理，并统计了不同时间分布的短信情况：如深夜短信、早上、下午等，同时统计了发送和接收短信的总次数、均值等

赛后反思：后来做另一个比赛时，才知道有个diff的时间差骚操作，并且结合一阶二阶时间差，往往会有比较好的效果，还是太年轻！


##### `in_out`

简单统计了短信发送和接收的比例

赛后反思：其实可以根据in out 做一些更细致化的操作的


#### voice表

对于voice表， 其实里面有大量的特征提取方法和`sms`表相同

下面说说相对于sms表增加的一些操作

`start_time 、 end_time`

通过这两个特征，可以统计通话时长。基于通话时长也可以展开一系列的操作。

比如：通话最长、最短，平均通话时长，通话时长少于多少的次数等等

另外，还可以统计没人每天平均通话时长、次数

赛后反思：也和sms一样，可以统计时间差等信息。同时还可以考虑使用滑动时间窗口进行统计，这也是后来参加一些比赛发现的骚操作。经验还是很重要！


#### wa 表

##### `wa_name`

这里当初直接进行one-hot了，其实可以先统计频率次数top n和最少次数top n 的one-hot的，这样就不用出现维度灾难的问题

##### `visit_cnt`

统计总和，方差等量，常规操作


##### `wa_type`

统计浏览方式，统计了比例啊 one-hot啊之类

赛后反思：其实可以根据不同的wa_type进行更细致化的统计，这样可能效果会好一点，不过也不一定

其他字段基本也是差不多操作，有兴趣欢迎浏览代码，代码中有一些pandas等的操作，也有详细注释



