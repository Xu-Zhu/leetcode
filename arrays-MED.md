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

## 3 4 55.Jump Game
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
