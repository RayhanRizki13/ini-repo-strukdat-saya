# <h1 align="center">Laporan Praktikum Modul SINGLY LINKED LIST (4)</h1>
<p align="center">RAYHAN RIZKI PUTRA</>

## Dasar Teori

3. MODUL 4 SINGLY LINKED LIST
## Guided 

### 1. [Nama Topik]

```C++
Type infotype : int
Type address : pointer to ElmList

Type ElmList <
    info : infotype
    next : address
>

Type List : < First : address >

procedure createList(input/output L : List)
function alokasi(x : infotype) → address
procedure dealokasi(input/output P : address)
procedure printInfo(input L : List)
procedure insertFirst(input/output L : List, input P : address)
```
Kode di atas digunakan untuk menampilkan list .
## Unguided 

### 1. [Soal,]

singlylist.h

```C++
#ifndef SINGLYLIST_H
#define SINGLYLIST_H

#include <iostream>
using namespace std;

typedef int infotype;

struct ElmList;
typedef ElmList* address;

struct ElmList {
    infotype info;
    address next;
};

struct List {
    address First;
};


void createList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertFirst(List &L, address P);

#endif


```
singlylist.cpp

```C++
#include "Singlylist.h"

void createList(List &L) {
    L.First = nullptr;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = nullptr;
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = nullptr;
}

void printInfo(List L) {
    address P = L.First;
    while (P != nullptr) {
        cout << P->info << " ";
        P = P->next;
    }
    cout << endl;
}

void insertFirst(List &L, address P) {
    P->next = L.First;
    L.First = P;
}

```

main.cpp

```C++

#include "Singlylist.h"

int main() {
    List L;
    address P1, P2, P3, P4, P5;

    createList(L);

    P1 = alokasi(2);
    insertFirst(L, P1);

    P2 = alokasi(0);
    insertFirst(L, P2);

    P3 = alokasi(8);
    insertFirst(L, P3);

    P4 = alokasi(12);
    insertFirst(L, P4);

    P5 = alokasi(9);
    insertFirst(L, P5);

    printInfo(L);

    return 0;
}

```


#### Output:
<img width="390" height="50" alt="Image" src="https://github.com/user-attachments/assets/a5204347-6d65-40f2-bf73-a7b37c7022e3" />

Kode di atas digunakan untuk membuat dan menampilkan isi Singly Linked List berupa data 9, 12, 8, 0, dan 2 menggunakan tiga file program Singlylist.h, Singlylist.cpp, dan main.cpp.

#### Full code Screenshot:


singlylist.h
<img width="690" height="509" alt="Image" src="https://github.com/user-attachments/assets/2b9cc879-77f4-4252-afbe-8644888d3df6" />

singlylist.cpp
<img width="492" height="572" alt="Image" src="https://github.com/user-attachments/assets/765f539e-1977-4103-afdb-813db0ce95ce" />

main.cpp
<img width="412" height="476" alt="image" src="https://github.com/user-attachments/assets/2d08c8c4-72d0-483a-bbb4-5372396e4ab8" />


### 2. [SOAL]

singlylist.h

```C++
#ifndef SINGLYLIST_H
#define SINGLYLIST_H

#include <iostream>
using namespace std;

typedef int infotype;

struct ElmList;
typedef ElmList* address;

struct ElmList {
    infotype info;
    address next;
};

struct List {
    address First;
};

// Deklarasi fungsi/prosedur
void createList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void insertFirst(List &L, address P);
void deleteFirst(List &L);
void deleteLast(List &L);
void deleteAfter(List &L, address Prec);
void printInfo(List L);
int nbList(List L);
void deleteList(List &L);

#endif


```

singlylist.cpp

```C++

#include "Singlylist.h"

void createList(List &L) {
    L.First = nullptr;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = nullptr;
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = nullptr;
}

void insertFirst(List &L, address P) {
    P->next = L.First;
    L.First = P;
}

void deleteFirst(List &L) {
    if (L.First != nullptr) {
        address P = L.First;
        L.First = P->next;
        dealokasi(P);
    }
}

void deleteLast(List &L) {
    if (L.First != nullptr) {
        if (L.First->next == nullptr) {
            deleteFirst(L);
        } else {
            address Q = L.First;
            address P = nullptr;
            while (Q->next != nullptr) {
                P = Q;
                Q = Q->next;
            }
            P->next = nullptr;
            dealokasi(Q);
        }
    }
}

void deleteAfter(List &L, address Prec) {
    if (Prec != nullptr && Prec->next != nullptr) {
        address P = Prec->next;
        Prec->next = P->next;
        dealokasi(P);
    }
}

void printInfo(List L) {
    address P = L.First;
    while (P != nullptr) {
        cout << P->info << " ";
        P = P->next;
    }
    cout << endl;
}

int nbList(List L) {
    int count = 0;
    address P = L.First;
    while (P != nullptr) {
        count++;
        P = P->next;
    }
    return count;
}

void deleteList(List &L) {
    while (L.First != nullptr) {
        deleteFirst(L);
    }
}

```

main.cpp

```C++
#include "Singlylist.h"

int main() {
    List L;
    address P1, P2, P3, P4, P5;

    createList(L);

    // Membuat list dari soal pertama
    P1 = alokasi(2);
    insertFirst(L, P1);
    P2 = alokasi(0);
    insertFirst(L, P2);
    P3 = alokasi(8);
    insertFirst(L, P3);
    P4 = alokasi(12);
    insertFirst(L, P4);
    P5 = alokasi(9);
    insertFirst(L, P5);

    cout << "Isi List awal: ";
    printInfo(L);

    // Penghapusan node sesuai soal
    cout << endl << "Hapus node 9 (deleteFirst)" << endl;
    deleteFirst(L);
    printInfo(L);

    cout << "Hapus node 2 (deleteLast)" << endl;
    deleteLast(L);
    printInfo(L);

    cout << "Hapus node 8 (deleteAfter)" << endl;
    deleteAfter(L, L.First); // setelah 12
    printInfo(L);

    cout << endl << "Jumlah node : " << nbList(L) << endl;

    cout << endl << "- List Berhasil Terhapus -" << endl;
    deleteList(L);
    cout << "Jumlah node : " << nbList(L) << endl;

    return 0;
}
```

### Output

### Fullscreenshot

<img width="347" height="243" alt="image" src="https://github.com/user-attachments/assets/61eaeba9-ffa9-4d3a-a277-5eff7435e824" />

singlylist.h

<img width="451" height="578" alt="image" src="https://github.com/user-attachments/assets/e43dcddd-c016-4730-ac38-97accd7e52ef" />

singlylist.cpp

<img width="1712" height="3404" alt="Image" src="https://github.com/user-attachments/assets/1ff4b0fc-1307-4650-b821-cc173bbea7dc" />

main.cpp

<img width="578" height="730" alt="image" src="https://github.com/user-attachments/assets/64b39fc0-d5c9-4de0-94c7-a964dc2906ae" />

kode ini menampilkan proses penghapusan node pada singly linked list hingga tersisa data 12 dan 0, lalu menghapus seluruh node tinggal 0

## Kesimpulan
Kedua kode tersebut menunjukkan cara membuat, menampilkan, dan menghapus data pada Singly Linked List. Soal pertama menampilkan proses pembentukan list dengan data 9 12 8 0 2, 
sedangkan soal kedua menampilkan proses penghapusan hingga list kosong dengan jumlah node 0.
## Referensi
Penggunaan Algoritma Doubly Linked List Untuk Insertion Dan Deletion — oleh Agung Wijoyo et al., Universitas Pamulang.







