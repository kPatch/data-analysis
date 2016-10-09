# data-analysis
Notes and Code on Data Analysis using Python

```python
// Open file and read
path = 'this/is/a/path/file.txt'
open(path).readline() // Read a single line

// Read file as JSON
import json
path = 'this/a/path/file.txt'
records = [json.loads(line) for line in open(path)] // A list comprehension

records[0] // Prints the first record

print records[0]['tz']
```

**Counting Time Zones in Pure Python**

```python
time_zones = [rec['tz' for rec in records] // Will throw an error if not all records have a time zone field

time_zones = [rec['tz'] for rec in records if 'tz' in rec] // Add conditional check

time_zones[:10] // Look at the first 10 time zones
```

**Counting Using Python
```python
// The tough way

def get_count(sequence):
    counts = {}
    for x in sequence:
        if x in counts:
            counts[x] += 1
        else:
            counts[x] = 1
    return counts
```

**Counting Using Pandas**

```python
from pandas import DataFrame, Series
import pandas as pd
frame = DataFrame(records)
frame 
frame['tz'][:10]
tz_counts = frame['tz'].value_counts()
tz_counts[:10]

```

The main pandas data structure is the DataFrame

You can do a bit of **munging** to fill in a substitue value for unknown and missing time zone data in records
The fillna function can replace missing (NA) values and unknown (empty strings) values can be replaced by boolean array indexing

```python
clean_tz = frame['tz'].fillna('Missing')
clean_tz[clean_tz == ''] = 'Unknown'
tz_counts = clean_tz.value_counts()
tz_counts[:10]
``` 

**Plot a Graph**
```python
tz_counts[:10].plot(kind='barth', rot=0)

```
