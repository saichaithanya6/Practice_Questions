## Linked List

#### Merging two linked list in ascending order:

You are given the heads of two sorted linked lists list1 and list2.

Merge the two lists into one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

![image](https://github.com/user-attachments/assets/f214a414-2998-4521-911a-e4ef7c951950)

```d
class Solution(object):
    def mergeTwoLists(self, list1, list2):
        """
        :type list1: Optional[ListNode]
        :type list2: Optional[ListNode]
        :rtype: Optional[ListNode]
        """
        dummy= ListNode()
        cur = dummy  # We are creating dummy list because we need to print the entire list and it will be easy to create dummy listnode which is equal to current list

        while list1 and list2:
          if list1.value > list2.value: #We dump the node which has less value in any of the list
            cur.next = list2
            list2 = list2.next
          else:
            cur.next = list1
            list1 = list1.next
          cur= cur.next

        if list1: #The last node will be remaining, so we dump it if any of the nodes are left in the list
          cur.next = list1
        else:
          cur.next = list2

        return dummy.next
 ```
Understanding cur.next in cur.next = list2 or cur.next = list1

In a singly linked list, each node has:

* A value (val)
* A pointer to the next node (next)

What Does cur.next Do?

cur.next refers to the next node in the linked list after cur. When we write:       

Why cur = cur.next is Necessary
- After linking cur.next to a node, we need to move cur forward to continue building the merged list. If we don't, all subsequent assignments (cur.next = ...) will keep modifying cur.next of the same node, breaking the linked list structure.
  
![image](https://github.com/user-attachments/assets/1392aeb0-0bfb-4039-96bb-aa5e24d55944)
