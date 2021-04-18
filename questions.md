# Questions discussed

All the solution codes (in `C++`) can be accessed at appropriate difficulty folder [here](https://github.com/anuragtomer/practice_coding/tree/master/leetcode)
1. Given a node 'p' of BST, and root, return the inorder successor of 'p'. Note that there is no pointer to parent.  
https://www.lintcode.com/problem/inorder-successor-in-bst/     
    <details>
        <summary>Quick Solution</summary>

    - If given node has right child, return the left most child of right child of 'p'.
    - Otherwise, starting from root, push all the parents till 'p' in stack and pop till immediate 
      parent is successor (`p.val < parent.val`)

    </details>

2. Given a list of pair of `<take_off, landing>` time of flights, return the maximum no of flights that will be in air simultaneously.  
https://www.lintcode.com/problem/number-of-airplanes-in-the-sky/
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
https://leetcode.com/problems/ones-and-zeroes/
    <details>
        <summary>Quick Solution</summary>
    
    - DP problem (0-1 knapsack variant).
    - For each element of array, try to follow two paths. Either take this and see if at most 
      conditions are met or ignore current element and try to fulfill conditions from other elements.

    </details>
    
4. Given an array of positive numbers and a positive target, find minimum contiguous subarray whose sum is greater  
   than or equal to `target`.  
https://leetcode.com/problems/minimum-size-subarray-sum/
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
https://leetcode.com/problems/next-permutation/
    <details>
        <summary>Quick Solution</summary>
    
    - Starting from last to first, find first entry which is non-increasing.
    - Find smallest greater element than the value found in step `1`. Again do this from the end.
    - Swap elements from step `1` and step `2`.
    - Reverse the subarray after index from step `1`.

    </details>
    
6. Given 2 strings, find the minimum no of deletions you need to make such that resulting strings are same.  
https://leetcode.com/problems/delete-operation-for-two-strings/

    <details>
        <summary>Quick Solution</summary>
    
    - Modified LCS.
    - Find the longest common subsequence in 2 strings using DP.
    - return `size1 + size2 - 2*(lcs)`
    
    </details>
    
7. Given a sorted array A of unique numbers, find the k-th missing number starting from the leftmost number of the array.  
https://leetcode.com/problems/missing-element-in-sorted-array/
https://code.dennyzhang.com/missing-element-in-sorted-array/
    <details>
        <summary>Quick Solution</summary>
        
    - Binary search
    - If the missing no falls in left half, search the missing no in left half. If it falls in right half,
      change the no of missing no to-be-searched by how many missing nos are gone in left half.
    - At any point of time, missing_nos_in_range = highest_value - lowest_value + 1 - range_size;

    </details>
    
8. Given n sorted lists, merge them and return single sorted merged list.  
https://leetcode.com/problems/merge-k-sorted-lists/
    <details>
        <summary>Quick Solution</summary>
        
    - One solution is to use min heap to keep track of minimum out of each head of list.
    - Keep incrementing head of lists which is added to final result list.
    - Second solution is to build on mergeSort which works on 2 lists.
    - If there are more than 2 lists, divide the no of lists in half and apply mergeSort. Do this step recursively.
    
    </details>
    
9. Given `n` and `k` such that `1 <= k < n`, return an array with values 1 to n such that the number of distinct
   differences between adjacent numbers is k.  
https://leetcode.com/problems/beautiful-arrangement-ii/
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
    https://leetcode.com/problems/reconstruct-a-2-row-binary-matrix/
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
https://leetcode.com/problems/jump-game/
    
    <details>
        <summary>Quick Solution</summary>
        
    - Start with `reach = 0`, meaning I can reach 0th index always.
    - Run loop starting from 0 upto `reach`.
    - Update `reach` to be maximum of `(i + nums[i])`, `reach`.
    - If `reach` >= size of array, then you can reach the end, otherwise return `false`.
    
    </summary>
    
- Follow up: Assume input is such that you can always reach the end, return the minimum no of jumps.  
      https://leetcode.com/problems/jump-game-ii/
      
    <details>
        <summary>Quick Solution</summary>
        
    - Keep track of what is the farthest I could go if I took a jump from any node seen till now, lets call this `farthest`.
    - Keep track of what is the farthest I could go if I just stuck with the first index, lets call this `currentFarthest`.
    - For each number in array, do the following:
        - Update `farthest` to max of `(farthest, i + nums[i])`.
        - If `current_index = currentFarthest`, i.e. this is the last index I could reach if I stick with my original 
          jump position. I'm now forced to take a jump. Set `no-of-jumps++`, and `currentFarthest = farthest`.
    - Return `no-of-jumps`.
     
     </summary>

12. Given a coordinate `(sr, sc)` representing the starting pixel (row and column) of the flood fill, and a pixel value 
    `newColor`, "flood fill" the image.  
https://leetcode.com/problems/flood-fill/

    <details>
        <summary>Quick Solution</summary>
        
    - Starting from given pixel, do a dfs to neighboring nodes (below step 2).
    - If current node has the original Color, change it to newColor and check for its neighboring nodes.
    
    </details>

13. Given a string `s`, find the length of the longest substring without repeating chars.  
https://leetcode.com/problems/longest-substring-without-repeating-characters/

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
https://leetcode.com/problems/maximum-subarray/

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
https://leetcode.com/problems/implement-trie-prefix-tree/

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
https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/

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
https://leetcode.com/problems/find-median-from-data-stream/

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
https://leetcode.com/problems/validate-binary-search-tree/  

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
https://leetcode.com/problems/spiral-matrix/  

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
https://leetcode.com/problems/boundary-of-binary-tree/  
https://www.lintcode.com/problem/boundary-of-binary-tree/  

    <details>
        <summary>Quick Summary</summary>
        
    - Plain DFS.
    - Find left nodes of the tree(top-down), then leaves(left-right), and then right(bottom-up).
    - When traversing left nodes, if some node does not have a left node, go to its right.
    - When traversing right nodes, if some node does not have a right node, go it its left.
    
    </details>

21. Given an integer `n` representing the total number of bits in the code, return any sequence of gray code of `n` bits.  
https://leetcode.com/problems/gray-code/

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
https://leetcode.com/problems/most-stones-removed-with-same-row-or-column/  

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
https://leetcode.com/problems/minimum-sideway-jumps/

    <details>
        <summary>Quick Summary</summary>
        
    - DP question.
    - Maintain a `min_jump` counter for each row, begin with {1, 0, 1}.
    - For each entry in obstacles array, check the following:
        - if kth row has obstacle, set `min_jump[k] = inf`
        - For each point which does not have obstacle, update `min_jump[i] = min(min_jump[i], min(min_jump[i+1], min_jump[i+2]) + 1)`
    - Return min of `min_jump`.
    
    </details>
