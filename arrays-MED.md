# leetcode
## medium
## 1 11. Container With Most Water
```
class Solution {
    public int maxArea(int[] height) {
        int left = 0;
        int right = height.length - 1;
        int storge = 0;
        while(left < right) {
            storge = Math.max(storge,(right - left) * Math.min(height[left],height[right]));
            if(height[left] < height[right]) {
                left++; }
            else {
                right--;}
        }
        return storge;
    }
}
```
By using left and right two pointer, we could have the height and bottom. By using while loop and if-else condition loop we will have the answer.

## 2 16 3Sum Closest
```
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        int result = nums[0] +nums[1] +nums[nums.length - 1];
        Arrays.sort(nums);
        for(int i = 0; i < nums.length -2; i++) {
            int left = i + 1;
            int right = nums.length - 1;
            while(left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if(sum > target) {
                    right--;
                } else {
                    left ++;
                }
                if(Math.abs(result - target) > Math.abs(sum - target)) {
                result = sum;
                }
            }
        }
     return result;   
    }
}
```
## 3 18.4Sum Closest
```
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        ArrayList<List<Integer>> res = new ArrayList<List<Integer>>();
        if(nums.length<4)return res;
        Arrays.sort(nums);
        for(int i = 0; i < nums.length -3; i++) {
            if(nums[i] + nums[i+1] + nums[i+2] +nums[i+3] > target) {
                break;
            }
            if(nums[i] + nums[nums.length -3] +nums[nums.length - 2] + nums[nums.length -1] < target) {
               continue;
            }
            if(i>0&&nums[i]==nums[i-1])continue;
            for(int j = i + 1; j < nums.length -2; j++) {
                if(nums[i] + nums[j] + nums[j + 1] + nums[j + 2] > target) {
                    break;
                }
                if(nums[i] + nums[j] + nums[nums.length -2] + nums[nums.length -1] < target) {
                    continue;
                } 
                if(j>i+1&&nums[j]==nums[j-1])continue;
                
                int low = j + 1;
                int high = nums.length -1;
                while(low < high) {
                    int sum = nums[i] + nums[j] + nums[low] + nums[high];
                    if(sum == target) {
                        res.add(Arrays.asList(nums[i], nums[j], nums[low], nums[high]));
                    while(low<high&&nums[low]==nums[low+1])low++; //skipping over duplicate on low
                    while(low<high&&nums[high]==nums[high-1])high--; //skipping over duplicate on high
                    low++; 
                    high--;
                }
                //move window
                else if(sum<target)low++; 
                else high--;

                    }
                }
            }
        return res;
    }
}
```

## 4 55.Jump Game
```
class Solution {
    public boolean canJump(int[] nums) {
        int goal = nums.length - 1;
        for(int i = nums.length - 2; i >= 0; i--) {
            if(nums[i] + i >= goal) {
                goal = i;
            }
        }
        return goal <= 0;
    }
}
```
Base on Greedy alogrithm.

## 5 73 set matrix zeroes
```
class Solution {
    public void setZeroes(int[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;
        boolean row = false, col = false;
        for(int i = 0; i < m; i++) {
            for(int j = 0; j < n; j++) {
                if(matrix[i][j] == 0) {
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                    if(i == 0){
                       row = true;
                     }
                    if(j == 0) {
                       col = true;
                }
                }
            }
        }
        for(int i = 1;i < m; i++){
            if(matrix[i][0] == 0) {
                for(int j = 1; j < n; j++) {
                    matrix[i][j] = 0;
                }
            }
        }
        for(int j = 1; j < n; j++) {
            if(matrix[0][j] == 0) {
                for(int i = 1; i < m ; i++) {
                    matrix[i][j] = 0;
                }
            }
        }
        if (row){
            for (int j = 0; j < n; j++)
                 matrix[0][j] = 0;
         }
        if (col){
            for(int i = 0; i < m; i++)
                matrix[i][0] = 0;
        }
    }
}
```
The point we set two boolean pointer is if we simply set matrix[i][0] and matrix[0][j] = 0 it will initialize entire matrix to zero after we run next two for loops. Because we will have matrix[0][0] = 0 and it is incorrect.

## 6 228 Summary Ranges
```
class Solution {
    public List<String> summaryRanges(int[] nums) {
        List<String> list = new ArrayList();
        for(int i = 0; i < nums.length; i++) {
            int a = nums[i];
            while( i + 1 < nums.length && nums[i+1] - nums[i] == 1) {
                i++;
            }
            if(a != nums[i]) {
                list.add(a + "->"+nums[i]);
            } else {
                list.add(a+"");
            }
        }
     return list;   
    }
}
```
The idea is we need to find mutiple arithmetic progressions.  
we have an a = nums[i] as a start. By using a while loop we will have the end. Also we update the value of i in for loops.
## 7 229 Majority Element II
```
class Solution {
    public List<Integer> majorityElement(int[] nums) {
        if(nums == null || nums.length == 0) return new ArrayList<Integer>();
        List<Integer> result = new ArrayList<Integer>();
        int number1 = nums[0], number2 = nums[0],count1 = 0, count2 = 0;
        for(int i = 0; i < nums.length; i++) {
            if(nums[i] == number1) {
                count1++;
            } else if(nums[i] == number2) {
                count2++;
            } else if(count1 == 0) {
                number1 = nums[i];
                count1 = 1;
            } else if(count2 == 0) {
                number2 = nums[i];
                count2 = 1;
            } else {
                count1--;
                count2--;
            }
        }
        count1 = 0;
        count2 = 0;
        for(int i = 0; i < nums.length; i++) {
            if(nums[i] == number1) {
                count1++;
            }
            if(nums[i] == number2) {
                count2++;
            }
        }
        if(count1 > nums.length/3) {
            result.add(number1);
        }
        if(count2 > nums.length/3 && number1 != number2) {
            result.add(number2);
        }
        return result;
    }
}
```
Since we need to find majoirty elements. It could be at most two numbers cause they should show up more than N/3 times. Which we set numbers1 and number2. we also have count1, count2. The idea of first for loop is trying two looking for the target numbers which we will put them into the next for loop. We will have out result array after second for loop done.
## 8 442. Find All Duplicates in an Array
```
class Solution {
    public List<Integer> findDuplicates(int[] nums) {
        List<Integer> result = new ArrayList<Integer>();
        for(int i = 0; i < nums.length; i++) {
            int val = Math.abs(nums[i]) - 1;
            if(nums[val] > 0) {
                nums[val] = - nums[val];
            } else {
                result.add(val+1);
            }
        }
        return result;
    }
}
```
We set val = Math.abs(nums[i]) - 1 which means nums[i] = val + 1. The idea we use math.abs beacuse we will change nums[val] to negative. After we finished changing all nums[val]. we will look for which nums[val] > 0 then we change it to negative. if some nums[val] are alreaday less than 0 we add that exaclty val+1 in to array.

## 9 526. Beautiful Arrangement
```
public class Solution {
   
    int count = 0;
    public int countArrangement(int N) {
        if (N == 0) return 0;
       
        helper(N, N, new int[N + 1]);
        return count;
    }
    
    private void helper(int N, int pos, int[] used) {
        if (pos == 0) {
            count++;
            return;
        }
        
        for (int i = N; i > 0; i--) {
            if (used[i] == 0 && (i % pos == 0 || pos % i == 0)) {
                used[i] = 1;
                helper(N, pos - 1, used);
                used[i] = 0;
            }
        }
    }
 ```
 This solution was based on marks which is used[i]. We used i-- for loop cause larger integer is hard to be divisible. It will improve 
the performance.
## best solution:
```
class Solution {
   private int count = 0;
    private void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
    private void helper(int[] nums, int start) {
        if (start == 0) {
            count++;
            return;
        }
        for (int i = start; i > 0; i--) {
            swap(nums, start, i);
            if (nums[start] % start == 0 || start % nums[start] == 0) helper(nums, start-1);
            swap(nums,i, start);
        }
    }
    public int countArrangement(int N) {
        if (N == 0) return 0;
        int[] nums = new int[N+1];
        for (int i = 0; i <= N; i++) nums[i] = i;
        helper(nums, N);
        return count;
    }
}
```
By using swap nums[i] and nums[start] we can avoid duplicate cases.
## 10. 238. Product of Array Except Self
```
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int leng = nums.length;
        int[] res = new int[leng];
        res[0] = 1;
        //i - left 
        for(int i = 1; i < leng; i++) {
            res[i] = res[i - 1] * nums[i - 1];
        }
        //right
        int right = 1;
        for(int i = leng -2; i >= 0; i--) {
            right *= nums[i+1];
            res[i] *= right;
        }
        return res;
    }
}
```
There are two parts. left part and right part for i. let's have an example first 2, 3, 4, 5. so 2 left: none 3-left: 2 4-left: 2 3, 4-left:2 3 4. Once we int res[0] = 1; so i -left will be: nums[i-1] * res[i -1]. On the right part. we int right = 1. By using for loop with i-- we do the same way. At last res[i]*= right will be the final answer.
