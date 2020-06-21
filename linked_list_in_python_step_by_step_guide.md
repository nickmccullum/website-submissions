# Linked Lists in Python:  A Step-by-Step Guide

## Linked Lists: A Quick Example
    

A linked list is a way of storing values or elements, which is also known as a data structure. Unlike in arrays or lists where elements are stored next to each other, linked lists hold the value and a pointer to the next node in its structure. In order to visualize this better, consider the following figure.

![](https://lh6.googleusercontent.com/hfZMMGmxwASr0VnDa8rSgS1oLwZ7LV4W9VfV9bKEXPgKySt_9rQHuuFNvwTbSgA_hAJ3hZuxnmC_obbJ9ZFDgiX7lCbuJVpyvOUiuwhWBc58gcX65GTs0MCsKJkHKOwA3ecSdKQ)

The above is a simple way to visualize a linked list. It is also called a singly linked list and can only be iterated in one direction. It has three nodes with the values 12, 99, and 37. Each node also has a pointer referring to each succeeding element. The first node is called the head and it is where iterations through the linked list have to be started. As the last node has no succeeding node, it points to null.

In practice, linked lists can be used as a foundation to implement other data structures such as lists/arrays, stacks, and queues. They also can be implemented without the foundation of linked lists but it is a common practice to do so.

Now let us look into the fundamentals of Linked Lists.

## Fundamentals of Linked Lists
    

From a more technical standpoint, a linked list can be called a linear data structure that consists of a collection of nodes. In its most fundamental form, a node has its data element and a pointer to the subsequent node in the linear collection. The way linked lists are stored in the memory are not governed by their physical placement and therefore, elements can be inserted or deleted efficiently from anywhere in the sequence.

![](https://lh3.googleusercontent.com/PBzwbvpdnvgOImjDmss2jAZz0LuBDHU06BPqCiZIuir85UddNx586cNOzXtCWjg_zILnNv_v4ehuAMa76IunB7W0Tw7X9PNdQIr29rFI-WRCEXGcVYKLl69wE3hQWQA32ocH6iI)

The above is how a node looks like. A node always has its data and pointer values. In more advanced linked lists such as doubly linked lists, there could be another pointer referring to its preceding node. Therefore, they can be iterated in both ways. However, we will learn about singly linked lists first.

## Let’s Practice in Python
    

Now we know that linked lists consist of nodes and each node has a data value and a pointer value to the next node. We also learned that the first element of a linked list is known as its head. Let us implement all that knowledge into Python code.

### Creation of a Linked List
    

In the following, we have created a simple Node class and a Linked List class to implement a singly linked list in our code.
```python
class  MyNode:
	def  __init__(self, data=None):
		self.data = data
		self.next_node = None
	def  set_next_node(self, next_node):
		self.next_node = next_node
	def  get_next_node(self):
		return  self.next_node
class  MyLinkedList:
	def  __init__(self):
		self.head = None
	def  set_head(self, head):
		self.head = head
	def  get_head(self):
		return  self.head
```
  

MyNode class denotes the Node class and MyLinkedList denotes the Linked List class we have created.

Let us now create a college of triangle numbers using nodes and then create a linked list. We will use the first five triangle numbers, 0, 1, 3, 6, 10.

Let’s first create the nodes for demonstration purposes.
```python
node_1 = MyNode(0)
node_2 = MyNode(1)
node_3 = MyNode(3)
node_4 = MyNode(6)
node_5 = MyNode(10)
```
  

Create a linked list and set its head to be the first node.
```python
my_tri_nums = MyLinkedList()
my_tri_nums.set_head(node_1)
```
  

Now we have a linked list with one node. If we request for its pointer to the next node, we will not get an output as there is no node in the head which is pointed towards another.

`my_tri_nums.get_head().get_next_node()`

  

This gives no output.

Let us fix that and point node_1 to node_2.

`node_1.set_next_node(node_2)`

  

Run the previous code again now.

`my_tri_nums.get_head().get_next_node()`

  

Output:

`<__main__.MyNode at 0x160d9526b88>`

  

We can perceive that there indeed is an element in the head in which is pointing.

Let us verify the node by requesting for the data it is storing.

`my_tri_nums.get_head().get_next_node().data`

  

Output:

`1	`

  

Likewise, we can set the remaining nodes to point to the successive triangular numbers.
```python
node_2.set_next_node(node_3)
node_3.set_next_node(node_4)
node_4.set_next_node(node_5)
```
  

Let us get the 5th triangular number by traversing through the linked list we have created.

`my_tri_nums.get_head().get_next_node().get_next_node().get_next_node().get_next_node().data`

  

Output:

`10`

  

There we have created our own linked list.

### Traversing Through a Linked List
    

Now let us see how we can print the whole linked list at once.

Let us add a new function to our MyLinkedList class.
```python
def  print_all(self):
	current_node = self.head
	while current_node is  not  None:
		print(current_node.data)
		current_node = current_node.next_node
```
  

Let us go through all the steps we did before and then now print the whole linked list.

`my_tri_nums.print_all()`

  

Output:
```
0
1
3
6
10
```
  

### Inserting Items into a Linked List
    

Insertion of new elements into a Linked List is just as simple as changing the pointer value referring to the new node. We have three use cases for the insertion.

#### Inserting at the beginning
    

In this scenario, we are adding another element before the existing head of the linked list. In order to successfully add the item, we have to perform the following two steps.

1.  Set the pointer of the new element to the existing head of the linked list.
    
2.  Set the new element as the new head of the linked list.
    

Let us perform those two steps in our code.

We will first create a node_0 variable with the data value of -1 to add to our my_tri_num linked list.

`node_0 = MyNode(-1)`

  

Now we will point it to the existing head of the linked list.

`node_0.set_next_node(my_tri_nums.get_head())`

  

We will now replace the existing head with node_0.

`my_tri_nums.set_head(node_0)`

  

We can now print our updated list and confirm the insertion.

`my_tri_nums.print_all()`

  

Output:
```
-1
0
1
3
6
10
```
  

We can include all the above steps in one function as follows and include in our My_Linked_List class.
```python
def  insert_node_beg(self, new_node):
	new_node.set_next_node(self.get_head())
	self.set_head(new_node)
```
  

We can then run,

`my_tri_nums.insert_node_beg(MyNode(-1))`

  

If we print the linked list, the output will be the same as before.
```
-1
0
1
3
6
10
```
  

#### Inserting to the middle
    

Let us now consider the scenario where we have to insert a new element to the middle of the linked list. We will insert a new with the data 2 in between node_2 and node_3. If we are to perform a successful insertion, we will have to perform the following two steps.

1.  Set the pointer of the new element to node_3
    
2.  Set the pointer of node_2 to the new element
    

We will add a new function to our MyLinkedList class to perform the above two steps.

  
```python
def  insert_node_beg(self, new_node):
	new_node.set_next_node(self.get_head())
	self.set_head(new_node)
```
  

We will now insert a new node as follows.

`my_tri_nums.insert_node_mid(my_tri_nums.get_head().get_next_node().get_next_node(), MyNode(2))`

  

If we print all the linked list, it will output,
```
-1
0
1
2
3
6
10
```
  
  
#### Inserting to the end
    

Let us now consider the easiest scenario out of all. We will be inserting an element to the end of the linked list and we only need to point the existing end node to the new node.

We will write a function for that.
```python
def  insert_node_end(self, new_node):
	current_node = self.head
	while(current_node.get_next_node()):
		current_node = current_node.get_next_node()
		current_node.set_next_node(new_node)
```
  

We will now insert a node with the value 15 to the end of the linked list we have created.

`my_tri_nums.insert_node_end(MyNode(15))`

  

If we print the linked list, it will output the following.
```
-1
0
1
2
3
6
10
15
```
  

### Deleting Items from a Linked List
    

Now that we have mastered creation, traversing, and insertion, we will now look at how to delete elements from the linked list.

Just like before, modifications done to the linked list is almost always about rearranging the pointers. We will consider the three scenarios deletion at the beginning, deletion in the middle, deletion at the end.

#### Deleting at the beginning
    

In this, we only have to set the head of our linked list to its second item.

We will write a function for that.
```python
def  delete_node_beg(self):
	self.set_head(self.get_head().get_next_node())
```
  

We can run the function,

`my_tri_nums.delete_node_beg()`

  

and get the output to confirm its functionality.
```
0
1
2
3
6
10
15
```
  

#### Deleting from the middle
    

In this scenario, let us imagine we are to delete node_2 element with the value 1 from our linked list. In order to successfully execute the deletion, we are to point node_1 to node_3. We will write a function for that.
```python
def  delete_node_mid(self,middle_node):
	current_node = self.head
	while(current_node.get_next_node().get_next_node() == middle_node):
		current_node = current_node.get_next_node()
		current_node.set_next_node(current_node.get_next_node().get_next_node())
```
  

As we want to delete node_2 with the value 1, we will now confirm the value we want to delete by executing,

`my_tri_nums.get_head().get_next_node().data`

  

Output:

`1`

  

Let us run our function.

`my_tri_nums.delete_node_mid(my_tri_nums.get_head().get_next_node())`

  

Run a print_all() to confirm the deletion.

`my_tri_nums.print_all()`

  

Output:
```
0
2
3
6
10
15
```
  
  

#### Deleting at the end
    

This is by far the easiest deletion to perform as we are only supposed to change the pointing value of the node before the last node to null. We will write a function for that.
```python
def  delete_node_end(self):
	current_node = self.head
	while(current_node.get_next_node().get_next_node()):
		current_node = current_node.get_next_node()
		current_node.set_next_node(None)
```
  

Let us run it.

`my_tri_nums.delete_node_end()`

  

If we run print_all(), it will output,
```
0
2
3
6
10
```
  

There it is. That is how we create our own Linked List and Node classes. We will now look at the Python libraries that can be used to make the whole Linked List process much easier.

## Linked Lists Python Libraries
    

Deque from the collections module of Python is a great place to start Linked Lists. Deque is essentially for doubly linked lists and we will look at a few use cases and get ourselves familiar with its functionalities.

### Creation of a linked list
    

We can simply import the collections module and get started as follows.

from collections import deque

`my_list = deque()`

  

There we have created a linked list called my_list.

If we print it, it will return,

`deque([])`

  

It means space has been created for us to add new nodes to the linked list.

### Insertion of elements
    

We can insert elements to the end by using the append command.
```python
my_list.append(1)
my_list.append(2)
```
  

If we print it, it will output,

`deque([1, 2])`

  

We can also insert elements into its head position by using appendleft().

`my_list.appendleft(3)`

  

If we print it,

`deque([3, 1, 2])`

  

We can insert elements to its middle by using the insert function.

Its syntax is as insert( index, value).

The index is the position we want to insert a value to and value is the value we are inserting. Let us insert value 4 to the position 2 governed by zero indexing convention.

`my_list.insert(2,4)`

  

Print the whole linked list,

`deque([3, 1, 4, 2])`

  

### Deletion of elements
    

We remove elements by using the element value. It will remove the first occurrence of the specified value.

`my_list.remove(4)`

  

If we print it,

`deque([3, 1, 2])`

  

If we are to delete it by the index, we can use the Python wide del command.

`del my_list[1]`

  

Print the linked list,

`deque([3, 2])`

  

We can also use the pop function to remove elements. It will delete the last element and will print the value.

`my_list.pop()`

  

Output:

`2`

  

If we print the linked list, it will output,

`deque([3])`

  

confirming that the last value has been removed.

We can also remove the head value by using the popleft() function.

## Doubly Linked Lists
    

We know that singly linked lists were learned about having two components in each of its nodes.

1.  A data value
    
2.  A pointer to the next node
    

As there is only one pointer, we can only traverse through the linked list in one direction.

However, in doubly linked lists, there is one more addition of another pointer. This pointer refers to each node’s preceding node. The following is a node of a doubly linked list in its most basic form.

![](https://lh3.googleusercontent.com/OQXNQuChmFbbuGSQM9eiwDnNx_WHIplW4Y9RBjwLn3NX0BtmmUfs8PyZduRc6J56Pn8-2B3IFGbm_nmmDHKYHGAHl4ZOzjoSp0Hji8PfsOFAG6AxhTau4Ik1Fur1SczyZ1jURzk)

If we consider the above figure, we can see that there are two pointers in addition to the data.

We can modify our previously written MyNode class by adding another variable prev_node facilitating doubly linked lists.
```python
class  MyNode:
	def  __init__(self, data=None):
		self.data = data
		self.next_node = None
		self.prev_node = None
	def  set_next_node(self, next_node):
		self.next_node = next_node
	def  get_next_node(self):
		return  self.next_node
	def  set_prev_node(self, next_node):
		self.next_node = next_node
	def  get_prev_node(self):
		return  self.next_node
```
  

This way, we can even create circular linked lists by pointing each linked list’s last node to its first node and vice versa.

The biggest advantage of circular linked lists is that traversing through the list can be initiated at any arbitrary node. They are extremely similar to singly linked lists and therefore, they are as easy to use and implement in code. However, one thing to keep in mind is that while traversing through the linked list, the arbitrary starting point has to be remembered, or else it will traverse through the linked list indefinitely.

  

## Conclusion
    

Linked lists are an efficient way to store data. They are linear, dynamic, and can be resized during runtime. Tasks such as low-level memory management are usually implemented using linked lists. Each node usually represents blocks of memories of any size. Linked lists make it easier to free, reassign, and reorder them.

Data in linked lists do not have to be in contiguous memory blocks and therefore, enable easy removal and addition of data unlike with arrays. However, there are some inherent disadvantages such as accessing elements which happen to be slower than it is with arrays.
