# LeetCode练习题

1. 删除排序数组中的重复项

```java
public int removeDuplicates(int[] nums) {
  if (nums == null) {
    return 0;
  }
  int i = 0;
  for (int j = 0; j < nums.length; j++) {
    if (nums[j] != nums[i]) {
      i++;
      nums[i] = nums[j];
    }
  }
  return i + 1;
}
```



2. 旋转数组

```java
public void rotate(int[] nums, int k) {
  // 暴力解法
  if (nums == null) {
    return;
  }
  int temp,previous;
  for (int i = 0; i < k; i++) {
    previous = nums[nums.length - 1];
    for (int j = 0; j < nums.length; j++){
      temp = nums[j];
      nums[j] = previous;
      previous = temp;
    }
  }
}
public void rotate(int[] nums, int k) {
  // 空间换时间
  int[] a = new int[nums.length];
  for (int i = 0; i < nums.length; i++) {
    a[(i + k) % nums.length] = nums[i];
  }
  for (int i = 0; i < nums.length; i++) {
    nums[i] = a[i];
  }
}
public void rotate(int[] nums, int k) {
  // 使用环状替换
  k %= nums.length;
  int count = 0;
  for (int i = 0; count < nums.length; i++) {
    int current = i;
    int prev = nums[i];
    do {
      int next = (current + k) % nums.length;
      int temp = nums[next];
      nums[next] = prev;
      prev = temp;
      current = next;
      count++;
    } while (i != current);
  }
}

public void rotate(int[] nums, int k) {
  // 链表反转
  k %= nums.length;
  reverse(nums, 0, nums.length - 1);
  reverse(nums, 0, k - 1);
  reverse(nums, k, nums.length - 1);
}
public void reverse(int[] nums, int start, int end) {
  while (start < end) {
    int temp = nums[start];
    nums[start] = nums[end];
    nums[end] = temp;
    start++;
    end--;
  }
}
```



3. 合并两个有序链表

```java
// 迭代解法
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
  ListNode preNode = new ListNode(-1);
  ListNode prev = preNode;
  while (l1 != null && l2 != null) {
    if (l1.val < l2.val) {
      prev.next = l1;
      l1 = l1.next;
    } else {
      prev.next = l2;
      l2 = l2.next;
    }
    prev = prev.next;
  }
  prev.next = l1 == null ? l2 : l1;
  return preNode.next;
}
// 递归解法
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
  if (l1 == null) {
    return l2;
  } else if (l2 == null) {
    return l1;
  } else if(l1.val < l2.val) {
    l1.next = mergeTwoLists(l1.next, l2);
    return l1;
  } else {
    l2.next = mergeTwoLists(l1, l2.next);
    return l2;
  }
}
```



4. 合并两个有序数组

```java
public void merge(int[] nums1, int m, int[] nums2, int n) {
  System.arraycopy(nums2, 0, nums1, m, n);
  Arrays.sort(nums1);
}

public void merge(int[] nums1, int m, int[] nums2, int n) {
  // 双指针，从数组头开始
  int[] numsCopy = new int[m];
  System.arraycopy(nums1, 0, numsCopy, 0, m);
  int p1 = 0;
  int p2 = 0;
  int p3 = 0;
  while ((p1 < m) && (p2 < n)) {
    nums1[p3++] = numsCopy[p1] < nums2[p2] ? numsCopy[p1++] : nums2[p2++];
  }
  if (p1 < m) {
    System.arraycopy(numsCopy, p1, nums1, p1 + p2, m + n - p1 - p2);
  }
  if (p2 < n) {
    System.arraycopy(nums2, p2, nums1, p1 + p2, m + n - p1 - p2);
  }
}

public void merge(int[] nums1, int m, int[] nums2, int n) {
  // 双指针，从数组尾部开始
  int p1 = m - 1;
  int p2 = n - 1;
  int p3 = m + n - 1;
  while (p1 >= 0 && p2 >= 0) {
    nums1[p3--] = nums1[p1] < nums2[p2] ? nums2[p2--] : nums1[p1--];
  }
  System.arraycopy(nums2, 0, nums1, 0, p2 + 1);
}
```



5. 两数之和

```java
public int[] twoSum(int[] nums, int target) {
  int[] res = new int[2];
  Map<Integer, Integer> map = new HashMap<>();
  for (int i = 0; i < nums.length; i++) {
    if (map.containsKey(nums[i])) {
      res[0] = map.get(nums[i]);
      res[1] = i;
    }
    map.put(target - nums[i], i);
  }
  return res;
}
```



6. 移动零

```java
public void moveZeroes(int[] nums) {
  if (nums == null) {
    return;
  }
  int j = 0;
  for (int i = 0; i < nums.length; i++) {
    if (nums[i] != 0) {
      int temp = nums[i];
      nums[i] = nums[j];
      nums[j] = temp;
      j++;
    }
  }
}
```



7. 加一

```java
public int[] plusOne(int[] digits) {
  for (int i = digits.length - 1; i >= 0; i--) {
    digits[i]++;
    digits[i]%=10;
    if (digits[i] != 0) return digits;
  }
  digits = new int[digits.length + 1];
  digits[0] = 1;
  return digits;
}
```



8. 设计循环双端队列

```java
class MyCircularDeque {

    private int capacity;
    private int[] item;
    private int head;
    private int tail;


    /** Initialize your data structure here. Set the size of the deque to be k. */
    public MyCircularDeque(int k) {
        this.capacity = k + 1;
        item = new int[capacity];
        head = 0;
        tail = 0;
    }
    
    /** Adds an item at the front of Deque. Return true if the operation is successful. */
    public boolean insertFront(int value) {
        if (isFull()) return false;
        head = (head - 1 + capacity) % capacity;
        item[head] = value;
        return true;
    }
    
    /** Adds an item at the rear of Deque. Return true if the operation is successful. */
    public boolean insertLast(int value) {
        if (isFull()) return false;
        item[tail] = value;
        tail = (tail + 1) % capacity;
        return true;
    }
    
    /** Deletes an item from the front of Deque. Return true if the operation is successful. */
    public boolean deleteFront() {
        if (isEmpty()) return false;
        head = (head + 1) % capacity;
        return true;
    }
    
    /** Deletes an item from the rear of Deque. Return true if the operation is successful. */
    public boolean deleteLast() {
        if (isEmpty()) return false;
        tail = (tail - 1 + capacity) % capacity;
        return true;
    }
    
    /** Get the front item from the deque. */
    public int getFront() {
        if (isEmpty()) return -1;
        return item[head];
    }
    
    /** Get the last item from the deque. */
    public int getRear() {
        if (isEmpty()) return -1;
        return item[(tail - 1 + capacity) % capacity];
    }
    
    /** Checks whether the circular deque is empty or not. */
    public boolean isEmpty() {
        return head == tail;
    }
    
    /** Checks whether the circular deque is full or not. */
    public boolean isFull() {
        return (tail + 1) % capacity == head;
    }
}

/**
 * Your MyCircularDeque object will be instantiated and called as such:
 * MyCircularDeque obj = new MyCircularDeque(k);
 * boolean param_1 = obj.insertFront(value);
 * boolean param_2 = obj.insertLast(value);
 * boolean param_3 = obj.deleteFront();
 * boolean param_4 = obj.deleteLast();
 * int param_5 = obj.getFront();
 * int param_6 = obj.getRear();
 * boolean param_7 = obj.isEmpty();
 * boolean param_8 = obj.isFull();
 */
```



9. 接雨水

```java
// 暴力法
public int trap2(int[] height) {
  int ans = 0;
  int size = height.length;
  for (int i = 1; i < size - 1; i++) {
    int max_left = 0, max_right = 0;
    for (int j = i; j >= 0; j--) {
      max_left = Math.max(max_left, height[j]);
    }
    for (int j = i; j < size; j++) {
      max_right = Math.max(max_right, height[j]);
    }
    ans += Math.min(max_left, max_right) - height[i];
  }
  return ans;
}
// 双指针法
public int trap(int[] height) {
  int left = 0, right = height.length - 1;
  int ans = 0;
  int max_left = 0, max_right = 0;
  while (left < right) {
    if (height[left] < height[right]) {
      if (height[left] >= max_left) {
        max_left = height[left];
      } else {
        ans += (max_left - height[left]);
      }
      ++left;
    } else {
      if (height[right] >= max_right) {
        max_right = height[right];
      } else {
        ans += (max_right - height[right]);
      }
      --right;
    }
  }
  return ans;
}
```