
# <h1 align="center">Laporan Praktikum Modul 10 <br>TREE</h1>
<p align="center"> ULIL FAHMI NURWIDYA - 103112430178</p>

## Dasar Teori
Struktur data pohon adalah representasi hierarkis non-linear yang terdiri dari kumpulan simpul (node) yang terhubung, dimulai dari simpul akar (root) tanpa induk, sedangkan simpul lain mempunyai satu induk dan bisa mempunyai beberapa anak, kalau simpul tanpa anak di namakan daun. Jenis khususnya merupakan Binary Tree yang membatasi setiap simpul maksimal mempunyai dua anak, adalah anak kiri dan kanan, dengan pengembangan lebih lanjut menjadi Binary Search Tree (BST) yang mengatur penempatan nilai berdasarkan aturan: seluruh nilai di subpohon kiri lebih kecil dari induknya dan nilai di subpohon kanan lebih besar, sehingga mempercepat proses pencarian, penyisipan, dan penghapusan data. Penelusuran data dilakukan melalui tiga metode traversal—pre-order (akar, kiri, kanan), in-order (kiri, akar, kanan) yang pada BST menghasilkan urutan menaik, dan post-order (kiri, kanan, akar)—yang umumnya diimplementasikan menggunakan fungsi rekursif, di mana fungsi memanggil dirinya sendiri untuk menangani setiap subpohon secara berulang, memungkinkan pengelolaan data yang efisien dan terstruktur dalam pemrograman.


## Guided

### Guided 1
```c++
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *kiri, *kanan;
};

Node *buatNode(int nilai)
{
    Node *baru = new Node();
    baru->data = nilai;
    baru->kiri = baru->kanan = NULL;
    return baru;
}

Node *insert(Node *root, int nilai)
{
    if (root == NULL)
        return buatNode(nilai);
    
    if (nilai < root->data)
        root->kiri = insert(root->kiri, nilai);
    else if (nilai > root->data)
        root->kanan = insert(root->kanan, nilai);

    return root;
}

Node *search(Node *root, int nilai)
{
    if (root == NULL || root->data == nilai)
        return root;

    if (nilai < root->data)
        return search(root->kiri, nilai);

    return search(root->kanan, nilai);
}

Node *nilaiTerkecil(Node *node)
{
    Node *current = node;
    while (current && current->kiri != NULL)
        current = current->kiri;

        return current;
}

Node *hapus(Node *root, int nilai)
{
    if (root == NULL)
        return root;

    if (nilai < root->data)
        root->kiri = hapus(root->kiri, nilai);
    else if (nilai > root->data)
        root->kanan = hapus(root->kanan, nilai);
    else
    {
        if (root->kiri == NULL)
        {
            Node *temp = root->kanan;
            delete root;
            return temp;
        }
        else if (root->kanan == NULL){
            Node *temp = root->kiri;
            delete root;
            return temp;
        }
        Node *temp = nilaiTerkecil(root->kanan);
        root->data = temp->data;
        root->kanan = hapus(root->kanan, temp->data);
    }
    return root;
}

Node *update(Node *root, int Lama, int baru)
{
    if (search(root, Lama) != NULL)
    {
        root = hapus(root, Lama);
        root = insert(root, baru);
        cout << "Data " << Lama << " diupdate menjadi " << baru << endl;
    }
    else
    {
        cout << "Data " << Lama << " tidak ditemukan!" << endl;
    }
    return root;
}

void preOrder(Node *root)
{
    if (root != NULL)
    {
        cout << root->data << " ";
        preOrder(root->kiri);
        preOrder(root->kanan);
    }
}

void inOrder(Node *root)
{
    if (root != NULL)
    {
        inOrder(root->kiri);
        cout << root->data << " ";
        inOrder(root->kanan);
    }
}

void postOrder(Node *root)
{
    if (root != NULL)
    {
        postOrder(root->kiri);
        postOrder(root->kanan);
        cout << root->data << " ";
    }
}

int main()
{
    Node *root = NULL;

    cout << "=== 1. INSERT DATA ===" << endl;
    root = insert(root, 10);
    insert(root, 5);
    insert(root, 20);
    insert(root, 3);
    insert(root, 7);
    insert(root, 15);
    insert(root, 25);
    cout << "Data berhasil dimasukan.\n" << endl;

    cout << "=== 2. TAMPILKAN TREE (TRAVELSAL) ===" << endl;
    cout << "PreOrder : ";
    preOrder(root);
    cout << endl;
    cout << "InOrder : ";
    inOrder(root);
    cout << endl;
    cout << "PostOrder : ";
    postOrder(root);
    cout << "\n" << endl;

    cout << "=== 3. TEST SEARCH ===" << endl;
    int cari1 = 7, cari2 = 99;
    cout << "Cari " << cari1 << ": " << (search(root,cari1) ? "Ketemu" : "Tidak Aada") << endl;
    cout << "Cari " << cari2 << ": " << (search(root,cari2) ? "Ketemu" : "Tidak Aada") << endl;
    cout << endl;

    cout << "=== 4. TEST UPDATE ===" << endl;
    root = update(root, 5, 8);
    cout << "Hasil Order setelah update: ";
    cout << endl;
    cout << endl;

    cout << "PreOrder : ";
    preOrder(root);
    cout << endl;
    cout << "InOrder : ";
    inOrder(root);
    cout << endl;
    cout << "PostOrder : ";
    postOrder(root);
    cout << "\n" << endl;

    cout << "== 5. TEST DELETE ===" << endl;
    cout << "Menghapus angka 20..." << endl;
    root = hapus(root, 20);

    cout << "PreOrder : ";
    preOrder(root);
    cout << endl;
    cout << "InOrder : ";
    inOrder(root);
    cout << endl;
    cout << "PostOrder : ";
    postOrder(root);
    cout << "\n" << endl;

    return 0;
}
```

> Output
> 
> ![Screenshot bagian x](Output/Guided.png)

Program ini mengimplementasikan Binary Search Tree (BST) lengkap dalam C++ dengan fitur CRUD (Create, Read, Update, Delete). Program mampu menangani penghapusan node di berbagai kondisi (0, 1, atau 2 anak) serta menjaga integritas struktur pohon saat pembaruan data. Untuk verifikasi, tersedia tiga teknik penelusuran: Pre-Order, In-Order, dan Post-Order.

## UNGUIDED

#### bstree.h
```c++
#ifndef BSTREE_H
#define BSTREE_H

#include <iostream>
using namespace std;

/* === STRUKTUR NODE BST === */
typedef struct Node {
    int data;
    Node* kiri;
    Node* kanan;
} Node;

/* === DEKLARASI FUNGSI === */
Node* buatNode(int x);
void insertBST(Node* &akar, int x);

void inorder(Node* akar);
void preorder(Node* akar);
void postorder(Node* akar);

int jumlahNode(Node* akar);
int totalNilai(Node* akar);
int tinggiPohon(Node* akar);

#endif
```
#### bstree.cpp
```c++
#include "bstree.h"

Node* buatNode(int x) {
    Node* baru = new Node;
    baru->data = x;
    baru->kiri = NULL;
    baru->kanan = NULL;
    return baru;
}

void insertBST(Node* &akar, int x) {
    if (akar == NULL) {
        akar = buatNode(x);
    } else if (x < akar->data) {
        insertBST(akar->kiri, x);
    } else if (x > akar->data) {
        insertBST(akar->kanan, x);
    }
}

void inorder(Node* akar) {
    if (akar != NULL) {
        inorder(akar->kiri);
        cout << akar->data << " ";
        inorder(akar->kanan);
    }
}

void preorder(Node* akar) {
    if (akar != NULL) {
        cout << akar->data << " ";
        preorder(akar->kiri);
        preorder(akar->kanan);
    }
}

void postorder(Node* akar) {
    if (akar != NULL) {
        postorder(akar->kiri);
        postorder(akar->kanan);
        cout << akar->data << " ";
    }
}

int jumlahNode(Node* akar) {
    if (akar == NULL)
        return 0;
    return 1 + jumlahNode(akar->kiri) + jumlahNode(akar->kanan);
}

int totalNilai(Node* akar) {
    if (akar == NULL)
        return 0;
    return akar->data + totalNilai(akar->kiri) + totalNilai(akar->kanan);
}

int tinggiPohon(Node* akar) {
    if (akar == NULL)
        return 0;

    int kiri = tinggiPohon(akar->kiri);
    int kanan = tinggiPohon(akar->kanan);

    return (kiri > kanan) ? kiri + 1 : kanan + 1;
}
```
#### main.cpp
```c++
#include <iostream>
#include "bstree.h"
using namespace std;

int main() {
    Node* akar = NULL;

    /* Input data ke BST */
    insertBST(akar, 1);
    insertBST(akar, 2);
    insertBST(akar, 6);
    insertBST(akar, 4);
    insertBST(akar, 5);
    insertBST(akar, 3);
    insertBST(akar, 6); // duplikat
    insertBST(akar, 7);

    /* === SOAL 1 === */
    cout << "=== HASIL SOAL 1 ===" << endl;
    inorder(akar);
    cout << endl;

    /* === SOAL 2 === */
    cout << "\n=== HASIL SOAL 2 ===" << endl;
    inorder(akar);
    cout << endl;
    cout << "Tinggi Pohon   : " << tinggiPohon(akar) << endl;
    cout << "Jumlah Node    : " << jumlahNode(akar) << endl;
    cout << "Total Nilai    : " << totalNilai(akar) << endl;

    /* === SOAL 3 === */
    cout << "\n=== HASIL SOAL 3 ===" << endl;
    cout << "Preorder   : ";
    preorder(akar);
    cout << endl;

    cout << "Postorder  : ";
    postorder(akar);
    cout << endl;

    return 0;
}
```
> Output soal 1,2,3
> 
> ![Screenshot bagian x](Output/Output1.2.3png)

Program ini digunakan untuk membuat struktur data Binary Search Tree (BST) menggunakan C++ dengan konsep linked list, di mana setiap node memiliki data serta dua pointer ke anak kiri dan kanan. Data dimasukkan secara rekursif sehingga nilai yang lebih kecil ditempatkan di sisi kiri dan nilai yang lebih besar di sisi kanan, sesuai aturan BST. Program menyediakan tiga cara penelusuran pohon, yaitu In-Order, Pre-Order, dan Post-Order, untuk menampilkan data dengan urutan yang berbeda.
## Referensi

1. Wikipedia: https://en.wikipedia.org/wiki/Binary_search_tree
2. Javatpoint: https://www.javatpoint.com/binary-search-tree
3. HackerEarth: https://www.hackerearth.com/practice/data-structures/trees/binary-search-tree/tutorial/
4. Baeldung: https://www.baeldung.com/cs/binary-search-trees
5. StudyTonight: https://www.studytonight.com/data-structures/binary-search-tree
6. Cornell University: https://www.cs.cornell.edu/courses/cs2110/2014fa/L15-BinarySearchTree/bst.html
7. University of Washington: https://courses.cs.washington.edu/courses/cse373/20wi/lectures/lecture5.pdf
