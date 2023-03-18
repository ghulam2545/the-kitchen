## Binary Search

Binary search is a search algorithm used to find the position of a specific value in a sorted array or list. The idea behind binary search is to repeatedly divide the search interval in half until the target value is found, or until the interval is empty.

The algorithm works by first comparing the target value with the middle element of the array. If the target value is equal to the middle element, the search is complete. If the target value is less than the middle element, the search continues in the lower half of the array. If the target value is greater than the middle element, the search continues in the upper half of the array. This process is repeated until the target value is found or the interval is empty.


```cpp
#include <iostream>
using namespace std;

// returns index of specified key or -1 for not found
int binary_search(int arr[], int n, int key) {
    int low = 0, high = n - 1;
    int mid = 0;
    int res = -1;

    while (low <= high) {
        mid = low + (high - low) / 2;  // to avoid overflow
        if (arr[mid] == key)
            return mid;
        else if (key < arr[mid]) {
            high = mid - 1;
        } else {
            low = mid + 1;
        }
    }
    return res;
}

int main() {
    int n = 0;
    cin >> n;
    int arr[n];
    for (int i = 0; i < n; ++i) cin >> arr[i];

    int key = 0;
    cin >> key;

    cout << binary_search(arr, n, key);

    return 0;
}
```

> Time Complexity: O(logn)
>
> Space Complexity: O(1)