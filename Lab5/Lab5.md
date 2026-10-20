# Lab 5 - Garfield Zhang

## Sloution
```
public class LZW {
    private static int R = 256; // number of input chars
    private static int W = 9; // codeword width
    private static int L = (int)Math.pow(2, W); // number of codewords = 2^W

    public static void compress() {
        W = 9;
        L = (int) Math.pow(2, W);

        String input = BinaryStdIn.readString();
        TST<Integer> st = new TST<Integer>();
        for (int i = 0; i < R; i++)
            st.put("" + (char) i, i);
        int code = R + 1; // R is codeword for EOF

        while (input.length() > 0) {
            String s = st.longestPrefixOf(input); // Find max prefix match s.

            BinaryStdOut.write(st.get(s), W); // Print s's encoding.

            if (code >= L && W < 16) {
                W++;
                L = (int) Math.pow(2, W);
            }

            int t = s.length();
            if (t < input.length() && code < L) // Add s to symbol table.
                st.put(input.substring(0, t + 1), code++);
            input = input.substring(t); // Scan past s in input.

            
        }
        BinaryStdOut.write(R, W);
        BinaryStdOut.close();
    }

    public static void expand() {
        W = 9;
        L = (int)Math.pow(2, W);

        String[] st = new String[(int) Math.pow(2, 16)];
        int i; // next available codeword value
        // initialize symbol table with all 1-character strings
        for (i = 0; i < R; i++)
            st[i] = "" + (char) i;
        st[i++] = ""; // (unused) lookahead for EOF

        int codeword = BinaryStdIn.readInt(W);
        if (codeword == R)
            return; // expanded message is empty string
        String val = st[codeword];

        while (true) {
            

            BinaryStdOut.write(val);
            
            if(i >= L && W < 16){
                W++;
                L = (int)Math.pow(2, W);
            }

            codeword = BinaryStdIn.readInt(W);
            if (codeword == R)
                break;
            String s = st[codeword];
            if (i == codeword)  
                s = val + val.charAt(0); // special case hack
            if (i < L)
                st[i++] = val + s.charAt(0);
            val = s;
        }
        BinaryStdOut.close();
    }
}
```


## Expalin

The overall idea of the solution is simply checking if the symbol table size "int L" is full nor not, if it is we add the W(width) by one bit.

Compress and expand both check if we need to increment the width and symbol table for next code word before we adds the current code word in. One problem I ran into is where to put the increment check I still don't understand why I need to put it after I created the current code word and before I put it in the symbol table. The other problem is I forgot to initiallize L and W to 9 in compress since they are global variables.


## Time and Space Complexity
### time:
    compress O(N^2); cause of subString()
    expand O(N); number of codewords in symbol table;

### Space
    compress size of file and dictionary O(FD);
    expand size of dictioanry and its reference array O(D);