## Weighted directed edge  
```  
public class DirectedEdge
{
 private final int v, w;
 private final double weight;
 public DirectedEdge(int v, int w, double weight)
 {
 this.v = v;
 this.w = w;
 this.weight = weight;
 }
 public int from()
 { return v; }
 public int to()
 { return w; }
 public int weight()
 { return weight; }
}  
```  
## Edge-weighted digraph  
```  
public class EdgeWeightedDigraph
{
 private final int V;
 private final Bag<DirectedEdge>[] adj;
 public EdgeWeightedDigraph(int V)
 {
 this.V = V;
 adj = (Bag<DirectedEdge>[]) new Bag[V];
 for (int v = 0; v < V; v++)
 adj[v] = new Bag<DirectedEdge>();
 }
 public void addEdge(DirectedEdge e)
 {
 int v = e.from();
 adj[v].add(e);
 }
 public Iterable<DirectedEdge> adj(int v)
 { return adj[v]; }
}  
```  
## Dijkstra's algorithm  
```  
public class DijkstraSP
{
 private DirectedEdge[] edgeTo;
 private double[] distTo;
 private IndexMinPQ<Double> pq;
 public DijkstraSP(EdgeWeightedDigraph G, int s)
 {
 edgeTo = new DirectedEdge[G.V()];
 distTo = new double[G.V()];
 pq = new IndexMinPQ<Double>(G.V());
 for (int v = 0; v < G.V(); v++)
 distTo[v] = Double.POSITIVE_INFINITY;
 distTo[s] = 0.0;
 pq.insert(s, 0.0);
 while (!pq.isEmpty())
 {
 int v = pq.delMin();
 for (DirectedEdge e : G.adj(v))
 relax(e);
 }
 }
 }  
  private void relax(DirectedEdge e)
 {
 int v = e.from(), w = e.to();
 if (distTo[w] > distTo[v] + e.weight())
 {
 distTo[w] = distTo[v] + e.weight();
 edgeTo[w] = e;
 if (pq.contains(w)) pq.decreaseKey(w, distTo[w]);
 else pq.insert (w, distTo[w]);
 }
 }  
 ```  
 ## Shortest paths in edge-weighted DAGs  
 ```  
 public class AcyclicSP
{
 private DirectedEdge[] edgeTo;
 private double[] distTo;
 public AcyclicSP(EdgeWeightedDigraph G, int s)
 {
 edgeTo = new DirectedEdge[G.V()];
 distTo = new double[G.V()];
 for (int v = 0; v < G.V(); v++)
 distTo[v] = Double.POSITIVE_INFINITY;
 distTo[s] = 0.0;
 Topological topological = new Topological(G);
 for (int v : topological.order())
 for (DirectedEdge e : G.adj(v))
 relax(e);
 }
 }  
 ```  
 
