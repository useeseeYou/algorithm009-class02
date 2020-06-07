## 学习笔记

### 一周总结

本周学习了递归，分治，回溯，知识点内容不算多，但是明显感觉学习曲线有些陡峭了，学起来有点费劲，而且练习题看别人的题解也有一些费劲
不过多少也有收获，以前无法理解的知识点有了个全面的认识，还有一些思维模式上的转变


### 递归，范型递归，树的递归

递归的本质就是循环函数自身，和循环的区别在于，循环是通过程序内部实现的迭代器循环访问某个集合类型的数据集合，而递归是通过代码自己实现一个迭代器，循环函数本身，边界值，异常情况处理，都需要开发人员自己设计和考虑。
虽然两者都是循环的思维，看着近似，其实区别还是非常大的，解决的问题也是不一样的。

#### 一. 范型递归
递归函数设计重要的几个元素

- 递归终止条件
- 当前层处理逻辑
- 下去到下一层
- 下层回到本层后的清扫逻辑

递归思维训练方式

- 抵制人肉递归，不要自己手动一层一层的去计算
- 找到最近重复性
- 数学归纳法思维

递归代码模板

``` java
// Java
public void recur(int level, int param) {
  // terminator
  if (level > MAX_LEVEL) {
    // process result
    return;
  }
  // process current logic
  process(level, param);
  // drill down
  recur( level: level + 1, newParam);
  // restore current status
}
```

``` python
# Python
def recursion(level, param1, param2, ...):
    # recursion terminator
    if level > MAX_LEVEL:
       process_result
       return
    # process logic in current level
    process(level, data...)
    # drill down
    self.recursion(level + 1, p1, ...)
    # reverse the current level status if needed
```

#### 二. 树的递归

树的重复子问题和规律非常符合递归思维

树的访问最多的就是递归，每一层调用下一层的时候传入左右子节点，直到左右子节点为`null`开始`return`

### 分治，回溯

#### 一. 分治

分治实质还是递归，实现也是用递归，只不过找到问题重复性，分解子问题，最终合并结果

#### 二. 回溯

回溯的实质也是递归，和分治类似，回溯需要暂存结果集，递归过程中每次与结果集比较，是否符合要求，不符合需要重新选择路线计算
