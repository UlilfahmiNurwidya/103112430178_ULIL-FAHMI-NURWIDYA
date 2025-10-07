# <h1 align="center">Laporan Praktikum Modul 2 <br> PENGENALAN BAHASA C++ (BAGIAN KEDUA) </h1>
<p align="center">ULIL FAHMI NURWIDYA - 103112430178</p>

## Dasar Teori

Array merupakan kumpulan data dengan nama yang sama dan setiap elemen bertipe data sama. Untuk mengakses setiap komponen / elemen array berdasarkan indeks dari setiap elemen. C++ merupakan bahasa pemrograman yang dikembangkan oleh Bjarne Stroustrup pada awal tahun 1980-an pada Bell Laboratories. C++ merupakan pengembangan dari bahasa C menggunakan penambahan konsep pemrograman berorientasi objek (Object-Oriented Programming / OOP), sehingga dapat digunakan untuk membangun perangkat lunak dari skala kecil hingga besar dengan lebih efisien.C++ tetap menjadi salah satu bahasa pemrograman penting yang digunakan untuk pengembangan berbagai jenis perangkat lunak sampai saat ini.
## Guided

### soal 1 (call_by_pointer.cpp)
```c++
#include <iostream>
using namespace std;

void tukar(int *px, int *py); 

int main()
{
    int a = 10, b = 20;
    cout << "Sebelum ditukar: a = " << a << ", b = " << b << endl;
    tukar(&a, &b);
    cout << "Setelah ditukar: a = " << a << ", b = " << b << endl;
    return 0;
}

void tukar(int *px, int *py)
{
    int temp = *px;
    *px = *py;
    *py = temp;
}

```
> Output
> ![Screenshot bagian x](modul2/output/guided1.png)

Program ini digunakan untuk menukar nilai dua variabel (a dan b) menggunakan fungsi dengan parameter pointer (call by address).

### soal 2 (call_by_reference.cpp)
```c++
#include <iostream>
using namespace std;

void tukar(int &x, int &y);

int main()
{
    int a = 10, b = 20;
    cout << "Sebelum ditukar: a = " << a << ", b = " << b << endl;
    tukar(a, b);
    cout << "Setelah ditukar: a = " << a << ", b = " << b << endl;
    return 0;
}

void tukar(int &x, int &y)
{
    int temp = x;
    x = y;
    y = temp;
}

```
> Output
> ![Screenshot bagian x](modul2/output/guided2.png)

Program tersebut menukar value dua variabel (a dan b) menggunakan fungsi dengan parameter referensi (&). Karena parameter memakai tanda &, maka variabel yang dikirim ke fungsi tak disalin, namun diakses langsung value aslinya.


## Unguided

### Soal 1

```c++
#include <iostream>
using namespace std;

int main()
{
    int matriks[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    int transpose[3][3];

    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            transpose[j][i] = matriks[i][j];
        }
    }
    cout << "Matriks Awal:" << endl;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << matriks[i][j] << " ";
        }
        cout << endl;
    }
    cout << "\nMatriks Hasil Transpose:" << endl;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << transpose[i][j] << " ";
        }
        cout << endl;
    }

    return 0;
}

```
> Output
> ![Screenshot bagian x](modul2/output/unguided1.png)

program tersebut bisa disimpulkan operasi transpose matriks yang dapat dilakukan dengan cara menukar posisi baris menjadi kolom dan kolom menjadi baris menggunakan konsep array dua dimensi dan perulangan bersarang.

### Soal 2

```c++
#include <iostream>
using namespace std;

void kuadratkan(int &x) {
    x = x * x; 
}

int main() {
    int angka = 5; 

    cout << "Nilai awal: " << angka << endl;

    kuadratkan(angka);

    cout << "Nilai setelah dikuadratkan: " << angka << endl;

    return 0;
}

```

> Output
> ![Screenshot bagian x](modul2/output/unguided2.png)

Dari program ini dapat disimpulkan bahwa penggunaan parameter referensi (&) dalam fungsi C++ memungkinkan sebuah fungsi untuk mengubah nilai asli variabel yang dikirim dari luar fungsi.

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure (diakses blablabla)
