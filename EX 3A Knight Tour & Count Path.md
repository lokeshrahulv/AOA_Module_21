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
Developed by: ASHWIN KUMAR S
Register Number: 212222240013
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
