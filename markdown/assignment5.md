# Assignment #5: Greedy穷举Implementation

Updated 1939 GMT+8 Oct 21, 2024

2024 fall, Complied by 李皓翔 物院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 04148: 生理周期

brute force, http://cs101.openjudge.cn/practice/04148

思路：



代码：

```python
def pm(x,y,ix,iy):
    j=0
    while True:
        if abs(y-x-ix*j)%iy==0:
            break
        j+=1
    return max(y,x+ix*j)

t=0
while True:
    t+=1
    p,e,i,d=map(int,input().split())
    if p+e+i+d==-4:
        break
    a=pm(p,e,23,28)
    ans=pm(a,i,644,33)
    print(f'Case {t}: the next triple peak occurs in {(ans-d+21251)%21252+1} days.')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](..\pic\5-1.png)



### 18211: 军备竞赛

greedy, two pointers, http://cs101.openjudge.cn/practice/18211

思路：



代码：

```python
p=int(input())
cost=list(map(int,input().split()))
cost.sort()
pa=0
pb=len(cost)-1
em=0
ans=[]
flag=True
while pa<=pb:
    if p>=cost[pa]:
        p-=cost[pa]
        pa+=1
        em+=1
        flag=True
    else:
        if em==0:
            break
        if flag:
            flag=False
            ans.append(em)
        em-=1
        p+=cost[pb]
        pb-=1
ans.append(em)
print(max(ans))
```



代码运行截图 ==（至少包含有"Accepted"）==

![](C:\Users\15143\Desktop\pic\5-2.png)



### 21554: 排队做实验

greedy, http://cs101.openjudge.cn/practice/21554

思路：



代码：

```python
n=int(input())
l=list(map(int,input().split()))
li=[]
for i in range(n):
    li.append([l[i],i+1])
li.sort()
s=0
w=n-1
for i in li:
    print(i[1],end=' ')
    s+=w*i[0]
    w-=1
print()
print(f'{s/n:.2f}')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](C:\Users\15143\Desktop\pic\5-1.png)



### 01008: Maya Calendar

implementation, http://cs101.openjudge.cn/practice/01008/

思路：



代码：

```python
n=int(input())
print(n)
for i in range(n):
    d,m,y=input().split()
    d=d[:-1]
    m1={'pop':0, 'no':1, 'zip':2, 'zotz':3, 'tzec':4, 'xul':5, 'yoxkin':6, 'mol':7, 'chen':8, 'yax':9, 'zac':10, 'ceh':11, 'mac':12, 'kankin':13, 'muan':14, 'pax':15, 'koyab':16, 'cumhu':17,'uayet':18}
    day=int(d)+m1[m]*20+int(y)*365
    yp=(day)//260
    day=day%260
    dp=day%13+1
    m2=['imix', 'ik', 'akbal', 'kan', 'chicchan', 'cimi', 'manik', 'lamat', 'muluk', 'ok', 'chuen', 'eb', 'ben', 'ix', 'mem', 'cib', 'caban','eznab', 'canac', 'ahau']
    mp=m2[day%20]
    print(dp,mp,yp)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](C:\Users\15143\Desktop\pic\5-4.png)



### 545C. Woodcutters

dp, greedy, 1500, https://codeforces.com/problemset/problem/545/C

思路：



代码：

```python
n=int(input())
w=[]
h=[]
for i in range(n):
    a,b=map(int,input().split())
    w.append(a)
    h.append(b)
ans=2
p=w[0]
for i in range(1,n-1):
    if w[i]-p>h[i]:
        ans+=1
        p=w[i]
    elif w[i+1]-w[i]>h[i]:
        ans+=1
        p=w[i]+h[i]
    else:
        p=w[i]
if n==1:
    ans=1
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](C:\Users\15143\Desktop\pic\5-5.png)



### 01328: Radar Installation

greedy, http://cs101.openjudge.cn/practice/01328/

思路：



代码：

```python
import math
o = []
while True:
    n, d = map(int,input().split())
    if n == 0 and d == 0:
        break
    else:
        l = []
        ans = 1
        for i in range(n):
            l.append(list(map(int,input().split())))
        input()
        l.sort(key = lambda x:(x[0],-x[1]))
        if l[0][1] > d:
            ans = -1
            o.append(ans)
            continue
        else:
            up_x = math.sqrt(d**2-l[0][1]**2) + l[0][0] + d
            i = 1
            while i < n:
                x, y = l[i][0], l[i][1]
                if y > d:
                    ans = -1
                    break
                else:
                    if x > up_x:
                        up_x = math.sqrt(d**2-y**2) + x + d
                        ans += 1
                    else:
                        up_y = math.sqrt(d**2-(x-up_x+d)**2)
                        if y > up_y and x > up_x -d:
                            up_x = math.sqrt(d**2-y**2) + x + d
                            ans += 1
                        if y > up_y and x < up_x -d:
                            up_x = math.sqrt(d**2-y**2) + x + d
                i += 1
        o.append(ans)
for i in range(len(o)):
    a = i+1
    print('Case ' + str(a) + ': ' + str(o[i]))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![](C:\Users\15143\Desktop\pic\5-6.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

完成了每日选做，最近比较忙，只能坚持跟进每日选做，没有拓展，期中后打算多抽些时间做洛谷和晴问



