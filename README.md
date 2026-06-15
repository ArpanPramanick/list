# PYTHON LISTS

A list is container that can store multiple values (of multiple or same types) in a specific order.

Lists are one of 4 built-in data types in Python used to store collections of data.

```python
numbers = [10, 20, 30, 40]
```

- `numbers` → variable
- `[10, 20, 30, 40]` → list object
- `10, 20, 30, 40` → elements/items

```python
data = [10, "Python", 3.14, True]
```

| FEATURE | SUPPORTED? |
|---|---|
| Ordered | ✅ Yes |
| Mutable | ✅ Yes |
| Duplicate values allowed | ✅ Yes |
| Heterogeneous data allowed | ✅ Yes |
| Indexed | ✅ Yes |
| Dynamic size | ✅ Yes |

## Lists are Mutable

Hence,
```python
a = [1, 2]
b = [1, 2]
```

### How things are happening?

*First stmt*: `a = [1, 2]`, Python starts to execute RHS, It required 2 objects 10, 20 which are **small integer**, hence python checks Integer Cache whether they exist or not, but they aren't there

1. Python first creates an object in memory with value 1, then creates another object in memory with value 2.
2. Now Python creates list object *refa*, and store the references inside that. Now a is made to that reference *refa*

*Next stmt*: `b = [1, 2]`, Python starts to execute RHS, It required 2 objects 1, 2 which are **small integer**, hence python checks Integer Cache whether they exist or not, but they are there!

1. Python reuses those object references already available inside memory in memory
2. Now Python creates another list object *refb*, and store the references inside that. Now a is made to that reference *refa*

*Hence*,
```python
print(a is b)
```

Returns FALSE, because

> **Python does not automatically intern/reuse separately created list/dict/set literals.** Because change in the value by any of the referencing variable would affect other variables as mutable objects allow to change the value of the actual object if all of them reference to the same object!

| Data Type | Mutable? | Python may reuse same object? |
|---|---|---|
| int | No | Often Yes |
| float | No | Sometimes |
| str | No | Often Yes (interning) |
| tuple | No | Sometimes |
| list | Yes | No for separately created lists |
| dict | Yes | No |
| set | Yes | No |

---

## CREATING LISTS

```python
lst = []        # nums = [1, 2, 3, 4]
```
or
```python
lst = list()    # lst = list("python")
```

### 1. `list(iterable)`

A built-in constructor function in Python that creates a new list object by taking an iterable as a single parameter. This function iterates over that given iterable object and sometimes creates separate objects with by considering each of the elements as a single element of the iterable, thus the list is created.

→ iterable is optional. If omitted, an empty list is created.
→ If provided, Python takes each element from the iterable and puts it into a new list.
→ `list()` creates a new list object and populates it with the elements obtained by iterating over the given iterable. Whether new element objects are created depends on how the iterable produces its elements. The list itself always stores references to the resulting element objects.

| Iterable | Does iteration produce new objects? | Example |
|---|---|---|
| list | Usually No | `list([1,2,3])` |
| tuple | Usually No | `list((1,2,3))` |
| set | Usually No | `list({1,2,3})` |
| dict (keys) | Usually No | `list(d)` |
| dict.keys() | Usually No | `list(d.keys())` |
| dict.values() | Usually No | `list(d.values())` |
| range | Yes (range yields integer values one by one.) | `list(range(5))` |
| str | Character string objects are yielded | `list("abc")` |
| Generator | Depends on generator code | `list(gen)` |

### WHY!?

Iterables like string, ex. `str="abc"` by `list()` produces 3 objects: `"a"`, `"b"`, `"c"` but these objects are not there in the memory, hence Python need to create them.

Although iterables list/tuple/set, ex `lst=[10, 20, 30]` by `list()` produces 3 objects: `10, 20, 30` but these objects are already there in the memory, Python will not create them.

**Verification:**
```python
print(type(list))
```
**Output:**
```
<class 'type'>
```

Like `int()`, `float()`, `str()`, etc., `list()` is used to create list objects.

→ `a = []` ≡ `a = list()`

**Iterable:** An iterable is an object that can provide its elements one by one. Examples: string, tuple, set, dictionary, range, list. But int, float, Boolean are not iterables, hence `list()` will not work on non-iterables.

```python
int a=6
x=list(6)    # ✗
x=list(a)    # ✗
```

---

## String → List

```python
s = "python"
lst = list(s)
print(lst)
```
**Output:** `['p', 'y', 't', 'h', 'o', 'n']`

What happens internally? Python iterates over the object:

`'p' → 'y' → 't' → 'h' → 'o' → 'n'`

and stores each of the elements into a new list.

Hence if we change `s`, it will not affect `lst`!

```python
s = "java"
print(lst)
```
**Output:** `['p', 'y', 't', 'h', 'o', 'n']`

See `list()` has created new string element objects while creating `lst`!

## Tuple → List

```python
t = (10, 20, 30)
lst = list(t)
```
**Output:** `[10, 20, 30]`

What happens internally? Python iterates over the object and stores the references directly.

If we change `t`, it will not affect `lst`! Because, int references remain same for `lst`!

```python
t = (20, 30)
print(lst)
```
**Output:** `[10, 20, 30]`

## Set → List

```python
s = {10, 20, 30}
lst = list(s)
print(lst)
```
**Possible output:** `[10, 20, 30]` or `[30, 10, 20]`

As sets are unordered. list preserves whatever order the set provides internally.

## Range → List

```python
r = range(5)
print(r)
lst = list(r)
print(lst)
```
**Output:** `[0, 1, 2, 3, 4]`

What happens internally? Python reads: `0 → 1 → 2 → 3 → 4`

## Dictionary → List

```python
d = {"a": 10, "b": 20, "c": 30}
list(d)
```
**Output:** `['a', 'b', 'c']`

### Why only keys?

When Python iterates over a dictionary, it iterates over keys by default.

Internally:
```python
for x in d:
    print(x)
```
prints: `a, b, c`

Therefore: `list(d)` becomes `['a', 'b', 'c']`

---

## Dictionary

```python
d = {"a": 10, "b": 20, "c": 30}
list(d)
```
**Output:** `['a','b','c']`

### Dictionary Values
```python
list(d.values())
```
**Output:** `[10, 20, 30]`

### Dictionary Keys
```python
list(d.keys())
```
**Output:** `['a', 'b', 'c']`

### Dictionary Items
```python
list(d.items())
```
**Output:** `[('a', 10), ('b', 20), ('c', 30)]`

---

## *** List to List:

```python
a = [10,20,30]
b = list(a)
```
because `b` new list reference is created by iterating over the elements of list `a` and storing the references in `b`

**Memory:** As refa != refb, `a is b` results **False**!

But internally, both are referencing to same int element objects, Hence,

`a[0] is b[0]` results **True**!
`a[1] is b[1]` results **True**!
…

### Compare with Assignment

```python
a = [10,20,30]
b = a
```

**Memory:** As refa == refb, `a is b` results **True**!

Any change in the list through any of the referencing variable, will make change in the actual memory object as lists are mutable.

```python
a[0]=11
print(a)        #[11, 20, 30]
print(b)        #[10, 20, 30]
print(a is b)
```

> **`list()` Creates a Shallow Copy:** `b = list(a)` ≡ `b = a.copy()`

### 2. `[element1, element2, …]` Method

It takes more than one element (object reference) as input and creates list by directly storing those references!

| | BASE `[ ]` | `list()` |
|---|---|---|
| **Purpose** | Always creates a new list object by storing the passed reference parameters directly as list elements. | Always creates a new list object. The elements placed inside that list may or may not be newly created objects, depending on the iterable being converted. |
| **Parameters** | Can take more than one element as parameter and store each of their references directly inside to create the list object.<br>`Lst =[12]`, `lst = ["ab"]` 👌<br>`Lst = ["Ab", "Cd"]` 👌<br>`Lst = [12, True, "Ab"]` 👌 | At a time maximum one iterable object allowed to create the list by iteration over that.<br>`Lst = list(12)` 🖕<br>`Lst = list("ab")` 👌<br>`Lst = list("Ab", "Cd")` 🖕<br>`Lst = list(12, True, "Ab")` 🖕 |
| **String -> List** | `lst=["ab"]` `lst=["ab", "cd"]`<br>```python<br>s = "ab"<br>lst=[s]<br>s = "cd"<br>print(lst)<br>#OP: ['ab']<br>``` | ```python<br>lst=list("ab")<br>s = "ab"<br>lst=list(s)<br>s = "cd"<br>print(lst)<br>#OP: ['a', 'b']<br>``` |
| **List -> List (Mutable obj -> List)** | ```python<br>l = [1, 2]<br>lst = [l]<br>l.append(3)<br>print(lst)<br>#OP: [[1, 2, 3]]<br>print(l)<br>#OP: [1, 2, 3]<br>```<br>It happened as `lst` is storing actual reference of `l` | ```python<br>l = [1, 2]<br>lst = list(l)<br>l.append(3)<br>print(lst)<br>#OP: [1, 2]<br>print(l)<br>#OP: [1, 2, 3]<br>```<br>It happened as `lst` is not storing actual reference of `l`, rather only the integer references used by `l` |

### 8. Nested List:

```python
x = [1,2,3]
a = [x]
print(a)
print(a[0])
print(a[0][0])
```

### Internal Memory Concept:

List stores references to objects, not actual objects themselves. Python physically doesn't put the value inside the list.

In int, `a=10`
1. Python creates an integer object 10 somewhere in memory.
2. And x stores the address/reference of that object.

In List, `a = [10, 20, 30]`
1. Python actually creates three integer objects:
2. and the list stores references to them.

A list does not usually store the actual object; it stores the address (reference) of the object. If Python copied the entire object every time it was placed in a list, tuple, dictionary, etc., a lot of memory would be wasted. Instead, Python stores only a small reference pointing to the object.

**Proof:**
```python
x = 10
a = [x]
print(id(x))
print(id(a[0]))
```

### Nested List Memory:

```python
x = [1,2,3]
a = [x]
```
Now we perform, `x.append(4)`

---

## INDEXING

Supports both +VE & -VE indexing.

| 10 | 20 | 30 | 40 | 50 |
|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 |
| -5 | -4 | -3 | -2 | -1 |

It supports SLICING.

It is Mutable, hence we can change values inside the list.

---

## LIST INBUILT METHODS

### 1. Adding Elements

#### `list.append(elmnt)`: appends that element reference to the end of the list as it is passed as the parameter.

As element reference is stored, then if the element is mutable, it affects the list where it is appended, if element is not mutable, it will not affect the list.

**Case-1: Immutable Element,**
```python
y = [2, 3]
z = 7
y.append(z)
z = 5
print(y)
```
As int object is immutable, hence `z=5` will create another object with value 5 although rebinding `z` does not affect stored references as element 3 of list `y` at memory!

**Case-2: Mutable Element,**
```python
y = [2, 3]
z = [5, 6]
y.append(z)
z[0] = 9
print(y)
```
As list object is mutable, hence `z[0] = 9` will create another int object with value 9 although `z` gets modified and as element 3 of list `y` is this `z`, it also reflects the changes!

> `elmnt`: Required. An element of any type: int, float, bool, str, complex, list, tuple, set, dict, function, class object, None.

| INT | LIST | DICT | FUNCTION |
|---|---|---|---|
| `nums = [1, 2]`<br>`nums.append(3)`<br>`nums: [1,2, 3]` | `lst = [1, 2]`<br>`lst.append([3,4])`<br>`lst:[1,2,[3, 4]]` | `lst = [1, 2]`<br>`lst.append({"name": "Arpan"})`<br>`[1, 2, {1: 'Ab'}]` | `def greet():`<br>&nbsp;&nbsp;`print("Hello")`<br>`lst = [1]`<br>`lst.append(greet)`<br>`[1, <function greet at 0x…>]` |

#### 2. `list.extend(iterable)`: adds the specified iterable elements to the end of the current list.

> `iterable`: Required. An iterable like list, tuple, set, dict.

It acts same exactly as `list()`

It actually does,
```python
for item in iterable:
    list.append(item)
```

| INT | LIST | DICT | FUNCTION |
|---|---|---|---|
| `nums = [1, 2]`<br>`nums.extend(3)`<br>`ERROR!`<br>`(TypeError: 'int' object is not iterable)` | `lst = [1, 2]`<br>`lst.extend([3,4])`<br>`lst:[1, 2, 3, 4]` | `lst = [1, 2]`<br>`lst.extend({1: "Ab"})`<br>`[1, 2, 1]` | `def greet():`<br>&nbsp;&nbsp;`print("Hello")`<br>`lst = [1]`<br>`lst.append(greet)`<br>`ERROR!` |

➔ **append() vs extend()**: Same as `[]` vs `list()`

#### 3. `list.insert(pos, elmnt)`: inserts a reference to the given object at pos in list.

> `pos`: Required. A number specifying in which position to insert the value
> `elmnt`: Required. An element of any type (string, number, object etc.)

It never throws indexing error.

| Value of POS | Result | Example |
|---|---|---|
| 0 | Insert at beginning | |
| 0 ≤ pos ≤ len(list) | Insert at that position | `lst.insert(1, 99)` → `[10, 99, 20, 30]` |
| ≥ len(list) | Insert at end | `lst.insert(10, 99)` → `[10, 20, 30, 99]` |
| ≤ - len(list) | Insert at beginning | `lst.insert(-10, 99)` → `[99, 10, 20, 30]` |

### 2. Removing Elements

#### 1. `list.remove(elmnt)`: removes the first occurrence (from left) of the element with the specified value. If value not present, throws ERROR.

> `elmnt`: Required. Any type (string, number, list etc.) The element you want to remove.

```python
nums = [10,20,30,20]
nums.remove(20)    #nums: [10, 30, 20]
nums.remove(99)    #ERROR!
```

#### 2. `list.pop(pos)`: removes the element at the specified position. If pos is out of bound, it throws OUT OF INDEX ERROR.

> `pos`: Optional. A number specifying the position of the element you want to remove, default value is -1, which returns the last item

```python
nums = [10,20,30,20]
nums.pop(3)        #nums: [10, 20, 30]
nums.pop(3)        #OUT OF BOUND ERROR!
```

#### 3. `list.clear()`: method removes all the elements from a list, makes that an empty list.

```python
nums = [10,20,30,20]
nums.clear()       #nums: []
```

### 3. Searching in List

#### 1. `list.index(elmnt, start, end)`: returns the position at the first occurrence of the elmnt value within the range, throws ERROR if element is not present, never throws indexing ERROR.

> `elmnt`: Required. Any type (string, number, list, etc.). The element to search for
> `start`: Required. Optional. A number representing where to start the search, default is 0
> `end`: Optional. A number representing where to end the search, default is -1

| Condition | Example Code | Output | Result |
|---|---|---|---|
| Element found | `lst.index(20)` | `1` | Returns first matching index |
| Element absent | `lst.index(50)` | `ValueError: 50 is not in list` | Element not found |
| start > len(lst) | `lst.index(20, 10)` | `ValueError: 20 is not in list` | Empty search range |
| Empty search range start == len(lst) | `lst.index(20, 6)` | `ValueError: 20 is not in list` | Empty search range |
| end > len(lst) | `lst.index(20, 1, 100)` | `1` | Searches until list end |
| start > end | `lst.index(20, 4, 2)` | `ValueError: 20 is not in list` | Empty search range |
| Negative start | `lst.index(20, -3)` | `3` | -3 becomes index 3 |
| Negative end | `lst.index(20, 0, -1)` | `1` | Searches in lst[0:5] |
| Both negative | `lst.index(20, -4, -1)` | `3` | Searches in lst[2:5] |
| start == end | `lst.index(20, 2, 2)` | `ValueError: 20 is not in list` | Empty search range |
| Valid range but element outside range | `lst.index(20, 4, 5)` | `ValueError: 20 is not in list` | Element exists in list but not in searched range |
| Valid range with multiple matches | `lst.index(20, 2)` | `3` | Returns first match within the range |

#### 2. `list.count(value)`: returns the number of elements with the specified value, if no element is there with that value, returns 0.

> `value`: Required. Any type (string, number, list, tuple, etc.). The value to search for

```python
[10, 20, 30, 20, 20].count(20)    #returns 3
[10, 20, 30, 20, 20].count(99)    #returns 0
```

### 5. Sorting

#### 1. `sorted(iterable, key=key, reverse=reverse)`: returns a **sorted list** of the specified iterable object and returns a **new list**, all elements of the iterable object must need to be comparable among themselves else produces *TypeError: '>' not supported*.

> `iterable`: Required. The sequence to sort, list, dictionary, tuple etc
> `key`: Optional. A Function to execute to decide the order. Default is None
> `reverse`: Optional. A Bool. **False sorts ascending, True sorts descending**. Default is False

> Python 3 does **not allow ordering comparisons between unrelated types** like:
> - int and str
> - str and complex   So comparison type funct can't determine which element is largest.
> - float and str
> - etc.

```python
nums = [10,20,30,20]
nums2 = sorted(nums)
print(nums2)    #nums: [10,20,30,20], nums2: [10,20, 20,30]
```
*Original list remains unchanged*

```python
print(sorted("python"))    #returns ['h','n','o','p','t','y']
```

```python
print(sorted({"c":3,"a":1,"b":2}))    #returns ['a', 'b', 'c']
```
*By default, all functions iterate over key of iterable dict*

```python
print(sorted([10, 4.5, True]))    #returns [True, 4.5, 10]
```

```python
print(sorted([1, "arpan", 2+3j, 4.5]))    #returns TypeError: '>' not supported between instances of 'str' and 'int'
```

#### 2. `list.sort(reverse=True|False, key=myFunc)`: sorts the list ascending by default. You can also make a function to decide the sorting criteria(s) and **does sorting on existing list**, all elements of the list must need to be comparison supported among themselves else produces *TypeError: '>' not supported*.

> `key`: Optional. A Function to execute to decide the order. Default is None
> `reverse`: Optional. A Bool. **False sorts ascending**, **True sorts descending**. Default is False

```python
nums = [10,20,30,20]
nums.sort()
print(nums)    #nums: [10, 20, 20, 30]
```
*Original list changed*

```python
def myFunc(e):    #function returns the length of values:
    return len(e)
```

```python
cars = ['Ford', 'TATA', 'BMW', 'VW']
cars.sort(key=myFunc)    #OP['VW','BMW','Ford','TATA']
```

```python
def myFunc(e):    ##function that returns the 'year' value:
    return e['year']

cars = [
  {'car': 'Ford', 'year': 2000},
  {'car': 'Mitsubishi', 'year': 2000},
  {'car': 'BMW', 'year': 2019},
  {'car': 'VW', 'year': 2011}
]
cars.sort(key=myFunc, reverse=True)
print(cars)
```
**OP:** `[{'car': 'BMW', 'year': 2019}, {'car': 'VW', 'year': 2011}, {'car': 'Ford', 'year': 2000}, {'car': 'Mitsubishi', 'year': 2000}]`

```python
nums = [4,1,3]
nums = nums.sort()    #nums.sort() returns None
print(nums)    #nums: None
```

| Feature | `sorted()` | `sort()` |
|---|---|---|
| Type | Built-in function | List method |
| Works on | Any iterable | Only lists |
| Modifies original list? | ❌ No | ✅ Yes |
| Returns | New sorted list | None (But internally sorts inplace) |
| Syntax | `sorted(iterable)` | `list.sort()` |

#### 3. `list.reverse()`: **In place** reversal of list, reverses order of the elements.

### 6. Useful Functions

#### 1. `len(list)`: returns length (# of elements) of the list.

```python
nums = [10,20,30,20]
len(nums)    #returns 4
```

#### 2. `max(list)`: returns max among elements of the list by comparing among them. All elements inside the list must need to be **comparable**, else produces *TypeError: '>' not supported*.

```python
nums = [10,20,30,20]
max(nums)    #returns 30
```
```python
max([10, 4.5, True])    #returns 10
```
```python
max([1, "arpan", 2+3j, 4.5])    #returns TypeError: '>' not supported between instances of 'str' and 'int'
```

#### 3. `min(list)`: returns min among elements of the list by comparing among them.

`min(list)` `max(list)`

#### 4. `sum(list)`: returns the arithmetic sum of the elements. The elements should be **numeric types** (int, float, bool, complex) or otherwise support addition. If addition is not supported between the elements, a **TypeError** is raised.

---

## NESTED LISTS: Lists inside lists.

```python
MATRIX = [
  [1,2,3],
  [4,5,6],
  [7,8,9]
]
```

**ACCESS:** `MATRIX[1][2]`   **OUTPUT:** `6`

## OPERATORS ON LIST

#### 1. + (Concatenation):
```python
[1, 2] + [3, "Ab"]
```
**Output:** `[1,2,3,"Ab"]`

#### 2. * (Repetition):
```python
[1,2] * 3
```
**Output:** `[1,2,1,2,1,2]`

#### 3. In (Membership):
```python
10 in [10,20,30]
```
**Output:** `True`

## COPYING LIST

#### 1. Assignment
```python
a = [10,20,30]
b = a
# Both point to the same list, hence any changes made on
# the list by any of the variable, affects the common list
b.append(40)
a    #Output: [10,20,30,40]
```

#### 2. Shallow Copy
```python
c = a.copy()
#Now separate list objects exist.
```

## ITERATING THROUGH LISTS

#### 1. Using for
```python
nums = [10,20,30]
for x in nums:
    print(x)
```

#### 2. Using range()
```python
for i in range(len(nums)):
    print(nums[i])
```

#### 3. enumerate()
```python
for index, value in enumerate(nums):
    print(index, value)
```
**Output:**
```
0 10
1 20
2 30
```

## LIST COMPREHENSION

| Traditional | List comprehension | List comprehension with condition |
|---|---|---|
| ```python<br>squares = []<br>for x in range(5):<br>    squares.append(x*x)<br>```<br>OP: `[0,1,4,9,16]` | ```python<br>squares = [x*x for x in range(5)]<br>```<br>OP: `[0,1,4,9,16]` | ```python<br>evens = [x for x in range(10) if x%2==0]<br>```<br>OP: `[0,2,4,6,8]` |

| Operation | Complexity |
|---|---|
| Access/Delete by index | O(1) |
| append() | O(1) amortized |
| pop() last | O(1) |
| insert() beginning | O(n) |
| remove() | O(n) |
| search | O(n) |
| sort() | O(n log n) |
