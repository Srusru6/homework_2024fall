# Assignment #B: Dec Mock Exam大雪前一天

Updated 1649 GMT+8 Dec 5, 2024

2024 fall, Complied by 李皓翔 物院



**说明：**

1）⽉考： AC1。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E22548: 机智的股民老张

http://cs101.openjudge.cn/practice/22548/

思路：



代码：

```python
a=list(map(int,input().split()))
n=len(a)
ans=0
r=[0 for i in range(n)]
l=[0 for i in range(n)]
r[-1]=a[-1]
l[0]=a[0]
for i in range(1,n):
    r[n-i-1]=max(r[n-i],a[n-i-1])
    l[i]=min(l[i-1],a[i])
for i in range(n):
    ans=max(ans,r[i]-l[i])
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\11-1.png)



### M28701: 炸鸡排

greedy, http://cs101.openjudge.cn/practice/28701/

思路：



代码：

```python
n,k=map(int,input().split())
t=list(map(int,input().split()))
t.sort(reverse=True)
s=sum(t)
for i in t:
    if i>s/k:
        s-=i
        k-=1
print('%.3f'%(s/k))
```



代码运行截图 ==（至少包含有"Accepted"）==

![](..\pic\11-2.png)



### M20744: 土豪购物

dp, http://cs101.openjudge.cn/practice/20744/

思路：

考试的时候没想到dp，死磕了好久

代码：

```python
p=list(map(int,input().split(',')))
n=len(p)
dp=[0 for i in range(n)]
dp[0]=p[0]
for i in range(1,n):
    dp[i]=max(dp[i-1]+p[i],p[i])
dp1=[0 for i in range(n)]
dp1[0]=0
dp1[1]=max(p[0],p[1])
for i in range(2,n):
    dp1[i]=max(dp1[i-1]+p[i],dp[i-2]+p[i])
print(max(dp+dp1))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\11-3.png)



### T25561: 2022决战双十一

brute force, dfs, http://cs101.openjudge.cn/practice/25561/

思路：



代码：

```python
def dfs(dis,k):
    if k==n+1:
        ct=0
        for i in range(1,m+1):
            j=0
            tp=0
            for j in range(0,len(disc[i])):
                if disc[i][j][0]<=dis[i]:
                    tp=max(disc[i][j][1],tp)
            ct-=tp
        s=sum(dis)
        ct-=(s//300)*50          
        return ct+s
    p=[]
    for op in av[k]:
        dis[op]+=price[k][op]
        p.append(dfs(dis,k+1))
        dis[op]-=price[k][op]
    return min(p)

n,m=map(int,input().split())
price=[[-1 for j in range(m+1)]for i in range(n+1)]
av=[[] for i in range(n+1)]
for i in range(1,n+1):
    tem=input().split()
    for item in tem:
        item=list(map(int,item.split(':')))
        av[i].append(item[0])
        price[i][item[0]]=item[-1]
disc=[[]for i in range(m+1)]
for i in range(1,m+1):
    tem=input().split()
    for item in tem:
        item=list(map(int,item.split('-')))
        disc[i].append(item)
    disc[i].sort()

dis=[0 for i in range(m+1)]
ans=0
print(dfs(dis,1))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\11-4.png)



### T20741: 两座孤岛最短距离

dfs, bfs, http://cs101.openjudge.cn/practice/20741/

思路：

考试差一点写完……先找到一个岛屿的所有边界点，再一次次向外扩张，第k次时碰到陆地，最短距离就是k

代码：

```python
from collections import deque

n=int(input())
l=[]
for i in range(n):
    tem=input()
    l.append([])
    for j in range(len(tem)):
        l[-1].append(tem[j])
f=False
x=0
y=0
for i in range(n):
    for j in range(n):
        if l[i][j]=='1':
            x=i
            y=j
            f=True
            break
    if f:
        break

st=deque([(x,y)])
side=deque([])
vdt=[[True for _ in range(n)] for _ in range(n)]
vdt[x][y]=False
while st:
    x,y=st.popleft()
    for i,j in [(1,0),(-1,0),(0,1),(0,-1)]:
        if x+i<n and x+i>-1 and y+j<n and y+j >-1 and vdt[x+i][y+j]:
            if l[x+i][y+j]=='0':
                side.append((x,y))
            else:
                l[x+i][y+j]='2'
                st.append((x+i,y+j))
                vdt[x+i][y+j]=False
k=0
while True:
    te=deque([])
    flag=False
    k+=1
    while side:
        x,y=side.popleft()
        for i,j in [(1,0),(-1,0),(0,1),(0,-1)]:
            if x+i<n and x+i>-1 and y+j<n and y+j >-1 and vdt[x+i][y+j]:
                vdt[x+i][y+j]=False
                if l[x+i][y+j]=='1':
                    flag=True
                    break
                else:
                    te.append((x+i,y+j)) 
        if flag:
            break
    side=te
    if flag:
        break    
        
print(k-1)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\11-5.png)



### T28776: 国王游戏

greedy, http://cs101.openjudge.cn/practice/28776

思路：

可以证明任意两个大臣交换位置不影响其他人，而他们两人的最大值最小时要求乘积大的在后，而每两个人大的在后就是冒泡排序，即按乘积大小给所有人升序排序

代码：

```python
n=int(input())
a,b=map(int,input().split())
l=[]
for i in range(n):
    l.append(list(map(int,input().split())))
l=sorted(l,key=lambda x:x[0]*x[1])
for i in range(n-1):
    a*=l[i][0]
print(a//l[-1][1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\11-6.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

考试的时候只AC1，大部分时间耗在思考炸鸡排，后来跳过，双十一又磕了很久，考试结束前差点做完孤岛，后来独立加时半小时，发现孤岛写完就可以AC，国王游戏自己也能想出来……感觉难题还是得先读全卷在着手做——当然更希望期末考试用不到这个教训（doge）



