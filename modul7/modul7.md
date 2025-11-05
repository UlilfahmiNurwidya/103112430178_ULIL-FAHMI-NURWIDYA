# <h1 align="center">Laporan Praktikum Modul 7 <br> Stack</h1>
<p align="center">Ulil Fahmi Nurwidya - 103112430178</p>

## Dasar Teori
Program stack merupakan salah satu bentuk struktur data linear yang bekerja berdasarkan prinsip LIFO (Last In First Out), artinya elemen yang terakhir dimasukkan akan menjadi elemen pertama yang diambil. Stack dapat direpresentasikan menggunakan **array** atau **pointer**, dengan satu penunjuk utama yang disebut **TOP** untuk menunjukkan posisi elemen teratas. Operasi dasar pada stack meliputi **push** (menambah elemen ke atas stack), **pop** (menghapus elemen dari atas stack), dan **printInfo** (menampilkan isi stack). Selain itu, dapat ditambahkan operasi tambahan seperti **balikStack** untuk membalik urutan data, **pushAscending** untuk menyisipkan elemen agar tetap terurut menaik, serta **getInputStream** untuk membaca input secara berurutan dari pengguna. Dengan implementasi berbasis array, stack memiliki batas ukuran tetap, namun mudah diakses karena indeks dapat digunakan langsung tanpa manajemen memori dinamis.

## Guide

```go
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *next;
};

bool isEmpety(Node *top)
{
    return top == nullptr;
}

void push(Node *&top, int data){
    Node *newNode = new Node;
    newNode -> data = data;
    newNode -> next = top;
    top = newNode;
}

int pop(Node *&top)
{
    if (isEmpety(top))
    {
        cout << "Stack Kosong, tidak bisa pop!" << endl;
        return 0;
    }

    int poppedData = top -> data;
    top = top -> next;

    Node *temp;
    return poppedData;
}

void show (Node *top)
{
    if (isEmpety(top))
    {
        cout << "Stack kosong," << endl;
        return;
    }
    cout << "TOP -> ";
    Node *temp = top;

    while (temp != nullptr)
    {
        cout << temp->data << "-> ";
        temp = temp->next;
    }

    cout << "NULL" << endl;

}

int main()
{
    Node *stack = nullptr;

    push(stack, 10);
    push(stack, 20);
    push(stack, 30);

    cout << "Menampilkan isi stack:" << endl;
    show (stack);

    cout << "pop;" << pop(stack) << endl;

    cout << "Menampilkan sisa Stack:" << endl;
    show(stack);

    return 0;
}
```


## Unguide

### Soal 1
<img width="715" height="646" alt="image" src="https://github.com/user-attachments/assets/761f442c-15d1-433e-a5d4-64bce8768eae" />


### stack.h
```go
#ifndef STACK_H
#define STACK_H

const int MAX = 20;
typedef int infotype;

struct Stack {
    infotype info[MAX];
    int top;
};

void createStack(Stack &S);
bool isEmpty(Stack S);
bool isFull(Stack S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);

void balikStack(Stack &S);

#endif

```

### stack.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

bool isEmpty(Stack S) {
    return S.top == -1;
}

bool isFull(Stack S) {
    return S.top == MAX - 1;
}

void push(Stack &S, infotype x) {
    if (!isFull(S)) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

infotype pop(Stack &S) {
    if (!isEmpty(S)) {
        infotype x = S.info[S.top];
        S.top--;
        return x;
    } else {
        cout << "Stack kosong!" << endl;
        return -1;
    }
}

void printInfo(Stack S) {
    if (isEmpty(S)) {
        cout << "Stack kosong!" << endl;
        return;
    }

    cout << "[TOP] ";
    for (int i = S.top; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    createStack(temp);

    while (!isEmpty(S)) {
        push(temp, pop(S));
    }
    S = temp;
}

```

### main.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    Stack S;
    createStack(S);

    push(S, 3);
    push(S, 4);
    push(S, 2);
    push(S, 9);
    pop(S);
    push(S, 8);
    pop(S);
    push(S, 2);
    pop(S);
    push(S, 3);
    push(S, 9);

    cout << "Isi stack awal:" << endl;
    printInfo(S);

    cout << "\nIsi stack setelah dibalik:" << endl;
    balikStack(S);
    printInfo(S);

    return 0;
}   
```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%207/jawaban%201.png)

Pada program di bikin sebuah ADT Stack yang mengimplementasikan menggunakan array dengan atribut info sebagai penyimpan data dan top sebagai penanda elemen teratas. Fungsi createStack() menginisialisasi stack dalam keadaan kosong dengan top = -1. Operasi push() digunakan untuk menambahkan elemen baru ke bagian atas stack selama tidak penuh, sedangkan pop() menghapus dan mengembalikan elemen teratas jika stack tidak kosong. Prosedur printInfo() berfungsi menampilkan isi stack dari elemen paling atas hingga paling bawah. Selain itu, prosedur balikStack() membalik urutan elemen dengan memanfaatkan stack sementara sehingga susunan data menjadi terbalik. Secara keseluruhan, stack pada program ini bekerja dengan prinsip LIFO (Last In First Out).

### Soal 2
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%207/soal%202.png)

### stack.h
```go
#ifndef STACK_H
#define STACK_H

const int MAX = 20;
typedef int infotype;

struct Stack {
    infotype info[MAX];
    int top;
};

void createStack(Stack &S);
bool isEmpty(Stack S);
bool isFull(Stack S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);

void balikStack(Stack &S);
void pushAscending(Stack &S, infotype x);

#endif
```

### stack.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

bool isEmpty(Stack S) {
    return S.top == -1;
}

bool isFull(Stack S) {
    return S.top == MAX - 1;
}

void push(Stack &S, infotype x) {
    if (!isFull(S)) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

infotype pop(Stack &S) {
    if (!isEmpty(S)) {
        infotype x = S.info[S.top];
        S.top--;
        return x;
    } else {
        cout << "Stack kosong!" << endl;
        return -1;
    }
}

void printInfo(Stack S) {
    if (isEmpty(S)) {
        cout << "Stack kosong!" << endl;
        return;
    }
    cout << "[TOP] ";
    for (int i = S.top; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    createStack(temp);

    while (!isEmpty(S)) {
        push(temp, pop(S));
    }
    S = temp;
}

void pushAscending(Stack &S, infotype x) {
    Stack temp;
    createStack(temp);

    while (!isEmpty(S) && S.info[S.top] > x) {
        push(temp, pop(S));
    }

    push(S, x);

    while (!isEmpty(temp)) {
        push(S, pop(temp));
    }
}

```

### main.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    Stack S;
    createStack(S);

    pushAscending(S, 3);
    pushAscending(S, 4);
    pushAscending(S, 8);
    pushAscending(S, 2);
    pushAscending(S, 3);
    pushAscending(S, 9);

    cout << "Stack setelah pushAscending:" << endl;
    printInfo(S);

    cout << "\nStack setelah dibalik:" << endl;
    balikStack(S);
    printInfo(S);

    return 0;
}
```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%207/jawaban%202.png)

Pada program kedua, ditambahkan prosedur pushAscending() untuk menjaga agar elemen stack tetap tersusun secara ascending dari bawah ke atas setiap kali data baru dimasukkan. Prosedur ini memanfaatkan stack sementara untuk menampung elemen yang lebih besar dari nilai yang akan disisipkan, kemudian data baru dipush ke stack utama dan elemen sementara dikembalikan lagi. Dengan cara tersebut, urutan ascending tetap terjaga meskipun proses penyisipan dilakukan berkali-kali. Saat ditampilkan dengan printInfo(), susunan terlihat seperti descending dari atas ke bawah, tetapi sebenarnya ascending dari bawah ke atas.

### Soal 3
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%207/soal%203.png)

### stack.h
```go
#ifndef STACK_H
#define STACK_H

const int MAX = 20;
typedef int infotype;

struct Stack {
    infotype info[MAX];
    int top;
};

void createStack(Stack &S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);
void getInputStream(Stack &S);

#endif


```

### stack.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < MAX - 1) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

infotype pop(Stack &S) {
    if (S.top >= 0) {
        infotype x = S.info[S.top];
        S.top--;
        return x;
    } else {
        cout << "Stack kosong!" << endl;
        return -1;
    }
}

void printInfo(Stack S) {
    if (S.top < 0) {
        cout << "Stack kosong!" << endl;
        return;
    }

    cout << "[TOP] ";
    for (int i = S.top; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    createStack(temp);

    while (S.top >= 0) {
        push(temp, pop(S));
    }
    S = temp;
}

void getInputStream(Stack &S) {
    cout << "Masukkan angka satu per satu (ENTER untuk selesai): ";

    cin.ignore(); // membersihkan buffer sebelum membaca char
    char c;
    cin.get(c);

    while (c != '\n') {
        if (c >= '0' && c <= '9') {
            push(S, c - '0');
        } else {
            cout << "\nKarakter '" << c << "' diabaikan (bukan angka)" << endl;
        }
        cin.get(c);
    }
}
```

### main.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    Stack S;
    createStack(S);

    getInputStream(S);

    cout << "\nIsi Stack:" << endl;
    printInfo(S);

    cout << "\nSetelah dibalik:" << endl;
    balikStack(S);
    printInfo(S);

    return 0;
}
```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%207/jawaban%203.png)

Pada program ketiga, ditambahkan prosedur getInputStream() yang membaca input pengguna karakter per karakter hingga menekan ENTER. Jika karakter berupa angka, maka dikonversi menjadi integer dan dimasukkan ke stack menggunakan push(). Dengan cara ini, pengguna dapat memasukkan deretan angka seperti string (misal 4729601), dan angka-angka tersebut tersimpan secara berurutan di stack. Prosedur ini membuat pengisian stack lebih fleksibel dan praktis.

## Referensi
1. https://www.w3schools.com/cpp/cpp_functions.asp
2. https://www.w3schools.com/cpp/cpp_arrays.asp
3. https://www.w3schools.com/cpp/cpp_user_input.asp
4. https://www.w3schools.com/cpp/cpp_while_loop.asp
5. https://www.w3schools.com/cpp/cpp_stacks.asp
