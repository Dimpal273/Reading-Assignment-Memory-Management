# Reading-Assignment-Memory-Management
1) Consider a swapping system in which memory consists of the following hole sizes in memory order: 10MB, 4MB, 20MB, 18MB, 7MB, 9MB, 12MB, and 15MB. Which hole is taken for successive segment requests of:12MB,10MB,9MB for first fit? 20MB, 10MB, 18MB
    best fit? 12MB, 10MB, 9MB
    worst fit? 20MB, 18MB, 15MB(finds the largest possible one to fit)
    next fit? 20MB, 18MB, 9MB

2) What is the difference between a physical address and a virtual address?
    Real memory uses physical addresses. These are the numbers that the memory chips react to on the bus. Virtual addresses are the logical addresses that refer to a process’ address space. Thus a machine with a 32-bit word can generate virtual addresses up to 4 GB regardless of whether the machine has more or less memory than 4 GB.

3) Using the page table of Fig. 3-9 of MOS4e, give the physical address corresponding to each of the following virtual addresses:20, 4100, 8300
    20 - 8212, 4100 - 4100, 8300 - 24684

4) Copy on write is an interesting idea used on server systems. Does it make any sense on a smartphone? Why?
    If the smartphone supports multiprogramming, which the iPhone, Android,and Windows phones all do, then multiple processes are supported. If a process forks and pages are shared between parent and child, copy on write definitely makes sense. A smartphone is smaller than a server, but logically it is not so different.

5) If FIFO page replacement is used with four page frames and eight pages, how many page faults will occur with the reference string 0172327103 if the four frames are initially empty? Repeat this problem for LRU.
    The page frames for FIFO are as follows:
    x0172333300, xx017222233, xxx01777722, xxxx0111177
    The page frames for LRU are as follows:
    x0172327103, xx017232710, xxx01773271, xxxx0111327
    FIFO yields six page faults; LRU yields seven.

6) In the WSClock algorithm of Fig. 3-20(c) on pg. 220 of MOS4e, the hand points to a page with R=0. If tau(400), will this page be removed? What about if tau(1000)?
    The age of the page is 2204 − 1213 = 991. If τ = 400, it is definitely out of the working set and was not recently referenced so it will be evicted. The τ = 1000 situation is different. Now the page falls within the working set (barely), so it is not removed.

7) Virtual memory provides a mechanism for isolating one process from another. What memory management difficulties would be involved in allowing two operating systems to run concurrently? How might these difficulties be addressed?
     The problem is how to quickly switch to another operating system and therefore how to deal with the TLB. Typically, you want to give some number of TLB entries to each kernel and ensure that each kernel operates within its proper virtual memory context. But sometimes the hardware (e.g., some Intel architectures) wants to handle TLB misses without knowledge of what you are trying to do. So, you need to either handle the TLB miss in software or provide hardware support for tagging TLB entries with a context ID

8) When segmentation and paging are both being used, as in MULTICS, first the segment descriptor must be looked up, then the page descriptor. Does the TLB also work this way, with two levels of lookup?
    No. The search key uses both the segment number and the virtual page number,so the exact page can be found in a single match.

9) A student in a compiler design course proposes to the professor a project of writing a compiler that will produce a list of page references that can be used to implement the optimal page replacement algorithm. Is this possible? Why or why not? Is there anything that could be done to improve paging efficiency at run time?
    This is probably not possible except for the unusual and not very useful case of a program whose course of execution is completely predictable at compilation time. If a compiler collects information about the locations in the code of calls to procedures, this information might be used at link time to rearrange the object code so that procedures were located close to the code that calls them. This would make it more likely that a procedure would be on the same page as the calling code. Of course this would not help much for procedures called from many places in the program.