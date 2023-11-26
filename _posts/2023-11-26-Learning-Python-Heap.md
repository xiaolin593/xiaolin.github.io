---
layout: post
title: "Learning Python - Heap"
date: 2023-11-26
categories: [programming]
tags: [python]
---


## Basic Heap Operations
```python
import heapq

min_heap = [7, 3, 4, 2, 5, 6, 1, 8, 10, 9]

# sort heap in ascending order
heapq.heapify(min_heap)

# elements in heap after heapify are not necessarily in order
print(min_heap) 

# sort heap in descending order
max_heap = [-num for num in min_heap]
heapq.heapify(max_heap)

# push new element 11 to min_heap
heapq.heappush(min_heap, 11)

# peek first element at the top of heap
first_element = heapq.nlargest(1, min_heap)[0] # first_element = min_heap[0]

# sort a list in place using heap.
# first heapify
# second while-loop with heappop() operation
heapq.heapify(min_heap)
while len(min_heap) > 0:
    element = heapq.heappop(min_heap)
    print(element)

# re-initialize min_heap
min_heap = [7, 3, 4, 2, 5, 6, 1, 8, 10, 9]

# push element to heap, then pop and return smallest/largest from heap
element = heapq.heappushpop(min_heap, 0)

# push element to heap, pop and return the smallest item from heap
element = heapq.heapreplace(min_heap, 11)

# return top N largest elements from heap
n = 5
top_5_largest = heapq.nlargest(n, min_heap, key = None)
print(top_5_largest)

# return top N smallest elements from heap
top_5_smallest = heapq.nsmallest(n, min_heap, key  = None)
print(top_5_smallest)
```

## Advanced Heap Operations
```python
import heapq
# heapsort
# push all values onto heap and popping off the smallest values one at a time
def heapsort(iterable):
    h = []
    for value in iterable:
        heapq.heappush(h, value)
    return [heapq.heappop(h) for i in range(len(h))]

sorted_list = heapsort([1, 3, 5, 7, 9, 2, 4, 6, 8, 0])
print(sorted_list)


# useful for assigning comparison values (such as task priorities) along with main record being tracked
h = []
heapq.heappush(h, (5, 'write code'))
heapq.heappush(h, (7, 'release product'))
heapq.heappush(h, (1, 'write spec'))
heapq.heappush(h, (3, 'create tests'))
entry = heapq.heappop(h)
print(entry)

```

## PriorityQueue Implementation Notes
A priority queue is common use for a heap, and it presents several implementation challenges:
- Sort stability: how do you get two tasks with equal priorities to be returned in the order they were originally added?
- Tuple comparison breaks for (priority,task) pairs if the priorities are equal and the tasks do not have a default comparison order
- If the priority of a task changes, how do you move it to a new position in the heap?
- Or if a pending task needs to be deleted, how do you find it and remove from the queue?

A solution for first two challenges is to store entries as 3-element list including priority, an entry count, and the task. The entry count serves as tie-breaker with same priority are returned in the order they were added.

Since no two entry counts are the same, the tuple comparison will never attempt to directly compare two tasks. 

Finding a task can be done with a dictionary pointing to an entry in the queue.
Removing the entry or changing its priority is more difficult because it would break the heap structure invariants. So, a possible solution is to mark the entry as removed and add a new entry with revised priority

```python
import itertools
import heapq

pq = []                     # list of entries arranged in a heap
entry_finder = {}           # mapping of tasks to entries
REMOVED = '<removed-task>'  # placeholder for a removed task
counter = itertools.count() # unique sequence count

def add_task(task, priority = 0):
    'Add a new task or update the priority of an existing task'
    if task in entry_finder:
        remove_task(task)
    count = next(counter)
    entry = [priority, count, task]
    entry_finder[task] = entry
    heapq.heappush(pq, entry)

def remove_task(task):
    'Mark an existing task as REMOVED. Raise KeyError if not found.'
    entry = entry_finder.pop(task)
    entry[-1] = REMOVED

def pop_task():
    'Remove and return the lowest priority task. Raise KeyError if empty.'
    while pq:
        priority, count, task = heapq.heappop(pq)
        if task is not REMOVED:
            del entry_finder[task]
            return task
    raise KeyError('pop from an empty priority queue')
```
