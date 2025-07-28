
````java
class Solution {

    // 🔁 DFS wali function banayi hai Topological Sort ke liye
    public static void Topo(ArrayList<ArrayList<Integer>> g , int [] visit,int node,Stack<Integer> st){
        visit[node] = 1; // ✅ Visit mark kar diya

        // 👇 Ab har neighbour ko check karenge
        for(int i = 0;i<g.get(node).size();i++){
            int curr = g.get(node).get(i); // 🔍 Current neighbour liya
            
            if(visit[curr]==0){ // 🤔 Agar visit nahi hua hai
                Topo(g,visit,curr,st); // 📞 Recursive call kar diya
            }
        }

        st.push(node); // 🔚 Sab complete ho gaya toh stack me daal diya
    }

    // 🌟 Yahan se actual Topological Sort start ho rahi hai
    public static ArrayList<Integer> topoSort(int V, int[][] edges) {

        // 📦 Graph ko banaya adjacency list ke form me
        ArrayList<ArrayList<Integer>> g = new ArrayList<>();
        for(int i = 0;i<V;i++){
            g.add(new ArrayList<>());
        }

        // 🔗 Sab edges ko graph me daal diya
        for(int i = 0;i<edges.length;i++){
            int u = edges[i][0]; // From node
            int v = edges[i][1]; // To node
            g.get(u).add(v);     // Edge add kiya
        }

        Stack<Integer> st  = new Stack<>(); //  Stack banaya nodes store karne ke liye
        int visit [] = new int[V];          //  Visit array banayi

        // Har node ko visit kar rahe hai
        for(int i = 0;i<V;i++){
            if(visit[i]==0){ // ❗ Agar visit nahi hua toh
                Topo(g,visit,i,st); // ➡ DFS call kiya
            }
        }

        ArrayList<Integer> ans = new ArrayList<>(); // 📋 Answer list banayi
        while(!st.isEmpty()){ //  Stack khali hone tak
            ans.add(st.pop()); //  Stack se pop karte jao
        }

        return ans; //  Final sorted list return kar di
    }
}
