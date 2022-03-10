```  
private class Node
{
 private Key key;
 private Value val;
 private Node left, right;
 public Node(Key key, Value val)
 {
 this.key = key;
 this.val = val;
 }
}  
```  
**Skeleton**  
```  
public class BST<Key extends Comparable<Key>, Value>
{
 private Node root;
 private class Node
 { /* see previous slide */ }
 public void put(Key key, Value val)
 { /* see next slides */ }
 public Value get(Key key)
 { /* see next slides */ }
 public void delete(Key key)
 { /* see next slides */ }
 public Iterable<Key> iterator()
 { /* see next slides */ }
}  
```  
