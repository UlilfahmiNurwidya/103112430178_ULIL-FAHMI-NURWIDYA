# <h1 align="center">Laporan Praktikum Modul 13 <br>MULTI LINKED LIST</h1>
<p align="center">ULIL FAHMI NURWIDYA - 103112430178</p>

## Dasar Teori
Multi Linked List adalah struktur data di mana beberapa list saling terhubung, biasanya dalam hubungan induk (parent) dan anak (child). Setiap elemen induk dapat memiliki sub-list yang berisi elemen anak, sehingga sangat efektif untuk merepresentasikan data hierarkis atau relasi satu-ke-banyak.
## Guided

### Guided 1
```c++
#include <iostream>
#include <string>
using namespace std;

struct ChildNode
{
    string info;
    ChildNode *next;
};

struct ParentNode
{
    string info;
    ChildNode *childHead;
    ParentNode *next;
};

ParentNode *createParent(string info)
{
    ParentNode *newNode = new ParentNode;
    newNode->info = info;
    newNode->childHead = NULL;
    newNode->next = NULL;
    return newNode;
}

ChildNode *createChild(string info)
{
    ChildNode *newNode = new ChildNode;
    newNode->info = info;
    newNode->next = NULL;
    return newNode;
}

void insertParent(ParentNode *&head, string info)
{
    ParentNode *newNode = createParent(info);
    if (head == NULL)
    {
        head = newNode;
    }
    else
    {
        ParentNode *temp = head;
        while (temp->next != NULL)
        {
            temp = temp->next;
        }
        temp->next = newNode;
    }
}

void insertChild(ParentNode *head, string parentInfo, string childInfo)
{
    ParentNode *p = head;
    while (p != NULL && p->info != parentInfo)
    {
        p = p->next;
    }
    
    if (p != NULL)
    {
        ChildNode *newChild = createChild(childInfo);
        
        if (p->childHead == NULL)
        {
            p->childHead = newChild;
        }
        else
        {
            ChildNode *c = p->childHead;
            while (c->next != NULL)
            {
                c = c->next;
            }
            c->next = newChild;
        }
    }
}

void printAll(ParentNode *head)
{
    ParentNode *p = head;
    while (p != NULL)
    {
        cout << p->info;
        ChildNode *c = p->childHead;
        if (c != NULL)
        {
            while (c != NULL)
            {
                cout << " -> " << c->info;
                c = c->next;
            }
        }
     cout << endl;
        p = p->next;
    }
}

int main()
{
    ParentNode *list = NULL;
    
    insertParent(list, "Parent Node 1");
    insertParent(list, "Parent Node 2");
    
    printAll(list);
    cout << "\n";
    
    insertChild(list, "Parent Node 1", "Child Node A");
    insertChild(list, "Parent Node 1", "Child Node B");
    insertChild(list, "Parent Node 2", "Child Node C");
    
    printAll(list);
    
    return 0;
}
```

> Output
> ![Screenshot bagian x](Output/Guided1.png)

Program ini mendemonstrasikan Multi Linked List dengan struktur one-to-many. Dua node induk berfungsi sebagai entitas utama yang masing-masing memiliki daftar node anak terpisah, merepresentasikan hubungan hierarkis (seperti departemen dan pegawainya).

## UNGUIDED 
### unguided1
#### multilist.h
```c++
#ifndef MULTILIST_H_INCLUDED
#define MULTILIST_H_INCLUDED

#include <iostream>
using namespace std;

#define Nil NULL
typedef bool boolean;

/* === TYPE DATA === */
typedef int infotypeinduk;
typedef int infotypeanak;

/* === DEKLARASI ADDRESS === */
typedef struct elemen_list_induk *address;
typedef struct elemen_list_anak *address_anak;

/* === STRUKTUR ELEMEN ANAK === */
struct elemen_list_anak {
    infotypeanak info;
    address_anak next;
    address_anak prev;
};

/* === STRUKTUR LIST ANAK === */
struct listanak {
    address_anak first;
    address_anak last;
};

/* === STRUKTUR ELEMEN INDUK === */
struct elemen_list_induk {
    infotypeinduk info;
    listanak lanak;
    address next;
    address prev;
};

/* === STRUKTUR LIST INDUK === */
struct listinduk {
    address first;
    address last;
};

/* ===== PROTOTYPE FUNGSI ===== */

/* pengecekan list kosong */
boolean ListEmpty(listinduk L);
boolean ListEmptyAnak(listanak L);

/* pembuatan list */
void CreateList(listinduk &L);
void CreateListAnak(listanak &L);

/* manajemen memori */
address alokasi(infotypeinduk X);
address_anak alokasiAnak(infotypeanak X);
void dealokasi(address P);
void dealokasiAnak(address_anak P);

/* pencarian */
address findElm(listinduk L, infotypeinduk X);
address_anak findElm(listanak L, infotypeanak X);

/* insert */
void insertLast(listinduk &L, address P);
void insertLastAnak(listanak &L, address_anak P);

/* delete */
void delLast(listinduk &L, address &P);
void delLastAnak(listanak &L, address_anak &P);

/* print */
void printInfo(listinduk L);

#endif
```
#### multilist.cpp
```c++
#include <iostream>
#include "multilist.h"
using namespace std;

/* ===== PENGECEKAN LIST KOSONG ===== */
boolean ListEmpty(listinduk L){
    return (L.first == Nil);
}

boolean ListEmptyAnak(listanak L){
    return (L.first == Nil);
}

/* ===== CREATE LIST ===== */
void CreateList(listinduk &L){
    L.first = Nil;
    L.last = Nil;
}

void CreateListAnak(listanak &L){
    L.first = Nil;
    L.last = Nil;
}

/* ===== ALOKASI & DEALOKASI ===== */
address alokasi(infotypeinduk X){
    address P = new elemen_list_induk;
    P->info = X;
    CreateListAnak(P->lanak);
    P->next = Nil;
    P->prev = Nil;
    return P;
}

address_anak alokasiAnak(infotypeanak X){
    address_anak P = new elemen_list_anak;
    P->info = X;
    P->next = Nil;
    P->prev = Nil;
    return P;
}

void dealokasi(address P){
    delete P;
}

void dealokasiAnak(address_anak P){
    delete P;
}

/* ===== FIND ===== */
address findElm(listinduk L, infotypeinduk X){
    address P = L.first;
    while(P != Nil){
        if(P->info == X){
            return P;
        }
        P = P->next;
    }
    return Nil;
}

address_anak findElm(listanak L, infotypeanak X){
    address_anak P = L.first;
    while(P != Nil){
        if(P->info == X){
            return P;
        }
        P = P->next;
    }
    return Nil;
}

/* ===== INSERT INDUK ===== */
void insertLast(listinduk &L, address P){
    if(ListEmpty(L)){
        L.first = P;
        L.last = P;
    }else{
        L.last->next = P;
        P->prev = L.last;
        L.last = P;
    }
}

/* ===== INSERT ANAK ===== */
void insertLastAnak(listanak &L, address_anak P){
    if(ListEmptyAnak(L)){
        L.first = P;
        L.last = P;
    }else{
        L.last->next = P;
        P->prev = L.last;
        L.last = P;
    }
}

/* ===== DELETE ANAK ===== */
void delLastAnak(listanak &L, address_anak &P){
    if(!ListEmptyAnak(L)){
        P = L.last;
        L.last = P->prev;
        if(L.last != Nil){
            L.last->next = Nil;
        }else{
            L.first = Nil;
        }
        dealokasiAnak(P);
    }
}

/* ===== DELETE INDUK ===== */
void delLast(listinduk &L, address &P){
    if(!ListEmpty(L)){
        P = L.last;
        address_anak Q;
        while(!ListEmptyAnak(P->lanak)){
            delLastAnak(P->lanak, Q);
        }
        L.last = P->prev;
        if(L.last != Nil){
            L.last->next = Nil;
        }else{
            L.first = Nil;
        }
        dealokasi(P);
    }
}

/* ===== PRINT ===== */
void printInfo(listinduk L){
    address P = L.first;
    while(P != Nil){
        cout << "Induk : " << P->info << endl;
        address_anak Q = P->lanak.first;
        while(Q != Nil){
            cout << "  Anak : " << Q->info << endl;
            Q = Q->next;
        }
        P = P->next;
    }
}
```
#### main.cpp
```c++
#include <iostream>
#include "multilist.h"
using namespace std;

int main(){
    listinduk L;
    address P;
    address_anak Q;

    CreateList(L);

    /* Insert Induk */
    P = alokasi(1);
    insertLast(L, P);

    P = alokasi(2);
    insertLast(L, P);

    P = alokasi(3);
    insertLast(L, P);

    /* Insert Anak */
    P = findElm(L, 1);
    Q = alokasiAnak(10);
    insertLastAnak(P->lanak, Q);

    Q = alokasiAnak(20);
    insertLastAnak(P->lanak, Q);

    P = findElm(L, 2);
    Q = alokasiAnak(30);
    insertLastAnak(P->lanak, Q);

    /* Tampilkan */
    cout << "=== DATA MULTI LINKED LIST ===" << endl;
    printInfo(L);

    return 0;
}
```
> Output
> ![Screenshot bagian x](Output/soal2.png)

Program tersebut digunakan untuk mengimplementasikan struktur data Multi Linked List, yang terdiri dari list induk dan list anak di mana setiap elemen induk dapat memiliki beberapa elemen anak. Program ini menyediakan fungsi untuk membuat list, menambah dan menghapus data induk maupun anak, serta menampilkan seluruh isi data beserta hubungannya.

### unguided2

#### circularlist.h
```c++
#ifndef CIRCULARLIST_H_INCLUDED
#define CIRCULARLIST_H_INCLUDED

#include <iostream>
using namespace std;

#define Nil NULL

/* === TYPE DATA === */
typedef struct {
    string nama;
    string nim;
    char jenis_kelamin;
    float ipk;
} infotype;

typedef struct ElmList *address;

/* === ELEMEN LIST === */
struct ElmList {
    infotype info;
    address next;
};

/* === LIST === */
struct List {
    address First;
};

/* === PROTOTYPE FUNGSI === */
void createList(List &L);
address alokasi(infotype x);
void dealokasi(address P);

void insertFirst(List &L, address P);
void insertAfter(List &L, address Prec, address P);
void insertLast(List &L, address P);

void deleteFirst(List &L, address &P);
void deleteAfter(List &L, address Prec, address &P);
void deleteLast(List &L, address &P);

address findElm(List L, infotype x);
void printInfo(List L);

#endif
```
#### circularlist.cpp
```c++
#include "circularlist.h"

/* === CREATE LIST === */
void createList(List &L){
    L.First = Nil;
}

/* === ALOKASI === */
address alokasi(infotype x){
    address P = new ElmList;
    P->info = x;
    P->next = Nil;
    return P;
}

/* === DEALOKASI === */
void dealokasi(address P){
    delete P;
}

/* === INSERT FIRST === */
void insertFirst(List &L, address P){
    if(L.First == Nil){
        L.First = P;
        P->next = P;
    }else{
        address Q = L.First;
        while(Q->next != L.First){
            Q = Q->next;
        }
        P->next = L.First;
        Q->next = P;
        L.First = P;
    }
}

/* === INSERT AFTER === */
void insertAfter(List &L, address Prec, address P){
    P->next = Prec->next;
    Prec->next = P;
}

/* === INSERT LAST === */
void insertLast(List &L, address P){
    if(L.First == Nil){
        insertFirst(L, P);
    }else{
        address Q = L.First;
        while(Q->next != L.First){
            Q = Q->next;
        }
        Q->next = P;
        P->next = L.First;
    }
}

/* === DELETE FIRST === */
void deleteFirst(List &L, address &P){
    if(L.First != Nil){
        address Q = L.First;
        while(Q->next != L.First){
            Q = Q->next;
        }
        P = L.First;
        if(P->next == P){
            L.First = Nil;
        }else{
            L.First = P->next;
            Q->next = L.First;
        }
        P->next = Nil;
    }
}

/* === DELETE AFTER === */
void deleteAfter(List &L, address Prec, address &P){
    P = Prec->next;
    Prec->next = P->next;
    P->next = Nil;
}

/* === DELETE LAST === */
void deleteLast(List &L, address &P){
    if(L.First != Nil){
        address Q = L.First;
        address Prec = Nil;
        while(Q->next != L.First){
            Prec = Q;
            Q = Q->next;
        }
        P = Q;
        if(Prec == Nil){
            L.First = Nil;
        }else{
            Prec->next = L.First;
        }
        P->next = Nil;
    }
}

/* === FIND ELM (BERDASARKAN NIM) === */
address findElm(List L, infotype x){
    if(L.First != Nil){
        address P = L.First;
        do{
            if(P->info.nim == x.nim){
                return P;
            }
            P = P->next;
        }while(P != L.First);
    }
    return Nil;
}

/* === PRINT INFO === */
void printInfo(List L){
    if(L.First != Nil){
        address P = L.First;
        do{
            cout << P->info.nama << " | "
                 << P->info.nim << " | "
                 << P->info.jenis_kelamin << " | "
                 << P->info.ipk << endl;
            P = P->next;
        }while(P != L.First);
    }
}
```
#### main.cpp
```c++
#include <iostream>
#include "circularlist.h"
using namespace std;

/* FUNGSI CREATE SESUAI MODUL */
address createData(string nama, string nim, char jk, float ipk){
    infotype x;
    address P;
    x.nama = nama;
    x.nim = nim;
    x.jenis_kelamin = jk;
    x.ipk = ipk;
    P = alokasi(x);
    return P;
}

int main(){
    List L;
    address P1, P2;
    infotype x;

    createList(L);

    cout << "coba insert first, last, dan after" << endl;

    P1 = createData("Danu","04",'l',4.0);
    insertFirst(L,P1);

    P1 = createData("Fahmi","06",'l',3.45);
    insertLast(L,P1);

    P1 = createData("Bobi","02",'l',3.71);
    insertFirst(L,P1);

    P1 = createData("Ali","01",'l',3.3);
    insertFirst(L,P1);

    P1 = createData("Gita","07",'p',3.75);
    insertLast(L,P1);

    x.nim = "07";
    P1 = findElm(L,x);
    P2 = createData("Cindi","03",'p',3.5);
    insertAfter(L,P1,P2);

    x.nim = "02";
    P1 = findElm(L,x);
    P2 = createData("Hilmi","08",'p',3.3);
    insertAfter(L,P1,P2);

    x.nim = "04";
    P1 = findElm(L,x);
    P2 = createData("Eli","05",'p',3.4);
    insertAfter(L,P1,P2);

    printInfo(L);
    return 0;
}
```

> Output
> ![Screenshot bagian x](Output/soal3.png)

Program circular linked list tersebut mengimplementasikan Circular Linked List untuk menyimpan data mahasiswa yang terdiri dari nama, NIM, jenis kelamin, dan IPK. Pada struktur ini, setiap node memiliki satu pointer yang menunjuk ke node berikutnya, dan node terakhir akan menunjuk kembali ke node pertama sehingga membentuk list melingkar. Program menyediakan operasi dasar seperti membuat list, menambah data di awal, di akhir, dan setelah node tertentu, menghapus data, mencari data mahasiswa berdasarkan NIM, serta menampilkan seluruh isi list.

## Referensi

1. https://www.geeksforgeeks.org/multilist-in-data-structure/
2. https://www.tutorialspoint.com/data_structures_algorithms/linked_list_algorithms.htm
3. https://www.programiz.com/dsa/linked-list
4. https://www.geeksforgeeks.org/circular-linked-list/
5. https://www.programiz.com/dsa/circular-linked-list
6. https://www.javatpoint.com/multi-linked-list-in-data-structure
7. https://www.javatpoint.com/circular-linked-list
8. https://www.geeksforgeeks.org/doubly-linked-list/
