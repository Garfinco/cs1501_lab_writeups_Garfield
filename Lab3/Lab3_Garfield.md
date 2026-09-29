
# Lab 3 Garfield Zhang Remove Sub-Folders from the Filesystem

## Sloution
```
class Solution {
    public List<String> removeSubfolders(String[] folder) {
        List<String> folder_list = new ArrayList<>();
        
        // sort the array first
        Arrays.sort(folder);
        
        folder_list.add(folder[0]);
        int cur_list = 0;

        // go through the array checks each folder
        for(int i = 1; i < folder.length; i++){ 

            // add the folder does not start with the folder inside result
            if(!folder[i].startsWith(folder_list.get(cur_list) + "/")){
                folder_list.add(folder[i]);
                cur_list++;
            }
        }
        return folder_list;
    }
}
```

## Expalin
    After I look at the problem I choose the appraoch using substring first, because I did not know ".startsWith()" is a thing when doing the lab in recitation. At first I was think I'm gonna check each folder path by path by looking at its length and each path "/x -> /x -> /x" using sub String. It took way too long to implement using subString. After I discover ".startsWith()", things get a lot easier.
![Project Screenshot](case_3.png)
    Since we already sorted the array, the shorter length folder wwill be at front followed by longer sub folder inside it. So all we need to do is check if the folder after the first one is its sub folder or not. But after I finish implementing it, it gave wrong answer when doing case 3. Looking at case 3 we can see a/b/c and a/b/ca both starts with a/b then .startWith() will think the start with the same folder which causes it removing the a/b/ca folder after a/b/c added to the result. I fix this by adding a "/" when checking with .startsWith() it will check the folder is under a/b/c/ instead of a/b/c.

    


## Time and Space Complexity

### time:
    

### Space
  