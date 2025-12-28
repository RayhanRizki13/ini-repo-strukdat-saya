# <h1 align="center">MULTI LINKED LIST</h1>
<p align="center">Rayhan Rizki Putra</p>

## Dasar Teori

Multi List itu kumpulan dari beberapa list yang saling terhubung. Setiap elemen di dalamnya bisa punya list sendiri. Biasanya ada list utama (induk) dan list tambahan yang jadi anaknya.

## Guided 

### 1. [Nama Topik]

```C++
#include <iostream>
using namespace std;

int main() {
    cout << "ini adalah file code guided praktikan" << endl;
    return 0;
}
```
Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function cout untuk mengeksekusi nya.

## Unguided 

### 1. [Soal]

**multilist.h**
```C++
#ifndef SLL_H
#define SLL_H
#include <iostream>
using namespace std;

struct Mahasiswa {
    string nama;
    string nim;
    char kelamin; 
    float ipk;
};

struct Node {
    Mahasiswa info;
    Node *next;
};

struct List {
    Node *first;
};

void createList(List &L);
Node* alokasi(Mahasiswa x);
void insertFirst(List &L, Node *p);
void insertLast(List &L, Node *p);
void insertAfter(Node *prec, Node *p);
void printInfo(List L);

#endif
}
```
**multilist.cpp**
```C++
#include "multilist.h"

void createList(List &L) {
    L.first = NULL;
}

Node* alokasi(Mahasiswa x) {
    Node *p = new Node;
    p->info = x;
    p->next = NULL;
    return p;
}

void insertFirst(List &L, Node *p) {
    p->next = L.first;
    L.first = p;
}

void insertLast(List &L, Node *p) {
    if (L.first == NULL) {
        L.first = p;
    } else {
        Node *q = L.first;
        while (q->next != NULL) q = q->next;
        q->next = p;
    }
}

void insertAfter(Node *prec, Node *p) {
    p->next = prec->next;
    prec->next = p;
}

void printInfo(List L) {
    Node *p = L.first;

    while (p != NULL) {
        cout << "Nama : " << p->info.nama << endl;
        cout << "NIM  : " << p->info.nim << endl;
        cout << "L/P  : " << p->info.kelamin << endl;
        cout << "IPK  : " << p->info.ipk << endl << endl;
        p = p->next;
    }
}
```
**main.cpp**
```C++
#include "multilist.h"

int main() {
    List L;
    createList(L);

    cout << "coba insert first, last, dan after" << endl;

    Mahasiswa m1 = {"Ali", "01", 'L', 3.3};
    insertFirst(L, alokasi(m1));

    Mahasiswa m2 = {"Bobi", "02", 'L', 3.71};
    insertLast(L, alokasi(m2));

    Mahasiswa m3 = {"Cindi", "03", 'P', 3.5};
    insertLast(L, alokasi(m3));

    Mahasiswa m4 = {"Danu", "04", 'L', 4.0};
    Node *p = L.first;
    while (p->info.nama != "Cindi") p = p->next;
    insertAfter(p, alokasi(m4));

    insertLast(L, alokasi({"Eli", "05", 'P', 3.4}));
    insertLast(L, alokasi({"Fahmi", "06", 'L', 3.45}));
    insertLast(L, alokasi({"Gita", "07", 'P', 3.75}));
    insertLast(L, alokasi({"Hilmi", "08", 'L', 3.3}));

    printInfo(L);

    return 0;
}
```
#### Output:
<img width="467" height="698" alt="image" src="https://github.com/user-attachments/assets/17b2e250-321b-4e7d-9c8c-8ed4d017acd7" />


Kode ini menunjukkan cara menambahkan data mahasiswa ke dalam single linked list lalu menampilkannya dari awal sampai akhir.

#### Full code Screenshot:


multilist.h
<img width="349" height="495" alt="image" src="https://github.com/user-attachments/assets/0193ebe4-66a8-4f49-8753-b8b3efb4f618" />

singlylist.cpp
<img width="516" height="734" alt="image" src="https://github.com/user-attachments/assets/53028b69-3434-4d61-8e0e-1a420ffd5530" />

main.cpp
<img width="514" height="553" alt="image" src="https://github.com/user-attachments/assets/6836f800-19a9-4b76-b47a-e9d838304b38" />


## Kesimpulan
Praktikum ini memahami cara kerja Multi Linked List dan cara memasukkan data ke dalam sebuah linked list, khususnya bagaimana menambah data di awal, akhir, dan setelah elemen tertentu serta menampilkannya kembali secara berurutan.

## Referensi
Syahputra, F., Sabrina, E., Ilham, M., Saputra, R. A., & Sitepu, Z. B. (2025). Penerapan Ai Di Platform Linkedin Learning Untuk Meningkatkan Keterampilan Profesional Mahasiswa: Penelitian. Jurnal Pengabdian Masyarakat dan Riset Pendidikan, 3(3), 327-332.
