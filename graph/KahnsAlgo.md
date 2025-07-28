```java
class Solution {

    // Ye function main logic hai kahn's algorithm ka (BFS approach for topological sort)
    public static ArrayList<Integer> kanshAlgo(ArrayList<ArrayList<Integer>> g, int[] indegree, Queue<Integer> q) {
        ArrayList<Integer> ans = new ArrayList<>(); // Ye list final answer store karegi

        // Jab tak queue khali na ho
        while (!q.isEmpty()) {
            int curr = q.remove(); // Queue se ek node nikala

            // Us node ke sab neighbours ke indegree kam karenge
            for (int i = 0; i < g.get(curr).size(); i++) {
                int el = g.get(curr).get(i); // Neighbour node
                indegree[el]--; // Uska indegree ek kam kiya

                // Agar ab wo neighbour ka indegree 0 ho gaya, to queue me daal diya
                if (indegree[el] == 0) {
                    q.add(el);
                }
            }

            // Ab is node ko answer me daal diya
            ans.add(curr);
        }

        // Final topological order return
        return ans;
    }

    // Ye main function hai jo graph banata hai aur kahn's algorithm call karta hai
    public static ArrayList<Integer> topoSort(int V, int[][] edges) {
        // Step 1: Graph ko adjacency list ke form me banaya
        ArrayList<ArrayList<Integer>> g = new ArrayList<>();
        for (int i = 0; i < V; i++) {
            g.add(new ArrayList<>()); // Har node ka ek empty list banaya
        }

        // Step 2: Saare edges ko graph me daala
        for (int i = 0; i < edges.length; i++) {
            int u = edges[i][0]; // From node
            int v = edges[i][1]; // To node
            g.get(u).add(v);     // u se v ke beech edge daala
        }

        // Step 3: Har node ka indegree count karenge
        int[] indegree = new int[V];
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < g.get(i).size(); j++) {
                int el = g.get(i).get(j); // Neighbour node
                indegree[el]++; // Uska indegree badhaya
            }
        }

        // Step 4: Queue banayi, sab nodes jinke indegree 0 hai unko daal diya
        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < V; i++) {
            if (indegree[i] == 0) {
                q.add(i); // Ye nodes directly start karne layak hai
            }
        }

        // Step 5: Ab kahn's algorithm se topological sort nikaalenge
        return kanshAlgo(g, indegree, q);
    }
}
````
### Jaldi Samajhne ke liye Summary:

1. **Graph banaya** adjacency list ke form me.

2. **Indegree array banayi**: har node pe kitni edges aa rahi hain, wo count kiya.

3. **Queue me un nodes ko daala** jinka `indegree == 0` tha. Ye wo nodes hain jinke pehle koi node nahi aata.

4. **Queue se ek ek node nikala**, uske har neighbour ka `indegree--` kiya.

5. **Agar neighbour ka indegree 0 ho gaya**, to usko bhi queue me daala.

6. Ye process **tab tak chalaate rahe jab tak queue khali na ho jaye**.

7. Jo bhi nodes queue se nikle, unhe ek list me daala. **Ye hi final Topological Sort hai**.

