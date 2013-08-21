Yaha分词
========
"哑哈"中文分词，更快或更准确，由你来定义。通过简单定制，让分词模块更适用于你的需求。
"Yaha" You can custom your Chinese Word Segmentation efficiently by using Yaha


安装
======
pip install haya


Feature
========
* 基本功能：
  * 精确模式，将句子切成最合理的词。
  * 全模式，所有的可能词都被切成词，不消除歧义。
  * 搜索引擎模式，在精确的基础上再次驿长词进行切分，提高召回率，适合搜索引擎创建索引。
  * 备选路径，可生成最好的多条切词路径，可在此基础上根据其它信息得到更精确的分词模式。

* 可用插件：
  * 正则表达式插件
  * 人名前缀插件
  * 地名后缀插件
  * 定制功能。分词过程产生4种阶段，每个阶段都可以加入个人的定制。

* 附加功能：
  * 新词学习功能。通过输入大段文字，学习到此内容产生的新老词语。
  * 获取大段文本的关键字。
  * 获取大段文本的摘要。
  * 支持用户自定义词典



在线演示
========
TODO


Algorithm
=========
* 核心是基于查找句子的最大概率路径来进行分词。
* 保证效率的基础上，对分词的各个阶段进行定义，方便用户添加属于自己的分词方法(默认有正则，前缀名字与后缀地名)。
* 用户可自定义使用动态规划或Dijdstra算法得到最优的一条或多条路径，再次可根据词性(中科大ictclas的作法)等其它信息得获得最优路径。
* 使用“最大熵”算法来实现对大文本的新词发现能力，很适合使用它来创建自定义词典，或在SNS等场合进行数据挖掘的工作。
* 相比已存在的结巴分词，去掉了很消耗内存的Trie树结构，以及新词发现能力并不强的HMM模型(未来此模型可能当成一个备选插件加入到此模块)。


阶段讲解
========
* stage 1是在分句中实现，通过正则可直接将数字或英文单词分成独立的词，生成独立的这些词不再参与下一步的分词。
* stage 2在创建有向无环图之前实现，对分句进行预扫描，加入一些可能形成的词，并赋予一定的概率。
* stage 3在创建有向无环图期间实现，从字典得到词的概率，或通过一些匹配模式得到可能的词，赋予一定概率。
* stage 4在得到有向无环图的最大概率之后（程序实现当中是最短路径），对一些不能成词的单字再继续进行处理；或得到最短的多条路径之后，根据用户的兴趣得到最终的一条路径。若用户有兴趣，可以在这一步实现对词性的分析。


目前状态
========
时间过得真快，之前说上面提到的内容的核心部分得到实现，现在要说上面提到的内容90%已得到实现。包含很有意思的自动生词，自动摘要，关键字提取等。 最后要感谢jieba的作者，目前的字典是直接从jieba项目拷贝过来的。
