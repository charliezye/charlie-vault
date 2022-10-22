## Binary Search Trees
#### Goals 
The following goals are general goals included as an outline every data structure. Some data structures may have sections that are different than the goals shown here.
1) Understand the structure of each and how they conceptually function
2) Learn how to implement the data structure itself
3) Learn how basic operations function, how to implement them, and their space/time complexity
	1) Traversal
	2) Insertion    
	3) Deletion
	4) Searching
	5) Sorting
	6) Merging
4) More Complex Operations
5) Other factors to consider
6) Understand what they are good and bad at and when to use them

---

### 1) Structure/Function

AKA digital tree or prefix tree

A trie is a type of k-ary search tree used for storing and searching a specific key from a set. Search complexities can be brought to their optimal limit with these, the key length.

- A well balanced BST has search time proportional to M * log N, where M is the maximum string length and N is the number of keys in the tree
- Using Trie, the key can be searched in O(M) time. 

#### Structure Specifics
- Every node in a Trie consists of multiple branches, each branch a possible character of keys
- Mark the last node of every key as the end of word node
	- A Trie node field isEndOfWord is used to distinguish this

The main issue with a trie is that it has a memory requirement of **O(ALPHABET_SIZE * key_length * N)** where N is the number of keys in Trie.
- There are more efficient representations of nodes such as compressed tries/, ternary search trees, etc. to minimize this

### 2) Implementation
How to implement a Trie Data Structure?
1. Create a root node with the help of TrieNode() constructor.
2. Store a collection of strings that have to be inserted in the trie in a vector of strings say, arr.
3. Insert all strings in Trie with the help of the insert() function

### 3) Basic Operations

#### Insertion
###### O(key_length)
1. Every char of input key is inserted as an individual node
	- Note the children are an array of pointers to next-level trie nodes
2.  Key character acts as index to array children
3. If input key is new or extension of existing key, construct non-existing (char) nodes and mark end of word field for last node of key
4. If input key is prefix of existing key in Trie, siomply mark last node of key as the end of a word

- Key length determines Trie depth

###### Code
```
 // If not present, inserts key into trie
    // If the key is prefix of trie node,
    // just marks leaf node
    static void insert(String key)
    {
        int level;
        int length = key.length();
        int index;
      
        TrieNode pCrawl = root;
      
        for (level = 0; level < length; level++)
        {
            index = key.charAt(level) - 'a';
            if (pCrawl.children[index] == null)
                pCrawl.children[index] = new TrieNode();
      
            pCrawl = pCrawl.children[index];
        }
      
        // mark last node as leaf
        pCrawl.isEndOfWord = true;
    }
```

#### Searching
###### O(key_length)
1. Similar to insert, but only compares chars and moves down
2. Search can terminate due to end of string or lack of key in trie
	- If end of string and isEndofWord of last node is true, then key exists in trie
	- If lack of key then search terminates without checking all chars of key

###### Code
```
    // Returns true if key presents in trie, else false
    static boolean search(String key)
    {
        int level;
        int length = key.length();
        int index;
        TrieNode pCrawl = root;
      
        for (level = 0; level < length; level++)
        {
            index = key.charAt(level) - 'a';
      
            if (pCrawl.children[index] == null)
                return false;
      
            pCrawl = pCrawl.children[index];
        }
      
        return (pCrawl.isEndOfWord);
    }
      
```

#### Delete

