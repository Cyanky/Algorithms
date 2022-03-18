## Search implementation for red-black BSTs  
```  
public Val get(Key key)
{
 Node x = root;
 while (x != null)
 {
 int cmp = key.compareTo(x.key);
 if (cmp < 0) x = x.left;
 else if (cmp > 0) x = x.right;
 else if (cmp == 0) return x.val;
 }
 return null;
}  
```  
## Red-black BST representation  
```  
private static final boolean RED = true;
 private static final boolean BLACK = false;
 private class Node
 {
 Key key;
 Value val;
 Node left, right;
 boolean color; // color of parent link
 }
 private boolean isRed(Node x)
 {
 if (x == null) return false;
 return x.color == RED;
 }  
 ```  
   
   ## Insertion in a LLRB tree  
   ```  
   private Node put(Node h, Key key, Value val)
 {
 if (h == null) return new Node(key, val, RED);
 int cmp = key.compareTo(h.key);
 if (cmp < 0) h.left = put(h.left, key, val);
 else if (cmp > 0) h.right = put(h.right, key, val);
 else if (cmp == 0) h.val = val;
 if (isRed(h.right) && !isRed(h.left)) h = rotateLeft(h);
 if (isRed(h.left) && isRed(h.left.left)) h = rotateRight(h);
 if (isRed(h.left) && isRed(h.right)) flipColors(h);

 return h;
 }  
 ```
   
