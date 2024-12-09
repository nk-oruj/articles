
***
# x86-64 Assembly Basics

Tags: #Assembly
***
## Registers
| **64-bit** | **32-bit** | **16-bit** | **8-bit** | **Name**        | **Expressional Purpose** | **Functional Purpose**    | **Functional Effect** | **Functional Usage** |
| ---------- | ---------- | ---------- | --------- | --------------- | ------------------------ | ------------------------- | --------------------- | -------------------- |
| rax        | eax        | ax         | ah,al     |                 | `1st` integer operand    | return value              | yes                   | carefree             |
| rbx        | ebx        | bx         | bh,bl     |                 | `2nd` integer operand    |                           | no                    | push                 |
| rcx        | ecx        | cx         | ch,cl     |                 | `3rd` integer operand    | `4th` integer argument    | yes                   | carefree             |
| rdx        | edx        | dx         | dh,dl     |                 | `4th` integer operand    | `3rd` integer argument    | yes                   | carefree             |
| rsi        | esi        | si         | sil       | source register | `5th` integer operand    | `2nd` integer argument    | yes                   | carefree             |
| rdi        | edi        | di         | dil       | dest register   | `6th` integer operand    | `1st` integer argument    | yes                   | carefree             |
| rbp        | ebp        | bp         | bpl       | base pointer    |                          | stack frame start pointer | careful               | careful              |
| rsp        | esp        | sp         | spl       | stack pointer   |                          | stack frame end pointer   | careful               | careful              |
| r8         | r8d        | r8w        | r8b       |                 |                          | `5th` integer argument    | yes                   | carefree             |
| r9         | r9d        | r9w        | r9b       |                 |                          | `6th` integer argument    | yes                   | carefree             |
| r10        | r10d       | r10w       | r10b      |                 |                          |                           | yes                   | carefree             |
| r11        | r11d       | r11w       | r11b      |                 |                          |                           | yes                   | carefree             |
| r12        | r12d       | r12w       | r12b      |                 |                          |                           | no                    | push                 |
| r13        | r13d       | r13w       | r13b      |                 |                          |                           | no                    | push                 |
| r14        | r14d       | r14w       | r14b      |                 |                          |                           | no                    | push                 |
| r15        | r15d       | r15w       | r15b      |                 |                          |                           | no                    | push                 |
## Instructions
| **Arithmetic**                                                                                                | **Logic**                                                                                                                                                                              | **Jumps**                                                                                                                            | **Stack**                                             |
| ------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------- |
| add ⟨dest⟩ ⟨src⟩  <br>sub ⟨dest⟩ ⟨src⟩  <br>inc ⟨dest⟩  <br>dec ⟨dest⟩  <br>imul ⟨dest⟩ ⟨src⟩  <br>div ⟨dest⟩ | and ⟨dest⟩ ⟨src⟩  <br>or ⟨dest⟩ ⟨src⟩  <br>not ⟨dest⟩  <br>shr ⟨dest⟩, ⟨imm⟩  <br>shr ⟨dest⟩, cl  <br>shl ⟨dest⟩, ⟨imm⟩  <br>shl ⟨dest⟩, cl  <br>sar ⟨dest⟩, ⟨imm⟩  <br>sar ⟨dest⟩, cl | jmp ⟨label⟩  <br>cmp ⟨dest⟩ ⟨src⟩  <br>je ⟨label⟩  <br>jne ⟨label⟩  <br>jg ⟨label⟩  <br>jge ⟨label⟩  <br>jl ⟨label⟩  <br>jle ⟨label⟩ | call ⟨label⟩  <br>ret  <br>push ⟨src⟩  <br>pop ⟨dest⟩ |
## Notes
1. for 7 or more integer arguments use the stack
2. for floating point number arguments use %xmm0-%xmm7
## References
- [https://math.hws.edu/eck/cs220/f22/registers.html]()
- https://wiki.osdev.org/System_V_ABI
- https://courses.cs.washington.edu/courses/cse378/10au/sections/Section1_recap.pdf
- https://cs61.seas.harvard.edu/site/2018/Asm2/