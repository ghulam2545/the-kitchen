# Bubble Sort

Bubble sort is a simple sorting algorithm that repeatedly steps through a list of items to be sorted, compares adjacent elements and swaps them if they are in the wrong order. The pass through the list is repeated until the list is sorted.

The algorithm gets its name from the way smaller elements "bubble" to the top of the list as it is being sorted. Here's how it works:

1. Starting from the first element, compare each pair of adjacent elements.
2. If the elements are in the wrong order, swap them.
3. Move to the next pair of adjacent elements and repeat step 2.
4. Continue this process until no more swaps are needed. At this point, the list is sorted.

```cpp
#include <iostream>
using namespace std;

void bubble_sort(int arr[], int n) {
    for (int i = 0; i < n - 1; ++i) {
        for (int j = 0; j < n - 1 - i; ++j) {
            if (arr[j] > arr[j + 1]) {  // for decreasing chage ">" to "<"
                swap(arr[j], arr[j + 1]);
            }
        }
    }
}

int main() {
    int n = 0;
    cin >> n;

    int arr[n];
    for (int i = 0; i < n; ++i) cin >> arr[i];

    bubble_sort(arr, n);
    for (int i = 0; i < n; ++i) cout << arr[i] << ' ';

    return 0;
}
```

> Time Complexity: O(n^2)
>
> Space Complexity: O(1)
