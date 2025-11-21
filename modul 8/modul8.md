# <h1 align="center">Laporan Praktikum Modul 8 <br>QUEUE</h1>
<p align="center">ULIL FAHMI NURWIDYA - 103112430178</p>

## Dasar Teori
Queue merupakan struktur data yang bekerja sama kaya antrean di loket tiket Kereta Api, di mana orang yang datang lebih awal akan dilayani lebih dulu, sedangkan yang datang belakangan akan dilayani kemudian—prinsip ini dikenal sebagai FIFO (*First In First Out*). Pada Queue, elemen yang pertama masuk akan menjadi elemen yang pertama keluar, sehingga sangat sesuai untuk kondisi yang membutuhkan urutan layanan yang teratur dan adil. Dalam bahasa C, Queue dapat dibuat menggunakan array maupun linked list; array menawarkan pengelolaan indeks yang sederhana, sedangkan linked list memberikan fleksibilitas lebih saat menambah atau menghapus elemen tanpa perlu menggeser elemen lainnya.

## Guided

### Guided 1
```c++
#include <iostream>
using namespace std;

#define MAX 5

struct Queue {
    int data[MAX];
    int head;
    int tail;
};

void createQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmpty(Queue Q) {
    return (Q.head == -1 && Q.tail == -1);
}

bool isFull(Queue Q) {
    return (Q.tail == MAX - 1);
}

void printQueue(Queue Q) {
    if (isEmpty(Q)) {
        cout << "Queue kosong!" << endl;
    } else {
        cout << "Queue : ";
        for (int i = Q.head; i <= Q.tail; i++) {
            cout << Q.data[i] << " ";
        }
        cout << endl;
    }
}

void enqueue(Queue &Q, int x) {
    if (isFull(Q)) {
        cout << "Queue penuh! Tidak bisa menambah data." << endl;
    } else {
        if (isEmpty(Q)) {
            Q.head = Q.tail = 0;
        } else {
            Q.tail++;
        }
        Q.data[Q.tail] = x;
        cout << "Enqueue: " << x << endl;
    }
}

void dequeue(Queue &Q) {
    if (isEmpty(Q)) {
        cout << "Queue kosong! Tidak ada data yang dihapus." << endl;
    } else {
        cout << "Dequeue: " << Q.data[Q.head] << endl;
        if (Q.head == Q.tail) {
            Q.head = Q.tail = -1;
        } else {
            for (int i = Q.head; i < Q.tail; i++) {
                Q.data[i] = Q.data[i + 1];
            }
            Q.tail--;
        }
    }
}

int main() {
    Queue Q;
    createQueue(Q);

    enqueue(Q, 5);
    enqueue(Q, 2);
    enqueue(Q, 7);
    printQueue(Q);

    dequeue(Q);
    printQueue(Q);

    enqueue(Q, 4);
    enqueue(Q, 9);
    printQueue(Q);

    dequeue(Q);
    dequeue(Q);
    printQueue(Q);

    return 0;
}
```

> Output
> 
> ![Screenshot bagian x]()

Program ini membuat struktur data Queue berbasis array dengan prinsip FIFO, di mana elemen yang pertama masuk menjadi yang pertama keluar. Queue dikelola dengan indeks head dan tail, serta dilengkapi fungsi untuk mengecek kondisi kosong/penuh, menambah elemen (enqueue), menghapus elemen (dequeue), dan menampilkan isi antrean. Pada fungsi main, program menguji operasi-operasi tersebut dengan menambah, menghapus, dan mencetak isi Queue.

## UNGUIDED

### Soal 1
Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme
queue Alternatif 1 (head diam, tail bergerak).

#### queue.h
```c++
#ifndef QUEUE_H
#define QUEUE_H

const int MAX = 5;
typedef int infotype;

struct Queue {
    infotype info[MAX];
    int head, tail;
};

void createQueue(Queue &Q);
bool isEmptyQueue(Queue Q);
bool isFullQueue(Queue Q);
void enqueue(Queue &Q, infotype x);
infotype dequeue(Queue &Q);
void printInfo(Queue Q);

#endif
```
#### queue.cpp
```c++
#include <iostream>
#include "queue.h"
using namespace std;

void createQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q) {
    return (Q.head == -1 && Q.tail == -1);
}

bool isFullQueue(Queue Q) {
    return (Q.tail == MAX - 1);
}

void enqueue(Queue &Q, infotype x) {
    if (isFullQueue(Q)) {
        cout << "Queue penuh!" << endl;
    } else {
        if (isEmptyQueue(Q)) {
            Q.head = 0;
            Q.tail = 0;
        } else {
            Q.tail++;
        }
        Q.info[Q.tail] = x;
    }
}

infotype dequeue(Queue &Q) {
    if (isEmptyQueue(Q)) {
        cout << "Queue kosong!" << endl;
        return -1;
    }

    infotype x = Q.info[Q.head];

    if (Q.head == Q.tail) {
        createQueue(Q); // kembali kosong
    } else {
        Q.head++;
    }

    return x;
}

void printInfo(Queue Q) {
    cout << Q.head << " - " << Q.tail << "\t|\t";

    if (isEmptyQueue(Q)) {
        cout << "empty queue" << endl;
    } else {
        for (int i = Q.head; i <= Q.tail; i++) {
            cout << Q.info[i] << " ";
        }
        cout << endl;
    }
}

```

#### main.cpp
```c++
#include <iostream>
#include "queue.h"
using namespace std;

int main() {
    Queue Q;
    createQueue(Q);

    cout << "   H - T   |   Queue Info" << endl;

    printInfo(Q);

    enqueue(Q, 8);  printInfo(Q);
    enqueue(Q, 3);  printInfo(Q);
    enqueue(Q, 9);  printInfo(Q);

    dequeue(Q);     printInfo(Q);

    enqueue(Q, 4);  printInfo(Q);

    dequeue(Q);     printInfo(Q);
    dequeue(Q);     printInfo(Q);

    return 0;
}

```
> Output soal 1
> 
> ![Screenshot bagian x]()

Program tersebut mengimplementasikan struktur data Queue berbasis array dengan fungsi dasar seperti membuat queue, mengecek kosong atau penuh, menambah elemen (enqueue), menghapus elemen (dequeue), dan menampilkan isi queue, lalu menguji semua operasi tersebut di dalam main.cpp sesuai konsep FIFO.

### Soal 2
Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme
queue Alternatif 2 (head bergerak, tail bergerak).

#### queue.cpp
```c++
#include <iostream>
#include "queue.h"
using namespace std;

void createQueue(Queue &Q){
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q){
    return (Q.head == -1 && Q.tail == -1);
}

bool isFullQueue(Queue Q){
    return (Q.tail == MAX - 1);
}

void enqueue(Queue &Q, infotype x){
    if (isFullQueue(Q)){
        cout << "Queue penuh!" << endl;
        return;
    }

    if (isEmptyQueue(Q)){
        Q.head = 0;
        Q.tail = 0;
        Q.info[Q.tail] = x;
    } else {
        Q.tail++;
        Q.info[Q.tail] = x;
    }
}

infotype dequeue(Queue &Q){
    if (isEmptyQueue(Q)){
        cout << "Queue kosong!" << endl;
        return -1;
    }

    infotype val = Q.info[Q.head];

    if (Q.head == Q.tail){
        createQueue(Q);
    } else {
        Q.head++;  
    }

    return val;
}

void printInfo(Queue Q){
    cout << Q.head << " - " << Q.tail << "\t|\t";

    if (isEmptyQueue(Q)){
        cout << "empty queue" << endl;
        return;
    }

    for (int i = Q.head; i <= Q.tail; i++){
        cout << Q.info[i] << " ";
    }
    cout << endl;
}
```

> Output soal 2
> 
> ![Screenshot bagian x]()

Program ini baik head maupun tail bergerak maju mengikuti operasi enqueue dan dequeue. Pendekatan ini lebih realistis karena elemen yang keluar benar-benar dilewati oleh head. Namun tetap tidak efisien karena array tidak berputar; ketika tail mencapai ujung array, queue dianggap penuh walaupun masih ada ruang kosong di depan akibat dequeuing.


### Soal 3
Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme
queue Alternatif 3 (head dan tail berputar).

#### queue.cpp
```c++
#include <iostream>
#include "queue.h"
using namespace std;

void createQueue(Queue &Q){
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q){
    return (Q.head == -1);
}

bool isFullQueue(Queue Q){
    return ((Q.tail + 1) % MAX == Q.head);
}

void enqueue(Queue &Q, infotype x){
    if (isFullQueue(Q)){
        cout << "Queue penuh!" << endl;
        return;
    }

    if (isEmptyQueue(Q)){
        Q.head = 0;
        Q.tail = 0;
        Q.info[Q.tail] = x;
    } else {
        Q.tail = (Q.tail + 1) % MAX;
        Q.info[Q.tail] = x;
    }
}

infotype dequeue(Queue &Q){
    if (isEmptyQueue(Q)){
        cout << "Queue kosong!" << endl;
        return -1;
    }

    infotype val = Q.info[Q.head];

    if (Q.head == Q.tail){  
        createQueue(Q);     
    } else {
        Q.head = (Q.head + 1) % MAX;
    }

    return val;
}

void printInfo(Queue Q){
    cout << Q.head << " - " << Q.tail << "\t|\t";

    if (isEmptyQueue(Q)){
        cout << "empty queue" << endl;
        return;
    }

    int i = Q.head;
    while (true){
        cout << Q.info[i] << " ";
        if (i == Q.tail) break;
        i = (i + 1) % MAX;
    }

    cout << endl;
}
```

> Output soal 3
> 
> ![Screenshot bagian x]()
> 
Program ini menggunakan konsep circular sehingga head dan tail berputar kembali ke indeks 0 menggunakan operasi modulo. Ruang kosong akibat dequeue dapat digunakan kembali, dan queue hanya penuh jika (tail + 1) % MAX == head. Implementasi ini paling efisien karena memaksimalkan penggunaan array dan sangat cocok untuk sistem antrian yang berjalan terus-menerus.

## Referensi
