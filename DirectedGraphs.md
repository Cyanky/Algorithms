## Adjacency-lists digraph representation  
```  
public class Digraph
{
 private final int V;
 private final Bag<Integer>[] adj;
 public Digraph(int V)
 {
 this.V = V;
 adj = (Bag<Integer>[]) new Bag[V];
 for (int v = 0; v < V; v++)
 adj[v] = new Bag<Integer>();
 }
 public void addEdge(int v, int w)
 {
 adj[v].add(w);
 }
 public Iterable<Integer> adj(int v)
 { return adj[v]; }
}  
```  
## Depth-first search (in directed graphs)  
```  
public class DirectedDFS
{
 private boolean[] marked;
 public DirectedDFS(Digraph G, int s)
 {
 marked = new boolean[G.V()];
 dfs(G, s);
 }
 private void dfs(Digraph G, int v)
 {
 marked[v] = true;
 for (int w : G.adj(v))
 if (!marked[w]) dfs(G, w);
 }
 public boolean visited(int v)
 { return marked[v]; }
}  
```  
## Bare-bones web crawler  
```  
Queue<String> queue = new Queue<String>();
 SET<String> marked = new SET<String>();
 String root = "http://www.princeton.edu";
 queue.enqueue(root);
 marked.add(root);
 while (!queue.isEmpty())
 {
 String v = queue.dequeue();
 StdOut.println(v);
 In in = new In(v);
 String input = in.readAll();
 String regexp = "http://(\\w+\\.)*(\\w+)";
 Pattern pattern = Pattern.compile(regexp);
 Matcher matcher = pattern.matcher(input);
 while (matcher.find())
 {
 String w = matcher.group();
 if (!marked.contains(w))
 {
 marked.add(w);
 queue.enqueue(w);
 }
 }
 }  
 ```  
 ## Depth-first search order  
 ```  
 public class DepthFirstOrder
{
 private boolean[] marked;
 private Stack<Integer> reversePost;
 public DepthFirstOrder(Digraph G)
 {
 reversePost = new Stack<Integer>();
 marked = new boolean[G.V()];
 for (int v = 0; v < G.V(); v++)
 if (!marked[v]) dfs(G, v);
 }
 private void dfs(Digraph G, int v)
 {
 marked[v] = true;
 for (int w : G.adj(v))
 if (!marked[w]) dfs(G, w);
 reversePost.push(v);
 }
 public Iterable<Integer> reversePost()
 { return reversePost; }
}  
```  
