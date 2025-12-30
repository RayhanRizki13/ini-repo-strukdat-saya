# <h1 align="center">GRAPH<h1>
<p align="center">Rayhan Rizki Putra</p>

## Dasar Teori
Graph merupakan himpunan tidak kosong dari node (vertec) dan garis penghubung (edge). Contoh sederhana tentang graph, yaitu antara Tempat Kost Anda dengan Common Lab. Tempat Kost Anda dan Common Lab merupakan node (vertec). Jalan yang menghubungkan tempat Kost dan Common Lab merupakan garis penghubung antara keduanya (edge)
## Guided 

### 1. [GRAPH]
**[GRAP.h]**
```C++
#ifndef GRAPH_H_INCLUDE
#define GRAPH_H_INCLUDE
typedefintinfoGraph;
typedefstruct ElmNode*adrNode;
typedefstruct ElmEdge*adrEdge;

structElmNode{
    infoGraph info;
    intVisited;
    intPred;
    adrEdgefirstEdge;
    adrNode Next;
};
    structElmEdge{
    adrNode Node;
    adrEdge Next;
};

struct Graph {
    adrNode First;
};

adrNode AllocateNode(infoGraphX);
adrEdgeAllocateEdge(adrNodeN);
void CreateGraph(Graph &G);
void InsertNode(Graph &G,infoGraphX);
void DeleteNode(Graph &G,infoGraphX);
void ConnectNode(adrNodeN1,adrNode N2);
void DisconnectNode (adrNodeN1, adrNodeN2);
adrNodeFindNode(Graph G,infoGraphX);
adrEdgeFindEdge(adrNodeN,adrNodeNFind);
void PrintInfoGraph (Graph G);
void PrintTopologicalSort(Graph G);

#endif

#ifndef GRAPH_H_INCLUDE
#define GRAPH_H_INCLUDE

typedefintinfoGraph;
typedefstruct ElmNode*adrNode;
typedefstruct ElmEdge*adrEdge;

structElmNode{
    infoGraph info;
    intVisited;
    adrEdgefirstEdge;
    adrNode Next;
};

struct ElmEdge{
    adrNode Node;
    adrEdge Next;
};
struct Graph {
    adrNode First;
};

//Adds Node
ElmNode addNode(infoGrapha,intb, adrEdgec,adrNoded){
    ElmNodenewNode;
    newNode.Info= a;
    newNode.Visited=b ;
    newNode.firstEdge= c;
    newNode.Next = d;
returnnewNode;
}
//Addsanedgetoa graph
void addEdge(ElmNodenewNode){
    ElmEdgenewEdge;
    newEdge.Node = newNode.Next;
    newEdge.Next = newNode.firstEdge;
}
```

## Unguided 

### 1. [Soal]
**[graph.h]**
```C++
#ifndef GRAPH_ALT_H
#define GRAPH_ALT_H

#include <iostream>
using namespace std;

typedef char DataNode;
typedef struct Vertex *PtrVertex;
typedef struct Edge *PtrEdge;

struct Vertex {
    DataNode label;
    bool isVisited;
    PtrEdge edgeList;
    PtrVertex nextVertex;
};

struct Edge {
    PtrVertex target;
    PtrEdge nextEdge;
};

struct Graph {
    PtrVertex head;
};

void initGraph(Graph &G);
PtrVertex addVertex(Graph &G, DataNode x);
void addEdge(PtrVertex V1, PtrVertex V2);
void showGraph(Graph G);

void clearVisited(Graph &G);
void DFS(Graph G, PtrVertex start);
void BFS(Graph G, PtrVertex start);

#endif

```

**[graph.cpp]**
```C++
#include "graph.h"
#include <queue>

void initGraph(Graph &G) {
    G.head = NULL;
}

PtrVertex addVertex(Graph &G, DataNode x) {
    PtrVertex V = new Vertex;
    V->label = x;
    V->isVisited = false;
    V->edgeList = NULL;
    V->nextVertex = G.head;
    G.head = V;
    return V;
}

void addEdge(PtrVertex V1, PtrVertex V2) {
    PtrEdge E1 = new Edge;
    E1->target = V2;
    E1->nextEdge = V1->edgeList;
    V1->edgeList = E1;

    PtrEdge E2 = new Edge;
    E2->target = V1;
    E2->nextEdge = V2->edgeList;
    V2->edgeList = E2;
}

void showGraph(Graph G) {
    PtrVertex V = G.head;
    while (V != NULL) {
        cout << V->label << " -> ";
        PtrEdge E = V->edgeList;
        while (E != NULL) {
            cout << E->target->label << " ";
            E = E->nextEdge;
        }
        cout << endl;
        V = V->nextVertex;
    }
}

void clearVisited(Graph &G) {
    PtrVertex V = G.head;
    while (V != NULL) {
        V->isVisited = false;
        V = V->nextVertex;
    }
}

void DFS(Graph G, PtrVertex start) {
    if (start == NULL || start->isVisited) return;

    cout << start->label << " ";
    start->isVisited = true;

    PtrEdge E = start->edgeList;
    while (E != NULL) {
        DFS(G, E->target);
        E = E->nextEdge;
    }
}

void BFS(Graph G, PtrVertex start) {
    queue<PtrVertex> Q;
    start->isVisited = true;
    Q.push(start);

    while (!Q.empty()) {
        PtrVertex V = Q.front();
        Q.pop();
        cout << V->label << " ";

        PtrEdge E = V->edgeList;
        while (E != NULL) {
            if (!E->target->isVisited) {
                E->target->isVisited = true;
                Q.push(E->target);
            }
            E = E->nextEdge;
        }
    }
}

```

**[main.cpp]**
```C++
#include "graph.h"

int main() {
    Graph G;
    initGraph(G);

    PtrVertex A = addVertex(G, 'A');
    PtrVertex B = addVertex(G, 'B');
    PtrVertex C = addVertex(G, 'C');
    PtrVertex D = addVertex(G, 'D');
    PtrVertex E = addVertex(G, 'E');
    PtrVertex F = addVertex(G, 'F');
    PtrVertex G1 = addVertex(G, 'G');
    PtrVertex H = addVertex(G, 'H');

    addEdge(A, B);
    addEdge(A, C);
    addEdge(B, D);
    addEdge(B, E);
    addEdge(C, F);
    addEdge(C, G1);
    addEdge(D, H);
    addEdge(E, H);
    addEdge(F, H);
    addEdge(G1, H);

    showGraph(G);

    cout << "\nDFS dari A: ";
    clearVisited(G);
    DFS(G, A);

    cout << "\n\nBFS dari A: ";
    clearVisited(G);
    BFS(G, A);

    return 0;
}

```
#### Output:
<img width="332" height="186" alt="image" src="https://github.com/user-attachments/assets/a78f2e07-81f7-4e5d-a9f7-2400708ccad0" />

Program ini bertujuan untuk memahami ADT Graph tidak berarah dalam merepresentasikan hubungan antar simpul menggunakan adjacency list. Operasi penambahan simpul, penghubungan edge, serta penelusuran DFS dan BFS menunjukkan bagaimana simpul-simpul saling terhubung melalui pointer. Penggunaan atribut visited membantu mencegah kunjungan berulang sehingga proses penelusuran berjalan lebih efisien dan teratur.

#### Full code Screenshot:


graph.h
<img width="336" height="507" alt="image" src="https://github.com/user-attachments/assets/9f051e2c-6610-41e5-b1d5-59e09f650bf8" />

graph.cpp
<img width="321" height="959" alt="image" src="https://github.com/user-attachments/assets/e96cc837-34fb-497d-9987-59c02449bb49" />

main.cpp
<img width="254" height="450" alt="image" src="https://github.com/user-attachments/assets/b1c18ee5-7222-4359-ae7a-c81170b29436" />

## Kesimpulan
Program ini dibuat untuk mengimplementasikan struktur data Graph tak berarah (undirected graph) menggunakan bahasa pemrograman C++. Graph direpresentasikan dalam bentuk adjacency list, di mana setiap simpul (vertex) memiliki daftar sisi (edge) yang terhubung dengannya.
## Referensi
GeeksforGeeks. (n.d.). Graph data structure.


