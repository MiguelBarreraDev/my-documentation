# Binary Tree

Is a tree data structure in which each parent node can have at most
two children.
Each node of a binary tree consists of three items:
- Data item
- Address of left child
- Address of right child
- Address of the parent

## Types of Binary Tree

### Full Binary Tree
- Every parent node has either two or no children
- Algotihm
```c
bool isFullBinaryTree(struct Node *root)
{
  if (!root)
    return (false);

  if (!root->left && !root->right)
    return (true);

  if (root->left && root->right)
    return (isFullBinaryTree(root->left) && isFullBinaryTree(root->right));

  return (false);
}

```
### Perfect Binary Tree
- Every node has exactly two child nodes
- All leaf nodes are at the some level
- Algotihm
```c
bool isPerfect(struct node *root, int depth, int level)
{
  if (!root)
    return (false);

  if (!root->left && !root->right)
    return (depth == level)

  if (!root->left || !root->right)
    return (false);

  return (isPerfect(root->left) && isPerfect(root->right));
}
```

### Complete Binary Tree
- All the leaf element must lean towards the left
- The last leaf element might not have a right siblign
- How a complete Binary Tree is Created?
```c
/**
 * 0. from an array -> [0, 1, 5, 7, 8]
 * 1. The first element to be the root node
 * 2. Second element as a left child of the root node
 * 3. Third element as the the right child
 * 4. The next two element as children of the left node of the second level
 * 5. The next two element as children of the right node of the second level
 * 6. Keep repeating until you reach the las element
 */
              0
            1   5
          7   8
```
- Algotihm
```c
bool isComplete(struct node *root, index, numberNodes)
{
  if (!root)
    return (true);

  if (index >= numberNodes)
    return (false);

  return (isComplete(root->left, 2 * index + 1, numberNodes) && isComplete(root->right, 2 * index + 2, numberNodes));
}
```
- Relationship between array indexes and tree element
  If the  index of any element in the array is _i_
  - Left child: 2i + 1
  - right child: 2i + 2
  - parent: lowerBound((i-1)/2)


### Balanced Binary Tree
- The difference between the height of the left and the right subtree
  for each node is either 0 or 1
