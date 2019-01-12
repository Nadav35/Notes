# Linked List
A linked list is a data strucure that consists of a series of nodes that are connected to eachother by instance variable @next_node. Each node holds a value and a pointer to the next node (or nil for the last node).
* Abstract data Type (ADT)
* There is also a doubly linked list which implies that each node should also hold a pointer to the previous node
* Linked lists will ultimately be used in lieu of arrays for our HashMap buckets.
* Linked List API
  * `#first`
  * `#empty?`
  * `#append(key, val)`
  * `#update(key, val)`
  * `#get(key)`
  * `#include?(key)`
  * `#remove(key)`