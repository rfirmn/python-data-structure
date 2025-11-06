# Modul Praktikum Struktur Data

## **Modul 10: Tree (Binary Tree & Binary Search Tree)**

### **Tujuan Praktikum**

1. Memahami konsep penggunaan fungsi rekursif.
2. Mengimplementasikan fungsi rekursif dalam pemrograman.
3. Mengaplikasikan struktur data *Tree* dalam pemrograman.
4. Mengimplementasikan *Binary Tree* dan *Binary Search Tree (BST)* menggunakan Python.

---

## **10.1 Pengertian Rekursif**

Rekursif adalah teknik pemrograman di mana sebuah fungsi memanggil dirinya sendiri selama kondisi tertentu masih terpenuhi. Rekursif digunakan untuk menyelesaikan masalah yang dapat dipecah menjadi sub-masalah yang lebih kecil dengan pola yang sama.

### **Karakteristik Fungsi Rekursif:**

* Memiliki **base case** (kondisi berhenti).
* Memiliki **recursive step** yaitu pemanggilan fungsi itu sendiri.

### **Contoh Rekursif: Pangkat**

```python
def pangkat_dua(x):
    if x == 0:
        return 1
    else:
        return 2 * pangkat_dua(x - 1)

print(pangkat_dua(4))  # Output: 16
```

---

## **10.2 Kekurangan Rekursif**

* Membutuhkan memori lebih banyak karena *stack frame* bertambah setiap pemanggilan.
* Waktu eksekusi bisa lebih lambat daripada iteratif.

Namun rekursif **lebih mudah dipahami** untuk struktur data seperti **Tree**, karena Tree juga bersifat hierarkis.

---

## **10.3 Pengertian Tree**

**Tree** adalah struktur data non-linear yang terdiri dari simpul-simpul (*node*) yang saling terhubung. Tree memiliki satu node akar (*root*) dan node-node lain yang menjadi *child*.

### **Istilah-istilah dalam Tree:**

| Istilah | Penjelasan                        |
| ------- | --------------------------------- |
| Root    | Node paling atas                  |
| Parent  | Node yang memiliki child          |
| Child   | Node turunan dari parent          |
| Leaf    | Node yang tidak memiliki child    |
| Sibling | Node-node dengan parent yang sama |
| Depth   | Level kedalaman node              |

---

## **10.4 Binary Tree dan Binary Search Tree (BST)**

### **Binary Tree**

Setiap node memiliki **maksimal 2 anak** (left dan right).

### **Binary Search Tree (BST)**

BST memiliki aturan:

* Node kiri < Node parent
* Node kanan > Node parent

---

## **10.5 ADT Binary Search Tree (Python)**

File: `bstree.py`

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

class BST:
    def __init__(self):
        self.root = None

    def insert(self, value):
        self.root = self._insert_recursive(self.root, value)

    def _insert_recursive(self, node, value):
        if node is None:
            return Node(value)
        if value < node.value:
            node.left = self._insert_recursive(node.left, value)
        elif value > node.value:
            node.right = self._insert_recursive(node.right, value)
        return node

    def inorder(self, node):
        if node:
            self.inorder(node.left)
            print(node.value, end=" ")
            self.inorder(node.right)

    def preorder(self, node):
        if node:
            print(node.value, end=" ")
            self.preorder(node.left)
            self.preorder(node.right)

    def postorder(self, node):
        if node:
            self.postorder(node.left)
            self.postorder(node.right)
            print(node.value, end=" ")

    def find(self, value):
        return self._find_recursive(self.root, value)

    def _find_recursive(self, node, value):
        if node is None or node.value == value:
            return node
        if value < node.value:
            return self._find_recursive(node.left, value)
        else:
            return self._find_recursive(node.right, value)

    def count_nodes(self, node):
        if node is None:
            return 0
        return 1 + self.count_nodes(node.left) + self.count_nodes(node.right)

    def sum_values(self, node):
        if node is None:
            return 0
        return node.value + self.sum_values(node.left) + self.sum_values(node.right)

    def depth(self, node):
        if node is None:
            return 0
        return 1 + max(self.depth(node.left), self.depth(node.right))
```

---

## **10.6 Program Utama (`main.py`)**

```python
from bstree import BST

bst = BST()
values = [1, 2, 6, 4, 5, 3, 6, 7]

for v in values:
    bst.insert(v)

print("In-order Traversal:")
bst.inorder(bst.root)
print("\nPre-order Traversal:")
bst.preorder(bst.root)
print("\nPost-order Traversal:")
bst.postorder(bst.root)

print("\n\nKedalaman Tree:", bst.depth(bst.root))
print("Jumlah Node:", bst.count_nodes(bst.root))
print("Total Penjumlahan Nilai:", bst.sum_values(bst.root))
```

---

## **Output yang Diharapkan**

```
In-order: 1 2 3 4 5 6 7
Pre-order: 4 2 1 3 6 5 7
Post-order: 1 3 2 5 7 6 4
Kedalaman Tree: 3
Jumlah Node: 7
Total Penjumlahan Nilai: 28
```

