# Belajar Queue di Python

## Deskripsi Modul

Modul ini dirancang untuk membantu peserta memahami konsep **Queue (Antrian)** dalam Python, mulai dari operasi dasar hingga implementasi menggunakan berbagai metode dan varian Queue. Peserta akan belajar secara praktis melalui contoh kode dan latihan aplikasi nyata.

---

## Pendahuluan

**Queue** adalah struktur data yang bekerja dengan prinsip **FIFO (First In First Out)**, artinya elemen yang pertama kali masuk adalah elemen yang pertama kali keluar.

### Contoh Dunia Nyata:

* Antrian kasir di supermarket.
* Antrian print job di printer.
* Task scheduling pada sistem operasi.

---

## Tujuan Pembelajaran

Setelah mengikuti modul ini, peserta akan:

1. Memahami konsep FIFO.
2. Menguasai operasi dasar queue: enqueue, dequeue, peek, isEmpty, isFull, size.
3. Mampu mengimplementasikan queue menggunakan berbagai metode di Python.
4. Mengenal varian queue khusus: Circular Queue, Priority Queue, Deque.
5. Mengaplikasikan queue dalam simulasi dunia nyata.

---

![Queue](https://media.geeksforgeeks.org/wp-content/uploads/20220816162225/Queue.png)

## Operasi Dasar Queue

### 1. Enqueue

Menambahkan elemen ke belakang queue.

```python
queue = []
queue.append(10)  # Menambahkan 10
queue.append(20)  # Menambahkan 20
print(queue)  # Output: [10, 20]
```

### 2. Dequeue

Menghapus elemen dari depan queue.

```python
item = queue.pop(0)  # Menghapus 10
print(item)  # Output: 10
print(queue)  # Output: [20]
```

### 3. Peek / Front

Melihat elemen di depan tanpa menghapusnya.

```python
front = queue[0]
print(front)  # Output: 20
```

### 4. isEmpty

Memeriksa apakah queue kosong.

```python
is_empty = len(queue) == 0
print(is_empty)  # Output: False
```

### 5. isFull (opsional)

Memeriksa apakah queue penuh (jika kapasitas terbatas).

```python
MAX_SIZE = 5
is_full = len(queue) == MAX_SIZE
print(is_full)  # Output: False
```

### 6. Size / Length

Mengetahui jumlah elemen dalam queue.

```python
size = len(queue)
print(size)  # Output: 1
```

---

## Implementasi Queue

### 1. Menggunakan list

```python
queue = []
queue.append(1)
queue.append(2)
queue.pop(0)
```

**Kelebihan:** sederhana.
**Kekurangan:** dequeue lambat karena shifting elemen.

### 2. Menggunakan collections.deque

```python
from collections import deque
queue = deque()
queue.append(1)
queue.append(2)
queue.popleft()
```

**Kelebihan:** enqueue dan dequeue cepat (O(1)).
**Kekurangan:** kurang fleksibel dibanding list untuk operasi indexing.

### 3. Menggunakan queue.Queue

```python
from queue import Queue
queue = Queue(maxsize=5)
queue.put(1)
queue.put(2)
queue.get()
```

**Kelebihan:** thread-safe.
**Kekurangan:** lebih kompleks untuk implementasi sederhana.

### 4. Menggunakan linked list manual

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class QueueLinkedList:
    def __init__(self):
        self.front = self.rear = None

    def enqueue(self, data):
        node = Node(data)
        if self.rear is None:
            self.front = self.rear = node
            return
        self.rear.next = node
        self.rear = node

    def dequeue(self):
        if self.front is None:
            return None
        temp = self.front
        self.front = self.front.next
        if self.front is None:
            self.rear = None
        return temp.data
```

**Kelebihan:** fleksibel, tidak ada batas kapasitas.
**Kekurangan:** lebih kompleks dibanding list/deque.

---

## Varian Queue / Queue Khusus

### 1. Circular Queue

Queue yang menghubungkan akhir ke awal untuk efisiensi.

```python
# Implementasi sederhana circular queue
```

### 2. Priority Queue

Queue di mana elemen dengan prioritas lebih tinggi keluar lebih dulu.

```python
import queue
pq = queue.PriorityQueue()
pq.put((2, 'task2'))
pq.put((1, 'task1'))
print(pq.get())  # Output: (1, 'task1')
```

### 3. Double-Ended Queue (Deque)

Queue yang bisa menambahkan/menghapus di kedua ujung.

```python
from collections import deque
dq = deque([1,2,3])
dq.appendleft(0)
dq.pop()
```

---

## Kompleksitas Operasi

| Implementasi | Enqueue | Dequeue | Peek |
| ------------ | ------- | ------- | ---- |
| List         | O(1)    | O(n)    | O(1) |
| deque        | O(1)    | O(1)    | O(1) |
| queue.Queue  | O(1)    | O(1)    | O(1) |
| Linked List  | O(1)    | O(1)    | O(1) |

---

## Queue Code

```python
# Implementasi Lengkap Fungsi Queue menggunakan list
class QueueList:
    def __init__(self, max_size=None):
        self.queue = []
        self.max_size = max_size

    def enqueue(self, item):
        if self.max_size and len(self.queue) >= self.max_size:
            print("Queue penuh!")
            return
        self.queue.append(item)
        print(f"{item} ditambahkan ke queue")

    def dequeue(self):
        if self.is_empty():
            print("Queue kosong!")
            return None
        item = self.queue.pop(0)
        print(f"{item} dikeluarkan dari queue")
        return item

    def peek(self):
        if self.is_empty():
            print("Queue kosong!")
            return None
        return self.queue[0]

    def is_empty(self):
        return len(self.queue) == 0

    def is_full(self):
        if self.max_size:
            return len(self.queue) >= self.max_size
        return False

    def size(self):
        return len(self.queue)

# Contoh Penggunaan
q = QueueList(max_size=5)
q.enqueue(10)
q.enqueue(20)
q.enqueue(30)
print(f"Elemen depan queue: {q.peek()}")
q.dequeue()
q.dequeue()
print(f"Apakah queue kosong? {q.is_empty()}")
print(f"Ukuran queue: {q.size()}")

```


## Contoh Aplikasi Queue

### 1. Simulasi Antrian Kasir

```python
from collections import deque
kasir = deque()
kasir.append('Alice')
kasir.append('Bob')
print(kasir.popleft())  # Output: Alice
```

### 2. Print Job Queue

```python
print_queue = deque(['doc1', 'doc2'])
print(print_queue.popleft())
```

### 3. BFS pada Graph

```python
from collections import deque
def bfs(graph, start):
    visited = set()
    queue = deque([start])
    while queue:
        vertex = queue.popleft()
        if vertex not in visited:
            print(vertex)
            visited.add(vertex)
            queue.extend(set(graph[vertex]) - visited)
```

### 4. Task Scheduling Sederhana

```python
tasks = deque()
tasks.append('Task1')
tasks.append('Task2')
while tasks:
    current = tasks.popleft()
    print(f'Processing {current}')
```

---

## Referensi / Bacaan Tambahan

* [Python Official Documentation: queue](https://docs.python.org/3/library/queue.html)
* [Python Collections Module: deque](https://docs.python.org/3/library/collections.html#collections.deque)
* Buku "Data Structures and Algorithms in Python" oleh Michael T. Goodrich
