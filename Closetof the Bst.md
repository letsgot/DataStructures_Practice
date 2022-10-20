Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

Given target value is a floating point.
You are guaranteed to have only one unique value in the BST that is closest to the target.



Using Binary search 
public int closestValue(TreeNode root, double target) {
        // write your code here
        int val,closet = root.val;

        while(root!=null){
            val = root.val;
            closet = (Math.abs(val - target) < Math.abs(target - closet)) ? val:closet;
            root = val<target ? root.right : root.left;
        }

        return closet;
}
