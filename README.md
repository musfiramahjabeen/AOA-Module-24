# AOA-Module-24
## Day 1 - CHERRY PICK UP PROBLEM
You are given a rows x cols matrix grid representing a field of cherries where grid[i][j] represents the number of cherries that you can collect from the (i, j) cell.

You have two robots that can collect cherries for you:

Robot #1 is located at the top-left corner (0, 0), and
Robot #2 is located at the top-right corner (0, cols - 1).
Return the maximum number of cherries collection using both robots by following the rules below:

From a cell (i, j), robots can move to cell (i + 1, j - 1), (i + 1, j), or (i + 1, j + 1).
When any robot passes through a cell, It picks up all cherries, and the cell becomes an empty cell.
When both robots stay in the same cell, only one takes the cherries.
Both robots cannot move outside of the grid at any moment.
Both robots should reach the bottom row in grid.
![image](https://github.com/user-attachments/assets/776622c6-7509-43ac-b015-e76e5ae4121f)

```py
class Solution(object):
    def cherryPickup(self, grid):
        ROW_NUM = len(grid)
        COL_NUM = len(grid[0])
        memo = [[[-1] * COL_NUM for _ in range(COL_NUM)] for _ in range(ROW_NUM)]
        def dp(i, j1, j2):
            if (i == ROW_NUM or j1 < 0 or j1 >= COL_NUM or j2 < 0 or j2 >= COL_NUM or grid[i][j1] == -1 or grid[i][j2] == -1):
                return 0
            if memo[i][j1][j2] != -1:
                return memo[i][j1][j2]

            cherries = grid[i][j1]
            
            if j1 != j2:
                cherries += grid[i][j2]

            max_cherries = 0
            for d1 in [-1, 0, 1]:
                for d2 in [-1, 0, 1]:
                    max_cherries = max(max_cherries, dp(i + 1, j1 + d1, j2 + d2))

            memo[i][j1][j2] = cherries + max_cherries
            return memo[i][j1][j2]

        return max(0, dp(0, 0, COL_NUM - 1))
        
grid=[[3,1,1],
      [2,5,1],
      [1,5,5],
      [2,1,1]]
ob=Solution()
print(ob.cherryPickup(grid))
```
## Day 2 - KNAPSACK PROBLEM
### Create a python program for 0/1 knapsack problem using naive recursion method
```py
def knapSack(W, wt, val, n):
    dp = [[0] * (W + 1) for _ in range(n + 1)]
    for i in range(n + 1):
        for w in range(W + 1):
            if i == 0 or w == 0:
                dp[i][w] = 0
            elif wt[i - 1] <= w:
                dp[i][w] = max(val[i - 1] + dp[i - 1][w - wt[i - 1]], dp[i - 1][w])
            else:
                dp[i][w] = dp[i - 1][w]
    return dp[n][W]
x=int(input())
y=int(input())
W=int(input())
val=[]
wt=[]
for i in range(x):
    val.append(int(input()))
for y in range(y):
    wt.append(int(input()))
n = len(val)
print('The maximum value that can be put in a knapsack of capacity W is: ',knapSack(W, wt, val, n))
```
## Day 3 - TRAVELLING SALES MAN PROBLEM
### Solve Travelling Sales man Problem for the following graph
![image](https://github.com/user-attachments/assets/120c240c-613e-4bc8-ad51-ea5b1441cc96)

```py
from sys import maxsize
from itertools import permutations
V = 4
 

def travellingSalesmanProblem(graph, s):
    vertex = [] 
    for i in range(V): 
        if i != s: 
            vertex.append(i) 
    min_path = maxsize 
    next_permutation=permutations(vertex)
    for i in next_permutation:
        current_pathweight = 0
        k = s 
        for j in i: 
            current_pathweight += graph[k][j] 
            k = j 
        current_pathweight += graph[k][s] 
        min_path = min(min_path, current_pathweight) 
    return min_path
if __name__ == "__main__":
 
    graph = [[0, 10, 15, 20], [10, 0, 35, 25],
            [15, 35, 0, 30], [20, 25, 30, 0]]
    s = 0
    print(travellingSalesmanProblem(graph, s))
```
## Day 4 - BRUTE FORCE ALGORITHM
### Create a python program using brute force method of searching for the given substring in the main string.
```py
def match(string, sub):
    l = len(string)
    ls = len(sub)
    for i in range(l - ls + 1):
        found = True
        for j in range(ls):
            if string[i + j] != sub[j]:
                found = False
                break
        if found:
            print(f"Found at index {i}")

str1=input()
str2=input()

```
