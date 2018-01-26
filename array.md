# leetcode
Start from array part. I hope I could finish 10 for everyday.
Arrays 类
java.util.Arrays 类能方便地操作数组，它提供的所有方法都是静态的。
具有以下功能：
给数组赋值：通过 fill 方法。
对数组排序：通过 sort 方法,按升序。
比较数组：通过 equals 方法比较数组中元素值是否相等。
查找数组元素：通过 binarySearch 方法能对排序好的数组进行二分查找法操作。

coding languge:Java

1.Merge Sorted Array
Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

solution: 
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        while(n > 0) {
        nums1[m+n-1] = (m == 0 || nums2[n-1] > nums1[m-1]) ? nums2[--n] : nums1[--m];
        }
    }
}
due to nums1 and nums2 are both sort arrays, we dont have to consider the sort detail any more.
why m+n-1 cause nums[0]
m==0 which is empty for both nums1[] and nums2[]. Hence,nums1[m+n-1] is empty
Or
nums1[m+n-1]= when nums2[n-1] > nums1[m-1] 
If ture = nums2[n-1] else nums1[n-1]

2. two sum 
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

solution:
time complexity n^2:
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for (int i = 0; i < nums.length -1; i++){
            for (int j = i+1; j < nums.length; j++){          
         if (nums[i] == target - nums[j]){
            return new int[] {i,j};
         }
       }
    }
        throw new IllegalArgumentException("No two sum solution");
    }
}

Using double for loop to achieve the goal. 
Why i< nums.length-1 ?
Cause nums[] start from nums[0].
We should return to a new int[] {i,j}
Most important:
throw new IllegalArgumentException("No two sum solution");
Cause there might be no solution.

Solution 2:
time complexity o(n)
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] res = new int[2];
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        for(int i = 0; i <nums.length; i++) {
            if (map.containsKey(target - nums[i])) {
                res[1] = i;
                res[0] = map.get(target - nums[i]);
                return res;
            }
            map.put(nums[i] , i);
        }
        return res;
    }
}
//public int[] twoSum(int[] numbers, int target) {
//       Map<Integer, Integer> map = new HashMap<Integer, Integer>();
//        for (int i = 0; i < numbers.length; map.put(numbers[i], ++i)) 
//            if (map.containsKey(target - numbers[i])) 
//                return new int[]{map.get(target - numbers[i]),i};
//        return new int[]{0,0};
//    }
//}

3. Largest Number At Lease Twice of Others
In a given integer array nums, there is always exactly one largest element.

Find whether the largest element in the array is at least twice as much as every other number in the array.

If it is, return the index of the largest element, otherwise return -1.


class Solution {
    public int dominantIndex(int[] nums) {
        int maxIndex = 0;
        for (int i = 0; i < nums.length; ++i) {
            if (nums[i] > nums[maxIndex])
                maxIndex = i;
        }
        for (int i = 0; i < nums.length; ++i) {
            if (maxIndex != i && nums[maxIndex] < 2 * nums[i])
                return -1;
        }
        return maxIndex;
        
    }
}

The idea is we int maxIndex = 0. By using for loop, we could have a nums[maxIndex] after we traveled nums[]. It will be the max value.
Then we may have another for loop to figure out wether the nums[maxIndex] is twice as nums[i].
Why maxIndex != i?
Cause the nums[] may be : [1]
which means maxIndex is 0 and i = 0. In that case, the function would return -1 if we dont have a != condition.

4. Min Cost Climbing Stairs
class Solution {
   // public int minCostClimbingStairs(int[] cost) {
//        int f1 = 0, f2 = 0;
 //       for(int i = 0; i < cost.length; i++) {
//            int totalCost = cost[i] + Math.min(f1,f2);
//            f1 = f2;
//            f2 = totalCost;
//        }
//        return Math.min(f1,f2);
//    }
public int minCostClimbingStairs(int[] cost) {
        int dp0 = 0;
        int dp1 = 0;
        int dp2 = 0;
        for (int i = 2; i < cost.length + 1; i++) {
            dp2 = Math.min(dp0 + cost[i - 2] , dp1 + cost[i - 1]);
            dp0 = dp1;
            dp1 = dp2;
        }
        return dp2;
    }
}

two different solutions;
Point f1 = f2; 
f2 = totalCost;
return Math.min(f1,f2) e.p. cost[]={0,0,1,0}. We would get a expectation 1 if we return to totalCost.

solution2:
return dp2. In this case we coultnt return to Math.min(dp0,dp1) cause dp2 = Math.min(totalCost(i-2)+Cost[i-2], totalCost(i-1)+Cost(i-1).

5.
