# Python Lists

This is a GitHub-ready Markdown version based on your PDF notes.

## What is a List?

A list is a container that can store multiple values (same or different types) in a specific order.

```python
numbers = [10, 20, 30, 40]
data = [10, "Python", 3.14, True]
```

## Properties

- Ordered
- Mutable
- Supports indexing
- Supports slicing
- Allows duplicates

## Creating Lists

```python
lst = []
nums = [1, 2, 3]

lst = list()
chars = list("python")
```

## list(iterable)

```python
list("abc")
list((1,2,3))
list(range(5))
```

## String to List

```python
list("python")
# ['p','y','t','h','o','n']
```

## Tuple to List

```python
list((10,20,30))
```

## Dictionary to List

```python
d = {"a":10,"b":20}

list(d)
# ['a','b']
```

## Indexing

```python
nums = [10,20,30,40,50]

nums[0]
nums[-1]
```

## Slicing

```python
nums[:]
nums[1:]
nums[:3]
nums[::-1]
```

## append()

```python
nums.append(100)
```

## extend()

```python
nums.extend([4,5])
```

## insert()

```python
nums.insert(1,99)
```

## remove()

```python
nums.remove(20)
```

## pop()

```python
nums.pop()
nums.pop(2)
```

## clear()

```python
nums.clear()
```

## index()

```python
nums.index(20)
```

## count()

```python
nums.count(20)
```

## sorted()

```python
sorted(nums)
```

Returns a new list.

## sort()

```python
nums.sort()
```

Sorts the original list.

## reverse()

```python
nums.reverse()
```

## Useful Functions

```python
len(nums)
max(nums)
min(nums)
sum(nums)
```

## Nested Lists

```python
matrix = [
 [1,2,3],
 [4,5,6],
 [7,8,9]
]

matrix[1][2]
```

## Operators

```python
[1,2] + [3,4]
[1,2] * 3
10 in [10,20,30]
```

## Copying

```python
b = a
c = a.copy()
```

## Iteration

```python
for x in nums:
    print(x)

for i in range(len(nums)):
    print(nums[i])

for index, value in enumerate(nums):
    print(index, value)
```

## List Comprehension

```python
squares = [x*x for x in range(5)]

evens = [x for x in range(10) if x % 2 == 0]
```

## Time Complexity

| Operation | Complexity |
|------------|------------|
| Access | O(1) |
| append() | O(1) amortized |
| pop() last | O(1) |
| insert() beginning | O(n) |
| remove() | O(n) |
| search | O(n) |
| sort() | O(n log n) |
