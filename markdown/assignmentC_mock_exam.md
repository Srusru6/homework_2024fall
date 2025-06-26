# Assignment #C: 202505114 Mock Exam

Updated 1518 GMT+8 May 14, 2025

2025 spring, Complied by 李皓翔 物院



> **说明：**
>
> 1. **⽉考**：AC6 。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。
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

### E06364: 牛的选举

http://cs101.openjudge.cn/practice/06364/

思路：



代码：

```python
n,k=map(int,input().split())
a=[]
for i in range(n):
    a.append(list(map(int,input().split()))+[i+1])
a=sorted(a,reverse=True)
b=a[:k]
b=sorted(b,reverse=True,key=lambda x:x[1])
print(b[0][2])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250520205509094](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250520205509094.png)



### M04077: 出栈序列统计

http://cs101.openjudge.cn/practice/04077/

思路：



代码：

```python
n=int(input())

def f(x,cr):
    if x==n:
        return 1
    if cr==0:
        return f(x+1,1)
    else:
        return f(x+1,cr+1)+f(x,cr-1)

print(f(0,0))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250520210551344](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250520210551344.png)



### M05343:用队列对扑克牌排序

http://cs101.openjudge.cn/practice/05343/

思路：



代码：

```python
q=[[] for i in range(9)]
n=int(input())
l=input().split()
q2=[[] for i in range(4)]
for it in l:
    q[int(it[1])-1].append(it)
for tem in q:
    for it in tem:
        q2[ord(it[0])-ord('A')].append(it)
ans=[]
for tem in q2:
    for it in tem:
        ans.append(it)
    
for i in range(9):
    tem=' '.join(q[i])
    print(f'Queue{i+1}:'+tem)
for j in range(4):
    tem=' '.join(q2[j])
    ap=chr(ord('A')+j)
    print('Queue'+ap+':'+tem)
print(' '.join(ans))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250520212122423](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250520212122423.png)



### M04084: 拓扑排序

http://cs101.openjudge.cn/practice/04084/

思路：



代码：

```python
class GraphPoint:
    def __init__(self,value):
        self.child=[]
        self.parent=[]
        self.value=value


v,a=map(int,input().split())
b=[True for i in range(v)]
m=[GraphPoint(i) for i in range(v+1)]
for i in range(a):
    x,y=map(int,input().split())
    b[y-1]=False
    m[x].child.append(y)
    m[y].parent.append(x)
s=[]
for i in range(v):
    if b[i]:
        s.append(i+1)

ans=[]
t=[]
while s:
    i=s[0]
    s=s[1:]
    ans.append(i)
    for j in m[i].child:
        m[j].parent.remove(i)
        if not m[j].parent:
            s.append(j)
    s.sort()
tem=[f'v{ans[i]}'for i in range(v)]
print(' '.join(tem))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250520214619805](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250520214619805.png)



### M07735:道路

Dijkstra, http://cs101.openjudge.cn/practice/07735/

思路：



代码：

```python
import heapq

K = int(input())
N = int(input())
R = int(input())

adj = [[] for _ in range(N + 1)]
for _ in range(R):
    s, d, L, T = map(int, input().split())
    adj[s].append((d, L, T))

dist = [[float('inf')] * (K + 1) for _ in range(N + 1)]
dist[1][0] = 0 

heap = []
heapq.heappush(heap, (0, 1, 0))

result = -1
found = False

while heap:
    current_dist, u, cost = heapq.heappop(heap)
    if u == N:
        result = current_dist
        break
    if current_dist > dist[u][cost]:
        continue  
    for edge in adj[u]:
        v, L, T = edge
        new_cost = cost + T
        if new_cost > K:
            continue  
        new_dist = current_dist + L
        if new_dist < dist[v][new_cost]:
            dist[v][new_cost] = new_dist
            heapq.heappush(heap, (new_dist, v, new_cost))

print(result)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250520221314052](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250520221314052.png)



### T24637:宝藏二叉树

dp, http://cs101.openjudge.cn/practice/24637/

思路：



代码：

```python
n = int(input())
val = list(map(int, input().split()))
val = [0] + val 

def dfs(i):
    if i > n:
        return (0, 0)
    left = dfs(2 * i)
    right = dfs(2 * i + 1)
    rob = val[i] + left[1] + right[1]
    not_rob = max(left[0], left[1]) + max(right[0], right[1])
    return (rob, not_rob)

max_rob = max(dfs(1))
print(max_rob)

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250520224518809](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250520224518809.png)



## 2. 学习总结和收获

<mark>如果发现作业题目相对简单，有否寻找额外的练习题目，如“数算2025spring每日选做”、LeetCode、Codeforces、洛谷等网站上的题目。</mark>











