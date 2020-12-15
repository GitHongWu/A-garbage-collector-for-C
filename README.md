# A-garbage-collector-for-C

### Background
Dynamic memory (i.e. memory accessed via the malloc and free family of commands) is essential to many programs in the freedom, control, and interpretability it allows. We’ve talked about 2 different types of management for dynamic memory: implicit allocators and explicit allocators. This assignment focuses on the implicit allocator, perhaps better known as the garbage collector. Intuitively, we want this tool to find the blocks (or chunks as we refer to them) that are not being used and return them to the process as free chunks.

For further reference, please see section 9.10 (and specifically 9.10.2) of the book.

Memory layout review
As a quick review, we can visualize dynamic memory (aka the heap) as a list of chunks. From class, we know that each allocated or free block is started with header (shown as ‘h’ in the figure below), contains a payload (‘x’), and has some form of padding at the end.



----------------------------------------------------------------------  
| h  | x  | x  | h  |    | h  | x  | h  |    |    |    |    |    |    ...  
----------------------------------------------------------------------  
^              ^         ^         ^  
|              |         |         |  
a              b         c         the rest of the heap...  

`code()   \n
asdasdadsas
`  
`code()`
