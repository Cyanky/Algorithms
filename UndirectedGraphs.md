## Graph API  
```  
public class Graph
Graph(int V) create an empty graph with V vertices
Graph(In in) create a graph from input stream
void addEdge(int v, int w) add an edge v-w
Iterable<Integer> adj(int v) vertices adjacent to v
int V() number of vertices
int E() number of edges
String toString() string representation  

In in = new In(args[0]);
Graph G = new Graph(in);
for (int v = 0; v < G.V(); v++)
 for (int w : G.adj(v))
 StdOut.println(v + "-" + w);  
 ```  
 ## Typical graph-processing code  
 ```  
 public static int degree(Graph G, int v)
{
 int degree = 0;
 for (int w : G.adj(v)) degree++;
 return degree;
}
compute maximum degree
public static int maxDegree(Graph G)
{
 int max = 0;
 for (int v = 0; v < G.V(); v++)
 if (degree(G, v) > max)
 max = degree(G, v);
 return max;
}
compute average degree public static double averageDegree(Graph G)
{ return 2.0 * G.E() / G.V(); }
count self-loops
public static int numberOfSelfLoops(Graph G)
{
 int count = 0;
 for (int v = 0; v < G.V(); v++)
 for (int w : G.adj(v))
 if (v == w) count++;
 return count/2; // each edge counted twice   
 }  
 
 ```
    
 ## Adjacency-list graph representation:  
 ```  
 public class Graph
{
 private final int V;
 private Bag<Integer>[] adj;
 public Graph(int V)
 {
 this.V = V;
 adj = (Bag<Integer>[]) new Bag[V];
 for (int v = 0; v < V; v++)
 adj[v] = new Bag<Integer>();
 }
 public void addEdge(int v, int w)
 {
 adj[v].add(w);
 adj[w].add(v);
 }
 public Iterable<Integer> adj(int v)
 { return adj[v]; }
}  
```  
## DFS  
```  
public class DepthFirstPaths
{
 private boolean[] marked;
 private int[] edgeTo;
 private int s;
 public DepthFirstPaths(Graph G, int s)
 {
 ...
 dfs(G, s);
 }
 private void dfs(Graph G, int v)
 {
 marked[v] = true;
 for (int w : G.adj(v))
 if (!marked[w])
 {
 dfs(G, w);
 edgeTo[w] = v;
 }
 }
}  
```  
## BFS  
```  
public class BreadthFirstPaths
{
 private boolean[] marked;
 private int[] edgeTo;
 …
 private void bfs(Graph G, int s)
 {
 Queue<Integer> q = new Queue<Integer>();
 q.enqueue(s);
 marked[s] = true;
 while (!q.isEmpty())
 {
 int v = q.dequeue();
 for (int w : G.adj(v))
 {
 if (!marked[w])
 {
 q.enqueue(w);
 marked[w] = true;
 edgeTo[w] = v;
 }
 }
 }
 }
}  
```  
