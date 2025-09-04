#### Remove duplicates from Sorted Array
```java
class Solution {
    // Function to remove duplicates from the given array.
    ArrayList<Integer> removeDuplicates(int[] arr) {
        // code here
        int i = 0;
        int j = i+1;
        int n = arr.length;
        ArrayList<Integer> list = new ArrayList<>();
        while(i<n){
            list.add(arr[i]);
            
            while(j<n && arr[i]==arr[j] ){
                j++;
            }
            
            i = j;
            j = i+1;
        }
        return list;
    }
}
```
