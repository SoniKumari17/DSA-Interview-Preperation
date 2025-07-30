# Floyd Warshall Algorithm - Simple Intuition

## Simple Intuition

**"Har node ko ek baar *bridge* (intermediate node) maan lo aur check karo kya uske through better (shorter) path mil raha hai ya nahi."**

---

##  Aur simple words mein socho:

- Suppose you want to go from **A to C**.
- Check:  
   *Kya A se B aur B se C jaake A to C faster ho sakta hai?*  
    Yani `dist[A][C] = min(dist[A][C], dist[A][B] + dist[B][C])`

Aisa hi har **pair of nodes (i, j)** ke liye **har node (k)** ko intermediate maan ke check karte hain.

---

## One line yaad rakhne ke liye:

> **Try all paths i → k → j and update if it's shorter than direct i → j.**

---

## Negative weight cycle detection:

- Jab khud ka distance khud se (`dist[i][i]`) negative ho jaye, iska matlab hai:

> **Cycle hai jiska total weight negative hai (infinite loop ho sakta hai profit ya time mein)**

---

##  Triple Nested Loops: (i, j, k)

- Time Complexity: **O(V³)**  
- Works with **negative weights** (but not with negative weight *cycles* in result)

----
### java code 
````java
import java.util.*;

class GfG {
    // Infinity ke liye ek large value define kar rahe hain
    static final int INF = (int) 1e8;

    // Floyd Warshall Algorithm
    static void floydWarshall(int[][] dist, int V) {
        // Teen nested loops: har ek node ko intermediate node maan ke check karenge
        for (int k = 0; k < V; k++) { // k = intermediate node
            for (int i = 0; i < V; i++) { // i = source node
                for (int j = 0; j < V; j++) { // j = destination node
                    // Agar i to k and k to j dono reachable hain tabhi check karenge
                    if (dist[i][k] != INF && dist[k][j] != INF)
                        // i to j ka distance update karo agar intermediate se better path milta ho
                        dist[i][j] = Math.min(dist[i][j], dist[i][k] + dist[k][j]);
                }
            }
        }

        // Ab check karenge negative weight cycle hai ya nahi
        // Agar kisi node ka khud ka distance negative hai to matlab cycle hai
        for (int i = 0; i < V; i++) {
            if (dist[i][i] < 0) {
                System.out.println("Negative weight cycle detected!");
                return;
            }
        }

        // Agar koi bhi dist[i][i] < 0 nahi mila to cycle nahi hai
        System.out.println("No negative weight cycle.");
    }

    // Main function jahan se code run hota hai
    public static void main(String[] args) {
        int V = 4;
        int INF = (int) 1e8;

        // Graph ka adjacency matrix form
        // graph[i][j] = i se j ka weight, agar path nahi hai to INF
        int[][] graph = {
            {0,     1,     INF,   INF},
            {INF,   0,    -1,     INF},
            {INF,   INF,   0,     -1},
            {-1,    INF,   INF,   0}
        };

        // Algorithm call karo
        floydWarshall(graph, V);
    }
}
````
# Time Complexity Comparison: Floyd Warshall vs Dijkstra

## 1. Floyd Warshall Algorithm

- **Time Complexity:** O(V³)
- **Space Complexity:** O(V²) (due to distance matrix)
- **Use Case:** When you need shortest paths between all pairs of nodes.

## 2. Dijkstra’s Algorithm

- **Time Complexity (single run):**  
  - Using Priority Queue (Min-Heap): O((V + E) log V)

- **All-Pairs Shortest Paths using Dijkstra:**  
  - Run Dijkstra from every node: V * O((V + E) log V)  
  - **Total:** O(V * (V + E) log V)

## Comparison Table

| Feature                        | Floyd Warshall              | Dijkstra (with heap)              |
|-------------------------------|-----------------------------|----------------------------------|
| Handles negative weights?     | Yes (no negative cycles)    | No (fails with negative weights) |
| Detects negative weight cycle | Yes                         | No                               |
| All-pairs shortest paths      | Yes                         | Yes (run V times)                |
| Time complexity (all-pairs)   | O(V³)                       | O(V * (V + E) log V)             |
| Best for                      | Dense graphs, small V       | Sparse graphs, no negative weights |

