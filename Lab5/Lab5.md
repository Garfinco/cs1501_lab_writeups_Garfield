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

>After I look at the problem I choose the appraoch using substring first, because I did not know ".startsWith()" is a thing when doing the lab in recitation. At first I was think I'm gonna check each folder path by path by looking at its length and each path "/x -> /x -> /x" using sub String. It took way too long to implement using subString. After I discover ".startsWith()", things get a lot easier.

![Project Screenshot](https://github.com/Garfinco/cs1501_lab_writeups_Garfield/blob/main/Lab3/case%203.png)

>Since we already sorted the array, the shorter length folder wwill be at front followed by longer sub folder inside it. So all we need to do is check if the folder after the first one is its sub folder or not. But after I finish implementing it, it gave wrong answer when doing case 3. Looking at case 3 we can see a/b/c and a/b/ca both starts with a/b then .startWith() will think the start with the same folder which causes it removing the a/b/ca folder after a/b/c added to the result. I fix this by adding a "/" when checking with .startsWith() it will check the folder is under a/b/c/ instead of a/b/c.


## Time and Space Complexity
### time:
    O(nlogn) numbers of folder inside the array + the sorting

### Space
    O(n) numbers of folder in array