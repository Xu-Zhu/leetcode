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
