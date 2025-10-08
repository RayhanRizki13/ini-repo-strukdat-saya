# <h1 align="center">Laporan Praktikum Modul Pengenalan Bahasa C++ (1)</h1>
<p align="center">Arvinanto Bahtiar</p>

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

Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function cout untuk mengeksekusi nya.

#### Full code Screenshot:


## Kesimpulan
Ringkasan dan interpretasi pandangan kalia dari hasil praktikum dan pembelajaran yang didapat[1].

## Referensi
[1] I. Holm, Narrator, and J. Fullerton-Smith, Producer, How to Build a Human [DVD]. London: BBC; 2002.
