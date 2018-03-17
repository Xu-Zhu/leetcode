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
