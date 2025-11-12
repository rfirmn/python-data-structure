# Struktur Data - Double Linked List (Python)

## Pendahuluan
Double Linked List adalah struktur data linier yang terdiri dari simpul (node) yang saling terhubung melalui dua referensi: satu ke simpul berikutnya (*next*) dan satu ke simpul sebelumnya (*prev*). Struktur ini memungkinkan traversal dua arah, memberikan fleksibilitas lebih dibandingkan Single Linked List.

<img width="1492" height="202" alt="image" src="https://github.com/user-attachments/assets/930f2c2e-40f1-4fb9-8fd3-13840ee65f22" />

### 1. Konsep Dasar Double Linked List
- **Definisi**: Kumpulan node yang disusun secara linier, di mana setiap node memiliki:
  - **Data**: Informasi yang disimpan (misalnya, bilangan bulat).
  - **Next**: Referensi ke node berikutnya.
  - **Prev**: Referensi ke node sebelumnya.
- **Ciri-ciri**:
  - Bidirectional (dapat dilalui dari awal ke akhir atau sebaliknya).
  - Ukuran dinamis (bisa bertambah atau berkurang).
  - Memiliki referensi `head` (atau `first`) ke node pertama dan `tail` ke node terakhir.
- **Struktur Node**:
  ```python
  class Node:
      def __init__(self, data):
          self.info = data
          self.next = None
          self.prev = None
  ```

### 2. Deklarasi Tipe Data
Berikut adalah implementasi struktur data untuk Double Linked List dalam Python:

- **Kelas Node**: Merepresentasikan simpul dengan data, referensi ke node berikutnya (*next*), dan node sebelumnya (*prev*).
- **Kelas List**: Merepresentasikan list dengan referensi ke node pertama (`first`) dan node terakhir (`last`).
- **Implementasi di `list.py`**:
  ```python
  class Node:
      def __init__(self, data):
          self.info = data
          self.next = None
          self.prev = None

  class List:
      def __init__(self):
          self.first = None
          self.last = None

      def createList(self):
          """Menginisialisasi list kosong."""
          self.first = None
          self.last = None

      def createElement(self, x):
          """Membuat node baru dengan data x."""
          return Node(x)

      def insertFirst(self, P):
          """Menyisipkan node P di awal list."""
          if P:
              P.next = self.first
              P.prev = None
              if self.first:
                  self.first.prev = P
              else:
                  self.last = P
              self.first = P

      def insertLast(self, P):
          """Menyisipkan node P di akhir list."""
          if P:
              P.prev = self.last
              P.next = None
              if self.last:
                  self.last.next = P
              else:
                  self.first = P
              self.last = P

      def printList(self):
          """Menampilkan semua elemen dalam list dari depan ke belakang."""
          if not self.first:
              print("List kosong")
          else:
              current = self.first
              while current:
                  print(current.info, end=" ")
                  current = current.next
              print()

      def printListReverse(self):
          """Menampilkan semua elemen dalam list dari belakang ke depan."""
          if not self.last:
              print("List kosong")
          else:
              current = self.last
              while current:
                  print(current.info, end=" ")
                  current = current.prev
              print()

      def deleteFirst(self):
          """Menghapus node pertama dari list."""
          if self.first:
              P = self.first
              self.first = P.next
              if self.first:
                  self.first.prev = None
              else:
                  self.last = None
              return P
          return None

      def deleteLast(self):
          """Menghapus node terakhir dari list."""
          if self.last:
              P = self.last
              self.last = P.prev
              if self.last:
                  self.last.next = None
              else:
                  self.first = None
              return P
          return None

      def searchInfo(self, x):
          """Mencari node dengan data x."""
          current = self.first
          while current and current.info != x:
              current = current.next
          return current
  ```

### 3. Operasi Dasar pada Double Linked List
Berikut adalah penjelasan operasi dasar yang diimplementasikan:

#### a. Membuat List Kosong (`createList`)
- **Fungsi**: Menginisialisasi list menjadi kosong.
- **Penjelasan**: Mengatur atribut `first` dan `last` ke `None`.
- **Contoh Penggunaan**:
  ```python
  L = List()
  L.createList()  # List sekarang kosong
  ```

#### b. Membuat Elemen Baru (`createElement`)
- **Fungsi**: Membuat node baru dengan data tertentu.
- **Penjelasan**: Mengembalikan objek `Node` dengan data `x`, `next = None`, dan `prev = None`.
- **Contoh Penggunaan**:
  ```python
  newNode = L.createElement(5)  # Membuat node dengan data 5
  ```

#### c. Menyisipkan Elemen di Awal (`insertFirst`)
- **Fungsi**: Menyisipkan node baru di awal list.
- **Penjelasan**: Menghubungkan node baru ke `first`, memperbarui `prev` dari node lama (jika ada), dan mengatur `first`. Jika list kosong, node baru juga menjadi `last`.
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
- **Penjelasan**: Menghubungkan node baru ke `last`, memperbarui `next` dari node lama (jika ada), dan mengatur `last`. Jika list kosong, node baru juga menjadi `first`.
- **Contoh Penggunaan**:
  ```python
  P = L.createElement(3)
  L.insertLast(P)  # List sekarang berisi: 10 3
  L.printList()  # Output: 10 3
  ```

#### e. Menampilkan List (`printList`)
- **Fungsi**: Menampilkan semua elemen dalam list dari depan ke belakang.
- **Penjelasan**: Melintasi list dari `first` hingga akhir, mencetak setiap data. Jika list kosong, tampilkan pesan "List kosong".
- **Contoh Penggunaan**:
  ```python
  L.printList()  # Output: 10 3
  ```

#### f. Menampilkan List Terbalik (`printListReverse`)
- **Fungsi**: Menampilkan semua elemen dalam list dari belakang ke depan.
- **Penjelasan**: Melintasi list dari `last` hingga awal menggunakan referensi `prev`. Eksklusif untuk Double Linked List.
- **Contoh Penggunaan**:
  ```python
  L.printListReverse()  # Output: 3 10
  ```

### 4. Operasi Tambahan
Berikut adalah operasi tambahan untuk memperkaya fungsionalitas:

#### a. Menghapus Elemen Pertama (`deleteFirst`)
- **Fungsi**: Menghapus node pertama dari list dan mengembalikan node yang dihapus.
- **Penjelasan**: Mengatur `first` ke node berikutnya, memperbarui `prev` dari node baru (jika ada), dan menangani kasus list menjadi kosong.
- **Contoh Penggunaan**:
  ```python
  P = L.deleteFirst()
  if P:
      print(f"Elemen yang dihapus: {P.info}")
  L.printList()  # Output: 3
  ```

#### b. Menghapus Elemen Terakhir (`deleteLast`)
- **Fungsi**: Menghapus node terakhir dari list dan mengembalikan node yang dihapus.
- **Penjelasan**: Mengatur `last` ke node sebelumnya, memperbarui `next` dari node baru (jika ada), dan menangani kasus list menjadi kosong.
- **Contoh Penggunaan**:
  ```python
  P = L.deleteLast()
  if P:
      print(f"Elemen yang dihapus: {P.info}")
  L.printList()  # Output: (kosong)
  ```

#### c. Mencari Elemen (`searchInfo`)
- **Fungsi**: Mencari node dengan data tertentu.
- **Penjelasan**: Melintasi list dari `first` hingga menemukan node dengan data `x` atau mencapai akhir (`None`).
- **Contoh Penggunaan**:
  ```python
  found = L.searchInfo(4)
  if found:
      print(f"Data {found.info} ditemukan")
  else:
      print("Data 4 tidak ditemukan")
  ```

### 5. Implementasi Lengkap
Berikut adalah file lengkap untuk implementasi Double Linked List dalam Python:

#### File: `list.py`
```python
class Node:
    def __init__(self, data):
        self.info = data
        self.next = None
        self.prev = None

class List:
    def __init__(self):
        self.first = None
        self.last = None

    def createList(self):
        """Menginisialisasi list kosong."""
        self.first = None
        self.last = None

    def createElement(self, x):
        """Membuat node baru dengan data x."""
        return Node(x)

    def insertFirst(self, P):
        """Menyisipkan node P di awal list."""
        if P:
            P.next = self.first
            P.prev = None
            if self.first:
                self.first.prev = P
            else:
                self.last = P
            self.first = P

    def insertLast(self, P):
        """Menyisipkan node P di akhir list."""
        if P:
            P.prev = self.last
            P.next = None
            if self.last:
                self.last.next = P
            else:
                self.first = P
            self.last = P

    def printList(self):
        """Menampilkan semua elemen dalam list dari depan ke belakang."""
        if not self.first:
            print("List kosong")
        else:
            current = self.first
            while current:
                print(current.info, end=" ")
                current = current.next
            print()

    def printListReverse(self):
        """Menampilkan semua elemen dalam list dari belakang ke depan."""
        if not self.last:
            print("List kosong")
        else:
            current = self.last
            while current:
                print(current.info, end=" ")
                current = current.prev
            print()

    def deleteFirst(self):
        """Menghapus node pertama dari list."""
        if self.first:
            P = self.first
            self.first = P.next
            if self.first:
                self.first.prev = None
            else:
                self.last = None
            return P
        return None

    def deleteLast(self):
        """Menghapus node terakhir dari list."""
        if self.last:
            P = self.last
            self.last = P.prev
            if self.last:
                self.last.next = None
            else:
                self.first = None
            return P
        return None

    def searchInfo(self, x):
        """Mencari node dengan data x."""
        current = self.first
        while current and current.info != x:
            current = current.next
        return current
```

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

    print("Isi list (depan ke belakang):", end=" ")
    L.printList()  # Output: digit NIM dalam urutan input

    print("Isi list (belakang ke depan):", end=" ")
    L.printListReverse()  # Output: digit NIM dalam urutan terbalik

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
