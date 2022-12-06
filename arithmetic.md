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

链表问题解法：

合并有序链表：双指针，比较大小后移；

分割链表：生成2个链表，一个存储大于给定值的，一个存储小于给定值的。

合并k个有序链表：优先级队列；

单链表的倒数第k个节点：一个指针先走k个节点，再一个指针p2指向head，开始同步走n-k个节点，此时p2走过n-k个节点，也就是倒数第k个节点；

单链表中点：p1走一步，p2走2步，p2指向链表尾部时候，p1指向中点；

链表成环：p1走一步，p2走2步，如果会相遇，说明成环；

链表相交：a-->b;b-->a遍历，a，b相交节点后链表长度一致。
