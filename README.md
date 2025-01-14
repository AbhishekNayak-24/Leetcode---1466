# Leetcode---1466
Reorder Routes to Make All Paths Lead To the City Zero
// code in java
import java.util.*;

public class Solution {
    public int minReorder(int n, int[][] connections) {
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            graph.add(new ArrayList<>());
        }
        for (int[] connection : connections) {
            graph.get(connection[0]).add(connection[1]);
            graph.get(connection[1]).add(-connection[0]);
        }
        
        return dfs(graph, new boolean[n], 0);
    }
    
    private int dfs(List<List<Integer>> graph, boolean[] visited, int node) {
        int change = 0;
        visited[node] = true;
        for (int neighbor : graph.get(node)) {
            if (!visited[Math.abs(neighbor)]) {
                change += dfs(graph, visited, Math.abs(neighbor)) + (neighbor > 0 ? 1 : 0);
            }
        }
        return change;
    }
}
