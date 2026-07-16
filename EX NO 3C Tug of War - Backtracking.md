
# EX 3C Tug of War problem - Backtracking.
## DATE:13-08-2026
## AIM:
To write a Java program to for given constraints.
Given an integer array nums, return true if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or false otherwise.
Example 1:
Input: Enter the number of elements: 4
Enter the elements of the array:
1 5 11 5
Output: true
Explanation: The array can be partitioned as [1, 5, 5] and [11].

Constraints:

1 <= nums.length <= 200
1 <= nums[i] <= 100

## Algorithm
1. Start  
2. Read the integer `n` — the number of elements in the array.  
3. Read `n` integers into the array `nums`.  
4. Compute the total sum of all elements:  
   - `totalSum = sum(nums)`  
5. If `totalSum` is **odd**, return `false` because it cannot be equally partitioned.  
6. Calculate the target subset sum:  
   - `target = totalSum / 2`  
7. Initialize a boolean array `dp[target + 1]` where `dp[i]` represents whether a subset sum of `i` is possible.  
   - Set `dp[0] = true` (base case: sum `0` is always achievable).  
8. For each element `num` in `nums`:  
   - Iterate `j` from `target` down to `num`.  
   - Update: `dp[j] = dp[j] || dp[j - num]`  
   - (This ensures we use each element only once per subset.)  
9. After processing all numbers, if `dp[target]` is `true`, print `true`; otherwise, print `false`.  
10. End  
  

## Program:
```
/*
Developed by: Vamsi Krishna G
Register Number: 212223220120 
*/
import java.util.Scanner;

public class Solution {

    public boolean canPartition(int[] nums) {
        int totalSum = 0;
        for (int num : nums) {
            totalSum += num;
        }

        // If total sum is odd, can't split equally
        if (totalSum % 2 != 0) return false;

        int target = totalSum / 2;
        boolean[] dp = new boolean[target + 1];
        dp[0] = true; // Base case: sum 0 is always possible

        // For each number, update dp array backward
        for (int num : nums) {
            for (int j = target; j >= num; j--) {
                dp[j] = dp[j] || dp[j - num];
            }
        }

        return dp[target];
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Solution sol = new Solution();

        //System.out.print("Enter the number of elements: ");
        int n = scanner.nextInt();

        int[] nums = new int[n];
       // System.out.println("Enter the elements of the array:");
        for (int i = 0; i < n; i++) {
            nums[i] = scanner.nextInt();
        }

        boolean canBePartitioned = sol.canPartition(nums);
        System.out.println(canBePartitioned);
    }
}

```

## Output:

<img width="726" height="381" alt="image" src="https://github.com/user-attachments/assets/4a848402-a5d7-49d0-9b7e-c8df325db96c" />


## Result:
The program successfully implemented and the expected output is verified.
