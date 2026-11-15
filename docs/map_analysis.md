# Map Analysis Laboratory

## Core goal
The goal of this lab was to implement a custom Map that stores key-value pairs. A map allows us to associate a value with a unique key and retrieve that value when needed. My implementation uses a vector to store the key-value pairs. Each entry contains a string key and an integer value. The entries are kept in alphabetical order by key, which makes the map organized and easier to inspect.

## Required operations

- insert a new key-value pair;
The insert() function adds a new key-value pair to the map. After inserting an entry, it calls sortEntries() to keep the keys in alphabetical order.

- duplicate-Key Prevention
Before inserting a new entry, the function checks whether the key already exists using contains(). If the key is already stored, insertion is rejected and the original value remains unchanged.

- finding Whether a Key Exists
The contains() function uses findIndex() to search for a key. It returns true if the key is found and false otherwise.

- updating an Existing Value
The update() function searches for an existing key and changes its associated value. If the key does not exist, it returns false. Updating a value does not change the size or order of the map.

- removing an Existing Key
The erase() function searches for the requested key and removes its entry from the vector. If the key is not found, it returns false. The remaining entries stay sorted.

- retrieving a Value by Key
The at() functions retrieve the value associated with a key. If the key does not exist, they throw an out_of_range exception. The non-const version returns a reference which allows the stored value to be modified directly.

- listing Keys and Values
The keys() function returns a vector containing all stored keys, while values() returns a vector containing their corresponding values. Both functions preserve the order of the original entries.

- maintaining Sorted Order
The sortEntries() function uses std::sort to arrange entries alphabetically by key. This keeps the map organized after every successful insertion. Removing or updating an entry does not require another sort because neither operation changes the keys.

## Analysis expectations

- average-case time complexity of insertion, lookup, and deletion;
The average-case time complexity of insertion, lookup, and deletion is O(n) in this implementation. Insertion checks whether the key already exists, adds the new entry, and sorts the vector. Lookup searches through the entries using linear search. Deletion also searches for the key before removing it.

- best-case and worst-case behavior;
The best case for searching is O(1), when the requested key is found at the first position. The worst case is O(n), when the key is at the end or does not exist. Insertion also requires searching for duplicates. Also, sorting the vector takes O(n log n) time in the average case. Deletion takes O(n) time because searching and shifting the remaining vector elements may be necessary.

- why duplicate-key handling matters;
Becasue it ensures that every key identifies only one value. Without this rule, the same key could be associated with multiple values, making it unclear which value should be retrieved or updated. My implementation checks for an existing key before inserting a new entry. If the key already exists, the insertion returns false without changing the map.

- the difference between a search by key and scanning all entries;
Searching by key means looking for one specific entry using its key. My implementation uses findIndex() to check entries until it finds a match or reaches the end of the vector. Scanning all entries means visiting every stored entry, such as when generating the complete list of keys or values. Both operations can take O(n) time, but they serve different purposes.

- trade-offs between sorted vectors and hash-based maps;
A sorted vector stores entries together in memory and keeps them organized alphabetically. It is simple to implement and does not require additional data structures for storing entries. However, inserting entries can be expensive because the vector must be sorted again. A hash-based map usually provides average O(1) insertion and lookup when the hash function distributes keys well. However, it does not automatically maintain alphabetical order and requires additional handling for collisions.

- memory overhead and performance of `keys()` and `values()`.
The keys() and values() functions each create a new vector and copy the requested information into it. Both functions take O(n) time and use O(n) additional memory for the returned vector. The original map remains unchanged. These functions are useful when a separate list of all keys or values is needed.

## Big-O focus

- insert() searches for duplicate keys, adds a new entry, and sorts the vector. Sorting makes the average complexity O(n log n). The worst case is O(n²) when sorting requires quadratic time.

- contains() uses linear search to find a key. Its average and worst-case complexity are both O(n).

- update() searches for the key and changes its value if found. Its complexity is O(n).

- erase() searches for the key and removes the entry. Removing an element may also require shifting other elements, so its complexity is O(n).

- at() searches for the requested key and returns its value. Its complexity is also O(n).

- keys() visits every entry and copies each key into a new vector. Its complexity is also O(n).

- values() visits every entry and copies each value into a new vector. Its complexity is O(n).

Map can store and manage key-value pairs using a vector. Keeping the entries sorted makes the data organized, while duplicate prevention ensures that each key remains unique. Even though this implementation is simple and easy to understand, searching and updating entries can take O(n) time. A hash-based map could provide faster average-case lookups, while a balanced search tree could maintain sorted keys with O(log n) search, insertion, and deletion.
