# 1: Introduction

My design is a player inventory for a video game. For each item in the inventory, information must be stored on its name and the quantity of the item in the inventory. It will be built atop a ``HashTable<string, unsigned int>.``

# 2: Design Philosophy

The client of this inventory system would be a hypothetical game company developing a winter survival game. The user would be the players of the mentioned game. The multiset would be used to track the inventory of the player as well as any other inventories in the game. They want something relatively simple and efficient, as there is concern over a large number of inventory items causing excessive lag. They want it to be easily modified in the future, as features such as weight tracking are expected to be implemented at a later date.

The game being developed has save states, and as such the player inventory system must have a way to save and load inventory data from memory, otherwise it will not be useable for its intended purpose. 

# 3: Core Operations

### bool contains(string name)
* **Purpose:** Checks if a given string is associated with a value in the multiset. Allows the game to check if the player has an item, for example if a player attempts to open a door, the game may check first to see if the player’s inventory contains a key to the door. Returns true if the name is in the multiset, and false otherwise. 
* **Possible Edge Cases:** In theory this method shouldn’t need much handling of edge cases since if the name is not found, the method will simply return false. 
* **Time Complexity:** should typically be O(1), O(n) in worst case
* **How the data structure supports/constrains this operation:**

### unsigned int get(string name)
* **Purpose:** get returns the quantity associated with a given item. Allows you to check how much of an item the player inventory has when you only have the name of the item. 
* **Possible Edge Cases:** Because it is possible that a name will be given which is not contained in the multiset, the method must be able to handle not being able to give a proper return value, likely via ‘std::optional.’
* **Time Complexity:** Should be O(1)
* **How the data structure supports/constrains this operation:** HashTables have a generally better search time complexity than AVLTrees and sequences, meaning hashtables support this operation. 

### bool addItem(string name, int quantity)
* **Purpose:** Adds an item to the inventory. Needed to populate the inventory. Used by the game whenever a player picks up an item. Int quantity will default to 1. Returns false if an item could not be added. 
* **Possible Edge Cases:**  someone attempting to add a negative quantity of items will likely be problematic, so to deal with this the input will not be accepted unless it is positive. 
* **Time Complexity:** should typically be O(1), O(n) in worst case
* **How the data structure supports/constrains this operation:** Hashtables have a generally better time complexity than AVLTrees and sequences for simple insertion. Resizing the hashtable will need to happen occaisonally, however in this case occasional momentary dips in performance are acceptable. 


### bool removeItem(string name, int quantity)
* **Purpose:** Removes a designated number of a specified item from the inventory. If no quantity is given, it will remove all of that item from the inventory. Used by the game whenever the player drops an item or triggers any other event that could cause inventory items to be removed or consumed in the future.
* **Possible Edge Cases:** Someone could attempt to remove a negative amount of items, likely resulting in gameplay errors later down the line. An additional potential edge case is someone attempting to remove more of an item than currently exists. In both cases, the method will simply return false before removing the item to prevent potential issues. 
* **Time Complexity:** should typically be O(1), O(n) in worst case.
* **How the data structure supports/constrains this operation:** Hashtables have a generally better time complexity than AVLTrees and Sequences for simple removal. Resizing the hashtable will need to happen occaisonally, however in this case occasional momentary dips in performance are acceptable. 

### int size()
* **Purpose:** Allows you to check the size of the multiset. Useful when iterating through the multiset. Allows checking the size without creating a local list of all elements in the multiset.
* **Possible Edge Cases:** since no user input is provided, there shouldn't be any major edge cases. 
* **Time Complexity:** Should be an average of O(1) if size is updated during insertions and deletions.
* **How the data structure supports/constrains this operation:** Using hashtables likely doesn't meaningfully impact the performance of this method, since any data type could likely utilize a similar counter to keep track of size. 

# 4: Set Operations

## union_with()
* **Purpose:** union_with() is a set operation which will be used to quickly combine two different inventories. This will be implanted so that later on the developers can add a button which instantly transfers all items in a different inventory to the player’s inventory. 

* **Possible edge cases:** As long as logic for adding items is implemented properly there should be no issues. 

* **Time Complexity:** should be O(n + m) where n and m are the number of elements in each inventory. 

* **How the data structure supports/constrains this operation:** Hashtable has an insert which are on average faster than insertion in sequences and AVL trees, though in this case performance gain may be less great due to the operation likely causing at least 1 resize in the new multiset.

## intersection_with()
* **Purpose:** Intersection_with() is a set operation which will be used to allow the player to quickly take items from another inventory if they already have that item in their inventory. This allows common items like arrows to be quickly added to the players inventory. 

* **Possible edge cases:** As long as logic for adding items is implemented properly there should be no issues. 

* **Time Complexity:** should be O(n + m) where n and m are the number of elements in each inventory. 

* **How the data structure supports/constrains this operation:** Hashtable has an insert which are on average faster than insertion in sequences and AVL trees, though in this case performance gain may be less great due to the operation likely causing at least 1 resize in the new multiset.

# 5: Extension Feature

## serialize() / deserialize()

# 6: UML Diagram

# 7: Trade-off Analysis

# 8. Alternative Design Outline

# 9. Evaluation Plan

# 10. Conclusion

# References
