# Assignment #7: 20250402 Mock Exam

Updated 1624 GMT+8 Apr 2, 2025

2025 spring, Complied by 李皓翔 物院



> **说明：**
>
> 1. **⽉考**：AC6(自己计时做的，月考有事没去)。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。
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

### E05344:最后的最后

http://cs101.openjudge.cn/practice/05344/



思路：



代码：

```python
class ListNode:
    def __init__(self,value=-1):
        self.val=value
        self.next=None

n,k=map(int,input().split())
head=ListNode(1)
p=head
for i in range(2,n+1):
    cur=ListNode(i)
    p.next=cur
    p=cur
cur.next=head

for i in range(n-1):
    for j in range(k):
        p=cur
        cur=cur.next
    print(cur.val,end=' ')
    p.next=cur.next
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250402192422069](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250402192422069.png)



### M02774: 木材加工

binary search, http://cs101.openjudge.cn/practice/02774/



思路：



代码：

```python
n,k=map(int,input().split())
l=[int(input()) for i in range(n)]
up=max(l)
down=1
if sum(l)<k:
    print(0)
else:
    while up>down:
        length=(up+down+1)//2
        tem=0
        for it in l:
            tem+=it//length
        if tem>=k:
            down=length
        else:
            up=length-1
    print(down)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250402201104963](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250402201104963.png)



### M07161:森林的带度数层次序列存储

tree, http://cs101.openjudge.cn/practice/07161/



思路：



代码：

```python
from collections import deque

class TreeNode:
    def __init__(self,value,num):
        self.val=value
        self.child=[]
        self.branch=num

n=int(input())
forest=[]
for _ in range(n):
    l=input().split()
    root=TreeNode(l[0],int(l[1]))
    i=1
    q=deque([root])
    while q:
        cur=q.popleft()
        for j in range(cur.branch):
            new=TreeNode(l[2*i],int(l[2*i+1]))
            cur.child.append(new)
            if new.branch!=0:
                q.append(new)
            i+=1
    forest.append(root)

def dfs(node:TreeNode):
    if node.branch!=0:
        for it in node.child:
            dfs(it) 
    print(node.val,end=' ')

for it in forest:
    dfs(it)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250403113401212](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250403113401212.png)



### M18156:寻找离目标数最近的两数之和

two pointers, http://cs101.openjudge.cn/practice/18156/



思路：



代码：

```python
n=int(input())
l=list(map(int,input().split()))
l.sort()
i=0
j=len(l)-1
ans=float('inf')
while i<j:
    tem=l[i]+l[j]
    if tem==n:
        ans=tem
        break
    if abs(tem-n)<abs(ans-n) or (abs(tem-n)==abs(ans-n) and tem<ans):
        ans=tem
    if tem>n:
        j-=1
    if tem<n:
        i+=1
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250403102043680](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250403102043680.png)



### M18159:个位为 1 的质数个数

sieve, http://cs101.openjudge.cn/practice/18159/



思路：



代码：

```python
import math

T=int(input())
request=[int(input()) for i in range(T)]
n=max(request)
prime=[True for i in range(n+1)]
prime[0],prime[1]=False,False
for i in range(2,int(math.sqrt(n))+1):
    if prime[i]:
        for j in range(i*i,n,i):
            prime[j]=False
ans=[]
for it in request:
    tem=[]
    for i in range(11,it,10):
        if prime[i]:
            tem.append(i)
    ans.append(tem)
for i in range(T):
    print(f'Case{i+1}:')
    if len(ans[i]):
        print(' '.join(list(map(str,ans[i]))))
    else:
        print('NULL')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250403104220214](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250403104220214.png)



### M28127:北大夺冠

hash table, http://cs101.openjudge.cn/practice/28127/



思路：



代码：

```python
M=int(input())
dic={} #name:[[pass_qus],try_times]
for i in range(M):
    name,q,r=input().split(',')
    if name not in dic:
        dic[name]=[set(),0]
    dic[name][1]+=1
    if r=='yes':
        dic[name][0].add(q)
grades=sorted(list(dic.keys()),key=lambda x:[-len(dic[x][0]),dic[x][1],x])
for i in range(min(len(grades),12)):
    print(i+1,grades[i],len(dic[grades[i]][0]),dic[grades[i]][1])
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20250403105900202](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250403105900202.png)



## 2. 学习总结和收获

月考有事没去，跟进作业和选做，还是没有什么卡点的











