

# **Modul 14 — GRAPH**

## **🎯 Tujuan Praktikum**

1. Memahami konsep dasar graph.
2. Mengimplementasikan struktur graph menggunakan pendekatan dinamis (multilist) dengan Python.

---

# **14.1 Pengertian Graph**

**Graph** adalah himpunan tidak kosong berisi **node (vertex)** dan **edge** yang menghubungkan node-node tersebut.

Contoh sederhana:

* Tempat Kost → Node
* Common Lab → Node
* Jalan yang menghubungkan keduanya → Edge

Dalam Python, graph direpresentasikan menggunakan **linked list** (multilist), adjacency list, atau adjacency matrix.

---

# **14.2 Jenis-Jenis Graph**

## **14.2.1 Directed Graph (Graph Berarah)**

Pada **graph berarah**, setiap edge memiliki **arah** tertentu.

Contoh:

```
A → B → C
```

Pada graph berarah:

* Jika terdapat edge A → B, **belum tentu** ada edge B → A.
* Representasi dinamis yang umum dipakai: **multilist / adjacency list**.

---

## **A. Representasi Graph (Multilist / Adjacency List)**

Dalam materi asli, representasi menggunakan pointer dan dynamic linked list:

```c
struct ElmNode { info, visited, pred, firstEdge, next };
struct ElmEdge { Node, next };
```

Dalam Python kita meniru konsep tersebut:

### **Implementasi Node dan Edge (Multilist versi Python)**

```python
class Edge:
    def __init__(self, node):
        self.node = node
        self.next = None


class Node:
    def __init__(self, info):
        self.info = info
        self.visited = False
        self.pred = 0               # jumlah predecessor
        self.first_edge = None
        self.next = None            # pointer ke node berikutnya (multilist)
```

### **Struktur Graph**

```python
class Graph:
    def __init__(self):
        self.first = None
```

---

# **14.2.1 — Topological Sort**

## **a. Pengertian**

Topological Sort adalah proses mengubah **urutan partial** menjadi **urutan linear** dengan syarat:

Jika X < Y → X harus muncul sebelum Y dalam hasil.

Contoh kasus sehari-hari:

1. **Mata kuliah** dengan prasyarat.
2. **Pekerjaan proyek** yang memiliki urutan.
3. **Urutan pembuatan tabel database** yang saling mereferensi.

Contoh partial order:

```
1<2  2<4  4<6  2<10  4<8
6<3  1<3  3<5  5<8
7<5  7<9  9<4  9<10
```

Hasil topological sort **bukan satu-satunya** — banyak kemungkinan urutan valid.

---

## **b. Representasi Topological Sort (Python Version)**

Kita akan memakai representasi adjacency list multilist seperti materi asli.

---

# **🔧 Implementasi Graph Berarah + Topological Sort (Versi Python)**

## **1. Menambah Node**

```python
def insert_node(g, info):
    new_node = Node(info)

    if g.first is None:
        g.first = new_node
    else:
        p = g.first
        while p.next:
            p = p.next
        p.next = new_node
    return new_node
```

## **2. Menghubungkan Node (Directed Edge X → Y)**

```python
def connect(n1, n2):
    new_edge = Edge(n2)
    new_edge.next = n1.first_edge
    n1.first_edge = new_edge

    # update jumlah predecessor untuk topological sort
    n2.pred += 1
```

## **3. Mencari Node**

```python
def find_node(g, info):
    p = g.first
    while p:
        if p.info == info:
            return p
        p = p.next
    return None
```

---

# **4. Topological Sort**

Mengikuti algoritma asli:

* Pilih node dengan predecessor = 0
* Masukkan ke hasil
* Kurangi predecessor successor
* Hapus dari graph
* Ulangi sampai habis

### **Implementasi Python**

```python
def topological_sort(g):
    result = []

    # copy pointer graph
    nodes = []
    p = g.first
    while p:
        nodes.append(p)
        p = p.next

    while nodes:
        # cari node tanpa predecessor
        zero_pred = None
        for n in nodes:
            if n.pred == 0:
                zero_pred = n
                break

        if zero_pred is None:
            raise Exception("Graph memiliki siklus. Topological sort gagal.")

        result.append(zero_pred.info)

        # kurangi predecessor dari successor
        e = zero_pred.first_edge
        while e:
            e.node.pred -= 1
            e = e.next

        # hapus node itu dari list
        nodes.remove(zero_pred)

    return result
```

---

# **14.2.2 Undirected Graph (Graph Tidak Berarah)**

Pada graph tidak berarah:

* Jika A terhubung ke B, maka B otomatis terhubung ke A.

Contoh:

```
A — B — C
```

Representasi menggunakan adjacency list juga.

---

# **14.2.2 — Representasi Undirected Graph dengan Python**

```python
def connect_undirected(n1, n2):
    # n1 → n2
    e1 = Edge(n2)
    e1.next = n1.first_edge
    n1.first_edge = e1

    # n2 → n1
    e2 = Edge(n1)
    e2.next = n2.first_edge
    n2.first_edge = e2
```

---

# **14.3 Penelusuran Graph (Traversal)**

Traversal penting untuk:

* Menentukan ketetanggaan
* Mencari jalur
* Mencari shortest path
* Mengubah graph → tree

---

# **A. BFS (Breadth First Search)**

Urutan kunjungan:

1. Depth 0
2. Depth 1
3. Depth 2
   ... dan seterusnya

### **Implementasi BFS**

```python
from collections import deque

def bfs(start):
    q = deque()
    q.append(start)
    start.visited = True

    while q:
        x = q.popleft()
        print(x.info, end=" ")

        e = x.first_edge
        while e:
            if not e.node.visited:
                e.node.visited = True
                q.append(e.node)
            e = e.next
```

---

# **B. DFS (Depth First Search)**

DFS menggunakan **stack** atau **rekursi**.

### **Implementasi DFS (rekursif)**

```python
def dfs(node):
    node.visited = True
    print(node.info, end=" ")

    e = node.first_edge
    while e:
        if not e.node.visited:
            dfs(e.node)
        e = e.next
```

---

# **Reset Status Visited**

```python
def reset_visited(g):
    p = g.first
    while p:
        p.visited = False
        p = p.next
```

---

# **Contoh Penggunaan**

```python
g = Graph()

# buat node
A = insert_node(g, "A")
B = insert_node(g, "B")
C = insert_node(g, "C")
D = insert_node(g, "D")

# graph berarah
connect(A, B)
connect(A, C)
connect(B, D)
connect(C, D)

# topological sort
print("Topo Sort:", topological_sort(g))
```

