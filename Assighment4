# DSA Assignment #4: 线性结构

*Updated 2026-03-23 22:22 GMT+8*
 *Compiled by <mark>肖云天、生命科学学院</mark> (2026 Spring)*
<font color='pink'>粉色代表这道题是已知知识点的困难题目</font>

<font color='skyblue'>天蓝色代表这道题是新知识点，需要记忆</font>




>**说明：**
>
>1. **解题与记录：**
>
>     对于每一个题目，请提供其解题思路（可选），并附上使用Python或C++编写的源代码（确保已在OpenJudge， Codeforces，LeetCode等平台上获得Accepted）。请将这些信息连同显示“Accepted”的截图一起填写到下方的作业模板中。（推荐使用Typora https://typoraio.cn 进行编辑，当然你也可以选择Word。）无论题目是否已通过，请标明每个题目大致花费的时间。
>
>2. **提交安排：**提交时，请首先上传PDF格式的文件，并将.md或.doc格式的文件作为附件上传至右侧的“作业评论”区。确保你的Canvas账户有一个清晰可见的本人头像，提交的文件为PDF格式，并且“作业评论”区包含上传的.md或.doc附件。
> 
>3. **延迟提交：**如果你预计无法在截止日期前提交作业，请提前告知具体原因。这有助于我们了解情况并可能为你提供适当的延期或其他帮助。  
>
>请按照上述指导认真准备和提交作业，以保证顺利完成课程要求。



## 1. 题目

### <font color='skyblue'>E160.相交链表</font>

hash table, linked list, two pinters, https://leetcode.cn/problems/intersection-of-two-linked-lists/

思路：
方法二：双指针
思路和算法

使用双指针的方法，可以将空间复杂度降至 O(1)。

只有当链表 headA 和 headB 都不为空时，两个链表才可能相交。因此首先判断链表 headA 和 headB 是否为空，如果其中至少有一个链表为空，则两个链表一定不相交，返回 null。

当链表 headA 和 headB 都不为空时，创建两个指针 pA 和 pB，初始时分别指向两个链表的头节点 headA 和 headB，然后将两个指针依次遍历两个链表的每个节点。**具体做法如下**：

- 每步操作需要同时更新指针 pA 和 pB。

- 如果指针 pA 不为空，则将指针 pA 移到下一个节点；如果指针 pB 不为空，则将指针 pB 移到下一个节点。

- 如果指针 pA 为空，则将指针 pA 移到链表 headB 的头节点；如果指针 pB 为空，则将指针 pB 移到链表 headA 的头节点。

- 当指针 pA 和 pB 指向同一个节点或者都为空时，返回它们指向的节点或者 null。

**证明**

下面提供双指针方法的正确性证明。考虑两种情况，第一种情况是两个链表相交，第二种情况是两个链表不相交。

情况一：两个链表相交

链表 headA 和 headB 的长度分别是 m 和 n。假设链表 headA 的不相交部分有 a 个节点，链表 headB 的不相交部分有 b 个节点，两个链表相交的部分有 c 个节点，则有 a+c=m，b+c=n。

如果 a=b，则两个指针会同时到达两个链表相交的节点，此时返回相交的节点；

如果 a！=b，则指针 pA 会遍历完链表 headA，指针 pB 会遍历完链表 headB，两个指针不会同时到达链表的尾节点，然后指针 pA 移到链表 headB 的头节点，指针 pB 移到链表 headA 的头节点，然后两个指针继续移动，在指针 pA 移动了 a+c+b 次、指针 pB 移动了 b+c+a 次之后，两个指针会同时到达两个链表相交的节点，该节点也是两个指针第一次同时指向的节点，此时返回相交的节点。

情况二：两个链表不相交

链表 headA 和 headB 的长度分别是 m 和 n。考虑当 m=n 和 m
！=n 时，两个指针分别会如何移动：

如果 m=n，则两个指针会同时到达两个链表的尾节点，然后同时变成空值 null，此时返回 null；

如果 m！=n，则由于两个链表没有公共节点，两个指针也不会同时到达两个链表的尾节点，因此两个指针都会遍历完两个链表，在指针 pA 移动了 m+n 次、指针 pB 移动了 n+m 次之后，两个指针会同时变成空值 null，此时返回 null。



代码：<font color='skyblue'>即便知道了核心原理，写出代码也是不容易的。核心就是在指针达到尾节点的下一个None后再进行跳转</font>

```python
class Solution:  
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:  
        if not headA or not headB:  
            return None  
        node_a=headA  
        node_b=headB  
        while node_a != node_b:#如果两个链表有焦点，那么他们一定会在走完lenA+lenB之前在焦点相遇  
            node_a=node_a.next if node_a else headB  
            node_b=node_b.next if node_b else headA#if node_x判断是否走到尽头，如果一个走到尽头而另外一个没有的话，、  
#那么他们一定都要走到None这一步，因此到达终点时需要的步数仍旧是一样的，就相当于None是每个列表的尾节点  
#如果两个链表同时到达None就直接输出None了；反之则能够成为达到末尾的标志，进而实现跳转。  
        return node_a
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20260329164121.png]]




### <font color='skyblue'>E206.反转链表</font>

recursion, linked list, https://leetcode.cn/problems/reverse-linked-list/


思路：
1.递归方法
**`recursion`将以 `curr` 为头节点的链表反转，并把 `prev` 作为 `curr` 的前一个节点接在后面**
返回头节点以代表整个链表
基础：
```python
function print_values_in_reverse(ListNode head)
    if head is NOT null
        print_values_in_reverse(head.next)
        print head.val
```


代码：

```python
class Solution:  
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:  
        def recursion(curr,prev):#给出当前节点和前一个节点之后，将前一个结点及其之后的所有节点都反转并返回头节点  每次输入在当前层就要反转顺序d的两个节点
            if not curr:  
                return prev#终止条件：没有值需要指向prev，即为prev是反转后头节点  
            res=recursion(curr.next,curr)#1.将后续的全部链表指针反转后输出头节点  
            curr.next=prev#2.将本次要反转的两个节点顺序反转  
            return res#res代表反转过后的链表的头节点  
        return recursion(head,None)
```

2.不需要使用prev数值传入，只需要依次遍历相邻两项并逐个修改就可以了
```python
    def reverse_list(self, head):
        previous = None
        current = head
        while current is not None:
            next_node = current.next
            current.next = previous
            previous = current
            current = next_node
        return previous

```

代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20260329165930.png]]




### <font color='skyblue'>M234.回文链表</font>

linked list, two pointers, https://leetcode.cn/problems/palindrome-linked-list/

<mark>请用快慢指针实现</mark> `O(1)` 空间复杂度。

思路：
1.递归
- **递归天然实现了从后往前访问**
    
- **`self.front_pointer` 实现了从前往后移动**
    
- 两者配合，同时从两端向中间比较

代码：

```python
class Solution:  
    def isPalindrome(self, head: Optional[ListNode]) -> bool:  
        self.front=head  
        def recursion(curr=head):  
            if curr==None:  
                return True  
            else:  
                if not recursion(curr.next):  
                    return False  
                elif self.front.val!=curr.val:  
                    return False  
                else:  
                    self.front=self.front.next  
            return True  
        return recursion(head)
```
思路：
2.双指针判断中点+反转链表
避免使用 O(n) 额外空间的方法就是改变输入。

我们可以将链表的后半部分反转（修改链表结构），然后将前半部分和后半部分进行比较。比较完成后我们应该将链表恢复原样。虽然不需要恢复也能通过测试用例，但是使用该函数的人通常不希望链表结构被更改。

该方法虽然可以将空间复杂度降到 O(1)，但是在并发环境下，该方法也有缺点。在并发环境下，函数运行时需要锁定其他线程或进程对链表的访问，因为在函数执行过程中链表会被修改。

算法

整个流程可以分为以下五个步骤：

找到前半部分链表的尾节点。
反转后半部分链表。
判断是否回文。
恢复链表。
返回结果。

代码：
```python
class Solution:  
    def isPalindrome(self, head: Optional[ListNode]) -> bool:  
        def end_of_first_half(head):  
            if not head:  
                return None  
            else:  
                slow,fast=head,head  
                while fast.next and fast.next.next:#保证不是已经到达末尾，且先检验.next防止报错  
                    slow=slow.next  
                    fast=fast.next.next  
                return slow  
  
        def reverse(curr,prev):  
            if not curr:  
                return prev  
            else:  
                res=reverse(curr.next,curr)  
                curr.next=prev  
                return res  
  
        if not head:  
            return True  
        mid=end_of_first_half(head)  
  
        head_2=reverse(mid.next,None)  
        mid.next = None  
        p1=head  
        p2=head_2  
        while p2:  
            if p2.val!=p1.val:  
                return False  
            else:  
                p1=p1.next  
                p2=p2.next  
        return True
```
还是好丑。但至少通过了

代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20260329203601.png]]
**![[Pasted image 20260329215300.png]]**




### <font color='skyblue'>M24591:中序表达式转后序表达式</font><font color='red'>调度场算法</font>


stack, http://cs101.openjudge.cn/practice/24591/

思路：
其实中缀表达式之所以难处理，本质上就是因为运算符[优先级](https://zhida.zhihu.com/search?content_id=120938058&content_type=Article&match_order=1&q=%E4%BC%98%E5%85%88%E7%BA%A7&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3NzUwNTEzMjMsInEiOiLkvJjlhYjnuqciLCJ6aGlkYV9zb3VyY2UiOiJlbnRpdHkiLCJjb250ZW50X2lkIjoxMjA5MzgwNTgsImNvbnRlbnRfdHlwZSI6IkFydGljbGUiLCJtYXRjaF9vcmRlciI6MSwiemRfdG9rZW4iOm51bGx9.AuMH46yMV28agVsjXd31ZU1Qjf3IUU89BlJP46zKmZ8&zhida_source=entity)。如果我们把表达式全部按优先级加上括号，把`3+5*4^2-1`变成`(3+(5*(4^2)))-1`，很容易递归地计算。但是，“按优先级加括号”并不是很好实现，所以我们换一种思路，仍使用**栈**来解决问题。

为什么要使用栈？因为当我们读到a+b时，我们并不知道后面是`a+b+c`还是`a+b*c`，所以不能立刻转化为`a b +`，而要暂缓一步，把加号存到栈里，等到有了足够的信息时，再把它放出来。

什么时候有_足够的信息_呢，不妨倒过来想。

假设**乘方**是表达式里优先级最高的运算，那我们一读到`a^b`，不管b后面是什么运算符，都可以立刻把它变成`a b ^`。

对于**乘法**，可能有`a*b^c^d^...`这样的长链，但一旦我们读到另一个**`*`**或者一个**`+`**，形成了`a*b^c^d^...*`或`a*b^c^d^...+`的形式，前面那个**`*`**便可以放心地放于此符号之前。

而**加法**也是类似，但是放出来的条件仅有读到另一个**`+`**。

归纳一下发现，栈顶的运算符可以被弹出的条件是其**优先级不低于新读入的运算符**。当然，当表达式结束时，也要把栈里剩余的运算符依次弹出。

一般地，我们采取这样的算法：

1. 依次按顺序读入，

2. 读到数字：直接输出；
3. 读到运算符：如果栈顶的运算符优先级不低于该运算符，则输出栈顶运算符并使之出栈，直到栈空或不满足上述条件为止；然后入栈。

4. 当读入完毕时，依次输出并弹出栈顶运算符，直到栈被清空。

[Wikipedia](https://link.zhihu.com/?target=https%3A//zh.wikipedia.org/wiki/%25E8%25B0%2583%25E5%25BA%25A6%25E5%259C%25BA%25E7%25AE%2597%25E6%25B3%2595)上有一张图片描绘了这个过程：

![](https://picx.zhimg.com/v2-5d60fe34ae244a296cd3562617facea7_1440w.jpg)

Salix alba绘制的示意图

## 处理括号

括号的优先级是多少？你可能条件反射地说，括号的优先级当然是最高的。但是，在调度场算法中，这样的处理会出问题——如果简单地把括号当成一种拥有最高优先级的运算符，当你读到左括号就立刻输出了，这当然不对。

恰恰相反，我们得把左括号的优先级当作最低。不仅如此，还必须在算法中对括号特别处理。注意，后缀表达式里没有括号，所以括号不应该被输出。由于括号里一定是一个完整的表达式，所以可以这样修改算法：

1. 依次按顺序读入，

2. 读到数字：直接输出；
3. 读到**一般**运算符：如果栈顶的运算符优先级不低于该运算符，则输出栈顶运算符并使之出栈，直到栈空或不满足上述条件为止；然后入栈；
4. 读到**左括号**：直接入栈；
5. 读到**右括号**：输出栈顶运算符并使之出栈，直到栈顶为左括号为止；令左括号出栈。

6. 当读入完毕时，依次输出并弹出栈顶运算符，直到栈被清空。
from
[算法学习笔记(39): 调度场算法 - 知乎](https://zhuanlan.zhihu.com/p/147623236)
小数的处理需要使用到==正则表达式==
```python
import re
def tokenize_expression(expression):
    """将表达式分割为数字和运算符的列表"""
    # 匹配：数字（包括小数）、运算符（+-*/）、括号等
    pattern = r'\d+\.?\d*|[+\-*/()]'
    tokens = re.findall(pattern, expression)
    return tokens
```
```text
\d+     # 匹配一个或多个数字（0-9）
\.?     # 匹配零个或一个小数点
\d*     # 匹配零个或多个数字
[+\-*/()]  # 字符集，匹配其中任意一个字符
| #或
tokens为列表
`\-` 中的 `\` 是**转义字符**，用于告诉正则表达式引擎：这里的 `-` 是**字面意义的连字符**，而不是特殊意义的范围符号。
```

代码：

```python
import re  
def main():  
    priority={'+':1,'-':1,'*':2,'/':2,'(':0}#处于一致性原则，虽然(的运算方式不与其他符号严格相同，但是为了方便放入过程，将其赋予0的优先级  
    others={'+','-','*','/','(',')'}  
    n=int(input())  
    while True:  
        try:  
            hi=input().strip()  
            pattern=r'\d+\.?\d*|[+\-*/()]'  
            tokens=re.findall(pattern,hi)  
            res = []  
            stack = []  
            for i in tokens:  
                if i not in others:  
                    res.append(i)  
                else:  
                    if i != ')':  
                        if not stack or priority[stack[-1]]<priority[i]:  
                            stack.append(i)  
                        else:  
                            if i=='(':  
                                stack.append(i)  
                            else:  
                                while stack and priority[stack[-1]]>=priority[i]:  
                                    a=stack.pop()  
                                    res.append(a)  
                                stack.append(i)  
                    else:  
                        while stack[-1]!='(':  
                            a=stack.pop()  
                            res.append(a)  
                        stack.pop()  
            while stack:  
                res.append(stack.pop())  
            print(*res)  
  
  
        except EOFError :  
            break  
  
if __name__ == '__main__':  
    main()
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20260330223213.png]]




### <font color='skyblue'>M146.LRU缓存</font>

#hash table, #doubly-linked list, https://leetcode.cn/problems/lru-cache/
请你设计并实现一个满足  [LRU (最近最少使用) 缓存](https://baike.baidu.com/item/LRU) 约束的数据结构。

实现 `LRUCache` 类：

- `LRUCache(int capacity)` 以 **正整数** 作为容量 `capacity` 初始化 LRU 缓存
- `int get(int key)` 如果关键字 `key` 存在于缓存中，则返回关键字的值，否则返回 `-1` 。
- `void put(int key, int value)` 如果关键字 `key` 已经存在，则变更其数据值 `value` ；如果不存在，则向缓存中插入该组 `key-value` 。如果插入操作导致关键字数量超过 `capacity` ，则==**应该 逐出 最久未使用的关键字**。==

函数 `get` 和 `put` 必须以 `O(1)` 的平均时间复杂度运行。
思路：
在 Python 语言中，有一种结合了哈希表与双向链表的数据结构 OrderedDict，只需要短短的几行代码就可以完成本题。在 Java 语言中，同样有类似的数据结构 LinkedHashMap。

**小贴士**

在双向链表的实现中，使用一个**伪头部**（dummy head）和**伪尾部**（dummy tail）标记界限，这样在添加节点和删除节点的时候就不需要检查相邻的节点是否存在。
==注意本题中，Dnode需要自己先定义==


代码

```python
class Dlinknode:  
    def __init__(self,value=None,key=None):  
        self.value=value  
        self.next=None  
        self.prev=None  
        self.key=key  
  
class LRUCache:  
  
    def __init__(self, capacity: int):  
        dummy1=Dlinknode()  
        dummy2=Dlinknode()  
        self.capacity=capacity  
        self.keys=dict()#使用哈希表建立key与node之间的关系 严格来说应该命名为self.cache或者self.key_to_node  
        self.head=dummy1  
        self.tail=dummy2#这里发现，在头部添加节点时，头部的后一个不一定存在！因此，将头部的next初始化为dummy尾。反之类似。  
        self.head.next=dummy2  
        self.tail.prev=dummy1  
        self.size=0  
    def get(self, key: int) -> int:  
        if key not in self.keys:  
            return -1  
        else:  
            node=self.keys[key]  
            self.moveToHead(node)  
            return node.value  
  
    def put(self, key: int, value: int) -> None:  
        if key not in self.keys:  
            node=Dlinknode(value,key)  
            self.keys[key]=node  
            self.addToHead(node)  
            self.size+=1  
            if self.size > self.capacity:  
                a=self.removeTail()  
                self.keys.pop(a.key)#这里需要弹出a.key!!!  
                self.size-=1  
        else:  
            node=self.keys[key]  
            node.value=value  
            self.moveToHead(node)  
  
  
    def addToHead(self,node):#定义一些辅助函数来更好地进行操作  
        node.prev=self.head  
        node.next=self.head.next  
        self.head.next.prev=node  
        self.head.next=node  
  
    def removeNode(self,node):  
        node.prev.next=node.next  
        node.next.prev=node.prev#至于node的相关前后，由node移动到的地方决定，到那时再更改这两个值就可以  
  
    def moveToHead(self,node):  
        self.removeNode(node)  
        self.addToHead(node)  
  
    def removeTail(self):  
        node=self.tail.prev  
        self.removeNode(node)  
        return node #方便进行后续的哈希表删除操作  
# Your LRUCache object will be instantiated and called as such:  
# obj = LRUCache(capacity)  
# param_1 = obj.get(key)  
# obj.put(key,value)
```



<mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20260331001344.png]]




### <font color='pink'>P2698 [USACO12MAR] </font><font color='skyblue'>Flowerpot S</font>

#monotonic_queue, https://www.luogu.com.cn/problem/P2698

思路：
  **数学转化**：在按 $x$ 坐标排序后的水滴序列中，找到一个子序列 $[i, j]$，满足 $\max(y_i \dots y_j) - \min(y_i \dots y_j) \ge D$，且最小化 $x_j - x_i$。
><font color='pink'>**解题思路**</font>
>
> 1.  **排序**：首先将所有水滴按 $x$ 坐标从小到大排序。
> 2.  **双指针**：使用左右两个指针 `l` 和 `r` 维护一个窗口。
>     *   右指针 `r` 不断向右移动，增加窗口内的水滴。
>     *   当窗口内的 $\max(y) - \min(y) \ge D$ 时，尝试收缩左指针 `l`，以减小窗口宽度并更新全局最小值。
> 3.  **单调队列**：为了高效地在 $O(1)$ 时间内获取当前窗口内的最大值和最小值，我们维护两个单调队列：
>     *   `max_q`：单调递减队列，队头存储当前窗口 $y$ 的最大值。
>     *   `min_q`：单调递增队列，队头存储当前窗口 $y$ 的最小值。

单调队列与单调栈的理念相似，重要的是什么情况下栈内的一些内容可以被丢掉
而在这道题中，以单调队列的max_q为例，如果新加入的值大于原来的一些旧值，那么这些旧值就可以丢弃了--即使指针范围改变，只要新值没有被丢掉，那么旧值的有无都不会影响最大值的值。（因为至少是新值）
代码

```python
from collections import deque  
N,D=map(int,input().strip().split())  
ls=[]  
for _ in range(N):  
    ls.append(tuple(map(int,input().strip().split())))  
ls.sort(key=lambda x:x[0])  
max_q=deque()  
min_q=deque()  
l=0  
res=float('inf')  
for r in range(N):  
    while max_q and ls[max_q[-1]][1]<=ls[r][1]:#在最大值出队时判断的依据是索引值  
        #这里使用<=，是因为同样地，前一个当前值的最大值有无不影响最大值实际结果，且由于最大值出队的依据是l索引，因此两个该值都会在正确的地方被移除  
        max_q.pop()  
    max_q.append(r)  
    while min_q and ls[min_q[-1]][1]>=ls[r][1]:  
        min_q.pop()  
    min_q.append(r)  
    while ls[max_q[0]][1]-ls[min_q[0]][1]>=D:  
        res=min(res,ls[r][0]-ls[l][0])  
        l+=1#尝试收缩，直到遍历完最小的可能；之后l再右移，放弃当前组合，来尝试新r下的更小值（不放弃当然也可以，但是会大大复杂代码逻辑）  
        if max_q[0]<l:#这里注意！l,r是索引，index,x,y是三个独立的值。因此，正确的做法应该是在max_q中储存索引来代表，防止此处比较位置（索引值）的困难  
            max_q.popleft()  
        if min_q[0]<l:  
            min_q.popleft()  
if res==float('inf'):  
    print('-1')  
else:  
    print(res)
```



<mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20260331161221.png]]




## 2. 学习总结和个人收获

<mark>如果发现作业题目相对简单，有否寻找额外的练习题目，如“数算2026spring每日选做”、LeetCode、Codeforces、洛谷等网站上的题目。</mark>

需要增加练习：
tag #链表 #栈 #单调栈



