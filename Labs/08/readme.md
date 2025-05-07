## Question-1:
```.asm
include irvine32.inc

.data
	input dword 4 dup(?)
	msg1 byte "Enter any 4 integers: ", 0
	msg2 byte "All the integers are equal", 0
	msg3 byte "Integers are not equal", 0

.code
main proc
	mov edx, offset msg1
	call writestring
	call crlf
	mov ecx, 4
	mov esi, offset input
	input_loop:
		call readint
		mov [esi], eax
		add esi, 4
	loop input_loop

	mov ecx, 3
	mov esi, offset input 
	mov eax, [esi]
	equal_loop:
		add esi, 4
		cmp eax, [esi]
		jne not_equal
	loop equal_loop
	mov edx, offset msg2
	call writestring
	call crlf
	jmp end_loop

	not_equal:
		mov edx, offset msg3
		call writestring
		call crlf 
		jmp end_loop

	end_loop:
		exit
		main endp
		end main

```
#### If the integers are equal:
![image](https://github.com/user-attachments/assets/d7cd6acf-b18a-4084-96d9-a2bca555a880)


#### If the integers are not equal:
![image](https://github.com/user-attachments/assets/eb072948-f866-4b86-b3d8-bbb7dcc34922)


## Question-2:
```.asm
include irvine32.inc

.data
	array sword 0, 0, 0, 150, 120, 35, -12, 66, 4, 0
	msg1 byte "First non-zero value is: ", 0

.code
main proc
	mov ecx, lengthof array / 2
	mov esi, offset array
	mov ax, [esi]
	non_zero_loop:
		add esi, 2
		cmp ax, [esi]
		jnz found
		mov ax, [esi]
	loop non_zero_loop
	jmp end_main

	found:
		mov edx, offset msg1
		call writestring
		movzx eax, word ptr [esi]
		call writeint
		call crlf
		jmp end_main

	end_main:
		exit
		main endp
		end main
```
![image](https://github.com/user-attachments/assets/c83bdcdd-1a84-4547-9090-1d5e684b41c5)


## Question-3:
```.asm
include irvine32.inc

.data
	array dword 0, 0, 0, 150, 120, 35, -12, 66, 4, 0
	var dword 5
	x dword ?
	msg1 byte "value of x is: ", 0

.code
main proc
	mov ecx, lengthof array  ;ecx = 10
	mov edx, var		
	add edx, 1				 ; edx = 6

	cmp var, ecx			
	jc another_check
	jmp else_value
	

	another_check:
		cmp ecx, edx
		jnc final
		jmp else_value

	final:
		mov ebx, 0
		mov x, ebx
		jmp end_main

	else_value:
		mov ebx, 1
		mov x, ebx
		jmp end_main

	end_main:
		mov edx, offset msg1
		call writestring
		mov eax, x
		call writeint
		call crlf
		exit
		main endp
		end main
```

![image](https://github.com/user-attachments/assets/aeafe16d-096f-4fe7-b747-5b2df50bf41a)


## Question-4:
```.asm
include irvine32.inc

.data
	var dword 0
	msg1 byte "Hello ", 0
	msg2 byte "World ", 0

.code
main proc
	;desination < source --> cf = 1
	mov eax, var
	
	while_loop:
		cmp eax, 10
		ja end_while

		cmp eax, 5
		jnl else_block
		mov edx, offset msg1
		call writestring
		call crlf
		add eax, 1
		jmp while_loop

		else_block:
			mov edx, offset msg2
			call writestring
			call crlf
			add eax, 1
			jmp while_loop

end_while:
	exit
main endp
end main
```
![image](https://github.com/user-attachments/assets/73355b7a-b519-4e5c-9138-f2dcc280a18f)


## Question-5:
```.asm
include irvine32.inc

.data
	arr WORD 10, 4, 7, 14, 299, 156, 3, 19, 29, 300, 20
	msg1 byte "Found ", 0
	msg2 byte "Not found ", 0
	input byte "Enter any integer: ", 0

.code
main proc
	mov ecx, lengthof arr 
	mov esi, offset arr
	print:
		movzx eax, word ptr [esi]
		call writeint
		add esi, 2
		mov eax, 32
		call writechar
		loop print

	;taking input
	call crlf
	mov edx, offset input
	call writestring
	call readint

	mov ecx, lengthof arr
	mov esi, 0
	find_loop:
		cmp ax, arr[esi]
		jz found
		add esi, 2
		loop find_loop
	jmp not_found

	found:
		mov edx, offset msg1
		call writestring
		call crlf
		jmp end_main

	not_found:
		mov edx, offset msg2
		call writestring
		call crlf
		jmp end_main

end_main:	
	exit
	main endp
	end main
```
![image](https://github.com/user-attachments/assets/838c844f-5948-4080-944e-70d26a54cfcc)
![image](https://github.com/user-attachments/assets/98243f70-1fa3-40e7-9d93-ca1b07efef23)

## Question-6:
```.asm
include irvine32.inc

.data
	arr WORD 10, 4, 7, 14, 299, 156, 3, 19, 29, 300, 20
	count dword ?

.code
main proc
	mov ecx, lengthof arr - 1
	outer_loop:
		mov count, ecx
		mov esi, 0
		mov edi, type arr
		mov ecx, lengthof arr - 1

		inner_loop:
			mov ax, arr[edi]
			cmp ax, arr[esi]
			jge no_swap
			xchg ax, arr[esi]
			mov arr[edi], ax

			no_swap:
				add esi, type arr
				add edi, type arr
				loop inner_loop

		mov ecx, count
		loop outer_loop

	mov ecx, lengthof arr
	mov esi, 0
	print_loop:
		movzx eax, arr[esi]
		call writedec
		add esi, type arr
		mov eax, 32
		call writechar

		loop print_loop
	
	call crlf

	exit
	main endp
	end main
```
![image](https://github.com/user-attachments/assets/f19c2be3-0f20-4f4e-83d4-ba7597122751)

## Question-7:
```.asm
include irvine32.inc

.data
	arr byte "Monday", 0, 0, 0, 0,
			 "Tuesday", 0, 0, 0,
			 "Wednesday", 0,
			 "Thursday", 0, 0,
			 "Friday", 0, 0, 0, 0,
			 "Saturday", 0, 0,
			 "Sunday", 0, 0, 0, 0
	

.code
main proc
	call readint
	mov ebx, 10
	imul ebx
	mov ebx, eax
	sub ebx, 10
	mov eax, ebx

	mov esi, ebx
	mov ecx, 10
	call crlf
	print_loop:
		movzx eax, arr[esi]
		inc esi
		call writechar
		loop print_loop

	

	exit
	main endp
	end main
```
![image](https://github.com/user-attachments/assets/c0b9d91a-b336-4555-9560-5509bb94e52a)

## Question-8:
```.asm
include irvine32.inc

.data
	msg1 byte "Entered input is an alphabet", 0
	msg2 byte "Entered input is NOT an alphabet", 0
	

.code
main proc
	call readchar
	call writechar
	call crlf
	cmp al, "A"
	jl lower_check
	cmp ah, "Z"
	jle is_alpha

	lower_check:
		cmp al, "a"
		jl not_alpha
		cmp al, "z"
		jle is_alpha

	is_alpha:
		mov edx, offset msg1
		call writestring
		call crlf
		jmp end_main

	not_alpha:
		mov edx, offset msg2
		call writestring
		call crlf

end_main:
	exit
	main endp
	end main
```
![image](https://github.com/user-attachments/assets/062b7695-b876-461e-a548-9ed88001bca4)
![image](https://github.com/user-attachments/assets/67c50e9a-e338-437d-b02f-7cb1d57754cf)

