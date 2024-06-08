# CH 11 : Trees

## 11.1 Introduction to Trees

- Tree: connected undirected graph with no simple circuits
- Forest: undirected graph with no simple circuits (collection of trees)
- 一个无向图是树当且仅当在它的每对顶点之间存在唯一简单通路
- 选定一个根节点后，树可以被唯一地画出（Rooted Tree）
- Sibling: 有同样父节点的节点称为Siblings
- Ancestors: 从该节点到根节点Path上所有节点称为该节点的Ancestors
- Descendants: 所有以该节点为Ancestors的节点称为该节点的Descendants
- Internal Vertex: 有孩子的点叫内点
- Ordered Rooted Tree: 每个内点的孩子都排序的有根树，按从左到右的顺序
- Level: The level of vertex v in a rooted tree is the length of the unique path from the root to v ==例如，只有Root的树，Level和Height都为0，空树的Height为-1==
- Height: The height of a rooted tree is the maximum of the levels of its vertices
- Balance: 所有叶节点都在Levels h or h-1的Rooted Tree ==平衡树==
- 𝑛 个顶点的树含有 𝑛−1 条边
- 树都是二部图，$𝐾_{1,𝑛}$ 和 $𝐾_{𝑚,1}$ 是树

!!! note "Counting"
	给出节点数n，让你计算可以构造出Tree的数量，记得关注是unrooted tree还是rooted tree
	
	例子： n=5 , unrooted=3 , rooted=9.
	
	计算Rooted Tree个数的时候，可以从The longest path from root这个角度切入

- 对于任何树，都有 $|E|=|V|-1$
- 对于Full m-ary Tree with i internal vertices，共有 n=mi+1 vertices (Tips:n=l+i，因此也可以算出来叶节点的个数)
	- 满m叉树：值该树的节点要么是叶节点要么是满节点

!!! example
	How many leaves does a full 3-ary tree with 100 vertices have?
	
	$i=\frac{n-1}{m}=\frac{100-1}{3}=33$ ， $l=n-i=100-33=67$


## 11.2 Applications of Trees

=== "Binary Search Tree 二叉搜索树"
	很基本的构造
=== "Decision Tree 决策树"
	每一个Internal Vertex对应一个决策
=== "Prefix Codes 前缀码"
	- 为了确保一串bit string对应不超过一种Letter序列，一个Letter的编码不应该出现在另一个Letter编码的开头，如： e:0,a:10,b:110
	- 用一个Binary Tree来构造编码，往左的边对应0，往右的边对应1，则编码为该树叶节点对应的序列：
	![[PrefixCode.png]]
=== "Huffman Tree 哈夫曼树"
	使得每个叶节点都有权值，则定义 ==节点的带权路径长度== 为节点到Root的路径长度于节点权值的乘积。称所有节点的带权路径长度之和为树的带权路径长度。
	
	其中，带权路径长度最短的树称为Huffman Tree，按照哈夫曼树进行Prefix Coding，得到哈夫曼编码
	
	构造哈夫曼树的哈夫曼算法如下：
	
	- 有n个原始节点，权值分别为$\{W_1 ,W_2,..., W_n\}$ ，构造成n颗二叉树的集合$F=\{T_1, T_2,... ,T_n\}$ ，其中每颗二叉树 $T_i$ 只有一个带权为 $W_i$ 的根节点，左右孩子均空
	- 在F中pop两颗根节点权值最小的二叉树，作为树的左右孩子构造新树，且置根节点为左右孩子权值之和，将新二叉树压入F中
	- 重复上一步，直到F中只剩一颗树，这颗树就是Huffman Tree
	
	!!! danger
		遇到诸如 `What is the average number of bits required to encode a character?` ，注意最后结果不是单纯的所有bit位相加除以字母数，而是各个character的bit位数乘以它们的权值再相加 (即 ==加权平均数== )
## 11.3 Tree Traversal

- preorder traversal 对应 Prefix Form(波兰表达式)
- inorder traversal 对应 Infix Form(正常的表达式)
- postorder traversal 对应 Postfix Form(逆波兰表达式)

