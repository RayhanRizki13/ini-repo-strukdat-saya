NAMA : RAYHAN RIZKI PUTRA
NIM : 103112400244
KELAS : IF-04
SOAL 1

SLLInventory.h
```C++
#ifndef SLLINVENTORY_H
#define SLLINVENTORY_H

#include <string>
using namespace std;

struct Product {
    string Nama;
    string SKU;
    int Jumlah;
    float HargaSatuan;
    float DiskonPersen; 
};

struct Node;
typedef Node* address;

struct Node {
    Product info;
    address next;
};

struct List {
    address head;
};


bool isEmpty(const List &L);
void createList(List &L);
address allocate(const Product &P);
void deallocate(address addr);

void insertFirst(List &L, const Product &P);
void insertLast(List &L, const Product &P);
void insertAfter(List &L, address Q, const Product &P);

void deleteFirst(List &L, Product &P);
void deleteLast(List &L, Product &P);
void deleteAfter(List &L, address Q, Product &P);

bool updateAtPosition(List &L, int posisi, const Product &P);
bool updateAtPositionInteractive(List &L, int posisi);

void viewList(const List &L);
void searchByFinalPriceRange(const List &L, float minPrice, float maxPrice);


void MaxHargaAkhir(const List&L);

#endif
```

SLLInventory.cpp
```C++

#include <iostream>
#include <iomanip>
#include "SLLInventory.h"

bool isEmpty(const List &L) {
    return L.head == nullptr;
}

void createList(List &L) {
    L.head = nullptr;
}

address allocate(const Product &P) {
    address p = new Node;
    p->info = P;
    p->next = nullptr;
    return p;
}

void deallocate(address addr) {
    delete addr;
}

void insertFirst(List &L, const Product &P) {
    address p = allocate(P);
    p->next = L.head;
    L.head = p;
}

void insertLast(List &L, const Product &P) {
    address p = allocate(P);
    if (isEmpty(L)) {
        L.head = p;
        return;
    }
    address cur = L.head;
    while (cur->next != nullptr) cur = cur->next;
    cur->next = p;
}

void insertAfter(List &L, address Q, const Product &P) {
    if (Q == nullptr) return;
    address p = allocate(P);
    p->next = Q->next;
    Q->next = p;
}

void deleteFirst(List &L, Product &P) {
    if (isEmpty(L)) return;
    address p = L.head;
    P = p->info;
    L.head = p->next;
    deallocate(p);
}

void deleteLast(List &L, Product &P) {
    if (isEmpty(L)) return;
    if (L.head->next == nullptr) {
        P = L.head->info;
        deallocate(L.head);
        L.head = nullptr;
        return;
    }
    address prev = nullptr, cur = L.head;
    while (cur->next != nullptr) {
        prev = cur;
        cur = cur->next;
    }
    P = cur->info;
    prev->next = nullptr;
    deallocate(cur);
}

void deleteAfter(List &L, address Q, Product &P) {
    if (Q == nullptr || Q->next == nullptr) return;
    address p = Q->next;
    P = p->info;
    Q->next = p->next;
    deallocate(p);
}

static float HargaAkhir(const Product &P) {
    return P.HargaSatuan * (1.0f - P.DiskonPersen / 100.0f);
}

bool updateAtPosition(List &L, int posisi, const Product &P) {
    if (posisi <= 0) return false;
    address cur = L.head;
    int idx = 1;
    while (cur != nullptr && idx < posisi) {
        cur = cur->next;
        idx++;
    }
    if (cur == nullptr) return false;
    cur->info = P;
    return true;
}

bool updateAtPositionInteractive(List &L, int posisi) {
    if (posisi <= 0) return false;
    address cur = L.head;
    int idx = 1;
    while (cur != nullptr && idx < posisi) {
        cur = cur->next;
        idx++;
    }
    if (cur == nullptr) return false;
    Product P;
    cout << "Masukkan data baru untuk posisi " << posisi << "\n";
    cout << "Nama: ";
    getline(cin >> ws, P.Nama);
    cout << "SKU: ";
    getline(cin, P.SKU);
    cout << "Jumlah: ";
    cin >> P.Jumlah;
    cout << "HargaSatuan: ";
    cin >> P.HargaSatuan;
    cout << "DiskonPersen: ";
    cin >> P.DiskonPersen;
    cur->info = P;
    return true;
}

void viewList(const List &L) {
    if (isEmpty(L)) {
        cout << "List kosong." << endl;
        return;
    }
    address cur = L.head;
    int idx = 1;
    cout << left << setw(5) << "No" << setw(20) << "Nama" << setw(8) << "SKU" << setw(8) << "Jumlah" << setw(14) << "HargaSatuan" << setw(14) << "Diskon(%)" << setw(14) << "HargaAkhir" << endl;
    cout << string(85, '-') << endl;
    while (cur != nullptr) {
        cout << setw(5) << idx
             << setw(20) << cur->info.Nama
             << setw(8) << cur->info.SKU
             << setw(8) << cur->info.Jumlah
             << setw(14) << fixed << setprecision(2) << cur->info.HargaSatuan
             << setw(14) << cur->info.DiskonPersen
             << setw(14) << fixed << setprecision(2) << HargaAkhir(cur->info)
             << endl;
        cur = cur->next;
        idx++;
    }
}

void searchByFinalPriceRange(const List &L, float minPrice, float maxPrice) {
    if (isEmpty(L)) {
        cout << "List kosong." << endl;
        return;
    }
    address cur = L.head;
    int idx = 1;
    bool found = false;
    cout << "Hasil pencarian HargaAkhir dalam rentang [" << minPrice << ", " << maxPrice << "]:" << endl;
    while (cur != nullptr) {
        float ha = HargaAkhir(cur->info);
        if (ha >= minPrice && ha <= maxPrice) {
            cout << "Posisi " << idx << ": " << cur->info.Nama << " (SKU: " << cur->info.SKU << ") - HargaAkhir = " << fixed << setprecision(2) << ha << endl;
            found = true;
        }
        cur = cur->next;
        idx++;
    }
    if (!found) cout << "Tidak ditemukan produk dalam rentang tersebut." << endl;
}

void MaxHargaAkhir(const List &L) {
    if (isEmpty(L)) {
        cout << "List kosong." << endl;
        return;
    }
    address cur = L.head;
    float maxHA = HargaAkhir(cur->info);
    while (cur != nullptr) {
        float ha = HargaAkhir(cur->info);
        if (ha > maxHA) maxHA = ha;
        cur = cur->next;
    }
    cur = L.head;
    int idx = 1;
    cout << "Produk dengan HargaAkhir maksimum (" << fixed << setprecision(2) << maxHA << "):" << endl;
    while (cur != nullptr) {
        float ha = HargaAkhir(cur->info);
        if (abs(ha - maxHA) < 1e-3) {
            cout << "Posisi " << idx << ": " << cur->info.Nama << " (SKU: " << cur->info.SKU << ") - Jumlah: " << cur->info.Jumlah << " - HargaSatuan: " << cur->info.HargaSatuan << " - Diskon(%): " << cur->info.DiskonPersen << "\n";
        }
        cur = cur->next;
    idx++;
    }
}
```

main.cpp

```C++
#include <iostream>
#include "SLLInventory.h"
using namespace std;

int main() {
    List L;
    createList(L);

    Product p1 {"Pulpen", "A001", 20, 2500.0f, 0.0f};
    Product p2 {"Buku Tulis", "A002", 15, 5000.0f, 10.0f};
    Product p3 {"Penghapus", "A003", 30, 1500.0f, 0.0f};

    insertLast(L, p1);
    insertLast(L, p2);
    insertLast(L, p3);

    cout << "-- List awal --" << endl;
    viewList(L);
    cout << endl;

    Product temp;
    deleteFirst(L, temp);
    cout << "Setelah deleteFirst() -> produk yang dihapus: " << temp.Nama << " (" << temp.SKU << ")" << endl;

    cout << "-- List setelah deleteFirst --" << endl;
    viewList(L);
    cout << endl;

    Product newP {"Stabilo", "A010", 40, 9000.0f, 5.0f};
    bool ok = updateAtPosition(L, 2, newP);
    if (!ok) cout << "Update gagal: posisi tidak ada." << endl;

    cout << "-- List setelah update posisi 2 --" << endl;
    viewList(L);
    cout << endl;

    cout << "-- Searching HargaAkhir [2000,7000] --" << endl;
    searchByFinalPriceRange(L, 2000.0f, 7000.0f);
    cout << endl;

    MaxHargaAkhir(L);
    return 0;
}

```

### OUTPUT

<img width="756" height="494" alt="Image" src="https://github.com/user-attachments/assets/6b3283b7-d8bc-44b2-8289-a09c15ecbc39" />

SOAL 2

DLLPlaylist.h

```C++
#ifndef DLLPLAYLIST_H
#define DLLPLAYLIST_H

#include <iostream>
#include <string>
using namespace std;

struct Song {
    string Title;
    string Artist;
    int DurationSec;
    int PlayCount;
    float Rating;
};

struct Node {
    Song info;
    Node* prev;
    Node* next;
};

struct List {
    Node* head;
    Node* tail;
};

bool isEmpty(List L);
void createList(List &L);
Node* allocate(Song S);
void deallocate(Node* P);

void insertFirst(List &L, Song S);
void insertLast(List &L, Song S);
void insertAfter(List &L, Node* Q, Song S);
void insertBefore(List &L, Node* Q, Song S);

void deleteFirst(List &L, Song &S);
void deleteLast(List &L, Song &S);
void deleteAfter(List &L, Node* Q, Song &S);
void deleteBefore(List &L, Node* Q, Song &S);

void updateAtPosition(List &L, int posisi);
void updateBefore(List &L, Node* Q);

float getPopularityScore(Song S);
void viewList(List L);
void searchByPopularityRange(List L, float minScore, float maxScore);

#endif

```

DLLPlaylist.cpp

```C++

#include "DLLPlaylist.h"

bool isEmpty(List L) {
    return (L.head == NULL && L.tail == NULL);
}

void createList(List &L) {
    L.head = NULL;
    L.tail = NULL;
}

Node* allocate(Song S) {
    Node* P = new Node;
    P->info = S;
    P->prev = NULL;
    P->next = NULL;
    return P;
}

void deallocate(Node* P) {
    delete P;
}

void insertFirst(List &L, Song S) {
    Node* P = allocate(S);
    if (isEmpty(L)) {
        L.head = P;
        L.tail = P;
    } else {
        P->next = L.head;
        L.head->prev = P;
        L.head = P;
    }
}

void insertLast(List &L, Song S) {
    Node* P = allocate(S);
    if (isEmpty(L)) {
        L.head = P;
        L.tail = P;
    } else {
        L.tail->next = P;
        P->prev = L.tail;
        L.tail = P;
    }
}

void insertAfter(List &L, Node* Q, Song S) {
    if (Q != NULL) {
        Node* P = allocate(S);
        P->next = Q->next;
        P->prev = Q;
        if (Q->next != NULL) {
            Q->next->prev = P;
        } else {
            L.tail = P;
        }
        Q->next = P;
    }
}

void insertBefore(List &L, Node* Q, Song S) {
    if (Q != NULL) {
        if (Q == L.head) {
            insertFirst(L, S);
        } else {
            Node* P = allocate(S);
            P->next = Q;
            P->prev = Q->prev;
            Q->prev->next = P;
            Q->prev = P;
        }
    }
}

void deleteFirst(List &L, Song &S) {
    if (!isEmpty(L)) {
        Node* P = L.head;
        S = P->info;

        if (L.head == L.tail) {
            L.head = NULL;
            L.tail = NULL;
        } else {
            L.head = L.head->next;
            L.head->prev = NULL;
        }

        deallocate(P);
    }
}

void deleteLast(List &L, Song &S) {
    if (!isEmpty(L)) {
        Node* P = L.tail;
        S = P->info;

        if (L.head == L.tail) {
            L.head = NULL;
            L.tail = NULL;
        } else {
            L.tail = L.tail->prev;
            L.tail->next = NULL;
        }

        deallocate(P);
    }
}

void deleteAfter(List &L, Node* Q, Song &S) {
    if (Q != NULL && Q->next != NULL) {
        Node* P = Q->next;
        S = P->info;

        Q->next = P->next;
        if (P->next != NULL) {
            P->next->prev = Q;
        } else {
            L.tail = Q;
        }

        deallocate(P);
    }
}

void deleteBefore(List &L, Node* Q, Song &S) {
    if (Q != NULL && Q->prev != NULL) {
        Node* P = Q->prev;
        S = P->info;

        if (P->prev != NULL) {
            P->prev->next = Q;
            Q->prev = P->prev;
        } else {
            L.head = Q;
            Q->prev = NULL;
        }

        deallocate(P);
    }
}

void updateAtPosition(List &L, int posisi) {
    Node* P = L.head;
    int idx = 1;

    while (P != NULL && idx < posisi) {
        P = P->next;
        idx++;
    }

    if (P != NULL) {
        Song S;
        cout << "Masukkan Title baru: ";
        getline(cin, S.Title);
        cout << "Masukkan Artist baru: ";
        getline(cin, S.Artist);
        cout << "Masukkan Duration: ";
        cin >> S.DurationSec;
        cout << "Masukkan PlayCount: ";
        cin >> S.PlayCount;
        cout << "Masukkan Rating: ";
        cin >> S.Rating;
        cin.ignore();

        P->info = S;
    }
}

void updateBefore(List &L, Node* Q) {
    if (Q != NULL && Q->prev != NULL) {
        Node* P = Q->prev;
        Song S;

        cout << "Masukkan Title baru: ";
        getline(cin, S.Title);
        cout << "Masukkan Artist baru: ";
        getline(cin, S.Artist);
        cout << "Masukkan Duration: ";
        cin >> S.DurationSec;
        cout << "Masukkan PlayCount: ";
        cin >> S.PlayCount;
        cout << "Masukkan Rating: ";
        cin >> S.Rating;
        cin.ignore();

        P->info = S;
    }
}

float getPopularityScore(Song S) {
    return 0.8 * S.PlayCount + 20.0 * S.Rating;
}

void viewList(List L) {
    Node* P = L.head;
    int pos = 1;

    cout << "\n=== PLAYLIST ===\n";
    while (P != NULL) {
        cout << pos << ". " << P->info.Title << " | "
             << P->info.Artist << " | Dur: " << P->info.DurationSec
             << " | Play: " << P->info.PlayCount
             << " | Rating: " << P->info.Rating
             << " | Popularity: " << getPopularityScore(P->info)
             << endl;

        P = P->next;
        pos++;
    }
}

void searchByPopularityRange(List L, float minScore, float maxScore) {
    Node* P = L.head;
    int pos = 1;

    cout << "\n=== HASIL SEARCH ===\n";

    while (P != NULL) {
        float score = getPopularityScore(P->info);
        if (score >= minScore && score <= maxScore) {
            cout << pos << ". " << P->info.Title 
                 << " | Popularity: " << score << endl;
        }
        P = P->next;
        pos++;
    }
}
```

main.cpp

```C++
#include "DLLPlaylist.h"

Node* getNodeAt(List L, int posisi) {
    Node* P = L.head;
    int idx = 1;
    while (P != NULL && idx < posisi) {
        P = P->next;
        idx++;
    }
    return P;
}

int main() {
    List L;
    createList(L);

    // Data lagu
    Song S1 = {"Senja di Kota", "Nona Band", 210, 150, 4.2};
    Song S2 = {"Langkahmu", "Delta", 185, 320, 4.8};
    Song S3 = {"Hujan Minggu", "Arka", 240, 90, 3.9};

    insertLast(L, S1);
    insertLast(L, S2);
    insertLast(L, S3);

    viewList(L);

    Song temp;
    deleteLast(L, temp);

    cout << "\n=== UPDATE POSISI 2 ===\n";
    cin.ignore(); 
    Song dummy;
    updateAtPosition(L, 2);

    viewList(L);

    cout << "\n=== INSERT BEFORE POSISI 2 ===\n";
    Song Snew = {"Senandung", "Mira", 175, 120, 4.0};

    Node* pos2 = getNodeAt(L, 2);
    insertBefore(L, pos2, Snew);

    viewList(L);

    cout << "\n=== UPDATE BEFORE POSISI 2 ===\n";
    updateBefore(L, pos2);

    viewList(L);

    cout << "\n=== DELETE BEFORE POSISI 3 ===\n";
    Node* pos3 = getNodeAt(L, 3);
    deleteBefore(L, pos3, temp);

    viewList(L);

    cout << "\n=== SEARCH (150 - 300) ===\n";
    searchByPopularityRange(L, 150.0, 300.0);

    return 0;
}
```
### OUTPUT
<img width="808" height="161" alt="image" src="https://github.com/user-attachments/assets/c384c035-9ac0-4ca1-992c-ee2b8789aca6" />

SOAL KETIGA

StackMahasiswa.h

```C++

#ifndef STACKMAHASISWA_H
#define STACKMAHASISWA_H

#include <iostream>
#include <string>
using namespace std;

const int MAX = 6;

struct Mahasiswa {
    string Nama;
    string NIM;
    float NilaiTugas;
    float NilaiUTS;
    float NilaiUAS;
};

struct StackMahasiswa {
    Mahasiswa dataMahasiswa[MAX];
    int Top;
};

// Prototype
bool isEmpty(StackMahasiswa StackMHS);
bool isFull(StackMahasiswa StackMHS);
void createStack(StackMahasiswa &StackMHS);

void Push(StackMahasiswa &StackMHS);
void Pop(StackMahasiswa &StackMHS);
void Update(StackMahasiswa &StackMHS, int posisi);
void View(StackMahasiswa StackMHS);

float hitungNilaiAkhir(Mahasiswa MHS);
void SearchNilaiAkhir(StackMahasiswa StackMHS, float NilaiMin, float NilaiMax);

void MaxNilaiAkhir(StackMahasiswa StackMHS);

#endif

```

StackMahasiswa.cpp

```C++
#include "StackMahasiswa.h"

bool isEmpty(StackMahasiswa StackMHS) {
    return StackMHS.Top == -1;
}

bool isFull(StackMahasiswa StackMHS) {
    return StackMHS.Top == MAX - 1;
}

void createStack(StackMahasiswa &StackMHS) {
    StackMHS.Top = -1;
}

void Push(StackMahasiswa &StackMHS) {
    if (isFull(StackMHS)) {
        cout << "Stack penuh!\n";
        return;
    }

    Mahasiswa M;

    cin.ignore();
    cout << "Nama         : "; getline(cin, M.Nama);
    cout << "NIM          : "; getline(cin, M.NIM);
    cout << "Nilai Tugas  : "; cin >> M.NilaiTugas;
    cout << "Nilai UTS    : "; cin >> M.NilaiUTS;
    cout << "Nilai UAS    : "; cin >> M.NilaiUAS;

    StackMHS.Top++;
    StackMHS.dataMahasiswa[StackMHS.Top] = M;
}

void Pop(StackMahasiswa &StackMHS) {
    if (isEmpty(StackMHS)) {
        cout << "Stack kosong!\n";
        return;
    }
    StackMHS.Top--;
}

void Update(StackMahasiswa &StackMHS, int posisi) {
    if (posisi < 1 || posisi > StackMHS.Top + 1) {
        cout << "Posisi tidak valid!\n";
        return;
    }

    Mahasiswa M;
    cin.ignore();
    cout << "Update Nama        : "; getline(cin, M.Nama);
    cout << "Update NIM         : "; getline(cin, M.NIM);
    cout << "Update NilaiTugas  : "; cin >> M.NilaiTugas;
    cout << "Update NilaiUTS    : "; cin >> M.NilaiUTS;
    cout << "Update NilaiUAS    : "; cin >> M.NilaiUAS;

    StackMHS.dataMahasiswa[posisi - 1] = M;
}

float hitungNilaiAkhir(Mahasiswa MHS) {
    return (0.2 * MHS.NilaiTugas) + (0.4 * MHS.NilaiUTS) + (0.4 * MHS.NilaiUAS);
}

void View(StackMahasiswa StackMHS) {
    if (isEmpty(StackMHS)) {
        cout << "Stack kosong!\n";
        return;
    }

    cout << "\n=== DATA STACK MAHASISWA ===\n";

    for (int i = StackMHS.Top; i >= 0; i--) {
        cout << "Posisi " << i + 1 << endl;
        cout << "Nama       : " << StackMHS.dataMahasiswa[i].Nama << endl;
        cout << "NIM        : " << StackMHS.dataMahasiswa[i].NIM << endl;
        cout << "NilaiAkhir : " << hitungNilaiAkhir(StackMHS.dataMahasiswa[i]) << endl;
        cout << "-------------------------\n";
    }
}

void SearchNilaiAkhir(StackMahasiswa StackMHS, float NilaiMin, float NilaiMax) {
    cout << "\n=== HASIL SEARCH NILAI AKHIR ===\n";

    for (int i = 0; i <= StackMHS.Top; i++) {
        float nilaiAkhir = hitungNilaiAkhir(StackMHS.dataMahasiswa[i]);
        if (nilaiAkhir >= NilaiMin && nilaiAkhir <= NilaiMax) {
            cout << "Ditemukan di posisi " << i + 1 << endl;
            cout << "Nama  : " << StackMHS.dataMahasiswa[i].Nama << endl;
            cout << "NIM   : " << StackMHS.dataMahasiswa[i].NIM << endl;
            cout << "NilaiAkhir : " << nilaiAkhir << endl;
            cout << "-------------------------\n";
        }
    }
}

void MaxNilaiAkhir(StackMahasiswa StackMHS) {
    if (isEmpty(StackMHS)) {
        cout << "Stack kosong!\n";
        return;
    }

    float maxNilai = -999;
    int posisi = -1;

    for (int i = 0; i <= StackMHS.Top; i++) {
        float nilai = hitungNilaiAkhir(StackMHS.dataMahasiswa[i]);
        if (nilai > maxNilai) {
            maxNilai = nilai;
            posisi = i + 1;
        }
    }

    cout << "\n=== NILAI AKHIR TERBESAR ===\n";
    cout << "Nama  : " << StackMHS.dataMahasiswa[posisi - 1].Nama << endl;
    cout << "NIM   : " << StackMHS.dataMahasiswa[posisi - 1].NIM << endl;
    cout << "Nilai Akhir : " << maxNilai << endl;
    cout << "Posisi      : " << posisi << endl;
}
```

main.cpp

```C++
#include "StackMahasiswa.h"

int main() {
    StackMahasiswa S;
    createStack(S);

    Mahasiswa M1 = {"Venti", "11111", 75.7, 82.1, 65.5};
    Mahasiswa M2 = {"Xiao", "22222", 87.4, 88.9, 81.9};
    Mahasiswa M3 = {"Kazuha", "33333", 92.3, 88.8, 82.4};
    Mahasiswa M4 = {"Wanderer", "44444", 95.5, 85.5, 90.5};
    Mahasiswa M5 = {"Lynette", "55555", 77.7, 65.4, 79.9};
    Mahasiswa M6 = {"Chasca", "66666", 99.9, 93.6, 87.3};

    S.Top++; S.dataMahasiswa[S.Top] = M1;
    S.Top++; S.dataMahasiswa[S.Top] = M2;
    S.Top++; S.dataMahasiswa[S.Top] = M3;
    S.Top++; S.dataMahasiswa[S.Top] = M4;
    S.Top++; S.dataMahasiswa[S.Top] = M5;
    S.Top++; S.dataMahasiswa[S.Top] = M6;

    View(S);

    Pop(S);

    View(S);

    cout << "\n=== UPDATE POSISI 3 ===\n";
    cin.ignore();
    Mahasiswa Upd = {"Heizou", "77777", 99.9, 88.8, 77.7};
    S.dataMahasiswa[2] = Upd;

    View(S);

    SearchNilaiAkhir(S, 85.5, 95.5);

    MaxNilaiAkhir(S);

    return 0;
}
```
### OUTPUT
<img width="495" height="810" alt="image" src="https://github.com/user-attachments/assets/b8434b7c-f369-4166-be2f-4c6cc55fd0a1" />

SOAL KEEMPAT

QueuePengiriman.h

```C++
#ifndef QUEUEPENGIRIMAN_H
#define QUEUEPENGIRIMAN_H
#include <iostream>
using namespace std;

const int MAX = 5;

struct Paket {
    string KodeResi;
    string NamaPengirim;
    int BeratBarang; 
    string Tujuan;
};

struct QueueEkspedisi {
    Paket dataPaket[MAX];
    int Head;
    int Tail;
};

bool isEmpty(QueueEkspedisi Q);
bool isFull(QueueEkspedisi Q);
void createQueue(QueueEkspedisi &Q);
void enQueue(QueueEkspedisi &Q);
void deQueue(QueueEkspedisi &Q);
void viewQueue(QueueEkspedisi Q);

int TotalBiayaPengiriman(QueueEkspedisi Q);

#endif
```

QueuePengiriman.cpp

```C++
#include "QueuePengiriman.h"

bool isEmpty(QueueEkspedisi Q) {
    return (Q.Head == -1 && Q.Tail == -1);
}

bool isFull(QueueEkspedisi Q) {
    return (Q.Tail == MAX - 1);
}

void createQueue(QueueEkspedisi &Q) {
    Q.Head = -1;
    Q.Tail = -1;
}

void enQueue(QueueEkspedisi &Q) {
    if (isFull(Q)) {
        cout << "Queue penuh! Tidak bisa tambah data.\n";
    } else {
        Paket P;
        cout << "Masukkan Kode Resi       : ";
        cin >> P.KodeResi;
        cout << "Masukkan Nama Pengirim   : ";
        cin >> P.NamaPengirim;
        cout << "Masukkan Berat Barang(kg): ";
        cin >> P.BeratBarang;
        cout << "Masukkan Tujuan          : ";
        cin >> P.Tujuan;

        if (isEmpty(Q)) {
            Q.Head = Q.Tail = 0;
        } else {
            Q.Tail++;
        }
        Q.dataPaket[Q.Tail] = P;

        cout << "Data berhasil ditambahkan!\n";
    }
}

void deQueue(QueueEkspedisi &Q) {
    if (isEmpty(Q)) {
        cout << "Queue kosong! Tidak bisa hapus.\n";
    } else {
        cout << "Menghapus paket dengan Resi: " 
             << Q.dataPaket[Q.Head].KodeResi << endl;

        for (int i = Q.Head; i < Q.Tail; i++) {
            Q.dataPaket[i] = Q.dataPaket[i + 1];
        }

        Q.Tail--;
        if (Q.Tail < Q.Head) {
            createQueue(Q);
        }
    }
}

void viewQueue(QueueEkspedisi Q) {
    if (isEmpty(Q)) {
        cout << "Queue kosong!\n";
    } else {
        cout << "\n=== Daftar Paket Dalam Queue ===\n";
        for (int i = Q.Head; i <= Q.Tail; i++) {
            cout << "Posisi " << i << " :\n";
            cout << "  Resi      : " << Q.dataPaket[i].KodeResi << endl;
            cout << "  Pengirim  : " << Q.dataPaket[i].NamaPengirim << endl;
            cout << "  Berat     : " << Q.dataPaket[i].BeratBarang << " kg\n";
            cout << "  Tujuan    : " << Q.dataPaket[i].Tujuan << endl;
            cout << "------------------------------\n";
        }
    }
}

int TotalBiayaPengiriman(QueueEkspedisi Q) {
    int total = 0;
    if (isEmpty(Q)) return 0;

    for (int i = Q.Head; i <= Q.Tail; i++) {
        total += Q.dataPaket[i].BeratBarang * 8250;
    }
    return total;
}
```

main.cpp

```C++
#include <iostream>
#include "QueuePengiriman.h"
using namespace std;

int main() {
    QueueEkspedisi Q;
    createQueue(Q);

    int pilihan;
    do {
        cout << "\n--- Komaniya Ekspress ---\n";
        cout << "1. Input Data Paket\n";
        cout << "2. Hapus Data Paket\n";
        cout << "3. Tampilkan Queue Paket\n";
        cout << "4. Hitung Total Biaya Pengiriman\n";
        cout << "5. Exit\n";
        cout << "Pilihan anda : ";
        cin >> pilihan;

        switch (pilihan) {
        case 1:
            enQueue(Q);
            break;

        case 2:
            deQueue(Q);
            break;

        case 3:
            viewQueue(Q);
            break;

        case 4:
            cout << "\nTotal biaya pengiriman: Rp "
                 << TotalBiayaPengiriman(Q) << endl;
            break;

        case 5:
            cout << "Program selesai.\n";
            break;

        default:
            cout << "Pilihan tidak valid!\n";
        }
    } while (pilihan != 5);

    return 0;
}
```

### OUTPUT
<img width="539" height="542" alt="image" src="https://github.com/user-attachments/assets/caaaaa49-cc89-48dc-83b3-3d9fa780b299" />




