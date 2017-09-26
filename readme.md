# 软件工程实验1

开发一个Java命令行程序，实现从文本文件中读取数据并根据要求生 成图结构，输出该图结构，并在其上进行一系列计算操作，实时展示各操作的结果。其中包括如下功能。

1.输入一个文本文件，只接受大小写字母，连续的大小写字母构成单词。

2.根据读入的文本生成一幅有向图，边为前一个词指向后一个词，边权为这条边在文本中出现的次数。

3.将这张有向图可视化，生成一张图片并展示出来。

4.在生成有向图之后，用户输入任意两个英文单词word1、word2，程序从图中查询它们的“桥接词”。其中，桥接词的定义为“word1、word2的桥接词word3:图中存在两条边word1->word3, word3- >word2”。输入的word1或word2如果不在图中出现，则输出“No word1 or word2 in the graph!”。如果不存在桥接词，则输出“No bridge words from word1 to word2!”。如果存在一个或多个桥接词，则输出“The bridge words from word1 to word2 are: xxx, xxx, and xxx.”。

5.用户输入一行新文本，程序根据之前根据输入文 件生成的图，计算该新文本中两两相邻的单词的 bridge word，将bridge word插入新文本的两个单词之间，输出到屏幕上展示。如果两个单词无bridge word，则保持不变，不插入任何单词; 如果两个单词之间存在多个bridge words，则随机 从中选择一个插入进去形成新文本。

6.用户输入两个单词，程序计算它们之间在图中的最短路径，以某种突出的方式将路径标注在原图并展示在屏幕上，同时展示路径的长度。计算出所有的最短路径，并以不同
的突出显示方式展示出来。如果输入的两个单词不可达，则给出提示。

7.随机游走功能。进入该功能时，程序随机的从图中选择一个节 点，以此为起点沿出边进行随机遍历，记录经 过的所有节点和边，直到出现第一条重复的边 为止，或者进入的某个节点不存在出边为止。 在遍历过程中，用户也可随时停止遍历。遍历结束后，将遍历的所有节点构造文本，展示出来。

# 待求解问题描述与数学模型

本实验可以看成是一个有向图G=<V, E>。其中V为图中结点的集合，各点需要保存的值为其代表的单词，即一个字符串。E为图中边的集合，每条边<u, v> (<u,v>∈E)需要保存一个值w，为单词对<S(u), S(v)>在G表示的文章中出现过的次数。

1.	建图：输入数据是一个String类型的对象，要求必须为合法的文件名且对应的文件为ASCII字符的文本文件。对于对应的内容，我们可以看作是若干单词组成的线性表。我们需要输出一个有向图，可以是自定义的Graph类型的对象。

2.	图的可视化：输入数据是一个有向图（自定义类型），输出一张图片，为这个有向图的可视化表示。

3.	查询桥接词：输入数据为String类型的对象s1, s2，以及有向图G=<V, E>。首先找到点u, v∈V，使得w(u)=s1, w(v)=s2，这里需要保证V中存在w为s1和s2的结点。然后我们要找到集合V’={x | x∈V, (u, x)∈E, (x, v)∈E}，这里我们可以将V’保存为一个数组，作为输出数据。

4.	生成新文本：输入一个String类型的对象s，以及有向图G=<V,E>。s为一个合法的英文句子。对于s中的每相邻两个单词，如果他们在V中有对应的结点，且在G中存在桥接词，随机取其中一个，加在两个单词中间。如果这两个单词间有标点符号，默认加在标点符号左边。输出数据为一个String类型的对象，表示处理后的句子。

5.	最短路径：输入String类型的对象w1，w2，以及有向图G=<V,E>。要求w1，w2为合法的英语单词，且存在u,v∈V，使w(u)=s1, w(v)=s2。对于这样的u，v，我们查询G中从u到v的边权值和最小的路径，同时记录下各点在最短路径上的前驱结点。输出值为一个整数，表示u到v最短路径的权值和。

6.	随机游走：输入为有向图G=<V,E>。先随机找一个结点v[0]∈V，然后随机找一条边，使得起点为v[0]。将这条边记为<v[0],v[1]>∈E，之后对于每一个结点v[i]，随机取边<v[i], v[i+1]>∈E，直到边<v[i], v[i+1]>之前访问过或有中断命令。然后输出数组v[0]，v[1]，……。


