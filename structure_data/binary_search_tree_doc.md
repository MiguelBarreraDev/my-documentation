# Binary Search Tree
- Quickly allows us to maintain a sorted list of numbers
- It is called binary tree because each tree node has a maximun of two children
- It is called a search tree because it can be used to search a number in O(log(n)) time

## Properties
1. All nodes of left subtree are less than the root node
2. All nodes of right subtree are more than the root node
3. Both subtrees of each node are also BSTs

## Basic Ooperations

### Search Operation
- If the value is below the root, we need to only search in the left subtree
- If the value is above the root, we need to only search in the right subtree
```c
node *searchData(struct node *root, int number)
{
  if (!root)
    return (NULL);

  if (number == root->data)
    return (root);

  if (number < root->data)
    return searchData(root->left)
  
  if (number > root->data)
    return searchData(root->right)
}
```
- If the value is found in any of the subtrees, it is propagated up so tha in
  the end it is returned
- If the value is not found, Null is returned
### Insert Operation
- We keep going to either right subtree or left subtree depending on the value
- When we reach a point left or right subtree is null, we put the new node there
```c
node *insertData(node *node, data)
{
  if (node == NULL)
    return (createNode(data));

  if (data < node->data)
    node->left = insertData(node->left, data);
  
  if (data > node->data)
    node->right = insertData(node->right, data);

  return (node);
}
```
- We still have to exit from the function without doing any changes to the rest of the tree
  - In the case of NULL, the newly created node is returned and attached to the parent node
  - Otherwise the same node is returned without any change as we go up until we return to the root

### Deletion Operation
- Case 1: The node is the leaf node
  1. Simmply delete the node from the tree
- Case 2: The node has a single child node
  1. Replace that node with its child node
  2. Remove the child node from its original position
- Case 3: The node has two children nodes
  1. Get the inorder successor of that node
  2. Replace the node will the inorder successor
  3. Remove the inorder successor from its original position

## URL's
- https://www.programiz.com/dsa/binary-search-tree
