# Assignment #3: 惊蛰 Mock Exam

Updated 1641 GMT+8 Mar 5, 2025

2025 spring, Complied by 李皓翔 物院



> **说明：**
>
> 1. **惊蛰⽉考**：AC6（有事未现场参加，事后计时考试）。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。
>
> 2. **解题与记录：**
>
>    对于每一个题目，请提供其解题思路（可选），并附上使用Python或C++编写的源代码（确保已在OpenJudge， Codeforces，LeetCode等平台上获得Accepted）。请将这些信息连同显示“Accepted”的截图一起填写到下方的作业模板中。（推荐使用Typora https://typoraio.cn 进行编辑，当然你也可以选择Word。）无论题目是否已通过，请标明每个题目大致花费的时间。
>
> 3. **提交安排：**提交时，请首先上传PDF格式的文件，并将.md或.doc格式的文件作为附件上传至右侧的“作业评论”区。确保你的Canvas账户有一个清晰可见的头像，提交的文件为PDF格式，并且“作业评论”区包含上传的.md或.doc附件。
>
> 4. **延迟提交：**如果你预计无法在截止日期前提交作业，请提前告知具体原因。这有助于我们了解情况并可能为你提供适当的延期或其他帮助。 
>
> 请按照上述指导认真准备和提交作业，以保证顺利完成课程要求。



## 1. 题目

### E04015: 邮箱验证

strings, http://cs101.openjudge.cn/practice/04015



思路：



代码：

```python
while True:
    try:   
        l=input()
        u=True
        if l[0]=='@' or l[0]=='.':
            u=False
        if l[-1]=='@' or l[-1]=='.':
            u=False
        f1=False
        f2=False
        for i in l:
            if f1 and i=='@':
                u=False
                break
            if f1 and i=='.':
                f2=True
                break
            if i=='@' and not f1:
                f1=True
        if '@.' in l or '.@' in l:
            u=False
        o=u and f2 
        o=o and f1
        if o:
            print("YES")
        else:
            print("NO")

    except EOFError:
        break
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250309131332400](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250309131332400.png)



### M02039: 反反复复

implementation, http://cs101.openjudge.cn/practice/02039/



思路：



代码：

```python
n=int(input())
l=input()
m=len(l)//n
ans=''
mat=[['' for j in range(n)]for i in range(m)]
k=False
p=0
for i in range(m):
    k=not k
    if k:
        for j in range(n):
            mat[i][j]=l[p]
            p+=1
    else:
        for j in range(n-1,-1,-1):
            mat[i][j]=l[p]
            p+=1
for i in range(n):
    for j in range(m):
        ans+=mat[j][i]
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250309211154528](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250309211154528.png)



### M02092: Grandpa is Famous

implementation, http://cs101.openjudge.cn/practice/02092/



思路：



代码：

```python
while True:
    N,M=map(int,input().split())
    if N==0:
        break
    s={}
    for i in range(N):
        tem=input().split()
        for it in tem:
            if it in s:
                s[it]+=1
            else:
                s[it]=1
    ss=sorted(s,key=lambda x:s[x],reverse=True)
    i=2
    go=s[ss[1]]
    while i<len(ss):
        if s[ss[i]]!=go:
            break
        i+=1
    print(' '.join(list(map(str,sorted(list(map(int,ss[1:i])))))))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250309212930392](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250309212930392.png)



### M04133: 垃圾炸弹

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

![image-20250309131409916](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250309131409916.png)



### T02488: A Knight's Journey

backtracking, http://cs101.openjudge.cn/practice/02488/



思路：



代码：

```python
def dfs(x,y,b,k,n,m):
    if k==n*m:
        return [(x,y)]
    for i,j in [(-2,-1),(-2,1),(-1,-2),(-1,2),(1,-2),(1,2),(2,-1),(2,1)]:
        if b[x+i][y+j] :
            b[x][y]=False
            pans=dfs(x+i,y+j,b,k+1,n,m)
            b[x][y]=True
            if pans:
                pans.append((x,y))
                return pans
            else:
                continue
    return []


def solution(n,m):
    b=[[False for i in range(n+4)]for j in range(m+4)]
    for i in range(2,m+2):
        for j in range(2,n+2):
            b[i][j]=True
    ans=dfs(2,2,b,1,n,m)
    if ans:
        return ans

for i in range(int(input())):
    n,m=map(int,input().split())
    l=solution(n,m)
    if not l:
        print(f'Scenario #{i+1}:' )
        print('impossible')
        print()
        continue
    l=l[::-1]
    ans=''
    for x,y in l:
        ans+=chr(ord('A')+x-2)+str(y-1)
    print(f'Scenario #{i+1}:' )
    print(ans)
    print()
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250310164429193](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250310164429193.png)



### T06648: Sequence

heap, http://cs101.openjudge.cn/practice/06648/



思路：



代码：

```python
import heapq
def f(p,c,n):
    h=[]
    ans=[]
    vd=set()
    vd.add((0,0))
    heapq.heappush(h,(p[0]+c[0],0,0))
    while len(ans)<n:
        s,i,j=heapq.heappop(h)
        ans.append(s)
        if i+1<n and (i+1,j) not in vd:
            heapq.heappush(h,(p[i+1]+c[j],i+1,j))
            vd.add((i+1,j))
        if j+1<n and (i,j+1) not in vd:
            heapq.heappush(h,(p[i]+c[j+1],i,j+1))
            vd.add((i,j+1)) 
    return ans


for _ in range(int(input())):
    m,n=map(int,input().split())
    l=list(map(int,input().split()))
    l.sort()
    for _ in range(m-1):
        l=f(l,sorted(list(map(int,input().split()))),n)
    print(' '.join(list(map(str,l))))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20250310213039787](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250310213039787.png)



## 2. 学习总结和收获

月考有事没去，自己计时考的，题感觉比计概简单，但好久没做了，会被一些低级错误卡手（指输出格式错误或是缩进漏了）











