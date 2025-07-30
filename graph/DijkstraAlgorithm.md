
#  Dijkstra's Algorithm Using PriorityQueue (Java) 
## Intuition:

Hum ek graph ke andar source node se har node tak ka **shortest distance** nikalna chahte hain. 

Dijkstra ka idea ye hai:
- Sabse pehle source node ko le lo.
- Fir har step par **minimum distance** wala node uthao (isiliye PriorityQueue use karte hain).
- Aur us node ke neighbours ka distance update karo agar shorter path milta hai.
- Jab tak queue khali na ho, repeat karo.

Isme hum PriorityQueue ka use karte hain taki har baar minimum distance wale node ko fast nikaal sakein.

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
