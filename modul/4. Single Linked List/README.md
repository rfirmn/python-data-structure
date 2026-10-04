# Struktur Data - Single Linked List (Python)

## Pendahuluan
Single Linked List adalah struktur data linier yang terdiri dari simpul (node) yang saling terhubung melalui referensi ke simpul berikutnya. Setiap simpul berisi data dan referensi ke simpul berikutnya, memungkinkan penyimpanan data secara dinamis tanpa batasan ukuran tetap.

![Single Linked List](https://github.com/user-attachments/assets/30f51dee-e4c5-48e1-8e43-1498c32c14fa)

### 1. Konsep Dasar Single Linked List
- **Definisi**: Kumpulan node yang disusun secara linier, di mana setiap node memiliki:
  - **Data**: Informasi yang disimpan (misalnya, bilangan bulat).
  - **Referensi/Next**: Referensi ke node berikutnya.
- **Ciri-ciri**:
  - Unidirectional (hanya dapat dilalui dari awal ke akhir).
  - Ukuran dinamis (bisa bertambah atau berkurang).
  - Memiliki referensi `head` (atau `first`) yang menunjuk ke node pertama.
- **Struktur Node**:
  ```python
  class Node:
      def __init__(self, data):
          self.info = data
          self.next = None
  ```

### 2. Deklarasi Tipe Data
Berikut adalah implementasi struktur data untuk Single Linked List dalam Python:

- **Kelas Node**: Merepresentasikan simpul dengan data dan referensi ke simpul berikutnya.
- **Kelas List**: Merepresentasikan list dengan referensi ke node pertama (`first`).
- **Implementasi di `list.py`**:
  ```python
  class Node:
      def __init__(self, data):
          self.info = data
          self.next = None
  ```
  ### Konsep Dasar: class Node
  Komputer tidak memiliki tipe data bawaan bernama "Node". Oleh karena itu, kita membuat class baru bernama Node untuk memberi tahu Python:
  > *"Setiap kali saya membuat satu elemen Linked List, elemen tersebut wajib memiliki dua buah variabel internal di dalamnya."*
  
  Kasus eksekusi `n1 = Node(10)`:
  - <small>Python mengalokasikan satu blok ruang memori baru.</small>
  - <small>Parameter data menerima nilai 10.</small>
  - <small>Variabel n1.info diisi dengan angka 10.</small>
  - <small>Variabel n1.next diisi dengan None.</small>

  
  ```python
  class List:
      def __init__(self):
          self.first = None
  ```

  
  ### Konsep Dasar: class List

  Kelas ini bertugas menyimpan akses pintu masuk utama dan menyediakan metode-metode manipulasi data (seperti insert, delete, dan search).
  
  > *"Jika hanya menulis first = None (tanpa self.), variabel first hanya dianggap sebagai variabel lokal sementara di dalam fungsi __init__. Begitu fungsi __init__ selesai dieksekusi, variabel first akan langsung dihapus dari memori RAM oleh Python!Dengan menulis self.first = None, variabel tersebut disimpan secara permanen di dalam objek List selama program berjalan."*
   
  Detail komponen `class List`:
  - <small><b>def __init__(self):</b> Dipanggil otomatis saat sebuah objek List baru dibuat (misalnya: `L = List()`).</small>
  - <small><b>self:</b> Memberi tahu Python bahwa variabel ini adalah milik internal dari objek List tertentu yang sedang dibuat.</small>
  - <small><b>self.first = None:</b> Menginisialisasi pointer utama dengan nilai `None` sebagai penanda awal bahwa list masih kosong.</small>


  ```python
      def createList(self):
          """Menginisialisasi list kosong."""
          self.first = None
  ```

  
    ### Konsep Dasar: createList(self)
    
    Fungsi ini bertugas untuk mengosongkan atau mereset LinkedList.
    
    > *"Mengubah `self.first` menjadi `None` artinya seluruh rangkaian node di belakangnya otomatis terlepas dan hilang dari list."*
    
    Detail eksekusi `createList()`:
    - <small><b>Panggilan Fungsi:</b> Dieksekusi melalui objek list yang ada (misalnya: `L.createList()`).</small>
    - <small><b>self.first = None:</b> Memutus akses ke node pertama sehingga list kembali menjadi kosong.</small>


   ```python
      def createElement(self, x):
          """Membuat node baru dengan data x."""
          return Node(x)
  ```
  ### Konsep Dasar: createElement(self, x)

  Fungsi ini bertugas membuat satu objek Node baru berbasis nilai x.
  
  Contoh Kasus: `P = L.createElement(10)`
  - <small><b>Input Data:</b> Parameter x menerima angka 10.</small>
  - <small><b>Pembuatan Objek:</b> Python mengeksekusi `Node(10)` dan menyiapkan ruang memori baru.</small>
  - <small><b>Pengisian Atribut:</b> Objek baru memiliki `info = 10` dan `next = None` (belum terhubung ke list).</small>
  - <small><b>Pengembalian Objek:</b> Objek node diserahkan keluar dan disimpan di variabel P.</small>
  
  ```python
      def insertFirst(self, P):
          """Menyisipkan node P di awal list."""
          if P:
              P.next = self.first
              self.first = P
  ```

  ### Konsep Dasar: insertFirst(self, P)

  Fungsi ini bertugas menyisipkan node P ke posisi paling depan (awal) dari list.
  
  Contoh Kasus: Rantai awal `[20] -> None`, lalu dijalankan `L.insertFirst(P)` dengan `P = Node(10)`
  
  - <small><b>Kondisi Awal:</b> `self.first` menunjuk ke Node(20).</small>
  - <small><b>Langkah 1 (P.next = self.first):</b> Pointer `P.next` dihubungkan ke Node(20). Rantai sementara menjadi `[10] -> [20] -> None`.</small>
  - <small><b>Langkah 2 (self.first = P):</b> Pointer utama `self.first` dialihkan menunjuk ke Node(10).</small>
  - <small><b>Kondisi Akhir:</b> List menjadi `self.first -> [10] -> [20] -> None`.</small>

  ```python
      def insertLast(self, P):
          """Menyisipkan node P di akhir list."""
          if P:
              if not self.first:
                  self.first = P
              else:
                  last = self.first
                  while last.next:
                      last = last.next
                  last.next = P
  ```
  ### Konsep Dasar: insertLast(self, P)

  Fungsi ini bertugas menyisipkan node P ke posisi paling belakang (ujung akhir) dari list.
  
  Contoh Kasus: Rantai awal `self.first -> [10] -> None`, lalu dijalankan `L.insertLast(P)` dengan `P = Node(20)`
  
  - <small><b>Kondisi Awal:</b> `self.first` menunjuk ke Node(10), dan `Node(10).next` bernilai `None`.</small>
  - <small><b>Pemeriksaan List:</b> Kondisi `if not self.first` bernilai False, kode masuk ke blok `else`.</small>
  - <small><b>Penelusuran (Looping):</b> Variable `last` menunjuk ke Node(10). Loop `while last.next` langsung berhenti karena `Node(10).next` adalah `None`.</small>
  - <small><b>Penyambungan (last.next = P):</b> Pointer `Node(10).next` diubah dari `None` menjadi menunjuk ke Node(20).</small>
  - <small><b>Kondisi Akhir:</b> List menjadi `self.first -> [10] -> [20] -> None`.</small>
  
  ```python
      def printList(self):
          """Menampilkan semua elemen dalam list."""
          if not self.first:
              print("List kosong")
          else:
              current = self.first
              while current:
                  print(current.info, end=" ")
                  current = current.next
              print()
  ```
  ### Konsep Dasar: printList(self)

  Fungsi ini bertugas memeriksa status list dan mencetak semua data (.info) secara berurutan ke layar.
  
  Contoh Kasus: Rantai awal `self.first -> [10] -> [20] -> None`, lalu dijalankan `L.printList()`
  
  - <small><b>Pemeriksaan List:</b> `self.first` ada (bukan None), kode mengeksekusi blok `else`.</small>
  - <small><b>Inisialisasi:</b> Variable `current` menunjuk ke Node(10).</small>
  - <small><b>Iterasi 1:</b> Mencetak `10 ` (dengan spasi). Pointer `current` bergeser ke Node(20).</small>
  - <small><b>Iterasi 2:</b> Mencetak `20 ` (dengan spasi). Pointer `current` bergeser ke `None`.</small>
  - <small><b>Penghentian:</b> Loop berhenti karena `current` bernilai `None`. `print()` dipanggil untuk pindah baris.</small>
  - <small><b>Hasil Output Layar:</b> `10 20 `</small>

  
  ```python
      def deleteFirst(self):
          """Menghapus node pertama dari list."""
          if self.first:
              P = self.first
              self.first = P.next
              return P
          return None
  ```
  ### Konsep Dasar: deleteFirst(self)

  Fungsi ini bertugas melepas elemen pertama dari list dan mengembalikannya.
  
  Contoh Kasus: Rantai awal `self.first -> [10] -> [20] -> None`, lalu dijalankan `deleted_node = L.deleteFirst()`
  
  - <small><b>Kondisi Awal:</b> `self.first` menunjuk ke Node(10), dan `Node(10).next` menunjuk ke Node(20).</small>
  - <small><b>Isolasi Node (P = self.first):</b> Variable `P` memegang objek Node(10).</small>
  - <small><b>Pergeseran Header (self.first = self.first.next):</b> Pointer utama `self.first` dialihkan langsung ke Node(20).</small>
  - <small><b>Pemutusan Rantai (P.next = None):</b> Pointer `P.next` diubah dari Node(20) menjadi `None`.</small>
  - <small><b>Kondisi Akhir:</b> List tersisa `self.first -> [20] -> None`, dan variabel `deleted_node` memegang `[10] -> None`.</small>


  ```python
      def deleteLast(self):
          """Menghapus node terakhir dari list."""
          if not self.first:
              return None
          if not self.first.next:
              P = self.first
              self.first = None
              return P
          current = self.first
          while current.next.next:
              current = current.next
          P = current.next
          current.next = None
          return P
  ```
  ### Konsep Dasar: deleteLast(self)
  
  Fungsi ini bertugas melepas elemen paling belakang (terakhir) dari list dan mengembalikannya.
  
  Contoh Kasus: Rantai awal `self.first -> [10] -> [20] -> [30] -> None`, lalu dijalankan `deleted_node = L.deleteLast()`
  
  - <small><b>Kondisi Awal:</b> Rantai terdiri dari 3 node. Pointer `self.first` menunjuk ke Node(10).</small>
  - <small><b>Penelusuran (Looping):</b> Variable `current` berjalan dari Node(10) dan berhenti di Node(20) karena `Node(20).next.next` bernilai `None`.</small>
  - <small><b>Isolasi Node (P = current.next):</b> Variable `P` menyimpan objek Node(30).</small>
  - <small><b>Pemutusan Rantai (current.next = None):</b> Pointer `Node(20).next` diubah dari Node(30) menjadi `None`.</small>
  - <small><b>Kondisi Akhir:</b> List tersisa `self.first -> [10] -> [20] -> None`, dan variabel `deleted_node` memegang Node(30).</small>

  ```python
      def searchInfo(self, x):
          """Mencari node dengan data x."""
          current = self.first
          while current and current.info != x:
              current = current.next
          return current
  ```
    ### Konsep Dasar: searchInfo(self, x)
  
  Fungsi ini bertugas mencari dan mengembalikan objek Node yang isi data (.info) nilainya sama dengan x.
  
  Contoh Kasus: Rantai awal `self.first -> [10] -> [20] -> [30] -> None`, lalu dijalankan `result = L.searchInfo(20)`
  
  - <small><b>Inisialisasi:</b> Variable `current` menunjuk ke Node(10).</small>
  - <small><b>Iterasi 1:</b> `current.info` adalah 10 (10 != 20). Loop berlanjut, `current` bergeser menunjuk ke Node(20).</small>
  - <small><b>Iterasi 2:</b> `current.info` adalah 20 (20 != 20 bernilai False). Loop berhenti.</small>
  - <small><b>Pengembalian:</b> Fungsi mengembalikan objek Node(20) secara utuh ke variabel `result`.</small>

### 3. Operasi Dasar pada Single Linked List
Berikut adalah penjelasan operasi dasar yang diimplementasikan:

#### a. Membuat List Kosong (`createList`)
- **Fungsi**: Menginisialisasi list menjadi kosong.
- **Penjelasan**: Mengatur atribut `first` ke `None` untuk menandakan list kosong.
- **Contoh Penggunaan**:
  ```python
  L = List()
  L.createList()  # List sekarang kosong
  ```

#### b. Membuat Elemen Baru (`createElement`)
- **Fungsi**: Membuat node baru dengan data tertentu.
- **Penjelasan**: Mengembalikan objek `Node` dengan data `x` dan `next` diatur ke `None`.
- **Contoh Penggunaan**:
  ```python
  newNode = L.createElement(5)  # Membuat node dengan data 5
  ```

#### c. Menyisipkan Elemen di Awal (`insertFirst`)
- **Fungsi**: Menyisipkan node baru di awal list.
- **Penjelasan**: Menghubungkan node baru ke `first` dan mengatur `first` ke node baru.
- **Contoh Penggunaan**:
  ```python
  L = List()
  L.createList()
  P = L.createElement(10)
  L.insertFirst(P)  # List sekarang berisi: 10
  L.printList()  # Output: 10
  ```

#### d. Menyisipkan Elemen di Akhir (`insertLast`)
- **Fungsi**: Menyisipkan node baru di akhir list.
- **Penjelasan**: Jika list kosong, node menjadi `first`. Jika tidak, cari node terakhir dan sambungkan node baru.
- **Contoh Penggunaan**:
  ```python
  P = L.createElement(3)
  L.insertLast(P)  # List sekarang berisi: 10 3
  L.printList()  # Output: 10 3
  ```

#### e. Menampilkan List (`printList`)
- **Fungsi**: Menampilkan semua elemen dalam list.
- **Penjelasan**: Melintasi list dari `first` hingga akhir, mencetak setiap data. Jika list kosong, tampilkan pesan "List kosong".
- **Contoh Penggunaan**:
  ```python
  L.printList()  # Output: 10 3
  ```

### 4. Operasi Tambahan
Berikut adalah operasi tambahan untuk memperkaya fungsionalitas:

#### a. Menghapus Elemen Pertama (`deleteFirst`)
- **Fungsi**: Menghapus node pertama dari list dan mengembalikan node yang dihapus.
- **Penjelasan**: Mengatur `first` ke node berikutnya dan memutuskan hubungan node pertama.
- **Contoh Penggunaan**:
  ```python
  P = L.deleteFirst()
  if P:
      print(f"Elemen yang dihapus: {P.info}")
  L.printList()  # Output: 3
  ```

#### b. Menghapus Elemen Terakhir (`deleteLast`)
- **Fungsi**: Menghapus node terakhir dari list dan mengembalikan node yang dihapus.
- **Penjelasan**: Jika hanya ada satu node, hapus `first`. Jika tidak, cari node sebelum terakhir dan putuskan hubungan ke node terakhir.
- **Contoh Penggunaan**:
  ```python
  P = L.deleteLast()
  if P:
      print(f"Elemen yang dihapus: {P.info}")
  L.printList()  # Output: (kosong)
  ```

#### c. Mencari Elemen (`searchInfo`)
- **Fungsi**: Mencari node dengan data tertentu.
- **Penjelasan**: Melintasi list hingga menemukan node dengan data `x` atau mencapai akhir (`None`).
- **Contoh Penggunaan**:
  ```python
  found = L.searchInfo(4)
  if found:
      print(f"Data {found.info} ditemukan")
  else:
      print("Data tidak ditemukan")
  ```

### 5. Implementasi Lengkap
Berikut adalah file lengkap untuk implementasi Single Linked List dalam Python:

#### File: `main.py` (Contoh dengan 10 Digit NIM)
```python
from list import List

def main():
    L = List()
    L.createList()

    # Input 10 digit NIM
    nim = []
    print("Input NIM (Student ID) digit by digit:")
    for i in range(10):
        digit = int(input(f"Digit {i + 1}: "))
        nim.append(digit)
        L.insertLast(L.createElement(digit))  # Menyisipkan di akhir

    print("Isi list:", end=" ")
    L.printList()  # Output: digit NIM dalam urutan input

    # Contoh operasi tambahan
    print("Menghapus elemen pertama...")
    P = L.deleteFirst()
    if P:
        print(f"Elemen yang dihapus: {P.info}")
    print("Isi list:", end=" ")
    L.printList()

    print("Menghapus elemen terakhir...")
    P = L.deleteLast()
    if P:
        print(f"Elemen yang dihapus: {P.info}")
    print("Isi list:", end=" ")
    L.printList()

    print("Mencari digit 4...")
    found = L.searchInfo(4)
    if found:
        print(f"Data {found.info} ditemukan")
    else:
        print("Data 4 tidak ditemukan")

if __name__ == "__main__":
    main()
```
