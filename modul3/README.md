# <h1 align="center">Laporan Praktikum Modul 3 <br> Abstract Data Type </h1>
<p align="center">ULIL FAHMI NURWIDYA - 103112430178</p>

## Dasar Teori

Tipe Data Abstrak (Abstract Data Type atau ADT) merupakan konsep dasar dalam ilmu komputer yang menggambarkan suatu tipe data dari sisi logika atau matematika, bukan dari cara implementasi teknisnya. ADT menjelaskan **apa** yang dapat dilakukan oleh suatu tipe data, bukan **bagaimana** cara melakukannya. Secara umum, ADT terdiri atas dua elemen utama: kumpulan data yang disimpan dan himpunan operasi (fungsi atau metode) yang dapat dijalankan terhadap data tersebut. Inti dari konsep ADT adalah **abstraksi**, yaitu pemisahan antara definisi perilaku (antarmuka publik) dan rincian implementasi (seperti struktur data dan algoritma yang digunakan). Contohnya, ADT *Stack* memiliki operasi *push* (menambah data) dan *pop* (mengambil data), tanpa memperhatikan apakah implementasinya menggunakan *array* atau *linked list*.


## Guided

### guided 1
```c++
#include <iostream>
using namespace std;

void kuadratkan(int &angka)
{
    angka = angka * angka;
}

int main()
{
    int nilai;

    cout << "Masukkan nilai awal yang ingin dikuadratkan: ";
    cin >> nilai;

    cout << "Nilai awal: " << nilai << endl;

    kuadratkan(nilai);

    cout << "Nilai setelah dikuadratkan: " << nilai << endl;

    return 0;
}
```
Kode ini mendemonstrasikan Call by Reference, di mana fungsi kuadratkan menerima parameter referensi (int &angka) yang terhubung langsung dengan variabel asli di fungsi main(). Dengan demikian, setiap perubahan yang dilakukan pada angka di dalam fungsi akan langsung memengaruhi nilai asli variabel tersebut.

> Output
> ![Screenshot bagian x](modul3/output/guide1.png)

### guided 2
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
Kode ini menunjukkan Call by Pointer, di mana fungsi 'tukar' menerima alamat memori dari variabel 'a' dan 'b' ('&a', '&b'). Dengan menggunakan operator dereference ('*'), fungsi langsung menukar nilai di alamat tersebut. Akibatnya, nilai asli 'a' dan 'b' di 'main()' berubah dari '10, 20' menjadi '20, 10', membuktikan bahwa fungsi dapat memodifikasi variabel di luar cakupannya.
> Output
> ![Screenshot bagian x](modul3/output/guide2.png)


## Unguided

### Soal 1

```c++
#include <iostream>
#include <iomanip>
using namespace std;

const int N = 3;

void inputMatriks(int M[N][N]) {
    cout << "Masukkan elemen-elemen Matriks " << N << "x" << N << ":\n";
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            cout << "Elemen [" << i + 1 << "][" << j + 1 << "]: ";
            cin >> M[i][j];
        }
    }
}

void transposeMatriks(int asal[N][N], int hasil[N][N]) {
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            hasil[j][i] = asal[i][j];
        }
    }
}

void tampilMatriks(int M[N][N], string judul) {
    cout << "\n" << judul << ":\n";
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            cout << setw(4) << M[i][j];
        }
        cout << endl;
    }
}

int main() {
    int A[N][N], AT[N][N];

    inputMatriks(A);
    transposeMatriks(A, AT);

    tampilMatriks(A, "Matriks Asli");
    tampilMatriks(AT, "Matriks Transposenya");

    return 0;
}

```
>
Kode program C++ ini berfungsi untuk melakukan **transpose** pada matriks 3×3 dengan membagi tugas ke tiga fungsi utama. Fungsi 'inputMatriks' meminta pengguna memasukkan elemen matriks, 'transposeMatriks' menukar baris dan kolom dengan logika 'hasil[j][i] = asal[i][j], dan 'tampilMatriks' menampilkan hasilnya secara rapi menggunakan 'setw(4)'. Fungsi 'main()' mengatur alur program dengan memanggil ketiga fungsi tersebut secara berurutan: input, proses, dan output.
> Output
> ![Screenshot bagian x](modul3/output/unguid1.png)
