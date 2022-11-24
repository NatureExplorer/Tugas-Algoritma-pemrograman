### Latihan

1. Height of Presidents. List Height berikut adalah data tinggi badan presiden negara A. 

height = \[189 170 189 163 183 171 185 168 173 183 173 173 175 178 183 193 178 173
 174 183 183 168 170 178 182 180 183 178 182 188 175 179 183 193 182 183
 177 185 188 188 182 185\]

Buatlah program python dengan mengimplementasikan numpy array untuk mengitung rata-rata, median , simpangan baku, dan tinggi maksimum dan minimum pada data height tersebut.
```python
import numpy as np

height = [189, 170, 189, 163, 183, 171, 185, 168, 173, 183, 173, 173, 175, 178, 183, 193, 178, 173, 174, 183, 183, 168, 170, 178, 182, 180, 183, 178, 182, 188, 175, 179, 183, 193, 182, 183, 177, 185, 188, 188, 182, 185]

mean = np.mean(height)
median = np.median(height)
standar_deviasi = np.std(height)
maximum = np.max(height)
minimum = np.min(height)

print("Nilai rata-rata : ", mean)
print("Nilai median : ", median)
print("Nilai simpangan baku : ", standar_deviasi)
print("Nilai tinggi maksimum : ", maximum)
print("Nilai tinggi mininum : ", minimum)
```

2. Estimating pi using dart


![Image 1](https://raw.githubusercontent.com/riksameidy/exercise-alpro-2022/master/estimating_pi_with_dart.png)


Anda adalah pemain dart yang sangat buruk sehingga ketika anda melemparkan dart ke target, hasilnya selalu random. Anda ingin menggunakan ketidakahlian anda untuk sesuatu yang lain, yaitu mengestimasikan nilai $\pi$. Nilai $\pi$ dapat di estimasikan dengan cara membangkitkan bilangan acak pada area biru dan orange.
Karena setiap lemparan akan menghasilkan titik secara acak, baik di area orange maupun biru, maka peluang dart akan kena di  lingkaran orange adalah rasio antara luas persegi biru dan lingkaran orange:

$$P_{circle} = \frac{Area_{circle}}{Area_{square}} = \frac{\pi r^2}{(2r)^2} = \frac{\pi}{4}$$

dengan menggunakan approksimasi, maka peluang $P_{circle}$ dapat didekati dengan :

$$ P_{circle} \approx \frac{N_{circle}}{N_{square}+N_{circle}} $$

$$ \frac{\pi}{4} \approx \frac{N_{circle}}{N_{square}+N_{circle}} $$

dimana $N_{circle}$ adalah jumlah dart yang kena di di  lingkaran orange dan $N_{square}$ adalah jumlah dart yang kena di area biru. Berdasarkan persamaan diatas kita juga mendapatkan hubungan berikut:

$$ N = N_{circle} + N_{square}$$

dimana N adalah jumlah pelemparan total dari dart.

Asumsikan titik pusat lingkaran adalah koordinat (0,0)

Buatlah program python dengan numpy array untuk mengestimasikan nilai $\pi$ dengan jumlah N=10000 dan r = 1 menggunakan cara:
- Unvectorized Solution
- Vectorized Solution
```python
#Unvectorized
import numpy as np 
N = 10000
dart_positions = 2 * np.random.rand(N, 2) - 1

Ncircle = [0]
for x, y in dart_positions:
    if np.sqrt (x**2 + y**2) < 1:
        Ncircle.append(Ncircle[-1] + 1)
    else:
        Ncircle.append (Ncircle[-1])

running_estimate = []
for n_total, n_circle in enumerate(Ncircle [1:]):
    running_estimate.append(4*n_circle / (n_total +1))
```

```python
#Vertorized
N = 10000
dart_positions = 2 *np.random.rand(N, 2) - 1

dist_from_origin = np.sqrt((dart_positions**2).sum(axis = 1))

is_in_circle = dist_from_origin< 1

num_in_circle = np.cumsum(is_in_circle)
num_thrown = np.arange(1, N+1)

running_estimate = 4 * num_in_circle / num_thrown

running_estimate[:1000]
```

3. Menghitung Akurasi Model 

Sebuah model Neural Network mendapatkan hasil label target berikut setelah dilakukan proses forward propagation.

| x1  | x2  | x3  | predicted class |
| --- | --- | --- | --------------- |
| 1   | 0   | 1   | 0               |
| 2   | 1   | 0   | 1               |
| -1  | 3   | 5   | 1               |
| 1   | 1   | 1   | 0               |
| 0   | 4   | 3   | 1               | 

sementara data aslinya adalah sebagai berikut:

| x1  | x2  | x3  | actual class |
| --- | --- | --- | ------------ |
| 0   | 4   | 3   | 1            |
| 1   | 1   | 1   | 0            |
| -1  | 3   | 5   | 0            |
| 2   | 1   | 0   | 1            |
| 1   | 0   | 1   | 0            |


Untuk mengevaluasi model tersebut, maka digunakan metrics bernama akurasi yang didefinisikan sebagai:

$$accuracy = \frac{TP + TN}{N}$$

dimana :
- TP adalah jumlah kelas 1 yang tepat diklasifikasikan sebagai 1 (saat predicted class= 1 dan actual class = 1)
- TN adalah jumlah kelas 0 yang tepat diklasifikasian sebagai 0 (saat peredicted class=0 dan actual class = 0)
- N adalah total data

buatlah sebuah program python untuk menghitung akurasi dari model tersebut dengan menggunakan cara:
- Unvectorized Solution
- Vectorized Solution
```python
import numpy as np
predicted = np.array([[1,0,1,0],
         [2,1,0,1],
         [-1,3,5,1],
         [1,1,1,0],
         [0,4,3,1]])
actual = np.array([[1,0,1,0],
        [2,1,0,1],
        [-1,3,5,0],
        [1,1,1,0],
        [0,4,3,1]])

rowcolumnpredicted = [predicted[0,3:],
                       predicted[1,3:],
                       predicted[2,3:],
                       predicted[3,3:],
                       predicted[4,3:]]

rowcolumnactual = [actual[0,3:],
                       actual[1,3:],
                       actual[2,3:],
                       actual[3,3:],
                       actual[4,3:]]

N = len(predicted)
i = 0
TP = 0
TN = 0
while i<N:
        if(rowcolumnpredicted[i] == 1 and rowcolumnactual[i] == 1):
            TP = TP+1
        elif(rowcolumnpredicted[i] == 0 and rowcolumnactual[i] == 0):
            TN = TN+1
        i = i+1
 #UNVECTORIZED
accuracy_unvectorized = (TP+TN)/N
print(accuracy_unvectorized)

#VECTORIZED
accuracy_vectorized = np.divide(np.add(TP,TN), N)
print(accuracy_vectorized)
```
