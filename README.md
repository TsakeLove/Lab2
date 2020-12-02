# Page Allocator

### About Page Allocator


A general purpose memory allocator performs several tasks: allocating a block of memory of a given size, freeing an allocated block of memory, and resizing an allocated block of memory.
This task implements the functions of the page distributor. A page is an uninterrupted part of memory divided by a multiple of a power of two and has three states: free, divided into blocks, not occupied by a multi-page block

### Algorithms

- #### Memory allocation function

    `void* Allocator::mem_alloc(uint16_t size)`

 The function is designed to allocate memory. Initially, we check if one page is enough for us to allocate memory. If there is enough, we find the first page that is split into the necessary blocks of memory, check if there are free blocks and return a link to the first byte of the block. If not, we calculate the required number of pages, find the memory area in which the given number will be freely hidden, and return the index of the first page.

- #### Memory realloc function

    `void* Allocator::mem_realloc(void *adr, uint16_t size);`

The function is designed to change the amount of memory.
go through the pages to find on which page the block you want to change. If the address is passed such that the alignment returns the old size, then return the address. If the size is less than the one that is now free the old address and return. If it is necessary to allocate more memory than now, then we go through the array of pages, look for the necessary block, and free the old one.

 - #### Memory free function

     `void Allocator::mem_free(void *adr)`

      The function serves to free memory. We go through the pages and check the block or address belongs to this page. If so, we find the block itself and free memory in it. If not, then the data is on several pages, we check how many pages are used and free memory on them.

 - #### Unite page function
 
     `void Allocator::unite_page(uint16_t page_index)`

      The function is designed to combine pages. We pass an array of pages through itd if there are several parsing pages with free memory, then we connect them.

  #### Example 
  Code:
   Allocator allocator;
   allocator.init();`
   void * adr1 = allocator.mem_alloc(15);
   void * adr2 = allocator.mem_alloc(16);
   void * adr3 = allocator.mem_alloc(63);
   allocator.mem_realloc(adr3, 79);
   allocator.mem_dump();

