---
theme: seriph
background: https://images.unsplash.com/photo-1484665739383-a1069a82d4be?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=1080&ixid=MnwxfDB8MXxyYW5kb218MHx8cHJvZ3JhbW1pbmd8fHx8fHwxNzA5NTgxOTU5&ixlib=rb-4.0.3&q=80&utm_campaign=api-credit&utm_medium=referral&utm_source=unsplash_source&w=1920
class: text-center
highlighter: shiki
transition: slide-left
title: Estructuras de Datos y Algoritmos 1
lineNumbers: true
---

# Estructuras de Datos y Algoritmos 1 📘✨

Repasemos los conceptos fundamentales de las estructuras de datos y algoritmos. 🧠

---

# Órdenes Temporales ⌛

¿Alguna vez te has preguntado por qué algunos programas son más rápidos que otros? Aquí está el secreto: **Órdenes Temporales**.

```cpp {maxHeight:'350px'}
void printArray(int arr[], int size) {
    for(int i = 0; i < size; i++) {
        cout << arr[i] << " ";
    }
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr)/sizeof(arr[0]);
    printArray(arr, size);
    return 0;
}
```

Ejemplos de órdenes temporales:
- **O(n):** Tiempo lineal. 📈
- **O(1):** Tiempo constante. ⏱
- **O(log n):** Logarítmico. 🌲

---

# Tipos Abstractos de Datos (TAD) 📦

**TAD** son las reglas del juego. Definen cómo interactuamos con nuestros datos.

- **Lista:** Secuencia de elementos.
- **Set:** Colección de elementos únicos.
- **Diccionario:** Pares de clave-valor.
- ¿ Algún otro ?

---

# TAD Lista 📝

Las listas son como una lista de compras. Puedes agregar, quitar y buscar elementos.

```cpp {all|8-10|12-14|16-18|20-22|24-26|28-30|32-34|all}{maxHeight:'350px'}
#ifndef LIST_H
#define LIST_H

template <class T>
class List
{
public:
    // pre:
    // post: the element is inserted at the end of the list
    virtual void insert(T element) = 0;

    // pre: the index is valid (0 <= index < size)
    // post: the element is inserted at the given index
    virtual void insertAt(int index, T element) = 0;

    // pre: -
    // post: remove the first element that is equal to the given element
    virtual void remove(T element) = 0;

    // pre: the index is valid (0 <= index < size)
    // post: the element is removed at the given index
    virtual void removeAt(int index) = 0;

    // pre: -
    // post: returns if the list is empty
    virtual bool isEmpty() = 0;

    // pre: the index is valid (0 <= index < size)
    // post: returns the element at the given index
    virtual T get(int index) = 0;

    // pre: -
    // post: returns the size of the list
    virtual int getSize() = 0;
};

#endif
```


---

# TAD Set

Los conjuntos son como una colección de elementos únicos. No hay duplicados. Utiles para buscar y eliminar elementos sin importar su orden.

```cpp {all|8-10|12-14|16-18|20-22|24-26|all}{maxHeight:'350px'}
#ifndef SET_H
#define SET_H

template <class T>
class Set
{
public:
    // pre:
    // post: the element is inserted in the set
    virtual void insert(T element) = 0;

    // pre:
    // post: the element is removed from the set
    virtual void remove(T element) = 0;

    // pre:
    // post: returns if the element is in the set
    virtual bool contains(T element) = 0;

    // pre:
    // post: returns if the set is empty
    virtual bool isEmpty() = 0;

    // pre:
    // post: returns the size of the set
    virtual int getSize() = 0;
};

#endif
```

---


# TAD Diccionario o tabla 📚

Los diccionarios son como una tabla de datos. Cada elemento tiene una clave única y un valor asociado.

```cpp {all|8-10|12-14|16-18|20-22|24-26|28-30|all}{maxHeight:'350px'}
#ifndef DICTIONARY_H
#define DICTIONARY_H

template <class K, class V>
class Dictionary
{
public:
    // pre:
    // post: the key-value pair is inserted in the dictionary
    virtual void insert(K key, V value) = 0;

    // pre:
    // post: the key-value pair is removed from the dictionary
    virtual void remove(K key) = 0;

    // pre:
    // post: returns if the key is in the dictionary
    virtual bool contains(K key) = 0;

    // pre:
    // post: returns the value associated with the key
    virtual V get(K key) = 0;

    // pre:
    // post: returns if the dictionary is empty
    virtual bool isEmpty() = 0;

    // pre:
    // post: returns the size of the dictionary
    virtual int getSize() = 0;
};

#endif
```

---

# Estructuras de Datos

Las estructuras de datos son como cajas de herramientas. Cada una tiene su propósito y ventajas.

- **Array:** Acceso rápido, tamaño fijo.
- **Lista Enlazada:** Dinámica, fácil de expandir.
- **Árbol Binario de Busqueda:** Búsqueda eficiente.
- **AVL:** Árbol balanceado.

<br>

Estructuras de datos vs Tipo abstracto de datos:

- ¿ Cuál es la diferencia entre una estructura de datos y un tipo abstracto de datos ?
- ¿ Quién determina el órden de las operaciones ? 

---

# Lista Simple y Doble Enlace 🔗
Dos variantes de listas enlazadas

```cpp {all|1-10|3|4-5|13-20|all}{maxHeight:'350px'}
class Node {
public:
    int data;
    Node* prev;
    Node* next;
    Node(int d) {
        data = d;
        prev = NULL;
        next = NULL;
    }
};

int main() {
    Node* head = new Node(1);
    Node* second = new Node(2);
    head->next = second;
    second->prev = head;
    cout << "Elemento: " << second->prev->data << " <-> " << second->data << endl;
    return 0;
}
```

---

# Arrays vs. Listas Enlazadas
Cuál es mejor?

**Arrays:** Rápidos para el acceso a posiciones específicas, problemas con tamaño variable.

**Listas Enlazadas:** Lentas para el acceso a cualquier posición, tamaño variable.

---

# Árboles Binarios de Búsqueda (ABB) 🌳

Los ABB almacenan datos de forma ordenada. Cada nodo tiene un valor y dos hijos: uno menor y otro mayor.

```cpp {all|1-9|11-19|12-13|14-15|16-17|21-29|all}{maxHeight:'300px'}
class Node {
public:
    int key;
    Node *left, *right;
    Node(int item) {
        key = item;
        left = right = NULL;
    }
};

Node* insert(Node* node, int key) {
    if (node == NULL) 
        return new Node(key);
    if (key < node->key)
        node->left = insert(node->left, key);
    else if (key > node->key)
        node->right = insert(node->right, key);
    return node;
}

int main() {
    Node* root = NULL;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    return 0;
}
```
<br>

> Orden de operaciones: **O(log n)** (caso promedio)

---

# Recomendaciones 📌
Para comenzar con A2, es importante que repases los conceptos fundamentales de las estructuras de datos y algoritmos.

- **Órdenes Temporales:** ¿Cuánto tiempo toma una operación?
- **TAD:** Listas, conjuntos y diccionarios.
- **Estructuras de Datos:** Arrays, listas enlazadas, árboles binarios de búsqueda.

---
layout: quote
---
# Ahora sí, ¡a comenzar con A2! 🚀
