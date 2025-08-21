### Given a sorted array. The task is to convert it into a Balanced Binary Search Tree (BST). Return the root of the BST.

````java
class Solution {
    public Node construct(int l,int h,int [] nums){
        //return ab root end ho jaye
        if(l>h) return null;
        //cal mid 
        int mid = (l+h)/2;
        //root node banao
        Node n = new Node(nums[mid]);
        //connect left part to root left
        n.left = construct(l,mid-1,nums);
        //connect right part to root right
        n.right = construct(mid+1,h,nums);
        //return tree
        return n;
    }
    public Node sortedArrayToBST(int[] nums) {
        // Code here
        return construct(0,nums.length-1,nums);
    }
}
