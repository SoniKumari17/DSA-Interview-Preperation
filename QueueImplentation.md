# Storing Pairs in Queue 

## 1. Using `int[]`

```java
Queue<int[]> q = new LinkedList<>();
q.add(new int[]{node, parent});
```` 
## 2. Using a Custom Class
```java
class Pair {
    int node, parent;

    Pair(int node, int parent) {
        this.node = node;
        this.parent = parent;
    }
}

// Queue of custom Pair objects
Queue<Pair> q = new LinkedList<>();
q.add(new Pair(node, parent));
 ````
