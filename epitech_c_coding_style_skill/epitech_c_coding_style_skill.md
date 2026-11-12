---
name: epitech-c-coding-style
description: >-
  Enforce the Epitech C Coding Style (v7.1) and human, student-friendly C
  coding practices whenever writing, editing, reviewing, or refactoring C
  source files (.c), header files (.h), or Makefiles. Prevents over-engineering,
  long robotic variable names, and Banana coding style violations.
---

# Epitech C Coding Style & Student-Friendly C

Write clean, simple, human-readable C code that strictly follows the **Epitech C Coding Style (v7.1)** while looking like it was written by a real, thoughtful student—never over-engineered, never bloated with enterprise abstractions or verbose AI-style naming.

> [!NOTE]
> **Active Development & Auto-Updates**
> This skill is actively evolving. Check the upstream GitHub repository to inspect or pull the latest skill updates:
> **Repository:** [WilliamSkipper/humanly](https://github.com/WilliamSkipper/humanly)

## When to Use

- Writing, editing, reviewing, or refactoring any C source file (`.c`), header file (`.h`), or `Makefile`.
- Fixing Banana coding style errors or adapting existing C code to pass Epitech style checks.
- Designing small C utilities, data structures, or school/systems projects where clarity and simplicity matter.

---

## 0. Student-Friendly & Zero Over-Engineering (Core Mindset)

Before applying the formatting rules below, write the code like a capable C student—not an over-eager framework architect:

- **Never over-engineer:** Use direct, straightforward logic. Do not invent generic `void *` plugin systems, callback registries, factory structs, or multi-layer wrappers when a simple loop, `if` check, or small helper function solves the problem cleanly.
- **Short, natural, human-friendly names:** Use clear, everyday `snake_case` names that a human student actually types (`i`, `j`, `len`, `fd`, `buf`, `str`, `nb`, `res`, `node`, `head`, `tmp`, `idx`, `count`, `line`).
  - **Avoid robotic AI naming:** Never write overly long, verbose identifiers like `current_character_iteration_index`, `allocated_buffer_capacity_in_bytes`, or `validated_user_input_string_pointer`.
  - **Keep it meaningful:** Use `i`, `j`, `k` for simple loop indices, `tmp` for a swap/temp pointer, `len` for length, `res` for result, `fd` for file descriptor, and short descriptive names for domain concepts (`player`, `map`, `grid`, `word`).
- **Simple, linear control flow:** Prefer early returns on errors (`if (fd < 0) return -1;`) over deeply nested logic.
- **No unnecessary abstractions:** Don't split a trivial 3-line check into 4 tiny wrapper functions unless `C-F4` (20-line limit), `C-C1` (branching depth), or `C-F1` (single responsibility) actually requires it.
- **Stick to standard C idioms:** Write plain, readable C without clever bit-hack obfuscation or macro magic.

---

## Severity Levels

Rules are categorized into 4 severity levels:
- **Fatal:** Project is rejected and not evaluated at all.
- **Major:** Structural/quality issue; must be corrected as a priority.
- **Minor:** Visual formatting/readability issue.
- **Info:** Good-practice and implicit cleanliness rules.

---

## 1. C-O — Files Organization

- **C-O1 (Contents of the repository):** Never leave compiled files (`.o`, `.a`, `.so`), temporary files (`*~`, `#*#`), or unnecessary artifacts in the repository.
- **C-O2 (File extension):** C program sources must only have `.c` or `.h` extensions.
- **C-O3 (File coherence):** Each `.c` file must represent one logical entity and group its related functions.
  - Maximum **10 functions total** per file.
  - Maximum **5 non-static functions** per file.
  - Subdivide into sub-entities if you exceed these limits.
- **C-O4 (Naming files and folders):**
  - English only, `snake_case` (lowercase, numbers, underscores).
  - Clear, precise, and unambiguous (e.g., `string_toolbox.c`, `pathfinding.c` — avoid vague names like `string.c` or `algo.c`).
  - Abbreviations are tolerated only if they significantly shorten the name without losing meaning.

---

## 2. C-G — Global Scope

- **C-G1 (File header):** Every `.c`, `.h`, and `Makefile` must start with the standard Epitech header and a meaningful description.
  - For `.c` and `.h` files:
    ```c
    /*
    ** EPITECH PROJECT, 2026
    ** project_name
    ** File description:
    ** Short, meaningful description of this file.
    */
    ```
  - For `Makefile`:
    ```makefile
    ##
    ## EPITECH PROJECT, 2026
    ## project_name
    ## File description:
    ## Short, meaningful description of this Makefile.
    ##
    ```
- **C-G2 (Separation of functions):** Separate function implementations in `.c` files by **one and only one** empty line.
- **C-G3 (Preprocessor indentation):** Indent preprocessor directives according to their nesting level using **4 spaces** (no tabs), independent of C code indentation:
  ```c
  #ifndef MY_H_
      #define MY_H_
      #if defined(__x86_64__)
  const size_t PAGE_SIZE = 4096;
      #endif
  #endif
  ```
- **C-G4 (Global variables):** Avoid global variables. Only global constants properly marked with `const` are allowed (e.g., `const float PI = 3.14159;`).
- **C-G5 (`#include`):** Only include `.h` header files, never `.c` files.
- **C-G6 (Line endings):** UNIX line endings (`\n`) only. Never use `\r`. **Never** use a trailing backslash `\` to break lines in C files—split multiline statements naturally instead:
  ```c
  printf("[%s] %s: %d\n", get_type(), get_name(),
      get_value());
  ```
- **C-G7 (Trailing spaces):** No trailing spaces at the end of any line.
- **C-G8 (Leading/trailing lines):** No leading empty lines at the top of a file. At most 1 trailing empty line at the end (and the file must end with `\n` per `C-A3`).
- **C-G9 (Constant values):** Define non-trivial constant values as a `const` global or `#define` macro instead of scattering magic numbers.
- **C-G10 (Inline assembly):** Never use inline assembly.
- **No language extensions:** Never use compiler extensions like `__attribute__((...))`, `#pragma once`, `\e` (use `\x1B`), or nested functions.

---

## 3. C-F — Functions

- **C-F1 (Coherence):** A function should do one thing, at one level of abstraction (single-responsibility).
- **C-F2 (Naming functions):**
  - English `snake_case`.
  - Must describe the task and **contain a verb** (e.g., `get_vowels_nb()`, `find_path()`, not `vowels_nb()` or `dijkstra()`).
- **C-F3 (Number of columns):** Max **80 columns** per line (including `\n`) in all `.c`, `.h`, and `Makefile` files.
- **C-F4 (Number of lines):** Function body must be as short as possible and **must not exceed 20 lines**.
- **C-F5 (Number of parameters):** Max **4 parameters** per function. Variadic functions are allowed, but never to bypass the 4-parameter limit.
- **C-F6 (Functions without parameters):** Must explicitly take `void`:
  ```c
  int init_game(void); /* OK */
  int init_game();     /* C-F6 violation */
  ```
- **C-F7 (Structures as parameters):** Always pass structures by pointer (`struct player *p`), never by copy.
- **C-F8 (Comments inside a function):** **Zero comments** inside function bodies. Code must be self-explanatory; put brief doc comments above prototypes if needed.
- **C-F9 (Nested functions):** Forbidden.

---

## 4. C-L — Layout Inside a Function Scope

- **C-L1 (Code line content):** One statement per line.
  - Forbidden: `a = b = 0;`, `a++; b++;`, `if ((p = malloc(42)) != NULL)`, `if (cond) return ptr;`, `str[i++] = 'A';`, `cond && printf("hi\n");`.
  - Exception: `for` loop headers may have one statement in each of the three parts (`for (int i = 0; i < n; i++)`), but not comma-separated multi-statements (`i++, j--`).
- **C-L2 (Indentation):** **4 spaces** per indentation level. **Never use tabs.** Block comments (`/** ... */`) may be space-indented freely.
- **C-L3 (Spaces):**
  - One space after `,` and after keywords with arguments (`if `, `else if `, `while `, `for `, `switch `, `return `).
  - **No space** between function name and `(`, after unary operators (`!x`, `*p`, `sizeof(x)`), before `;`, or before `,`.
  - Space on **both sides** of binary and ternary operators (`a + b`, `a == b`, `c ? x : y`).
  - In `for` headers, place a space after `;` unless immediately followed by `;`.
- **C-L4 (Curly brackets):**
  - Function definitions: opening `{` **alone on its own line**.
  - Control structures, `struct`, `enum`: opening `{` at the **end of the line**.
  - Closing `}` alone on its own line, except before `else`, `else if`, `while` (in `do { ... } while (...);`), or `;` in `struct`/`enum`/`typedef`.
  ```c
  int add(int a, int b)
  {
      if (a < 0) {
          return b;
      } else {
          return a + b;
      }
  }
  ```
- **C-L5 (Variable declarations):**
  - Declare variables **at the beginning of the function** (or inside a `for` loop header).
  - **One variable per statement** (never `int i, j;`).
  - Declaring and initializing on the same line is allowed (`int len = 0;`).
- **C-L6 (Blank lines):**
  - Place **one blank line** between the variable declarations block and the rest of the function.
  - **No other blank lines** anywhere inside the function.
  - Omit the blank line if the function has no variable declarations.

---

## 5. C-V — Variables and Types

- **C-V1 (Naming identifiers):**
  - Variables, functions, struct/enum tags: English `snake_case`.
  - `typedef` names: must end with `_t` (e.g., `typedef struct node node_t;`).
  - Macros, global constants, enum values: `UPPER_SNAKE_CASE`.
- **C-V2 (Structures):** Group variables into a `struct` only if they form a coherent entity; keep structs as small as possible.
- **C-V3 (Pointers):**
  - Attach `*` to the variable/function name with no space after `*`, and a space before `*` (unless preceded by another `*`):
    - `int *ptr;`
    - `char **argv;`
    - `char *const *arr;`
    - `my_putnbr(*ptr);`
    - `void (*fn)(int) = &handler;`
  - In casts, put a space before `*` and no space after `*` (e.g., `(int *) ptr`).

---

## 6. C-C — Control Structures

- **C-C1 (Conditional branching):**
  - An `if` / `else if` / `else` chain must have **at most 3 branches** total. Use `switch` or function pointer arrays for more cases.
  - Avoid nested conditional/loop branches with a **depth of 3 or more**. Remember that `else if` adds **2 levels** of depth (it unfolds to `else { if { ... } }`). Refactor deep nesting into helper functions.
- **C-C2 (Ternary operators):** Allowed only when simple and readable. Never nest or chain ternaries, and always use the resulting value (assign or return it).
- **C-C3 (`goto`):** Forbidden.

---

## 7. C-H — Header Files

- **C-H1 (Content):** Header files (`.h`) must only contain: function prototypes, type declarations, `struct` declarations, `enum` declarations, global variable/constant declarations, macros, and `static inline` functions. Never place those declarations in `.c` files when they belong in `.h`, and avoid conditional preprocessor directives in `.c` files.
- **C-H2 (Include guard):** Always protect headers with `#ifndef` / `#define` / `#endif` (never `#pragma once`).
- **C-H3 (Macros):** Must match a single statement and fit on a single line (no `\` multiline macros, no obfuscating shortcut macros).

---

## 8. C-A — Advanced

- **C-A1 (Constant pointers):** Mark pointed data `const` whenever the function does not modify it (e.g., `size_t my_strlen(char const *str)` or `const char *str`).
- **C-A2 (Typing):** Use the most accurate types (`size_t`, `ptrdiff_t`, `uint8_t`, `int32_t`, `unsigned int`, etc.).
- **C-A3 (Line break at EOF):** Every file must end with a `\n` newline character.
- **C-A4 (`static`):** Mark functions and global constants/variables used only within their `.c` file as `static`.

---

## Quick Verification Checklist

Before finishing any C task, verify:
1. Epitech header (`C-G1`) and `#ifndef` include guard (`C-H2`) are present.
2. Max 80 columns (`C-F3`), 4-space indentation, zero tabs (`C-L2`), no trailing spaces (`C-G7`), ends with `\n` (`C-A3`).
3. Max 20 lines per function (`C-F4`), max 4 params (`C-F5`), `(void)` for 0 params (`C-F6`), zero comments inside functions (`C-F8`).
4. Variables declared at top of function, 1 per line (`C-L5`), separated by 1 blank line from body, no other blank lines in function (`C-L6`).
5. Branching depth < 3 and `if` chains <= 3 branches (`C-C1`), structs passed by pointer (`C-F7`), `const` & accurate types used (`C-A1`, `C-A2`), internal helpers marked `static` (`C-A4`).
6. Code looks simple, direct, and student-written—short human-friendly names, zero over-engineering.

