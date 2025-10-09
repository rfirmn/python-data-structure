# Modul 3: ABSTRACT DATA TYPE (ADT)
---

## TUJUAN PRAKTIKUM

1. Memahami konsep **Abstract Data Type (ADT)** dan penggunaannya dalam pemrograman.
2. Mengetahui bagaimana cara **membuat, menggunakan, dan memisahkan ADT** dalam Python.
3. Mampu mengimplementasikan **ADT mahasiswa** dan **ADT pelajaran** secara modular.
4. Memahami peran ADT sebagai dasar untuk mempelajari struktur data yang lebih kompleks.

---

## 3.1 Pengantar Abstract Data Type (ADT)

### Definisi Tipe Data Abstrak (ADT)
Tipe Data Abstrak (Abstract Data Type/ADT) adalah model matematis atau spesifikasi logis dari sebuah tipe data. ADT mendefinisikan tipe data hanya berdasarkan perilaku dan operasi yang didukungnya, tanpa menentukan detail bagaimana data tersebut disimpan atau operasi tersebut diimplementasikan.

Sederhananya, ADT adalah kontrak atau cetak biru yang menjawab pertanyaan: "Apa yang dapat dilakukan oleh tipe data ini?"

Tiga Komponen Utama ADT:

1. Data (Nilai): Kumpulan nilai yang dapat ditampung oleh ADT.

2. Operasi (Behavior): Kumpulan fungsi atau metode yang mendefinisikan cara data dapat diakses, dimodifikasi, atau dikelola.

2. Aksioma (Hukum): Kondisi atau aturan yang mengatur bagaimana operasi-operasi tersebut berinteraksi dan memelihara konsistensi data.

### Abstraksi
**Abstraksi** berarti menyembunyikan detail implementasi dari pengguna. Seorang pengguna ADT (seorang programmer yang menggunakan ADT Stack, misalnya) hanya perlu tahu cara memanggil operasi `push()` dan `pop()`. Mereka tidak perlu tahu apakah data Stack disimpan menggunakan array dinamis (seperti list Python) atau menggunakan linked list.

Ini memungkinkan kita untuk berpikir pada level yang lebih tinggi (logika) tanpa terbebani oleh detail tingkat rendah (fisik penyimpanan).

### Contoh Analogi:
Bayangkan Remote TV sebagai ADT.

- Operasi (ADT): Tombol Volume Naik, Tombol Ganti Channel, Tombol Power.

- Detail Implementasi (Struktur Data): Sirkuit internal, kabel, sensor inframerah.

Anda, sebagai pengguna, hanya peduli dengan operasi remote (menaikkan volume). Anda tidak perlu tahu sirkuit internalnya. Jika pabrikan mengubah sirkuit internal (mengganti struktur data), asalkan tombolnya (operasi ADT) bekerja sama, Anda tidak terpengaruh.

---

### Komponen ADT

| Jenis Operasi | Deskripsi | Penamaan Umum |
|----------------|------------|----------------|
| **Konstruktor / Kreator** | Membentuk objek bertipe ADT | `__init__`, `create_...` |
| **Selector / Getter** | Mengambil nilai komponen | `get_...` |
| **Mutator / Setter** | Mengubah nilai komponen | `set_...` |
| **Validator** | Memeriksa keabsahan nilai | `is_valid_...` |
| **Destruktor** | Menghapus atau membebaskan memori (Python otomatis dengan garbage collector) | `__del__` |
| **Input / Output** | Membaca dan menampilkan nilai objek | `input_...`, `display_...` |
| **Operator Relasional** | Perbandingan antar objek | `__eq__`, `__lt__`, dsb |
| **Konversi Tipe** | Mengubah ke tipe dasar dan sebaliknya | `to_dict()`, `from_dict()` |

---

## 3.2 ADT dalam Konteks Python

### Hubungan ADT dan Data Structure
| ADT | Contoh Struktur Data di Python |
|------|-----------------------------|
| Stack | `list`, `collections.deque` |
| Queue | `queue.Queue`, `deque` |
| Set | `set` |
| Map | `dict` |
| List | `list` |

### Perbedaan ADT dan Structure data

| Aspek | Tipe Data Abstrak (ADT) | Struktur Data (Data Structure) |
|----------------|------------|----------------|
| **Definisi** | Model logis, kontrak perilaku. | Implementasi fisik data dan operasi. |
| **Pertanyaan** | APA yang bisa dilakukan? | BAGAIMANA itu dilakukan? |
| **Sifat** | Konseptual, Teoritis (Bebas Bahasa Pemrograman). | Konkret, Kode Aktual (Tergantung Bahasa Pemrograman). |
| **contoh** | Stack, Queue, List, Dictionary. | Array, Linked List, Hash Table, Binary Tree. |


---

## 3.3 Contoh Implementasi ADT di Python
---
### Contoh 1: Class and Function

```python
class Mahasiswa:
    def __init__(self, nim, nilai1, nilai2):
        self.nim = nim
        self.nilai1 = nilai1
        self.nilai2 = nilai2

# === Konstruktor ===
def create_mahasiswa(nim: str, nilai1: int, nilai2: int) -> Mahasiswa:
    """Membuat objek Mahasiswa baru"""
    return Mahasiswa(nim, nilai1, nilai2)

# === Input/Output ===
def input_mahasiswa() -> Mahasiswa:
    nim = input("Masukkan NIM: ")
    nilai1 = int(input("Masukkan nilai 1: "))
    nilai2 = int(input("Masukkan nilai 2: "))
    return create_mahasiswa(nim, nilai1, nilai2)

def tampil_mahasiswa(mhs: Mahasiswa):
    print(f"NIM: {mhs.nim}, Nilai1: {mhs.nilai1}, Nilai2: {mhs.nilai2}")

# === Fungsi Tambahan ===
def rata_rata(mhs: Mahasiswa) -> float:
    return (mhs.nilai1 + mhs.nilai2) / 2

```
---
### Contoh 2: Queue
**Queue** (Antrian) adalah ADT koleksi terurut di mana penambahan elemen baru (operasi `enqueue` atau `insert`) hanya terjadi di satu ujung yang disebut Rear (Belakang), dan penghapusan elemen (operasi `dequeue` atau `remove`) hanya terjadi di ujung yang berlawanan, yang disebut Front (Depan). Queue mengikuti prinsip FIFO (First-In, First-Out)—elemen yang pertama masuk adalah yang pertama keluar.

```python
# queue.py
class Queue:
    def __init__(self, max_size):
        """Konstruktor: membuat queue kosong dengan ukuran maksimum tertentu"""
        self.max_size = max_size
        self.items = []

    # === Konstruktor / Kreator ===
    @staticmethod
    def create_queue(max_size: int):
        """Membuat objek Queue baru"""
        return Queue(max_size)

    # === Primitif Utama ===
    def enqueue(self, item):
        """Menambahkan elemen ke belakang antrian"""
        if self.is_full():
            print("Queue penuh! Tidak bisa menambah data.")
        else:
            self.items.append(item)
            print(f"Enqueue: {item}")

    def dequeue(self):
        """Menghapus elemen dari depan antrian"""
        if self.is_empty():
            print("Queue kosong! Tidak bisa menghapus data.")
        else:
            removed = self.items.pop(0)
            print(f"Dequeue: {removed}")
            return removed

    # === Selector ===
    def peek(self):
        """Melihat elemen terdepan tanpa menghapusnya"""
        if self.is_empty():
            print("Queue kosong!")
        else:
            print(f"Elemen terdepan: {self.items[0]}")
            return self.items[0]

    # === Validator ===
    def is_empty(self):
        """Mengembalikan True jika queue kosong"""
        return len(self.items) == 0

    def is_full(self):
        """Mengembalikan True jika queue penuh"""
        return len(self.items) >= self.max_size

    # === Display ===
    def display(self):
        """Menampilkan isi queue"""
        if self.is_empty():
            print("Queue kosong.")
        else:
            print("Isi Queue:", self.items)

from queue import Queue

# Membuat queue dengan kapasitas maksimal 5 elemen
antrian = Queue.create_queue(5)

# Operasi queue
antrian.enqueue("Andi")
antrian.enqueue("Budi")
antrian.enqueue("Citra")

antrian.display()
antrian.peek()

antrian.dequeue()
antrian.display()

antrian.enqueue("Dewi")
antrian.enqueue("Eka")
antrian.enqueue("Fajar")  # melebihi kapasitas

antrian.display()

```
### Contoh 3: Stack

Stack adalah ADT yang mengikuti prinsip LIFO (Last-In, First-Out) — elemen yang terakhir dimasukkan akan menjadi yang pertama keluar. Stack memiliki dua operasi utama:

`push()` → menambahkan elemen ke puncak stack.

`pop()` → menghapus elemen dari puncak stack.

Analogi sederhana: tumpukan piring. Piring yang terakhir diletakkan di atas akan menjadi yang pertama diambil.

```python
class Queue:
def __init__(self, max_size):
self.max_size = max_size
self.items = []


@staticmethod
def create_queue(max_size: int):
return Queue(max_size)


def enqueue(self, item):
if self.is_full():
print("Queue penuh!")
else:
self.items.append(item)
print(f"Enqueue: {item}")


def dequeue(self):
if self.is_empty():
print("Queue kosong!")
else:
removed = self.items.pop(0)
print(f"Dequeue: {removed}")
return removed


def peek(self):
if not self.is_empty():
print(f"Front: {self.items[0]}")
return self.items[0]


def is_empty(self):
return len(self.items) == 0


def is_full(self):
return len(self.items) >= self.max_size


def display(self):
print("Isi Queue:", self.items if self.items else "Queue kosong")


# Contoh penggunaan
antrian = Queue.create_queue(5)
antrian.enqueue("Andi")
antrian.enqueue("Budi")
antrian.enqueue("Citra")
antrian.display()
antrian.dequeue()
antrian.display()
```
