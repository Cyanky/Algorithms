## Implementing hash code: user-defined types  
``` 
public final class Transaction implements Comparable<Transaction>
{
 private final String who;
 private final Date when;
 private final double amount;
 public Transaction(String who, Date when, double amount)
 { /* as before */ }
 ...
 public boolean equals(Object y)
 { /* as before */ }

 public int hashCode()
 {
 int hash = 17;
 hash = 31*hash + who.hashCode();
 hash = 31*hash + when.hashCode();
 hash = 31*hash + ((Double) amount).hashCode();
 return hash;
 }
}  
```  
  
  ##  Separate chaining S  
  ```  
  public class SeparateChainingHashST<Key, Value>
{
 private int M = 97; // number of chains
 private Node[] st = new Node[M]; // array of chains
 private static class Node
 {
 private Object key;
 private Object val;
 private Node next;
 ...
 }
 private int hash(Key key)
 { return (key.hashCode() & 0x7fffffff) % M; }
 public Value get(Key key) {
 int i = hash(key);
 for (Node x = st[i]; x != null; x = x.next)
 if (key.equals(x.key)) return (Value) x.val;
 return null;
 }
}   
```  

  ##  Linear probing ST implementation  
  ```  
  public class LinearProbingHashST<Key, Value>
{
 private int M = 30001;
 private Value[] vals = (Value[]) new Object[M];
 private Key[] keys = (Key[]) new Object[M];
 private int hash(Key key) { /* as before */ }
 public void put(Key key, Value val)
 {
 int i;
 for (i = hash(key); keys[i] != null; i = (i+1) % M)
 if (keys[i].equals(key))
 break;
 keys[i] = key;
 vals[i] = val;
 }
 public Value get(Key key)
 {
 for (int i = hash(key); keys[i] != null; i = (i+1) % M)
 if (key.equals(keys[i]))
 return vals[i];
 return null;
 }
}  
```  
