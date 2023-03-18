## Linear Search

Linear search, also known as sequential search, is a simple algorithm for finding an element within a list of items. It involves examining each item in the list one by one in order until the desired element is found or the end of the list is reached.

The linear search algorithm works by starting at the beginning of the list and comparing each element with the target element. If the element matches the target, the search is successful and the algorithm returns the index of the matching element. If the end of the list is reached without finding the target element, the search is unsuccessful and the algorithm returns a special value (such as -1) to indicate that the element was not found.


```cpp
#include <iostream>
using namespace std;

// returns index of specified key or -1 for not found
int linear_search(int arr[], int n, int key) {
    int res = -1;
    for (int i = 0; i < n; ++i) {
        if (arr[i] == key) return i;
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

    cout << linear_search(arr, n, key);

    return 0;
}
```