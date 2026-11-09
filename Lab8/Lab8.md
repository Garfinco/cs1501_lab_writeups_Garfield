# Lab 8 - Garfield Zhang

## Sloution
```
class Solution {
    public boolean isValid(String s) {
        if(s.length() % 2 != 0){
            return false;
        }

        Stack<Character> c = new Stack<>();

        for(int i = 0; i < s.length(); i++){
            char current = s.charAt(i);

            if(current == '(' || current == '{' || current == '['){
                c.push(current);
                continue;
            }

            // if all the char is ( or [ or {
            if(c.isEmpty()){
                return false;
            }

            switch(current){
                case ')':
                    if(c.peek() == '('){
                        c.pop();
                    } else{
                        return false;
                    }
                    break;
                case '}':
                    if(c.peek() == '{'){
                        c.pop();
                    } else{
                        return false;
                    }
                    break;
                case ']':
                    if(c.peek() == '['){
                        c.pop();
                    } else{
                        return false;
                    }
                    break;
                default:
                    return false;
            }
        }

        return c.isEmpty();
    }
}

```


## Expalin
In a loop we go through all the chrarcter(brackets) in String s. 
1. We use a if statment push all the left bracket into a stack.
2. Then when we see a right bracket we check if the top of the stack has a left bracket that match the current right bracket
3. return true when the stack is empty after the loop (pushed all the left bracket).

I also did the simple check. If the String length is not a even number it must return false, since there will always be a left brakcet missing a right bracket 

## Time and Space Complexity
### time:
    O(N), iterate throught the whole array length = N

### Space
    O(N/2) = O(N) 
    created a stack that stored all the left bracket which is half the the array
    