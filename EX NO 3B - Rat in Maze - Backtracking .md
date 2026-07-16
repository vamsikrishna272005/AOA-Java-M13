
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
