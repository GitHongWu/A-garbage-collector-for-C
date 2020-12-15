# A-garbage-collector-for-C

### Background
Dynamic memory (i.e. memory accessed via the malloc and free family of commands) is essential to many programs in the freedom, control, and interpretability it allows. We’ve talked about 2 different types of management for dynamic memory: implicit allocators and explicit allocators. This assignment focuses on the implicit allocator, perhaps better known as the garbage collector. Intuitively, we want this tool to find the blocks (or chunks as we refer to them) that are not being used and return them to the process as free chunks.

For further reference, please see section 9.10 (and specifically 9.10.2) of the book.

Memory layout review  
As a quick review, we can visualize dynamic memory (aka the heap) as a list of chunks. From class, we know that each allocated or free block is started with header (shown as ‘h’ in the figure below), contains a payload (‘x’), and has some form of padding at the end.


```
----------------------------------------------------------------------  
| h  | x  | x  | h  |    | h  | x  | h  |    |    |    |    |    |    ...  
----------------------------------------------------------------------  
^              ^         ^         ^  
|              |         |         |  
a              b         c         the rest of the heap...  
```
In the figure, ‘a’ represents an allocated section of the heap with a payload + padding taking up 2 words worth of space. Similarly, ‘b’ is a free node of size 1 word.

While you will not need to delve into the details of this implementation or structure to complete homework 4, it will be helpful to keep this image in mind while you implement your garbage collector.

Chunk structure

```
typedef struct chunk {
         size_t size;
         struct chunk* next;
         struct chunk* prev;
} chunk;
```

### The programming part
In this homework, we build a basic, conservative garbage collector for C programs. Starting from the set of root pointers present in the stack and global variables, we traverse the “object graph” (in the case of malloc, a chunk graph) to find all chunks reachable from the root. These are marked using the third lowest order bit in the size field of each chunk. We have implemented several helpful functions for you ranging from checking for marked chunks to navigation of the heap. Please read the skeleton code to get a feel for what is available and what you should be doing. Ultimately, you will need to implement the sweeping functionality of the garbage collector, the pointer-confirmation functionality, and a portion of the marking functionality.
