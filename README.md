# <h1 align="center">Laporan Praktikum Modul 1 <br> PENGENALAN C++ </h1>
<p align="center">ULIL FAHMI NURWIDYA - 103112430178</p>

## Dasar Teori

C++ merupakan bahasa pemrograman yang dikembangkan oleh Bjarne Stroustrup pada awal tahun 1980-an pada Bell Laboratories. C++ merupakan pengembangan dari bahasa C menggunakan penambahan konsep pemrograman berorientasi objek (Object-Oriented Programming / OOP), sehingga dapat digunakan untuk membangun perangkat lunak dari skala kecil hingga besar dengan lebih efisien.C++ tetap menjadi salah satu bahasa pemrograman penting yang digunakan untuk pengembangan berbagai jenis perangkat lunak sampai saat ini.
## Guided

### soal 1

aku mengerjakan perulangan

## Unguided

### Soal 1

copy paste soal nomor 1 disini

```c++
#include <iostream>
#include <iomanip>
using namespace std;

float tambah(float a, float b) { return a + b; }
float kurang(float a, float b) { return a - b; }
float kali(float a, float b) { return a * b; }
float bagi(float a, float b) { return (b != 0) ? a / b : 0; }

int main() {
    float bil1, bil2;

    cout << "Masukkan bilangan pertama (float): ";
    cin >> bil1;

    cout << "Masukkan bilangan kedua (float): ";
    cin >> bil2;

    cout << "\n--- Hasil Operasi Aritmatika ---" << endl;
    cout << fixed << setprecision(2);

    cout << "Penjumlahan : " << tambah(bil1, bil2) << endl;
    cout << "Pengurangan : " << kurang(bil1, bil2) << endl;
    cout << "Perkalian   : " << kali(bil1, bil2) << endl;

    if (bil2 != 0) {
        cout << "Pembagian   : " << bagi(bil1, bil2) << endl;
    } else {
        cout << "Pembagian   : Tidak dapat dilakukan (pembagian dengan nol)" << endl;
    }

    return 0;
}

```
>

Penjelasan ttg kode kalian disini

### Soal 2

soal nomor 2A

```go
package main

func main() {
	fmt.Println("kode untuk soal nomor 2A")
}
```

> Output
> ![Screenshot bagian x](output/screenshot_soal2A.png)

penjelasan kode

Kalau adalanjutan di lanjut disini aja

soal nomor 2B

```go
package main

func main() {
	fmt.Println("kode untuk soal nomor 2B")
}
```

> Output
> ![Screenshot bagian x](output/screenshot_soal2B.png)

penjelasan bedanya sesuai soal

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure (diakses blablabla)
