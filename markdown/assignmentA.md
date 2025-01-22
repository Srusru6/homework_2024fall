# Assignment #10: dp & bfs

Updated 2 GMT+8 Nov 25, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### LuoguP1255 数楼梯

dp, bfs, https://www.luogu.com.cn/problem/P1255

思路：



代码：

```python
n=int(input())
dp=[i+1 for i in range(n)]
for i in range(2,n):
    dp[i]=dp[i-1]+dp[i-2]
print(dp[-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\10-1.png)



### 27528: 跳台阶

dp, http://cs101.openjudge.cn/practice/27528/

思路：



代码：

```python
n=int(input())
dp=[i+1 for i in range(n)]
for i in range(2,n):
    dp[i]=sum(dp[0:i])+1
print(dp[-1])
```



代码运行截图 ==（至少包含有"Accepted"）==

![](..\pic\10-2.png)



### 474D. Flowers

dp, https://codeforces.com/problemset/problem/474/D

思路：



代码：

```python
t, k = map(int, input().split())
l = []
p = 0
for _ in range(t):
    a, b = map(int, input().split())
    l.append((a, b))
    p = max(p, a, b)

dp = [1] * (k)
for i in range(k, p + 1):
    dp.append((dp[-1] + dp[-k]) % 1000000007)

s = {0: 0}
q = 0
for i in range(1, p + 1):
    q += dp[i]
    q %= 1000000007
    s[i] = q

for a, b in l:
    print((s[b] - s[a - 1]) % 1000000007)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\10-3.png)



### LeetCode5.最长回文子串

dp, two pointers, string, https://leetcode.cn/problems/longest-palindromic-substring/

思路：



代码：

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        n=len(s)
        dp=[[False for _ in range(n)] for _ in range(n)]
        ans=''
        for i in range(n):
            for j in range(i,-1,-1):
                if i-j<=2:
                    dp[j][i]= s[i]==s[j]
                else:
                    dp[j][i]= s[i]==s[j] and dp[j+1][i-1]
                if dp[j][i] and i-j+1>len(ans):
                    ans=s[j:i+1]
        return ans
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\10-4.png)





### 12029: 水淹七军

bfs, dfs, http://cs101.openjudge.cn/practice/12029/

思路：



代码：

```python
from collections import deque
import sys


def cover():
    he=h[X][Y]
    if he<h[I][J]:
        return False
    l=deque([(X,Y)])
    while l:
        x,y=l.popleft()
        if x==I and y==J :
            return True
        if ed[x][y]:
            continue
        ed[x][y]=True
        for i,j in [(1,0),(-1,0),(0,1),(0,-1)]:
            if he>h[x+i][y+j] and not ed[x+i][y+j]:
                l.append((x+i,y+j))
    return False


l=deque(list(map(int,sys.stdin.read().split())))
ans=[]
for _ in range(l.popleft()):
    M=l.popleft()
    N=l.popleft()
    h=[[1001 for _ in range(N+2)]for _ in range(M+2) ]
    for i in range(1,M+1):
        for j in range(1,N+1):
            h[i][j]=l.popleft()
    I=l.popleft()
    J=l.popleft()
    f=False
    le=[]
    for _ in  range(l.popleft()):
        le.append((l.popleft(),l.popleft()))
    le=sorted(le,key=lambda b:h[b[0]][b[1]],reverse=True)
    ed=[[False for _ in range(N+1)]for _ in range(M+1)]
    for X,Y in le:
        f=cover()
        if f:
            break   
    if f:
        ans.append('Yes')
    else:
        ans.append('No')

sys.stdout.write("\n".join(ans)+"\n")
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\10-5.png)



### 02802: 小游戏

bfs, http://cs101.openjudge.cn/practice/02802/

思路：



代码：

```python
from collections import deque
import copy

def dfs(x,y,a,b):
    
    stack=deque([(x,y)])
    vd=[[float('inf') for _ in range(h+4)] for _ in range(w+4)]
    vd[x][y]=0
    while stack:
        x,y=stack.popleft()
        for i,j in [(1,0),(-1,0),(0,1),(0,-1)]:
            xi=1
            yj=1
            while l[x+i*xi][y+j*yj]:
                vd[x+i*xi][y+j*yj]=min(vd[x+i*xi][y+j*yj],vd[x][y]+1)
                l[x+i*xi][y+j*yj]=False
                stack.append((x+i*xi,y+j*yj))
                xi+=1
                yj+=1
    return vd[a][b]
        
    
ans=[]    
while True:
    w,h=map(int,input().split())
    if w==0 :
        break
    l=[[True for _ in range(h+4)] for _ in range(w+4)]
    l[0]= [False for _ in range(h+4)]
    l[-1]=[False for _ in range(h+4)]
    for i in range(1,w+3):
        l[i][0]=False
        l[i][-1]=False
    for i in range(2,h+2):
        tem=input()
        for j in range(2,w+2):
            if tem[j-2]=='X':
                l[j][i]=False
    an=[]
    while True:
        x,y,a,b=map(int,input().split())
        if x==0:
            break
        tem=copy.deepcopy(l)
        l[a+1][b+1]=True
        an.append(dfs(x+1,y+1,a+1,b+1))
        l=tem
    ans.append(an)

for i in range(len(ans)):
    print(f'Board #{i+1}:')
    for j in range(len(ans[i])):
        if ans[i][j]==float('inf'):
            print(f'Pair {j+1}: impossible.')
        else:
            print(f'Pair {j+1}: {ans[i][j]} segments.')
    print()
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\10-6.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

Flowers真的狠狠给我的优化上了一节课

水淹七军的输入输出太难搞了

感觉现在dfs，bfs都比较熟练了



