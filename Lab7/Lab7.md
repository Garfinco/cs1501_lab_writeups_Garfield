# Lab 7 - Garfield Zhang

## Sloution
```
class Solution {
    public int[][] floodFill(int[][] image, int sr, int sc, int color) {
        int start = image[sr][sc];

        if (start == color) {
            return image;
        }

        changeColor(image, sr, sc, color, start);

        return image;
    }

    public void changeColor (int[][] image, int r, int c, int color, int start){
        if(r < 0 || c < 0 || r >= image.length || c >= image[0].length){
            return;
        }
        if (image[r][c] != start) {
            return;
        }

        if(image[r][c] == start){
            image[r][c] = color;
        }

        changeColor(image, r-1, c, color, start);
        changeColor(image, r, c-1, color, start);
        changeColor(image, r+1, c, color, start);
        changeColor(image, r, c+1, color, start);
    }
}
```


## Expalin

The problem want use the fill the 2D array from a starting point and fill all the same color block that is its neighbor repeat this process till the arrays is filled.

My appraoch is using a recursive helper emthod where it checked current index if it is the same as the satrting index color if yes change it to the desiered color and use call the helper again to four different directions (all neighbors).
> How it runs
1. check if the starting index color is already the color we want if so return the array since there is no point of filling it anymore we will just end up searching for all the color that is the color we want and do nothing
2. call the recursive helper where it check if we need to change the current index's color or not (same color as starting index? if yes change it), then recursively check all its neighbor

## Time and Space Complexity
### time:
    R - rows
    C - columns
    O(R*C*4) = O(R*C)

### Space
    Same idea as runtime big O since we using 4 recursive call of a 2D array
    O(R*C)