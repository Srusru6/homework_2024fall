# Assignment #D: 图 & 散列表

Updated 2042 GMT+8 May 20, 2025

2025 spring, Complied by 李皓翔 物院



> **说明：**
>
> 1. **解题与记录：**
>
>    对于每一个题目，请提供其解题思路（可选），并附上使用Python或C++编写的源代码（确保已在OpenJudge， Codeforces，LeetCode等平台上获得Accepted）。请将这些信息连同显示“Accepted”的截图一起填写到下方的作业模板中。（推荐使用Typora https://typoraio.cn 进行编辑，当然你也可以选择Word。）无论题目是否已通过，请标明每个题目大致花费的时间。
>
> 2. **提交安排：**提交时，请首先上传PDF格式的文件，并将.md或.doc格式的文件作为附件上传至右侧的“作业评论”区。确保你的Canvas账户有一个清晰可见的头像，提交的文件为PDF格式，并且“作业评论”区包含上传的.md或.doc附件。
>
> 3. **延迟提交：**如果你预计无法在截止日期前提交作业，请提前告知具体原因。这有助于我们了解情况并可能为你提供适当的延期或其他帮助。 
>
> 请按照上述指导认真准备和提交作业，以保证顺利完成课程要求。



## 1. 题目

### M17975: 用二次探查法建立散列表

http://cs101.openjudge.cn/practice/17975/

<mark>需要用这样接收数据。因为输入数据可能分行了，不是题面描述的形式。OJ上面有的题目是给C++设计的，细节考虑不周全。</mark>

```python
import sys
input = sys.stdin.read
data = input().split()
index = 0
n = int(data[index])
index += 1
m = int(data[index])
index += 1
num_list = [int(i) for i in data[index:index+n]]
```



思路：

忘记输入可以重复了，代码补的有些难看

代码：

```python
import sys
input = sys.stdin.read
data = input().split()
index = 0
n = int(data[index])
index += 1
m = int(data[index])
index += 1
num_list = [int(i) for i in data[index:index+n]]
hash=[True for i in range(m)]
ans=[]
vd=set()
h={}
for i in range(n):
    if num_list[i] in vd:
        ans.append(h[num_list[i]])
        continue
    vd.add(num_list[i])
    ind=num_list[i]%m
    j=1
    rind=ind+(-1)**j*(j//2)**2
    while not hash[rind]:
        j+=1
        rind=(ind+(-1)**j*(j//2)**2)%m
    ans.append(rind)
    hash[rind]=False
    h[num_list[i]]=rind
print(' '.join(list(map(str,ans))))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250527130943626](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250527130943626.png)



### M01258: Agri-Net

MST, http://cs101.openjudge.cn/practice/01258/

思路：

审题没看到”多组数据“，调了半天

代码：

```python
from heapq import *

while True:
    try:
        n=int(input())
        link = [[0] * n for _ in range(n)]

        arr = []
        while len(arr) < n * n:
            arr += list(map(int, input().split()))

        k = 0
        for i in range(n):
            for j in range(n):
                link[i][j] = (arr[k], j)
                k += 1

        vd=set()
        vd.add(0)
        h=link[0][1:]
        heapify(h)

        ans=0
        while len(vd)<n:
            l,des=heappop(h)
            if des in vd:
                continue
            vd.add(des)
            ans+=l
            for i in range(n):
                if i in vd:
                    continue
                heappush(h,link[des][i])
        print(ans)
    except EOFError:
        break
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250527135925512](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250527135925512.png)



### M3552.网络传送门旅游

bfs, https://leetcode.cn/problems/grid-teleportation-traversal/

思路：

容易tle

代码：

```python
class Solution:
    def minMoves(self, matrix: List[str]) -> int:
        from collections import deque
        from collections import defaultdict
        n=len(matrix)
        m=len(matrix[0])
        link=defaultdict(list)
        for i in range(n):
            for j in range(m):
                if matrix[i][j]!='.' and matrix[i][j]!='#':
                    link[matrix[i][j]].append((i,j))

        vd=[[n*m +1 for j in range(m)]for i in range(n)]
        vd[0][0]=0
        q=deque([(0,0,0)])
        if matrix[0][0]!='.':
            for x,y in link[matrix[0][0]]:
                if x==0 and y==0:
                    continue
                q.append((x,y,0))
        while q:
            x,y,d=q.popleft()
            if x==n-1 and y==m-1:
                return d
            for i,j in [(1,0),(-1,0),(0,1),(0,-1)]:
                xx,yy=x+i,y+j
                if xx>=0 and xx<n and yy>=0 and yy<m and matrix[xx][yy]!='#':
                    if d+1<vd[xx][yy]:
                        vd[xx][yy]=d+1
                        q.append((xx,yy,d+1))
                    if matrix[xx][yy]!='.':
                        for xxx,yyy in link[matrix[xx][yy]]:
                            if xxx==xx and yyy==yy:
                                continue
                            if d+1<vd[xxx][yyy]:
                                q.append((xxx,yyy,d+1))
                                vd[xxx][yyy]=d+1
                        del link[matrix[xx][yy]]
        
        return -1
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250527171506367](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250527171506367.png)



### M787.K站中转内最便宜的航班

Bellman Ford, https://leetcode.cn/problems/cheapest-flights-within-k-stops/

思路：



代码：

```python
class Solution:
    def findCheapestPrice(self, n: int, flights: List[List[int]], src: int, dst: int, k: int) -> int:
        graph=[[] for _ in range(n)]
        for it in flights:
            graph[it[0]].append((it[0],it[1],it[2]))
        
        vd=[[float('inf') for j in range(k+2)] for i in range(n)]
        vd[src]=[0 for j in range(k+2)]
        q=[(-1,src,0)]
        for i in range(k+1):
            nq=[]
            for it in q:
                x,y,price=it
                for item in graph[y]:
                    y,z,p2=item
                    if  vd[y][i]+p2<vd[z][i+1]:
                        nq.append((y,z,p2))
                        vd[z][i+1]=vd[y][i]+p2
            q=nq
        ans=min(vd[dst])
        if ans==float('inf'):
            return -1
        return ans
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250527195535275](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250527195535275.png)



### M03424: Candies

Dijkstra, http://cs101.openjudge.cn/practice/03424/

思路：



代码：

```python
from heapq import *
n,m=map(int,input().split())
graph=[[]for _ in range(n)]
for _ in range(m):
    x,y,l=map(int,input().split())
    graph[x-1].append((l,y-1))

q=[(0,0)]
heapify(q)
vd=[float('inf') for _ in range(n)]
vd[0]=0

while q:
    pl,x=heappop(q)
    if pl>vd[x]:
        continue
    for it in graph[x]:
        l,y=it
        if pl+l<vd[y]:
            vd[y]=pl+l
            heappush(q,(vd[y],y))
print(vd[n-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250527203749881](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250527203749881.png)



### M22508:最小奖金方案

topological order, http://cs101.openjudge.cn/practice/22508/

思路：



代码：

```python
n,m=map(int,input().split())
vd=set(range(n))
graph=[set() for i in range(n)]
pre=[set() for i in range(n)]

for i in range(m):
    x,y=map(int,input().split())
    if x in vd:
        vd.remove(x)
    graph[y].add(x)
    pre[x].add(y)

ans=100*n
price=0
while len(vd)!=0:
    for i in list(vd):
        ans+=price
        vd.remove(i)

        for j in graph[i]:
            pre[j].remove(i)
            if len(pre[j])==0:
                vd.add(j)

    price+=1
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250527213412235](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250527213412235.png)



## 2. 学习总结和收获

努力刷题ing，机考加油！











