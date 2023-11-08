# Algroithms - Sort

In this note on sorting algorithms, we cover the following algorithms:
- [Bubble Sort](#bubble-sort)
- [Insertion Sort](#insertion-sort)
- [Merge Sort](#merge-sort)
- [Quick Sort](#quick-sort)

_Disclaimer: The pseudo-code was developed with assistance from [GitHubCopilot](https://copilot.github.com/)_

## Bubble Sort


_"Bubble sort is a comparison-based sorting algorithm that repeatedly swaps adjacent elements if they are in the wrong order. It is implemented using nested loops."_
<div style="text-align: right; font-style: italic;"> - Github Copilot </div>

<br>
Two neighboring elements are compared at a time.
They swap places if the second is smaller than the first. 
Start at the beginning of the list. 
For each iteration, the largest elements “bubble” to the back of the list.

### Pseudocode
```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
```

### Key points
- comparison-based
- in-place
- stable

### Complexity
- Time: O(n<sup>2</sup>)
- Space: O(1)


## Insertion Sort

_"Insertion sort is a comparison-based sorting algorithm that builds a sorted array one element at a time by comparing each element to its predecessor and swapping them if they are in the wrong order. It is implemented using nested loops."_
<div style="text-align: right; font-style: italic;"> - Github Copilot </div>

<br>


### Pseudocode
```python
def insertion_sort(arr):
    n = len(arr)
    for i in range(1, n):
        key = arr[i]
        j = i - 1
        while j >= 0 and key < arr[j]:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key
```

### Key points
- comparison-based
- in-place
- stable

### Complexity
- Time: O(n<sup>2</sup>)
- Space: O(1)


## Merge Sort

_"Merge sort is a comparison-based sorting algorithm that divides an array into two halves, sorts each half recursively, and then merges the two halves into a sorted array. It is implemented using recursion."_
<div style="text-align: right; font-style: italic;"> - Github Copilot </div>


<br>
The idea is to split an n-sized list into n sublists. 
Then merge two sublists at a time.
Start by removing the first element from each list, compare them, and add the smallest to the merged list. 
If/when the sublists have more than one element, continue comparing against the first element of each list, adding the smallest to the merge list. 
When a sublist has been completely emptied, the rest of the remaining list should be able to be added to the end of the merged list.
Repeat merging lists recursively until all sublists have been merged into a single list.

### Pseudocode
```python
def merge_sort(arr):
    if len(arr) > 1:
        mid = len(arr) // 2
        left = arr[:mid]
        right = arr[mid:]

        merge_sort(left)
        merge_sort(right)

        i = j = k = 0
        while i < len(left) and j < len(right):
            if left[i] < right[j]:
                arr[k] = left[i]
                i += 1
            else:
                arr[k] = right[j]
                j += 1
            k += 1

        while i < len(left):
            arr[k] = left[i]
            i += 1
            k += 1

        while j < len(right):
            arr[k] = right[j]
            j += 1
            k += 1
```

### Key points
- comparison-based
- not in-place
- stable

### Complexity
- Time: O(n log n)
- Space: O(n)


## Quick Sort

_"Quick sort is a comparison-based sorting algorithm that divides an array into two halves, sorts each half recursively, and then combines the two halves into a sorted array. It is implemented using recursion."_
<div style="text-align: right; font-style: italic;">- GitHub Copilot </div>

Find a "pivot" element, and move all the numbers smaller than this value in front, and all the numbers larger behind. 
Repeat this in each of the sections created, recursively, until all elements have been moved into place. 

### Pseudocode
```python
def quick_sort(arr, low, high):
    if low < high:
        pivot = partition(arr, low, high)
        quick_sort(arr, low, pivot - 1)
        quick_sort(arr, pivot + 1, high)

def partition(arr, low, high):
    pivot = arr[high]
    i = low - 1
    for j in range(low, high):
        if arr[j] < pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1
```

### Key points
- comparison-based
- in-place
- unstable

### Complexity
- Time: O(n log n)
- Space: O(log n)


