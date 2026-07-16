
# EX 3A N Queens Problem - Backtracking Approach.
## DATE: 10-08-2026
## AIM:
To Write a Java program for N queens using backtracking approach.
You are given an integer N. For a given N x N chessboard, find a way to place 'N' queens such that no queen can attack any other queen on the chessboard.
A queen can be attacked when it lies in the same row, column, or the same diagonal as any of the other queens. You have to print one such configuration.
Chess Board
<img width="241" height="209" alt="image" src="https://github.com/user-attachments/assets/96aacb61-4f34-423f-b324-5e34454e42b8" />


Note :

Get the input from the user for N . The value of N must be from 1 to 4

If solution exists Print a binary matrix as output that has 1s for the cells where queens are placed

If there is no solution to the problem  print  "Solution does not exist"

## Algorithm
1. Start  
2. Read the integer `N` — the size of the chessboard and the number of queens to be placed.  
3. Initialize an `N × N` chessboard with all cells set to `0`.  
4. Define a recursive function `solveNQUtil(board, col)` to place queens one column at a time:  
   - If `col >= N`, all queens are placed successfully → return `true`.  
   - For each row `i` in column `col`:  
     - Check if placing a queen at `(i, col)` is safe using the `isSafe()` function.  
     - If safe:  
       - Place a queen (`board[i][col] = 1`).  
       - Recursively call `solveNQUtil(board, col + 1)` to place the rest.  
       - If successful, return `true`.  
       - If not, backtrack (`board[i][col] = 0`).  
   - If no safe position is found in this column, return `false`.  
5. The `isSafe()` function checks if a queen can be placed at position `(row, col)` by verifying:  
   - No other queen exists in the same row on the left.  
   - No other queen exists in the upper-left diagonal.  
   - No other queen exists in the lower-left diagonal.  
6. If the recursive function returns `false`, print “Solution does not exist.”  
7. If successful, print the board configuration where `1` indicates a queen’s position.  
8. End  
   

## Program:
```
/*

Developed by: Vamsi Krishna G
Register Number:  212223220120
*/
import java.util.Scanner;

public class NQueens {
    static int N;

    static void printSolution(int[][] board) {
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                System.out.print(board[i][j] + " ");
            }
            System.out.println();
        }
    }

    static boolean isSafe(int[][] board, int row, int col) {
        for (int i = 0; i < col; i++)
            if (board[row][i] == 1)
                return false;

        for (int i = row, j = col; i >= 0 && j >= 0; i--, j--)
            if (board[i][j] == 1)
                return false;

        for (int i = row, j = col; i < N && j >= 0; i++, j--)
            if (board[i][j] == 1)
                return false;

        return true;
    }

    static boolean solveNQUtil(int[][] board, int col) {
        if (col >= N)
            return true;

        for (int i = 0; i < N; i++) {
            if (isSafe(board, i, col)) {
                board[i][col] = 1;

                if (solveNQUtil(board, col + 1))
                    return true;

                board[i][col] = 0;
            }
        }
        return false;
    }

    static boolean solveNQ() {
        int[][] board = new int[N][N];

        if (!solveNQUtil(board, 0)) {
            System.out.println("Solution does not exist");
            return false;
        }

        printSolution(board);
        return true;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        N = scanner.nextInt();
        solveNQ();
    }
}

```

## Output:

<img width="811" height="404" alt="image" src="https://github.com/user-attachments/assets/64584491-f648-4f9a-8803-0c1f5026f1ef" />


## Result:
The program successfully implemented and the ouput is verified. 


# EX 3B Rat in Maze- Backtracking 
## DATE:12-08-2026
## AIM:
To write a Java program to for given constraints.
here is a ball in a maze with empty spaces (represented as 0) and walls (represented as 1). The ball can go through the empty spaces by rolling up, down, left or right, but it won't stop rolling until hitting a wall. When the ball stops, it could choose the next direction.

Given the m x n maze, the ball's start position and the destination, where start = [startrow, startcol] and destination = [destinationrow, destinationcol], return true if the ball can stop at the destination, otherwise return false.

You may assume that the borders of the maze are all walls (see examples).
<img width="573" height="573" alt="image" src="https://github.com/user-attachments/assets/d6f1c054-cdc2-4bb3-9c55-512fb2cf0fb7" />
Input: maze = [[0,0,1,0,0],[0,0,0,0,0],[0,0,0,1,0],[1,1,0,1,1],[0,0,0,0,0]], start = [0,4], destination = [4,4]
Output: true
Explanation: One possible way is : left -> down -> left -> down -> right -> down -> right.


## Algorithm
1. Start  
2. Read the dimensions of the maze: `m` (rows) and `n` (columns).  
3. Read the maze as a 2D grid of size `m × n`, where:  
   - `0` represents an open path  
   - `1` represents a wall  
4. Read the starting position `start[]` and the destination position `destination[]`.  
5. Initialize a 2D boolean array `visit[m][n]` to track visited cells.  
6. Define a recursive function `dfs(m, n, maze, curr, destination, visit)` that:  
   - Returns `false` if the current cell is already visited.  
   - Returns `true` if the current cell equals the destination cell.  
   - Marks the current cell as visited.  
   - Defines four movement directions: up, down, left, right.  
   - For each direction:  
     - Move continuously (roll) in that direction until hitting a wall (`1`) or the boundary of the maze.  
     - Once stopped, recursively call `dfs()` from the stopping position.  
     - If any recursive call returns `true`, propagate success upward.  
7. In the `hasPath()` function:  
   - Initialize parameters and call the DFS function from the starting position.  
   - Return `true` if the destination can be reached, otherwise `false`.  
8. Print the result.  
9. End  
   

## Program:
```
/*
Developed by: Vamsi Krishna G
Register Number:  212223220120
*/
import java.util.*;

public class Main {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int m = sc.nextInt();
        int n = sc.nextInt();

        int[][] maze = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                maze[i][j] = sc.nextInt();
            }
        }

        int[] start = new int[]{sc.nextInt(), sc.nextInt()};
        int[] destination = new int[]{sc.nextInt(), sc.nextInt()};

        Solution sol = new Solution();
        boolean result = sol.hasPath(maze, start, destination);

        System.out.println(result);
    }
}

class Solution {

    public boolean dfs(int m, int n, int[][] maze, int[] curr, int[] destination, boolean[][] visit) {
        if (visit[curr[0]][curr[1]]) return false;
        if (curr[0] == destination[0] && curr[1] == destination[1]) return true;
        visit[curr[0]][curr[1]] = true;

        int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};

        for (int[] dir : dirs) {
            int x = curr[0];
            int y = curr[1];

            // roll until hitting a wall
            while (x + dir[0] >= 0 && x + dir[0] < m &&
                   y + dir[1] >= 0 && y + dir[1] < n &&
                   maze[x + dir[0]][y + dir[1]] == 0) {
                x += dir[0];
                y += dir[1];
            }

            if (dfs(m, n, maze, new int[]{x, y}, destination, visit)) {
                return true;
            }
        }

        return false;
    }

    public boolean hasPath(int[][] maze, int[] start, int[] destination) {
        int m = maze.length;
        int n = maze[0].length;
        boolean[][] visit = new boolean[m][n];
        return dfs(m, n, maze, start, destination, visit);
    }
}

```

## Output:
<img width="896" height="600" alt="image" src="https://github.com/user-attachments/assets/c5055299-923b-476d-a5df-4251b351c08f" />



## Result:
The program successfully implemented and the expected output is verified.


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


# EX 3D Sudoku solver - Backtracking.
## DATE: 14-08-2026
## AIM:
To write a Java program to solve a Sudoku puzzle by filling the empty cells.

For example:
<img width="357" height="322" alt="image" src="https://github.com/user-attachments/assets/334b8c39-d547-4743-aca0-de92e38bdd1c" />



## Algorithm
1. Start  
2. Read a 9×9 Sudoku board as input, where empty cells are represented by `0`.  
3. Define a function `isSafe(board, row, col, num)` that checks if a number `num` can be placed at position `(row, col)` without violating Sudoku rules:  
   - The number should not already exist in the same row.  
   - The number should not already exist in the same column.  
   - The number should not already exist in the same 3×3 subgrid.  
4. Define a recursive function `solveSudoku(board, row, col)` to fill the board:  
   - If `row == 9`, all rows are filled → return `true` (solution found).  
   - If `col == 9`, move to the next row by calling `solveSudoku(board, row + 1, 0)`.  
   - If the current cell is already filled (`board[row][col] != 0`), move to the next column.  
5. For an empty cell `(row, col)`:  
   - Try placing numbers `1` to `9` one by one.  
   - For each number, check if it is safe using `isSafe()`.  
   - If safe, place the number and recursively call `solveSudoku(board, row, col + 1)`.  
   - If the recursive call returns `true`, a valid solution is found → return `true`.  
   - Otherwise, reset the cell to `0` (backtrack) and try the next number.  
6. If no valid number can be placed, return `false` to backtrack further.  
7. If the function returns `true`, print the solved Sudoku board.  
8. If the function returns `false`, print "No solution exists."  
9. End  
  

## Program:
```
/*
Developed by: Vamsi Krishna G
Register Number:  212223220120
*/
import java.util.Scanner;

public class SudokuSolver {

    static boolean isSafe(int[][] board, int row, int col, int num) {
        for (int i = 0; i < 9; i++) {
            if (board[row][i] == num || board[i][col] == num)
                return false;
        }

        int startRow = row - row % 3;
        int startCol = col - col % 3;

        for (int i = 0; i < 3; i++)
            for (int j = 0; j < 3; j++)
                if (board[startRow + i][startCol + j] == num)
                    return false;

        return true;
    }

    static boolean solveSudoku(int[][] board, int row, int col) {
        if (row == 9)
            return true;

        if (col == 9)
            return solveSudoku(board, row + 1, 0);

        if (board[row][col] != 0)
            return solveSudoku(board, row, col + 1);

        for (int num = 1; num <= 9; num++) {
            if (isSafe(board, row, col, num)) {
                board[row][col] = num;
                if (solveSudoku(board, row, col + 1))
                    return true;
                board[row][col] = 0; // backtrack
            }
        }
        return false;
    }

    static void printBoard(int[][] board) {
        for (int[] row : board) {
            for (int val : row)
                System.out.print(val + " ");
            System.out.println();
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int[][] board = new int[9][9];

        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                board[i][j] = sc.nextInt();
            }
        }

        if (solveSudoku(board, 0, 0)) {
            System.out.println("Solved Sudoku:");
            printBoard(board);
        } else {
            System.out.println("No solution exists.");
        }

        sc.close();
    }
}

```

## Output:

<img width="1029" height="658" alt="image" src="https://github.com/user-attachments/assets/8835bd6c-b7b9-4d14-bdb9-2c30c03e7cb0" />


## Result:
The program successfully implemented and the expected output is verified.


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
