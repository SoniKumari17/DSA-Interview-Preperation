#### aproach-1
```java
class Solution {
    public int[] rearrangeArray(int[] nums) {
        int n = nums.length;
        ArrayList<Integer> pos = new ArrayList<>();
        ArrayList<Integer> neg = new ArrayList<>();

        for(int i = 0;i<n;i++){
            if(nums[i]>0) {
                pos.add(nums[i]);
            }else{
                neg.add(nums[i]);
            }
        }

        for(int i = 0;i<n/2;i++){
            nums[2*i] = pos.get(i);
            nums[2*i+1] = neg.get(i);
        }
        return nums;
    }
}
```
#### Aproach 2
```java
class Solution {
    public int[] rearrangeArray(int[] nums) {
        int n = nums.length;
        int [] res = new int[n];
        int P = 0;
        int N = 1;
    
        for(int i = 0;i<n;i++){
            if(nums[i]>0) {
                res[P] = nums[i];
                P += 2;
            }else{
                res[N] = nums[i];
                 N += 2;
            }
        }
        return res;
    }
}
```
