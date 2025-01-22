# Assignment #4: T-primes + 贪心

Updated 0337 GMT+8 Oct 15, 2024

2024 fall, Complied by 李皓翔  物院

**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知9月19日导入选课名单后启用。**作业写好后，保留在自己手中，待9月20日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 34B. Sale

greedy, sorting, 900, https://codeforces.com/problemset/problem/34/B



思路：



代码

```python
n,k=map(int,input().split())
l=list(map(int,input().split()))
a=0
for i in range(k):
    if min(l)>=0:
        break
    a-=min(l)
    l.pop(l.index(min(l)))
print(a)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![4-1](..\pic\4-1.png)

### 160A. Twins

greedy, sortings, 900, https://codeforces.com/problemset/problem/160/A

思路：



代码

```python
n=int(input())
l=list(map(int,input().split()))
l.sort()
l=l[::-1]
s=sum(l)
p=0
j=0
for i in l:
    j+=1
    p+=i
    if p>s//2:
        break
print(j)
```



代码运行截图 ==（至少包含有"Accepted"）==

![4-2](..\pic\4-2.png)

### 1879B. Chips on the Board

constructive algorithms, greedy, 900, https://codeforces.com/problemset/problem/1879/B

思路：

最优解必为一列与一行两种情况中的最小值

代码

```python
for t in range(int(input())):
    n=int(input())
    a=list(map(int,input().split()))
    b=list(map(int,input().split()))
    print(min(sum(b)+n*min(a),sum(a)+n*min(b)))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![4-3](C:\Users\15143\Desktop\pic\4-3.png)



### 158B. Taxi

*special problem, greedy, implementation, 1100, https://codeforces.com/problemset/problem/158/B

思路：



代码

```python
n=int(input())
l=list(map(int,input().split()))
p=[0 for i in range(4)]
for i in l:
    p[i-1]+=1
a=p[0]
b=p[1]
c=p[2]
d=p[3]
ans=d
ans+=c
a-=min(a,c)
ans+=b//2
if b%2==1:
    ans+=1
    a-=min(a,2)
ans+=(a-1)//4+1
print(ans)

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![4-4](..\pic\4-4.png)



### *230B. T-primes（选做）

binary search, implementation, math, number theory, 1300, http://codeforces.com/problemset/problem/230/B

思路：



代码

```python

import math as m
 
n = int(input())
l = list(map(int, input().split()))
q = max(l)
 
s = [True] * (int(m.sqrt(q)) + 1)
s[0] = s[1] = False
for i in range(2, int(m.sqrt(q)) + 1):
    if s[i]:
        for j in range(i * i, int(m.sqrt(q)) + 1, i):
            s[j] = False
 
p = [i for i, a in enumerate(s) if a]
pl = {i**2 for i in p}
 
for i in l:
    if i in pl:
        print("YES")
    else:
        print("NO")

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![4-5](..\pic\4-5.png)



### *12559: 最大最小整数 （选做）

greedy, strings, sortings, http://cs101.openjudge.cn/practice/12559

思路：

贪心策略：

情况1：前两个无包含关系，取小/大者

情况2：前两个有包含关系，取长度长者相同部分后与短者比较，取小/大者

综合得程序中的实现方法，取x+y，y+x小/大者

代码

```python
def compare(x,y):
    if x+y>y+x:
        return False
    else:
        return True

n=int(input())
l=input().split()
for i in range(n):
    for j in range(n-1):
        if compare(l[j],l[j+1]):
            l[j+1],l[j]=l[j],l[j+1]
p=''
for i in l:
    p+=i
print(p,end=' ')
p=''
for i in l[::-1]:
    p+=i
print(p)

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![4-5](..\pic\4-6.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

完成了至今的每日选做，感觉编程能力到位了，算法能力还有待提升，开始看《算法基础与在线实践》



