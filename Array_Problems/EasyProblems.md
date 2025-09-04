#### 1.Remove duplicates from Sorted Array
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
#### 2.Left Rotate an Array By D place :
```java 
class Solution {
    void leftRotate(int[] arr, int d) {
        int n = arr.length;
        d = d % n; // in case d > n

        while (d > 0) { 
            int temp = arr[0];
            
            // shift all elements left by 1
            for (int i = 1; i < n; i++) { 
                arr[i - 1] = arr[i]; 
            }
            
            arr[n - 1] = temp; // put first element at the end
            d--; // reduce rotations
        }
    }
}
```
#### 🔹 Approach 2: Using Extra Array

 Store first d elements in a temp array, shift the rest, then put temp at the end.

##### Steps

Save first d elements in temp.

Shift remaining n-d elements left.

Copy temp elements at the end.
```java
class Solution {
    void leftRotate(int[] arr, int d) {
        int n = arr.length;
        d = d % n;
        int[] temp = new int[d];
        
        // Step 1: Copy first d elements
        for (int i = 0; i < d; i++) {
            temp[i] = arr[i];
        }
        
        // Step 2: Shift remaining elements
        for (int i = d; i < n; i++) {
            arr[i - d] = arr[i];
        }
        
        // Step 3: Copy back temp
        for (int i = 0; i < d; i++) {
            arr[n - d + i] = temp[i];
        }
    }
}
Time: O(n)
Space: O(d)
```

#### 🔹 Approach 3: Reversal Algorithm (Best & Famous)

Ye sabse efficient aur interview favourite hai.

##### Steps

Reverse first d elements.

Reverse remaining n-d elements.

Reverse whole array.

#### Example

arr = [1,2,3,4,5,6,7], d=2

Reverse first 2 → [2,1,3,4,5,6,7]

Reverse last 5 → [2,1,7,6,5,4,3]

Reverse all → [3,4,5,6,7,1,2]

```java
class Solution {
    void leftRotate(int[] arr, int d) {
        int n = arr.length;
        d = d % n;
        reverse(arr, 0, d - 1);      // Step 1
        reverse(arr, d, n - 1);      // Step 2
        reverse(arr, 0, n - 1);      // Step 3
    }
    
    void reverse(int[] arr, int l, int r) {
        while (l < r) {
            int temp = arr[l];
            arr[l] = arr[r];
            arr[r] = temp;
            l++;
            r--;
        }
    }
}
Time: O(n)
Space: O(1)
```
#### 3.Move all zeroes to the end
Given:
arr = [0, 1, 0, 3, 12]
Output:
[1, 3, 12, 0, 0]
Order of non-zero elements preserve karna hai

#### Approach 1: Brute Force (Using Extra Array)

Ek new array banao aur pehle saare non-zero copy karo, fir baaki jagah zero bhar do.

##### Steps

Traverse array, non-zero elements ko ek new list me daalo.

Fir baaki positions ko 0 se fill karo.

Copy back agar inplace karna ho.
```java
class Solution {
    void moveZeroes(int[] arr) {
        int n = arr.length;
        int[] temp = new int[n];
        int index = 0;

        // Step 1: Put non-zeros in temp
        for (int i = 0; i < n; i++) {
            if (arr[i] != 0) {
                temp[index++] = arr[i];
            }
        }

        // Step 2: Fill remaining with 0
        while (index < n) {
            temp[index++] = 0;
        }

        // Step 3: Copy back to original
        for (int i = 0; i < n; i++) {
            arr[i] = temp[i];
        }
    }
}
Time: O(n)
Space: O(n)
Not in-place → extra space use hota hai.
```
#### 🔹 Approach 2: Two-Pass In-place

Ek pass me non-zero elements ko front me laao, fir baaki ko 0 fill karo.

Steps

Ek index pointer rakho pos = 0.

Har non-zero element ko arr[pos++] me daalo.

Jab sab non-zero ho gaye, remaining positions ko 0 set karo.
```java
class Solution {
    void moveZeroes(int[] arr) {
        int n = arr.length;
        int pos = 0;

        // Step 1: Put all non-zeros at start
        for (int i = 0; i < n; i++) {
            if (arr[i] != 0) {
                arr[pos++] = arr[i];
            }
        }

        // Step 2: Fill rest with 0
        while (pos < n) {
            arr[pos++] = 0;
        }
    }
}
Time: O(n)
Space: O(1)
```

