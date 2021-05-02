# Questions discussed

Continuation from [questions_1.md](https://github.com/anuragtomer/questions/blob/main/questions_1.md).  
All the solution codes (in `C++`) can be accessed at appropriate difficulty folder [here](https://github.com/anuragtomer/practice_coding/tree/master/leetcode)

1. Given a binary array nums, return the maximum length of a contiguous subarray with an equal number of 0 and 1.  
<https://leetcode.com/problems/contiguous-array/>  
    <details>
    <summary>Quick Summary</summary>

    - Create a hash that maps each sum to the first index that sum was seen.
    - For each incoming 0, decrease your sum, and for each incoming 1, increase your sum.
    - For each sum, check if you've seen this previously. If so, calculate the max length from current index to first time this sum was seen.
    - If this is a new sum, save it in hash.
    - Idea is, if we reached at some sum x, and after few ups and down, I again see x, that means
    </details>

2. Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers.  
<https://leetcode.com/problems/3sum-closest/>  
    <details>
    <summary>Quick Summary</summary>

    - Sort the input.
    - Run a loop for each element, `nums[i]`.
    - Run `j` loop from beginning, `k` loop from end.
    - Search closest triplets of `nums[i] + nums[j] + nums[k]` to `target`.
    - If its not the closest, but the `sum` is smaller than `target`, we need higher number, increment `j`
    - Else if the sum is more than the `target`, we need a smaller number, decrement `k`.
    - Return the closest.
    </details>

3. You are given an `n x n` 2D matrix representing an image, rotate the image by 90 degrees (clockwise).  
<https://leetcode.com/problems/rotate-image/>  
    <details>
    <summary>Quick Summary</summary>

    - Flip the image upside down.
    - Transpose the image about diagonal.
    </details>
