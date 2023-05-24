# Leetcode-Python9
Stack and queue 1
## 232. Implement Queue using Stacks, 225. Implement Stack using Queues.

May 23, 2023  4h

The ninth day is for stack and queue.\
The challenges today are about how to realize the operations of the two data structures. While using stack to execute queue's operation, two stacks are needed. An in and an out. While using a queue to execute stack's operations, just one queue is needed.

## Introduction
[Reading link](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/%E6%A0%88%E4%B8%8E%E9%98%9F%E5%88%97%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.md)\
This article is written in C++.

## 232. Implement Queue using Stacks
[leetcode](https://leetcode.com/problems/implement-queue-using-stacks/)\
[reading](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0232.%E7%94%A8%E6%A0%88%E5%AE%9E%E7%8E%B0%E9%98%9F%E5%88%97.md)\
[video](https://www.bilibili.com/video/BV1nY4y1w7VC/?spm_id_from=333.788&vd_source=63f26efad0d35bcbb0de794512ac21f3)\
Stack follows the first in last out rule, while queue follows the first in first out rule.\
Here we use two stacks, an in one and an out one, to solve this question.
```python
class MyQueue:
    def __init__(self):
        """
        in is responsible for push, and out is responsible for pop
        """
        self.stack_in = []
        self.stack_out = []     

    def push(self, x: int) -> None:
        """
        有新元素进来，就往in里面push
        """
        self.stack_in.append(x)

    def pop(self) -> int:
        """
        Removes the element from in front of queue and returns that element.
        """
        if self.empty():
            return None
        #如果输出栈不为空，直接从出栈弹出数据就可以了。
        #输出栈如果为空，就把进栈数据全部导入进来，再从出栈弹出数据。
        if self.stack_out:
            return self.stack_out.pop()
        else:
            for i in range(len(self.stack_in)):
                self.stack_out.append(self.stack_in.pop())
            return self.stack_out.pop()

    def peek(self) -> int:
        """
        Get the front element.
        """
        #直接使用已有的pop函数
        ans = self.pop()
        #因为pop函数弹出了元素res，所以再添加回去
        self.stack_out.append(ans)
        return ans

    def empty(self) -> bool:
        """
        只要in或者out有元素，说明队列不为空
        """
        return not (self.stack_in or self.stack_out)
```

## 225. Implement Stack using Queues
[leetcode](https://leetcode.com/problems/implement-stack-using-queues/)\
[reading](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0225.%E7%94%A8%E9%98%9F%E5%88%97%E5%AE%9E%E7%8E%B0%E6%A0%88.md)\
[video](https://www.bilibili.com/video/BV1Fd4y1K7sm/?spm_id_from=pageDriver&vd_source=63f26efad0d35bcbb0de794512ac21f3)\
To use one queue to realize stack's operations, we can select the peek number and **put back to the front of the queue**, until the desired number becomes the peek of the queue. In this way, we won't need two queues for this question.
```python
class MyStack:
    def __init__(self):
        self.que = deque()

    def push(self, x: int) -> None:
        """
        元素 x 入栈
        put elemnet x into the stack, using queue to realize this.
        """
        self.que.append(x)

    def pop(self) -> int:
        """移除栈顶元素"""
        if self.empty():
            return None
        # get the top n-1 element, and put back to the front of the queue.
        for i in range(len(self.que)-1):
            self.que.append(self.que.popleft())
        return self.que.popleft()

    def top(self) -> int:
        """获取栈顶元素, 是队列的尾部元素"""
        if self.empty():
            return None
        return self.que[-1]

    def empty(self) -> bool:
        """返回栈是否为空"""
        return not self.que
```









