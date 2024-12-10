
***
# x86-64 Assembly and Abstraction Implementations of Basic Control Flows

Tags: #Assembly 
***

## Assembly

- structure of examples
	1. c code for the statement
	2. assembly equivalent
	3. pseudo-code equivalent
	4. (sometimes) pseudo-code restructuring

### If Statement

```c
	if (y) {
		a = 1;
	}
```

```asm
	mov    y(%rip), %rax
	test   %rax, %rax
	je     .L1
	
	mov    $1, a(%rip)
.L1:
```

```pseudo
L1:
	goto L2 if not y;
	...
L2:
```
### If...Else Statement

```c
	if (y) {
		a = 1;
	} else {
		b = 1;
	}
```

```asm
	mov     y(%rip), %rax
	test    %rax, %rax
	je      .L1
	
	mov     $1, a(%rip)
	
	jmp     .L2
.L1:
	mov     $1, b(%rip)
.L2:	
```

```pseudo
L1:
	goto L2 if not y;
	...
	goto L3;
L2:
	...
L3:
```

```
L1:
	L3:
		goto L4 if not y;
		...
		goto L2;
	L4:
	
	...
L2:
```
### If...Else-If...Else Statement

```c
	if (y1) {
		a = 1;
	} else if (y2) {
		b = 1;
	} else if (y3) {
		c = 1;
	} else {
		d = 1;
	}
```

```asm
	mov     y1(%rip), %rax
	test    %rax, %rax
	je      .L1
	
	mov     $1, a(%rip)
	
	jmp     .L2
.L1:
	mov     y2(%rip), %rax
	test    %rax, %rax
	je      .L3
	
	mov     $1, b(%rip)
	
	jmp     .L2
.L3:
	mov     y3(%rip), %rax
	test    %rax, %rax
	je      .L4
	
	mov     $1, d(%rip)
	
	jmp     .L2
.L4:
	mov     $1, %rax
.L2:
```

```pseudo
L1:
	goto L2 if not y1;
	...
	goto L5;
L2:
	goto L3 if not y2;
	...
	goto L5;
L3:
	goto L4 if not y3;
	...
	goto L5;
L4:
	...
L5:
```

```pseudo
L1:
	L3:
		goto L4 if not y1;
		...
		goto L2;
	L4:

	L5:
		goto L6 if not y2;
		...
		goto L2; 
	L6:

	L7:
		goto L8 if not y3;
		...
		goto L2;
	L8:

	...
L2:
```
### While Statement

```c
	while (y) {
		a = 1;
	}
```

```asm
	jmp     .L1
.L2:
	mov     $1, a(%rip)
.L1:
	mov     y(%rip), %rax
	test    %rax, %rax
	jne     .L2
```

```pseudo
L1:
	goto L3;
L2:
	...
L3:
	goto L2 if y;
L4:
```

```pseudo
L1:
	goto L2 if not y;
	...
	goto L1;
L2:
```
### Break Statement (While)

```c
	while (y1) {
		a = 1;
		if (y2) break;
		b = 1;
	}
```

```asm
	jmp     .L1
.L3:
	mov     $1, a(%rip)
	
	mov     y2(%rip), $rax
	test    %rax, %rax
	jne     .L2
	
	mov     $1, b(%rip)
.L1:
	mov     y1(%rip), %rax
	test    %rax, %rax
	jne     .L3
.L2:

```

```pseudo
L1:
	goto L3;
L2:
	...
	goto L4 if y2;
	...
L3:
	goto L2 if y1;
L4:
```

``` pseudo
L1:
	goto L2 if not y1;
	...
	goto L2 if y2;
	...
	goto L1;
L2:
```
### Continue Statement (While)

```c
	while (y1) {
		a = 1;
		if (y2) continue;
		b = 1;
	}
```

```asm
	jmp     .L1
.L3:
	mov     $1, a(%rip)
	
	mov     y2(%rip), %raz
	test    %rax, %rax
	je      .L2

	jmp     .L1
.L2:
	mov     $1, b(%rip)
.L1:
	mov     y1(%rip), %rax
	test    %rax, %rax
	jne     .L3
```

```pseudo
L1:
	goto L4;
L2:
	...

	;; if (y2) continue; else {...}
	L3:
		goto L4 if not y2;
		(...)
		goto L5;
	L4:
		...
	L5:
	;;
	
	goto L2 if y1;
L6:
```

```
L1:
	goto L2 if not y1;
	...
	goto L1 if y2;
	...
	goto L1;
L2:
```
### Do...While Statement

```c
	do {
		a = 1;
	} while (y);
```

```asm
.L1:
	mov     $1, a(%rip)
	
	mov     y(%rip), %rax
	test    %rax, %rax
	jne     .L1
```

```pseudo
L1:
	...
	goto L1 if y;
L2:
```

### For Statement

```c
	for (int i = 0; i < y; i++) {
		a = 1;
	}
```

```asm
	mov     $0, -8(%rip)

	jmp     .L1
.L2:
	mov     $1, a(%rbp)
	add     $1, -8(%rbp)
.L1:
	mov     y(%rip), %rax
	mov     -8(%rbp), %rdx
	
	cmp     %rax, %rdx
	jl      .L2
```

```pseudo
L1:
	i = 0;
	goto L3;
L2:
	...
	i++;
L3:
	goto L2 if eval(i < 8);
L4:
```

```pseudo
i = 0;

L1:
	...
	
	L3:
		i++;
		goto L1 if eval(i < y);
	L4:
L2:
```

## Abstraction

- abstraction of the restructured pseudo-code
	- `with [name] ... end;` is equivalent to pseudo-code `L1: ... L2:`, `L3: ... L4:`, etc. (scoping label pairs)
	- `drop [name];`, `drop [name] if [condition];` is equivalent to pseudo-code `goto L2;`, `goto L2 if [condition];` (the lower label of the scope)
	- `lift [name];`, `lift [name] if [condition]` is equivalent to pseudo-code `goto L1;`, `goto L1 if [condition];` (the higher label of the scope)
	- `drop` and `lift` statements access only those scopes/names, inside of which they are called, and can access no other scope, not even the parallel ones
### If Statement

```pascal
	with Case
		drop Case if not y;
		...
	end;
```

### If...Else Statement

```pascal
	with Cases
		with Case1
			drop Case1 if not y;
			...
			drop Cases;
		end;

		...
	end;
```

### If...Else-If...Else Statement

```pascal
	with Cases
		with Case1
			drop Case1 if not y1;
			...
			drop Cases;
		end;

		with Case2
			drop Case2 if not y2;
			...
			drop Cases;
		end;

		with Case3
			drop Case3 if not y3;
			...
			drop Cases;
		end;

		...
	end;
```

### While Statement

```Pascal
	with Loop
		drop Loop if not y;
		...
		lift Loop;
	end;
```

### Break Statement (While)

```pascal
	with Loop
		drop Loop if not y1;
		...
		drop Loop if not y2;
		...
		lift Loop;
	end;
```

### Continue Statement (While)

```pascal
	with Loop
		drop Loop if not y1;
		...
		lift Loop if not y2;
		...
		lift Loop;
	end;
```

### Do...While Statement

```pascal
	with Loop
		...
		lift Loop if y;
	end;
```

### For Statement

```pascal
	i := 0;
	
	with Loop
		...

		with Step
			i := i + 1;
			drop Loop if not (i < A);
		end;
	end;	
```