# Assignment #4: 位操作、栈、链表、堆和NN

Updated 1203 GMT+8 Mar 10, 2025

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

### 136.只出现一次的数字

bit manipulation, https://leetcode.cn/problems/single-number/



<mark>请用位操作来实现，并且只使用常量额外空间。</mark>



代码：

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        ans=0
        for it in nums:
            ans^=it 
        return ans
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250311095001321](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250311095001321.png)



### 20140:今日化学论文

stack, http://cs101.openjudge.cn/practice/20140/



思路：



代码：

```python
def f(x):
    ans=[]
    i=0
    while i<len(x):
        if x[i]=='[':
            k=i
            i+=1
            while '0'<=x[i]<='9':
                i+=1
            a=1
            j=i
            while a!=0:
                if x[i]=='[':
                    a+=1
                elif x[i]==']':
                    a-=1
                i+=1
            i-=1
            for _ in range(int(''.join(x[k+1:j]))):
                ans=ans+f(x[j:i])
            
        else:
            ans.append(x[i])
        i+=1
    return ans
        
l=list(input())
print(''.join(f(l)))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250317164337131](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250317164337131.png)



### 160.相交链表

linked list, https://leetcode.cn/problems/intersection-of-two-linked-lists/



思路：



代码：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        A=headA
        B=headB
        while A!=B:
            if A:
                A=A.next
            else:
                A=headB
            if B:
                B=B.next
            else:
                B=headA
        return A
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250317160252937](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250317160252937.png)



### 206.反转链表

linked list, https://leetcode.cn/problems/reverse-linked-list/



思路：



代码：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        cur,pre=head,None
        while cur:
            tem=cur.next
            cur.next=pre
            pre=cur
            cur=tem
        return pre
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250317160326887](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250317160326887.png)



### 3478.选出和最大的K个元素

heap, https://leetcode.cn/problems/choose-k-elements-with-maximum-sum/



思路：



代码：

```python
from heapq import *
class Solution:
    def findMaxSum(self, nums1: List[int], nums2: List[int], k: int) -> List[int]:
        n=len(nums1)
        h1=[]
        for i in range(n):
            heappush(h1,(nums1[i],i))
        h2=[]
        ans=[0 for i in range(n)]
        vd=-1
        vans=0
        s=0
        for _ in range(n):
            c,i=heappop(h1)
            heappush(h2,nums2[i])
            if c==vd:
                ans[i]=vans
            else:
                ans[i]=s
            vd=c
            vans=ans[i]
            s+=nums2[i]
            if len(h2)==k+1:
                s-=heappop(h2)
        return ans
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20250318115840445](C:\Users\15143\AppData\Roaming\Typora\typora-user-images\image-20250318115840445.png)

### Q6.交互可视化neural network

https://developers.google.com/machine-learning/crash-course/neural-networks/interactive-exercises

**Your task:** configure a neural network that can separate the orange dots from the blue dots in the diagram, achieving a loss of less than 0.2 on both the training and test data.

**Instructions:**

In the interactive widget:

1. Modify the neural network hyperparameters by experimenting with some of the following config settings:
   - Add or remove hidden layers by clicking the **+** and **-** buttons to the left of the **HIDDEN LAYERS** heading in the network diagram.
   - Add or remove neurons from a hidden layer by clicking the **+** and **-** buttons above a hidden-layer column.
   - Change the learning rate by choosing a new value from the **Learning rate** drop-down above the diagram.
   - Change the activation function by choosing a new value from the **Activation** drop-down above the diagram.
2. Click the Play button above the diagram to train the neural network model using the specified parameters.
3. Observe the visualization of the model fitting the data as training progresses, as well as the **Test loss** and **Training loss** values in the **Output** section.
4. If the model does not achieve loss below 0.2 on the test and training data, click reset, and repeat steps 1–3 with a different set of configuration settings. Repeat this process until you achieve the preferred results.

给出满足约束条件的<mark>截图</mark>，并说明学习到的概念和原理。





## 2. 学习总结和收获

<mark>如果发现作业题目相对简单，有否寻找额外的练习题目，如“数算2025spring每日选做”、LeetCode、Codeforces、洛谷等网站上的题目。</mark>

在补寒假偷懒没做的选做，还是对理解有很大帮助的









