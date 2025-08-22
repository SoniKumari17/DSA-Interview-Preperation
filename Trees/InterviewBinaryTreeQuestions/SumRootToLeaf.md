
https://leetcode.com/problems/sum-root-to-leaf-numbers/?envType=study-plan-v2&envId=top-interview-150
```java
class Solution {
    int sum = 0;
    public int sumNumbers(TreeNode root) {
        getPathSum(root,0);
        return sum;
    }
    public void getPathSum(TreeNode root,int currentNumber){
          if(root == null) return ;

          currentNumber = currentNumber * 10 + root.val;
          if(root.left == null && root.right == null){
            sum += currentNumber;
            return;
          }
          getPathSum(root.left,currentNumber);
          getPathSum(root.right,currentNumber);
    }
}
