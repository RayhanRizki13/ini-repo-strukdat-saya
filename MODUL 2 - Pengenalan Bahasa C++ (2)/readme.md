# <h1 align="center">Laporan Praktikum Modul Pengenalan Bahasa C++ (1)</h1>
<p align="center">RAYHAN RIZKI PUTRA</>

## Dasar Teori

1. MODUL PENGENALAN BAHASA C++ BAGIAN 2Kode di atas digunakan untuk menampilkan isi array 1 dimensi, 2 dimensi, dan 3 dimensi ke layar.

## Guided 

### 1. [Nama Topik]

```C++
#include <iostream>

using namespace std;

int main () {
    // array 1 dimensi
    int arrID[5] = {10,20,30,40,50};
    cout << "Array 1 Dimensi" << endl;
    for (int i=0; i<5; i++) {
        cout << "arrID" << i << " = " << arrID[i] << endl; 
        
    }
    cout << endl;

    // array 2 dimensi baris & kolom
    int arr2D[2][3] = {
        {1,2,3},
        {4,5,6}
    };
    cout << "Array 2 Dimensi" << endl;
    for (int i=0; i<2; i++) {
        for (int j=0; j<3; j++) {
            cout << "arr2D[" << i << "}[" << j << "] = " << arr2D[i][j]
            << " ";
        }
        cout << endl;
    }
    cout << endl;
    
    //array multi dimensi (3D)
    int arr3D[2][2][3] = {
    { { 1, 2, 3 }, {4, 5, 6} },
    { { 7, 8, 9} , {10, 11, 12} }   
    };
    cout << "array 3 dimensi" << endl;
    for (int i=0; i<2; i++) {
        for (int j=0; j<2; j++) {
            for (int k=0; k<3; k++) {
                cout << "arr3D[" << i << "][" << j << "]["
                << k << "] = " << arr3D[i][j][k] << endl;
            }
        }
    }

    return 0;
}
```
Kode di atas digunakan untuk menampilkan isi array 1 dimensi, 2 dimensi, dan 3 dimensi ke layar. Setiap elemen array dicetak menggunakan perulangan for dan ditampilkan dengan cout agar hasilnya muncul di layar.
## Unguided 

### 1. [Soal,]

```C++
#include <iostream>
using namespace std;

int main() {
    int A[3][3], B[3][3], C[3][3];
    int i, j, k;

    cout << "Masukkan elemen matriks A (3x3):\n";
    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++) {
            cout << "A[" << i << "][" << j << "] = ";
            cin >> A[i][j];
        }
    }

    cout << "\nMasukkan elemen matriks B (3x3):\n";
    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++) {
            cout << "B[" << i << "][" << j << "] = ";
            cin >> B[i][j];
        }
    }

    cout << "\nHasil Penjumlahan (A + B):\n";
    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++) {
            C[i][j] = A[i][j] + B[i][j];
            cout << C[i][j] << "\t";
        }
        cout << endl;
    }

 
    cout << "\nHasil Pengurangan (A - B):\n";
    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++) {
            C[i][j] = A[i][j] - B[i][j];
            cout << C[i][j] << "\t";
        }
        cout << endl;
    }

    cout << "\nHasil Perkalian (A x B):\n";
    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++) {
            C[i][j] = 0;
            for (k = 0; k < 3; k++) {
                C[i][j] += A[i][k] * B[k][j];
            }
            cout << C[i][j] << "\t";
        }
        cout << endl;
    }

    return 0;
}
```
#### Output:
<img width="1445" height="101" alt="Image" src="https://github.com/user-attachments/assets/765e5709-aac4-4a09-8c01-e86ba15ab472" />
Kode di atas digunakan untuk menghitung dan menampilkan hasil operasi dua matriks 3×3. Pengguna memasukkan elemen matriks A dan B, lalu memilih operasi (tambah, kurang, atau kali). Hasil perhitungan ditampilkan ke layar dengan cout.
#### Full code Screenshot:
<img width="1334" height="2456" alt="Image" src="https://github.com/user-attachments/assets/042b8939-27f4-461f-a129-efa99a6ae6ac" />
### 2. [SOAL]
```C++
#include <iostream>
using namespace std;

void tukarReference(int &a, int &b, int &c) {
    int temp = a;
    a = b;
    b = c;
    c = temp;
}

int main() {
    int x = 10, y = 20, z = 30;
    cout << "Sebelum: x=" << x << ", y=" << y << ", z=" << z << endl;
    tukarReference(x, y, z);
    cout << "Sesudah: x=" << x << ", y=" << y << ", z=" << z << endl;
}
```
### Output
<img width="980" height="125" alt="Image" src="https://github.com/user-attachments/assets/cac56ab9-6966-4bc7-a534-86066adae4cf" />
### Fullscreenshot
<img width="1443" height="929" alt="Image" src="https://github.com/user-attachments/assets/202af98b-162b-4e37-a1d0-afcabb4a3c4a" />
### 3. [SOAL]
```C++
#include <iostream>
using namespace std;

int cariMaks(int a[], int n) {
    int maks = a[0];
    for (int i = 1; i < n; i++)
        if (a[i] > maks) maks = a[i];
    return maks;
}

int cariMin(int a[], int n) {
    int min = a[0];
    for (int i = 1; i < n; i++)
        if (a[i] < min) min = a[i];
    return min;
}

void rataRata(int a[], int n) {
    float total = 0;
    for (int i = 0; i < n; i++)
        total += a[i];
    cout << "Rata-rata: " << total / n << endl;
}

int main() {
    int arr[] = {11, 8, 5, 7, 12, 26, 3, 54, 33, 55};
    int n = sizeof(arr) / sizeof(arr[0]);
    int pilih;

    do {
        cout << "\n--- Menu Array ---\n";
        cout << "1. Tampilkan array\n";
        cout << "2. Nilai maksimum\n";
        cout << "3. Nilai minimum\n";
        cout << "4. Nilai rata-rata\n";
        cout << "5. Keluar\n";
        cout << "Pilih: ";
        cin >> pilih;

        switch (pilih) {
            case 1:
                for (int i = 0; i < n; i++) cout << arr[i] << " ";
                cout << endl;   
                break;
            case 2:
                cout << "Maksimum: " << cariMaks(arr, n) << endl;
                break;
            case 3:
                cout << "Minimum: " << cariMin(arr, n) << endl;
                break;
            case 4:
                rataRata(arr, n);
                break;
            case 5:
                cout << "Selesai.\n";
                break;
            default:
                cout << "Pilihan salah!\n";
        }
    } while (pilih != 5);
}

```
### Output
<img width="1335" height="851" alt="Image" src="https://github.com/user-attachments/assets/55a736e9-77a1-4eec-860c-c07d1d5a2d4c" />
### Full screenshot
<img width="1334" height="2646" alt="Image" src="https://github.com/user-attachments/assets/4ef11507-fe6a-4a8d-b13c-e54bba7e3ee0" />
## Kesimpulan
Kode ini menyediakan menu interaktif untuk mengolah sebuah array: tampilkan isi, cari maksimum, minimum, atau hitung rata-rata. Setiap operasi dikerjakan oleh fungsi terpisah, dan program berulang sampai pengguna memilih keluar.
## Referensi
Belajar Pemrograman Lanjut dengan C++ (Putra, Munawir, Yuniarti, 2023)


