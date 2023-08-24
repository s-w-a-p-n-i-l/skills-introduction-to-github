# Scrapping Table Data

```ts
import requests
from bs4 import BeautifulSoup
import pandas as pd
```
*Here,*we import `pandas` to arrange and store 

```ts
a=requests.get('https://www.worldometers.info/coronavirus/countries-where-coronavirus-has-spread/')
```
`a` -> variable
`requests` -> library
`.get `-> method

```ts
b=BeautifulSoup(a.text,'lxml')
```
library help to access the data
```ts
data=b.find('table',id='table3')
```
we here selected table because table  **cover all the elements** we want

***Now,***



```ts
// Extract Head 
head=data.find('tr')
h_data=[hd.text for hd in head.find_all('th')]
```
**Here** 
`columns=h_data` -> is to specify the column names
```ts
df=pd.DataFrame(columns=h_data)
```

```ts
//body
rows=data.find_all('tr')[1:]
for row in rows: 
    b_data=row.find_all('td')
    content=[bd.text for bd in b_data] 
    df.loc[len(df)]=content
```

`to_csv` -> save the file in ***Excel format***
```ts
print(df)
df.to_csv('jamla.csv',index=False)
```