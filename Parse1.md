```python
import re
import pandas as pd
import os
import string as st
```


```python
list = pd.read_csv("lt.txt", sep="\t")
#misc = pd.read_csv("p.txt", sep="\t")
```


```python
lt1 = list.replace(to_replace='\[', value="(", regex=True)
lt1 = lt1.replace(to_replace='\]', value=")", regex=True)
lt1 = lt1.replace(to_replace='\{', value="(", regex=True)
lt1 = lt1.replace(to_replace='\}', value=")", regex=True)
```


```python
lt1['paren'] = lt1['ALBUM'].str.contains("(", regex=False)
lt1['trailpar'] = lt1['ALBUM'].str.endswith(")", na=False)
```


```python
#lp = lt1[lt1['paren']==True]
```


```python
#lout = lp['ALBUM'].str.extractall(r"\(([^)]+)\)").unstack()
```


```python
lt1['misc'] = lt1.ALBUM.str.findall("\((.*?)\)").tolist()
```


```python
lt1['date1'] = lt1['ALBUM'].str.extract(r"\b(\d\d\d\d\)|\d\d\d\d\| \d\d\d\d\|\d\d\d\d\ |-\d\d\d\d\|\d\d\d\d-\d\d\d\d|\d\d\d\d-\d\d|199x|200x)", expand=True)
```


```python
lt1['nfo']= lt1['ALBUM'].str.extract(r"\b(EP|Bootleg|12''|12'' vinyl|12'' Vinyl|Vinyl|Tape Only|Tape Rip|OG TAPE RIP|TAPE RIP|Demo Tape|DEMO TAPE|demo tape|Maxi|Maxi Single|CDS|CDM|VLS|cassette|Promo|2CD|Single|320k|192k|128k|320 kbs|192 kbs|128 kbs|320Kbps|160 kbps|E.P. )", expand=True)
```


```python
#lt1['album']= lt1['ALBUM'].str.strip(r"\b(EP|Bootleg|12''|12'' vinyl|12'' Vinyl|Vinyl|Tape Only|Tape Rip|OG TAPE RIP|TAPE RIP|Demo Tape|DEMO TAPE|demo tape|Maxi|Maxi Single|CDS|CDM|VLS|cassette|Promo|2CD|Single|320k|192k|128k|320 kbs|192 kbs|128 kbs|320Kbps|160 kbps|E.P. )")
```


```python
#lt1['album'] = lt1['ALBUM'].str.rstrip(r"\b(\d\d\d\d\)|\d\d\d\d\| \d\d\d\d\|\d\d\d\d\ |-\d\d\d\d\|\d\d\d\d-\d\d\d\d|\d\d\d\d-\d\d|199x|200x)")
```


```python
lt1
