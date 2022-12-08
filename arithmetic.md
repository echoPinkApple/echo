### 704.

二分查找



```java
 class Solution {
        public int search(int[] nums, int target) {
            int left = 0;
            int right = nums.length - 1;
            int m;
            while (left <= right) {
                m = (left + right) >>> 1;
                if (nums[m] == target) {
                    return m;
                } else if (nums[m] > target) {
                    right = m - 1;
                } else {
                    left = m + 1;
                }
            }
            return -1;
        }
    }
```



### 278.

你是产品经理，目前正在带领一个团队开发新的产品。不幸的是，你的产品的最新版本没有通过质量检测。由于每个版本都是基于之前的版本开发的，所以错误的版本之后的所有版本都是错的。

假设你有 n 个版本 [1, 2, ..., n]，你想找出导致之后所有版本出错的第一个错误的版本。

你可以通过调用 bool isBadVersion(version) 接口来判断版本号 version 是否在单元测试中出错。实现一个函数来查找第一个错误的版本。你应该尽量减少对调用 API 的次数。

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/first-bad-version
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

利用二分查找，依次缩小左右边界

**关键在于左右边界的确定，left=mid+1，确保在端点处 left==right**

```java
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int l=0;
        int r=n;
        int m;
        while((r-l)>1){
            m=(l+r)>>>1;
            if(isBadVersion(m)){
                r=m;
            }
            else{
                l=m;
            }
        }
        return r;
    }
}


public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int left = 1, right = n;
        while (left < right) { // 循环直至区间左右端点相同
            int mid = left + (right - left) / 2; // 防止计算时溢出
            if (isBadVersion(mid)) {
                right = mid; // 答案在区间 [left, mid] 中
            } else {
                left = mid + 1; // 答案在区间 [mid+1, right] 中
            }
        }
        // 此时有 left == right，区间缩为一个点，即为答案
        return left;
    }
}
```

### 35.搜索插入位置

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

请必须使用时间复杂度为 O(log n) 的算法。

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/search-insert-position
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

数组升序排列，left左边的值总是小于待插入的值

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int l=0;
        int r=nums.length-1;
        int mid=0;
        while(l<=r){
            mid=(l+r)>>>1;
            if(nums[mid]==target){
                return mid;
            }
            else if(nums[mid]> target){
                r=mid-1;
            }
            else{
                l=mid+1;
            }
        }
        return l;
    }
}
```

### 链表问题解法：

合并有序链表：双指针，比较大小后移；

分割链表：生成2个链表，一个存储大于给定值的，一个存储小于给定值的。

**合并k个有序链表：优先级队列；**

单链表的倒数第k个节点：一个指针先走k个节点，再一个指针p2指向head，开始同步走n-k个节点，此时p2走过n-k个节点，也就是倒数第k个节点；

单链表中点：p1走一步，p2走2步，p2指向链表尾部时候，p1指向中点；

链表成环：p1走一步，p2走2步，如果会相遇，说明成环；

链表相交：a、b首尾相连  a-->b;b-->a遍历，a，b相交节点后链表长度一致。



链表反转：

```java
//递归实现
class Solution{
	public ListNode reverse(ListNode head){
        if(head==null || head.next==null){
            return head;
        } 
        ListNode last=reverse(head.next);
        head.next.next=head;
        head.next=null;
        return last;
    }
}
```

反转链表前n个元素

```java
class Solution{
    ListNode p=null;
    public ListNode reverseN(ListNode head,int n){
        if(n==1){
            p=head.next;
            return head;
        }
        ListNode last=reverseN(head.next,n-1);
        head.next.next=head;
        head.next=p;
        return last;
    }
}
```

反转链表[m,n]之间的元素

```java
	class Solution{
        public ListNode reverseBetween(ListNode head,int m, int n){
            if(m==1){
                return reverseN(head,n);
            }
            head.next=reverseBetween(head.next,m-1,n-1);
            return head;
        }
    }
```

k个一组反转链表

```java
class Solution{
	public ListNode reverse(ListNode a,ListNode b){
        //三个指针分别记录前驱节点，当前节点，后置节点
        ListNode pre,cur,next;
        pre=null;
        next=cur=head;
        while(cur!=b){
            next=cur.next;
            cur.next=pre;
            pre=cur;
            cur=next;
        }
        //最后一次循环导致cur=b.next;所以需要返回pre
        return pre;
    }
    public ListNode reverseByGroup(ListNode head,int k){
        if(head==null || head.next==null){
            return head;
        }
        ListNode a,b;
        a=b=head;
        for(int i=0;i<k;i++){
            if(b.next==null){
                //长度不足k则不反转
                return head;
            }
            b=b.next;
        }
        //反转小区间内的链表，获取反转后的链表头
        ListNode newHead=reverse(a,b);
        a.next=reverseByGroup(b,k);
        return newhead;
    }
}
```



寻找回文串

```java
class Solution{
    publlic String palindrome(String s,int left,int right){
        while(left>0 && right<s.length && s.chartAt(left)==s.chartAt(right)){
            left++;
            right--;
        }
        return s.subString(left+1,right);
    }
}
```

判断字符串是否是回文串

```java
class Solution{
    public boolean isPalindrome(String s){
        int left=0;
        int right=s.length-1;
        while(left<right){
            if(s.charAt(left)==s.charAt(right)){
                left++;
                right--;
            }
            else{
                return false;
            }
        }
        return true;
    }
}
```



判断回文链表

```java
//递归实现
class Solution{
    ListNode left;
    public boolean isPalindromeList(ListNode head){
        left=head;
        return travarse(head);
    }
    public boolean travarse(ListNode right){
        if(right==null)
            return true;
        boolean res=travarse(right.next);
        res=res&&(right.val==left.val);
        left=left.next;
        return res;
    }
}

//双指针实现
class Solution{
    public boolean isPalindromeList(ListNode head){
        ListNode left,right;
        while(right!=null || right.next!=null){
            left=left.next;
            right=rigt.next.next;
        }
        if(right!=null){
            left=left.next;
        }
        ListNode newLeft=head;
        ListNode newRight=reverse(left);
        while(newRight!=null){
            if(newLeft.var!=newRight.var){
                return false;
            }
        }
        return true;
        
    }
    public ListNode reverse(ListNode node){
        ListNode pre,cur,next;
        pre=null;
        cur=next=node;
        while(node!=null){
            next=node.next;
            node.next=pre;
            pre=cur;
            cur=next;
        }
    }
}
```



### 数组问题解法：

#### 快慢指针：

**去除重复元素**

```java
//快慢指针，由于是有序数组，两个指针指向的值不相等则慢指针前进一步，存储遇到的不重复值。
class Solution{
    public int removeDuplicate(int[] nums){
        if(nums==null){
            return 0;
        }
        int slow=0;
        int fast=0;
        while(fast!=(nums.length-1)){
            if(nums[slow]!=nums[fast]){
                nums[++slow]=nums[fast];
            }
            fast++;
        }
        return slow+1;
    }
}
```



**去除链表重复元素**

```java
//快慢指针遍历链表，值不同则慢指针指向快指针
class Solution{
    public ListNode removeDuplicate(ListNode head){
        if(head==null){
            return null;
        }
        ListNode slow;
        ListNode fast;
        slow=fast=head;
        while(fast!=null){
            if(slow.val==fast.val){
                slow.next=fast;
                slow=slow.next;
            }
            fast=fast.next;
        }
        //断开慢指针和原链表
        slow.next=null;
        return head;
    }
}
```



**移除元素**

```java
//将不重复的元素赋值给数组
class Solution{
    int removeElement(int[] nums,int target){
        int slow=0;
        int fast=0;
        while(fast!=nums.length-1){
            if(nums[fast]!=target){
                nums[slow++]=nums[fast];
            }
            fast++;
        }
        return fast+1;
    }
}
```

**移除**0

```java
//将非0元素赋值给数组。
class Solution{
    void removeZores(int[] nums){
        int slow=0;
        int fast=0;
        while(fast!=(nums.length-1)){
            if(nums[fast]!=0){
                nums[slow++]=nums[fast];
            }
            fast++;
        }
        while(slow!=(nums.length-1)){
            nums[slow++]=0;
        }
    }
}
```

#### 左右指针

**二分查找**

```java
class Solution{
    public int binarySearch(int[] nums,int target){
        int left=0;
        int right=nums.length-1;
        int mid=0;
        while(right>=left){
            mid=(nums[left]+nums[right])>>>1;
            if(target==nums[mid]){
                return mid;
            }
            else if(target<nums[mid]){
                right=mid-1;
            }
            else{
                left=mid+1;
            }
        }
        return -1;
    }
}
```

**两数之和**

```java
class Solution{
    public int[] sum(int[] nums,int target){
        int left=0;
        int right=nums.length-1;
        int temp=0;
        while(left<right){
            temp=nums[left]+nums[right];
            if(temp==target){
                return new int[]{left+1,right+1};
            }
            else if(temp>target){
                right--;
            }
            else{
                left++;
            }
        }
    }
}
```

**反转字符串**

```java
class Solution{
	public void reverseString(char[] s){
        int left=0;
        int right=s.length-1;
        while(left<right){
            char temp=s[left];
            s[left]=s[right];
            s[right]=temp;
            left++;
            right--;
        }
    }
}
```





**判断回文串**



```java
boolean isPalindrome(String s){
    // 一左一右两个指针相向而行
    int left = 0, right = s.length() - 1;
    while (left < right) {
        if (s.charAt(left) != s.charAt(right)) {
            return false;
        }
        left++;
        right--;
    }
    return true;
}
```



**寻找最长回文串**

```java
String longestPalindrome(String s) {
    String ret = "";
    for (int i = 0; i < s.length(); i++) {
        String temp1 = palindrome(s, i, i);
        String temp2 = palindrome(s, i, j + 1);
        ret = ret.length() > temp1.length() ? ret : temp1;
        ret = ret.length() > temp2.length() ? ret : temp2;
    }
    return ret;
}

String palindrome(String s, int l, int r) {
    while (l > 0 && r < s.length() && s.charAt(l) == s.charAt(r)) {
        l--;
        r++;
    }
    return s.substring(l + 1, r);
}
```



#### 一维数组前缀和[303. 区域和检索 - 数组不可变](https://leetcode.cn/problems/range-sum-query-immutable/)

```java
//计算前n个元素和，存储到index=n的位置,求[1,4]区间的和，用preSum[5]-preSum[1]
class NumArray {
    // 前缀和数组
    private int[] preSum;

    /* 输入一个数组，构造前缀和 */
    public NumArray(int[] nums) {
        // preSum[0] = 0，便于计算累加和
        preSum = new int[nums.length + 1];
        // 计算 nums 的累加和
        for (int i = 1; i < preSum.length; i++) {
            preSum[i] = preSum[i - 1] + nums[i - 1];
        }
    }
    
    /* 查询闭区间 [left, right] 的累加和 */
    public int sumRange(int left, int right) {
        return preSum[right + 1] - preSum[left];
    }
}

```



#### **二维数组前缀和**[304. 二维区域和检索 - 矩阵不可变](https://leetcode.cn/problems/range-sum-query-2d-immutable/)

```java
class NumMatrix {
    private int[][] preSum;

    public NumMatrix(int[][] nums) {
        int m = nums.length;
        int n = nums[0].length;
        if (n == 0) {
            return;
        }
        preSum = new int[m + 1][n + 1];
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                preSum[i][j] = preSum[i - 1][j] + preSum[i][j - 1] - preSum[i - 1][j - 1] + nums[i][j];
            }
        }
    }

    public int sumRegion(int x1, int y1, int x2, int y2) {
        return preSum[x2 + 1][y2 + 1] - preSum[x1][y2 + 1] - preSum[x2 + 1][y1] - preSum[x1][y1];
    }
}
```

#### 差分数组

```java
class Difference {
    private int[] diff;

    public Difference(int[] nums) {
        this.diff = new int[nums.length];
        this.diff[0] = nums[0];
        for (int i = 1; i < nums.length; i++) {
            diff[i] = nums[i] - nums[i - 1];
        }
    }

    public void increment(int l, int r, int val) {
        diff[l] += val;
        if (r + 1 < diff.length) {
            diff[r + 1] -= val;
        }
    }

    public int[] result() {
        int[] ret = new int[diff.length];
        ret[0] = diff[0];
        for (int i = 1; i < ret.length; i++) {
            ret[i] = ret[i - 1] + diff[i];
        }
        return ret;
    }
}
```

370.**区间加法**

```java
//利用差分数组
int[] getModifiedArray(int length,int[][] updates){
  int[] arr=new int[length];
  Difference diff=new Difference(arr);
  for(int[] temp: updates){
    int l=temp[0];
    int r=temp[1];
    int val=temp[2];
    diff.increment(l,r,val);
  }
  return dirr.result;
}
```

1109.**航班预订统计**

```java
int[] corpFlightBookings(int[][] bookings, int n){
  int[] arr=new int[n];
  Difference diff=new Difference(arr);
  for(int[] temp : bookings){
    diff.increment(temp[0]-1,temp[1]-1,temp[2]);
  }
  return diff.result();
}
```

1094.拼车

```java
boolean carPooling(int[][] trips, int capacity){
  int[] arr=new int[1001];
  Difference diff=new Difference(arr);
  for(int[] trip : trips){
    diff.increment(trip[1],trip[2],trip[0]);
  }
  int[] result= diff.result();
  for(int i=0;i<arr.length;i++){
    if(result[i]>capacity){
      return false;
    }
  }
  return true;
}
```



#### 数组遍历

**旋转数组**

```java

/**
 * 顺时针旋转数组90度
 */
class Solution {
    public void rotate(int[][] matrix) {
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }
        for (int[] row : matrix) {
            reverse(row);
        }
    }

    public void reverse(int[] row) {
        int l = 0;
        int r = row.length;
        while (l < r) {
            int temp = row[l];
            row[l] = row[r];
            row[r] = temp;
        }
    }

}
//逆时针旋转90度
// 将二维矩阵原地逆时针旋转 90 度
void rotate2(int[][] matrix) {
    int n = matrix.length;
    // 沿左下到右上的对角线镜像对称二维矩阵
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n - i; j++) {
            // swap(matrix[i][j], matrix[n-j-1][n-i-1])
            int temp = matrix[i][j];
            matrix[i][j] = matrix[n - j - 1][n - i - 1];
            matrix[n - j - 1][n - i - 1] = temp;
        }
    }
    // 然后反转二维矩阵的每一行
    for (int[] row : matrix) {
        reverse(row);
    }
}

```

**顺时针遍历数组**

```JAVA
public static List<Integer> spiralOrder(int[][] matrix) {
        int leftBound = 0;
        int upperBound = 0;
        int m = matrix.length;
        int n = matrix[0].length;
        int rightBound = m;
        int lowerBound = n;
        List<Integer> list = new LinkedList<>();
        while (list.size() < m * n) {
            //先从左到右遍历，在上边界小于下边界的情况
            if (upperBound <= lowerBound) {
                for (int i = leftBound; i < rightBound; i++) {
                    list.add(matrix[upperBound][i]);
                    i++;
                }
                upperBound++;
            }
			//从右上到左下遍历
            if (leftBound <= rightBound) {
                for (int i = upperBound; i < lowerBound; i++) {
                    list.add(matrix[i][rightBound - 1]);
                    i++;
                }
                rightBound--;
            }
            if (upperBound <= lowerBound) {
                for (int i = rightBound; i >= 0; i++) {
                    list.add(matrix[lowerBound - 1][i]);
                    i--;
                }
                lowerBound--;
            }
            if (leftBound <= rightBound) {
                for (int i = lowerBound; i >= 0; i++) {
                    list.add(matrix[i][leftBound]);
                    i--;
                }
                leftBound++;
            }
        }
        return list;
    }
```



#### [59. 螺旋矩阵 II](https://leetcode.cn/problems/spiral-matrix-ii/)****

```java
int[][] generateMatrix(int n) {
    int[][] matrix = new int[n][n];
    int upper_bound = 0, lower_bound = n - 1;
    int left_bound = 0, right_bound = n - 1;
    // 需要填入矩阵的数字
    int num = 1;
    
    while (num <= n * n) {
        if (upper_bound <= lower_bound) {
            // 在顶部从左向右遍历
            for (int j = left_bound; j <= right_bound; j++) {
                matrix[upper_bound][j] = num++;
            }
            // 上边界下移
            upper_bound++;
        }
        
        if (left_bound <= right_bound) {
            // 在右侧从上向下遍历
            for (int i = upper_bound; i <= lower_bound; i++) {
                matrix[i][right_bound] = num++;
            }
            // 右边界左移
            right_bound--;
        }
        
        if (upper_bound <= lower_bound) {
            // 在底部从右向左遍历
            for (int j = right_bound; j >= left_bound; j--) {
                matrix[lower_bound][j] = num++;
            }
            // 下边界上移
            lower_bound--;
        }
        
        if (left_bound <= right_bound) {
            // 在左侧从下向上遍历
            for (int i = lower_bound; i >= upper_bound; i--) {
                matrix[i][left_bound] = num++;
            }
            // 左边界右移
            left_bound++;
        }
    }
    return matrix;
}

```





### [977. 有序数组的平方](https://leetcode.cn/problems/squares-of-a-sorted-array/)

双指针 方法一：找到正数和负数的分界点，从分界点向两边遍历；方法二：从两个边界向分界点遍历。

```java
class Solution {
    public int[] sortedSquares(int[] nums) {
         if (nums.length < 1) {
            return null;
        }
        int left = 0;
        int right = nums.length - 1;
        int p = nums.length - 1;
        int[] result = new int[nums.length];
        while (p >= 0) {
            int r1 = nums[left] * nums[left];
            int r2 = nums[right] * nums[right];//比较两个指针指向的数的平方大小
            if (r1 > r2) {
                result[p] = r1;//将较大的数先放入数组最大位置
                left++;
            } else {
                result[p] = r2;
                right--;
            }
            p--;
        }
        return result;
    }
}
```

### [189. 轮转数组](https://leetcode.cn/problems/rotate-array/)

方法一：使用额外数组，通过(n+k)%length确定位置；

**方法二：环状替换**

方法三：数组翻转：先翻转整个数组，再翻转[0,k-1],[k,length-1]就得到结果。

```java
class Solution {
    public void rotate(int[] nums, int k) {
        k = k % nums.length;
        reverse(nums, 0, nums.length-1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, nums.length - 1);
    }
    public void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
}
```

### [283. 移动零](https://leetcode.cn/problems/move-zeroes/)

```java
//双指针，先将非0元素赋值到数组开头，再将之后元素赋值为0
class Solution{
    public void moveZeros(int[] nums){
        int slow=0;
        int fast=0;
        while(fast!=nums.length-1){
            if(nums[fast]!=0){
                nums[slow++]=nums[fast];
            }
            fast++;
        }
        while(slow!=nums.length+1){
            nums[slow++]=0;
        }
    }
}
```

### [167. 两数之和 II - 输入有序数组](https://leetcode.cn/problems/two-sum-ii-input-array-is-sorted/)

```java
//双指针，如果sum>target则，右指针左移，如果sum<target则左指针右移
class Solution{
    public int[] twoSum(int[] numbers,int target){
        int left=0;
        int right=numbers.length-1;
        int sum=0;
        while(left<right){
            sum=numbers[left]+numbers[right];
            if(sum==target){
                return new int[]{left+1,right+1};
            }
            else if(sum<target){
                left++;
            }
            else{
                right--;
            }
        }
    }
}
```

### [557. 反转字符串中的单词 III](https://leetcode.cn/problems/reverse-words-in-a-string-iii/)

```java
class Solution {
    public String reverseWords(String s) {
        StringBuilder buffer=new StringBuilder();
        int length=s.length();
        int fast=0;
        int slow=0;
        while (fast<length){
            slow=fast;
            while (fast<s.length() && s.charAt(fast)!=' '){
                fast++;
            }
            for (int i=slow;i<fast;i++){
                //倒数第i+slow个元素=fast+slow-i-1
                buffer.append(s.charAt(fast-i+slow-1));
            }
            //字符串末尾不添加空格
            if (fast<s.length()){
                buffer.append(' ');
                fast++;
            }
        }
        return buffer.toString();
    }
}
```

### [344. 反转字符串](https://leetcode.cn/problems/reverse-string/)

```java
//左右指针
class Solution {
    public void reverseString(char[] s) {
        int left=0;
        int right=s.length-1;
        while(left<right){
            char temp=s[left];
            s[left]=s[right];
            s[right]=temp;
            left++;
            right--;
        }
    }
}
```

