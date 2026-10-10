# Struktur Data - Stack (Python)

## Pendahuluan
Stack adalah struktur data linier yang mengikuti prinsip **LIFO** (Last In, First Out), di mana elemen yang terakhir dimasukkan adalah elemen yang pertama kali dikeluarkan. Stack sering digunakan dalam aplikasi seperti evaluasi ekspresi, manajemen panggilan fungsi (call stack), dan algoritma backtracking.

<img width="958" height="669" alt="image" src="https://github.com/user-attachments/assets/92b651fc-bfbf-43c7-9127-95643214271c" />

### 1. Konsep Dasar Stack
- **Definisi**: Koleksi elemen yang hanya memungkinkan penambahan (push) dan penghapusan (pop) elemen di satu ujung, yang disebut **top** (puncak).
- **Ciri-ciri**:
  - Operasi utama: **push** (menambahkan elemen ke puncak) dan **pop** (menghapus elemen dari puncak).
  - **Top**: Menunjuk ke elemen teratas stack.
  - Ukuran dinamis (tergantung implementasi).
  - Dapat diimplementasikan menggunakan array atau linked list.
- **Ilustrasi Operasi**:
  - Push: Menambahkan elemen ke puncak stack.
  - Pop: Menghapus elemen dari puncak stack dan mengembalikannya.
  - Peek: Melihat elemen teratas tanpa menghapusnya.
  - IsEmpty: Memeriksa apakah stack kosong.
  - IsFull: Memeriksa apakah stack penuh (khususnya pada implementasi berbasis array dengan ukuran tetap).

### 2. Deklarasi Tipe Data
Berikut adalah implementasi struktur data Stack dalam Python menggunakan dua pendekatan: **array** dan **linked list**.

#### Implementasi Berbasis Array
- **Kelas StackArray**: Menggunakan list Python sebagai penyimpanan dengan kapasitas tertentu.
- **Struktur**:
  ```python
  class StackArray:
      def __init__(self, capacity):
          self.capacity = capacity
          self.data = [None] * capacity
          self.top = -1
  ```

#### Implementasi Berbasis Linked List
- **Kelas Node**: Merepresentasikan simpul dengan data dan referensi ke simpul berikutnya.
- **Kelas StackList**: Menggunakan linked list dengan `top` sebagai referensi ke simpul teratas.
- **Struktur Node**:
  ```python
  class Node:
      def __init__(self, data):
          self.info = data
          self.next = None
  ```

### 3. Implementasi Lengkap
Berikut adalah implementasi lengkap untuk kedua pendekatan Stack dalam Python.

```python
class Node:
    def __init__(self, data):
        self.info = data
        self.next = None

class StackArray:
    def __init__(self, capacity):
        """Menginisialisasi stack berbasis array dengan kapasitas tertentu."""
        self.capacity = capacity
        self.data = [None] * capacity
        self.top = -1

    def isEmpty(self):
        """Memeriksa apakah stack kosong."""
        return self.top == -1

    def isFull(self):
        """Memeriksa apakah stack penuh."""
        return self.top == self.capacity - 1

    def push(self, x):
        """Menambahkan elemen x ke puncak stack."""
        if self.isFull():
            print("Stack penuh, tidak bisa push")
            return
        self.top += 1
        self.data[self.top] = x

    def pop(self):
        """Menghapus dan mengembalikan elemen dari puncak stack."""
        if self.isEmpty():
            print("Stack kosong, tidak bisa pop")
            return None
        item = self.data[self.top]
        self.data[self.top] = None
        self.top -= 1
        return item

    def peek(self):
        """Melihat elemen teratas tanpa menghapusnya."""
        if self.isEmpty():
            print("Stack kosong")
            return None
        return self.data[self.top]

    def size(self):
        """Mengembalikan jumlah elemen dalam stack."""
        return self.top + 1

    def printStack(self):
        """Menampilkan semua elemen dalam stack dari puncak ke dasar."""
        if self.isEmpty():
            print("Stack kosong")
        else:
            print("Isi stack (dari puncak ke dasar):", end=" ")
            for i in range(self.top, -1, -1):
                print(self.data[i], end=" ")
            print()

class StackList:
    def __init__(self):
        """Menginisialisasi stack berbasis linked list."""
        self.top = None

    def isEmpty(self):
        """Memeriksa apakah stack kosong."""
        return self.top is None

    def push(self, x):
        """Menambahkan elemen x ke puncak stack."""
        newNode = Node(x)
        newNode.next = self.top
        self.top = newNode

    def pop(self):
        """Menghapus dan mengembalikan elemen dari puncak stack."""
        if self.isEmpty():
            print("Stack kosong, tidak bisa pop")
            return None
        item = self.top
        self.top = self.top.next
        return item.info

    def peek(self):
        """Melihat elemen teratas tanpa menghapusnya."""
        if self.isEmpty():
            print("Stack kosong")
            return None
        return self.top.info

    def size(self):
        """Mengembalikan jumlah elemen dalam stack."""
        count = 0
        current = self.top
        while current:
            count += 1
            current = current.next
        return count

    def printStack(self):
        """Menampilkan semua elemen dalam stack dari puncak ke dasar."""
        if self.isEmpty():
            print("Stack kosong")
        else:
            print("Isi stack (dari puncak ke dasar):", end=" ")
            current = self.top
            while current:
                print(current.info, end=" ")
                current = current.next
            print()
```

### 4. Operasi Dasar pada Stack
Berikut adalah penjelasan operasi dasar yang diimplementasikan untuk kedua pendekatan.

#### a. Menginisialisasi Stack
- **Fungsi**: Membuat stack kosong.
- **Penjelasan**:
  - **Array**: Mengatur `top` ke `-1` dan menginisialisasi array dengan kapasitas tertentu.
  - **Linked List**: Mengatur `top` ke `None`.
- **Contoh Penggunaan**:
  ```python
  # Array
  S_array = StackArray(10)
  # Linked List
  S_list = StackList()
  ```

#### b. Memeriksa Stack Kosong (`isEmpty`)
- **Fungsi**: Memeriksa apakah stack kosong.
- **Penjelasan**:
  - **Array**: Mengembalikan `True` jika `top == -1`.
  - **Linked List**: Mengembalikan `True` jika `top` adalah `None`.
- **Contoh Penggunaan**:
  ```python
  print(S_array.isEmpty())  # Output: True
  print(S_list.isEmpty())   # Output: True
  ```

#### c. Memeriksa Stack Penuh (`isFull`) (Hanya untuk Array)
- **Fungsi**: Memeriksa apakah stack penuh.
- **Penjelasan**: Mengembalikan `True` jika `top == capacity - 1`.
- **Contoh Penggunaan**:
  ```python
  print(S_array.isFull())  # Output: False
  ```

#### d. Menambahkan Elemen (`push`)
- **Fungsi**: Menambahkan elemen ke puncak stack.
- **Penjelasan**:
  - **Array**: Jika tidak penuh, increment `top` dan tambahkan elemen ke `data[top]`.
  - **Linked List**: Buat node baru, sambungkan ke `top`, dan perbarui `top`.
- **Contoh Penggunaan**:
  ```python
  S_array.push(5)   # Stack: [5]
  S_list.push(5)    # Stack: [5]
  S_array.printStack()  # Output: 5
  S_list.printStack()   # Output: 5
  ```

#### e. Menghapus Elemen (`pop`)
- **Fungsi**: Menghapus dan mengembalikan elemen dari puncak stack.
- **Penjelasan**:
  - **Array**: Jika tidak kosong, ambil elemen di `data[top]`, set ke `None`, dan decrement `top`.
  - **Linked List**: Jika tidak kosong, ambil elemen di `top`, perbarui `top` ke node berikutnya, dan kembalikan data.
- **Contoh Penggunaan**:
  ```python
  item = S_array.pop()  # item = 5
  print(f"Popped: {item}")  # Output: Popped: 5
  item = S_list.pop()   # item = 5
  print(f"Popped: {item}")  # Output: Popped: 5
  ```

#### f. Melihat Elemen Teratas (`peek`)
- **Fungsi**: Mengembalikan elemen teratas tanpa menghapusnya.
- **Penjelasan**:
  - **Array**: Mengembalikan `data[top]` jika tidak kosong.
  - **Linked List**: Mengembalikan `top.info` jika tidak kosong.
- **Contoh Penggunaan**:
  ```python
  S_array.push(10)
  print(S_array.peek())  # Output: 10
  S_list.push(10)
  print(S_list.peek())   # Output: 10
  ```

#### g. Menghitung Ukuran Stack (`size`)
- **Fungsi**: Mengembalikan jumlah elemen dalam stack.
- **Penjelasan**:
  - **Array**: Mengembalikan `top + 1`.
  - **Linked List**: Menghitung jumlah node dari `top` hingga akhir.
- **Contoh Penggunaan**:
  ```python
  print(S_array.size())  # Output: 1
  print(S_list.size())   # Output: 1
  ```

#### h. Menampilkan Stack (`printStack`)
- **Fungsi**: Menampilkan semua elemen dari puncak ke dasar.
- **Penjelasan**: Melintasi stack dan mencetak setiap elemen. Jika kosong, tampilkan pesan "Stack kosong".
- **Contoh Penggunaan**:
  ```python
  S_array.push(3)
  S_array.printStack()  # Output: 3 10
  S_list.push(3)
  S_list.printStack()   # Output: 3 10
  ```

### 5. Contoh Aplikasi
Berikut adalah contoh aplikasi stack untuk memproses 10 digit NIM (Nomor Induk Mahasiswa).

```python
def main():
    # Inisialisasi stack
    S_array = StackArray(10)
    S_list = StackList()

    # Input 10 digit NIM
    nim = []
    print("Input NIM (Student ID) digit by digit:")
    for i in range(10):
        digit = int(input(f"Digit {i + 1}: "))
        nim.append(digit)
        S_array.push(digit)
        S_list.push(digit)

    # Menampilkan isi stack
    print("\nStack berbasis Array:")
    S_array.printStack()  # Output: digit NIM dari terakhir ke pertama
    print("Ukuran stack:", S_array.size())

    print("\nStack berbasis Linked List:")
    S_list.printStack()   # Output: digit NIM dari terakhir ke pertama
    print("Ukuran stack:", S_list.size())

    # Contoh operasi tambahan
    print("\nOperasi pada StackArray:")
    print("Melihat elemen teratas:", S_array.peek())
    print("Menghapus elemen teratas...")
    item = S_array.pop()
    if item is not None:
        print(f"Elemen yang dihapus: {item}")
    S_array.printStack()

    print("\nOperasi pada StackList:")
    print("Melihat elemen teratas:", S_list.peek())
    print("Menghapus elemen teratas...")
    item = S_list.pop()
    if item is not None:
        print(f"Elemen yang dihapus: {item}")
    S_list.printStack()

    # Memeriksa status stack
    print("\nStatus StackArray:")
    print("Kosong:", S_array.isEmpty())
    print("Penuh:", S_array.isFull())

    print("\nStatus StackList:")
    print("Kosong:", S_list.isEmpty())

if __name__ == "__main__":
    main()
```

### 6. Contoh Penggunaan
Berikut adalah contoh interaksi saat menjalankan `main.py` dengan input NIM `1234567890`:

#### Input:
```
Input NIM (Student ID) digit by digit:
Digit 1: 1
Digit 2: 2
Digit 3: 3
Digit 4: 4
Digit 5: 5
Digit 6: 6
Digit 7: 7
Digit 8: 8
Digit 9: 9
Digit 10: 0
```

#### Output:
```
Stack berbasis Array:
Isi stack (dari puncak ke dasar): 0 9 8 7 6 5 4 3 2 1
Ukuran stack: 10

Stack berbasis Linked List:
Isi stack (dari puncak ke dasar): 0 9 8 7 6 5 4 3 2 1
Ukuran stack: 10

Operasi pada StackArray:
Melihat elemen teratas: 0
Menghapus elemen teratas...
Elemen yang dihapus: 0
Isi stack (dari puncak ke dasar): 9 8 7 6 5 4 3 2 1

Operasi pada StackList:
Melihat elemen teratas: 0
Menghapus elemen teratas...
Elemen yang dihapus: 0
Isi stack (dari puncak ke dasar): 9 8 7 6 5 4 3 2 1

Status StackArray:
Kosong: False
Penuh: False

Status StackList:
Kosong: False
```
