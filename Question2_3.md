# MapReduce Sorting by Student Name

## Input Data

Create a file named `input3.txt` and paste the following content:

```plaintext
1001,John,45
1002,Jane,68
1003,Bob,75
1004,Alice,55
1005,Charlie,90
1006,Eve,82
1007,David,63
1008,Frank,78
1009,Grace,92
1010,Henry,60
1011,Isabel,70
1012,Jack,80
1013,Kate,88
1014,Liam,50
1015,Mia,72
1016,Noah,65
1017,Olivia,85
1018,Peter,58
1019,Quinn,76
1020,Riley,95
```

## Mapper

Create a file named `mapper3.py` and paste the following Python code:

```python
#!/usr/bin/env python

import sys

for line in sys.stdin:
    registration, name, marks = line.strip().split(',')
    print(f'{name}\t{registration},{marks}')
```

### Mapper Explanation

The Mapper reads input lines, extracts student details (registration, name, marks), and outputs key-value pairs in the format `name   registration,marks`. This format is crucial for sorting the data by student name during the MapReduce process.

## Reducer

Create a file named `reducer3.py` and paste the following Python code:

```python
#!/usr/bin/env python

import sys

current_key = None
student_details = []

for line in sys.stdin:
    key, value = line.strip().split('\t')
    registration, marks = value.split(',')
    student_details.append((registration, int(marks)))

if student_details:
    student_details.sort()
    for registration, marks in student_details:
        print(f'{registration},{marks}')
```

### Reducer Explanation

The Reducer processes the key-value pairs emitted by the Mapper. It accumulates student details in a list and sorts them by registration number. The output is in the format `registration,marks`.

## Testing

To check if the Mapper and Reducer are working, use the following commands:

```bash
cat input3.txt | python3 mapper3.py
cat input3.txt | python3 mapper3.py | sort | python3 reducer3.py
```

This should output the sorted student details based on their names.
```

Save this content in a file named `readme.md` in the same directory as your solution files. The explanations provide a clearer understanding of what each component does.
