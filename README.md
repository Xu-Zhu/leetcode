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

## 2 
