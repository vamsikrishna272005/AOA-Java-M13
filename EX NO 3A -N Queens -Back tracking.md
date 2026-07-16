
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
