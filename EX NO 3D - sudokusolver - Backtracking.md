
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
