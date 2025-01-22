# Assignment #7: Nov Mock Exam立冬

Updated 1646 GMT+8 Nov 7, 2024

2024 fall, Complied by 李皓翔 物院



**说明：**

1）⽉考： AC6。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E07618: 病人排队

sorttings, http://cs101.openjudge.cn/practice/07618/

思路：



代码：

```python
n=int(input())
list=[]
for i in range(n):
    a,b=input().split()
    b=int(b)
    list.append([b,a])
old=[]
ans=[]
for i in range(len(list)):
    if list[i][0]>=60:
        old.append(list[i])
    else:
        ans.append(list[i][1])
an=[]
for i in range(len(old)):
    m=0
    for j in range(1,len(old)):
        if old[j][0]>old[m][0]:
            m=j
    an.append(old[m][1])
    old[m][0]=0
for i in an+ans:
    print(i)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![7-1](..\pic\7-1.png)



### E23555: 节省存储的矩阵乘法

implementation, matrices, http://cs101.openjudge.cn/practice/23555/

思路：



代码：

```python
n,m1,m2=map(int,input().split())
a=[[0 for i in range(n)]for j in range(n)]
b=[[0 for i in range(n)]for j in range(n)]
c=[[0 for i in range(n)]for j in range(n)]
for i in range(m1):
    x,y,l=map(int,input().split())
    a[x][y]=l
for i in range(m2):
    x,y,l=map(int,input().split())
    b[x][y]=l
for x in range(n):
    for y in range(n):
        sum=0
        for i in range(n):
            sum+=a[x][i]*b[i][y]
        c[x][y]=sum
for x in range(n):
    for y in range(n):
        if c[x][y]!=0:
            print(x,y,c[x][y])
```



代码运行截图 ==（至少包含有"Accepted"）==

![7-1](..\pic\7-2.png)



### M18182: 打怪兽 

implementation/sortings/data structures, http://cs101.openjudge.cn/practice/18182/

思路：



代码：

```python
for _ in range(int(input())):
    n, m, b = map(int, input().split())
    ak = {}
    for i in range(n):
        t, x=map(int,input().split())
        if t not in ak:
            ak[t]=[x]
        else:
            ak[t].append(x)
    k=list(ak.keys())
    k.sort()
    f=True
    for i in k:
        ak[i].sort(reverse=True)
        for j in range(min(m,len(ak[i]))):
            b-=ak[i][j]
        if b<=0:
            print(i)
            f=False
            break
    if f:
        print('alive')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![7-1](..\pic\7-3.png)



### M28780: 零钱兑换3

dp, http://cs101.openjudge.cn/practice/28780/

思路：



代码：

```python
n,m=map(int,input().split())
l=list(map(int,input().split()))
l.sort(reverse=True)
dp=[0 for i in range(m+1)]
for it in l:
    for j in range(it,m+1):
        if dp[j-it]!=0 or j==it:
            if dp[j]==0:
                dp[j]=dp[j-it]+1
            else:
                dp[j]=min(dp[j],dp[j-it]+1)
if dp[-1]==0:
    print(-1)
else:
    print(dp[-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![7-1](..\pic\7-4.png)



### T12757: 阿尔法星人翻译官

implementation, http://cs101.openjudge.cn/practice/12757

思路：



代码：

```python
l=input().split()
ans=0
a=0
if l[0]=='negative':
    n=-1
    i=1
else:
    i=0
    n=1
w=['hundred', 'thousand', 'million']

def ind(word):
    for i in range(3):
        if w[i]==word:
            break
    return i

dic={ 'zero':0, 'one':1, 'two':2, 'three':3, 'four':4, 'five':5, 'six':6, 'seven':7, 'eight':8, 'nine':9, 'ten':10, 'eleven':11, 'twelve':12, 'thirteen':13, 'fourteen':14, 'fifteen':15, 'sixteen':16, 'seventeen':17, 'eighteen':18, 'nineteen':19, 'twenty':20, 'thirty':30, 'forty':40, 'fifty':50, 'sixty':60, 'seventy':70, 'eighty':80, 'ninety':90, 'hundred':100, 'thousand':1000, 'million':1000000 }
up=3
while i<len(l):
    if i<len(l)-1 and l[i] not in w and l[i+1] in w:
        if ind(l[i+1])>=up:
            ans+=dic[l[i]]
            ans*=dic[l[i+1]]
            a+=ans
            ans=0
            up=3
        else:
            ans+=dic[l[i]]*dic[l[i+1]]
            up=ind(l[i+1])
        i+=2
    elif l[i] in w:
        ans *= dic[l[i]]
        a+=ans
        ans=0
        up = 3
        i+=1
    else:
        ans+=dic[l[i]]
        i+=1

print((a+ans)*n)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![7-1](..\pic\7-5.png)



### T16528: 充实的寒假生活

greedy/dp, cs10117 Final Exam, http://cs101.openjudge.cn/practice/16528/

思路：



代码：

```python
n=int(input())
l=[]
for i in range(n):
    l.append(list(map(int,input().split())))
dp=[0 for i in range(62)]
l.sort()
for i in l:
    a,b=i[0],i[1]
    if a>0:
        dp[b]=max(max(dp[0:a])+1,dp[b])
    else:
        dp[b]=max(1,dp[b])
print(max(dp))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![7-1](..\pic\7-6.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

一个半小时AK，感觉思路都可以很快想到，但转换成代码还是有些卡，感觉进一步提升可以从补每日选做开始（感觉复习高数落了好多QwQ），发现吃饭的时候刷刷同学在群里问的问题很有帮助，可以有效避坑一些常见错误。



