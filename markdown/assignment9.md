# Assignment #9: dfs, bfs, & dp

Updated 2107 GMT+8 Nov 19, 2024

2024 fall, Complied by 李皓翔 物院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 18160: 最大连通域面积

dfs similar, http://cs101.openjudge.cn/practice/18160

思路：



代码：

```python
def f(x,y):
	if s[x][y]=='.':
		return 0
	p=1
	s[x][y]='.'
	for xi,yi in [(0,1),(0,-1),(1,1),(1,0),(1,-1),(-1,1),(-1,0),(-1,-1)]:
		p+= f(x+xi,y+yi)
	return p


for _ in range(int(input())):
	N,M=map(int,input().split())
	s=[['.' for i in range(M+2)] for j in range(N+2)]
	for i in range(1,N+1):
		s[i][1:M+1]=input()
	ans=[0]
	for i in range(1,N+1):
		for j in range(1,M+1):
			if s[i][j]=='W':
				ans.append(f(i,j))
	print(max(ans))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\9-1.png)



### 19930: 寻宝

bfs, http://cs101.openjudge.cn/practice/19930

思路：



代码：

```python
def f(x,y,p,s):
	if s[x][y]==1:
		return p
	if s[x][y]==2:
		return 999999
	else:
		s[x][y]=2
		tem=[]
		for i,j in [(1,0),(0,1),(-1,0),(0,-1)]:
			tem.append(f(x+i,y+j,p+1,s))
		s[x][y]=0
		return min(tem)


m,n=map(int,input().split())
s=[[2 for i in range(n+2)]for j in range(m+2)]
for i in range(1,m+1):
	s[i][1:-1]=list(map(int,input().split()))
ans=f(1,1,0,s)
if ans==999999:
	print('NO')
else:
	print(ans)
```



代码运行截图 ==（至少包含有"Accepted"）==

![](..\pic\9-2.png)



### 04123: 马走日

dfs, http://cs101.openjudge.cn/practice/04123

思路：



代码：

```python
def f(x, y, b,p):
    if b[x][y] == 1:
        b[x][y] = 0
        fl = True
        for i in b:
            for j in i:
                if j==1:
                    fl = False
                    break
        if fl:
            p+=1
        else:
            for i, j in [(1, 2), (1, -2), (2, 1), (2, -1), (-1, 2), (-1, -2), (-2, -1), (-2, 1)]:
                b,p = f(x + i, y + j, b, p)
        b[x][y] = 1
    return b,p

for _ in range(int(input())):
    n, m, x,y = map(int, input().split())
    b = [[0 for j in range(m + 4)] for i in range(n + 4)]
    for i in range(2, n + 2):
        for j in range(2, m + 2):
            b[i][j] = 1
    p=0
    b,p=f(x+2,y+2,b,p)
    print(p)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\9-3.png)



### sy316: 矩阵最大权值路径

dfs, https://sunnywhy.com/sfbj/8/1/316

思路：



代码：

```python
def f(x,y,b):
    if  x==n and y==m:
        return 0,[n,m]
    ans=[]
    tem=b[x][y]
    b[x][y]=-101
    for i,j in [(-1,0),(1,0),(0,1),(0,-1)]:
        if b[x+i][y+j]!=-101 :
            ans.append(f(x+i,y+j,b))
    b[x][y]=tem
    if len(ans)==0:
        return -100000,[-1,-1]
    ans=sorted(ans,key=lambda x:x[0])
    if ans[-1][0]!=-100000:
        return ans[-1][0]+b[x][y],[x,y]+ans[-1][1]
    else:
        return -100000,[-1,-1]

        
n,m=map(int,input().split())
b=[[-101 for i in range(m+2)] for j in range(n+2)]

for i in range(1,n+1):
    b[i][1:-1]=list(map(int,input().split()))
a,c=f(1,1,b)
for i in range(0,len(c),2):
    print(c[i],c[i+1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\9-4.png)





### LeetCode62.不同路径

dp, https://leetcode.cn/problems/unique-paths/

思路：



代码：

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp=[[0 for j in range(n+1)]for i in range(m+1)]
        dp[m][n-1]=1
        for i in range(m-1,-1,-1):
            for j in range(n-1,-1,-1):
                dp[i][j]=dp[i+1][j]+dp[i][j+1]
        return dp[0][0]
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\9-5.png)



### sy358: 受到祝福的平方

dfs, dp, https://sunnywhy.com/sfbj/8/3/539

思路：



代码：

```python
def f(l,p):
    if int(l)==0:
        return False
    if len(l)==1:
        if l in['1','4','9']:
            return True
        else:
            return False
    fl=False
    for i in range(1,len(l)):
        if f(l[0:i],p) and f(l[i:len(l)],p):
            fl=True
    if l in p:
        fl=True
    return fl


n=int(input())
p=[]
i=1
while i**2<=n:
    p.append(str(i**2))
    i+=1
if f(str(n),p):
    print('Yes')
else:
    print('No')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\9-6.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

感觉dfs，bfs题还是有些吃力，争取多刷题



