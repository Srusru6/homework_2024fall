# Assignment #5: 链表、栈、队列和归并排序

Updated 1348 GMT+8 Mar 17, 2025

2025 spring, Complied by 物院 李皓翔



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

### LC21.合并两个有序链表

linked list, https://leetcode.cn/problems/merge-two-sorted-lists/

思路：



代码：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        c=ListNode(0)
        ans=c
        while list1 and list2:
            if list1.val < list2.val:
                c.next=list1
                list1=list1.next
            else:
                c.next=list2
                list2=list2.next
            c=c.next
        if list1:
            c.next=list1
        else:
            c.next=list2
        return ans.next
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250321095038070](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250321095038070.png)



### LC234.回文链表

linked list, https://leetcode.cn/problems/palindrome-linked-list/

<mark>请用快慢指针实现。</mark>



代码：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def isPalindrome(self, head: Optional[ListNode]) -> bool:
        fc=sc=head
        while fc and fc.next:
            fc=fc.next.next
            sc=sc.next
        pre=None
        while sc:
            cur=sc
            sc=sc.next
            cur.next=pre
            pre=cur
        fc=head
        lc=cur
        while lc:
            if fc.val!=lc.val:
                return False
            fc=fc.next
            lc=lc.next
        return True
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250321101342821](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250321101342821.png)



### LC1472.设计浏览器历史记录

doubly-lined list, https://leetcode.cn/problems/design-browser-history/

<mark>请用双向链表实现。</mark>



代码：

```python
class BrowserHistory:
    def __init__(self, homepage: str):
        self.val=homepage
        self.next=None
        self.last=None
        self.current=self
        
    def visit(self, url: str) -> None:
        pre=self.current
        self.current.next=BrowserHistory(url)
        self.current=self.current.next
        self.current.last=pre

    def back(self, steps: int) -> str:
        for i in range(steps):
            if self.current.last==None:
                break
            self.current=self.current.last
        return self.current.val

    def forward(self, steps: int) -> str:
        for i in range(steps):
            if self.current.next==None:
                break
            self.current=self.current.next
        return self.current.val

# Your BrowserHistory object will be instantiated and called as such:
# obj = BrowserHistory(homepage)
# obj.visit(url)
# param_2 = obj.back(steps)
# param_3 = obj.forward(steps)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250321142132544](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250321142132544.png)



### 24591: 中序表达式转后序表达式

stack, http://cs101.openjudge.cn/practice/24591/

思路：



代码：

```python
for _ in range(int(input())):
    l=input()
    ans=[]
    s=[]
    i=-1
    pro={'*':2,'/':2,'+':1,'-':1,'(':0}
    while i<len(l)-1:
        i+=1
        it=l[i]
        if it==' ':
            continue
        if ord('0')<=ord(it)<=ord('9'):
            p=i
            while i<len(l) and (ord('0')<=ord(l[i])<=ord('9') or l[i]=='.'):
                i+=1
            ans.append(l[p:i])
            i-=1
            continue
        if it=='(':
            s.append(it)
            continue
        if it==')':
            while s[-1]!='(':
                ans.append(s.pop())
            s.pop()
            continue
        while s and s[-1]!='(' and pro[s[-1]]>=pro[it]:
            ans.append(s.pop())
        s.append(it)
    while s:
        ans.append(s.pop())
    print(' '.join(ans))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250324093854278](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250324093854278.png)



### 03253: 约瑟夫问题No.2

queue, http://cs101.openjudge.cn/practice/03253/

<mark>请用队列实现。</mark>



代码：

```python
while True:
    n,p,m=map(int,input().split())
    if n==0:
        break
    queue=[(i-1)%n+1 for i in range(p,n+p+1)]
    ind=0
    i=0
    ls=n
    ans=[]
    while i!=ls:
        ind+=1
        if ind==m:
            ind=0
            ans.append(queue[i])
        else:
            queue[ls]=queue[i]
            ls=(ls+1)%(n+1)
        i=(i+1)%(n+1)
    print(','.join(list(map(str,ans))))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250321103036633](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250321103036633.png)



### 20018: 蚂蚁王国的越野跑

merge sort, http://cs101.openjudge.cn/practice/20018/

思路：



代码：

```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr,0
    mid = len(arr) // 2
    left_half,t1 = merge_sort(arr[:mid]) 
    right_half,t2 = merge_sort(arr[mid:])
    ans,t=merge(left_half, right_half)
    return ans,t+t1+t2

def merge(left, right):
    sorted_arr = []
    n=len(left)
    i = j = 0
    t=0
    while i < len(left) and j < len(right):
        if left[i] >= right[j]:
            sorted_arr.append(left[i])
            i += 1
        else:
            sorted_arr.append(right[j])
            j += 1
            t+=(n-i)
    sorted_arr.extend(left[i:])
    sorted_arr.extend(right[j:])
    return sorted_arr,t

n=int(input())
l=[int(input()) for i in range(n)]
_,ans=merge_sort(l)
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250324173715673](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250324173715673.png)



## 2. 学习总结和收获

跟进每日选做，感觉群里同学的解法都很值得学习









