#### 1.find k closest elements 
https://leetcode.com/problems/find-k-closest-elements/description/
#### Solution Binary Search: 
````java 
class Solution {
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        List<Integer> closestList = new ArrayList<>();
        int left = 0;
        int right = arr.length - k;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (x - arr[mid] > arr[mid + k] - x) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        for (int i = left; i < left + k; i++) {
            closestList.add(arr[i]);
        }
        return closestList;
    }
}
````

}
