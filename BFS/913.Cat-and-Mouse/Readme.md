### 913.Cat-and-Mouse

此题是game thoery中的好题．看上去像常规的minMax问题，但实际上几乎所有的DFS解法都是不完备的，参看leetcode的讨论区．

正确的解法是用BFS.我们设计节点状态是(m,c,turn)，用color[m][c][turn]来记忆该状态的输赢情况．

首先我们将所有已知的状态加入一个队列．已知状态包括(0,c,turn)肯定是老鼠赢，(x,x,turn)且x!=0肯定是猫赢．我们尝试用BFS的思路，将这些已知状态向外扩展开去．

扩展的思路是：从队列中取出队首节点状态（m,c,t），找到它的所有邻接的parent的状态（m2,c2,t2）．这里的父子关系是指，(m2,c2,t2)通过t2轮（老鼠或猫）的操作，能得到(m,c,t).我们发现，如果(m,c,t)是老鼠赢而且t2是老鼠轮，那么这个(m2,c2,t2)一定也是老鼠赢．同理，猫赢的状态也类似．于是，我们找到了一种向外扩展的方法．

向外扩展的第二个思路是：对于(m2,c2,t2)，我们再去查询它的所有children（必定是对手轮）是否都已经标注了赢的状态．如果都是赢的状态，那么说明(m2,c2,t2)无路可走，只能标记为输的状态．特别注意的是，第一条规则通过child找parent，和第二条规则通过parent找child的算法细节是不一样的，一定要小心．

这样我们通过BFS不断加入新的探明输赢的节点．直到队列为空，依然没有探明输赢的节点状态，就是平局的意思！


[Leetcode Link](https://leetcode.com/problems/cat-and-mouse)