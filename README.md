# C Hash Table Implementation (Based on Ben Hoyt's Tutorial)

This repository contains a simple, efficient hash table implementation in C that follows Ben Hoyt's excellent [Build Your Own Hash Table in C](https://benhoyt.com/writings/hash-table-in-c/) tutorial. The purpose of this project is educational: to understand low-level data structure design and memory management in C by building a hash table from scratch.

> 💡 This implementation was directly inspired by and adapted from Ben Hoyt’s original work. All credit for the design and guiding principles belongs to him.

## 📦 Features

- Uses **open addressing** with **linear probing** for collision resolution.
- Automatically expands the table when it's more than half full.
- Stores key-value pairs where:
  - Keys are `const char*` (strings, copied via `strdup`)
  - Values are `void*` (user-provided pointers)
- Iteration support via a simple iterator type.
- Uses the **FNV-1a** hash function for good distribution and speed.

## 📚 File Structure

| File        | Description |
|-------------|-------------|
| `ht.c`      | Implementation of the hash table (`ht`) and its iterator (`hti`) |
| `ht.h`      | Public interface for using the hash table |
| `main.c`    | Optional: your test/demo file goes here |
| `README.md` | This file |

## 🛠️ How It Works

- **ht_create**: Allocates and initializes an empty hash table.
- **ht_set**: Inserts a key–value pair. Expands the table if it becomes more than half full.
- **ht_get**: Looks up a key and returns the corresponding value.
- **ht_destroy**: Frees all allocated memory — including the keys.
- **ht_iterator / it_next**: Iterates through all items in the hash table.

Internally, the hash table keeps an array of `ht_entry` structs. Each `ht_entry` stores a key and value. When inserting, it uses the FNV-1a hash of the key to find the initial slot and then probes forward until it finds an empty slot or an existing matching key.

## 🔁 Example Usage

```c
ht* table = ht_create();
ht_set(table, "name", "Mateo");
ht_set(table, "language", "C");

printf("%s\n", (char*)ht_get(table, "name"));  // Output: Mateo

ht_destroy(table);
```

To iterate:
```c
hti it = ht_iterator(table);
while (it_next(&it)) {
    printf("%s => %s\n", it.key, (char*)it.value);
}
```

## 📎 Credit
This project is a derivative and learning-based reimplementation of:

Ben Hoyt, Build Your Own Hash Table in C

Ben graciously released his work under the public domain. This adaptation is shared in that same spirit — to educate and encourage low-level programming skills.

## 📜 License
This project is released under the terms of the MIT License, with credit to Ben Hoyt for the original tutorial and inspiration.
