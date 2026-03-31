# Assignment #2: 位运算、前缀和、树状数组、归并排序 & 状态压缩

*Updated 2026-03-10 11:00 GMT+8*
 *Compiled by <mark>肖云天、生命科学学院</mark> (2026 Spring)*
<font color='pink'>粉色代表这道题来自于已知的知识点但没能想出正确的思路,查看了题解</font>

<font color='skyblue'>天蓝色代表这道题包含了之前没有掌握的语法/数据结构/算法,有迹可循</font>


**作业的各项评分细则及对应的得分**

| 标准                                 | 等级                                                         | 得分 |
| ------------------------------------ | ------------------------------------------------------------ | ---- |
| 按时提交                             | 完全按时提交：1分<br/>提交有请假说明：0.5分<br/>未提交：0分  | 1 分 |
| 源码、耗时（可选）、解题思路（可选） | 提交了4个或更多题目且包含所有必要信息：1分<br/>提交了2个或以上题目但不足4个：0.5分<br/>少于2个：0分 | 1 分 |
| AC代码截图                           | 提交了4个或更多题目且包含所有必要信息：1分<br/>提交了2个或以上题目但不足4个：0.5分<br/>少于：0分 | 1 分 |
| 清晰头像、PDF文件、MD/DOC附件        | 包含清晰的Canvas头像、PDF文件以及MD或DOC格式的附件：1分<br/>缺少上述三项中的任意一项：0.5分<br/>缺失两项或以上：0分 | 1 分 |
| 学习总结和个人收获                   | 提交了学习总结和个人收获：1分<br/>未提交学习总结或内容不详：0分 | 1 分 |
| 总得分： 5                           | 总分满分：5分                                                |      |
>
>
>
>**说明：**
>
>1. **解题与记录：**
>
>      对于每一个题目，请提供其解题思路（可选），并附上使用Python或C++编写的源代码（确保已在OpenJudge， Codeforces，LeetCode等平台上获得Accepted）。请将这些信息连同显示“Accepted”的截图一起填写到下方的作业模板中。（推荐使用Typora https://typoraio.cn 进行编辑，当然你也可以选择Word。）无论题目是否已通过，请标明每个题目大致花费的时间。
>
>2. **课程平台：**课程网站位于Canvas平台（https://pku.instructure.com ）。该平台将在<mark>第2周</mark>选课结束后正式启用。在平台启用前，请先完成作业并将作业妥善保存。待Canvas平台激活后，再上传你的作业。
>
>3. **提交安排：**提交时，请首先上传PDF格式的文件，并将.md或.doc格式的文件作为附件上传至右侧的“作业评论”区。确保你的Canvas账户有一个清晰可见的本人头像，提交的文件为PDF格式，并且“作业评论”区包含上传的.md或.doc附件。
>3. **延迟提交：**如果你预计无法在截止日期前提交作业，请提前告知具体原因。这有助于我们了解情况并可能为你提供适当的延期或其他帮助。  
>
>请按照上述指导认真准备和提交作业，以保证顺利完成课程要求。



## 1. 题目

### E868.二进制间距

bit manipulation, https://leetcode.cn/problems/binary-gap/

> 主要是练习面向对象编程写法，这样力扣题目，笔试都没有问题了。机考时候，不是必须OOP，能AC就可以。
>

思路：



代码：

```python
class Solution:  
    def binaryGap(self, n: int) -> int:  
        k=n.bit_length()  
        count=0  
        maximum=0  
        exist=False  
        for i in range(k):  
            if n&1 == 1:  
                if not exist:  
                    exist=True  
                else:  
                    count+=1  
                    maximum=max(maximum,count)  
                    count=0  
            else:  
                if exist:  
                    count+=1  
            n>>=1  
        return maximum
```
显然，LC官方题解的方法是更加漂亮的。与其一个一个计数，不如在找到1位置之后与前一个1的位置相减。
```python
class Solution:
    def binaryGap(self, n: int) -> int:
        last, ans, i = -1, 0, 0#last负责标记上一个1出现的位置，如果没有出现过1，则默认为-1.
        while n:
            if n & 1:
                if last != -1:
                    ans = max(ans, i - last)
                last = i
            n >>= 1
            i += 1
        return ans
```


代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20260320140258.png]]




### M304.二维区域和检索 - 矩阵不可变

prefix sum, https://leetcode.cn/problems/range-sum-query-2d-immutable/


思路：
很经典的二维前缀和，上个学期讲过，这个学期也算正式实现了
挺好
代码：

```python
from typing import List  
class NumMatrix:  
  
    def __init__(self, matrix: List[List[int]]):  
        r=len(matrix)  
        c=len(matrix[0])  
        self.prefix_sum=[[0]*(c+1) for _ in range(r+1)]  
        for row in range(1,r+1):  
            for col in range(1,c+1):  
                self.prefix_sum[row][col]=self.prefix_sum[row][col-1]+self.prefix_sum[row-1][col]\  
                                     -self.prefix_sum[row-1][col-1]+matrix[row-1][col-1]  
  
    def sumRegion(self, row1: int, col1: int, row2: int, col2: int) -> int:  
        return (self.prefix_sum[row2+1][col2+1]-self.prefix_sum[row2+1][col1]  
                -self.prefix_sum[row1][col2+1]+self.prefix_sum[row1][col1])  
  
# Your NumMatrix object will be instantiated and called as such:  
# obj = NumMatrix(matrix)  
# param_1 = obj.sumRegion(row1,col1,row2,col2)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20260320143242.png]]



### <font color='skyblue'>M1680.连接连续二进制数字</font>

bit manipulation, https://leetcode.cn/problems/concatenation-of-consecutive-binary-numbers/



思路：
注意取模。代码实现时，可以在循环内取模。为什么可以在中途取模？原理见 [模运算的世界：当加减乘除遇上取模](https://leetcode.cn/circle/discuss/mDfnkW/)。
**in another word,这个部分进行的操作可以理解为将res先乘以2的n次方，再加上某一个数字。而模运算对加法和乘法是保持的。**


代码：

```python
class Solution:  
    def concatenatedBinary(self, n: int) -> int:  
        res=0  
        for i in range(1,n+1):  
            res<<=i.bit_length()  
            res = (res|i)%(10**9+7)  #这里建议合并为一行，要不然Deepseek会报错（
        return res
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20260320152833.png]]




### M1461.检查一个字符串是否包含所有长度为 K 的二进制子串

bit manipulation, https://leetcode.cn/problems/check-if-a-string-contains-all-binary-codes-of-size-k/



思路：



代码：

```python
class Solution:  
    def hasAllCodes(self, s: str, k: int) -> bool:  
        nums_occurred=set()  
        if (2**k)>len(s):  
            return False  
        for i in range(0,len(s)-k+1):  
            nums_occurred.add(int(s[i:i+k],2))  
        if len(nums_occurred)==(2**k):  
            return True  
        else:  
            return False
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### <font color='skyblue'>M30178:（超出范围）数字华容道（Easy Version）</font>

merge sort, binary indexed tree, http://cs101.openjudge.cn/practice/30178/

思路：
这道题的特点是很难从简单样例进行模拟（imitation）来寻找规律。因此，需要从抽象的角度来理解这个问题。
我和AI探讨了40分钟的可解性证明问题，**仍旧没能理解**。
**不加证明地，我们指出以下事实：Johnson & Story (1879)**
*   **$N$** = 逆序对的总数（序列中大的数排在小的数前面的情况总数）。
*   **$R$** = 空格所在的行数（从下往上数，第 1 行、第 2 行……）。
结论：
*   **如果 $n$ 是奇数**：只要 $N$ 是**偶数**，拼图就一定可解。
*   **如果 $n$ 是偶数**：
    *   当空格在**从下往上数奇数行**（1, 3, 5...）时，要求 $N$ 是**偶数**。
    *   当空格在**从下往上数偶数行**（2, 4, 6...）时，要求 $N$ 是**奇数**。
    *   *（口诀：$N+R$ 必须是奇数）*
因此，原问题转化为了计算逆序对数的问题。
#### <font color='skyblue'>NEW!!~逆序对的计算方法：~</font>
**1.归并排序（new)**
对于每个数组，将其排序的方法可以是将其分成两半，每一半进行排序之后再一位一位拼在一起。
而在需要count逆序对的方法就在拼在一起的过程中：如果一个数组是顺序的，那么理论上两边排完序后每个右面的所有数字都应该比左面的大。如果存在左面的数a比右面的数b大的话，那么（a,...）与b都构成逆序对。
总逆序对数为左逆序+右逆序+二者之间。
**2.树状数组（new)**
树状数组的优势在于可以同时高效地计算前缀和与实现实时更新。如果某个数字出现了，就将数组的这一位设为1；那么每个数字的前缀和就是已经出现的比它小（<=）的数字个数。相减即可得到答案。
代码：

```python
n=int(input().strip())  
maze=[]  
for _ in range(n):  
    maze.append(list(map(int, input().strip().split())))  
def merge_count(arr):  
    if len(arr)<=1:  
        return arr,0  
    else:  
        mid=len(arr)//2  
        left,a=merge_count(arr[:mid])  
        right,b=merge_count(arr[mid:])  
        inv=a+b  
        i,j=0,0  
        res=[]  
        while i<len(left) and j<len(right):  
            if left[i]<=right[j]:  
                res.append(left[i])  
                i+=1  
            else:  
                res.append(right[j])  
                inv += len(left)-i  
                j+=1  
        if i<len(left):  
            res.extend(left[i:])  
        elif j<len(right):  
            res.extend(right[j:])  
    return res,inv  
def main():  
    flattened=[]  
    for row in range(n):  
        for col in range(n):  
            if maze[row][col]==0:  
                row_of_0=row  
            else:  
                flattened.append(maze[row][col])  
    _,inv=merge_count(flattened)  
  
    if n%2!=0:  
        if inv%2==0:  
            print('yes')  
        else:  
            print('no')  
    else:  
        if (inv+row_of_0)%2!=0:  
            print('yes')  
        else:  
            print('no')  
if __name__=='__main__':  
    main()
```
```python
class FenwickTree:  
    def __init__(self,size):  
        self.tree=[0]*(size+1)  
    def update(self,i,delta):  
        while i<len(self.tree):  
            self.tree[i]+=delta  
            i+=i&(-i)  
    def query(self,i):  
        s=0#初始和  
        while i>0:  
            s+=self.tree[i]  
            i-=i&(-i)  
        return s  

  
def main():  
    n = int(input().strip())  
    maze = []  
    for _ in range(n):  
        maze.append(list(map(int, input().strip().split())))  
    inv=0  
    flattened=[]  
    for row in range(n):  
        for col in range(n):  
            if maze[row][col]==0:  
                row_of_0=row  
            else:  
                flattened.append(maze[row][col])  
    tree=FenwickTree(n*n)  
    for i,num in enumerate(flattened):  
        tree.update(num,1)  
        inv+=i+1-tree.query(num)  
  
  
    if n%2!=0:  
        if inv%2==0:  
            print('yes')  
        else:  
            print('no')  
    else:  
        if (inv+row_of_0)%2!=0:  
            print('yes')  
        else:  
            print('no')  
if __name__=='__main__':  
    main()
```


代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20260320213956.png]]
![[Pasted image 20260320220921.png]]
两个方法的内存和时间对比


### <font color='pink'>T30201: 旅行售货商问题</font>

bitmask dp, http://cs101.openjudge.cn/practice/30201/

思路：
虽然做过一遍了，但是再次遇到这个问题时还是没能第一时间想出来怎么做。
`dp[mask][i]`代表经过路径为mask，现在在i位置时所需要的最小价格。由于所经过路径的mask1一定比所经过路径的任意子集maski大，因此在引用到`dp[mask][i]`时，它一定就是最小值。
我们需要i变量，因为这个路径连接到下一个节点所需要的价格与最后所处的位置有关。
初始状态为从0开始，即mask=001，i=0，dp=0.

代码：

```python
def main():  
    n=int(input().strip())  
    cost=[]  
    for _ in range(n):  
        cost.append(list(map(int, input().strip().split())))  
    full_mask=(1<<n)-1  
    INF=float('inf')  
    dp = [[INF]*n for _ in range(1<<n)]  
    dp[1][0]=0  
    for mask in range(1<<n):  
        for i in range(n):  
            if dp[mask][i]==INF:#以当前的路径不可能现在处于i位置  
                continue  
            for j in range(n):  
                if mask & (1<<j):#路径中已经包含了j位置，不能往回走  
                    continue  
                new_mask=mask|(1<<j)  
                new_cost=cost[i][j]+dp[mask][i]  
                if new_cost<dp[new_mask][j]:  
                    dp[new_mask][j]=new_cost  
    res=INF  
    for i in range(1,n):  
        all_cost=dp[full_mask][i]+cost[i][0]  
        if all_cost<res:  
            res=all_cost  
    print(res)  
if __name__ == '__main__':  
    main()
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20260321161510.png]]




## 2. 学习总结和个人收获

<mark>如果发现作业题目相对简单，有否寻找额外的练习题目，如“数算2025spring每日选做”、LeetCode、Codeforces、洛谷等网站上的题目。</mark>

### 拓展练习：（我还没做）来自LeetCode

| TSP拓展问题          |              |                          |           |
| ---------------- | ------------ | ------------------------ | --------- |
| 847. 访问所有节点的最短路径 | 允许重复访问节点     | `(node, mask)`           | 无起点/终点限制  |
| LCP 13. 寻宝       | 需要收集资源才能触发目标 | `(mask, last_mechanism)` | 需经过石头获取钥匙 |

这周的作业拖了一周才做:(
感觉前面的内容还很正常，第五题很难。（没有办法理解华容道问题的**证明思路**）但是跳过证明，运用Merge Sort和Fenwick Tree来解决逆序数还是很有教育意义的。第六题虽然之前做过了，但是还是没有扎实掌握到下次还能做出来的程度。因此又巩固了一遍，并将其标粉。

