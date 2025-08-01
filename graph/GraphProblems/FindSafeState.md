```java
class Solution {
    public List<Integer> Kahns(List<List<Integer>> g,int [] ind , Queue<Integer> q ){
        List<Integer> list = new ArrayList<>();
        while(!q.isEmpty()){
            int curr = q.remove();
            list.add(curr);
            
            for(int i = 0;i<g.get(curr).size();i++){
                int child = g.get(curr).get(i);
                ind[child]--;
                if(ind[child]==0){
                    q.add(child);
                }
            }
        }
        return list;
    }

    List<Integer> eventualSafeNodes(int V, List<List<Integer>> adj) {

        // Your code here
        List<List<Integer>> l = new ArrayList<>();
        for (int i = 0; i < V; i++) {
             l.add(new ArrayList<>());
        }
        //reverse arrray
        for(int i  = 0;i<V;i++){
        
            for(int j = 0;j<adj.get(i).size();j++){
                int u = adj.get(i).get(j);
                l.get(u).add(i);
            }
        }
        //Count Indegree
        int[] ind = new int[V];
        for(int i = 0;i<V;i++){
            for(int j = 0;j<l.get(i).size();j++){
                int el = l.get(i).get(j);
                ind[el]++;
            }
        }
        
        //putting node  that has indegree "0"
        Queue<Integer> q  = new LinkedList<>();
        for(int i = 0;i<V;i++){
            if(ind[i]==0){
              q.add(i);
            }
        }
        List<Integer> newlist = new ArrayList<>();
          newlist = Kahns(l,ind,q);
          Collections.sort(newlist);
          return newlist;
    }
}

