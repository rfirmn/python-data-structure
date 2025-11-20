### KONSEP UMUM MULTI LINKED LIST DENGAN RELASI PARENT-CHILD
Multi Linked List adalah struktur data yang mengizinkan lebih dari satu jenis hubungan antar elemen melalui pointer tambahan. Pada implementasi ini, kita memiliki tiga list yang **berdiri sendiri**:

1. List Parent – entitas utama  
2. List Child – entitas bawahan  
3. List Relasi – penghubung antara Parent dan Child (bisa 1-N atau M-N)

---

### BENTUK I – Relasi 1-N (One-to-Many) Pure  
Satu Parent memiliki banyak Child, satu Child hanya dimiliki oleh satu Parent.

<img width="1038" height="368" alt="image" src="https://user-images.githubusercontent.com/13241336/36650938-af7d7db4-1ad8-11e8-8a4d-43d83672f50f.png" />

```python
# file: multi_linked_list_1N.py
class NodeParent:
    def __init__(self, id_parent, nama):
        self.id = id_parent
        self.nama = nama
        self.first_child = None   # Head dari child milik parent ini (1-N)
        self.next = None          # Untuk linked list antar parent

class NodeChild:
    def __init__(self, id_child, data):
        self.id = id_child
        self.data = data
        self.next = None          # Child berikutnya dari parent yang sama

class MultiLinkedList_1N:
    def __init__(self):
        self.first_parent = None
        self.size = 0

    # INSERT PARENT
    def insertParent(self, id_parent, nama):
        if self.findParent(id_parent):
            print(f"[ERROR] Parent ID {id_parent} sudah ada!")
            return None
        new_parent = NodeParent(id_parent, nama)
        new_parent.next = self.first_parent
        self.first_parent = new_parent
        self.size += 1
        return new_parent

    # INSERT CHILD (1-N)
    def insertChild(self, id_parent, id_child, data):
        parent = self.findParent(id_parent)
        if not parent:
            print(f"[ERROR] Parent {id_parent} tidak ditemukan!")
            return False
        
        # Cek duplikat child di parent ini
        curr = parent.first_child
        while curr:
            if curr.id == id_child:
                print(f"[ERROR] Child ID {id_child} sudah ada di parent ini!")
                return False
            curr = curr.next
            
        new_child = NodeChild(id_child, data)
        new_child.next = parent.first_child
        parent.first_child = new_child
        return True

    # FIND PARENT
    def findParent(self, id_parent):
        curr = self.first_parent
        while curr:
            if curr.id == id_parent:
                return curr
            curr = curr.next
        return None

    # DELETE PARENT (dan semua child-nya otomatis terhapus)
    def deleteParent(self, id_parent):
        if not self.first_parent:
            return False
        if self.first_parent.id == id_parent:
            self.first_parent = self.first_parent.next
            self.size -= 1
            return True
        prev = self.first_parent
        curr = prev.next
        while curr:
            if curr.id == id_parent:
                prev.next = curr.next
                self.size -= 1
                return True
            prev = curr
            curr = curr.next
        return False

    # DELETE CHILD dari parent tertentu
    def deleteChild(self, id_parent, id_child):
        parent = self.findParent(id_parent)
        if not parent or not parent.first_child:
            return False
        if parent.first_child.id == id_child:
            parent.first_child = parent.first_child.next
            return True
        prev = parent.first_child
        curr = prev.next
        while curr:
            if curr.id == id_child:
                prev.next = curr.next
                return True
            prev = curr
            curr = curr.next
        return False

    # PRINT SEMUA
    def printAll(self):
        print("="*60)
        print("MULTI LINKED LIST – BENTUK I (Relasi 1-N)")
        print("="*60)
        if not self.first_parent:
            print("List Parent kosong.")
            return
        curr_p = self.first_parent
        while curr_p:
            print(f"Parent [{curr_p.id}] {curr_p.nama} → Child: ", end="")
            curr_c = curr_p.first_child
            if not curr_c:
                print("None", end="")
            else:
                while curr_c:
                    print(f"({curr_c.id}:{curr_c.data})", end=" → ")
                    curr_c = curr_c.next
            print("None")
            curr_p = curr_p.next
        print(f"Total Parent: {self.size}")
        print("="*60)
```

---

### BENTUK II – Relasi 1-N dan M-N Sekaligus (Hybrid)

<img width="1038" height="368" alt="image" src="https://github.com/user-attachments/assets/fd30cbc9-aceb-4579-a9f3-0a19b5be5cfa" />

```python
# file: multi_linked_list_hybrid.py
class NodeParent:
    def __init__(self, id_parent, nama):
        self.id = id_parent
        self.nama = nama
        self.first_child_1N = None     # Relasi 1-N
        self.first_relasi_MN = None    # Head relasi M-N dari parent ini
        self.next = None

class NodeChild1N:
    def __init__(self, id_child, data):
        self.id = id_child
        self.data = data
        self.next = None

class NodeChildMN:
    def __init__(self, id_child, data):
        self.id = id_child
        self.data = data
        self.next = None               # Untuk list child global (opsional)

class NodeRelasiMN:
    def __init__(self, parent_node, child_node):
        self.parent = parent_node      # pointer ke NodeParent
        self.child = child_node        # pointer ke NodeChildMN
        self.next = None               # next relasi dari parent yang sama

class MultiLinkedList_Hybrid:
    def __init__(self):
        self.first_parent = None
        self.first_child_MN = None

    def insertParent(self, id_p, nama):
        if self.findParent(id_p): return None
        np = NodeParent(id_p, nama)
        np.next = self.first_parent
        self.first_parent = np
        return np

    def insertChild1N(self, id_parent, id_child, data):
        parent = self.findParent(id_parent)
        if not parent: return False
        nc = NodeChild1N(id_child, data)
        nc.next = parent.first_child_1N
        parent.first_child_1N = nc
        return True

    def insertChildMN(self, id_child, data):
        if self.findChildMN(id_child): return None
        nc = NodeChildMN(id_child, data)
        nc.next = self.first_child_MN
        self.first_child_MN = nc
        return nc

    def insertRelasiMN(self, id_parent, id_child):
        parent = self.findParent(id_parent)
        child = self.findChildMN(id_child)
        if not parent or not child: return False
        rel = NodeRelasiMN(parent, child)
        rel.next = parent.first_relasi_MN
        parent.first_relasi_MN = rel
        return True

    def findParent(self, id_p):
        c = self.first_parent
        while c and c.id != id_p: c = c.next
        return c

    def findChildMN(self, id_c):
        c = self.first_child_MN
        while c and c.id != id_c: c = c.next
        return c

    def printAll(self):
        print("="*70)
        print("MULTI LINKED LIST – BENTUK II (1-N + M-N Hybrid)")
        print("="*70)
        p = self.first_parent
        while p:
            print(f"Parent [{p.id}] {p.nama}")
            print("   ├── 1-N Children  : ", end="")
            c1 = p.first_child_1N
            while c1:
                print(f"({c1.id}:{c1.data})", end=" → ")
                c1 = c1.next
            print("None" if not p.first_child_1N else "")
            
            print("   └── M-N Relations : ", end="")
            r = p.first_relasi_MN
            while r:
                print(f"({r.child.id}:{r.child.data})", end=" → ")
                r = r.next
            print("None" if not p.first_relasi_MN else "")
            p = p.next
        print("="*70)
```

---

### BENTUK III-A – Relasi M-N Klasik (Dengan Node Relasi Eksplisit)

<img width="1071" height="549" alt="image" src="https://github.com/user-attachments/assets/232b9af6-8a13-42a0-b331-a26360852fc8" />

```python
# file: multi_linked_list_MN_classic.py
class NodeParent:
    def __init__(self, id_parent, nama):
        self.id = id_parent
        self.nama = nama
        self.next = None
        self.relasi_head = None   # Daftar relasi dari parent ini

class NodeChild:
    def __init__(self, id_child, data):
        self.id = id_child
        self.data = data
        self.next = None

class NodeRelasi:
    def __init__(self, parent, child):
        self.parent = parent
        self.child = child
        self.next_from_parent = None
        self.next_from_child = None   # Bisa untuk traversal dari child (bi-directional)

class MultiLinkedList_MN_A:
    def __init__(self):
        self.first_parent = None
        self.first_child = None

    def insertParent(self, id_p, nama):
        if self.findParent(id_p): return None
        np = NodeParent(id_p, nama)
        np.next = self.first_parent
        self.first_parent = np
        return np

    def insertChild(self, id_c, data):
        if self.findChild(id_c): return None
        nc = NodeChild(id_c, data)
        nc.next = self.first_child
        self.first_child = nc
        return nc

    def insertRelasi(self, id_parent, id_child):
        p = self.findParent(id_parent)
        c = self.findChild(id_child)
        if not p or not c: return False
        if self._isRelated(p, c): 
            return False  # sudah terelasi
        rel = NodeRelasi(p, c)
        rel.next_from_parent = p.relasi_head
        p.relasi_head = rel
        return True

    def _isRelated(self, parent, child):
        r = parent.relasi_head
        while r:
            if r.child.id == child.id:
                return True
            r = r.next_from_parent
        return False

    def deleteRelasi(self, id_parent, id_child):
        p = self.findParent(id_parent)
        if not p or not p.relasi_head: return False
        if p.relasi_head.child.id == id_child:
            p.relasi_head = p.relasi_head.next_from_parent
            return True
        prev = p.relasi_head
        curr = prev.next_from_parent
        while curr:
            if curr.child.id == id_child:
                prev.next_from_parent = curr.next_from_parent
                return True
            prev = curr
            curr = curr.next_from_parent
        return False

    def findParent(self, id_p):
        c = self.first_parent
        while c and c.id != id_p: c = c.next
        return c

    def findChild(self, id_c):
        c = self.first_child
        while c and c.id != id_c: c = c.next
        return c

    def printAll(self):
        print("="*70)
        print("MULTI LINKED LIST – BENTUK III-A (M-N Klasik)")
        print("="*70)
        p = self.first_parent
        while p:
            print(f"Parent [{p.id}] {p.nama} → terhubung dengan → ", end="")
            r = p.relasi_head
            if not r:
                print("None")
            else:
                while r:
                    print(f"({r.child.id}:{r.child.data})", end="  ")
                    r = r.next_from_parent
                print()
            p = p.next
        print("="*70)
```

---

### BENTUK III-B – Relasi M-N Modern

<img width="1064" height="560" alt="image" src="https://github.com/user-attachments/assets/c37131ab-988e-4fc7-841d-0ffcda2f3822" />

```python
# file: multi_linked_list_MN_modern.py
class MultiLinkedList_MN_B:
    def __init__(self):
        self.parents = {}   # id → {nama, ...}
        self.children = {}  # id → data
        self.relasi = {}    # parent_id → set(child_id)

    def insertParent(self, id_p, nama):
        if id_p in self.parents:
            return False
        self.parents[id_p] = {'nama': nama}
        self.relasi[id_p] = set()
        return True

    def insertChild(self, id_c, data):
        if id_c in self.children:
            return False
        self.children[id_c] = data
        return True

    def insertRelasi(self, id_p, id_c):
        if id_p not in self.parents or id_c not in self.children:
            return False
        self.relasi[id_p].add(id_c)
        return True

    def deleteRelasi(self, id_p, id_c):
        if id_p in self.relasi:
            self.relasi[id_p].discard(id_c)

    def deleteParent(self, id_p):
        self.parents.pop(id_p, None)
        self.relasi.pop(id_p, None)

    def deleteChild(self, id_c):
        self.children.pop(id_c, None)
        for s in self.relasi.values():
            s.discard(id_c)

    def findChildrenOf(self, id_p):
        return self.relasi.get(id_p, set())

    def findParentsOf(self, id_c):
        return {p for p, childs in self.relasi.items() if id_c in childs}

    def printAll(self):
        print("="*70)
        print("MULTI LINKED LIST – BENTUK III-B (M-N Modern – Hash Based)")
        print("="*70)
        for pid, rel_set in self.relasi.items():
            p = self.parents[pid]
            childs = [f"({c}:{self.children[c]})" for c in rel_set]
            print(f"Parent [{pid}] {p['nama']} → {', '.join(childs) if childs else 'None'}")
        print(f"Total Parent: {len(self.parents)} | Total Child: {len(self.children)}")
        print("="*70)
```
