## 学习笔记

### 一周总结
本周学习了深度优先搜索，广度优先搜索，贪心算法和二分查找

### 深度优先搜索和广度优先搜索

- 深度优先搜索
  - 是对树的一种遍历方式
  - 从根节点开始访问，先遍历左子节点，直到为null然后退回到父节点再访问右子节点
  - 使用递归或者栈实现
- 广度优先搜索
  - 从根节点开始访问，先遍历每一层的所有节点，然后再去下层遍历
  - 使用队列实现

DFS代码模板
``` python
// 递归
visited = set() 
def dfs(node, visited):
    if node in visited: # terminator
    	# already visited 
    	return 
	visited.add(node) 
	# process current node here. 
	...
	for next_node in node.children(): 
		if next_node not in visited: 
			dfs(next_node, visited)
// 非递归
def DFS(self, tree): 
	if tree.root is None: 
		return [] 
	visited, stack = [], [tree.root]
	while stack: 
		node = stack.pop() 
		visited.add(node)
		process (node) 
		nodes = generate_related_nodes(node) 
		stack.push(nodes) 
	# other processing work 
	...
```

BFS代码模板

``` python
def BFS(graph, start, end):
    visited = set()
	queue = [] 
	queue.append([start]) 
	while queue: 
		node = queue.pop() 
		visited.add(node)
		process(node) 
		nodes = generate_related_nodes(node) 
		queue.push(nodes)
	# other processing work 
```

### 贪心算法

- 贪心算法的核心思想是只关心每次当前步骤中最优解，不关心全局最优解
- 无法和回溯、动态规划一样，能回退重新选择

### 二分查找

- 二分查找需要本身有序的
- 存在上下界
- 可以使用索引访问元素
- 二分查找需要定义好中间分区点