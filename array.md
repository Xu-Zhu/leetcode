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
m==0 which is empty for both nums1[] and nums2[]. Hence,nums1[m+n-1] is empty Or
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

4 Min Cost Climbing Stairs
      
    class Solution {  
    public int minCostClimbingStairs(int[] cost) {
            int f1 = 0, f2 = 0;
            for(int i = 0; i < cost.length; i++) {
            int totalCost = cost[i] + Math.min(f1,f2);
            f1 = f2;
            f2 = totalCost;
        }
         return Math.min(f1,f2);     
       }
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

5.Find Pivot Index
Given an array of integers nums, write a method that returns the "pivot" index of this array.
We define the pivot index as the index where the sum of the numbers to the left of the index is equal to the sum of the numbers to the right of the index.
If no such index exists, we should return -1. If there are multiple pivot indexes, you should return the left-most pivot index.
  
    class Solution {
    public int pivotIndex(int[] nums) {
        int totalLeft = 0, total = 0;
        for(int i = 0; i < nums.length; i++) {
            total = total +nums[i];
        }
        for(int i = 0; i < nums.length; i++) {
            if(i !=0) {
            totalLeft = totalLeft + nums[i-1];}
            if(totalLeft == total- totalLeft - nums[i]) {
                return i;
            }
        }   
        return -1;
      }
    }
     
6.1-bit and 2-bit Characters
    
    class Solution {
    public boolean isOneBitCharacter(int[] bits) {
        int n = bits.length;
        int i = 0;
        for (; i < n -1;) {
            if (bits[i] == 1) {
                i += 2;
            }
            else {
                i += 1;
            }
        }
        return i == n - 1;
        }
     }

Cause there are only two different types character either 10/11 or 0. we will plus 2 to i, if it comes 1,no matter wut comes after 1, it would be 10 or 11, plus 0 to i, if it only comes 0. Therefore, once we have traveled n-2 length, we would like to know the total sum of i wether equal to n-1 or not. Then return to n-1.  

## 7.  Remove Duplicates from Sorted Array
```
class Solution {
    public int removeDuplicates(int[] nums) {
        int i = 0;
        for(int j = 1; j < nums.length; j++) {
            if(nums[j] != nums[i]) {
                i++;
                nums[i] = nums[j];
            }
        }
    return i+1;
    }
}
```  
  
  The idea is have a i and j at the same time j is a faster pointer, i is the slower one. Which j = i + 1. By using for loop we can travel all the nums[] from nums[i] to nums[nums.length -1].  
  why i++ comes first ? also why return i+1.  
  Because we have alreday have a exactly value of nums[0] which is i=0. now we want to get a value for nums[1] which is i=1. If nums[i] != nums[j] we may put the value of nums[j] to nums[i]. 
    
    For example:  
  i = 0 ; j = 1;  
  nums[0] != nums[1]   
  if nums[i] = nums[j] comes first. which would be nums[0] =nums[1] . It changes the value of  nums[0]. Uncorrect.  
  The for loop may keep performing i++ j++ and if(nums[i] != nums[i+1]) section.    
  
##8. Remove Element
```
class Solution {
    public int removeElement(int[] nums, int val) {
        int i = 0;
        for(int j =0; j < nums.length; ++j) {
            if(nums[j] != val) {
                nums[i] = nums[j];
                i++;
            }
        }
        return i;
    }
}
```  
  
  I have set two pointers i and j， once num[j] !=val, makes nums[i] =nums[j]. At the same time i++ could be nums.length cause when nums[0] equal to a exactly integer , i++ will equal to 1 which is nums.length at that time.    
   

  
## 9.Degree of a n Array 
## Need review
```
class Solution {
    public int findShortestSubArray(int[] nums) {
        Map<Integer, Integer> left = new HashMap(),
            right = new HashMap(), count = new HashMap();

        for (int i = 0; i < nums.length; i++) {
            int x = nums[i];
            if (left.get(x) == null) {
                left.put(x, i);
            }
            right.put(x, i);
            count.put(x, count.getOrDefault(x, 0) + 1);
        }

        int ans = nums.length;
        int degree = Collections.max(count.values());
        for (int x: count.keySet()) {
            if (count.get(x) == degree) {
                ans = Math.min(ans, right.get(x) - left.get(x) + 1);
            }
        }
        return ans;
    }
} 
```
Since we can have the minum length from (right most) nums[x] - (left most) nums[x] + 1
set three hashmaps left; right; count.
using for loop to update ans value and use Math.min to get a minimum value by ans(x) with variable x.  
  
Another solution:
  ```
  public int findShortestSubArray(int[] nums) {
        if (nums.length == 0 || nums == null) return 0;
        Map<Integer, int[]> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++){
           if (!map.containsKey(nums[i])){
               map.put(nums[i], new int[]{1, i, i});  // the first element in array is degree, second is first index of this key, third is last index of this key
           } else {
               int[] temp = map.get(nums[i]);
               temp[0]++;
               temp[2] = i;
           }
        }
        int degree = Integer.MIN_VALUE, res = Integer.MAX_VALUE;
        for (int[] value : map.values()){
            if (value[0] > degree){
                degree = value[0];
                res = value[2] - value[1] + 1;
            } else if (value[0] == degree){
                res = Math.min( value[2] - value[1] + 1, res);
            } 
        }
        return res;
    }```


      
 We dont have to set 3 different nums[]. its not a effient way.   
 
  
## Need review upper solution as many times as possible.

## 10. Max Area of Island
## 2-D nums[]  
    
```nums[] [] grind.
  
int grid[][] = new int[10][10];

for(int i = 0; i < grid.length(); ++i) {
    for(int j = 0; j < grid[i].length(); ++j) {
        // Do whatever with grid[i][j] here
    }
}
```
  

    
## using DFS   

  
```public int maxAreaOfIsland(int[][] grid) {
        int max_area = 0;
        for(int i = 0; i < grid.length; i++)
            for(int j = 0; j < grid[0].length; j++)
                if(grid[i][j] == 1)max_area = Math.max(max_area, AreaOfIsland(grid, i, j));
        return max_area;
    }
    
    public int AreaOfIsland(int[][] grid, int i, int j){
        if( i >= 0 && i < grid.length && j >= 0 && j < grid[0].length && grid[i][j] == 1){
            grid[i][j] = 0;
            return 1 + AreaOfIsland(grid, i+1, j) + AreaOfIsland(grid, i-1, j) + AreaOfIsland(grid, i, j-1) + AreaOfIsland(grid, i, j+1);
        }
        return 0;
    }```
    
    
solution 2:
        
        ```public int maxAreaOfIsland(int[][] grid) {
        if (grid == null || grid.length == 0) {
            return 0;
        }
        int m = grid.length;
        int n = grid[0].length;
        int max = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1) {
                    int area = dfs(grid, i, j, m, n, 0);
                    max = Math.max(area, max);
                }
            }
        }
        return max;
    }

    int dfs(int[][] grid, int i, int j, int m, int n, int area) {
        if (i < 0 || i >= m || j < 0 || j >= n || grid[i][j] == 0) {
            return area;
        }
        grid[i][j] = 0;
        area++;
        area = dfs(grid, i + 1, j, m, n, area);
        area = dfs(grid, i, j + 1, m, n, area);
        area = dfs(grid, i - 1, j, m, n, area);
        area = dfs(grid, i, j - 1, m, n, area);
        return area;
    }```

  
  
  using two --for loops to travel entire int[] [] grid. if grid[i][j] == 1 start dfs then using Math.max(area,max_area) to find the maximum. cause max-area = Math.max(area,max_area). It will update max_area again and agian by for loop with variavble  i and j.  

dfs:
Two different version: || or &&. 
  
  && version : once grid[i] [j] = 1 has been explored and traveled, we changed the value to 0 and then we will explore adjacent grid[][].  
  The point of we change gird[i][j] to 0 is we wouldnt traveled it gain which we would only calculate it 1 time.   
  
    
## 11 Longest Continuous Increasing Subsequence.

soloution:

```class Solution {
    public int findLengthOfLCIS(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        int maxLength = 1;
        int res = 1;
        for(int i = 1;i < nums.length; i++) {
            if(nums[i-1] < nums[i]) {
                maxLength += 1;
                res = Math.max(res,maxLength);
            }
            else {
                maxLength = 1;
            }
        }
     return Math.max(res,maxLength);   
    }
}```
  
  if the nums isnt null. The maxLength will be at least 1. By using for loop we would have two defferent result. Either maxLength += 1 or reset maxLength after we have condition(nums[i-1] >= nums.length). Finally, return Math.max(res,maxLength).  
Point:  
we dont have to set i =0 , cause if three nums.length =1 e.p. : {1}. just return Math.max{res,maxLength}. 
To be honestly, we can also int res =1, cause we have exclude the situation which (nums.length == null) or (nums= null).
## 10.Search Insert Position
```class Solution {
    public int searchInsert(int[] nums, int target) {
        int position = 0;
        if(target < nums[0]) return 0;
        if(target > nums[nums.length-1]) return nums.length;
        for(int i = 0; i < nums.length;i++) {
            if(nums[i] < target) {
                position += 1;
            }
            else {
                break;
            }
        }
      return position;  
    }
}```


 
 

  
