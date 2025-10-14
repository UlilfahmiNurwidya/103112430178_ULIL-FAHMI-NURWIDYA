# <h1 align="center">Laporan Praktikum Modul 4 <br> SINGLY LINKED LIST (BAGIAN PERTAMA)</h1>
<p align="center">ULIL FAHMI NURWIDYA - 103112430178</p>

## Dasar Teori

Singly Linked List merupakan struktur data dinamis yang tersusun dari sejumlah node yang saling terhubung secara searah. Setiap node menyimpan data serta pointer yang menunjuk ke node berikutnya, dan rantai ini berakhir pada nilai NULL. Struktur ini memungkinkan proses penambahan dan penghapusan elemen dilakukan dengan efisien tanpa perlu menggeser data lain. Operasi utamanya mencakup penyisipan, penghapusan, penelusuran, serta pembaruan data, yang seluruhnya menggunakan pointer untuk mengatur keterkaitan antar node.

## Guided

### LINKEDLIST.CPP
```c++
#include <iostream>
using namespace std;

// Struktur Node
struct Node {
    int data;
    Node* next;
};

// Pointer awal
Node* head = nullptr;

// Fungsi untuk membuat node baru
Node* createNode(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = nullptr;
    return newNode;
}

// ========== INSERT DEPAN ==========
void insertDepan(int data) {
    Node* newNode = createNode(data);
    newNode->next = head;
    head = newNode;
    cout << "Data " << data << " berhasil ditambahkan di depan.\n";
}

// ========== INSERT BELAKANG ==========
void insertBelakang(int data) {
    Node* newNode = createNode(data);
    if (head == nullptr) {
        head = newNode;
    } else {
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }
    cout << "Data " << data << " berhasil ditambahkan di belakang.\n";
}

// ========== INSERT SETELAH NODE ==========
void insertSetelah(int target, int dataBaru) {
    Node* temp = head;
    while (temp != nullptr && temp->data != target) {
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "Data " << target << " tidak ditemukan!\n";
    } else {
        Node* newNode = createNode(dataBaru);
        newNode->next = temp->next;
        temp->next = newNode;
        cout << "Data " << dataBaru << " berhasil disisipkan setelah " << target << ".\n";
    }
}

// ========== DELETE FUNCTION ==========
void hapusNode(int data) {
    if (head == nullptr) {
        cout << "List kosong!\n";
        return;
    }

    Node* temp = head;
    Node* prev = nullptr;

    // Jika data di node pertama
    if (temp != nullptr && temp->data == data) {
        head = temp->next;
        delete temp;
        cout << "Data " << data << " berhasil dihapus.\n";
        return;
    }

    // Cari node yang akan dihapus
    while (temp != nullptr && temp->data != data) {
        prev = temp;
        temp = temp->next;
    }

    // Jika data tidak ditemukan
    if (temp == nullptr) {
        cout << "Data " << data << " tidak ditemukan!\n";
        return;
    }

    prev->next = temp->next;
    delete temp;
    cout << "Data " << data << " berhasil dihapus.\n";
}

// ========== UPDATE FUNCTION ==========
void updateNode(int dataLama, int dataBaru) {
    Node* temp = head;
    while (temp != nullptr && temp->data != dataLama) {
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "Data " << dataLama << " tidak ditemukan!\n";
    } else {
        temp->data = dataBaru;
        cout << "Data " << dataLama << " berhasil diupdate menjadi " << dataBaru << ".\n";
    }
}

// ========== DISPLAY FUNCTION ==========
void tampilkanList() {
    if (head == nullptr) {
        cout << "List kosong!\n";
        return;
    }

    Node* temp = head;
    cout << "Isi Linked List: ";
    while (temp != nullptr) {
        cout << temp->data << " -> ";
        temp = temp->next;
    }
    cout << "NULL\n";
}

// ========== MAIN PROGRAM ==========
int main() {
    int pilihan, data, target, dataBaru;

    do {
        cout << "\n=== MENU SINGLE LINKED LIST ===\n";
        cout << "1. Insert Depan\n";
        cout << "2. Insert Belakang\n";
        cout << "3. Insert Setelah\n";
        cout << "4. Hapus Data\n";
        cout << "5. Update Data\n";
        cout << "6. Tampilkan List\n";
        cout << "0. Keluar\n";
        cout << "Pilih: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                cout << "Masukkan data: ";
                cin >> data;
                insertDepan(data);
                break;
            case 2:
                cout << "Masukkan data: ";
                cin >> data;
                insertBelakang(data);
                break;
            case 3:
                cout << "Masukkan data target: ";
                cin >> target;
                cout << "Masukkan data baru: ";
                cin >> dataBaru;
                insertSetelah(target, dataBaru);
                break;
            case 4:
                cout << "Masukkan data yang ingin dihapus: ";
                cin >> data;
                hapusNode(data);
                break;
            case 5:
                cout << "Masukkan data lama: ";
                cin >> data;
                cout << "Masukkan data baru: ";
                cin >> dataBaru;
                updateNode(data, dataBaru);
                break;
            case 6:
                tampilkanList();
                break;
            case 0:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
        }
    } while (pilihan != 0);

    return 0;
}

```
> Output
> ![Screenshot bagian x](../modul4/output/guid1.png)

## Unguided

### Soal 1

buatlah single linked list untuk Antrian yang menyimpan data pembeli( nama dan pesanan). program memiliki beberapa menu seperti tambah antrian,  layani antrian(hapus), dan tampilkan antrian. \*antrian pertama harus yang pertama dilayani


```c++
#include <iostream>
#include <string>
using namespace std;

// Struktur Node untuk menyimpan data pembeli
struct Node {
    string nama;
    string pesanan;
    Node* next;
};

// Pointer head dan tail untuk antrian
Node* head = nullptr;
Node* tail = nullptr;

// Fungsi untuk menambah antrian (di belakang)
void tambahAntrian(string nama, string pesanan) {
    Node* newNode = new Node();
    newNode->nama = nama;
    newNode->pesanan = pesanan;
    newNode->next = nullptr;

    if (head == nullptr) {
        head = tail = newNode;
    } else {
        tail->next = newNode;
        tail = newNode;
    }
    cout << "Pembeli " << nama << " dengan pesanan \"" << pesanan << "\" berhasil ditambahkan ke antrian.\n";
}
void layaniAntrian() {
    if (head == nullptr) {
        cout << "Antrian kosong! Tidak ada yang bisa dilayani.\n";
        return;
    }

    Node* temp = head;
    cout << "Melayani pembeli: " << head->nama << " (Pesanan: " << head->pesanan << ")\n";
    head = head->next;

    if (head == nullptr) {
        tail = nullptr; 
    }

    delete temp;
}

void tampilkanAntrian() {
    if (head == nullptr) {
        cout << "Antrian kosong.\n";
        return;
    }

    Node* temp = head;
    cout << "\n=== Daftar Antrian Pembeli ===\n";
    while (temp != nullptr) {
        cout << "- Nama: " << temp->nama << ", Pesanan: " << temp->pesanan << endl;
        temp = temp->next;
    }
}

int main() {
    int pilihan;
    string nama, pesanan;

    do {
        cout << "\n=== MENU ANTRIAN PEMBELI ===\n";
        cout << "1. Tambah Antrian\n";
        cout << "2. Layani Antrian\n";
        cout << "3. Tampilkan Antrian\n";
        cout << "0. Keluar\n";
        cout << "Pilih menu: ";
        cin >> pilihan;
        cin.ignore();

        switch (pilihan) {
            case 1:
                cout << "Masukkan nama pembeli: ";
                getline(cin, nama);
                cout << "Masukkan pesanan: ";
                getline(cin, pesanan);
                tambahAntrian(nama, pesanan);
                break;
            case 2:
                layaniAntrian();
                break;
            case 3:
                tampilkanAntrian();
                break;
            case 0:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
        }
    } while (pilihan != 0);

    return 0;
}
```

> Output
> ![Screenshot bagian x](../modul4/output/un1.png)

Program ini menggunakan Single Linked List untuk mengelola antrian pembeli. Setiap Node menyimpan nama, pesanan, dan pointer ke data berikutnya. Pointer `front` menunjuk ke antrian pertama, sedangkan `rear` ke antrian terakhir. Fungsi `tambahAntrian()` menambah data di belakang, `layaniAntrian()` menghapus data paling depan sesuai konsep FIFO, dan `tampilkanAntrian()` menampilkan seluruh antrian. Program ini berjalan interaktif melalui menu sederhana.

### Soal 2

buatlah program kode untuk membalik (reverse) singly linked list (1-2-3 menjadi 3-2-1) 

```c++
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
};

Node* head = nullptr;

void tambahNode(int nilai) {
    Node* nodeBaru = new Node{nilai, nullptr};

    if (!head) {
        head = nodeBaru;
    } else {
        Node* bantu = head;
        while (bantu->next) {
            bantu = bantu->next;
        }
        bantu->next = nodeBaru;
    }
}

void tampilList() {
    if (!head) {
        cout << "Linked List kosong.\n";
        return;
    }

    Node* bantu = head;
    while (bantu) {
        cout << bantu->data;
        if (bantu->next) cout << " -> ";
        bantu = bantu->next;
    }
    cout << endl;
}

void balikList() {
    Node *sebelum = nullptr, *sekarang = head, *sesudah = nullptr;

    while (sekarang) {
        sesudah = sekarang->next;
        sekarang->next = sebelum;
        sebelum = sekarang;
        sekarang = sesudah;
    }

    head = sebelum;
}

int main() {
    tambahNode(10);
    tambahNode(20);
    tambahNode(30);

    cout << "Linked List sebelum dibalik:\n";
    tampilList();

    balikList();

    cout << "\nLinked List setelah dibalik:\n";
    tampilList();

    return 0;
}

```

> Output
> ![Screenshot bagian x](../modul4/output/un2.png)

Program ini menggunakan singly linked list dengan pointer `head` sebagai penanda node pertama. Fungsi `tambahNode()` menambah data di akhir list, `tampilList()` menampilkan isi list, dan `balikList()` membalik urutan node menggunakan tiga pointer bantu (`sebelum`, `sekarang`, `sesudah`). Setelah dibalik, `head` menunjuk ke node terakhir sehingga urutan list terbalik.
