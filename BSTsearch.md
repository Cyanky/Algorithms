```  
public Value get(Key key)
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
 
