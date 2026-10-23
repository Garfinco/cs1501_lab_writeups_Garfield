# Lab 6 - Garfield Zhang

## Sloution
```
class Solution {
    public int findJudge(int n, int[][] trust) {
        int judge = trust[0][1];
        for (int i = 1; i < trust.length; i++){
            if(i == judge){
                continue;
            }
            if(trust[i][1] != judge){
                return -1;
            }
        } 
        return judge;
    }
}
```


## Expalin

Pretty simple solution the goal is finding the person who meets both condtion
* that person trusts nobobdy -  so there will be no relationship at trust[that person].
* everybody else trust him - so every other trust[x][1] will be that person's int label

So in my solution I just used a loop iterate through the trust[] array with two conition
* if it is the judge skip 
* if somebody trust a different person than others return -1 there is no judge exist 



## Time and Space Complexity
### time:
    O(N) 
    the length of the array we have to go through the whole array to know is there a judge that everybody trusts

### Space
    O(N)
    the size of the array trust