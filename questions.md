# Questions discussed

All the solution codes (in `C++`) can be accessed at appropriate difficulty folder [here](https://github.com/anuragtomer/practice_coding/tree/master/leetcode)

1. Given a node 'p' of BST, and root, return the inorder successor of 'p'. Note that there is no pointer to parent.  
<https://www.lintcode.com/problem/inorder-successor-in-bst/>
    <details>
        <summary>Quick Solution</summary>

    - If given node has right child, return the left most child of right child of 'p'.
    - Otherwise, starting from root, push all the parents till 'p' in stack and pop till immediate  
      parent is successor (`p.val < parent.val`)

    </details>

2. Given a list of pair of `<take_off, landing>` time of flights, return the maximum no of flights that will be in air simultaneously.  
<https://www.lintcode.com/problem/number-of-airplanes-in-the-sky/>
    <details>
        <summary>Quick Solution</summary>

    - Sort on `take_off` time
    - Push one by one in min_heap. min heap is constructed on landing time.
    - If start time of incoming flight is greater than landing time of top of heap, pop heap until
      start time of incoming flight is less that landing time of top of heap (or heap is empty).
      Idea is to find overlapping flights.
    - Keep track of heap size after every insertion. Max of this would be the answer.

    </details>

3. Given a string array of 0's and 1's, find maximum subset of this array such that it has at most m 0's and n 1's.  
<https://leetcode.com/problems/ones-and-zeroes/>
    <details>
        <summary>Quick Solution</summary>

    - DP problem (0-1 knapsack variant).
    - For each element of array, try to follow two paths. Either take this and see if at most  
      conditions are met or ignore current element and try to fulfill conditions from other elements.

    </details>

4. Given an array of positive numbers and a positive target, find minimum contiguous subarray whose sum is greater  
   than or equal to `target`.  
<https://leetcode.com/problems/minimum-size-subarray-sum/>
    <details>
        <summary>Quick Solution</summary>

    - 2 pointer problem/sliding window problem.
    - Keep 2 pointers. The idea is that subarray defined by these 2 pointers would be the subarray which satisfies the
      given conditions.
    - Traverse each value from one end to another. Increase your ending pointer if the sum is still less than `target`.
    - If by adding the next element, the sum is greater than target, increase the starting pointer which denotes you are
      shrinking the array from beginning.
    - At each point in time, keep track what is the largest subarray size you saw.

    </details>

5. Given a array of integers, find the next permutation.  
<https://leetcode.com/problems/next-permutation/>
    <details>
        <summary>Quick Solution</summary>

    - Starting from last to first, find first entry which is non-increasing.
    - Find smallest greater element than the value found in step `1`. Again do this from the end.
    - Swap elements from step `1` and step `2`.
    - Reverse the subarray after index from step `1`.

    </details>

6. Given 2 strings, find the minimum no of deletions you need to make such that resulting strings are same.  
<https://leetcode.com/problems/delete-operation-for-two-strings/>
    <details>
        <summary>Quick Solution</summary>

    - Modified LCS.
    - Find the longest common subsequence in 2 strings using DP.
    - return `size1 + size2 - 2*(lcs)`

    </details>

7. Given a sorted array A of unique numbers, find the k-th missing number starting from the leftmost number of the array.  
<https://leetcode.com/problems/missing-element-in-sorted-array/>
<https://code.dennyzhang.com/missing-element-in-sorted-array/>
    <details>
        <summary>Quick Solution</summary>

    - Binary search
    - If the missing no falls in left half, search the missing no in left half. If it falls in right half,
      change the no of missing no to-be-searched by how many missing nos are gone in left half.
    - At any point of time, missing_nos_in_range = highest_value - lowest_value + 1 - range_size;

    </details>

8. Given n sorted lists, merge them and return single sorted merged list.  
<https://leetcode.com/problems/merge-k-sorted-lists/>
    <details>
        <summary>Quick Solution</summary>

    - One solution is to use min heap to keep track of minimum out of each head of list.
    - Keep incrementing head of lists which is added to final result list.
    - Second solution is to build on mergeSort which works on 2 lists.
    - If there are more than 2 lists, divide the no of lists in half and apply mergeSort. Do this step recursively.

    </details>

9. Given `n` and `k` such that `1 <= k < n`, return an array with values 1 to n such that the number of distinct
   differences between adjacent numbers is k.  
<https://leetcode.com/problems/beautiful-arrangement-ii/>
    <details>
        <summary>Quick Solution</summary>

    - If k = 1, return numbers in increasing order from 1 to n.
    - Keep 2 variables pointing to 1 and n, lets say i = 1, j = n.
    - while k != 1, alternatively push i/j to result array. Increment i if i is pushed/ decrement j if j is pushed.
      Reduce k.
    - Do step 1 when k reaches 1.

    </details>

10. Given an array `sum`, and 2 sums `sumA` and `sumB`, return 2 equal length arrays `A` and `B` consisting of only
    `0, 1` such that total sum of each array is equal to `sumA` and `sumB` respectively and `A[i]` + `B[i]` = `sum[i]`  
    <https://leetcode.com/problems/reconstruct-a-2-row-binary-matrix/>
    - Follow up: What if instead of filling up with just 0, 1, you could fill with numbers `1 to k`?

    <details>
        <summary>Quick Solution</summary>

    - At each index `i`, if `sum[i] == 2`, fill up `1` in both arrays `A` and `B`, and reduce `sumA` and `sumB` by 1.
    - If `sum[i] == 0`, fill up `0` in both arrays `A` and `B`.
    - if `sum[i] == 1`, fill up `1` in the array which has higher remaining sum.
    - at the end, check if sumA and sumB is zero.

    - TODO: Work out follow up question solution.

    </summary>

11. Given an array of non-negative integers `nums`, each element in the array represents your maximum jump length at  
    that position. Determine if you can reach the end of the array.  
<https://leetcode.com/problems/jump-game/>
    - Follow up: Assume input is such that you can always reach the end, return the minimum no of jumps.  
      <https://leetcode.com/problems/jump-game-ii/>
    <details>
        <summary>Quick Solution</summary>

    - Start with `reach = 0`, meaning I can reach 0th index always.
    - Run loop starting from 0 upto `reach`.
    - Update `reach` to be maximum of `(i + nums[i])`, `reach`.
    - If `reach` >= size of array, then you can reach the end, otherwise return `false`.
    - Followup Solution:
        - Keep track of what is the farthest I could go if I took a jump from any node seen till now, lets call this `farthest`.
        - Keep track of what is the farthest I could go if I just stuck with the first index, lets call this `currentFarthest`.
        - For each number in array, do the following:
            - Update `farthest` to max of `(farthest, i + nums[i])`.
            - If `current_index = currentFarthest`, i.e. this is the last index I could reach if I stick with my original  
            jump position. I'm now forced to take a jump. Set `no-of-jumps++`, and `currentFarthest = farthest`.
            - Return `no-of-jumps`.

     </details>

12. Given a coordinate `(sr, sc)` representing the starting pixel (row and column) of the flood fill, and a pixel value  
    `newColor`, "flood fill" the image.  
<https://leetcode.com/problems/flood-fill/>
    <details>
        <summary>Quick Solution</summary>

    - Starting from given pixel, do a dfs to neighboring nodes (below step 2).
    - If current node has the original Color, change it to newColor and check for its neighboring nodes.

    </details>

13. Given a string `s`, find the length of the longest substring without repeating chars.  
<https://leetcode.com/problems/longest-substring-without-repeating-characters/>
    <details>
        <summary>Quick Solution</summary>

    - Maintain an hash for each character. Value of hash tells when was the last time I saw this character.
    - Do the following for each character in the input string:
        - The `lowerbound` of our unique-char-substring would be max of `(current_lowerbound, last_time_I_saw_this_char)`.
        - Update `last_time_I_saw_this_char` to `current Index`.
        - Update `longestLength` as max of `(current longestLength, current_index - lowerBound + 1)`.
    - Return `longestLength`.

    </details>

14. Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest
    sum and return its sum.  
<https://leetcode.com/problems/maximum-subarray/>
    <details>
        <summary>Quick Summary</summary>

    - Kadane's algorithm
    - Traverse the array from left to right.
    - For each element, either the maximum sum subarray starts from this location, or it extends the current running max sum subarray.
      i.e. `may-be-longest = max(num[i], may-be-longest + num[i])`
    - This new `may-be-longest` can be the maximum sum subarray. `actual-longest = max(may-be-longest, actual-longest)`

    </details>

15. Implement the Trie class:  
    - `Trie()` Initializes the trie object.
    - `void insert(String word)` Inserts the string word into the trie.
    - `boolean search(String word)` Returns true if the string word is in the trie (i.e., was inserted before), and  
      false otherwise.
    - `boolean startsWith(String prefix)` Returns true if there is a previously inserted string word that has the  
      prefix prefix, and false otherwise.  
<https://leetcode.com/problems/implement-trie-prefix-tree/>
    <details>
        <summary>Quick Summary</summary>

    - Create a Node with 26 next pointers and a bool to denote whether some word ends at this.
    - When inserting, go down the 26 pointers for each char of input array, creating new nodes if need be. Mark the last
      pointer to denotes some word ends there.
    - For searching, for each character in input array, go down the 26 pointers. If you cannot go down, return false.  
      If all the chars are traversed but the last node is not marked as end, then return false.
    - For prefix, same as above but if you could traverse all the chars of input, return true.

    </details>

16. Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should  
    be set to `NULL`.  
<https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/>
    <details>
        <summary>Quick Summary</summary>

    - Do a `node-right-left` (reverse pre-order) traversal.
    - For each node, link up its children.
    - Find a next node whose at least one child is alive.
    - Link up right most child to leftmost child of next.
    - Recursively continue step 2-4 for right child, then left child.

    Other solution is to use some extra data structure:  
    - Do level order traversal.
    - Maintain 2 queues, one for current level, another for next level.
    - Traverse each queue, for each node push its children to next queue, and link up this current queue elements. Don't
      push `null` pointers to queue.
    - Swap current queue with next level queue when current queue is empty, and clear next level queue.
    - Do step 3, 4 till both queues are empty.

    </details>

17. Find median of running stream of numbers.  
<https://leetcode.com/problems/find-median-from-data-stream/>
    <details>
        <summary>Quick Summary</summary>

    - Multiple ways to solve this problem.
    - Idea is to keep `O(1)` access to nos which can be median.
    - For each incoming number, it would either be left of median, or right of current median.
    - Assume you use heaps to maintain left subarray and right subarray, take one `min_heap` and another `max_heap`.
    - So, aim would be to keep median numbers at top of heap.
    - If the current number is less than top of `min heap`, push it to `max heap`, otherwise push the new element
      to `min heap`.
    - Rebalance the heaps if one heap size > other heap size by 1.
    - At any point if you want to return median, if heap sizes are same, return half of sum of top elements.
      Otherwise, return the top of larger heap.

    </details>

18. Given the root of a binary tree, determine if it is a valid binary search tree.  
<https://leetcode.com/problems/validate-binary-search-tree/>  
    <details>
        <summary>Quick Summary</summary>

    - Idea is to limit the range of values each node is allowed to take, and as soon as some node violates  this limit,
      return `false`.
    - Begin with `-inf` to `+inf` range as min and max for root.
    - When validating left subtree, limit the range to `min` to `root->val`.
    - When validating right subtree, limit the range to `root->val` to `max`.
    - Return `false` if any of the subtree violates the conditions.
  
    </details>  

19. Given an `m X n` matrix, return all the elements of the matrix in spiral order.  
<https://leetcode.com/problems/spiral-matrix/>  
    <details>
        <summary>Quick Summary</summary>

    - Idea is to traverse in spiral order, and updating the limits of row and columns as and when you reach the edge of
      current limits.
    - Keep track of what is the movement you are currently doing, and can you continue doing that movement.
    - If you hit the right limit, you should change your movement to down, and reduce right limit by one.
    - If you hit the down limit, you should change your movement to left, and reduce down limit by one.
    - If you hit the left limit, you should change your movement to up, and increase the left limit by one.
    - If you hit the up limit, you should change your movement to right, and increase the up limit by one.
    - And so on. Do this until you can do some movement.

    </details>

20. Given a binary tree, return the boundary of the tree in anti-clockwise direction starting from root.  
<https://leetcode.com/problems/boundary-of-binary-tree/>  
<https://www.lintcode.com/problem/boundary-of-binary-tree/>  
    <details>
        <summary>Quick Summary</summary>

    - Plain DFS.
    - Find left nodes of the tree(top-down), then leaves(left-right), and then right(bottom-up).
    - When traversing left nodes, if some node does not have a left node, go to its right.
    - When traversing right nodes, if some node does not have a right node, go it its left.

    </details>

21. Given an integer `n` representing the total number of bits in the code, return any sequence of gray code of `n` bits.  
<https://leetcode.com/problems/gray-code/>
    <details>
        <summary>Quick Summary</summary>

    - Trick question.
    - Observe the pattern: For 1 bit, the result is `[0, 1]`. For 2 bits, the result is `[00, 01, 11, 10]`, viz.  
      `[0 + [0, 1], 1 + reverse([0, 1])]`. For 3 bits, the result is `[000, 001, 011, 010, 110, 111, 101, 100]`, viz.,  
      `[0 + [output of gray(2), 1 + reverse(gray(2)]`.
    - In effect, the recursive solution is find the gray code of n-1 bits. Push grey(n-1) to result. Then push `2^n +  
      reverse(gray(n-1))` to result.
    - Base condition is `gray(1) = [0, 1]`.

    </details>

22. You are given coordinates of n stones on a 2D plane. A stone can be removed if it shares either the same row or  
    same column as another stone. Return the maximum number of stones that can be removed.  
<https://leetcode.com/problems/most-stones-removed-with-same-row-or-column/>  
    <details>
        <summary>Quick Summary</summary>

    - Problem fits into template union-find algorithm.
    - We call a connected graph as an island.
    - One island must have at least one stone left.
    - The maximum stones can be removed = `total stones - total islands`.
    - Trick to treat 2D coordinates as a point in 1D plane:
        - Question has given that maximum value of coordinate can be 10000. So, treat `y` coordinate as point beyond 10000.
        - So, `x` coordinate is as is. But `y` coordinate is `11000(some no greater than 10000) + y`.
    - Now, link each x with its corresponding y, using `union-find` algorithm.
    - At the end, return `no_of_stones - no_of_connected_components`.

    </details>

23. You are given an array of `obstacles` of length `n+1`, where each obstacle ranges between 0-3,  
    0 - There is no obstacle  
    1,2,3 - There is obstacle on ith row.  
    The frog starts in lane 2. Return the minimum no of side jumps the frog needs, to reach any lane at point `n`.  
<https://leetcode.com/problems/minimum-sideway-jumps/>
    <details>
        <summary>Quick Summary</summary>

    - DP question.
    - Maintain a `min_jump` counter for each row, begin with {1, 0, 1}.
    - For each entry in obstacles array, check the following:
        - if kth row has obstacle, set `min_jump[k] = inf`
        - For each point which does not have obstacle, update `min_jump[i] = min(min_jump[i], min(min_jump[i+1], min_jump[i+2]) + 1)`
    - Return min of `min_jump`.

    </details>

24. Given an integer array `nums` and an integer `k`, return `true` if it is possible to divide this array into `k`  
    non-empty subsets whose subs are all equal.  
<https://leetcode.com/problems/partition-to-k-equal-sum-subsets/>
    <details>
        <summary>Quick Summary</summary>

    - DP. Try all subsets linearly and see if you've found k subsets.
    - NPC problem.
    - Maintain a bool `picked` array and `subsetSum` array.
    - For each unpicked num, mark it picked, push it to `subsetSum` array if possible(`subsetSub + num < targetsum`).  
      Otherwise, try the same with next element after marking current element unpicked, and removing it from current `subsetSum` index.
    - Recursively check if it is possible to push elements to some index of `subsetSum`.
    - If it is possible, return `true`, else `false`.

    </details>

25. You are given an array of `prerequisites` indicating which course must be taken before another. Return true if you  
    can take all the courses.  
<https://leetcode.com/problems/course-schedule/>  
    <details>
        <summary>Quick Summary</summary>

    - Basically, topological sorting question.
    - Create a dependency graph. And traverse it in dfs manner. If there is a loop, return false, else return true.

    </details>

26. You are given a vector of nums denoting type of fruit, and 2 baskets. You have to return what is the maximum no  
    of fruits you can pick, subjected to following conditions:
    - Each bucket can have only one type of fruit.
    - Once you start picking, you cannot skip over some index i, and pick some index j, for some j > i.  
<https://leetcode.com/problems/fruit-into-baskets/>  
    <details>
        <summary>Quick Summary</summary>

    - 2 pointer problem
    - Maintain a map (type_of_fruit->count) for each type of fruit you've picked.
    - Maintain a pointer j denoting the last element which is removed from map, inited to -1.
    - For each ith num in nums array, if the size of map > 2, keep incrementing j, and decrement the count of type of fruit an num[j].
    - If the count is 0, remove it from map. Push this new ith fruit in your map.
    - At each step, keep track of maxLength (i-j).
    - return maxLength.

    </details>

27. You are given an integer array `nums`, and 2 players. Game starts with player 1. Each player can picks one element  
    from either beginning or end, adds the number to its sum. Player with higher sum wins. Return whether player 1 can  
    win the game or not.  
<https://leetcode.com/problems/predict-the-winner/>  
    <details>
        <summary>Quick Summary</summary>

    - Min-max problem
    - At each decision, try 2 paths for A. Either pick from beginning and see if you win. Or pick from last and see
      if you win.
    - For B, try to win via both paths. Pick from beginning and try to win. And pick from end and try to win.
    - After each pick, let other player pick.
    - DP solution:
        - `dp(i, j) = max(nums[i] - dp(i+1, j), nums[j] - dp[i[j-1])`
        - Intuition is, you are adding `nums[i](or nums[j])` but will be losing out on `dp(i+1, j) (or dp[i][j-1])`.
        - return `dp[0][size] >= 0` if you want to find out if player 1 won., `dp[1][size] >= 0` if player 2 won.
    </details>

28. Given a string `s` containing only '`(`', '`)`' and '`*`'(can be treated as one '`(`' , '`)`' or empty string), return `true`  
    if `s` is valid.  
<https://leetcode.com/problems/valid-parenthesis-string/>  
    <details>
        <summary>Quick Summary</summary>

    - Try considering all * as close parenthesis, see if you close less than you open. If not, return false.
    - If 1 passes, from end of string, try considering all * as open parenthesis, and see if you have less close than  
      open. Return false if not.
    - Return true if you passed 2.  

    Another solution:
    - Maintain a range of minimum-maximum open parenthesis.
    - Lower limit of `minCount = 0` for following ops:
    - Do the following:
        - For each open parenthesis, increase `maxCount`, `minCount`.
        - For each close parenthesis, decrease `maxCount`, `minCount`.
        - For each *, increase `maxCount`, decrease `minCount`.
        - If at any point, `maxCount < 0`, return `false`.
    </details>

29. You are given a `pattern`, and a set of words. For each word in set of words, return `true`, if you can fit in characters  
    in `pattern`, and make it equal to word, subjected to condition that you cannot fit caps characters in `pattern`.  
<https://leetcode.com/problems/camelcase-matching/>  
    <details>
        <summary>Quick Summary</summary>

    - Greedy approach
    - For each char in word, if it matches currentChar of pattern, go ahead.
    - If current char in word is a caps char, but it does not match the current char of pattern, return false.
    - Do 2, 3 for each word.

    </details>

30. Given string num representing a non-negative integer `num`, and an integer `k`, return the smallest possible integer after removing k digits from  
    `num`.  
<https://leetcode.com/problems/remove-k-digits/>
    <details>
        <summary>Quick Summary</summary>

    - Traverse numbers from left to right, and look for a dip (num[i] < num[j], i > j).
    - Remove this number. Continue forward until you've removed k elements.
    - Idea is, lets say given number is `xxxabxxxx`, if a < b, removing a doesn't make much sense because `xxxbxxxx` would be greater than  
      `xxxaxxxx`, but this doesn't hold when a > b. Then it makes sense to remove `a` first.
    - Also, if the number is `xabxxxcdx` and `a < b` and `c < d`, it makes sense to remove `a` before `c` because `xbxxcdx` would be smaller  
      than `xabxxdx`.

    </details>

31. Given an array of integers `nums` and an integer `targetSum`, return the total number of continuous sumarrays whose sum equals to `targetSum`.  
<https://leetcode.com/problems/subarray-sum-equals-k/>
    <details>
        <summary>Quick Summary</summary>

    - If you maintain a prefix sum, its easy to see that `sum(ith index to jth index), sum[i,j] = sum(0, j) - sum(0, i-1)`.
    - So problem reduces to, once you've calculated prefix sum array, traverse over it to find all i, j such that  
      `sum(i, j) == targetSum`.
    - Alternatively, you can also maintain a hash which tells how many times it has seen this sum till now, and maintain a running sum (which is  
      nothing but sum[0, i-1]).
    - In your hash, look for `sum - targetSum`, if it is present, add it to count. This is because from `1`, we identified want `sum(0, j) - sum(0, i-1) == targetSum`,  
      and we saved `sum(0, i-1)` in our hash. So, we just check `sum(0, j) - targetSum` is there in hash or not.

    </details>

32. You are given 2 arrays, A and B, denoting dominos numbers. Find the minimum no of swaps between A(i) and B(i), such that either A has all  
    same numbers, or B has all same numbers.  
<https://leetcode.com/problems/minimum-domino-rotations-for-equal-row/>
    <details>
        <summary>Quick Summary</summary>

    - Create a set of first numbers of A and B.
    - For each of the next numbers of A and B, create another set.
    - Intersect this hash with original set. If the intersection is empty, return -1. If not, update original set with intersection set.
    - Idea is this, we want at least one of the initial numbers to be present across the 2 arrays.
    - Another way to solve this, first assume A[0] should be the number, and find the number of swaps as you go along the 2 arrays.
    - Next assume B[0] should be the number, and find the swaps.
    - Return minimum(ASwaps, BSwaps).

    </details>

33. Given the `root` of a binary tree, return the maximum path sum of any path (need not include root).  
<https://leetcode.com/problems/binary-tree-maximum-path-sum/>
    <details>
        <summary>Quick Summary</summary>

    - Maintain 2 variables, one of which tell what is the max sum in left/right subtree. Another which tells what is the maximum path sum  
      if you include root.
    - Find the maximum path sum in left subtree.
    - Find the maximum path sum in right subtree.
    - Update both variables accordingly.
    - `left = func(root->left, maxSum)`
    - `right = func(root->right, maxSum)`
    - `current = root->val + left + right`
    - `maxSum = max(maxSum, current)`
    - `maxSumPassingThroughRoot = root->val + max(left, right)`

    </details>

34. Given a linked list, return an array of next greater element corresponding to each node of the list.  
    If there is not next greater element, return 0 for that element.  
<https://leetcode.com/problems/next-greater-node-in-linked-list/>
    <details>
        <summary>Quick Summary</summary>

    - Keep a stack to maintain for which nodes next_greater is yet to be found.
    - If the current element is greater that the top of stack, pop elements from stack and set their next_greater to this current element.
    - At the end, for each element in stack, set their max_greater to 0.

    </details>

35. A company is planning to interview 2n people. Given the array costs where `costs[i] = [aCosti, bCosti]`,  
    the cost of flying the `ith` person to city `a` is `aCosti`, and the cost of flying the `ith` person to  
    city `b` is `bCosti`.
    Return the minimum cost to fly every person to a city such that exactly n people arrive in each city.  
<https://leetcode.com/problems/two-city-scheduling/>
    <details>
        <summary>Quick Summary</summary>

    - Greedy approach.
    - Create a max heap of difference of cost of visiting city `A` and that of `B`. Idea is, if the cost of visiting one city is way greater than  
      that of visiting other, we would want to ignore costlier city for this person.
    - Now, pop elements from heap, and try assigning the city to this person where the cost is low. Keep track of how many people have been sent  
      to city A vs city B. If you've already sent n people to one city, all the next people should be sent to other city.

    </details>

36. Given a string `s` and an integer `k`. You should construct `k` non-empty palindrome strings using all the characters in `s`.  
    Return `True` if you can use all the characters in `s` to construct `k` palindrome strings or `False` otherwise.  
<https://leetcode.com/problems/construct-k-palindrome-strings/>  
    <details>
        <summary>Quick Summary</summary>

    - Count the no of odd count characters.
    - Check if they are less or equal to `k`.
    </details>

37. Given an integer array `nums` and two integers `k` and `t`, return `true` if there are two distinct indices `i` and `j` in the array such that  
    `abs(nums[i] - nums[j]) <= t` and `abs(i - j) <= k`.  
<https://leetcode.com/problems/contains-duplicate-iii/>  
    <details>
    <summary>Quick Summary</summary>

    - Keep a `k` sized set(ordered).
    - For each incoming number `num[i]`, remove the oldest element `(i - k - 1)` from the set when the set has more than `k` elements.
    - Find the greatest smaller number than `nums[i] - t`.
    - If the number in step `3` is within t distance of nums[i], return true. Otherwise put this number in set and continue.
    </details>

38. Given an integer array `flowerbed` containing `0's` and `1's`, where 0 means empty and 1 means not empty, and an integer `n`, return if `n`  
    new flowers can be planted in the `flowerbed` such that no 2 flowers are adjacent when planted.  
<https://leetcode.com/problems/can-place-flowers/>
    <details>
        <summary>Quick Summary</summary>

    - For each index, check if neighbors have flower. If not, place it. Check for boundary conditions placements
    - Continue doing so until you've placed `n` flowers. If you've reached the end of `flowerbed` without placing `n` flowers, return `false`.
    </details>

39. Given a string consisting of parenthesis and integers, denoting tree in pre-order, return a tree corresponding to the string.  
<https://leetcode.com/problems/construct-binary-tree-from-string/>  
<https://www.lintcode.com/problem/construct-binary-tree-from-string/>  
    <details>
        <summary>Quick Summary</summary>

    - Read the string until you encounter '('.
    - Create root with string encountered till now.
    - In the remaining string, find the matching ')'. From this substring, create the left subtree of the   current root. (steps 1-4)
    - From the remaining string, create the right subtree of the current root. (steps 1-4)
    - Return the root.
    </details>

40. You have a browser of one tab where you start on the `homepage` and you can visit another `url`, get back in the history number of `steps` or move forward in the history number of `steps`.  
Implement the BrowserHistory class:  

    - `BrowserHistory(string homepage)` Initializes the object with the `homepage` of the browser.
    - `void visit(string url)` Visits `url` from the current page. It clears up all the forward history.
    - `string back(int steps)` Move `steps` back in history. If you can only return `x` steps in the history and `steps > x`, you will return only x steps. Return the current `url` after moving back in history at most `steps`.
    - `string forward(int steps)` Move steps forward in history. If you can only forward `x` steps in the history and `steps > x`, you will forward only `x` steps. Return the current `url` after forwarding in history at most `steps`.  
<https://leetcode.com/problems/design-browser-history/>  

    <details>
        <summary>Quick Summary</summary>

    - Can be done with either 2 stacks or 1 list.
    - For 2 stack solution, keep 2 stacks, `past` and `future`.
    - In initialization, initialize `past` with incoming `url` and clear the `future`.
    - In visit, initialize `past` with incoming `url` and clear `future`.
    - In back, pop from `back` and push it to `future`. Make sure you never empty the past stack. Return the top of the stack.
    - In forward, pop from `future` and push it to `back`. Return top of `back` stack.

    </details>

41. Given an `m x n` binary matrix filled with `0's` and `1's`, find the largest square containing only `1's` and return its area.  
<https://leetcode.com/problems/maximal-square/>  
    <details>
        <summary>Quick Summary</summary>

    - DP problem
    - Initialize a matrix `dp` such that dp[i][j] = 1 iff matrix[i][j] = '1'.
    - For each i, j of matrix, do the following:
        - if (matrix[i][j] == '1'), then
            - dp[i][j] = 1 + min(value above, value before, and value left-diagonally up.).
            - Also, keep track of max value across all dp[i][j]
    - Return square of max_value.
    </details>
