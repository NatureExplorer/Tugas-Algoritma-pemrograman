Exercise :
1. Buatlah sebuah series S. S adalah deret bilangan bulat dari -5 hingga 10 ! 
```python
import pandas as pd
import numpy as np

s = pd.Series([-5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
print (s)
```
2. Terdapat dataframe yang terdiri dari NIM dan nilai UTS mahasiswa sebagai kolom nya. 
- Buatlah dataframe tersebut dengan jumlah mahasiswa 100 orang. NIM di generate secara random tetapi harus unique. NIM terdiri 3 digit. Nilai UTS di generate secara random dengan batas dari [0-100]. Konstruksi kan dataframe tersebut dari sebuah dictionary! 
```python
x = (list(np.random.randint(low= 100, high = 999, size = 100)))
y = (list(np.random.randint(low = 0, high = 100, size = 100)))
df = pd.DataFrame({'NIM' : x, 'NILAI UTS' : y})
df.head(10)
```
- Dari dataframe nilai tersebut, hitung rata-rata , min-max dan quartil nya! 
```python
df.describe()   
```

- Tampilkan mahasiswa dengan nilai >= 50!
```python
df[df['NILAI UTS'] >= 50]
```
- Hapus data mahasiswa dengan nim genap! 
```python
res_1 = df[df['NIM'] %2 == 0].index
list_res = df.drop(res_1, inplace=True)
print(df['NIM'])
```

- Urutkan dataframe berdasarkan NIM terkecil ! 
```python
print(df.sort_values(by=['NIM']))
```
- Tampilkan 15 mahasiswa dengan nilai terbesar!
```python
res_2  = df.sort_values(by = 'NILAI UTS', ascending= False)
res_2.head(15)
```
