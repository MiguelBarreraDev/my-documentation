# Tree
Is a nonlinear hierarchical data structure that consists of nodes 
connected by edges.

## Why Tree Data Structure?
- Different tree data structures allow quicker and easier access to the data
- Linear data structure the time complexity increases with the increse in the data
  size

## Tree Terminologies
### Node
- Entity that contains a key or value and pointer to its child nodes
- The last nodes of each path are called **leaf nodes o external node**
- The node having at least a child node is called **internal node**

### Edge
- It is the link between any two nodes

### Root
- It is the topmost node of a tree

### Height of a Node
- Is the numbers of edges from the node to the deepest leaf

### Depth of a Node
- Is the number of edges from root to the node

### Height of a tree
- Is the height of the root or the depth of the deepest node

### Degree of a node
- Is the total number of branches of that node

### Forest
- Is a collection of disjoint trees


## Tree Travversal
Traversing a tree means visiting every node in the tree.
A hierarchical data structure like a tree can be traversed in different ways.

### Inorder
1. First, visit all the nodes in the left subtree
2. Then the root node
3. Visit all the nodes in the right subtree
### Preorder
1. Visit root node
2. Visit all the nodes in the left subtree
3. Visit all the nodes in the right subtree
### Postorder
1. Visit all the nodes in the left subtree
2. Visit all the nodes in the right subtree
3. Visit the root node


## Types of tree
- Binary Tree
- Binary Search Tree
- AVL Tree
- B-Tree
