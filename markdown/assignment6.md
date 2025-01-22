# Assignment #6: Recursion and DP

Updated 2201 GMT+8 Oct 29, 2024

2024 fall, Complied by 李皓翔 物院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### sy119: 汉诺塔

recursion, https://sunnywhy.com/sfbj/4/3/119  

思路：



代码：

```python
def pra(x,y):
    return chr(3*ord("B")-ord(x)-ord(y))

def drop(x,y,a):
    
    if a==1:
        ans.append(x+'->'+y)
    else:
        drop(x,pra(x,y),a-1)
        ans.append(x+'->'+y)
        drop(pra(x,y),y,a-1)


n=int(input()) 
ans=[]       
drop("A","C",n)
print(len(ans))
for i in ans:
    print(i)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\6-1.png)



### sy132: 全排列I

recursion, https://sunnywhy.com/sfbj/4/3/132

思路：



代码：

```python
def list(n,i,l,s,ans):
    if i==1:
        for j in range(n):
            if l[j]:
                s.append(j+1)   
                ans.append(s[:])
                s.pop()
    else:
        for j in range(n):
            if l[j]:
                l[j]=False
                s.append(j+1)
                list(n,i-1,l,s,ans)
                l[j]=True
                s.pop()
            
n=int(input())
l=[True for k in range(n)]
ans=[]
s=[]
list(n,n,l,s,ans)
for i in ans:
    print(' '.join(map(str,i)))
```



代码运行截图 ==（至少包含有"Accepted"）==

![](..\pic\6-2.png)



### 02945: 拦截导弹

dp, http://cs101.openjudge.cn/2024fallroutine/02945

思路：



代码：

```python
n=int(input())
l=list(map(int,input().split()))
l=l[::-1]
a=[-1 for i in range(n)]
a[0]=l[0]
up=0
for i in l[1:]:
    for j in range(up,-1,-1):
        if a[j]<=i:
            if a[j+1]==-1:
                a[j+1]=i
            else:
                a[j+1]=min(a[j+1],i)
            if j==up:
                up+=1
            break
        if j==0 and i<a[0]:
            a[0]=i

print(up+1)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\6-3.png)



### 23421: 小偷背包 

dp, http://cs101.openjudge.cn/practice/23421

思路：



代码：

```python
N,B=map(int,input().split())
l=[]
price=list(map(int,input().split()))
weight=list(map(int,input().split()))
for i in range(N):
    l.append([weight[i],price[i]])
l.sort()
p=[0 for i in range(B+1)]
for item in l:
    if item[0]>B:
        continue
    for i in range(B,item[0]-1,-1):
        if p[i-item[0]]!=0 or i==item[0]:
            p[i]=max(p[i],p[i-item[0]]+item[1])
up=B
while True:
    if up==0 or p[up]!=0 :
        print(p[up])
        break
    up-=1
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\6-4.png)



### 02754: 八皇后

dfs and similar, http://cs101.openjudge.cn/practice/02754

思路：



代码：

```python
import copy

def f(i,fill,s,ans):
    if i==8:
        ans.append(s[:])
    else:
        for j in range(1,9):
            if fill[i][j]:
                tem=copy.deepcopy(fill)
                s.append(j)
                for k in range(1,8-i):
                    fill[i+k][j]=False
                for k in range(1,8-i):
                    if j+k<=8 and j+k>=1:
                        fill[i+k][j+k]=False
                    if j-k<=8 and j-k>=1:
                        fill[i+k][j-k]=False
                f(i+1,fill,s,ans)
                s.pop()
                fill=tem


fill=[[True for m in range(9)] for k in range(9)]
ans=[]
f(0,fill,[],ans)

for i in range(int(input())):
    print(''.join(map(str,ans[-1+int(input())])))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\6-5.png)



### 189A. Cut Ribbon 

brute force, dp 1300 https://codeforces.com/problemset/problem/189/A

思路：



代码：

```python
n,a,b,c=map(int,input().split())
p=[0 for i in range(n+1)]
l=[a,b,c]
l.sort()
for it in l:
    for i in range(it,n+1):
        if p[i-it]!=0 or i==it:
            p[i]=max(p[i],p[i-it]+1)
print(p[-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\6-6.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

感觉跟进每日选做，最近题目感觉一下就上来了，作业没有什么卡顿就很快完成了。

也是在同步看《算法基础与在线实践》，看到动态规划之前。



