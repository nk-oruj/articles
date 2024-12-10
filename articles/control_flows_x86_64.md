
***
# x86-64 Assembly Implementations of Basic Control Flows

Tags: #Assembly 
***

## If Statement

```c
	if (y) {
		a = 1;
	}
```

```asm
	mov    y(%rip), %rax
	test   %ax, %rax
	je     .L1
	
	mov    $1, a(%rip)
.L1:
```

## If...Else Statement

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

## If...Else-If...Else Statement

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

## While Statement

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

## Break Statement (While)

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
	mov     y(%rip), %rax
	test    %rax, %rax
	jne     .L3
.L2:

```

## Continue Statement (While)

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
## Do...While Statement

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