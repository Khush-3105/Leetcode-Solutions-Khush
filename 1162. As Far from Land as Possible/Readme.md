# Problem: As Far from Land as Possible
Platform: Leetcode

Difficulty: Medium

Problem Link: https://leetcode.com/problems/as-far-from-land-as-possible/

## Problem Statement:

Given an n x n grid containing only values 0 and 1, where 0 represents water and 1 represents land, find a water cell such that its distance to the nearest land cell is maximized, and return the distance. If no land or water exists in the grid, return -1.

The distance used in this problem is the Manhattan distance: the distance between two cells (x0, y0) and (x1, y1) is |x0 - x1| + |y0 - y1|.

Example 1:

    Input: grid = [[1,0,1],[0,0,0],[1,0,1]]
    Output: 2
    Explanation: The cell (1, 1) is as far as possible from all the land with distance 2.

Example 2:

    Input: grid = [[1,0,0],[0,0,0],[0,0,0]]
    Output: 4
    Explanation: The cell (2, 2) is as far as possible from all the land with distance 4.


## My Approach:

    1. Seeing that the topic is a graph and related to the shortest path, I first thought of using BFS to solve the problem.
    2. We can first find out all the land, and then carry out BFS diffusion from the land, and then increase the counter by one for each layer of diffusion,
    3. Continue to "reclaim land" until the entire map no longer has oceans. The counter at this time is the distance from the farthest ocean to land.        


## Solution (In Java):

    class Solution {
        public int maxDistance(int[][] grid) {
            int m = grid.length, n = grid[0].length;
            Queue<int[]> queue = new LinkedList<>();
            boolean[][] visited = new boolean[m][n];
            for (int i = 0; i < m; i++) {
                for (int j = 0; j < n; j++) {
                    if (grid[i][j] == 1) {
                        queue.offer(new int[]{i, j});
                        visited[i][j] = true;
                    }
                }
            }

            if (queue.isEmpty() || queue.size() == m * n) {
                return -1;
            }
            int[][] DIRS = {{0, -1}, {0, 1}, {-1, 0}, {1, 0}};
            int step = 0;
            while (!queue.isEmpty()) {
                for (int size = queue.size(), i = 0; i < size; i++) {
                    int[] curr = queue.poll();
                    for (int[] dir : DIRS) {
                        int nextRow = curr[0] + dir[0], nextCol = curr[1] + dir[1];
                        if (nextRow < 0 || nextRow >= m || nextCol < 0 || nextCol >= n || visited[nextRow][nextCol] || grid[nextRow][nextCol] == 1) {
                            continue;
                        }
                        queue.offer(new int[]{nextRow, nextCol});
                        visited[nextRow][nextCol] = true;
                    }
                }
                step++;
            }
            return step-1;
        }
    }

## Output:
<img
  src="Output.png"
  alt="Alt text"
  title="Optional title"
  style="display: inline-block; margin: 0 auto; max-width: 300px">






