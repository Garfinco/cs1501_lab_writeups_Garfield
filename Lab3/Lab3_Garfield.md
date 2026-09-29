# Lab 2 Garfield Zhang 

## Sloution
```
class Solution {
    public List<String> removeSubfolders(String[] folder) {
        List<String> folder_list = new ArrayList<>();
        // sort the array first
        Arrays.sort(folder);
        folder_list.add(folder[0]);
        int cur_list = 0;

        for(int i = 1; i < folder.length; i++){ 
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
   

## Time and Space Complexity

### time:
    

### Space
  