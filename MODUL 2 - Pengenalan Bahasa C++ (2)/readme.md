# <h1 align="center">Laporan Praktikum Modul Pengenalan Bahasa C++ (1)</h1>
<p align="center">r</Rayhan RIZKI PUTRA>

## Dasar Teori

Berikan penjelasan teori terkait materi modul ini dengan bahasa anda sendiri serta susunan yang terstruktur per topiknya.

## Guided 

### 1. [Nama Topik]

```C++
#include <iostream>
using namespace std;

int main () {
    int a;
    int b;

    cout << "masukan angka: ";
    cin >> a;
    cout << "masukan angka: ";
    cin >> b;

    //operator aritmatika
    cout << "a + b = " << (a+b) << endl;
    cout << "a - b = " << (a-b) << endl;
    cout << "a * b = " << (a*b) << endl;
    cout << "a / b = " << (a/b) << endl;
    cout << "a % b = " << (a%b) << endl;

    //operator logika
    cout << "a < b = " << (a<b) << endl;
    cout << "a > b = " << (a>b) << endl;
    cout << "a <= b = " << (a<=b) << endl;
    cout << "a >= b = " << (a>=b) << endl;
    cout << "a == b = " << (a==b) << endl;
    cout << "a != b = " << (a!=b) << endl;
}#include <iostream>
using namespace std;

int main () {
    int a;
    int b;

    cout << "masukan angka: ";
    cin >> a;
    cout << "masukan angka: ";
    cin >> b;

    //operator aritmatika
    cout << "a + b = " << (a+b) << endl;
    cout << "a - b = " << (a-b) << endl;
    cout << "a * b = " << (a*b) << endl;
    cout << "a / b = " << (a/b) << endl;
    cout << "a % b = " << (a%b) << endl;

    //operator logika
    cout << "a < b = " << (a<b) << endl;
    cout << "a > b = " << (a>b) << endl;
    cout << "a <= b = " << (a<=b) << endl;
    cout << "a >= b = " << (a>=b) << endl;
    cout << "a == b = " << (a==b) << endl;
    cout << "a != b = " << (a!=b) << endl;
}

Kode di atas digunakan untuk menerima dua input bilangan bulat dari pengguna, lalu menampilkan hasil operasi
aritmatika (penjumlahan, pengurangan, perkalian, pembagian, dan sisa bagi) serta hasil perbandingan logika
(lebih kecil, lebih besar, sama dengan, dan tidak sama dengan) antara kedua bilangan tersebut menggunakan
fungsi cout untuk mencetak hasil ke layar.
```
Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function cout untuk mengeksekusi nya.

## Unguided 

### 1. [Buatlah program yang menerima input-an dua buah bilangan betipe float,]

```C++
#include <iostream>
using namespace std;

int main() {
    float a, b;

    cout << "Masukkan bilangan pertama: ";
    cin >> a;
    cout << "Masukkan bilangan kedua: ";
    cin >> b;

    cout << "\nHasil Penjumlahan: " << a + b << endl;
    cout << "Hasil Pengurangan: " << a - b << endl;
    cout << "Hasil Perkalian: " << a * b << endl;

    if (b != 0)
        cout << "Hasil Pembagian: " << a / b << endl;
    else
    return 0;
}

```
#### Output:
<img width="1476" height="340" alt="Image" src="https://github.com/user-attachments/assets/821ee03f-d068-40bb-89a5-6bc4b561edfc" />
Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function cout untuk mengeksekusi nya.

#### Full code Screenshot:
<img width="1485" height="940" alt="Image" src="https://github.com/user-attachments/assets/0e60e190-6e0c-49ae-899b-fe1e57c46008" />
### 2. [Buatlah sebuah program yang menerima masukan angka dan mengeluarkan output nilai
<img width="1488" height="919" alt="Image" src="https://github.com/user-attachments/assets/690e7092-ea2b-491b-921d-f3785cc4e468" />
### Output
<img width="1283" height="192" alt="Image" src="https://github.com/user-attachments/assets/8be7350a-b254-4575-9d03-88461cad712b" />
### Fullscreenshot
<img width="1487" height="932" alt="Image" src="https://github.com/user-attachments/assets/3d279e70-8006-41fa-9530-3b4d208fef61" />
### 3. [Membuat segitiga terbalik ]

#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Masukkan angka: ";
    cin >> n;

    for (int i = n; i >= 1; i--) {
        for (int s = n; s > i; s--) {
            cout << "  "; 
        }
        for (int j = i; j >= 1; j--) {
            cout << j << " ";
        }
        cout << "* ";
        for (int j = 1; j <= i; j++) {
            cout << j << " ";
        }
        cout << endl;
    }
    for (int s = 0; s < n; s++) {
        cout << "  "; 
    }
    cout << "*\n";

    return 0;
}

### Output
<img width="1485" height="218" alt="Image" src="https://github.com/user-attachments/assets/169fd6ae-2e64-4b8f-88d6-0f1650bf3634" />

### Full screenshot
<img width="1473" height="972" alt="Image" src="https://github.com/user-attachments/assets/f8e6d408-cdb5-4738-8bff-b81201493ed8" />
## Kesimpulan
Dapat mengetahui codingan input output tentang modul ini

## Referensi
ARIAPURI, Narlidya; PRASETYO, Andy. Efektivitas Aplikasi Kasir Menggunakan Code Blocks Berbasis C++. Teknik Informatika Politeknik Purbaya, 2018.
