## 学习总结

### 本周学习了数组，链表，跳表，栈，队列，双端队列，优先队列

#### 一. 学习后的理解和想法

1. 个人理解数据结构可分成两类，一是数据结构存储，二是数据结构应用

2. 数据结构存储本质都是数组或者链表，数组要申请连续内存空间，如果数组在扩容的时候申请内存空间无法满足会导致程序出错，链表本身是零散分布，通过每个节点持有下一个节点的指针访问元素，扩容的时候也不需要有大片连续内存空间，也就解决了数组在内存使用上的问题

3. 数据结构应用就是在数组和链表的基础上扩展一些高级功能，其中还包括基础的数据结构，有数组，链表，堆，栈，hash，高级一点的数据结构都是基于这些基础的扩展，更高级的会组合多个数据结构，形成一个新的数据结构，例如：PriorityQueue，LinkedHashMap，ArrayDeque等


#### 二. 各数据结构总结

- 数组
   - 支持随机访问元素，时间复杂度O(1)
   - 新增和删除涉及元素搬移，时间复杂度O(n)

- 链表
   - 新增和删除只需修改指针指向，时间复杂度O(1)
   - 不支持随机访问，访问元素只能每次从头开始遍历，时间复杂度O(n)

- 跳表
   - 跳表的实现基于链表，存储元素必须有序
   - 把链表升维，提取更粗粒度的数据建立索引
   - 有点像二分查找，AVL树的思想，不过维度更多，相应索引多占用空间大
   - 插入、删除、查询元素的时间复杂度都是O(log n)

- 栈
   - 后进先出，底层存储基于数组实现
   - 添加，删除元素的时间复杂度是O(1)
   - 随机查找元素时间复杂度是O(n)
   - 现实已经建议使用双端队列替换使用

- 队列
   - 先进先出，
   - 添加，删除元素的时间复杂度是O(1)
   - 随机查找元素的时间复杂度是O(n)
   - 在java中本身是一个抽象数据模型，队列的实现有很多种，有数组的也有链表的

- 双端队列
   - 结合了栈和队列的特点，头和尾两端都可添加删除元素
   - 随机查找元素的时间复杂度是O(n)

- 优先队列
   - 优先队列也属于队列的一种，只不过元素具有优先级顺序，取出元素优先级最高的一个
   - 取出元素的时间复杂度是O(log n)
   - 添加元素的时间复杂度是O(1)

## 每周作业

#### Deque旧Api改造为新的

旧API实现：

```java
Deque<String> deque = new LinkedList<String>();
deque.push("a");
deque.push("b");
deque.push("c");
System.out.println(deque);
String str = deque.peek();
System.out.println(str);
System.out.println(deque);
while(deque.size() > 0){
	System.out.println(deque.pop());
}
System.out.println(deque);
```

新API实现：

```java
Deque<String> deque =new LinkedList<String>();
deque.addFirst("a");
deque.addFirst("b");
deque.addFirst("c");
System.out.println(deque);
String str = deque.peekFirst();
System.out.println(str);
System.out.println(deque);
while(deque.size() > 0){
	System.out.println(deque.removeFirst());
}
System.out.println(deque);
```

#### Queue源码分析

 Queue的定义是一个interface，继承自Collection，提供一些基础方法，一些提供高级方法实现的类都是实现的Queue

 - add 添加元素，如果不支持动态扩容会有异常

 - offer 添加元素，容量不够会返回false，据官方解释优于add方法

 - remove 删除元素，如果为null会抛出异常

 - poll 删除元素，如果为null直接返回

 - element 查询返回队列头元素，如果为null，抛出异常

 - peek 查询返回队列头元素，如果为null直接返回

可能的异常：

```java
IllegalStateException
如果容量不够切不支持动态扩容会抛出IllegalStateException异常
ClassCastException
指定元素的类阻止元素加入队列抛出
NullPointerException
如果指定元素为null，并且队列不允许null值时抛出
IllegalArgumentException
如果元素无法添加到队列时抛出
```

#### Priority Queue源码分析

PriorityQueue的定义是class，继承AbstractQueue，AbstractQueue又继承自AbstractCollection，又实现了Queue，所以能看出PriorityQueue是一个实现了Queue的提供了高级功能的实现类

说说理解的一些实现细节处

- 通过数组存储数据

- add()方法直接调用了offer()方法，此方法不允许插入null值，支持动态扩容，长度小于64加倍，否则扩容50%，每次添加元素需要计算元素的优先级，调整元素位置

- remove()方法，从队列删除已经存在的元素，同样需要出发元素位置调整