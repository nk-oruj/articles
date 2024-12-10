
***
# x86-64 Assembly Basics

Tags: #Assembly
***
## Registers (with Conventions)

| **64-bit** | **32-bit** | **16-bit** | **8-bit** | **Name**      | **Functional Purpose**    | **Functional Effect** | **Functional Usage** |
| ---------- | ---------- | ---------- | --------- | ------------- | ------------------------- | --------------------- | -------------------- |
| rax        | eax        | ax         | ah,al     |               | return integer value      | yes                   | carefree             |
| rbx        | ebx        | bx         | bh,bl     |               |                           | no                    | push                 |
| rcx        | ecx        | cx         | ch,cl     |               | `4th` integer argument    | yes                   | carefree             |
| rdx        | edx        | dx         | dh,dl     |               | `3rd` integer argument    | yes                   | carefree             |
| rsi        | esi        | si         | sil       | src register  | `2nd` integer argument    | yes                   | carefree             |
| rdi        | edi        | di         | dil       | dest register | `1st` integer argument    | yes                   | carefree             |
| rbp        | ebp        | bp         | bpl       | base pointer  | stack frame start pointer | careful               | careful              |
| rsp        | esp        | sp         | spl       | stack pointer | stack frame end pointer   | careful               | careful              |
| r8         | r8d        | r8w        | r8b       |               | `5th` integer argument    | yes                   | carefree             |
| r9         | r9d        | r9w        | r9b       |               | `6th` integer argument    | yes                   | carefree             |
| r10        | r10d       | r10w       | r10b      |               |                           | yes                   | carefree             |
| r11        | r11d       | r11w       | r11b      |               |                           | yes                   | carefree             |
| r12        | r12d       | r12w       | r12b      |               |                           | no                    | push                 |
| r13        | r13d       | r13w       | r13b      |               |                           | no                    | push                 |
| r14        | r14d       | r14w       | r14b      |               |                           | no                    | push                 |
| r15        | r15d       | r15w       | r15b      |               |                           | no                    | push                 |
## Basic Instructions
| **Arithmetic**                                                                                                | **Logic**                                             | **Jumps**                                                                                                                                                | **Stack**                                             |
| ------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| add (src), (dest)  <br>sub (src), (dest)  <br>inc (dest)  <br>dec (dest)  <br>imul (src), (dest)  <br>div (dest) | and (src), (dest)  <br>or (src), (dest)  <br>not (dest) | jmp (label)<br>test (src), (dest)<br>cmp (src), (dest)  <br>je (label)  <br>jne (label)  <br>jg (label)  <br>jge (label)  <br>jl (label)  <br>jle (label) | call (label)  <br>ret  <br>push (src)  <br>pop (dest) |
## Notes
1. for 7 or more integer arguments use the stack
2. for floating point number arguments use %xmm0-%xmm7
3. %rip - instruction pointer
## References
- [https://math.hws.edu/eck/cs220/f22/registers.html]()
- https://wiki.osdev.org/System_V_ABI
- https://courses.cs.washington.edu/courses/cse378/10au/sections/Section1_recap.pdf
- https://cs61.seas.harvard.edu/site/2018/Asm2/