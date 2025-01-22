# Assignment #D: 十全十美 

Updated 1254 GMT+8 Dec 17, 2024

2024 fall, Complied by 李皓翔 物院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 02692: 假币问题

brute force, http://cs101.openjudge.cn/practice/02692

思路：



代码：

```python
n=int(input())
for _ in range(n):
    l=[0 for i in range(12)]
    for _ in range(3):
        tem=input().split()
        if tem[-1]=='even':
            for i in tem[0]:
                l[ord(i)-ord('A')]=4
            for i in tem[1]:
                l[ord(i)-ord('A')]=4
        else:
            a=1
            b=-1
            if tem[-1]=='down':
                a=-1
                b=1
            for i in tem[0]:
                if l[ord(i)-ord('A')]!=4 :
                    l[ord(i)-ord('A')]+=a
            for i in tem[1]:
                if l[ord(i)-ord('A')]!=4 :
                    l[ord(i)-ord('A')]+=b
    ans=[0,0]
    for i in range(12):
        if abs(l[i])>abs(ans[0]) and l[i]!=4:
            ans=[l[i],i]
    if ans[0]<0:
        an='light'
    else:
        an='heavy'
    print(f"{chr(ans[1]+ord('A'))} is the counterfeit coin and it is {an}. ")

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### 01088: 滑雪

dp, dfs similar, http://cs101.openjudge.cn/practice/01088

思路：



代码：

```python
def dfs(x,y):
    if dp[x][y]==1:
        p=[1]
        for i,j in [(1,0),(-1,0),(0,1),(0,-1)]:
            if h[x+i][y+j]<h[x][y]:
                p.append(dfs(x+i,y+j)+1)
        dp[x][y]=max(p)
    return dp[x][y]
R,C=map(int,input().split())
h=[[float('inf') for _ in range(C+2)]for _ in range(R+2)]
dp=[[1 for _ in range(C+2)]for _ in range(R+2)]
for i in range(1,R+1):
    tem=list(map(int,input().split()))
    for j in range(C):
        h[i][j+1]=tem[j]
ans=1
for xp  in range(1,R+1):
    for yp in range(1,C+1):
        ans=max(ans,dfs(xp,yp))
print(ans)
```



代码运行截图 ==（至少包含有"Accepted"）==





### 25572: 螃蟹采蘑菇

bfs, dfs, http://cs101.openjudge.cn/practice/25572/

思路：



代码：

```python
def dfs(bp):
    x=[bp[0][0],bp[1][0]]
    y=[bp[0][1],bp[1][1]]
    p=False
    if map[x[0]][y[0]]=='9' or map[x[1]][y[1]]=='9':
        return True
    for i,j in [(1,0),(-1,0),(0,1),(0,-1)]:
        if map[x[0]+i][y[0]+j]!='1' and map[x[1]+i][y[1]+j]!='1' and vd[x[0]][y[0]]:
            vd[x[0]][y[0]]=False
            p=p or dfs([(x[0]+i,y[0]+j),(x[1]+i,y[1]+j)])
            vd[x[0]][y[0]]=True
    return p

n=int(input())
map=[['1' for _ in range(n+2)]for _ in range(n+2)]
bp=[]
for i in range(1,n+1):
    tem=input().split()
    for j in range(1,n+1):
        if tem[j-1]!='5':
            map[i][j]=tem[j-1]
        else:
            map[i][j]='0'
            bp.append((i,j))
vd=[[True for _ in range(n+2)]for _ in range(n+2)]
if dfs(bp):
    print('yes')
else:
    print('no')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### 27373: 最大整数

dp, http://cs101.openjudge.cn/practice/27373/

思路：



代码：

```python
m=int(input())
n=int(input())
l=input().split()
for i in range(n-1):
    for j in range(n-2,i-1,-1):
        if  l[j]+l[j+1] <l[j+1]+l[j]:
            l[j],l[j+1]=l[j+1],l[j]
dp=['' for _ in range(m+1)]
for i in range(n):
    for j in range(m,len(l[i])-1,-1):
        if dp[j-len(l[i])]!='' or j==len(l[i]):
            dp[j]=max(dp[j-len(l[i])]+l[i],dp[j])
i=m
while dp[i]=='':
    i-=1
print(int(dp[i])) 
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### 02811: 熄灯问题

brute force, http://cs101.openjudge.cn/practice/02811

思路：



代码：

```python
import copy

def r(x):
    return (x+1)%2

l=[]
for i in range(5):
    l.append(list(map(int,input().split())))
li=[]
for i in range(2**6):
    tem=[]
    a=i
    for j in range(6):
        tem.append(a%2)
        a=a//2
    li.append(tem)
for case in li:
    pl=copy.deepcopy(l)
    act=[case]
    for i in range(5):
        for j in range(6):
            if act[i][j]==1:
                if j>0:
                    l[i][j-1]=r(l[i][j-1])
                if j<5:
                    l[i][j+1]=r(l[i][j+1])
                l[i][j]=r(l[i][j])
                if i<4:
                    l[i+1][j]=r(l[i+1][j])
        if i<4:
            tem=[l[i][k] for k in range(6)]
            act.append(tem)
    fl=True
    for k in l[-1]:
        if k==1:
            fl=False
            break
    if fl:
        break
    l=pl
for i in act:
    for j in i:
        print(j,end=' ')
    print()
            
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### 08210: 河中跳房子

binary search, greedy, http://cs101.openjudge.cn/practice/08210/

思路：



代码：

```python
L,N,M=map(int,input().split())
gap=[]
pt=0
for i in range(N):
    p=int(input())
    gap.append(p-pt)
    pt=p
gap.append(L-pt)
r=0
l=L
ans=[]
while r+1<l:
    m=(r+l)//2
    p=0
    s=0
    for i in gap:
        p+=i
        if p>=m:
            p=0
        else:
            s+=1
    if s>M:
        l=m
    else:
        r=m
        if s==M:
            ans.append(m)


print(max(ans))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

感觉最近题感上来了，考试加油，河中跳房子看的题解，感觉这个反向思路自己想还是困难的，思路一直是正向去遍历，看题解才恍然大悟


