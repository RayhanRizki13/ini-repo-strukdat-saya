# <h1 align="center">STACK</h1>
<p align="center">Rayhan Rizki Putra</p>

## Dasar Teori

Stack adalah struktur data yang bekerja seperti tumpukan. Elemen yang terakhir dimasukkan akan menjadi elemen pertama yang diambil. Konsep ini disebut LIFO (Last In First Out).
    
## Guided 

### 1. [stack]
**stack.h**
```C++
#ifndef STACK_TABLE
#define STACK_TABLE

#include <iostream>
using namespace std;

//ubah kapasitas sesuai kebutuhan
const int MAX = 10;

struct stackTable{
    int data[MAX];
    int top; // -1 = kosong

};

bool isEmpty(stackTable s);
bool isFull(stackTable s);
void createStack(stackTable &s);

void push(stackTable &s, int angka);
void pop(stackTable &s);
void update(stackTable &s, int posisi);
void view(stackTable s);
void searchData(stackTable s, int data);

#endif
```
**stak.cpp**
```C++
#include "stack.h"
#include <iostream>

using namespace std;

bool isEmpty(stackTable s) {
    return s.top == -1;
}

bool isFull(stackTable s){
    return s.top == MAX -1;
}

void createStack(stackTable &s) {
    s.top = -1;
}

void push(stackTable &s, int angka){
    if(isFull(s)){
        cout << "Stack Penuh!" << endl;
    } else {
        s.top++;
        s.data[s.top] = angka;
        cout << "Data " << angka << " berhasil ditambahkan kedalam stack!" << endl;
    }
}

void pop(stackTable &s){
    if(isEmpty(s)){
        cout << "Stack kosong!" << endl;
    } else {
        int val = s.data[s.top];
        s.top--;
        cout << "Data " << val << " Berhasil dihapus dari stack!" << endl;
    }
}

void update(stackTable &s, int posisi){
    if(isEmpty(s)){
        cout << "Stack kosong!" << endl;
        return;
    }
    if(posisi <= 0){
        cout << "Posisi tidak valid!" << endl;
        return;
    }

    //index = top - (posisi -1)
    int idx = s.top - (posisi -1);
    if(idx < 0 || idx > s.top){
        cout << "Posisi " << posisi << " Tidak valid!" << endl;
        return;
    }

    cout << "Update data posisi ke-" << posisi << endl;
    cout << "Masukkan angka: ";
    cin >> s.data[idx];
    cout << "Data berhasil diupdate!" << endl;
    cout << endl;
}

void view(stackTable s){
    if(isEmpty(s)){
        cout << "Stack Kosong!" << endl;
    } else {
        for(int i = s.top; i >= 0; --i){
            cout << s.data[i] << " ";
        }
    }
    cout << endl;
}

void searchData(stackTable s, int data){
    if(isEmpty(s)){
        cout << "Stack Kosong!" << endl;
        return;
    }
    cout << "Mencari data" << data << "..." << endl;
    int posisi = 1;
    bool found = false;

    for(int i = s.top; i >= 0; --i){
        if(s.data[i] == data){
            cout << "Data " << data << " ditemukan pada posisi ke-" << posisi << endl;
            cout << endl;
            found = true;
            break;
        }
        posisi++;
    }

    if(!found){
        cout << "Data " << data << " tidak ditemukan didalam stack!" << endl;
        cout << endl;
    }
}
```
**main.cpp**
```C++
#include "stack.h"
#include <iostream>

using namespace std;

int main(){
    stackTable s;
    createStack(s);

    push(s, 1);
    push(s, 2);
    push(s, 3);
    push(s, 4);
    push(s, 5);
    cout << endl;

    cout << "--- Stack setelah push ---" << endl;
    view(s);
    cout << endl;

    pop(s);
    pop(s);
    cout << endl;

    cout << "--- Stack setelah pop 2 kali ---" << endl;
    view(s);
    cout << endl;

    //Posisi dihitung dari TOP(1-based)
    update(s, 2);
    update(s, 1);
    update(s, 4);
    cout << endl;

    cout << "--- Stack setelah update ---" << endl;
    view(s);
    cout << endl;

    searchData(s, 4);
    searchData(s, 9);

    return 0;
}
```
Program ini mengimplementasikan struktur data stack menggunakan array dengan operasi dasar push, pop, dan fitur tambahan seperti update dan search data.

## Unguided 

### 1. [Soal]
**stack.h**
```C++
#ifndef STACK_H
#define STACK_H

const int MAX = 20;

struct Stack {
    int data[MAX];
    int top;
};

void createStack(Stack &S);
void push(Stack &S, int x);
int pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);
void getInputStream(Stack &S);

#endif
```
**stack.cpp**
```C++
#include <iostream>
#include "stack.h"
using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, int x) {
    if (S.top < MAX - 1) {
        S.top++;
        S.data[S.top] = x;
    }
}

int pop(Stack &S) {
    if (S.top >= 0) {
        int value = S.data[S.top];
        S.top--;
        return value;
    }
    return -1;
}

void printInfo(Stack S) {
    cout << "[TOP] ";
    for (int i = S.top; i >= 0; i--) {
        cout << S.data[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    createStack(temp);

    while (S.top >= 0) {
        push(temp, pop(S));
    }

    S = temp;
}

void getInputStream(Stack &S) {
    string input = "4729601"; 
    cout << input << endl;

    for (char ch : input) {
        push(S, ch - '0');
    }
}
```
**main.cpp**
```C++
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    cout << "Hello Word" << endl;  

    Stack S;
    createStack(S);

    getInputStream(S);  
    printInfo(S);

    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);

    return 0;
}
```
#### Output:
<img width="367" height="141" alt="image" src="https://github.com/user-attachments/assets/ffd7e1f3-21df-43b2-9efb-9a863a73decc" />



Program membuat sebuah stack, otomatis mengisi stack dengan angka 4729601, lalu menampilkan isi stack dari atas ke bawah. Setelah itu, program membalik urutan stack menggunakan stack sementara, dan menampilkan hasilnya.

#### Full code Screenshot:


stack.h
<img width="300" height="319" alt="image" src="https://github.com/user-attachments/assets/7cd93be4-ba1c-4801-a0e5-e4db574fc2b6" />


stack.cpp
<img width="434" height="840" alt="image" src="https://github.com/user-attachments/assets/8864993f-cf44-4c48-84a2-5efc81bf6e19" />


main.cpp
<img width="323" height="356" alt="image" src="https://github.com/user-attachments/assets/f5cac4ce-2368-4be1-9bc0-3f7276552039" />

## Kesimpulan
Cara kerja stack yang memakai prinsip LIFO, yaitu data yang masuk terakhir akan keluar duluan. Saya mencoba operasi dasar seperti push dan pop, lalu membuat fungsi untuk menampilkan isi stack dan membalik urutannya. Hasil percobaan menunjukkan bahwa stack bekerja sesuai logikanya dan proses pembalikan data berhasil. Praktikum ini membantu saya lebih paham cara menggunakan stack dalam program.

## Referensi
Yulyanto, A. (2012). Aplikasi Simulasi Pembelajaran Struktur Data Materi Stack (Doctoral dissertation, Universitas Mercu Buana).

