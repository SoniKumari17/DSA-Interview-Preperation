https://leetcode.com/problems/binary-search-tree-iterator/description/?envType=study-plan-v2&envId=top-interview-150
```java
class BSTIterator {
    List<Integer> list = new ArrayList<>();
    int index = -1;
    public BSTIterator(TreeNode root) {
        inorder(root);
    }
    public void inorder(TreeNode root){
        if(root==null) return ;
        inorder(root.left);
        list.add(root.val);
        inorder(root.right);
    }
    public int next() {
        if(index==-1){
            index = 0;
            return list.get(index);
        }
        index = index + 1;
        return list.get(index);
    }
    
    public boolean hasNext() {
        if(index==list.size()-1){
            return false;
        }
        return true;
    }
}
