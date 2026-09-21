# Lab 2 Garfield Zhang 

## Sloution
class Solution {
    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
        if (root1 == null) return root2;
        if (root2 == null) return root1;

        root1.val += root2.val;

        root1.left = mergeTrees(root1.left, root2.left);
        root1.right = mergeTrees(root1.right, root2.right);

        return root1;
    }
}

## Expalin
    Used recursion to solve the problem. It took me a while during Lab because I misdunderstood the reuqirement after that I came up wiht this pretty clean and simple code. It adds both node togther when both nodes exist which merge them together creating the new merged node in this case root 1 will be the merged tree at the end. If one of the nodes is null it will simply return the other one, if both are null it will just end up creating a null node.

## Time and Space Complexity

### time:
    Worst case O(n), n is the number of nodes of both trees
    Best case O(m), m when all the nodes that overlaps no null nodes

### Space
    O(h): height of the tree