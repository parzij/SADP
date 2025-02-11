# 1.1 Линейные списки

## практика 10.02.2025
###  Стандартный список


```
head -> |next| \ |next| 
        |data|  >|data| -> nullptr
```
как это выглядит в памяти

**организация обычного линейного списка**
```с++
typedef struct Item {
	Item* next = nullptr;
	int data;
	
} Item;

typedef Item* List;

```


---

```
head -> |next| -> |next| -> nullptr
		| 10 |    | 20 |
```
как это выглядит в памяти

**общая идея организации списка**
```
int main () {
	List head = new Item;
	head -> data = 10;
	head -> next = new Item;
	list p = head -> next;
	p -> data = 20;
	cout << head -> data << " " << p -> data << endl;
	return 0; 
}
```

---
```
head -> |next| -> |next| <- p -> nullptr
		| 5  | 10 | 20 |
```
как это выглядит в памяти

```
p = new Item;
p -> data = 5;
p -> next = head;
head = p;
```
добавления 5 в начало списка перед 10 и 20

```
p = head -> next -> next;
delete head -> next;
head -> next = p;
```
 удаление второго элемента из списка ['5', '10', '20'] ('10')
 (по факту мы обратились к 20, через 10, затем удалили указатель на 10 и прописали указатель с элемента '5' на элемент '20')
 
**Создание списка с элементами от '1' до '10' с использованием цикла**

```
head -> |next| -> |next| <- p
   p /> | 1  |    | i  | 
```
как это выглядит в памяти

```
int main() {
	List head = new Iteam;
	head -> data = 1;
	List p = head; // указатель на head
	for (int i = 2; i <= 10; i++) {
		p -> next = new Item;
		p = p -> next;
		p -> data = i;
	}

	for (p = head; p != nullptr;) {
		cout << p -> data << " ";
		p = p -> next;
	}
	cout << endl;
	return 0;	
}
```
---

**Удаление всех элементов списка**

```
for (p = head; p != nullptr;) {
	List temp = p;
	p = p -> next;
	delete temp;
}
```

**Добавление элементов в конец списка начиная с '10'**
```
int main() {
	List head = new Iteam;
	head -> data = 10;
	List p = head; // указатель на head
	for (int i = 9; i > 0; i--) {
		p = new Item;
		p -> data = i;
		p -> next = head;
		head = p;		
	}
}
```
------
---


### Двухсвязный список

```
	    |prev| <- |prev| <-   |prev|
head -> |next| -> |next| ->   |next| -> nullptr
		|data|    |data| ...  |data|
```
как это выглядит в памяти

**добавление нового элемента в конец двухсвязного списка
(два указателя)**
```
typedef struct Item {
	Item *prev = nullptr;
	Item *next = nullptr;
	int data;
} Item;

typedef Item* Dlist;

Dlist = new Item;
p -> data = 100;
p -> prev = tail;
tail -> next = p;
tail = next;
```
---

**удаление элемента с середины двухсвязного списка**
```
p -> prev -> next = p -> next;
p -> next -> prev = p -> prev;
delete p;
```


**два произвольный элемента, поменять их позиции в двухсвязном списке**
как выглядит на примере

```
          p                         (q)
          |                          |
          v                          v
(q) -> |prev |             (p) -> |prev |
	   |next | <- (q)             |next | <- (p)
	   |dataP|                    |dataQ|


```


реализация кодом
```
Dlist rprev = p -> prev;
Dlist rnext = p -> next;
p -> prev -> next = q;
p -> next -> prev = q;
q -> prev -> next = p;
q -> next -> prev = p;
p -> prev = q -> prev;
p -> next = q -> next;
q -> prev = rprev;
q -> next = rnext;
```
---
