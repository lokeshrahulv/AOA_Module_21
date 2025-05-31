# AOA_Module_21
# EX 3A Knight Tour & Count Path
## AIM:
To write a python program to find minimum steps to reach to specific cell in minimum moves by knight


## Algorithm
1. Use Breadth-First Search (BFS) starting from the knight’s position.
2. Enqueue the starting position with distance 0 and mark it as visited.
3. At each step, dequeue a cell and check if it is the target position.
4. If not, move the knight in all 8 possible moves and enqueue valid, unvisited cells with dist + 1.
5. Repeat until the target is reached, and return the number of steps (distance).
   
## Program:
```
/*
Program to implement to find minimum steps to reach to specific cell in minimum moves by knight.
Developed by: LOKESH RAHUL V V
Register Number: 212222100024
*/
```
```python
class cell:
     
    def __init__(self, x = 0, y = 0, dist = 0):
        self.x = x
        self.y = y
        self.dist = dist

def isInside(x, y, N):
    if (x >= 1 and x <= N and
        y >= 1 and y <= N):
        return True
    return False
def minStepToReachTarget(knightpos,
                         targetpos, N):
    # add your code here
    #Start here
    dx = [2, 2, -2, -2, 1, 1, -1, -1]
    dy = [1, -1, 1, -1, 2, -2, 2, -2]
    queue = []
    queue.append(cell(knightpos[0], knightpos[1], 0))
    visited = [[False for i in range(N + 1)] for j in range(N + 1)]
    visited[knightpos[0]][knightpos[1]] = True
    while(len(queue) > 0):
        t = queue[0]
        queue.pop(0)
        if(t.x == targetpos[0] and
           t.y == targetpos[1]):
            return t.dist
        for i in range(8):
            x = t.x + dx[i]
            y = t.y + dy[i]
            if(isInside(x, y, N) and not visited[x][y]):
                visited[x][y] = True
                queue.append(cell(x, y, t.dist + 1))
    
if __name__=='__main__':
    N = 30
    knightpos = [1, 1]
    targetpos = [30, 30]
    print(minStepToReachTarget(knightpos,
                               targetpos, N))
```

## Output:
![image](https://github.com/user-attachments/assets/748b3a6e-6c75-4c90-ac55-22b032a8dd34)





## Result:
The program executed successfully, and the minimum number of steps for the knight to reach the target was calculated.
# EX 3B Hamiltonian Circuit Problem
## AIM:
To write a python program to check whether Hamiltonian path exits in the given graph.

## Algorithm
1. Start from each vertex and mark it as visited.
2. Try visiting all other vertices one by one using edges.
3. Use dynamic programming to remember visited sets and paths.
4. If you can visit all vertices exactly once, a Hamiltonian path exists.
5. If no such path is found after checking all options, return "NO".

## Program:
```
/*
Program to implement to check whether Hamiltonian path exits in the given graph.
Developed by:  LOKESH RAHUL V V
Register Number: 212222100024
*/
```
```python
def Hamiltonian_path(adj, N):
    dp = [[False for i in range(1 << N)] for j in range(N)]
    for i in range(N):
        dp[i][1 << i] = True
    for i in range(1 << N):
        for j in range(N):
            if ((i & (1 << j)) != 0):
 
                for k in range(N):
                    if ((i & (1 << k)) != 0 and
                             adj[k][j] == 1 and
                                     j != k and
                          dp[k][i ^ (1 << j)]):
                        dp[j][i] = True
                        break
    for i in range(N):
        if (dp[i][(1 << N) - 1]):
            return True
    return False
    #End here
    
adj = [ [ 0, 1, 1, 1, 0 ] ,
        [ 1, 0, 1, 0, 1 ],
        [ 1, 1, 0, 1, 1 ],
        [ 1, 0, 1, 0, 0 ] ]
 
N = len(adj)
 
if (Hamiltonian_path(adj, N)):
    print("YES")
else:
    print("NO")
```

## Output:
![image](https://github.com/user-attachments/assets/e87f6ef6-bb9b-4b5d-8dba-f98033c99d3c)





## Result:
The Hamiltonian path program executed successfully, and it determined whether a Hamiltonian path exists in the given graph.# EX 3C Sudoku Solver
## AIM:
To write a python program to find the solution of sudoku puzzle using Backtracking.


## Algorithm
1. Find the first empty cell (cell with 0) in the Sudoku board.
2. Try placing numbers 1 to 9 in that empty cell.
3. For each number, check if it is safe (valid) to place by row, column, and 3×3 box rules.
4. If safe, place the number and recursively attempt to fill the next empty cell.
5. If the board is completely filled without conflicts, print the solution.  

## Program:
```
/*
Program to implement to to find the solution of sudoku puzzle using Backtracking.
Developed by:  LOKESH RAHUL V V
Register Number: 212222100024
*/
```
```py
board = [
    [0, 0, 0, 8, 0, 0, 4, 0, 3],
    [2, 0, 0, 0, 0, 4, 8, 9, 0],
    [0, 9, 0, 0, 0, 0, 0, 0, 2],
    [0, 0, 0, 0, 2, 9, 0, 1, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 7, 0, 6, 5, 0, 0, 0, 0],
    [9, 0, 0, 0, 0, 0, 0, 8, 0],
    [0, 6, 2, 7, 0, 0, 0, 0, 1],
    [4, 0, 3, 0, 0, 6, 0, 0, 0]
]

def printBoard(board):
    for i in range(0, 9):
        for j in range(0, 9):
            print(board[i][j], end=" ")
        print()

def isPossible(board, row, col, val):
    for j in range(0, 9):
        if board[row][j] == val:
            return False

    for i in range(0, 9):
        if board[i][col] == val:
            return False

    startRow = (row // 3) * 3
    startCol = (col // 3) * 3
    for i in range(0, 3):
        for j in range(0, 3):
            if board[startRow+i][startCol+j] == val:
                return False
    return True

def solve():
    for i in range(0, 9):
        for j in range(0, 9):
            if board[i][j] == 0:
                for val in range(1, 10):
                    if isPossible(board, i, j, val):
                        board[i][j] = val
                        solve()
                        board[i][j] = 0
                return
    printBoard(board)
    #End here
solve()
```

## Output:
![image](https://github.com/user-attachments/assets/08287a84-a826-4de0-8a9d-e54467cfdb73)





## Result:
The Sudoku solver program executed successfully and found the solution for the given puzzle.# EX 3D Pattern Matching
## AIM:
To write a python program to implement pattern matching on the given string using Brute Force algorithm.



## Algorithm
1. Start checking each letter of s1 with the first letter of s
2. If letters match, keep checking the next letters.
3. If letters don't match, move one step forward in s1 and restart checking.
4. If all letters of s2 match, return the starting position.
5. If no match is found till the end, return 0.  

## Program:
```
/*
Program to implement the Pattern Matching.
Developed by:  LOKESH RAHUL V V
Register Number: 212222100024
*/
```
```py
def BF(s1,s2):
    i = 0
    j = 0
    while(i < len(s1) and j < len(s2)):
        if(s1[i] ==  s2[j]):
            i += 1
            j += 1
        else:
            i = i - j + 1
            j = 0
    if(j >= len(s2)):
        return i - len(s2)
    else:
        return 0
    #End here
if __name__ == "__main__":
    a1=input() 
    a2=input() 
    b=BF(a1,a2)
    print(b)
```

## Output:
![image](https://github.com/user-attachments/assets/a2f4fb17-09f0-4aab-9106-2705993bcb0a)





## Result:
The brute force substring search program executed successfully and returned the starting index of the match or 0 if no match was found.
