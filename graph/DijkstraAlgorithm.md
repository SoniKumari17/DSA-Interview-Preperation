
#  Dijkstra's Algorithm Using PriorityQueue (Java) 
## Intuition:

## 🔍 Intuition (Dijkstra's Algorithm)

We will use a **Priority Queue (Min-Heap)** because our goal is to find the **minimum distance** from the source node to all other nodes.

Since we always want the node with the **smallest current distance**, a priority queue is ideal — it automatically gives us the node with the minimum distance at the top.

Each element we store in the priority queue will be in the form of:  
`(node, distance from source)`

---

### ✅ Distance Array:
We’ll maintain a **distance array** called `dist[]` where:

- `dist[i]` = shortest distance from source to node `i`.
- Initially, set all distances to **infinity** (`1e9`) since we don’t know the path yet.
- Set `dist[src] = 0` because the distance from the source to itself is always 0.

Also, add `(src, 0)` to the priority queue to begin processing.

---

### 🔁 Looping Through the Queue:
Then, we'll run a loop **until the queue becomes empty**.

- In each iteration, we remove the top node (the one with the current minimum distance).
- Then, we check all its **children (adjacent nodes)**.
- For each child, we check:  
  **Can we reach this child with a shorter path through the current node?**  
  If yes, we update the distance and push that child into the priority queue.

---

### 🧠 In Short:
The algorithm keeps choosing the shortest available path at every step.  
So instead of exploring longer paths first, it builds the shortest paths piece by piece — using smaller steps to reach each node optimally.

---

## Algorithm Steps:

1. **Graph banao:** Adjacency list se graph ko represent karo.
2. **Distance array banao:** Har node ka distance `infinity` (1e9) set karo, aur source node ka distance `0`.
3. **PriorityQueue banao:** `int[]` store karega jisme `int[]{node, distance}` hoga. Comparator lagao based on distance.
4. **PQ me source node daalo.**
5. Jab tak PQ empty na ho:
   - Node nikaalo jiska distance sabse kam ho.
   - Uske neighbours traverse karo.
   - Agar shorter path milta hai toh update karo and PQ me daal do.

---

##  Java Code

```java
class Solution {
    public int[] dijkstra(int V, int[][] edges, int src) {
        // Step 1: Graph ko adjacency list me convert karo
        ArrayList<ArrayList<int[]>> graph = new ArrayList<>();
        for (int i = 0; i < V; i++) {
            graph.add(new ArrayList<>());
        }

        // Step 2: Graph me edges add karo (undirected graph ke liye dono direction me)
        for (int i = 0; i < edges.length; i++) {
            int u = edges[i][0];
            int v = edges[i][1];
            int w = edges[i][2];

            graph.get(u).add(new int[]{v, w});
            graph.get(v).add(new int[]{u, w}); // Undirected edge
        }

        // Step 3: Distance array initialize karo sabko infinity se, sirf source ko 0
        int[] dist = new int[V];
        for (int i = 0; i < V; i++) {
            dist[i] = (int) 1e9;
        }
        dist[src] = 0;

        // Step 4: PriorityQueue banao jisme comparator ho based on distance
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
        
        // Step 5: Source node ko queue me daalo
        pq.offer(new int[]{src, 0});

        // Step 6: Jab tak PQ empty na ho
        while (!pq.isEmpty()) {
            int[] array = pq.poll();
            int parent = array[0];
            int d = array[1];

            // Step 7: Current node ke neighbours traverse karo
            for (int[] child : graph.get(parent)) {
                int cd = child[0]; // child node
                int wt = child[1]; // weight

                // Agar naya path chota hai toh update karo
                if (dist[parent] + wt < dist[cd]) {
                    dist[cd] = dist[parent] + wt;
                    pq.offer(new int[]{cd, dist[cd]});
                }
            }
        }

        // Step 8: Final distance array return karo
        return dist;
    }
}
