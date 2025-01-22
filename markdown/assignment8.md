# Assignment #8: 田忌赛马来了

Updated 1021 GMT+8 Nov 12, 2024

2024 fall, Complied by 李皓翔 物院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 12558: 岛屿周⻓

matices, http://cs101.openjudge.cn/practice/12558/ 

思路：



代码：

```python
n,m=map(int,input().split())
l=[list(input().split()) for i in range(n)]
s=[ [] for i in range(n)]
for i in range(n):
	s[i].append(0)
	for j in range(m):
		s[i].append(int(l[i][j]))
	s[i].append(0)
s=[[0 for i in range(m+2)]]+s+[[0 for i in range(m+2)]]
ans=0
for x in range(1,n+1):
	for y in range(1,m+1):
		if s[x][y]==1:
			if s[x+1][y]==0:
				ans+=1
			if s[x][y+1]==0:
				ans+=1
			if s[x-1][y]==0:
				ans+=1
			if s[x][y-1]==0:
				ans+=1
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\8-1.png)



### LeetCode54.螺旋矩阵

matrice, https://leetcode.cn/problems/spiral-matrix/

与OJ这个题目一样的 18106: 螺旋矩阵，http://cs101.openjudge.cn/practice/18106

思路：



代码：

```python
n=int(input())
s=[[0 for i in range(n)]for j in range(n)]
l=0
r=n-1
u=0
d=n-1
a=0
while l<r and u<d:
	for i in range(l,r+1):
		a+=1
		s[u][i]=a
	u+=1
	for i in range(u,d+1):
		a+=1
		s[i][r]=a
	r-=1
	for i in range(r,l-1,-1):
		a+=1
		s[d][i]=a
	d-=1
	for i in range(d,u-1,-1):
		a+=1
		s[i][l]=a
	l+=1
if n%2==1:
	s[n//2][n//2]=a+1
for i in s:
	print(' '.join(list(map(str,i))))
```



代码运行截图 ==（至少包含有"Accepted"）==

![](..\pic\8-2.png)



### 04133:垃圾炸弹

matrices, http://cs101.openjudge.cn/practice/04133/

思路：



代码：

```python
d=int(input())
n=int(input())
t=[list(map(int,input().split())) for i in range(n)]
ans=0
m=0
for i in range(1025):
	for j in range(1025):
		s=0
		for it in t:
			x,y,p=map(int,it)
			if abs(x-i)<=d and abs(y-j)<=d:
				s+=p
		if s>m:
			m=s
			ans=1
		elif s==m:
			ans+=1
print(ans,m)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\8-3.png)



### LeetCode376.摆动序列

greedy, dp, https://leetcode.cn/problems/wiggle-subsequence/

与OJ这个题目一样的，26976:摆动序列, http://cs101.openjudge.cn/routine/26976/

思路：



代码：

```python
n=int(input())
l=list(map(int,input().split()))
dp=[[1001,-1001] for i in range(n+1)]
up=0
for x in l:
	for i in range(up,-1,-1):
		if x>dp[i][0]:
			dp[i+1][1]=max(x,dp[i+1][1])
		if x<dp[i][1]:
			dp[i+1][0]=min(x,dp[i+1][0])
	up+=1
	dp[0][1]=max(x,dp[0][1])
	dp[0][0]=min(x,dp[0][0])
for i in range(n,-1,-1):
	if dp[i][0]!=1001 or dp[i][1]!=-1001:
		print(i+1)
		break
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\8-4.png)



### CF455A: Boredom

dp, 1500, https://codeforces.com/contest/455/problem/A

思路：



代码：

```python
n=int(input())
l=list(map(int,input().split()))
d={}
for i in range(n):
	if l[i] in d:
		d[l[i]]+=1
	else:
		d[l[i]]=1
ind=list(d.keys())
ind.sort()
dp=[0 for i in range(len(ind))]
dp[0]=d[ind[0]]*ind[0]
for i in range(1,len(ind)):
	if ind[i]!=ind[i-1]+1:
		dp[i]=dp[i-1]+d[ind[i]]*ind[i]
	else:
		dp[i]=max(dp[i-2]+d[ind[i]]*ind[i],dp[i-1])
print(dp[-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\8-5.png)



### 02287: Tian Ji -- The Horse Racing

greedy, dfs http://cs101.openjudge.cn/practice/02287

思路：



代码：

```python
while True:
	n=int(input())
	if n==0:
		break
	t=list(map(int,input().split()))
	k=list(map(int,input().split()))
	t.sort()
	k.sort()
	dp=[[0 for i in range(n+1)]for j in range(n+1)]
	for i in range(1,n+1):
		for j in range(1,n+1):
			if t[i-1]>k[j-1]:
				p=2
			elif t[i-1]<k[j-1]:
				p=0
			else:
				p=1
			dp[i][j]=max(dp[i-1][j],dp[i][j-1],dp[i-1][j-1]+p)

	print(dp[-1][-1]*200-n*200)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\8-6.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

前面五题都还行，田忌的greedy方法真的折磨，试了好几次才独立做出来；看到还有dp，做了一次就对了，20000ms但是没超时，只能说题目出的太善良了（捂脸）



