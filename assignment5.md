# DSA Assignment #5: 20260401 cs201 Mock Exam

*Updated 2026-04-01 15:20 GMT+8*
 *Compiled by <mark></mark> (2026 Spring)*



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

### E02039: 反反复复	

matrix, http://cs101.openjudge.cn/practice/02039/

思路：
矩阵按行输出和按列输出的时间复杂度是一样的  


代码：

```python
c=int(input().strip())  
s=str(input().strip())  
res=''  
r=len(s)//c  
maze=[['x']*c for _ in range(r)]  
  
#注意：矩阵按行输出和按列输出的时间复杂度是一样的  
for i in range(len(s)):  
    if i//c%2==0:  
        maze[i//c][i%c]=s[i]  
    else:  
        maze[i//c][c-1-i%c]=s[i]  
  
for col in range(c):  
    for row in range(r):  
        res+=maze[row][col]  
  
print(res)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20260403153009.png]]




### E02092: Grandpa is Famous	

implementation, http://cs101.openjudge.cn/practice/02092/


思路：



代码：

```python
from collections import defaultdict  
while True:  
    N,M=map(int,input().strip().split())  
    if N==M==0: break  
    gamer=defaultdict(int)  
    for _ in range(N):  
        curr_ls=list(map(int,input().strip().split()))  
        for j in curr_ls:  
            gamer[j]+=1  
  
    overall_ranking=[]  
    for ppl,times in gamer.items():  
        overall_ranking.append((ppl,times))  
  
    overall_ranking.sort(key=lambda x:(-x[1],x[0]))  
    i=1  
  
    res=[]  
    while True:  
        res.append(overall_ranking[i][0])  
        if i+1>=len(overall_ranking) or overall_ranking[i+1][1]!=overall_ranking[i][1]:  
            break  
        else:  
            i+=1  
  
  
    print(*res)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>


![[Pasted image 20260403154718.png]]


### <font color='pink'>M02774: 木材加工	</font>

#binary search, http://cs101.openjudge.cn/practice/02774/

思路：
注意！**最大化最小值**

核心思想：当问题求”最小化最大值“或”最大化最小值“时，二分枚举答案。

- 模版：<mark>验证函数 + 二分搜索</mark>
- 关键：讲优化问题转化为判定问题（“能否达到？”）
- 应用：袋子分球、预算分配、资源分配类问题

二分不只是查找，更是“缩小解空间”的通用策略。（来自上个学期的讲义）
1. **问题转化**  
    假设我们猜测小段长度为 `L`，那么：
    
    - 每根原木可以切出 `length // L` 段。
        
    - 总段数 = 所有原木的 `length // L` 之和。
        
    - 如果总段数 `>= K`，说明 `L` 可行（可能还可以更大）。
        
    - 如果总段数 `< K`，说明 `L` 太大，需要减小。
        
2. **二分查找**
    
    - 左边界 `left = 1`（最小可能长度）
        
    - 右边界 `right = max(原木长度)`（最大可能长度）
        
    - 当 `left <= right` 时：
        
        - `mid = (left + right) // 2`
            
        - 计算总段数：
            
            python
            
            total = sum(length // mid for length in woods)
            
        - 如果 `total >= K`，说明 `mid` 可行，尝试更大：`left = mid + 1`，并记录答案。
            
        - 否则，`right = mid - 1`
代码：

```python
N,K=map(int,input().strip().split())  
woods=[]  
for _ in range(N):  
    woods.append(int(input().strip()))  
def binary_search(condition,left,right):  
    ans=None  
    while left<=right:  
        mid=(left+right)//2  
        if condition(mid):  
            ans=mid  
            left=mid+1  
        else:  
            right=mid-1  
    if not ans:  
        return 0  
    else:  
        return ans  
condition = lambda x: sum((i // x) for i in woods) >= K  
print(binary_search(condition,1,max(woods)))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20260403214835.png]]



### M04077: 出栈序列统计

dp, dfs, math, http://cs101.openjudge.cn/practice/04077/

思路：
!!!宝刀未老，宝刀未老啊！！！
没想到一个学期后的我还能够写出来dfs还能通过！！！

代码：

```python
n=int(input().strip())  
  
ans=0  
def dfs(stack,res,length,i):  
    global ans  
    if length==n:  
        ans+=1  
        return  
    else:  
        if i<=n:  
            stack.append(i)  
            dfs(stack,res,length,i+1)  
            stack.pop()  
        if stack:  
            a=stack.pop()  
            res.append(a)  
            dfs(stack,res,length+1,i)  
            a1=res.pop()  
            stack.append(a1)  
        return  
dfs([],[],0,1)  
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20260403220901.png]]



### <font color='skyblue'>M30637: 合法出栈序列pub</font>

stack, http://cs101.openjudge.cn/practice/M30637/

思路：
你的代码逻辑看起来比较复杂，有一些边界条件可能没处理好。

我看了你的思路，判断出栈序列其实有更简单的方法：  
<font color='skyblue'>模拟一个栈</font>，同时遍历目标序列，依次将原字符串的字符压入栈，当栈顶等于当前目标字符时就弹出，直到无法匹配为止。

---

## 思路详解

设原字符串为 `x`，要判断的出栈序列为 `y`。

1. 用一个栈 `stack` 来模拟入栈过程。
    
2. 用一个指针 `i` 指向 `y` 当前要匹配的字符。
    
3. 依次将 `x` 的字符压入栈，每次压入后检查栈顶是否等于 `y[i]`，如果是则弹出并 `i++`，直到不匹配为止。
    
4. 最终如果 `i == len(y)` 说明完全匹配，输出 `YES`，否则 `NO`。
    

注意：`y` 的长度必须等于 `x` 的长度，且每个字符在 `x` 中出现且只出现一次（题目已说明没有重复字符）。


代码

```python
from collections import defaultdict  
s = input().strip()  
  
  
while True:  
    try:  
        n_str= input().strip()  
        ans=True  
        if len(n_str)!=len(s):  
            print('NO')  
            continue  
        else:  
            stack=[]  
            i=0  
            j=0  
            while j<len(s):  
                stack.append(s[j])  
                j+=1  
                while stack and stack[-1]==n_str[i]:  
                    stack.pop()  
                    i+=1  
            if i==len(s):  
                print('YES')  
            else:  
                print('NO')  
  
  
  
    except EOFError:  
        break
```



<mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20260404155551.png]]




### <font color='pink'>T30102:完美交易窗口</font>

monotonic stack, http://cs101.openjudge.cn/practice/T30102/

思路：
attempt 1 and its bugs
```python
from collections import deque  
min_q=deque()#递增的  
max_q=deque()#递减的  
N=int(input().strip())  
price=[]  
for _ in range(N):  
price.append(int(input().strip()))  
i=j=0  
res=-1  
for j in range(N):  
while max_q and price[max_q[-1]]<=price[j]:  
max_q.pop()  
max_q.append(j)  
while min_q and price[min_q[-1]]>=price[j]:  
min_q.pop()  
min_q.append(j)  
if min_q and (j==min_q[0] or i!=min_q[0]):  
while i!=min_q[0]:  
if min_q[0]==i:  
min_q.popleft()  
if max_q[0]==i:  
max_q.popleft()  
i+=1  
if max_q[0]==j:  
res=max(j-i+1,res)  
print(res)
```
问题：
 1. 相等最大值的处理错误（违反严格唯一最大值）

在维护 max_q 时，你使用了 price[max_q[-1]] <= price[j] 作为出栈条件。这意味着如果窗口内出现与 h[j] **相等**的值，它会被弹出。

- **导致的问题**：当 max_q[0] == j 时，代码会误以为 h[j] 是当前的唯一最大值，但实际上更早前可能出现过等于 h[j] 的价格（它只是被出栈了）。
    
- **反例**：输入 [2, 4, 3, 4]。  
    正确的完美窗口是 [2, 3]（价格为 3, 4），长度为 2。但你的代码计算区间 [0, 3] 时，遇到了第二个 4 会把第一个 4 弹出，误认为窗口 [0, 3] 是合法的，从而错误地输出 4。
    

2. 仅维护全局最小 i，导致漏掉合法的更短窗口（核心逻辑缺陷）

你的代码用 min_q[0] 强行绑定了窗口的左端点 i，即 i 始终是当前后缀区间的最早出现的全局最小值。

- **导致的问题**：对于某个结尾 j，为了保证 h[j] 是窗口内的严格最大值，买入点 i **不能超过 h[j] 左侧第一个大于等于 h[j] 的位置**。真正的最佳起点可能只是局部的最小值，而不是全局的 min_q[0]。
    
- **反例**：输入 [5, 1, 4, 2, 3, 4]。  
    当遍历到最后一个 4 时，最长合法窗口是 [3, 5]（价格 [2, 3, 4]），长度为 3。但因为全局最小值是 1，你的 min_q[0] 一直卡在价格 1 的位置不肯推进，导致代码只去校验错误的区间 [1, 5]，最终只输出了长度 2，完美错过了最佳答案。

### **正确解法：provided by Gemini&Deepseek**
使用类似于dp的思路，维护两个dp数组：Mmin和Mlast。同时，维护一个单调栈stack储存右指针j之前 从前到后的全部独立的统辖区域（独立的统辖区域以最大值k来代表，独立的统辖区域指代这个区域可以形成一个完美区间而且可行的最小值在前者之后（最大值小于前者的最大值）
```python
import sys  
def main():  
    input_data = sys.stdin.read().split()  
    if not input_data:  
        return  
  
    N=int(input_data[0])  
    price=[int(x) for x in input_data[1:1+N]]  
  
    stack=[]  
    min_M=[0]*N  
    min_last=[0]*N  
    res=0  
    for j in range(N):  
        curr_min=price[j]  
        curr_last=j  
        while stack and price[j]>price[stack[-1]]:  
            k=stack.pop()#前面的弱小辖区被合并了.注意！前一个辖区的最小值并不一定比后一个辖区的最小值小  
            #更新，取真正的最小值  
            if min_M[k]<curr_min:#如果合并的若干辖区中有人能够让最小值更小（由于是从后往前找，也更靠前）  
                #那么将其更新为当前辖区的最小值；否则，仅仅跳过检查前一个满足条件的辖区  
                curr_min=min_M[k]  
                curr_last=min_last[k]  
        min_M[j]=curr_min  
        min_last[j]=curr_last  
        stack.append(j)  
        if curr_last<j and price[j]>curr_min:#防止这个j为单独一人或者合并了值也为p[j]的辖区  
            res=max(res,j-curr_last+1)  
    print(res)  
if __name__=='__main__':  
    main()
```
<mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20260404181905.png]]




## 2. 学习总结和个人收获

<mark>如果发现作业题目相对简单（哈哈哈老师又在说笑了），有否寻找额外的练习题目，如“数算2026spring每日选做”、LeetCode、Codeforces、洛谷等网站上的题目。</mark>

3\5\6难。3之难，来源于二分本来就容易错；5之难，来源于测试数据考验鲁棒性（什么一个人进入工程师搭建的酒吧然后点了一个炒饭酒吧炸了的故事）以及没能想到建立栈模拟后意义比对；6之难，来源于将dp与单调栈完美融合，着实不露痕迹。3之难，Deepseek可解；5之难，Deepseek也行。唯有6之难，Deepseek hack错误代码6轮而不能，Gemini200s思考找到错误代码问题而答案给错，直至Gemini代码移交Deepseek检查方能得到正确解（但其实Deepseek改对一处改错一处）。噫吁嚱！危乎高哉！吾尝问6题难度与Deepseek，知此题仅为省赛签到。计算机之幽深艰邃，**或可知乎！**

这是Gemini给出的分析，虽然最后代码有错误但是分析思路是对的。
### 最优解法：单调栈 + 区间特征合并 $O(N)$
双指针滑动窗口在这道题中很难同时完美兼顾“严格最大”和“严格最小”两个排斥条件。
这道题有一个极其巧妙的 **O(N) 单调栈** 思路：

1. 对于任意一个卖出点 $j$，它的合法买入点 $i$ 必须满足：**$i$ 必须在 $j$ 左侧第一个 $\ge h[j]$ 的位置（记为 $L_j$）的右侧**。即窗口只能落在 $(L_j, j]$ 内，才能保证 $h[j]$ 是严格唯一最大。
2. 在限定的合法区间 $(L_j, j]$ 内部，我们需要找**最后一次出现的最小值**作为买入点 $i$。如果找最早出现的，最小值可能会在窗口内重复；只有最后一次出现的最小值，才能保证严格唯一最小。
3. **算法降维**：我们可以用单调栈来找 $L_j$。巧妙的是，每次当前元素 $j$ 把比它小的栈顶元素 $k$ 弹出去时，**顺手把被弹出区间 $(L_k, k]$ 的“最小值”和“最后出现的索引”继承合并到 $j$ 的状态里**。

### 修正后的 Python 代码：

```python
import sys

def solve():
    # 使用 sys.stdin.read 快速读取百万级数据，避免 I/O 超时
    input_data = sys.stdin.read().split()
    if not input_data:
        return
        
    N = int(input_data[0])
    price = [int(x) for x in input_data[1:N+1]]
    
    res = -1
    stack = [] # 单调栈，存索引，用于维护左侧第一个 >= price[j] 的屏障 L_j
    
    # 动态维护记录：每个被遮挡区间 (L_k, k] 内的 [最小值, 最小值最后出现的索引]
    M_min = [0] * N 
    M_last = [0] * N 
    
    for j in range(N):
        cur_min = price[j]
        cur_last = j
        
        # 遇到更大的 price[j] 时，栈内小于它的元素区间全部归并到 j 的可视区间内
        while stack and price[stack[-1]] < price[j]:
            k = stack.pop()
            
            # 如果弹出的子区间有更小的值，则继承它
            if M_min[k] < cur_min:
                cur_min = M_min[k]
                cur_last = M_last[k]
            # 注意：如果 M_min[k] == cur_min，我们不更新 cur_last，
            # 因为 k < j，这保留了“更靠右（晚出现）”的最小值索引，满足唯一性！
                
        # 记录当前 j 统御区间 (L_j, j] 的最小值特征
        M_min[j] = cur_min
        M_last[j] = cur_last
        stack.append(j)
        
        # 此时，cur_last 必定是区间 (L_j, j] 内的最完美的合法起点 i
        if cur_last < j and price[j] > cur_min:
            res = max(res, j - cur_last + 1)
            
    print(res)

if __name__ == '__main__':
    solve()
```

### 为什么这段代码无比精妙且正确？
1. **彻底解决区间界限**：`stack` 遇到大的就合并小的，保证了每个元素的统御区间绝对不跨越左边比它大的障碍物，$h[j]$ 永远是当前统计的严格最大值。
2. **巧妙解决重复最小值**：遇到相同最小值时，`if M_min[k] < cur_min` 中的 `<` 保证了靠右的索引胜出，完美避免了持有期间出现重复低价的情况。
3. **极限性能**：每个元素最多进栈一次、出栈一次。没有复杂的边界分情况讨论，完美达到了时间复杂度和空间复杂度均为 $O(N)$。

