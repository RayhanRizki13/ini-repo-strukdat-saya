# <h1 align="center">DOUBLYLINKEDLIST(BAGIANPERTAMA)</h1>
<p align="center">Rayhan Rizki Putra</p>
 
## Dasar Teori

Doubly Linked List adalah struktur data di mana setiap elemen memiliki dua penunjuk: satu menunjuk ke elemen sebelumnya (prev) dan satu lagi menunjuk ke elemen setelahnya (next).

## Guided 

### 1. [Nama Topik]

```C++
#include <iostream>
#define Nil NULL
using namespace std;

typedef int infotype; // Definisikan tipe data infotype sebagai integer untuk menyimpan informasi elemen
typedef struct elmlist *address; // Definisikan tipe address sebagai pointer ke struct elmlist

struct elmlist {
    infotype info; // Deklarasikan field info untuk menyimpan data elemen
    address next;
    address prev;
};

struct List { 
    address first; 
    address last; 
}; 

void insertFirst(List &L, address P) { 
    P->next = L.first; // Set pointer next dari P ke elemen pertama saat ini
    P->prev = Nil; // Set pointer prev dari P ke Nil karena menjadi elemen pertama
    if (L.first != Nil) L.first->prev = P; // Jika list tidak kosong, set prev elemen pertama lama ke P
    else L.last = P; // Jika list kosong, set last juga ke P
    L.first = P; // Update first list menjadi P
} 

void insertLast(List &L, address P) { 
    P->prev = L.last; // Set pointer prev dari P ke elemen terakhir saat ini
    P->next = Nil; // Set pointer next dari P ke Nil karena menjadi elemen terakhir
    if (L.last != Nil) L.last->next = P; // Jika list tidak kosong, set next elemen terakhir lama ke P
    else L.first = P; // Jika list kosong, set first juga ke P
    L.last = P; // Update last list menjadi P
} 

void insertAfter(List &L, address P, address R) { // Definisikan fungsi insertAfter untuk menyisipkan elemen setelah R
    P->next = R->next; // Set pointer next dari P ke elemen setelah R
    P->prev = R; // Set pointer prev dari P ke R
    if (R->next != Nil) R->next->prev = P; // Jika ada elemen setelah R, set prev elemen tersebut ke P
    else L.last = P; // Jika R adalah terakhir, update last menjadi P
    R->next = P; // Set next dari R ke P
}

address alokasi(infotype x) { // Definisikan fungsi alokasi untuk membuat elemen baru
    address P = new elmlist; // Alokasikan memori baru untuk elemen
    P->info = x; // Set info elemen dengan nilai x
    P->next = Nil; // Set next elemen ke Nil
    P->prev = Nil; // Set prev elemen ke Nil
    return P; 
} 

void printInfo(List L) { // Definisikan fungsi printInfo untuk mencetak isi list
    address P = L.first; // Set P ke elemen pertama list
    while (P != Nil) { // Loop selama P tidak Nil
        cout << P->info << " "; // Cetak info dari P 
        P = P->next; // Pindah ke elemen berikutnya
    } 
    cout << endl; 
}

int main() { 
    List L; 
    L.first = Nil; 
    L.last = Nil;
    address P1 = alokasi(1); 
    insertFirst(L, P1); 
    address P2 = alokasi(2); 
    insertLast(L, P2); 
    address P3 = alokasi(3); 
    insertAfter(L, P3, P1); 
    printInfo(L); 
    return 0; 
}
```
Program ini mendemonstrasikan cara membuat dan memanipulasi struktur data double linked list dengan menyisipkan tiga angka (1, 2, dan 3) di posisi yang berbeda sehingga menghasilkan urutan 1, 3, 2.

## Unguided 

### 1. [Soal]
**Doublylist.h**
```C++
#ifndef DOUBLYLIST_H
#define DOUBLYLIST_H

#include <iostream>
#include <string>
using namespace std;

struct Kendaraan {
    string nopol;
    string warna;
    int tahun;
};

typedef struct Node* address;

struct Node {
    Kendaraan data;
    address next;
    address prev;
};

struct List {
    address first;
    address last;
};

void createList(List &L);
address newNode(Kendaraan x);
void printList(List L);
void insertLast(List &L, address P);
address find(List L, string nopol);

void deleteByNopol(List &L, string nopol);

#endif
```

**Doublylist.cpp**
```C++
#include "DoublyList.h"
using namespace std;

void createList(List &L) {
    L.first = NULL;
    L.last = NULL;
}

address newNode(Kendaraan x) {
    address P = new Node;
    P->data = x;
    P->next = NULL;
    P->prev = NULL;
    return P;
}

void printList(List L) {
    cout << "DATA LIST 1\n\n";
    address P = L.last;
    while (P != NULL) {
        cout << "no polisi : " << P->data.nopol << endl;
        cout << "warna     : " << P->data.warna << endl;
        cout << "tahun     : " << P->data.tahun << endl;
        if (P->prev != NULL) cout << endl;
        P = P->prev;
    }
}

void insertLast(List &L, address P) {
    if (L.first == NULL) {
        L.first = L.last = P;
    } else {
        L.last->next = P;
        P->prev = L.last;
        L.last = P;
    }
}

address find(List L, string nopol) {
    address P = L.first;
    while (P != NULL) {
        if (P->data.nopol == nopol) return P;
        P = P->next;
    }
    return NULL;
}

void deleteByNopol(List &L, string nopol) {
    address P = find(L, nopol);
    if (P == NULL) {
        cout << "Data tidak ditemukan\n";
        return;
    }

    if (P == L.first && P == L.last) {
        L.first = L.last = NULL;
    } 
    else if (P == L.first) {
        L.first = P->next;
        L.first->prev = NULL;
    } 
    else if (P == L.last) {
        L.last = P->prev;
        L.last->next = NULL;
    } 
    else {
        P->prev->next = P->next;
        P->next->prev = P->prev;
    }

    cout << "Data dengan nomor polisi " << nopol << " berhasil dihapus.\n\n";
    delete P;
}
```

**main.c**
```C++
#include <iostream>
#include "DoublyList.h"
using namespace std;

int main() {
    List L;
    createList(L);

    Kendaraan x;
    string nopol;

    cout << "masukkan nomor polisi: ";
    cin >> x.nopol;
    cout << "masukkan warna kendaraan: ";
    cin >> x.warna;
    cout << "masukkan tahun kendaraan: ";
    cin >> x.tahun;
    insertLast(L, newNode(x));
    cout << endl;

    cout << "masukkan nomor polisi: ";
    cin >> x.nopol;
    cout << "masukkan warna kendaraan: ";
    cin >> x.warna;
    cout << "masukkan tahun kendaraan: ";
    cin >> x.tahun;
    insertLast(L, newNode(x));
    cout << endl;

    cout << "masukkan nomor polisi: ";
    cin >> nopol;
    if (find(L, nopol) != NULL) {
        cout << "nomor polisi sudah terdaftar\n\n";
    }

    cout << "masukkan nomor polisi: ";
    cin >> x.nopol;
    cout << "masukkan warna kendaraan: ";
    cin >> x.warna;
    cout << "masukkan tahun kendaraan: ";
    cin >> x.tahun;
    insertLast(L, newNode(x));
    cout << endl;

    printList(L);
    cout << endl;

    cout << "Masukkan Nomor Polisi yang dicari  : ";
    cin >> nopol;

    address P = find(L, nopol);
    if (P != NULL) {
        cout << "\nNomor Polisi : " << P->data.nopol << endl;
        cout << "Warna        : " << P->data.warna << endl;
        cout << "Tahun        : " << P->data.tahun << endl;
    }
    cout << endl;

    cout << "Masukkan Nomor Polisi yang akan dihapus  : ";
    cin >> nopol;
    deleteByNopol(L, nopol);

    printList(L);

    return 0;
}
```
#### Output:
<img width="350" height="675" alt="image" src="https://github.com/user-attachments/assets/f4f6ac27-8e9e-4a03-9f03-f4fc8cb501db" />


    
Doubly linked list lebih powerful daripada singly linked list karena bisa navigasi dua arah, membuat operasi insert/delete lebih efisien, terutama untuk operasi yang membutuhkan akses elemen sebelumnya.

#### Full code Screenshot:


doublylist.h
<img width="464" height="610" alt="image" src="https://github.com/user-attachments/assets/215ebd99-9b4a-4c6f-9a45-462c06a17e5e" />



doublylist.cpp
<img width="580" height="954" alt="image" src="https://github.com/user-attachments/assets/8c93e339-a1ee-429d-915d-1746e7424f0d" />
<img width="610" height="227" alt="image" src="https://github.com/user-attachments/assets/12a43b3f-3bdb-493c-af4c-0f5ba714890c" />


main.cpp
<img width="581" height="953" alt="image" src="https://github.com/user-attachments/assets/a0c610f2-da89-497d-922b-1f6dc2888c75" />
<img width="298" height="112" alt="image" src="https://github.com/user-attachments/assets/ab3c2900-c7db-4c9f-8fcd-f5e79d0545e8" />



## Kesimpulan
Doubly Linked List memberikan solusi yang lebih powerful dibandingkan Singly Linked List untuk kasus-kasus yang membutuhkan akses dua arah, meskipun membutuhkan memori lebih besar untuk menyimpan pointer tambahan. Struktur data ini sangat efektif untuk aplikasi yang memerlukan operasi insert dan delete yang pada berbagai posisi dalam list.

## Referensi
Sihombing, J. (2019). Penerapan stack dan queue pada array dan linked list dalam java. INFOKOM (Informatika & Komputer), 7(2), 15-24.
