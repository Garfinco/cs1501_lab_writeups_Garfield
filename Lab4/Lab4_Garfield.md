# Lab 4 Garfield Zhang Remove Sub-Folders from the Filesystem
<br>

## Solution
```
class Solution {
    public int maxProduct(int[] nums) {
        Arrays.sort(nums);
        int end_index = nums.length - 1; 
        return (nums[end_index - 1] - 1) * (nums[end_index] -1);
    }
}
```

### Explain
Sort the array first, so the largest number will be at the end, get the last two number both minus 1 and mutilply them

<br>

## Time and Space Complexity
### time:
    O(nlogn) Arrays.sort() sorting

### Space:
    O(n) numbers of int in array
  