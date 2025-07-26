# Given an undirected graph with V vertices and E edges, represented as a 2D vector edges[][], where each entry edges[i] = [u, v] denotes an edge between vertices u and v, determine whether the graph contains a cycle or not.
### 🧪 Example 1

**Input:**  
`V = 4`, `E = 4`,  
`edges = [[0, 1], [0, 2], [1, 2], [2, 3]]`

**Output:**  
`true`

**Explanation:**  
There is a cycle:  
`1 → 2 → 0 → 1`

```java
class Solution {

    public boolean isCycle(int V, int[][] edges) {
        // Sabse pehle graph ko adjacency list ke form me banate hain
        ArrayList<ArrayList<Integer>> graph = new ArrayList<>();

        // Har node ke liye ek empty list daal rahe hain jahan uske neighbors aayenge
        for(int i = 0; i < V; i++) {
            graph.add(new ArrayList<>());
        }

        // Ab edge list ko adjacency list me convert karte hain
        for(int i = 0; i < edges.length; i++) {
            int u = edges[i][0];
            int v = edges[i][1];

            // Kyunki graph undirected hai, dono side se connect karenge
            graph.get(u).add(v);
            graph.get(v).add(u);
        }

        // Ye array batayega kaunse node visit ho chuki hai
        boolean[] visit = new boolean[V];

        // Har node ke liye check karenge (graph disconnected bhi ho sakta hai)
        for(int i = 0; i < V; i++) {
            // Agar node visit nahi hui hai to bfs se cycle check karo
            if(visit[i] == false) {
                if(bfs(visit, graph, i, -1) == true) return true;
            }
        }

        // Agar kahin bhi cycle nahi mila
        return false;
    }

    // Ye function bfs lagake cycle check karega
    public boolean bfs(boolean[] visit, ArrayList<ArrayList<Integer>> graph, int node, int parent) {
        // Queue banayi jisme node aur uska parent store karenge
        Queue<int[]> q = new LinkedList<>();

        // Starting node ko queue me daala
        q.add(new int[]{node, parent});
        visit[node] = true; // mark as visited

        while(!q.isEmpty()) {
            int[] arr = q.remove();
            int curr = arr[0];   // current node
            int papa = arr[1];   // uska parent

            // Ab uske sare neighbors check karenge
            for(int i = 0; i < graph.get(curr).size(); i++) {
                int neighbor = graph.get(curr).get(i);

                // Agar neighbor pehle se visit nahi hua to queue me daal do
                if(visit[neighbor] == false) {
                    visit[neighbor] = true;
                    q.add(new int[]{neighbor, curr});
                }
                // Agar visit hua hai lekin parent nahi hai to matlab cycle mil gaya
                else if(neighbor != papa) {
                    return true; // cycle detected 🚨
                }
            }
        }

        // Agar queue khali ho gayi aur cycle nahi mila
        return false;
    }
}

```
## humne ArrayList bana ke firse usme Arraylish kiyu dala ?? 
### basically humne ye step kiyu kara ? 
```java 
for(int i = 0;i<V;i++){
    graph.add(new ArrayList<>());
}
```
## What This Line Does:
#### It initializes the adjacency list for a graph with V vertices.

#### Suppose:
#### You declared the graph as:
```java
ArrayList<ArrayList<Integer>> graph = new ArrayList<>();
```
#### Now this list is empty, meaning: graph = []
##### But in order to represent each vertex’s neighbors, you need a list inside this list — one for each vertex.
##### So after this loop:
```java
for (int i = 0; i < V; i++) {
    graph.add(new ArrayList<>());
}
```
##### You get:
```java
graph = [
  [],  // neighbors of vertex 0
  [],  // neighbors of vertex 1
  [],  // neighbors of vertex 2
  [],  // neighbors of vertex 3
]
```
##### Now, you can safely do:
##### graph.get(0).add(1); // add edge 0 -> 1
