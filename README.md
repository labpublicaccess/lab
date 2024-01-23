# Hadoop MapReduce Example

This guide will walk you through setting up a simple Hadoop MapReduce job using Python. Ensure you have VMware Player installed and configured.

1. Open VMware Player and start the master process:
   ```bash
   # Example command to start the process
   ./start-all.sh
   ```

2. Create an input file named `input.txt` in the master folder:
   ```bash
   # Use nano to create and edit the file
   sudo nano input.txt
   ```

3. Put the `input.txt` file into the Hadoop Distributed File System (HDFS):
   ```bash
   # Example command to put the file into HDFS
   hdfs dfs -put <path_to_file> /user/<your_username>/
   ```

4. Create a Mapper script (`mapper.py`):
   ```python
   #!/usr/bin/env python

   import sys

   # Input comes from STDIN (standard input)
   for line in sys.stdin:
       # Remove leading and trailing whitespaces
       line = line.strip()
       # Split the line into words
       words = line.split()
       # Output each word with a count of 1
       for word in words:
           print(f"{word}\t1")
   ```

5. Create a Reducer script (`reducer.py`):
   ```python
   #!/usr/bin/env python

   from operator import itemgetter
   import sys

   current_word = None
   current_count = 0
   word = None

   # Input comes from STDIN
   for line in sys.stdin:
       # Remove leading and trailing whitespaces
       line = line.strip()

       # Parse the input we got from the mapper
       word, count = line.split('\t', 1)

       # Convert count to an integer
       try:
           count = int(count)
       except ValueError:
           # Count was not a number, ignore this line
           continue

       # Check if the current word is the same as the previous word
       if current_word == word:
           current_count += count
       else:
           # Print the result for the previous word
           if current_word:
               print(f"{current_word}\t{current_count}")
           current_count = count
           current_word = word

   # Print the result for the last word
   if current_word == word:
       print(f"{current_word}\t{current_count}")
   ```

6. To run the Mapper and check the output:
   ```bash
   cat input.txt | python3 mapper.py
   ```

7. To run the Reducer, sort the output, and check the final result:
   ```bash
   cat input.txt | python3 mapper.py | sort | python3 reducer.py
   ```

Feel free to adapt the code and commands based on your specific environment and requirements. Happy coding!
```
