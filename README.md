# Count-Unguarded-Cells-in-the-Grid
You are given two integers m and n representing a 0-indexed m x n grid. You are also given two 2D integer arrays guards and walls where guards[i] = [rowi, coli] and walls[j] = [rowj, colj] represent the positions of the ith guard and jth wall respectively.

A guard can see every cell in the four cardinal directions (north, east, south, or west) starting from their position unless obstructed by a wall or another guard. A cell is guarded if there is at least one guard that can see it.

Return the number of unoccupied cells that are not guarded.

class Solution:
    def countUnguarded(self, m: int, n: int, guards: List[List[int]], walls: List[List[int]]) -> int:
        # Initialize grid with zeros
        g = [[0] * n for _ in range(m)] # g - 2D grid/matrix
        
        # Mark guards and walls as 2
        for x, y in guards:  # gx, gy -  guard's position 
            g[x][y] = 2    
        for x, y in walls:
            g[x][y] = 2
            
        # Directions: up, right, down, left
        dirs = [(-1, 0), (0, 1), (1, 0), (0, -1)]
        
        # Process each guard's line of sight
        for gx, gy in guards:
            for dx, dy in dirs: # dx, dy - movement direction offsets
                x, y = gx, gy
                while True:
                    x += dx
                    y += dy
                    # Check cells in current direction until hitting boundary or obstacle
                    if x < 0 or x >= m or y < 0 or y >= n or g[x][y] == 2:
                        break
                    g[x][y] = 1
        
        # Count unguarded cells (cells with value 0)
        return sum(row.count(0) for row in g)
        
