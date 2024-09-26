# Assignment #2: 语法练习

Updated 0126 GMT+8 Sep 24, 2024

2024 fall, Complied by 李皓翔 物院



## 1. 题目

### 263A. Beautiful Matrix

https://codeforces.com/problemset/problem/263/A



思路：



##### 代码

```python
for i in range(5):
    l=input()
    for j in range(9):
        if l[j]=='1':
            a=abs((j//2+1)-3)+abs(i-2)
print(a)

```



代码运行截图 ==（至少包含有"Accepted"）==![](..\pic\2-1.png)





### 1328A. Divisibility Problem

https://codeforces.com/problemset/problem/1328/A



思路：



##### 代码

```python
s=[]
for i in range(int(input())):
    a,b=map(int,input().split())
    s.append((b-a%b)%b)
for i in s:
    print(i)

```



代码运行截图 ==（至少包含有"Accepted"）==

![](..\pic\2-2.png)



### 427A. Police Recruits

https://codeforces.com/problemset/problem/427/A



思路：



##### 代码

```python
input()
n=0
a=0
l=input().split()
for i in l:
    m=int(i)
    if a==0 and m==-1:
        n+=1
    else:
        a+=m
print(n)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![](..\pic\2-3.png)



### 02808: 校门外的树

http://cs101.openjudge.cn/practice/02808/



思路：



##### 代码

```python
L,M=map(int,input().split())
st=[]
en=[]
for i in range(M):
    l,r=map(int,input().split())
    st.append(l)
    en.append(r)
st.sort()
en.sort()
i=0
j=1
ans=0
while j<=len(st):
    if j==len(st):
        ans+=en[j-1]-st[i]+1
        break
    while  en[j-1]>=st[j]:
        j+=1
        if j==len(st):
            break
    ans+=en[j-1]-st[i]+1
    i=j
    j+=1
print(L+1-ans)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![](..\pic\2-4.png)



### sy60: 水仙花数II

https://sunnywhy.com/sfbj/3/1/60



思路：



##### 代码

```python
a,b=map(int,input().split())
l=[]
for i in range(a,b+1):
    if (i//100)**3+(i%100//10)**3+(i%10)**3==i:
        l.append(i)
if len(l)>0:
    print(l[0],end='')
    for i in range(1,len(l)):
       print(' '+str(l[i]),end='')
else:
    print('NO')

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![](..\pic\2-5.png)



### 01922: Ride to School

http://cs101.openjudge.cn/practice/01922/



思路：

一开始brute 1000多ms，想到简单方法，答案一定是t=0后出发最早到达的，减到34ms。

拿到题还是该多想一下再写...

##### 代码

```python
import math as m
while True:
    N=int(input())
    if N==0:
        break
    else:
        v=[]
        t=[]
        for i in range(N):
            v1,t1=map(int,input().split())
            if t1>=0:
                v.append(v1)
                t.append(t1)
        a=[]
        for i in range(len(v)):
            a.append(16200/v[i]+t[i])
        print(m.ceil(min(a)))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![](..\pic\2-6.png)



## 2. 学习总结和收获

额外练习，9/25号前选做题





