## Latihan
1. Lengkapi tabel berikut ini!

| Sequence Type | Mutability | Access by Index | Duplicate Element | Change Element | Add / Remove Element |
| ------------- | ---------- | --------------- | ----------------- | -------------- | -------------------- |
| List          |            |                 |                   |                |                      |
| Tuple         |            |                 |                   |                |                      |
| Set           |            |                 |                   |                |                      |
| Dictionary    |            |                 |                   |                |                      |

**JAWAB=**

2. Terdapat data sebagai berikut: 
	**data:** 1,2,1,2,3,10,11,5,6,19,20,30,50,50,50,20,9,4,5,12,11,11,30,50,90,80,80
	dengan mengimplementasi sequence type , buatlah program untuk:
	- Menghitung rata rata dari data tersebut
	- Mencari apa saja nilai unik yang dari data tersebut
	- Menghitung frekuensi kemunculan dari setiap elemen unik tersebut
  
 **JAWAB=**
 ```python
 import statistics
data = (1,2,1,2,3,10,11,5,6,19,20,30,50,50,50,20,9,4,5,12,11,11,30,50,90,80,80)

total = 0
for jumlah in range (0,len(data)):
  total = total + data[jumlah]

mean = total / len(data)
modus = max(set(data),key = data.count)
mid = statistics.median(data)
print(f'Maka Nilai rata-rata data tersebut adalah {mean}')
print(f'Nilai modus dari data tersebut adalah {modus}')
print(f'Nilai Median dari data tersebut adalah {mid}'
```

3. Terdapat tabel grade mahasiswa sebagai berikut:

| NIM        | NAMA  | ALPRO | STRUKDAT | ADS | LMD | ALE |
| ---------- | ----- | ----- | -------- | --- | --- | --- |
| 1301142289 | ISA   | A     | A        | A   | A   | A   |
| 1301140389 | LIA   | C     | A        | B   | A   | AB  |
| 1301142099 | NAMDY | B     | B        | BC  | AB  | D   |
| 1301142091 | SANDI | B     | C        | D   | A   | A   | 

- Jelaskan sequence type apa yang cocok digunakan untuk mengolah data tersebut!
- Buatlah program untuk menghitung ipk dari setiap mahasiswa pada tabel tersebut!
**JAWAB=**

4. The Anagram Problem.

Original Text: 'Institut Teknologi Sumatera'

Result Text: EAIGLKNMROTSU

Buatlah program untuk mengubah sebuah string menjadi string lain dengan rule sebagai berikut:
- Hasil result string seluruhnya adalah capital.
- Tidak ada huruf yang duplikat dalam string result.
- Posisi character si string baru terurut secara ascending, namun index genap dan ganjil di tukar dalam pair. Contoh: AEJK menjadi EAKJ.
**JAWAB=**
```python
masukkan = input('Masukkan teks yang anda inginkan > ')
def swap(nums):
    for i in range(0, len(nums) - 1, 2):
        nums[i], nums[i + 1] = nums[i + 1], nums[i]
    return nums
anagram=''
word = masukkan.upper().replace(" ","")
sorted_word = sorted(set(word))
sorted_word = ''.join(sorted_word)
arr=list(sorted_word)
for x in swap(arr):
    anagram += x
print("Teks yang anda masukkan : "+masukkan)
print("Teks saat sudah menjadi anagram :" + anagram)
```
