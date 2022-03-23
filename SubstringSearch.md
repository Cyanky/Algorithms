## Screen scraping  
```  
public class StockQuote
{
 public static void main(String[] args)
 {
 String name = "http://finance.yahoo.com/q?s=";
 In in = new In(name + args[0]);
 String text = in.readAll();
 int start = text.indexOf("Last Trade:", 0);
 int from = text.indexOf("<b>", start);
 int to = text.indexOf("</b>", from);
 String price = text.substring(from + 3, to);
 StdOut.println(price);
 }
}  
```  
## Boyer-Moore  
```  
 public int search(String txt)
 {
 int N = txt.length();
 int M = pat.length();
 int skip;
 for (int i = 0; i <= N-M; i += skip)
 {
 skip = 0;
 for (int j = M-1; j >= 0; j--)
 {
 if (pat.charAt(j) != txt.charAt(i+j))
 {
 skip = Math.max(1, j - right[txt.charAt(i+j)]);
 break;
 }
 }
 if (skip == 0) return i;
 }
 return N;
}  
```  
## Rabin-Karp  
```  
public class RabinKarp
{
 private long patHash; // pattern hash value
 private int M; // pattern length
 private long Q; // modulus
 private int R; // radix
 private long RM; // R^(M-1) % Q
 public RabinKarp(String pat) {
 M = pat.length();
 R = 256;
 Q = longRandomPrime();
 RM = 1;
 for (int i = 1; i <= M-1; i++)
 RM = (R * RM) % Q;
 patHash = hash(pat, M);
 }
 private long hash(String key, int M)
 { /* as before */ }
 public int search(String txt)
 { public int search(String txt)
 {
 int N = txt.length();
 int txtHash = hash(txt, M);
 if (patHash == txtHash) return 0;
 for (int i = M; i < N; i++)
 {
 txtHash = (txtHash + Q - RM*txt.charAt(i-M) % Q) % Q;
 txtHash = (txtHash*R + txt.charAt(i)) % Q;
 if (patHash == txtHash) return i - M + 1;
 }
 return N;
 }}
}  
