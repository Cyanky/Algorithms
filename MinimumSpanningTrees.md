## Weighted edge  
```  
public class Edge implements Comparable<Edge>
{
 private final int v, w;
 private final double weight;
 public Edge(int v, int w, double weight)
 {
 this.v = v;
 this.w = w;
 this.weight = weight;
 }
 public int either()
 { return v; }
 public int other(int vertex)
 {
 if (vertex == v) return w;
 else return v;
 }
 public int compareTo(Edge that)
 {
 if (this.weight < that.weight) return -1;
 else if (this.weight > that.weight) return +1;
 else return 0;
 }
}  
```  
## Edge-weighted graph  
```  
public class EdgeWeightedGraph
{
 private final int V;
 private final Bag<Edge>[] adj;
 public EdgeWeightedGraph(int V)
 {
 this.V = V;
 adj = (Bag<Edge>[]) new Bag[V];
 for (int v = 0; v < V; v++)
 adj[v] = new Bag<Edge>();
 }
 public void addEdge(Edge e)
 {
 int v = e.either(), w = e.other(v);
 adj[v].add(e);
 adj[w].add(e);
 }
 public Iterable<Edge> adj(int v)
 { return adj[v]; }
}  
```  
## Kruskal's algorithm  
```  
public class KruskalMST
{
 private Queue<Edge> mst = new Queue<Edge>();
 public KruskalMST(EdgeWeightedGraph G)
 {
 MinPQ<Edge> pq = new MinPQ<Edge>();
 for (Edge e : G.edges())
 pq.insert(e);
 UF uf = new UF(G.V());
 while (!pq.isEmpty() && mst.size() < G.V()-1)
 {
 Edge e = pq.delMin();
 int v = e.either(), w = e.other(v);
 if (!uf.connected(v, w))
 {
 uf.union(v, w);
 mst.enqueue(e);
 }
 }
 }
 public Iterable<Edge> edges()
 { return mst; }
}  
```  
## Prim's algorithm  
```  
public class LazyPrimMST
{
 private boolean[] marked; // MST vertices
 private Queue<Edge> mst; // MST edges
 private MinPQ<Edge> pq; // PQ of edges
 public LazyPrimMST(WeightedGraph G)
 {
 pq = new MinPQ<Edge>();
 mst = new Queue<Edge>();
 marked = new boolean[G.V()];
 visit(G, 0);

 while (!pq.isEmpty() && mst.size() < G.V() - 1)
 {
 Edge e = pq.delMin();
 int v = e.either(), w = e.other(v);
 if (marked[v] && marked[w]) continue;
 mst.enqueue(e);
 if (!marked[v]) visit(G, v);
 if (!marked[w]) visit(G, w);
 }
 }
}
  private void visit(WeightedGraph G, int v)
 {
 marked[v] = true;
 for (Edge e : G.adj(v))
 if (!marked[e.other(v)])
 pq.insert(e);
 }
 public Iterable<Edge> mst()
 { return mst; }

  ```  
 
