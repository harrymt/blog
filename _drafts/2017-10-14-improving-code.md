---
published: false
---
## Improving Code


<img src="{{ site.baseurl }}/img/bloomberg-task.png">

### Sample Input/Output

**INPUT**
```
4
1234567890123
1234567890128
1111111111116
1111111111118
```

**OUTPUT**
```
NOT VALID
VALID
VALID
NOT VALID
```

**EXPLANATION**
By applying the formula used above, we check if the ISBN is valid.


### First Solution

```python
import sys

data = [
    '4',
    '1234567890123'
    '1234567890128',
    '1111111111116',
    '1111111111118'
]

for line in data:
    thesum = 0
    weight = 3
    if len(line) != 13:
        continue

    for char in list(line):
        if weight == 3:
            weight = 1
        else:
            weight = 3

        thesum = thesum + (int(char) * weight)

    if thesum % 10 == 0:
        print("VALID")
    else:
        print("NOT VALID")

```




### Second Solution

```python
if weight == 3:
    weight = 1
else:
    weight = 3
```

Turns into:

```python
weight += 2
weight %= 4
```

Results in full source:

```python
import sys

data = [
    '4',
    '1234567890123',
    '1234567890128',
    '1111111111116',
    '1111111111118'
]

for line in data:
    if len(line) != 13:
        continue

    thesum = 0
    weight = 3

    for char in list(line):
        weight += 2
        weight %= 4

        thesum += (int(char) * weight)

    if thesum % 10 == 0:
        print("VALID")
    else:
        print("NOT VALID")

```
