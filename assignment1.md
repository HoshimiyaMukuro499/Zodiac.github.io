# Assignment #1: OOP

*Updated 2026-03-03 11:25 GMT+8*
 *Compiled by <mark>***,生命科学学院</mark> (2026 Spring)*
颜色说明:
<font color='pink'>粉色代表这道题来自于已知的知识点但没能想出正确的思路,查看了题解</font>

<font color='skyblue'>天蓝色代表这道题包含了之前没有掌握的语法/数据结构/算法,有迹可循</font>

如果是分散的单个语法不会被标为天蓝色,而是计入笔记之中

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

### E27653: Fraction类

OOP, http://cs101.openjudge.cn/pctbook/E27653/

> 主要是练习面向对象编程写法，这样力扣题目，笔试都没有问题了。机考时候，不是必须OOP，能AC就可以。
>

思路：



代码：

```python
import math  
class Fraction:  
    def __init__(self,fenzi,fenmu):  
        self.fenzi = fenzi  
        self.fenmu = fenmu  
    def add(self,other):  
        new_fenmu=self.fenmu*other.fenmu  
        new_fenzi=self.fenzi*other.fenmu+self.fenmu*other.fenzi  
        a=math.gcd(new_fenzi,new_fenmu)  
        new_fenzi=new_fenzi//a  
        new_fenmu=new_fenmu//a  
        return Fraction(new_fenzi,new_fenmu)  
    def print(self):  
        print(f'{self.fenzi}/{self.fenmu}')  
ls=list(map(int,input().strip().split()))  
a=Fraction(ls[0],ls[1])  
b=Fraction(ls[2],ls[3])  
res=a.add(b)  
res.print()
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20260307082928.png]]




### <font color='skyblue'>E190.颠倒二进制位</font>

bit manipulation, https://leetcode.cn/problems/reverse-bits/


思路：



代码：

```python
class Solution:  
    def reverseBits(self, n: int) -> int:  
        res=0  
        for i in range(32):  
            res=(res<<1)|(n&1)  
            n>>=1  
        return int(res)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20260307154909.png]]



### E1356.根据数字二进制下 1 的数目排序

bit manipulation, https://leetcode.cn/problems/sort-integers-by-the-number-of-1-bits/

思路：
<font color='skyblue'>`x.bit_count()`计数数字1的个数</font>


代码：

```python
from typing import List  
class Solution:  
    def sortByBits(self, arr: List[int]) -> List[int]:  
        arr.sort()  
        arr.sort(key=lambda x:str(bin(x)).count('1'))  
        return arr
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20260307163307.png]]




### M27300: 模型整理

sortings, AI, http://cs101.openjudge.cn/pctbook/M27300/



思路：
好繁琐的一道格式题...我的解法是创建了一个default字典来存储各个模型的内容,之后将每个字典内部按照末尾M,B来排序,最后再转换会列表后按照名称字典序来排序.
最后的格式中,逗号与冒号后面都加了一个莫名所以的空格.


代码：

```python
from collections import defaultdict  
n=int(input().strip())  
ls=[]  
for _ in range(n):  
    ls.append(tuple(input().strip().split('-')))  
dct=defaultdict(list)  
for x in ls:  
    dct[x[0]].append(x[1])  
order={'M':1,'B':2}  
for key in dct.keys():  
    dct[key].sort(key=lambda x:(order[x[-1]],float(x[:-1])))  
res=[]  
for (key,value) in dct.items():  
    res.append((key,value))  
res.sort(key=lambda x:x[0])  
for (x,y) in res:  
    value_str=', '.join(y)  
    print(f'{x}: {value_str}')
```
优化后
```python
from collections import defaultdict

# 1. 简化输入处理
n = int(input().strip())
dct = defaultdict(list)

for _ in range(n):
    # 直接解包赋值，避免中间列表
    key, value = input().strip().split('-')
    dct[key].append(value)

# 2. 排序规则保持不变
order = {'M': 1, 'B': 2}
for key in dct:
    # 使用更清晰的变量名
    dct[key].sort(key=lambda x: (order[x[-1]], float(x[:-1])))

# 3. 直接对字典项排序并输出
for idx, (key, values) in enumerate(sorted(dct.items())):
    print(f'{idx}: {", ".join(values)}')
```


代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20260307170142.png]]


==粉色代表没能独立做出,查看了题解==
### <font color='pink'>M1536.排布二进制网格的最少交换次数</font>

greedy, matrix, <font color='red'>imitation</font> https://leetcode.cn/problems/minimum-swaps-to-arrange-a-binary-grid/
方法一：贪心
思路与算法

我们从上到下逐行确定，假设当前考虑到第 i 行，第 0…i−1 行都已经确定好。按题意第 i 行满足的条件为末尾连续零的个数大于等于 n−i−1， 那么我们考虑将 [i…n−1] 中的哪一行逐行交换到第 i 行。假设当前有多行都满足第 i 行的条件，我们应该选择哪一行交换到第 i 行呢？为了令最后交换次数最少，我们贪心地选择离第 i 行最近的那一行即可。

你可能会在想这样是否一定正确。我们可以考虑假设当前有若干行都能满足第 i 行，那么这些行一定都满足第 i+1…n−1 的限制条件，也就是说能交换到第 i 行的那些行一定也能交换到后面几行，因为随着行数的增加，限制条件越来越宽松。因此不会存在贪心地选择后，后面出现无法放置的情况。

最后来看实现。为了避免每次判断当前行是否满足末尾连续零的个数的限制条件的时候都要从后往前遍历当前行，造成不必要的时间消耗，我们需要先用 O(n^2) 的操作预处理出每一行最后一个 1 所在的位置，记为 pos[i]。这样我们就可以按照我们的策略模拟，从上到下逐行确定，对于第 i 行，只要找到第 i…n−1 行中使得 pos[j]≤i 成立的最近的那一行 j，我们将这一行交换到第 i 行即可，它对答案的贡献为 j−i。
**类似于冒泡排序,经过详尽的观察,可以发现冒泡排序需要的次数是最少的**
思路：



代码：

```python
from typing import List  
  
  
class Solution:  
    def minSwaps(self, grid: List[List[int]]) -> int:  
        n=len(grid)  
        def count_n(x:list):  
            res=0  
            for _ in range(n-1,-1,-1):  
                if x[_]==0:  
                    res+=1  
                else:  
                    break  
            return res  
        zeros=[]  
        for i in range(n):  
            zeros.append(count_n(grid[i]))  
        ans=0  
        exist=True  
        for i in range(n):  
            k=-1  
            for j in range(i,n):#第一次循环:寻找可以替换i的行j,并计算最少的交换次数(只要保证行j换到行i即可,不需要其他的部分恢复原状)  
                if zeros[j]>=n-i-1:  
                    k=j  
                    ans+=j-i  
                    break  
  
            if k!=-1:#第二次循环:进行实际的交换操作  
                for x in range(k-1,i-1,-1):  
                    zeros[x],zeros[x+1]=zeros[x+1],zeros[x]#列表元素互换  
  
            else:  
                exist=False  
                break        if exist:  
            return ans  
        else:  
            return -1
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>



### <font color='pink'>T20052:最大点数（同2048规则）</font>

dfs, matrices, http://cs101.openjudge.cn/pctbook/T20052/

思路：
之前自己写的一个版本代码,不知为何一直WA,破防了
决定参照AI写的AC代码


代码：
我的代码(最后仍旧WA)
```python
from collections import deque

m, n, p = map(int, input().strip().split())
board = []
for _ in range(m):
    board.append(list(map(int, input().strip().split())))
max_point = max(max(row) for row in board)

q = deque([(board, 0)])

def move(oldboard, direction):
    # 首先创建一个深拷贝避免修改原数组
    board = [oldboard[i][:] for i in range(m)]
    changed = False
    
    if direction == 'left':
        for i in range(m):
            # 把非零元素移动到最左边方便计算
            temp_row = [x for x in board[i] if x != 0]
            # 创建一个新表便于存储合并后的结果
            new_row = []
            j = 0
            while j < len(temp_row):
                if j + 1 < len(temp_row) and temp_row[j] == temp_row[j + 1]:
                    new_row.append(temp_row[j] * 2)
                    j += 2
                else:
                    new_row.append(temp_row[j])
                    j += 1
            # 补全 0 至原表长度
            while len(new_row) < n:
                new_row.append(0)
            # 检查是否更改并更新标志changed
            if board[i] != new_row:
                changed = True
                board[i] = new_row
    
    elif direction == 'right':
        for i in range(m):
            # 把非零元素移动到最右边方便计算
            temp_row = [x for x in board[i] if x != 0]
            # 创建一个新表便于存储合并后的结果
            new_row = []
            j = len(temp_row) - 1
            while j >= 0:
                if j - 1 >= 0 and temp_row[j] == temp_row[j - 1]:
                    new_row.insert(0, temp_row[j] * 2)
                    j -= 2
                else:
                    new_row.insert(0, temp_row[j])
                    j -= 1
            # 补全 0 至原表长度
            while len(new_row) < n:
                new_row.insert(0, 0)
            # 检查是否更改并更新标志changed
            if board[i] != new_row:
                changed = True
                board[i] = new_row
    
    elif direction == 'up':
        for j in range(n):
            # 提取当前列
            col = [board[i][j] for i in range(m)]
            # 把非零元素移动到最上面方便计算
            temp_col = [x for x in col if x != 0]
            # 创建一个新表便于存储合并后的结果
            new_col = []
            k = 0
            while k < len(temp_col):
                if k + 1 < len(temp_col) and temp_col[k] == temp_col[k + 1]:
                    new_col.append(temp_col[k] * 2)
                    k += 2
                else:
                    new_col.append(temp_col[k])
                    k += 1
            # Pad with zeros to maintain size
            while len(new_col) < m:
                new_col.append(0)
            # 检查是否更改并更新标志changed
            orig_col = [board[i][j] for i in range(m)]
            if orig_col != new_col:
                changed = True
                for i in range(m):
                    board[i][j] = new_col[i]
    
    elif direction == 'down':
        for j in range(n):
            # 提取当前列
            col = [board[i][j] for i in range(m)]
            # 把非零元素移动到最下面方便计算
            temp_col = [x for x in col if x != 0]
            # 创建一个新表便于存储合并后的结果
            new_col = []
            k = len(temp_col) - 1
            while k >= 0:
                if k - 1 >= 0 and temp_col[k] == temp_col[k - 1]:
                    new_col.insert(0, temp_col[k] * 2)
                    k -= 2
                else:
                    new_col.insert(0, temp_col[k])
                    k -= 1
            # 补全 0 至原表长度
            while len(new_col) < m:
                new_col.insert(0, 0)
            # 检查是否更改并更新标志changed
            orig_col = [board[i][j] for i in range(m)]
            if orig_col != new_col:
                changed = True
                for i in range(m):
                    board[i][j] = new_col[i]
    
    return board, changed

# BFS实现
visited = set()
max_value = max_point

while q:
    current_board, steps = q.popleft()
    
    # 转换为元组便于哈希
    board_tuple = tuple(tuple(row) for row in current_board)
    if board_tuple in visited or steps > p:
        continue
    visited.add(board_tuple)
    
    # 更新最大值
    current_max = max(max(row) for row in current_board)
    max_value = max(max_value, current_max)
    
    if steps == p:
        continue
        
    # 尝试所有方向移动
    for direction in ['left', 'right', 'up', 'down']:
        new_board, changed = move(current_board, direction)
        if changed:
            q.append((new_board, steps + 1))

print(max_value)
```
AI代码
```python
from collections import deque

def move_row_left(row):
    """处理单行左移的逻辑"""
    # 第一步：移除0，将数字靠左
    new_row = [x for x in row if x != 0]
    # 第二步：合并相邻相同数字
    for i in range(len(new_row) - 1):
        if new_row[i] == new_row[i + 1]:
            new_row[i] *= 2
            new_row[i + 1] = 0
    # 第三步：再次移除0，靠左
    new_row = [x for x in new_row if x != 0]
    # 第四步：补0到原长度
    new_row += [0] * (len(row) - len(new_row))
    return new_row

def move_row_right(row):
    """处理单行右移的逻辑（反转后左移再反转）"""
    # 反转行，左移，再反转回来
    reversed_row = row[::-1]
    moved_reversed = move_row_left(reversed_row)
    return moved_reversed[::-1]

def move_board(board, direction):
    """移动整个棋盘，返回(是否改变, 新棋盘, 新棋盘最大值)"""
    m, n = len(board), len(board[0])
    new_board = [row[:] for row in board]
    changed = False
    
    if direction == 'left':
        for i in range(m):
            new_row = move_row_left(new_board[i])
            if new_row != new_board[i]:
                changed = True
            new_board[i] = new_row
    
    elif direction == 'right':
        for i in range(m):
            new_row = move_row_right(new_board[i])
            if new_row != new_board[i]:
                changed = True
            new_board[i] = new_row
    
    elif direction == 'up':
        # 转置后当作左移处理
        transposed = [[new_board[j][i] for j in range(m)] for i in range(n)]#转置
        for i in range(n):
            new_col = move_row_left(transposed[i])
            if new_col != transposed[i]:
                changed = True
            transposed[i] = new_col
        # 转置回来
        new_board = [[transposed[j][i] for j in range(n)] for i in range(m)]
    
    elif direction == 'down':
        # 转置后当作右移处理
        transposed = [[new_board[j][i] for j in range(m)] for i in range(n)]
        for i in range(n):
            new_col = move_row_right(transposed[i])
            if new_col != transposed[i]:
                changed = True
            transposed[i] = new_col
        # 转置回来
        new_board = [[transposed[j][i] for j in range(n)] for i in range(m)]
    
    # 计算新棋盘最大值
    max_val = max(max(row) for row in new_board)
    
    return changed, new_board, max_val

def solve():
    # 读取输入
    m, n, p = map(int, input().strip().split())
    board = []
    for _ in range(m):
        board.append(list(map(int, input().strip().split())))
    
    # 初始最大值
    initial_max = max(max(row) for row in board)
    ans = initial_max
    
    # BFS队列：每个元素为 (棋盘, 当前棋盘最大值, 步数)
    q = deque()
    q.append((board, initial_max, 0))
    
    # 去重
    visited = set()
    visited.add(tuple(tuple(row) for row in board))
    
    while q:
        cur_board, cur_max, step = q.popleft()
        
        # 如果已经达到最大步数，不再从此状态扩展
        if step >= p:
            continue
        
        # 尝试四个方向
        for direction in ['left', 'right', 'up', 'down']:
            changed, new_board, new_max = move_board(cur_board, direction)
            
            if changed:
                # 更新全局最优
                ans = max(ans, new_max)
                
                # 转换为可哈希类型用于去重
                board_key = tuple(tuple(row) for row in new_board)
                if board_key not in visited:
                    visited.add(board_key)
                    q.append((new_board, new_max, step + 1))
    
    print(ans)

if __name__ == "__main__":
    solve()
```


代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20260307220205.png]]



## 2. 学习总结和个人收获

<mark>如果发现作业题目相对简单，有否寻找额外的练习题目，如“数算2025spring每日选做”、LeetCode、Codeforces、洛谷等网站上的题目。</mark>
==虽然最后一道题到最后也没能够找出来哪里错了很是不甘心,但是...首先,庆祝成功选上闫老师的数算B!!!感谢闫老师对于扩充名额的争取!==
闫老师的课程不进行无用概念的堆砌,而是在具体的例子中逐步阐述算法\结构的本质.很荣幸能与闫老师、班上大神云集的同学们一起,开启新学期的探索之旅.
这次作业5\6比较费力,分别是贪心与矩阵搜索.
## 3.附录(这次作业的笔记)
颜色说明:
<font color='pink'>粉色代表这道题来自于已知的知识点但没能想出正确的思路,查看了题解</font>

<font color='skyblue'>天蓝色代表这道题包含了之前没有掌握的语法/数据结构/算法,有迹可循</font>

如果是分散的单个语法不会被标为天蓝色,而是计入笔记之中
==春天的课程就选一些浅色系的颜色==
**位运算**
`Solution().reverseBits(5)` 中的 `Solution()` 扮演的是**类的实例化**作用。
```python
Solution().reverseBits(5)
```
可以拆解为：
  1. `Solution()` - 创建实例
- `Solution` 是一个类（class）
- `Solution()` 调用类的构造函数，创建该类的一个**实例对象**
- 相当于：
  ```python
  obj = Solution()  # 先创建实例
  obj.reverseBits(5)  # 再调用方法
  ```
   十进制与二进制转换方法

  一、十进制 → 二进制

  方法1：除2取余法（整数部分）
不断除以2，记录余数，直到商为0，然后将余数倒序排列。

**示例：将 13 转换为二进制**
```
13 ÷ 2 = 6 余 1 ↑
 6 ÷ 2 = 3 余 0 ↑
 3 ÷ 2 = 1 余 1 ↑
 1 ÷ 2 = 0 余 1 ↑
```
倒序取余数：1101
所以 13₁₀ = 1101₂

  方法2：Python内置函数
```python
# 方法1：bin() 函数
binary = bin(13)      # 返回 '0b1101'
binary_without_prefix = bin(13)[2:]  # 去掉 '0b' 前缀 → '1101'

# 方法2：format() 函数
binary = format(13, 'b')     # '1101'
binary_8bit = format(13, '08b')  # 8位二进制，不足补0 → '00001101'

# 方法3：f-string
binary = f"{13:b}"           # '1101'
binary_8bit = f"{13:08b}"    # '00001101'
```

二、二进制 → 十进制

  方法1：按权展开法
二进制数从右到左，每一位乘以2的相应次方，然后相加。

**示例：将 1101₂ 转换为十进制**
```
1 1 0 1
2³ 2² 2¹ 2⁰
= 1×2³ + 1×2² + 0×2¹ + 1×2⁰
= 8 + 4 + 0 + 1
= 13
```

  方法2：Python内置函数
```python
# 方法1：int() 函数，指定基数为2
decimal = int('1101', 2)      # 13

# 方法2：处理带前缀的二进制字符串
decimal = int('0b1101', 2)    # 13（0b前缀不影响）

# 方法3：直接转换
binary_str = '1101'
decimal = 0
for digit in binary_str:
    decimal = decimal * 2 + int(digit)  # 13
```
 五、常用技巧
```python
# 检查二进制位
num = 13  # 1101
bit_2 = (num >> 2) & 1  # 检查第2位（从0开始）→ 1

# 设置特定位
num |= (1 << 3)  # 设置第3位为1

# 清除特定位
num &= ~(1 << 1)  # 清除第1位

# 翻转特定位
num ^= (1 << 2)  # 翻转第2位
```
颠倒位
result<<1:左移1位
n&1:取个位
核心:把原数字二进制从后往前切下来,之后将结果左移并将切下来的数字接到原来结果的末尾.
```python
class Solution:
    def reverseBits(self, n: int) -> int:
        result = 0
        for i in range(32):
            result = (result << 1) | (n & 1)
            n >>= 1
        return result

print(Solution().reverseBits(5))  # 应该输出 2684354560
```
你的理解很接近了，但需要澄清一点：**n 本身就是二进制存储的，不是“变成”的**。
关键概念：计算机内部存储
当你写 `n = 5` 时：
- 在代码中你写的是十进制数字 `5`
    
- 但在计算机内存中，**实际存储的是二进制** `00000000 00000000 00000000 00000101`（32位int）
关键理解：**二进制和十进制只是表示形式**
`result` 输出的不是"自动变成十进制"，而是**所有整数在Python中默认以十进制形式显示**。
`int(x, y)` 的含义

这是 Python 中将**字符串或数字**转换为**整数**的函数，其中：

- **x**：要转换的值（通常是字符串）
- **y**：**进制数**（可选，默认为10）
基本用法
最常见的用法：字符串转十进制整数

num = int("123")     # 123（默认十进制）
num = int("456", 10) # 456（明确指定十进制）

---

Q:如果我想将某一个列表按照指定顺序(如首字母为C,D,B,E,G,F,A...)进行排序,应该使用什么样的语法?
A:自定义列表排序的多种方法

  1. 使用 `key` 参数 + 自定义顺序字典（最常用）

```python

#定义自定义顺序
custom_order = {'C': 1, 'D': 2, 'B': 3, 'E': 4, 'G': 5, 'F': 6, 'A': 7}
my_list = ['A', 'B', 'C', 'D', 'E', 'F', 'G']
sorted_list = sorted(my_list, key=lambda x: custom_order[x])
print(sorted_list)  # ['C', 'D', 'B', 'E', 'G', 'F', 'A']
```
---
zeros[x],zeros[x+1]=zeros[x+1],zeros[x]#列表元素互换
___
矩阵转置`transposed = [[new_board[j][i] for j in range(m)] for i in range(n)]`
___
