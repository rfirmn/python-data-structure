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

  class List:
      def __init__(self):
          self.first = None

      def createList(self):
          """Menginisialisasi list kosong."""
          self.first = None

      def createElement(self, x):
          """Membuat node baru dengan data x."""
          return Node(x)

      def insertFirst(self, P):
          """Menyisipkan node P di awal list."""
          if P:
              P.next = self.first
              self.first = P

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

      def deleteFirst(self):
          """Menghapus node pertama dari list."""
          if self.first:
              P = self.first
              self.first = P.next
              return P
          return None

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

      def searchInfo(self, x):
          """Mencari node dengan data x."""
          current = self.first
          while current and current.info != x:
              current = current.next
          return current
  ```

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

#### File: `list.py`
```python
class Node:
    def __init__(self, data):
        self.info = data
        self.next = None

class List:
    def __init__(self):
        self.first = None

    def createList(self):
        """Menginisialisasi list kosong."""
        self.first = None

    def createElement(self, x):
        """Membuat node baru dengan data x."""
        return Node(x)

    def insertFirst(self, P):
        """Menyisipkan node P di awal list."""
        if P:
            P.next = self.first
            self.first = P

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

    def deleteFirst(self):
        """Menghapus node pertama dari list."""
        if self.first:
            P = self.first
            self.first = P.next
            return P
        return None

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
