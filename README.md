# LINKED-LIST-IMPLEMENTAION

*COMPANY* : CODTECH IT SOULUTIONS

*NAME* : BHUMIKA

*INERN ID* : CT08K876

*DURATION* : 4 WEEKS

*MENTOR* : NEELA SANTOSH


Singly Linked List Implementation
------------------------------------------------------------------------
This C program (linked_list.c) provides a fundamental and illustrative implementation of a singly linked list, a cornerstone data structure in the realm of computer science. It is an indispensable concept for understanding how data can be organized and manipulated dynamically in memory, offering significant advantages over static data structures like arrays in certain scenarios. Unlike arrays, which store elements in contiguous memory blocks, linked lists utilize a chain of individual "nodes." Each node within this chain contains two primary components: a data field to hold the actual value, and a pointer (often referred to as a "link") that points to the next node in the sequence. This non-contiguous storage mechanism is what grants linked lists their remarkable flexibility, particularly in enabling highly efficient insertions and deletions of elements without the need for cumbersome shifting of other elements, a common bottleneck with arrays when frequent structural modifications are required. The program effectively leverages dynamic memory allocation functions provided by <stdlib.h> to manage the creation and destruction of nodes efficiently at runtime.

Logic Explained in Detail:
The entire structure and the operational behavior of the singly linked list are meticulously defined and implemented through a combination of a structure definition and several dedicated functions:

1. struct Node:
------------------------------------------------------------------------------

This structure serves as the atomic building block for every element within the linked list. It is defined to contain two essential members:

int data: This member is designed to store the actual integer value that this particular node will hold. It's important to note that while this example uses an int, the concept of a linked list is highly generalizable, and this member could be easily adapted to store any other data type (e.g., char, float, struct Person, etc.) or even a pointer to a more complex data structure.

struct Node *next: This is a pointer that points to another instance of the Node structure. It is the crucial "link" that establishes the sequential connection between the current node and the subsequent one in the list. When a node is the last in the list, its next pointer is conventionally set to NULL.

A global pointer struct Node *head = NULL; is declared. This head pointer is of paramount importance as it consistently points to the first node in the linked list. If the head pointer itself is NULL, it serves as a definitive indicator that the linked list is currently empty.

2. void insert(int value):
----------------------------------------------------------------------------------

This function is responsible for adding a new node, containing the specified value, to the end of the existing linked list.

The first step involves dynamic memory allocation: struct Node *newNode = (struct Node *)malloc(sizeof(struct Node));. malloc (memory allocate) is called to reserve a block of memory precisely the size of a Node structure. The returned void* pointer is then cast to (struct Node *) for type compatibility in C. This dynamic allocation ensures that nodes are created only when needed, making the list flexible in size.

newNode->data = value; assigns the integer value passed as an argument to the data field of the newly created node.

newNode->next = NULL; sets the next pointer of this newNode to NULL. This is a crucial step because, when a node is initially created for insertion at the end, it is, by definition, the last node in the list.

Case 1: Empty List: The condition if (head == NULL) checks if the linked list is currently empty. If this condition is true, it means there are no existing nodes. In this scenario, the newNode itself becomes the head of the list, effectively initializing the list.

Case 2: Non-Empty List: If the list already contains one or more nodes, a temporary pointer struct Node *temp = head; is initialized to point to the current head of the list.

A while (temp->next != NULL) loop is then used to traverse the list. Inside this loop, temp = temp->next; continuously moves the temp pointer forward, one node at a time. This traversal continues until temp reaches the very last node in the list (which is identified by its next pointer being NULL).

Once the loop terminates, temp is positioned at the last node of the original list. The line temp->next = newNode; then establishes the crucial link: the next pointer of the previously last node is updated to point to the newNode, thereby appending the newNode to the end of the list.

3. void delete(int value):
---------------------------------------------------------------------------------

This function is designed to remove the first occurrence of a node that contains the specified value from the linked list. This operation is inherently more complex than insertion because it requires careful manipulation of pointers to maintain the integrity of the list chain.

Two pointers are initialized: struct Node *temp = head (which will traverse the list and point to the current node being examined) and struct Node *prev = NULL (which will always point to the node immediately preceding temp).

Case 1: Deleting the Head Node: The condition if (temp != NULL && temp->data == value) specifically checks if the head node itself (pointed to by temp) contains the value to be deleted. If this condition is true, head is updated to point to the next node in the sequence (head = temp->next;), effectively bypassing the original head. The memory occupied by the original head node is then released back to the system using free(temp);, which is vital for preventing memory leaks. After deletion, the function returns.

Case 2: Deleting a Node Other Than Head: If the value is not found in the head node, a while (temp != NULL && temp->data != value) loop is initiated to search for the target node within the rest of the list. In each iteration of this loop:

prev = temp; updates the prev pointer to the current position of temp.

temp = temp->next; moves the temp pointer to the next node.

This ensures that throughout the search, prev consistently points to the node immediately before temp.

Value Not Found: After the loop completes, if (temp == NULL) checks if temp has become NULL. If true, it means the entire list was traversed, and the value was not found within any node. In this scenario, an "Value not found!" message is printed to the console, and the function returns.

Node Found and Deleted: If temp is not NULL (meaning the loop terminated because temp->data == value), the target node has been found. The line prev->next = temp->next; performs the critical relinking operation: the next pointer of the previous node (prev) is directly updated to point to the node that followed the one being deleted (temp->next). This effectively removes temp from the list's logical chain. Finally, free(temp); deallocates the memory previously occupied by the removed node, which is a fundamental aspect of dynamic memory management and crucial for preventing memory leaks.

4.  void display():
-----------------------------------------------------------------------------

This function's sole purpose is to traverse the entire linked list from its head to its end and print the data contained within each node.

A temporary pointer struct Node *temp = head; is initialized to the head of the list. Using a temporary pointer for traversal is a good practice as it ensures that the original head pointer (which marks the beginning of the list) remains unchanged.

A while (temp != NULL) loop continues to iterate as long as temp points to a valid node (i.e., it hasn't reached the end of the list).

Inside the loop, printf("%d -> ", temp->data); prints the integer data stored in the current node, followed by an arrow (-> ) for visual clarity.

temp = temp->next; moves the temp pointer to the next node in the sequence, preparing for the next iteration.

After the loop completes (when temp becomes NULL), printf("NULL\n"); is printed to explicitly indicate the end of the linked list, making the output easy to interpret.

Execution Flow:
------------------------------------------------------------------------------
The main function serves as the orchestrator, demonstrating a typical sequence of operations on the linked list to showcase its dynamic behavior:

insert(10); insert(20); insert(30);: These three calls sequentially add nodes with data 10, 20, and 30 to the end of the list. The list state becomes 10 -> 20 -> 30 -> NULL.

display();: This call prints the current state of the list to the console.

delete(20);: This call initiates the deletion process, targeting the node containing 20. The program will find and remove this node, relinking 10 directly to 30.

display();: This call prints the updated state of the list, which will now be 10 -> 30 -> NULL.

insert(40);: This call adds a new node with data 40 to the end of the currently modified list.

display();: This final call prints the ultimate state of the list, which will be 10 -> 30 -> 40 -> NULL.

This step-by-step execution clearly illustrates how elements can be dynamically added and removed from a linked list, highlighting its inherent flexibility and efficiency in managing collections of data where the size is not fixed beforehand.

Expected Output:
---------------------------------------------------------------------------------
Linked List: 10 -> 20 -> 30 -> NULL
Linked List: 10 -> 30 -> NULL
Linked List: 10 -> 30 -> 40 -> NULL




OUTPUT
----------------------------------------------------------------------

<img width="1918" height="1078" alt="Image" src="https://github.com/user-attachments/assets/70e10556-d370-4a77-a20d-5610c1ff256e" />
