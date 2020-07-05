# 学习笔记

## 字典树和并查集

### 字典树

字典树，Trie树，工程应用场景是搜索引擎，可以做到字符串智能匹配，统计，排序大量文本内容。

优点是最大程度减少字符串比较，效率优于哈希表

缺点是空间占用会稍大，空间换时间的思路，查询一个单词的时候，通过公共前缀去减少匹配时间
 
- 每个节点不存储完整单词
- 每个节点所有子节点路径表示出的单词是不相同的
- 从根节点出发到一个子节点途径的子节点连起来就是一个完整的单词

### 并查集

并查集常用与组团和配对问题，并查集包含三个主要函数
- 建立包含单元素集合的新并查集
- 把两个元素所在的集合合并
- 找到某个元素所在的集合的代表

并查集代码模板
``` java
class UnionFind {
    private int count = 0;
    private int[] parent;
    public UnionFind(int n) {
        count = n;
        parent = new int[n];
        for (int i = 0; i < n; i++) {
            parent[i] = i;
        }
    }
    public int find(int p) {
        while (p != parent[p]) {
            parent[p] = parent[parent[p]];
            p = parent[p];
        }
        return p;
    }
    public void union(int p, int q) {
        int rootP = find(p);
        int rootQ = find(q);
        if (rootP == rootQ) return;
        parent[rootP] = rootQ;
        count--;
    }
}
```

## 高级搜索

### 剪枝的实现和特性

剪枝适用于对状态树的搜索

如果发现一个分支已经处理过，可以把结果缓存起来，下次遇到直接返回，就是剪枝

如果发现一个分支结果肯定不对，或者不是最优解，则在求最优解的场景中可以把这样的分支剪掉

剪枝的目的是减小搜索空间，降低时间复杂度

### 双向BFS

从开始和结束两个位置同时BFS，其实也类似数组，链表中的双指针，第一次相遇的位置为中间位置，计算两边的层数之和即为开始和结束位置之间的总层数。

### 启发式搜索

启发式搜索常用优先级队列，优先级队列的优先级需要通过启发函数，估价函数决定。
启发式函数用来评价哪些节点最优看你是要找的节点，函数返回一个非负实数，也可以认为是从当前节点到目标节点路径的估计成本。
启发式函数是一种告知搜索方向的方法，它提供了一种明智的方法来猜测哪个邻居节点会导向一个目标

### 总结双向BFS模板代码
``` java
public int bidirectionalBFS(Map<Integer, List<Integer>> graph, int start, int end) {
    Set<Integer> visited = new HashSet<>();
    Set<Integer> startVisited = new HashSet<>();
    startVisited.add(start);
    Set<Integer> endVisited = new HashSet<>();
    endVisited.add(end);
    int step = 0;
    while (!startVisited.isEmpty() && !endVisited.isEmpty()) {
        if (startVisited.size() > endVisited.size()) {
            Set<Integer> temp = startVisited;
            startVisited = endVisited;
            endVisited = temp;
        }
        step++;
        Set<Integer> nextLevelVisited = new HashSet<>();
        for (int node : startVisited) {
            process(node, nextLevelVisited);
            for (int nextNode : nextLevelVisited) {
                if (endVisited.contains(nextNode)) {
                    return step;
                }
            }
        }
        startVisited = nextLevelVisited;
    }
    return 0;
}
```

## 红黑树和AVL树

### 红黑树

红黑树是近似平衡的二叉搜索树，确保任何一个节点的左右子树的高度差小于2倍。

红黑树是满足几个条件的二叉搜索树
- 每个节点不是红就是黑
- 不能有相邻的两个红色节点
- 根节点是黑色的
- 每个叶子节点是黑色的（NIL节点，空节点）
- 从任意一个节点到每个叶子节点的所有路径都包含相同数目的黑色节点

红黑树的关键性质，从根节点到叶子节点的最长的看你路径不多于最短路径的2倍长。

### AVL树

AVL树是一个严谨的二叉搜索树

定义平衡因子是左子树的高度减去右子树的高度，也可能是右子树减去左子树。

AVL树的平衡因子的绝对值不超过1，一般就是：-1，0，1

通过旋转操作进行树的平衡，一共4种旋转操作，左旋，右旋，左右旋，右左旋

AVL树的缺点：节点需要额外存储信息，每一次新增，删除都要严格执行平衡操作，维护成本高

他们二者的区别
- AVL树查询比红黑树快，因为AVL树是严格的平衡二叉树
- 插入，删除红黑树比AVL树快，因为AVL树每一次新增，删除都要严格执行平衡操作，红黑树不需要
- AVL树需要在每个节点存储平衡因子或者高度绝对值，空间上比红黑树消耗更多，红黑树只需存储颜色即可
- 红黑树在大多数高级语言的库函数中使用，AVL树常用于数据库索引
