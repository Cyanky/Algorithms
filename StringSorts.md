##   The String data type
```public final class String implements Comparable<String>
{
 private char[] value; // characters
 private int offset; // index of first char in array
 private int length; // length of string
 private int hash; // cache of hashCode()
 public int length()
 { return length; }
 public char charAt(int i)
 { return value[i + offset]; }


 private String(int offset, int length, char[] value)
 {
 this.offset = offset;
 this.length = length;
 this.value = value;
 }

 public String substring(int from, int to)
 { return new String(offset + from, to - from, value); }
 …  
 ```  
 ## LSD string sort  
 ```  
 public class LSD
{
 public static void sort(String[] a, int W)
 {
 int R = 256;
 int N = a.length;
 String[] aux = new String[N];
 for (int d = W-1; d >= 0; d--)
 {
 int[] count = new int[R+1];
 for (int i = 0; i < N; i++)
 count[a[i].charAt(d) + 1]++;
 for (int r = 0; r < R; r++)
 count[r+1] += count[r];
 for (int i = 0; i < N; i++)
 aux[count[a[i].charAt(d)]++] = a[i];
 for (int i = 0; i < N; i++)
 a[i] = aux[i];
 }
 }
}  
```  
## MSD string sort  
```  
public static void sort(String[] a)
{
 aux = new String[a.length];
 sort(a, aux, 0, a.length-1, 0);
}
private static void sort(String[] a, String[] aux, int lo, int hi, int d)
{
 if (hi <= lo) return;
 int[] count = new int[R+2];
 for (int i = lo; i <= hi; i++)
 count[charAt(a[i], d) + 2]++;
 for (int r = 0; r < R+1; r++)
 count[r+1] += count[r];
 for (int i = lo; i <= hi; i++)
 aux[count[charAt(a[i], d) + 1]++] = a[i];
 for (int i = lo; i <= hi; i++)
 a[i] = aux[i - lo];

 for (int r = 0; r < R; r++)
 sort(a, aux, lo + count[r], lo + count[r+1] - 1, d+1);
}  
```  
## 3-way string quicksor  
```  
private static void sort(String[] a)
 { sort(a, 0, a.length - 1, 0); }
 private static void sort(String[] a, int lo, int hi, int d)
 {
 if (hi <= lo) return;
 int lt = lo, gt = hi;
 int v = charAt(a[lo], d);
 int i = lo + 1;
 while (i <= gt)
 {
 int t = charAt(a[i], d);
 if (t < v) exch(a, lt++, i++);
 else if (t > v) exch(a, i, gt--);
 else i++;
 }
 sort(a, lo, lt-1, d);
 if (v >= 0) sort(a, lt, gt, d+1);
 sort(a, gt+1, hi, d);
 }  
 ```  
 ## Longest repeated substring:  
 ```  
  public String lrs(String s)
 {
 int N = s.length();
 String[] suffixes = new String[N];
 for (int i = 0; i < N; i++)
 suffixes[i] = s.substring(i, N);
 Arrays.sort(suffixes);
 String lrs = "";
 for (int i = 0; i < N-1; i++)
 {
 int len = lcp(suffixes[i], suffixes[i+1]);
 if (len > lrs.length())
 lrs = suffixes[i].substring(0, len);
 }
 return lrs;
 }
