# **1.2 Циклический список** 
## практика 2

date: 17.02.2025

```
|tail| -> 1)|next| -> |next| ... |next| -> на 1) next
            |data|    |data|     |data|
			(tail)    (head)
tail = nullptr;
head = tail -> next;
```

реализация кодом:
```
List p = new Item;
p -> next = tail -> next;
tail -> next = p;
tail = tail -> next;
```



## **Два указателя в списках**

```
         1)|next| -> |next| -> |next| -> на 1) next (циклически)
|head| ->  |data|    |data|    |data| <- |tail|
```

Два указателя на head и tail

```
#include <iostream>

using namespace std;

typededf struct Item {
	Item *next = nullptr;
	int data;
} Item;

typedef Item* List;

void toTail(List *pHead, List *pTail, int d) {
	List p = new Item;
	p -> data = d;
	if (!*pHead) {
		*pHead = p;
	} else {
		(*pTail) -> next = p;
	}
	*pTail = p;
}

int main() {
	List headPos = nullptr;
	List headNeg = nullptr;
	list tailPos = nullptr;
	List tailNeg = nullptr;
	
	int a, n;
	cin >> n;
	for (int i = 0; i < n; i++) {
		cin >> a;
		if (a >= 0) {
			toTail(&headPos, &tailPos, a);
		}
		toTail(&headNeg, &tailNeg, a);
	}
	if (!headPos) {
			headPos = headNeg;
	} else {
		tailPos -> next = headNeg;
	}

	for (List p = pHead; p; p = p -> next) {
		cout << p -> data << ' '; 
	}
	cout << endl;
	return 0;
}
```

