# <h1 align="center">Laporan Praktikum Modul ABSTRACT DATA TYPE (ADT) (3)</h1>
<p align="center">RAYHAN RIZKI PUTRA</>

## Dasar Teori

3. MODUL 3 ABSTRACT DATA TYPE (ADT)
## Guided 

### 1. [Nama Topik]

```C++
#include <iostream>
using namespace std;
struct mahasiswa{
 char nim[10];
 int nilai1,nilai2;
};
void inputMhs(mahasiswa &m);
float rata2(mahasiswa m);
int main()
{
 mahasiswa mhs;
 inputMhs(mhs);
 cout << “rata-rata = “ << rata2(mhs);
 return 0;
}
void inputMhs(mahasiswa &m){
 cout << “input nama = “;
 cin >> m.nim;
 cout << “input nilai = “;
 cin >> m.nilai1;
 cout << “input nilai2 = “;
 cin >> m.nilai2;
}
float rata2(mahasiswa m){
 return float(m.nilai1+m.nilai2)/2
```
Kode di atas digunakan untuk menampilkan list mahasiswa dan input nilai.
## Unguided 

### 1. [Soal,]

```C++
#include <iostream>
#include <string>
using namespace std;

struct Mahasiswa {
    string nama;
    string nim;
    float uts;
    float uas;
    float tugas;
    float nilaiAkhir;
};

float hitungNilaiAkhir(float uts, float uas, float tugas) {
    return (0.3 * uts) + (0.4 * uas) + (0.3 * tugas);
}

int main() {
    Mahasiswa mhs[10];
    int n;

    cout << "Masukkan jumlah mahasiswa (maks 10): ";
    cin >> n;
    cin.ignore(); 

    if (n > 10) n = 10; 

    for (int i = 0; i < n; i++) {
        cout << "\nData mahasiswa ke-" << i + 1 << endl;
        cout << "Nama   : ";
        getline(cin, mhs[i].nama);
        cout << "NIM    : ";
        getline(cin, mhs[i].nim);
        cout << "UTS    : ";
        cin >> mhs[i].uts;
        cout << "UAS    : ";
        cin >> mhs[i].uas;
        cout << "Tugas  : ";
        cin >> mhs[i].tugas;

        mhs[i].nilaiAkhir = hitungNilaiAkhir(mhs[i].uts, mhs[i].uas, mhs[i].tugas);
        cin.ignore();
    }

    cout << "\n=========================================\n";
    cout << "DATA MAHASISWA\n";
    cout << "=========================================\n";
    for (int i = 0; i < n; i++) {
        cout << "Nama        : " << mhs[i].nama << endl;
        cout << "NIM         : " << mhs[i].nim << endl;
        cout << "UTS         : " << mhs[i].uts << endl;
        cout << "UAS         : " << mhs[i].uas << endl;
        cout << "Tugas       : " << mhs[i].tugas << endl;
        cout << "Nilai Akhir : " << mhs[i].nilaiAkhir << endl;
        cout << "-----------------------------------------\n";
    }

    return 0;
}
```

#### Output:
<img width="1451" height="972" alt="Image" src="https://github.com/user-attachments/assets/a75593cc-3e41-458d-8b72-15d2b602a577" />
Kode di atas digunakan untuk menghitung dan menampilkan hasil operasi dua matriks 3×3. Pengguna memasukkan elemen matriks A dan B, lalu memilih operasi (tambah, kurang, atau kali). Hasil perhitungan ditampilkan ke layar dengan cout.
#### Full code Screenshot:
<img width="1334" height="2646" alt="Image" src="https://github.com/user-attachments/assets/8241a414-22f5-448e-bae0-f0ca5aa329e5" />


### 2. [SOAL]

pelajaran.h

```C++
#ifndef PELAJARAN_H
#define PELAJARAN_H
#include <string>
using namespace std;

struct pelajaran {
    string namaMapel;
    string kodePel;
};

// Fungsi untuk membuat data pelajaran baru
pelajaran create_pelajaran(string namaMapel, string kodePel);

// Prosedur untuk menampilkan data pelajaran
void tampil_pelajaran(pelajaran pel);

#endif
```


pelajaran.cpp

```C++
#ifndef PELAJARAN_H
#define PELAJARAN_H
#include <string>
using namespace std;

struct pelajaran {
    string namaMapel;
    string kodePel;
};

// Fungsi untuk membuat data pelajaran baru
pelajaran create_pelajaran(string namaMapel, string kodePel);

// Prosedur untuk menampilkan data pelajaran
void tampil_pelajaran(pelajaran pel);

#endif
```

main.cpp

```C++
#include <iostream>
#include "pelajaran.h"
using namespace std;

int main() {
    string namaMapel = "Struktur Data";
    string kodePel = "STD";

    pelajaran pel = create_pelajaran(namaMapel, kodePel);
    tampil_pelajaran(pel);

    return 0;
}
```
### Output
<img width="636" height="135" alt="Image" src="https://github.com/user-attachments/assets/4b578767-b2be-47f2-8b5b-a2d91f785b70" />
### Fullscreenshot
pelajaran.h
<img width="529" height="300" alt="Image" src="https://github.com/user-attachments/assets/97637202-c76a-45a5-b139-592e20482f48" />
pelajaran.cpp
<img width="566" height="308" alt="Image" src="https://github.com/user-attachments/assets/2db20fd2-3a30-4006-aad4-234667cc0724" />
main.cpp
<img width="570" height="257" alt="Image" src="https://github.com/user-attachments/assets/814d5cbe-e01c-4f5c-a0b9-b13347a0088a" />
kode diatas untuk membuat program lebih terstruktur, modular, dan mudah dikembangkan.

### 3. [SOAL]
```C++
#include <iostream>
using namespace std;

// Fungsi untuk menampilkan isi array 2D
void tampilArray(int arr[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << arr[i][j] << "\t";
        }
        cout << endl;
    }
}

// Fungsi untuk menukar isi dari dua array 2D pada posisi tertentu
void tukarElemen(int arr1[3][3], int arr2[3][3], int baris, int kolom) {
    int temp = arr1[baris][kolom];
    arr1[baris][kolom] = arr2[baris][kolom];
    arr2[baris][kolom] = temp;
}

// Fungsi untuk menukar isi dari dua pointer integer
void tukarPointer(int* ptr1, int* ptr2) {
    int temp = *ptr1;
    *ptr1 = *ptr2;
    *ptr2 = temp;
}

int main() {
    int A[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    int B[3][3] = {
        {9, 8, 7},
        {6, 5, 4},
        {3, 2, 1}
    };

    int x = 10, y = 20;
    int *p1 = &x;
    int *p2 = &y;

    cout << "Array A sebelum ditukar:\n";
    tampilArray(A);
    cout << "\nArray B sebelum ditukar:\n";
    tampilArray(B);

    // Menukar elemen pada posisi [1][2] (baris ke-2 kolom ke-3)
    tukarElemen(A, B, 1, 2);

    cout << "\nSetelah menukar elemen pada posisi [1][2]:\n";
    cout << "Array A:\n";
    tampilArray(A);
    cout << "\nArray B:\n";
    tampilArray(B);

    // Menampilkan nilai pointer sebelum ditukar
    cout << "\nNilai yang ditunjuk pointer sebelum ditukar:\n";
    cout << "p1 menunjuk nilai = " << *p1 << endl;
    cout << "p2 menunjuk nilai = " << *p2 << endl;

    // Menukar nilai yang ditunjuk pointer
    tukarPointer(p1, p2);

    cout << "\nNilai yang ditunjuk pointer setelah ditukar:\n";
    cout << "p1 menunjuk nilai = " << *p1 << endl;
    cout << "p2 menunjuk nilai = " << *p2 << endl;

    return 0;
}
```
### Output
<img width="647" height="502" alt="Image" src="https://github.com/user-attachments/assets/00505de1-3b1e-4dbb-bad0-1ac394e248d3" />
### Full screenshot
<img width="1712" height="3102" alt="Image" src="https://github.com/user-attachments/assets/0748d840-651f-4048-a344-7891bcbd8099" />
## Kesimpulan
Kode ini menunjukkan bagaimana penggunaan array dua dimensi (2D) dan pointer dalam bahasa C++. Program ini mendemonstrasikan tiga konsep utama.
## Referensi
Abstract Data Types in Object-Capability Systems — James Noble, Sophia Drossopoulou, Mark S. Miller, Toby Murray, Alex Potanin (ECOOP 2016)






