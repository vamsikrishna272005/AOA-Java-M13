
# EX 3E Generate Permutations using Backtracking  Approach.
## DATE: 16-08-2026
## AIM:
To write a Java program to for given constraints.
Given an array nums of distinct integers, return all the possible Permutation. You can return the answer in any order.
Example 1:
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
For example:
## Algorithm
1. Start  
2. Read the input array `nums` from the user.  
3. Initialize an empty list `ans` to store all generated permutations.  
4. Call the recursive function `backtrack(curr, ans, nums)` where:  
   - `curr` is a list storing the current permutation being built.  
   - `ans` stores all valid permutations found so far.  
5. In `backtrack()` function:  
   - **Base case:**  
     - If the size of `curr` equals the length of `nums`, a complete permutation is formed.  
     - Add a **copy** of `curr` to the result list `ans` and return.  
   - **Recursive case:**  
     - Iterate through each element `num` in `nums`.  
     - If `num` is already in `curr`, skip it (since each number can be used only once).  
     - Add `num` to `curr` (choose step).  
     - Recursively call `backtrack(curr, ans, nums)` to build the next position.  
     - After returning, remove the last added number from `curr` (unchoose step / backtrack).  
6. After all recursive calls complete, `ans` contains all possible permutations.  
7. Print the list of permutations.  
8. End  
   

## Program:
```
/*
Developed by: Vamsi Krishna G
Register Number: 212223220120 
*/
import java.util.*;

public class Solution {

    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        backtrack(new ArrayList<>(), ans, nums);
        return ans;
    }

    public void backtrack(List<Integer> curr, List<List<Integer>> ans, int[] nums) {
        // Base case: if permutation complete, add to result
        if (curr.size() == nums.length) {
            ans.add(new ArrayList<>(curr));
            return;
        }

        // Try each number not already in current list
        for (int num : nums) {
            if (curr.contains(num)) continue; // skip used numbers
            curr.add(num);                   // choose
            backtrack(curr, ans, nums);      // explore
            curr.remove(curr.size() - 1);    // unchoose (backtrack)
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String inputLine = scanner.nextLine().trim();
        inputLine = inputLine.replaceAll(".*\\[|\\].*", ""); 
        String[] parts = inputLine.split(",");

        int[] nums = new int[parts.length];
        for (int i = 0; i < parts.length; i++) {
            nums[i] = Integer.parseInt(parts[i].trim());
        }

        Solution solution = new Solution();
        List<List<Integer>> permutations = solution.permute(nums);
        System.out.println(permutations);
        scanner.close();
    }
}

```

## Output:

<img width="1279" height="353" alt="image" src="https://github.com/user-attachments/assets/2b5ba92b-e514-4180-96f7-f10557ea6e7a" />


## Result:
The program successfully implemented and the expected output is verified.
