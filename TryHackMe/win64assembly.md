# TryHackMe Notes: Windows x64 Assembly (win64assembly)

## 📌 Room Overview
This room provides a foundational understanding of Windows x64 Assembly language. Knowledge of x64 assembly is crucial for reverse engineering, malware analysis, and exploit development. It bridges the gap between high-level code (like C/C++) and the machine code executed by the CPU.

---

## Task 1 & 2: Introduction to Architecture and Registers
At the core of the CPU are **Registers**—small, extremely fast storage locations used to perform operations. In x64 architecture, general-purpose registers are 64 bits wide.

### Key 64-bit Registers
* **RAX:** Accumulator register (used for arithmetic and storing return values of functions).
* **RBX:** Base register (often used as a base pointer for memory access).
* **RCX:** Counter register (used for loop counters and the 1st argument in Windows x64 calling convention).
* **RDX:** Data register (used in I/O operations and the 2nd argument in Windows x64 calling convention).
* **RSI:** Source Index (used for string/memory copy operations).
* **RDI:** Destination Index (used for string/memory copy operations).
* **RSP:** Stack Pointer (points to the top of the stack).
* **RBP:** Base Pointer (points to the base of the current stack frame).
* **R8 - R15:** Additional general-purpose registers introduced in x64.
* **RIP:** Instruction Pointer (points to the memory address of the *next* instruction to be executed).

*Note: You can access smaller portions of these registers. For example, `RAX` (64-bit) -> `EAX` (32-bit) -> `AX` (16-bit) -> `AL` (lower 8-bit).*

---

## Task 3: Basic Instructions (Data Movement & Arithmetic)
Assembly instructions generally follow the syntax: `INSTRUCTION DESTINATION, SOURCE` (Intel syntax).

* `MOV dest, src`: Copies data from `src` to `dest`.
  * *Example:* `MOV RAX, 5` (Puts the value 5 into RAX).
* `LEA dest, src`: Load Effective Address. Loads the *memory address* of the source into the destination, not the value at that address.
  * *Example:* `LEA RAX, [RBX+8]` (Calculates RBX+8 and stores that address in RAX).
* `ADD dest, src`: Adds `src` to `dest` and stores the result in `dest`.
* `SUB dest, src`: Subtracts `src` from `dest`.
* `INC dest` / `DEC dest`: Increments (+1) or Decrements (-1) the destination.

---

## Task 4: The Stack
The Stack is a region of memory used for temporary storage, local variables, and managing function calls. It operates on a **LIFO** (Last-In, First-Out) principle.
* The stack grows **downward** in memory (from higher addresses to lower addresses).
* **RSP (Stack Pointer)** constantly updates to point to the top of the stack.

### Stack Instructions
* `PUSH operand`: Subtracts 8 from RSP (in x64) and places the operand at the new RSP address.
* `POP operand`: Retrieves the value at RSP, stores it in the operand, and adds 8 to RSP.

---

## Task 5: Control Flow
Programs rarely execute in a straight line. Control flow instructions alter the `RIP` (Instruction Pointer) to jump to different parts of the code.

* `CMP arg1, arg2`: Compares two values by subtracting arg2 from arg1. It doesn't store the result but updates the **RFLAGS** register (like the Zero Flag, ZF).
* `TEST arg1, arg2`: Performs a bitwise AND. Used often to check if a register is zero (`TEST RAX, RAX`).

### Jumping (Branching)
* `JMP address`: Unconditional jump. Always jumps to the address.
* `JE` / `JZ`: Jump if Equal / Jump if Zero (ZF = 1).
* `JNE` / `JNZ`: Jump if Not Equal / Jump if Not Zero (ZF = 0).
* `JG` / `JL`: Jump if Greater / Jump if Less (used for signed comparisons).
* `JA` / `JB`: Jump if Above / Jump if Below (used for unsigned comparisons).

---

## Task 6: Windows x64 Calling Convention (Fastcall)
When one function calls another, they must agree on how to pass arguments and return values. Windows x64 uses a specific convention known as **Microsoft x64 calling convention**:

1. **Arguments 1 to 4** are passed in specific registers (in this exact order):
   * 1st Arg: `RCX`
   * 2nd Arg: `RDX`
   * 3rd Arg: `R8`
   * 4th Arg: `R9`
2. **Additional Arguments (5+)** are pushed onto the **Stack** (pushed right-to-left so arg 5 is at the top).
3. **Return Value:** The function places its return value in the `RAX` register.
4. **Shadow Space:** The caller must allocate 32 bytes (4 words) of "shadow space" on the stack just before calling the function, giving the called function space to save RCX, RDX, R8, and R9 if needed.

### Function Calls
* `CALL address`: Pushes the current `RIP` (return address) onto the stack and jumps to the function address.
* `RET`: Pops the return address off the stack and loads it into `RIP`, returning control to the calling function.

---

## Summary (Cheat Sheet)
| Instruction/Concept | Description |
| :--- | :--- |
| **RAX** | Return value register |
| **RCX, RDX, R8, R9** | First 4 function arguments (Win64) |
| **RSP** | Stack Pointer (Top of stack) |
| **RIP** | Instruction Pointer (Next instruction) |
| **MOV vs LEA** | MOV gets the *value*; LEA gets the *address* |
| **Stack Growth** | Grows towards lower memory addresses |