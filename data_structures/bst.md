# Binary Search Tree

A data structure that has O(logn) search time for **find**, **insert** & **delete**. At the head is a root node, with at most 2 children. Everything in the left sub tree has to be less than or equal to the root node, and everything in the right sub tree has to be greater than the root node. Each sub tree is also a BST. 

## Find

* We are only given the root, so first thing is check if the value on the node is equal to the value of the root. Depending on the value, we either go left or right, if there are any children that aren't null. We will eventually either find the value and return true, or there will be no more children and we return false. 

## Insert

* Depending on value, the new node can either be at the left or right of the root. If it's bigger for example, we check to see if there's a right child. If there is, we make the same comparison we did before, only with the right child. Eventually there will be a place where there is no child, and that where the node will be inserted.

## delete

* if node to be deleted doesn't have kids it's pretty easy, we just delete the node's parent pointer that's pointing to it.

* if it has just one child, then this child takes its place. If it has 2 children, then take the largest child from the left subtree(or smallest from right subtree) and that's the new node. By definition, since this is the max on the left subtree, it can only have a right child, so if it does then this right child takes the node's place.

## balanced

* a balanced tree will have a logn depth, and the following properties
    * the difference between the left and right subtree is at most 1
    * both the left and right subtrees are also balanced
    * 
