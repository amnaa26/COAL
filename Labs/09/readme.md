## Question-1:
```.asm
include irvine32.inc

.data
	

.code
	ThreeProd proc
		push ebp
		mov ebp, esp
		mov eax, [ebp+8]
		mov ebx, [ebp+12]
		mul ebx
		mov ebx, [ebp+16]
		mul ebx
		call writedec
		call crlf
		pop ebp
		ret 16
	ThreeProd endp


main proc
	push 2
	push 4
	push 5

	call ThreeProd

	exit
	main endp
	end main
```
![image](https://github.com/user-attachments/assets/5831a46e-4722-4c0e-904d-bed2f6b41595)

## Question-2:
```.asm
include irvine32.inc

.data
	arr dword 23, 87, 5, 44, 66, 12, 91, 38, 70, 1, 56, 14, 79, 3, 33, 99, 25, 60, 7, 41
	msg1 byte "Minimum value: ", 0
	msg2 byte "Maximum value: ", 0

.code
	MinMaxArray proc
		push ebp
		mov ebp, esp
		mov ecx, [ebp+8]
		dec ecx
		mov esi, [ebp+12]
		mov eax, [esi]
		mov ebx, [esi]
		min_max_loop:
			cmp eax, [esi + 4]		;eax---> minimum
			jg minimum_found
			trying_maximum:
				cmp ebx, [esi+4]	;ebx--->maximum
				jl maximum_found
				jmp going_back
			minimum_found:
				mov eax, [esi+4]
				jmp trying_maximum
			maximum_found:
				mov ebx, [esi+4]
			going_back:
				add esi, 4
				loop min_max_loop
		
		pop ebp
		ret 12
	MinMaxArray endp


main proc
	push offset arr
	push lengthof arr
	call MinMaxArray
	mov edx, offset msg1
	call writestring
	call writedec
	call crlf
	mov edx, offset msg2
	call writestring
	mov eax, ebx
	call writedec
	call crlf
	exit
	main endp
	end main
```
![image](https://github.com/user-attachments/assets/f0e6700b-fb6f-4b8b-a0c6-e42a0bf11c24)

## Question-3:
```.asm
include irvine32.inc

.data
	msg1 byte "Enter a value: ", 0

.code
	LocalSquare proc
		ENTER 4, 0
		mov edx, offset msg1
		call writestring
		call readint
		mov [ebp-4], eax
		mul eax
		mov [ebp-4], eax
		call writedec
		
		LEAVE
		ret 4
	LocalSquare endp


main proc
	call LocalSquare

	main endp
	end main
```
![image](https://github.com/user-attachments/assets/5b2662bb-7ba8-4465-8245-8a1397afac6f)

## Question-4:
```.asm
include irvine32.inc

.data
	arr DWORD 4 dup (?)
	msg1 byte "Enter values: ", 0
	msg2 byte "Largest prime number is: ", 0
	msg3 byte "Not all numbers are prime..", 0
	check_var DWORD 1

.code
	CheckPrime proc
		ENTER 0, 0
		mov esi, [ebp+8]
		mov ecx, 4
		num_loop:
			mov eax, [esi]
			cmp eax, 2
			jl not_prime

			cmp eax, 2
			je go_to_num_loop
			
			mov ebx, 2
			check_loop:
				mov edx, 0
				mov eax, [esi]
				div ebx
				cmp edx, 0
				je not_prime
				inc ebx
				mov eax, [esi]
				cmp ebx, eax
			jl check_loop
		go_to_num_loop:
		add esi, 4
		loop num_loop
		jmp end_process

		not_prime:
				mov check_var, 0
		
		end_process:
			LEAVE
			ret 
	CheckPrime endp

	LargestPrime proc
		enter 0, 0
		mov esi, [ebp+8]
		mov eax, [esi]
		mov ecx, 3
		largest_loop:
			cmp eax, [esi+4]
			jge not_found
			mov eax, [esi+4]
		not_found:
			add esi, 4
			loop largest_loop

		leave
		ret
	LargestPrime endp

main proc
	mov edx, offset msg1
	call writestring
	call crlf
	mov ecx, lengthof arr
	mov esi, offset arr
	input_loop:
		call readint
		mov [esi], eax
		add esi, 4
	loop input_loop
	call crlf

	push offset arr
	call CheckPrime
	mov eax, check_var
	cmp eax, 1
	je largest_prime
	mov edx, offset msg3
	call writestring
	call crlf
	jmp end_main

	largest_prime:
		push offset arr
		call LargestPrime
		mov edx, offset msg2
		call writestring
		call writedec
		call crlf
		jmp end_main

end_main:
exit
main endp
end main
```
![image](https://github.com/user-attachments/assets/46d4d187-461f-46b8-b00d-f26d3845711f)
![image](https://github.com/user-attachments/assets/e3587074-fc74-4348-b3fe-82ffc6280da5)

## Question-5:

