#  Intuition for Prim's Algorithm using Priority Queue

---

##  Why do we use a Priority Queue?

We are trying to find a **Minimum Spanning Tree (MST)**, which means we always want to pick the edge with the **minimum weight** that connects a new node to the existing tree.  
So, we use a **priority queue (min-heap)** to always extract the edge with the **smallest weight first**.

---

## What do we store in the Priority Queue?

Each entry in the priority queue is a **triplet**:
**[parent node, current node, edge weight]**
This helps us track which node we’re visiting, what edge weight is used to reach it, and optionally, where we came from.

## Overall Process :
### Initialization:

Create a visited array of size V, initialized with 0.

Add the starting node (say node 0) to the priority queue with weight 0.
→ pq.offer([-1, 0, 0])

### MST Construction:

While the queue is not empty:

Remove the top element from the queue (minimum weight edge).

Check if the node is already visited:

If yes → skip (continue).

If not → mark as visited, and add its weight to the total MST weight.

For all adjacent (child) nodes of the current node:

If the child node is not yet visited, push it into the queue with its corresponding edge weight.

Final Step:

When the queue is empty, return the sum of all edge weights in the MST.

## Code in java

```java
import java.util.*;

class Solution {
    static int spanningTree(int V, int E, List<List<int[]>> edges) {
        //  Ye array batayega konsa node visit hua hai
        int[] visit = new int[V];

        //  Min heap banaya jisme hamesha minimum weight wali edge top pe aayegi
        // pq me ye store hoga: {parent, currentNode, weight}
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[2] - b[2]);

        //  Starting node 0 se start kar rahe with weight 0
        pq.offer(new int[]{-1, 0, 0});

        //  MST ka total weight store karne ke liye
        int weight = 0;

        // Jab tak queue empty na ho tab tak loop chalayenge
        while (!pq.isEmpty()) {
            int[] curr = pq.poll();
            int parent = curr[0]; // kaunse node se aaye ho (not needed here)
            int node = curr[1];   // abhi ka node
            int wt = curr[2];     // us edge ka weight

            //  Agar already visit ho chuka hai toh skip (cycle avoid)
            if (visit[node] == 1) continue;

            // Node ko mark karo visited aur weight me add karo
            visit[node] = 1;
            weight += wt;

            // Ab is node ke neighbors check karenge
            for (int[] neighbor : edges.get(node)) {
                int child = neighbor[0];      // neighbor node
                int edgeWeight = neighbor[1]; // edge ka weight

                // Agar neighbor visited nahi hai toh queue me daal do
                if (visit[child] == 0) {
                    pq.offer(new int[]{node, child, edgeWeight});
                }
            }
        }

        //  Final MST ka total weight return kar do
        return weight;
    }
}

