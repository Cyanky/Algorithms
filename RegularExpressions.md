## NFA simulation: Java implementation  
```  
public class NFA
{
 private char[] re; // match transitions
 private Digraph G; // epsilon transition digraph
 private int M; // number of states
 public NFA(String regexp)
 {
 M = regexp.length();
 re = regexp.toCharArray();
 G = buildEpsilonTransitionDigraph();
 }
 public boolean recognizes(String txt)
 { /* see next slide */ }
 public Digraph buildEpsilonTransitionDigraph()
 { /* stay tuned */ }
} 
  
  public boolean recognizes(String txt)
{
 Bag<Integer> pc = new Bag<Integer>();
 DirectedDFS dfs = new DirectedDFS(G, 0);
 for (int v = 0; v < G.V(); v++)
 if (dfs.marked(v)) pc.add(v);
 for (int i = 0; i < txt.length(); i++)
 {
 Bag<Integer> states = new Bag<Integer>();
 for (int v : pc)
 {
 if (v == M) continue;
 if ((re[v] == txt.charAt(i)) || re[v] == '.')
 states.add(v+1);
 }

 dfs = new DirectedDFS(G, states);
 pc = new Bag<Integer>();
 for (int v = 0; v < G.V(); v++)
 if (dfs.marked(v)) pc.add(v);
 }
 for (int v : pc)
 if (v == M) return true;
 return false;
}  
```  
