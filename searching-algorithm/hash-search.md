## Hash Search

A hash/hash table search is a method of searching for a specific element or key in a data structure called a hash table. A hash table is a data structure that stores key-value pairs, where the keys are hashed into indices of an array, allowing for efficient lookup of values based on their corresponding keys.

To perform a hash table search, the key is first hashed using a hash function, which returns the index of the array where the corresponding value is stored. The value at that index is then checked to see if it matches the search key.


```cpp
#include <iostream>
#include <unordered_map>
using namespace std;

// returns true if specified key is found otherwise false
bool hash_search(unordered_map<int, bool>& mp, int key) { return mp[key]; }

int main() {
    int n = 0;
    cin >> n;

    int val = 0;
    unordered_map<int, bool> mp;
    for (int i = 0; i < n; ++i) {
        cin >> val;
        mp[val] = true;
    }
    int key = 0;
    cin >> key;

    cout << hash_search(mp, key);

    return 0;
}
```

> Time Complexity: O(1) (average case)
>
> Space Complexity: O(1)
