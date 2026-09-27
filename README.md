# C++ Forum Management System

A C++ Object-Oriented Programming (OOP) project demonstrating custom dynamic memory management, operator overloading, deep copying, and class aggregation through a simulated forum system interface.

\---

## 📋 Overview

This repository contains a full C++ implementation of a console-based **Forum Management System**. The application models real-world forum structures—including users (**Clan**), posts (**Post**), forum categories (**Sekcija**), dates (**Datum**), and the overarching platform (**Forum**)—without using the C++ Standard Template Library (STL) containers for primary data structures.

This project serves as an educational reference for understanding foundational OOP principles, manual heap allocation, static class members, deep copy mechanics, and operator overloading.

\---

## ✨ Features \& Concepts

* **Manual Memory Management**: Utilizes pointers, dynamic arrays (`new`, `delete\[]`), and customized deep copying techniques.
* **Rule of Three / Five Implementation**: Proper definitions for constructors, copy constructors, assignment operators (`operator=`), and destructors to prevent memory leaks and dangling pointers.
* **Operator Overloading**:

  * Date arithmetic and comparison operators (`+`, `-`, `>`, `<`, `==`, `!=`, `>=`, `<=`).
  * Stream insertion operators (`<<`) for friendly output formatting.
* **Static Class Members**: Auto-incrementing unique IDs for members and forum posts using `static` counters.
* **Dynamic Array Resizing**: Dynamic array expansion (`expandClanovi`) when capacity limits are reached.
* **Interactive Console Menu**: Standard CLI menu allowing testing of individual components (`zadatak1` through `zadatak5`).

\---

## 🏗️ Architecture \& Class Overview

```
                          ┌─────────────┐
                          │    Forum    │
                          └──────┬──────┘
                                 │
                 ┌───────────────┴───────────────┐
                 │ 1..\*                          │ 1..\*
          ┌──────▼──────┐                 ┌──────▼──────┐
          │   Sekcija   │                 │    Clan     │
          └──────┬──────┘                 └──────┬──────┘
                 │ 1..\*                          │ 1
          ┌──────▼──────┐                 ┌──────▼──────┐
          │    Post     │───────────────► │    Datum    │
          └──────┬──────┘                 └─────────────┘
                 │ 1
                 ▼
          ┌─────────────┐
          │    Datum    │
          └─────────────┘
```

### 1\. `Datum` (Date Management)

* Manages heap-allocated integers for day, month, and year (`int\* \_dan`, `int\* \_mjesec`, `int\* \_godina`).
* Supports leap year checks, days-per-month calculation, date comparison, and date arithmetic (e.g., adding days `d1 + 30`, calculating differences `d1 - d2`).

### 2\. `Clan` (User / Member)

* Represents a forum user with a unique immutable ID (`\_clanId`), username, password, gender, and registration date (`Datum`).
* Auto-assigns unique IDs using static variable `\_brojacClanova`.

### 3\. `Post` (Forum Post)

* Represents a user post containing a unique ID (`\_postId`), author username, creation date, and post body.
* Uses dynamic string allocation and static integer-to-string ID generation via `\_itoa\_s` / `intToStr`.

### 4\. `Sekcija` (Forum Section / Category)

* Groups related posts using an array of pointers to `Post` objects (`Post\* \_postovi\[100]`).
* Supports adding new posts dynamically with capacity checks.

### 5\. `Forum` (Main System Orchestrator)

* Top-level object holding fixed-size section slots (`Sekcija \_sekcije\[20]`) and a dynamically resizable array of members (`Clan\* \_clanovi`).
* Implements `expandClanovi(int uvecanje)` to reallocate and copy member arrays when capacity is exceeded.

\---

## 🛠️ Utility Functions

The project includes standalone helper utilities:

* `alocirajTekst(const char\* tekst)`: Dynamically allocates memory and copies raw strings safely.
* `izracunajBrojZnamenki(int broj)`: Computes the number of digits in an integer using $\\lfloor \\log\_{10}(|x|) \\rfloor + 1$.
* `intToStr(int broj)`: Converts integers to dynamically allocated character arrays.
* `prijestupnaGodina(int godina)`: Determines leap years based on standard Gregorian rules.
* `getBrojDanaUMjesecu(int mjesec, int godina)`: Returns total days for a given month/year combination.

\---

## 🚀 Getting Started

### Prerequisites

* A C++11 (or newer) compatible compiler:

  * **MSVC** (Visual Studio 2019/2022) — *Recommended (uses MSVC-specific CRT security functions like `strcpy\_s` and `\_itoa\_s`)*
  * **GCC / Clang** (via MinGW or Linux with MSVC CRT extensions or standard function wrappers)

### Building and Running

#### Using Microsoft Visual Studio:

1. Open Visual Studio.
2. Create a new C++ Console Application project.
3. Replace `main.cpp` with the provided source code.
4. Build (`Ctrl + Shift + B`) and Run (`Ctrl + F5`).

#### Using GCC / g++ (Command Line):

> \*\*Note:\*\* If compiling with GCC/Clang, ensure support for CRT safe string functions or replace `strcpy\_s` and `\_itoa\_s` with standard C string functions (`strncpy`/`snprintf`).

```bash
g++ -std=c++11 -o forum\_app main.cpp
./forum\_app
```

\---

## 🎮 Interactive Menu

Upon launching the executable, you will be presented with a menu to select test cases:

```text
::Zadaci::
(1) zadatak 1 - Test Date class \& Date arithmetic
(2) zadatak 2 - Test Member (Clan) creation \& comparison
(3) zadatak 3 - Test Post creation \& ID generation
(4) zadatak 4 - Test Section (Sekcija) \& Post aggregation
(5) zadatak 5 - Test Full Forum functionality \& Dynamic array expansion
```

\---

