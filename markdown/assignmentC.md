# Assignment #C: 五味杂陈 

Updated 1148 GMT+8 Dec 10, 2024

2024 fall, Complied by 李皓翔 物院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 1115. 取石子游戏

dfs, https://www.acwing.com/problem/content/description/1117/

思路：



代码：

```python
while True:
    a,b=map(int,input().split())
    if a==0:
        break
    if a<b:
        a,b=b,a
    flag=False
    while a>0 and b>0:
        if a%b==0 or a//b>=2:
            flag=True
            fl=True
            break
        if b%(a-b)==0 or b//(a-b)>=2:
            flag=True
            fl=False
            break
        a,b=a-b,2*b-a
    if fl:
        print('win')
    else:
        print('lose')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\12-1.png)



### 25570: 洋葱

Matrices, http://cs101.openjudge.cn/practice/25570

思路：



代码：

```python
n=int(input())
m=[[0 for _ in range(n)]for _ in range(n)]
for i in range(n):
    tem=list(map(int,input().split()))
    for j in range(n):
        m[i][j]=tem[j]
ans=0
for i in range((n+1)//2):
    sum=m[i][i]
    for j in range(i+1,n-i):
        sum+=m[i][j]+m[j][i]
        sum+=m[n-i-1][j]+m[j][n-i-1]
    if n-i-1!=i:
        sum-=m[n-i-1][n-i-1]
    ans=max(ans,sum)
if n==1:
    ans=m[0][0]
print(ans)
```



代码运行截图 ==（至少包含有"Accepted"）==

![](..\pic\12-2.png)



### 1526C1. Potions(Easy Version)

greedy, dp, data structures, brute force, *1500, https://codeforces.com/problemset/problem/1526/C1

思路：



代码：

```python
import heapq as h
n=int(input())
l=list(map(int,input().split()))
life=0
po=[]
c=0
for i in l:
    if i>0:
        life+=i
        c+=1
    elif i+life<0 and po:
        tem=h.heappop(po)
        if tem<i:
            h.heappush(po,i)
            life+=-tem+i
        else:
            h.heappush(po,tem)
    elif i+life>=0:
        life+=i
        h.heappush(po,i)
print(len(po)+c)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\12-3.png)



### 22067: 快速堆猪

辅助栈，http://cs101.openjudge.cn/practice/22067/

思路：



代码：

```python
from collections import deque
stack=deque([])
max=deque([])
for i in range(1000002):
    try:
        tem=input().split()
    except EOFError:
        break
    if tem[0]=='pop' and stack:
        p=stack.pop()
        max.pop()
    if tem[0]=='min' and stack:
        print(max[-1])
    if tem[0]=='push':
        stack.append(int(tem[1]))
        if len(max)==0 : 
            max.append(int(tem[1]))
        elif int(tem[1])<max[-1]:
            max.append(int(tem[1]))
        else:
            max.append(max[-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\12-4.png)



### 20106: 走山路

Dijkstra, http://cs101.openjudge.cn/practice/20106/

思路：



代码：

```python
m,n,p=map(int,input().split())
h=[[float('inf') for i in range(n+2)]for j in range(m+2)]
for i in range(1,m+1):
    tem=input().split()
    for j in range(n):
        if tem[j]!='#':
            h[i][j+1]=int(tem[j])
for _ in range(p):
    x,y,a,b=map(lambda x:int(x)+1,input().split())
    s=[(0,x,y)]
    dij=[[float('inf') for i in range(n+2)]for j in range(m+2)]
    dij[x][y]=0
    while s:
        s=sorted(s,reverse=True)
        _,x,y=s.pop()
        for i,j in [(1,0),(-1,0),(0,1),(0,-1)]:
            if dij[x][y]+abs(h[x+i][y+j]-h[x][y])<dij[x+i][y+j]and h[x+i][y+j]!=float('inf'):
                dij[x+i][y+j]=dij[x][y]+abs(h[x+i][y+j]-h[x][y])
                s.append((dij[x+i][y+j],x+i,y+j))
    if dij[a][b]==float('inf'):
        print('NO')
    else:
        print(dij[a][b])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\12-4.png)



### 04129: 变换的迷宫

bfs, http://cs101.openjudge.cn/practice/04129/

思路：



代码：

```python
for _ in range(int(input())):
    R,C,K=map(int,input().split())
    m=[[False for i in range(C+1)]for j in range(R+1)]
    for i in range(R):
        tem=input()
        for j in range(C):
            if tem[j]=='.':
                m[i][j]=True
            if tem[j]=='S':
                s=(0,i,j)
                m[i][j]=True
            if tem[j]=='E':
                e=[i,j]
                m[i][j]=True
    t=[[float('inf') for i in range(C)]for j in range(R)]
    vd=[[True for i in range(C)]for j in range(R)]
    dji=[s]
    while dji:
        pt,x,y=dji.pop()
        vd[x][y]=False
        for i,j in [(1,0),(-1,0),(0,1),(0,-1)]:
            if  x+i<R and x+i>-1 and y+j<C and y+j>-1 and vd[x+i][y+j]:
                if m[x+i][y+j] or (pt+1)%K==0:
                    rt=pt+1
                elif  not(K%2==0 and pt%2==0)  and m[x][y] and (m[x+1][y] or m[x-1][y] or m[x][y+1] or m[x][y-1]):
                    ii=0
                    while (ii*2+pt+1)%K!=0:
                        ii+=1
                    rt=ii*2+pt+1
                else:
                    rt=float('inf')
                if rt<t[x+i][y+j]:
                    t[x+i][y+j]=rt
                    dji.append((rt,x+i,y+j))
                    dji=sorted(dji,reverse=True)
    if t[e[0]][e[1]]==float('inf'):
        print('Oop!')
    else:
        print(t[e[0]][e[1]])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\12-6.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

前面题目做的挺顺，就是时间有些紧张，还在多刷题

变换迷宫用Dijkstra写的，思路是有相邻石头时往回走一格（如果可以的话）再回来，直到2的倍数时间后如果可以就走进石头，但消耗额外步数，如此直接变成走山路



