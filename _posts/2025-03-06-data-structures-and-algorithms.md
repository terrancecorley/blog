---
layout: post
title:  "Data Structures & Algorithms"
date: 2025-03-06
categories: dsa
---

## Data Structures, what are they?
Arrays, queues, stacks, linked lists, hash maps, graphs, trees, heaps. These are all examples of data structures. To put it simply, data structures allow you to arrange and manipulate your data in an expected way. Programming languages will often abstract a lot of the code that makes these things work, and often for good reason, it would be a little tedious to have to programatically create commonly used data structures from scratch when usually as engineers we are only interested in using data structures as opposed to creating them. 

That said, I think it is still really valuable to learn about how these data structures work at a lower level, for multiple reasons. Not only will you understand these data structures better when you go to use them in your applications, but you will have a better grasp of performance trade offs by knowing the time and space complexity of each one and their given exposed methods, and for better or worse, a lot of companies still expect decent knowledge on these data structures when it comes to interviews.

I'll dive into one data structure now, a singly-linked list.

<br>
### Singly Linked List

*Disclaimer: Please excuse my rudimentary drawings, I'm still getting used to the tool Procreate*

// todo: give example on human chain touching shoulders
![My First Post Image]({{ "/assets/images/posts/2025-03-06-data-structures-and-algorithms/linked-list-1.png" | relative_url }})
![My First Post Image]({{ "/assets/images/posts/2025-03-06-data-structures-and-algorithms/linked-list-2.png" | relative_url }})
![My First Post Image]({{ "/assets/images/posts/2025-03-06-data-structures-and-algorithms/linked-list-3.png" | relative_url }})
![My First Post Image]({{ "/assets/images/posts/2025-03-06-data-structures-and-algorithms/linked-list-4.png" | relative_url }})
![My First Post Image]({{ "/assets/images/posts/2025-03-06-data-structures-and-algorithms/linked-list-5.png" | relative_url }})

```js
class Node { 
    constructor(val) {
        this.val = val;
        this.next = null;
    }
}

class SinglyLinkedList {
    constructor() {
        this.head = null;
        this.tail = null;
        this.length = 0;
    }

    append(val) {
        const newNode = new Node(val);
        if (!this.head) {
            this.head = newNode;
        } else {
            this.tail.next = newNode;
        }

        this.tail = newNode;
        this.length++;
    }
}
```
<br>

## Algorithms, what are they?
 
Use the example of adding to a singly linked list.