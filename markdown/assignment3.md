# Assign #3: Oct Mock Exam暨选做题目满百

Updated 1537 GMT+8 Oct 10, 2024

2024 fall, Complied by 李皓翔 物院



**说明：**

1）Oct⽉考： AC5。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++/C（已经在Codeforces/Openjudge上AC），截图（包含Accepted, 学号），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、作业评论有md或者doc。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E28674:《黑神话：悟空》之加密

http://cs101.openjudge.cn/practice/28674/



思路：



代码

```python
k=int(input())
s=input()
l=[]
a='ABCDEFGHIJKLMNOPQRSTUVWXYZ'
b='abcdefghijklmnopqrstuvwxyz'
for i in s:
    if i in a:
   ![3-1](C:\Users\15143\Desktop\pic\3-1.png)     l.append(a[(ord(i)-ord('A')-k)%26])
    else:
        l.append(b[(ord(i)-ord('a') - k) % 26])
for i in l:
    print(i,end='')

```



代码运行截图 ==（至少包含有"Accepted"）==

![](..\pic\3-1.png)



### E28691: 字符串中的整数求和

http://cs101.openjudge.cn/practice/28691/



思路：



代码

```python
l=input().split()
ans=0
for i in l:
    ans+=int(i[0]+i[1])
print(ans)
```



代码运行截图 ==（至少包含有"Accepted"）==

![](..\pic\3-2.png)



### M28664: 验证身份证号

http://cs101.openjudge.cn/practice/28664/



思路：



代码

```python
for i in range(int(input())):
    n=input()
    l=[7,9,10,5,8,4,2,1,6,3,7,9,10,5,8,4,2]
    s=0
    for j in range(len(n)-1):
        s+=l[j]*int(n[j])
    s=s%11
    dic=[1,0,'X',9,8,7,6,5,4,3,2]
    s=dic[s]
    if str(s)==n[-1]:
        print("YES")
    else:
        print("NO")

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![](..\pic\3-3.png)



### M28678: 角谷猜想

http://cs101.openjudge.cn/practice/28678/



思路：



代码

```python
n=int(input())
while n!=1:
    if n%2==0:
        print(f'{n}/2={n//2}')
        n=n//2
    else:
        print(f'{n}*3+1={n*3+1}')
        n=n*3+1
print('End')
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![](..\pic\3-4.png)



### M28700: 罗马数字与整数的转换

http://cs101.openjudge.cn/practice/28700/



思路：



##### 代码

```python
a=input()
if ord('9') >= ord(a[0]) >= ord('0'):
    a=int(a)
    l=''
    while a>=1000:
        l+='M'
        a-=1000
    while a>=500:
        l+='D'
        a-=500
    while a>=100:
        l+='C'
        a-=100
    while a>=50:
        l+='L'
        a-=50
    while a>=10:
        l+='X'
        a-=10
    while a>=5:
        l+='V'
        a-=5
    while a>=1:
        l+='I'
        a-=1
    ans=''
    if len(l)>=4:
        i=0
        while i < len(l):
            if len(l)>i+4 and l[i]+l[i+1]+l[i+2]+l[i+3]+l[i+4] in ['VIIII','LXXXX','DCCCC']:
                dic = {'VIIII': 'IX', 'LXXXX': 'XC', 'DCCCC': 'CM'}
                ans+=dic[l[i]+l[i+1]+l[i+2]+l[i+3]+l[i+4]]
                i+=5
            elif len(l)>i+3 and l[i]+l[i+1]+l[i+2]+l[i+3] in ['IIII','XXXX','CCCC']:
                dic={'IIII':'IV','XXXX':'XL','CCCC':'CD'}
                ans+=dic[l[i]+l[i+1]+l[i+2]+l[i+3]]
                i+=4
            else:
                ans+=l[i]
                i+=1
    else:
        ans=l
    print(ans)
else:
    r=len(a)
    ans=0
    i=0
    while i <r:
        if i+1<r and a[i]+a[i+1]=='CM':
            ans+=900
            i+=2
        elif i+1<r and a[i]+a[i+1]=='CD':
            ans+=400
            i+=2
        elif i + 1 < r and a[i] + a[i + 1] == 'XC':
            ans += 90
            i += 2
        elif i + 1 < r and a[i] + a[i + 1] == 'XL':
            ans += 40
            i += 2
        elif i + 1 < r and a[i] + a[i + 1] == 'IX':
            ans += 9
            i += 2
        elif i + 1 < r and a[i] + a[i + 1] == 'IV':
            ans += 4
            i += 2
        else:
            dic={'I' :1 ,'V' :5 ,'X' :10 ,'L' :50, 'C': 100, 'D' :500, 'M': 1000}
            ans+=dic[a[i]]
            i+=1
    print(int(ans))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![](..\pic\3-5.png)





### *T25353: 排队 （选做）

http://cs101.openjudge.cn/practice/25353/



思路：



代码

```python

N,D=map(int,input().split())
l=[]
for i in range(N):
    l.append(int(input()))

ans=[]
while len(l)>0:
    up=l[0]
    down=l[0]
    p=[l[0]]
    new=[]
    for i in range(1,len(l)):
        if l[i]>=up-D and l[i]<=down+D:
            p.append(l[i])
        else:
            new.append(l[i])
        down=min(down,l[i])
        up=max(up,l[i])
    l=new
    p.sort()
    ans.append(p)

for i in ans:
    for j in i:
        print(j)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![](..\pic\3-6.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。==

完成了晴问算法的“算法初步”部分









