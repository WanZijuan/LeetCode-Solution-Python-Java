# 24 - 交换相邻结点

## 题目描述
![problem](images/24.png)

## 解法一
1. 将链表遍历一遍取出value值；
2. 按相邻节点（奇偶下标）交换的顺序连接起来。
虽然方法很蠢，但是过了哈哈哈哈
>2018.01.20 review : 这个蠢蠢的方法不符合题意啊大哥༼༎ຶᴗ༎ຶ༽
```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def swapPairs(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        lists = []
        while head:
            lists.append(head.val)
            head = head.next
        for i in range( 0, len(lists), 2 ):
            if i + 1 < len(lists):
                lists[i], lists[i+1] = lists[i+1], lists[i]
        
        h = ListNode(0)
        node = h
        for i in range(len(lists)):
            node.next = ListNode(lists[i])
            node = node.next
        return h.next
            
head = ListNode(1)
node = head
for i in range(4):
    node.next = ListNode(i+2)
    node = node.next

s = Solution()
r = s.swapPairs(head)
while r:
    print(r.val)
    r = r.next
```

## 解法二
1. 加个dummy结点指向头结点；
2. 每隔一个结点原地交换一下；
```python
class Solution:
    def swapPairs(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        dummy = ListNode(0)
        dummy.next = head
        prev = dummy
        cur = head
        
        while cur and cur.next:
            prev.next = cur.next
            cur.next = cur.next.next
            prev.next.next = cur
            prev = cur
            cur = cur.next
        return dummy.next
```

## 解法三
递归:虽然能看懂人家的代码，但是要怎么才能自己想到这样的解决办法呢，哎。递归过程如下：
![progress](images/progress.jpg)
```python
class Solution:
    def swapPairs(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if head == None or head.next == None:
            return head
        tmp = head.next
        head.next = swapPairs(tmp.next)
        tmp.next = head
        return tmp
```