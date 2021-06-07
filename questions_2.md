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
    - Idea is, if we reached at some sum x, and after few ups and down, I again see x, that means the values between those indices would sum to 0.
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

4. Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.  
<https://leetcode.com/problems/word-break/>  
    <details>
    <summary>Quick Summary</summary>

    - DP
    - Create a bool vector that denotes till what index, the substring is possible to make using words in `wordDict`.
    - Mark `0th` index to `true`, as base condition.
    - Loop `i` through the length of the string.
    - Now, for each possible substring starting at index `j` and ending at `i`, `j < i`, check if it is present in wordDict. If it is, mark `i`th `dp` to `true` and try finding for `i+1`th index.
    </details>

5. Given a list of daily temperatures `T`, return a list such that, for each day in the input, tells you how many days you would have to wait until a warmer temperature. If there is no future day for which this is possible, put `0` instead.  
<https://leetcode.com/problems/daily-temperatures/>  
    <details>
    <summary>Quick Summary</summary>

    - Stack based question.
    - In stack, keep track of decreasing temperatures.
    - If there is a temperature on stack that is less than the current temperature, put difference in their indices in result vector corresponding stack temperature.
    </details>

6. You are given an array of integers `stones` where `stones[i]` is the weight of the `ith` stone.  
    We are playing a game with the stones. On each turn, we choose any two stones and smash them together. Suppose the stones have weights `x` and `y` with `x <= y`. The result of this smash is:  

    - If `x == y`, both stones are destroyed, and
    - If `x != y`, the stone of weight `x` is destroyed, and the stone of weight `y` has new weight `y - x`.  
    At the end of the game, there is *at most one* stone left.  

    Return the smallest possible weight of the left stone. If there are no stones left, return `0`.  
<https://leetcode.com/problems/last-stone-weight-ii/>  
    <details>
    <summary>Quick Summary</summary>

    - DP question.
    - The problem boils down to dividing set of stones in two groups such that their difference is minimum.
    - `TotalSum = Sum_of_group_1 + Sum_of_group_2`
    - `Difference = Sum_of_group_1 - Sum_of_group_2`
    - We want to `minimize(Difference)`
    - `TotalSum - Difference = 2 * Sum_of_group_2`
    - To `minimize(Difference)`, do `maximize(TotalSum - 2 * sum_of_group_2)`
    - PseudoCode:
        - Mark all possible sums using stones.
        - Find the highest possible `sum <= totalSum/2`, and return `totalSum - 2 * sum`
    </details>

7. In a deck of cards, each card has an integer written on it.  
    Return true if and only if you can choose X >= 2 such that it is possible to split the entire deck into 1 or more groups of cards, where:  
    - Each group has exactly X cards.  
    - All the cards in each group have the same integer.  
<https://leetcode.com/problems/x-of-a-kind-in-a-deck-of-cards/>  
    <details>
    <summary>Quick Summary</summary>

    - Math problem
    - Find the counts of each integer.
    - Find gcd of all the counts.
    - If gcd == 1, return false, else return true.
    </details>

8. Implement the RandomizedSet class:  
    - RandomizedSet() Initializes the RandomizedSet object.
    - bool insert(int val) Inserts an item val into the set if not present. Returns true if the item was not present, false otherwise.
    - bool remove(int val) Removes an item val from the set if present. Returns true if the item was present, false otherwise.
    - int getRandom() Returns a random element from the current set of elements (it's guaranteed that at least one element exists when this method is called). Each element must have the same probability of being returned.
<https://leetcode.com/problems/insert-delete-getrandom-o1/>  
    <details>
    <summary>Quick Summary</summary>

    - Keep a hash that maps value to its index, and a vector of nums.
    - Insertion
        - Push into vector and place last index in hash corresponding to number being inserted.
    - Removal
        - Find the location of current num using hash.
        - Swap it with last element in the vector.
        - Pop last element from vector, remove the element from hash.
    - getRandom
        - Get a random index
        - return the num from vector at that index.
    </details>

9. Given a binary tree with the following rules:  
    - `root.val == 0`
    - If `treeNode.val == x` and `treeNode.left != null`, then `treeNode.left.val == 2 * x + 1`
    - If `treeNode.val == x` and `treeNode.right != null`, then treeNode.`right.val == 2 * x + 2`  
    Now the binary tree is contaminated, which means all `treeNode.val` have been changed to `-1`.

    You need to first recover the binary tree and then implement the `FindElements` class:
    - `FindElements(TreeNode* root)` Initializes the object with a contaminated binary tree, you need to recover it first.
    - `bool find(int target)` Return if the `target` value exists in the recovered binary tree.  
<https://leetcode.com/problems/find-elements-in-a-contaminated-binary-tree/>  
    <details>
    <summary>Quick Summary</summary>

    - To recover the tree, do a level order traversal, and keep updating values of left and right child as per given conditions.
    - Also, push each value seen till now in a set.
    - To find, return if that value is there in set.
    </details>

10. You are given an integer array `nums` and an integer `x`. In one operation, you can either remove the leftmost or the rightmost element from the array `nums` and subtract its value from `x`. Note that this modifies the array for future operations.  
    Return the *minimum number* of operations to reduce `x` to *exactly* `0` if it's possible, otherwise, return `-1`.  
<https://leetcode.com/problems/minimum-operations-to-reduce-x-to-zero/>  
    <details>
    <summary>Quick Summary</summary>

    - Indirect way of asking maximize the contiguous array which has `sum = totalSum - x`.
    - Maintain a prefix-sum `hash` containing what is the `index`, this `sum` was seen.
    - Init `hash` with `0 = -1`, sum `0` was last seen at `-1th` index, meaning I should not take any element to make a sum 0.
    - If `current_sum - x` is seen before, update `maxLen` using `current_index` - index saved for `current_sum - x`
    - Put `current_index` for `current_sum` in `hash`.
    - If the numbers are non-negative, another solution can be 2 pointer solution, using the same approach, maximize `totalSum - target`.
        - Keep 2 pointers, `i` and `j`.
        - If `current_sum < totalSum - target`, add `nums_at_j` to `current_sum`.
        - Now, while `current_sum >= totalSum - target`, remove elements from beginning (`nums_at_i`). Also, if `current_sum == totalSum - target`, update `maxLen`.
    </details>

11. Given a characters array tasks, representing the tasks a CPU needs to do, where each letter represents a different task. Tasks could be done in any order. Each task is done in one unit of time. For each unit of time, the CPU could complete either one task or just be idle.  
    However, there is a non-negative integer n that represents the cooldown period between two same tasks (the same letter in the array), that is that there must be at least n units of time between any two same tasks.  
    Return the least number of units of times that the CPU will take to finish all the given tasks.  
<https://leetcode.com/problems/task-scheduler/>  
    <details>
    <summary>Quick Summary</summary>

    - Find out each task's frequency.
    - Also, find out what is the highest frequency.
    - Set `temporary_result` to `(highest_frequency - 1) * (n + 1)`. This means that just to accommodate the most frequent word, I would take up above specified space if I were to interleave `n` slots.
    - Now, if there were more tasks with same highest frequency, they would be placed immediately after the slots occupied by task in step 3. So we increase the `temporary_result` by 1 for each of same frequency task.
    - `temporary_result` is your minimum CPU time. But there can be a lot of less frequent tasks. So, those would have to be accommodated in between empty slots, or beyond `temporary_result` if there can't be accommodated in between. So, result would be `min(tasks.size(), temporary_result)`.
    </details>

12. Given an array of integers `heights` representing the histogram's bar height where the width of each bar is 1, return the area of the largest rectangle in the histogram.  
<https://leetcode.com/problems/largest-rectangle-in-histogram/>  
    <details>
    <summary>Quick Summary</summary>

    - Stack problem.
    - Maintain a stack that keeps all the increasing height histograms.
    - As soon as you see smaller height histogram, pop it off.
    - Update `maxArea` to be this poped `height *` (length of the histogram which had this height), i.e. `height * (current_index - 1 - index_of_current_top_of_histogram)`.
    </details>

13. Given a set of `n` people (numbered 1, 2, ..., n), we would like to split everyone into two groups of any size.  
    Each person may dislike some other people, and they should not go into the same group.  
    Formally, if `dislikes[i] = [a, b]`, it means it is not allowed to put the people numbered `a` and `b` into the same group.  
    Return true if and only if it is possible to split everyone into two groups in this way.  
<https://leetcode.com/problems/possible-bipartition/>  
    <details>
    <summary>Quick Summary</summary>

    - Idea is to assign one person to group A, and its neighbors to group B in DFS manner. At any point, if group is violated, return false, otherwise return true.
    - Create a neighbors map, and maintain a hash telling what is the group this person belongs to.
    - For each person, do a dfs for its neighbors with group `true`.
    - For each person, if it is not there in hash, add it to hash. and check for its neighbors with other group.
    - If person is there in hash, check if the group matches. If not, return false.
    </details>

14. You are given an array `nums` that consists of non-negative integers. Let us define rev(x) as the reverse of the non-negative integer x. For example, rev(123) = 321, and rev(120) = 21. A pair of indices (i, j) is nice if it satisfies all of the following conditions:

    - `0 <= i < j < nums.length`
    - `nums[i] + rev(nums[j]) == nums[j] + rev(nums[i])`
    Return the number of nice pairs of indices. Since that number can be too large, return it modulo `10^9 + 7`.
<https://leetcode.com/problems/count-nice-pairs-in-an-array/>  
    <details>
    <summary>Quick Summary</summary>

    - The condition can be rearranged to `(nums[i] - rev(nums[i])) == (nums[j] - rev(nums[j]))`.
    - Transform each `nums[i]` into `(nums[i] - rev(nums[i]))`.
    - Keep a map storing the frequencies of values that you have seen so far. For each i, check if `nums[i]` is in the map. If it is, then add that count to the overall count. Then, increment the frequency of `nums[i]`.
    </details>

15. There are `n` gas stations along a circular route, where the amount of gas at the `ith` station is `gas[i]`.  
    You have a car with an unlimited gas tank and it costs `cost[i]` of gas to travel from the `ith` station to its next `(i + 1)th` station. You begin the journey with an empty tank at one of the gas stations.  
    Given two integer arrays `gas` and `cost`, return the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return `-1`. If there exists a solution, it is *guaranteed* to be *unique*.  
<https://leetcode.com/problems/gas-station/>  
    <details>
    <summary>Quick Summary</summary>

    - Assume that you start from last gas station, and end at 0th station.
    - Update `fuel = gas[start] - cost[start]`.
    - Do the following till start > end:
        - If you have enough fuel (`fuel >= 0`), update `fuel` to include `end`'s `gas` and `cost`, and increase `end` by one.
        - If you don't have enough `fuel`, start 1 earlier, and update `fuel` accordingly.
    - Return `start` if `fuel >= 0`, else `-1`.
    </details>

16. Given the array orders, which represents the orders that customers have done in a restaurant, i.e., `orders[i]=[customerNamei,tableNumberi,foodItemi]` where `customerNamei` is the name of the customer, `tableNumberi` is the table customer sit at, and `foodItemi` is the item customer orders.  
Return the restaurant's "display table". The "display table" is a table whose row entries denote how many of each food item each table ordered. The first column is the table number and the remaining columns correspond to each food item in alphabetical order. The first row should be a header whose first column is "Table", followed by the names of the food items. Note that the customer names are not part of the table. Additionally, the rows should be sorted in numerically increasing order.  
<https://leetcode.com/problems/display-table-of-food-orders-in-a-restaurant/>  
    <details>
    <summary>Quick Summary</summary>

    -
    </details>

17. You are given an `m x n` integer matrix `heights` representing the height of each unit cell in a continent. The Pacific ocean touches the continent's left and top edges, and the Atlantic ocean touches the continent's right and bottom edges.  
Water can only flow in four directions: up, down, left, and right. Water flows from a cell to an adjacent one with an equal or lower height.  
Return a list of grid coordinates where water can flow to both the Pacific and Atlantic oceans.  
<https://leetcode.com/problems/pacific-atlantic-water-flow/>  
    <details>
    <summary>Quick Summary</summary>

    -
    </details>

18. Your country has an infinite number of lakes. Initially, all the lakes are empty, but when it rains over the nth lake, the nth lake becomes full of water. If it rains over a lake which is full of water, there will be a flood. Your goal is to avoid the flood in any lake.  
Given an integer array rains where:  

    1. `rains[i] > 0` means there will be rains over the `rains[i]` lake.  
    2. `rains[i] == 0` means there are no rains this day and you can choose one lake this day and dry it.  

    Return an array ans where:  
    1. `ans.length == rains.length`  
    2. `ans[i] == -1` if `rains[i] > 0`.  
    3. `ans[i]` is the lake you choose to dry in the ith day if `rains[i] == 0`.  
  If there are multiple valid answers return any of them. If it is impossible to avoid flood return an empty array.  
<https://leetcode.com/problems/avoid-flood-in-the-city/>  
    <details>
    <summary>Quick Summary</summary>

    -
    </details>

19. Given an array `nums` with n integers, your task is to check if it could become non-decreasing by modifying at most one element.  
We define an array is non-decreasing if `nums[i] <= nums[i + 1]` holds for every i (0-based) such that `(0 <= i <= n - 2)`.  
<https://leetcode.com/problems/non-decreasing-array/>  
    <details>
    <summary>Quick Summary</summary>

    -
    </details>

20. Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.  
<https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/>  
    <details>
    <summary>Quick Summary</summary>

    -
    </details>

21. You are given an integer array `nums` with no duplicates. A maximum binary tree can be built recursively from `nums` using the following algorithm:  

    1. Create a `root` node whose value is the maximum value in `nums`.  
    2. Recursively build the left subtree on the subarray prefix to the left of the maximum value.  
    3. Recursively build the right subtree on the subarray suffix to the right of the maximum value.  
Return the maximum binary tree built from `nums`.  
<https://leetcode.com/problems/maximum-binary-tree/>  
    <details>
    <summary>Quick Summary</summary>

    -
    </details>

22. You are given an array of words where each word consists of lowercase English letters.  
`wordA` is a predecessor of `wordB` if and only if we can insert exactly one letter anywhere in `wordA` without changing the order of the other characters to make it equal to `wordB`.  
A word chain is a sequence of words `[word1, word2, ..., wordk]` with `k >= 1`, where `word1` is a predecessor of `word2`, `word2` is a predecessor of `word3`, and so on. A single word is trivially a word chain with `k == 1`.  
Return the length of the longest possible word chain with words chosen from the given list of `words`.  
<https://leetcode.com/problems/longest-string-chain/>  
    <details>
    <summary>Quick Summary</summary>

    -
    </details>

23. You are given an integer array heights representing the heights of buildings, some bricks, and some ladders.  

    1. If the current building's height is greater than or equal to the next building's height, you do not need a ladder or bricks.  
    2. If the current building's height is less than the next building's height, you can either use one ladder or `(h[i+1] - h[i])` bricks.  
Return the furthest building you can reach using given bricks and ladders.  
    <details>
    <summary>Quick Summary</summary>

    -
    </details>

24. There are n ice cream bars. You are given an array `costs` of length n, where `costs[i]` is the price of the `ith` ice cream bar in `coins`. The boy initially has `coins` coins to spend, and he wants to buy as many ice cream bars as possible.  
Return the maximum number of ice cream bars the boy can buy with `coins` coins.  
<https://leetcode.com/problems/maximum-ice-cream-bars/>  
    <details>
    <summary>Quick Summary</summary>

    -
    </details>

25. Given an unsorted array nums, reorder it in-place such that `nums[0] <= nums[1] >= nums[2] <= nums[3]....`  
<https://www.lintcode.com/problem/508/>  
<https://www.leetcode.com/problems/wiggle-sort/>  
    <details>
    <summary>Quick Summary</summary>

    -
    </details>

26. Given a string s, return the longest palindromic substring in s.  
<https://leetcode.com/problems/longest-palindromic-substring/>  
    <details>
    <summary>Quick Summary</summary>

    -
    </details>

27. Given a string s containing only digits, return the number of ways to decode it.  
<https://leetcode.com/problems/decode-ways/>  
    <details>
    <summary>Quick Summary</summary>

    -
    </details>

28. Given an array of words and a width maxWidth, format the text such that each line has exactly maxWidth characters and is fully (left and right) justified.  

    1. Pack as many words as you can in each line.  
    2. Extra spaces should be distributed as evenly as possible.  
<https://leetcode.com/problems/text-justification/>  
    <details>
    <summary>Quick Summary</summary>

    -
    </details>

29. Given a string s, check if the letters can be rearranged so that two characters that are adjacent to each other are not the same.  
If possible, output any possible result.  If not possible, return the empty string.  
<https://leetcode.com/problems/reorganize-string/>  
    <details>
    <summary>Quick Summary</summary>

    -
    </details>

30. The API: `int read4(char *buf)` reads 4 characters at a time from a file.  
The return value is the actual number of characters read. For example, it returns 3 if there is only 3 characters left in the file.  
By using the `read4` API, implement the function `int read(char *buf, int n)` that reads n characters from the file.  
<https://www.lintcode.com/problem/660/>  
<https://www.leetcode.com/problems/read-n-characters-given-read4-ii-call-multiple-times/>  
    <details>
    <summary>Quick Summary</summary>

    -
    </details>

31. Check whether the original sequence `org` can be uniquely reconstructed from the sequences in `seqs`. The `org` sequence is a permutation of the integers from 1 to n. Reconstruction means building a shortest common supersequence of the sequences in `seqs` (i.e., a shortest sequence so that all sequences in `seqs` are subsequences of it). Determine whether there is only one sequence that can be reconstructed from `seqs` and it is the `org` sequence.  
<https://www.lintcode.com/problem/605/>  
<https://leetcode.com/problems/sequence-reconstruction/>
    <details>
    <summary>Quick Summary</summary>

    -
    </details>

32. Given an array and a number k, find the largest sum of the subarray containing at least k numbers. It may be assumed that the size of array is at-least k.  
<https://practice.geeksforgeeks.org/problems/largest-sum-subarray-of-size-at-least-k3121/1/>  
    <details>
    <summary>Quick Summary</summary>

    -
    </details>

33. Given an input string (s) and a pattern (p), implement wildcard pattern matching with support for '?' and '*' where:  
    1. '?' Matches any single character.  
    2. '*' Matches any sequence of characters (including the empty sequence).  
The matching should cover the entire input string (not partial).  
<https://leetcode.com/problems/wildcard-matching/>  
    <details>
    <summary>Quick Summary</summary>

    -
    </details>

34. You are given n​​​​​​ tasks labeled from 0 to n - 1 represented by a 2D integer array tasks, where tasks[i] = [enqueueTimei, processingTimei] means that the i​​​​​​th​​​​ task will be available to process at enqueueTimei and will take processingTimei to finish processing.  
You have a single-threaded CPU that can process at most one task at a time and will act in the following way:  
    1. If the CPU is idle and there are no available tasks to process, the CPU remains idle.  
    2. If the CPU is idle and there are available tasks, the CPU will choose the one with the shortest processing time. If multiple tasks have the same shortest processing time, it will choose the task with the smallest index.  
    3. Once a task is started, the CPU will process the entire task without stopping.  
    4. The CPU can finish a task then start a new one instantly.  
Return the order in which the CPU will process the tasks.  
<https://leetcode.com/problems/single-threaded-cpu/>  
    <details>
    <summary>Quick Summary</summary>

    -
    </details>
