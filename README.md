### EX3 Implementation of GSP Algorithm In Python
### DATE: 
### AIM: To implement GSP Algorithm In Python.
### Description:
The Generalized Sequential Pattern (GSP) algorithm is a data mining technique used for discovering frequent patterns within a sequence database. It operates by identifying sequences that frequently occur together. GSP works by employing a depth-first search strategy to explore and extract frequent patterns efficiently.
### Steps:
1. <strong>Database Scanning:</strong> GSP scans the sequence database to determine the support of each item in the dataset.
2. <strong>Candidate Generation:</strong> It generates a set of candidate sequences using frequent items found in the previous step.
3. <strong>Pattern Growth:</strong> It extends the candidate sequences by merging them to form longer patterns, checking their support against a user-defined minimum support threshold.
4. <strong>Repeat:</strong> The process continues until no new sequences meet the minimum support threshold.
<p align="justify">
GSP finds application in various domains such as market basket analysis, web usage mining, bioinformatics, and more. For instance, in retail, GSP can identify common purchasing patterns, helping businesses understand customer behavior for targeted marketing or inventory management.
</p>

### Procedure:
<p align="justify">
1. From collections import defaultdict, from itertools import combinations: Imports necessary libraries/modules. defaultdict is
used to create a dictionary with default values and combinations generates all possible combinations of a sequence.</p>
<p align="justify">
2. generate_candidates(dataset, k): Function to generate candidate k-item sequences from a dataset. It loops through each sequence in the
dataset and finds combinations of length k for each sequence, updating their counts in a dictionary.</p>
<p align="justify">
3. gsp(dataset, min_support): Function that implements the Generalized Sequential Pattern (GSP) algorithm. It iterates through increasing
sequence lengths (k) until no new frequent patterns are found. It calls generate_candidates() to find patterns of varying lengths.</p>
<p align="justify">
4. Example dataset for each category: Defines example sequences for top wear, bottom wear, and party wear categories.</p>
<p align="justify">
5. Minimum support threshold: Sets the minimum support count required for a pattern to be considered frequent.</p>
<p align="justify">
6. Perform GSP algorithm for each category: Applies the GSP algorithm for each category using the defined example datasets and the
minimum support threshold.</p>
<p align="justify">
7. Output the frequent sequential patterns for each category: Prints the frequent sequential patterns 
    along with their support counts
for each wear category.</p>
<p align="justify">
8. Visulaize the sequence patterns using matplotlib.
</p>
### Program:

```python
ffrom collections import defaultdict
from itertools import combinations

# Function to generate candidate k-item sequences
def generate_candidates(dataset, k):
  c = defaultdict(int)
  result = {}
  for seq in dataset:
    for comb in combinations(seq , k):
      c[comb] += 1
  for item , sup in c.items():
    if sup >= min_support:
      result[item] = sup
  return result

# Function to perform GSP algorithm
def gsp(dataset, min_support):
  c = defaultdict(int)
  fp = defaultdict(int)
  k = 1
  while True:
    c = generate_candidates(dataset , k)
    if not c:
      break
    fp.update(c)
    k += 1
  return fp;


# Example dataset for each category
dataset = [
    ['a' , 'b' , 'c' , 'b' , 'e' , 'c' , 'f' , 'g' , 'a' , 'b' , 'e'] ,
    ['a' , 'd' , 'b' , 'c' , 'c' , 'f' , 'g' , 'c', 'h'] ,
    ['b' , 'c' , 'a' , 'd', 'e' , 'b' , 'f' ,'c' , 'd' , 'f' , 'g' , 'h'] ,
    ['c' , 'e' , 'c' , 'e' , 'c']
]

# Minimum support threshold
min_support = 4

# Perform GSP algorithm for each category
dataset_result = gsp(dataset, min_support)

# Output the frequent sequential patterns for each category
grouped = defaultdict(list)
for pattern, support in dataset_result.items():
    grouped[len(pattern)].append((pattern, support))

# Print tables
for length in sorted(grouped.keys()):
    print(f"\nFrequent Sequential Patterns of length {length}\n")
    print("{:<25} {:<10}".format("Pattern", "Support"))
    print("-" * 35)

    for pattern, support in grouped[length]:
        print("{:<25} {:<10}".format(str(pattern), support))

```
### Output:

```
Frequent Sequential Patterns of length 1

Pattern                   Support   
-----------------------------------
('a',)                    4         
('b',)                    6         
('c',)                    10        
('e',)                    5         
('f',)                    4         

Frequent Sequential Patterns of length 2

Pattern                   Support   
-----------------------------------
('a', 'b')                6         
('a', 'c')                6         
('a', 'e')                4         
('a', 'f')                4         
('b', 'c')                9         
('b', 'b')                4         
('b', 'e')                6         
('b', 'f')                7         
('b', 'g')                5         
('c', 'b')                4         
('c', 'e')                7         
('c', 'c')                8         
('c', 'f')                7         
('c', 'g')                6         
('e', 'c')                5         
('f', 'g')                4         
('d', 'c')                4         
('d', 'f')                4         
('c', 'h')                5         

Frequent Sequential Patterns of length 3

Pattern                   Support   
-----------------------------------
('a', 'b', 'c')           7         
('a', 'b', 'e')           6         
('a', 'b', 'f')           5         
('a', 'b', 'g')           4         
('a', 'c', 'c')           4         
('a', 'c', 'f')           5         
('a', 'c', 'g')           5         
('a', 'f', 'g')           4         
('b', 'c', 'b')           5         
('b', 'c', 'e')           5         
('b', 'c', 'c')           5         
('b', 'c', 'f')           9         
('b', 'c', 'g')           8         
('b', 'c', 'a')           4         
('b', 'b', 'e')           4         
('b', 'e', 'f')           4         
('b', 'f', 'g')           7         
('c', 'b', 'e')           4         
('c', 'e', 'c')           6         
('c', 'f', 'g')           7         
('a', 'd', 'c')           4         
('a', 'd', 'f')           4         
('a', 'c', 'h')           4         
('d', 'b', 'c')           4         
('d', 'c', 'h')           4         
('d', 'f', 'g')           4         
('d', 'f', 'h')           4         
('b', 'c', 'h')           6         
('b', 'f', 'h')           5         
('c', 'c', 'h')           4         
('c', 'f', 'h')           5         
('c', 'g', 'h')           4         
('b', 'c', 'd')           4         
('b', 'd', 'f')           4         
('c', 'd', 'f')           4         

Frequent Sequential Patterns of length 4

Pattern                   Support   
-----------------------------------
('a', 'b', 'c', 'b')      4         
('a', 'b', 'c', 'e')      4         
('a', 'b', 'c', 'c')      4         
('a', 'b', 'c', 'f')      6         
('a', 'b', 'c', 'g')      6         
('a', 'b', 'b', 'e')      4         
('a', 'b', 'f', 'g')      5         
('a', 'c', 'b', 'e')      4         
('a', 'c', 'f', 'g')      5         
('b', 'c', 'b', 'e')      5         
('b', 'c', 'f', 'g')      9         
('b', 'c', 'a', 'b')      4         
('b', 'c', 'a', 'e')      4         
('b', 'e', 'f', 'g')      4         
('a', 'd', 'b', 'c')      4         
('a', 'd', 'c', 'h')      4         
('a', 'd', 'f', 'g')      4         
('a', 'd', 'f', 'h')      4         
('a', 'b', 'c', 'h')      4         
('d', 'b', 'c', 'h')      4         
('d', 'f', 'g', 'h')      4         
('b', 'c', 'c', 'h')      4         
('b', 'c', 'f', 'h')      6         
('b', 'c', 'g', 'h')      5         
('b', 'f', 'g', 'h')      5         
('c', 'f', 'g', 'h')      5         
('b', 'c', 'd', 'f')      5         
('b', 'c', 'd', 'g')      4         
('b', 'c', 'd', 'h')      4         
('b', 'd', 'f', 'g')      4         
('b', 'd', 'f', 'h')      4         
('c', 'd', 'f', 'g')      4         
('c', 'd', 'f', 'h')      4         

Frequent Sequential Patterns of length 5

Pattern                   Support   
-----------------------------------
('a', 'b', 'c', 'b', 'e') 5         
('a', 'b', 'c', 'f', 'g') 6         
('a', 'd', 'b', 'c', 'h') 4         
('a', 'd', 'f', 'g', 'h') 4         
('b', 'c', 'f', 'g', 'h') 6         
('b', 'c', 'd', 'f', 'g') 5         
('b', 'c', 'd', 'f', 'h') 5         
('b', 'c', 'd', 'g', 'h') 4         
('b', 'd', 'f', 'g', 'h') 4         
('c', 'd', 'f', 'g', 'h') 4         

Frequent Sequential Patterns of length 6

Pattern                   Support   
-----------------------------------
('b', 'c', 'd', 'f', 'g', 'h') 5         
```

### Visualization:
```python
import matplotlib.pylot as plt
patterns = []
supports = []

for pattern, support in dataset_result.items():
    patterns.append(str(pattern))
    supports.append(support)

plt.figure()
plt.plot(patterns, supports, marker='o')
plt.xlabel("Patterns")
plt.ylabel("Support Count")
plt.title("Frequent Sequential Patterns")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
### Output:



### Result:
Therefore , the implementation of gsp algoritm in python is completed successfully.
