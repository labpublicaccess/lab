# MapReduce Finding Unit-wise Salary

## Input Data
Certainly! Here's the Markdown with instructions, mapper code, reducer code, and explanations for the fourth question:

```markdown
# MapReduce Finding Unit-wise Salary

## Input Data

Create a file named `input4.txt` and paste the following content:

```plaintext
EmpNo,EmpName,Unit,Designation,Salary
1001,John,IMST,TA,30000
1002,Jack,CLOUD,PM,80000
1003,Joshi,FNPR,TA,35000
1004,Jash,ECSSAP,PM,75000
1005,Yash,FSADM,SPM,60000
1006,Smith,ICS,TA,24000
1007,Lion,IMST,SPM,56000
1008,Kate,FNPR,PM,76000
1009,Cassy,MFGADM,TA,40000
1010,Ronald,ECSSAP,SPM,65000
```

## Creating Input File

To create the input file, open a terminal and run the following command:

```bash
sudo gedit input4.txt
```

Paste the above content into the text editor and save the file.

## Mapper

Create a file named `mapper4.py` and paste the following Python code:

```python
#!/usr/bin/env python

import sys

for line in sys.stdin:
    if "EmpNo" not in line:
        _, _, unit, _, salary = line.strip().split(',')
        print(f'{unit}\t{salary}')
```

### Mapper Explanation

The Mapper reads input lines, extracts unit and salary information, and outputs key-value pairs in the format `unit   salary`. This format is necessary for grouping salaries by unit during the MapReduce process.

## Reducer

Create a file named `reducer4.py` and paste the following Python code:

```python
#!/usr/bin/env python

import sys

current_key = None
total_salary = 0

for line in sys.stdin:
    key, value = line.strip().split('\t')
    total_salary += int(value)

if current_key:
    print(f'{current_key}\t{total_salary}')
```

### Reducer Explanation

The Reducer processes the key-value pairs emitted by the Mapper. It accumulates the total salary for each unit. The output is in the format `unit   total_salary`.

## Testing

To check if the Mapper and Reducer are working, use the following commands:

```bash
cat input4.txt | python3 mapper4.py
cat input4.txt | python3 mapper4.py | sort | python3 reducer4.py
```

This should output the total salary for each unit.
```

Make sure to save this content in a file named `readme.md` in the same directory as your solution files. The additional instructions guide users on creating the input file using `sudo gedit`.
Create a file named `input4.txt` and paste the following content:

```plaintext
EmpNo,EmpName,Unit,Designation,Salary
1001,John,IMST,TA,30000
1002,Jack,CLOUD,PM,80000
1003,Joshi,FNPR,TA,35000
1004,Jash,ECSSAP,PM,75000
1005,Yash,FSADM,SPM,60000
1006,Smith,ICS,TA,24000
1007,Lion,IMST,SPM,56000
1008,Kate,FNPR,PM,76000
1009,Cassy,MFGADM,TA,40000
1010,Ronald,ECSSAP,SPM,65000
```

## Creating Input File

To create the input file, open a terminal and run the following command:

```bash
sudo gedit input4.txt
```

Paste the above content into the text editor and save the file.

## Mapper

Create a file named `mapper4.py` and paste the following Python code:

```python
#!/usr/bin/env python

import sys

for line in sys.stdin:
    if "EmpNo" not in line:
        _, _, unit, _, salary = line.strip().split(',')
        print(f'{unit}\t{salary}')
```

### Mapper Explanation

The Mapper reads input lines, extracts unit and salary information, and outputs key-value pairs in the format `unit   salary`. This format is necessary for grouping salaries by unit during the MapReduce process.

## Reducer

Create a file named `reducer4.py` and paste the following Python code:

```python
#!/usr/bin/env python

import sys

current_key = None
total_salary = 0

for line in sys.stdin:
    key, value = line.strip().split('\t')
    total_salary += int(value)

if current_key:
    print(f'{current_key}\t{total_salary}')
```

### Reducer Explanation

The Reducer processes the key-value pairs emitted by the Mapper. It accumulates the total salary for each unit. The output is in the format `unit   total_salary`.

## Testing

To check if the Mapper and Reducer are working, use the following commands:

```bash
cat input4.txt | python3 mapper4.py
cat input4.txt | python3 mapper4.py | sort | python3 reducer4.py
```

This should output the total salary for each unit.
