## Question-1:
```.asm
include irvine32.inc

.code
main proc
	mov ecx, 10
	mov edx, 0
	mov ebx, 1

	fibonacci:
		mov eax, edx
		call writedec
		call crlf

		add edx, ebx
		mov ebx, eax

		loop fibonacci

		exit

main endp
end main
```
![image](https://github.com/user-attachments/assets/6dc796fb-3c89-46db-9619-802fd920f15f)

## Question-2:
```.asm
include irvine32.inc

.code
main proc
	mov ecx, 4
	mov ebx, 1
	outer:
		mov edx, ecx
		mov ecx, ebx
		inc ebx
		inner:
			mov eax, 1
			call writedec
		loop inner
		call crlf
		mov ecx, edx
	loop outer

	exit

main endp
end main
```
![image](https://github.com/user-attachments/assets/6f0881c0-f10e-4e20-9c98-acd562919cfc)


```.asm
include irvine32.inc

.code
main proc
	mov ecx, 4
	mov eax, 1
	mov ebx, 4
	outer:
		mov edx, ecx
		mov ecx, ebx
		dec ebx
		inner:
			call writedec
		loop inner
		call crlf
		mov ecx, edx
	loop outer
	exit

main endp
end main
```
![image](https://github.com/user-attachments/assets/d0272d39-d56f-4848-8e98-39af1a54dfd9)


```.asm
include irvine32.inc

.data
	array dword 4,3,2,1

.code
main proc
	mov ecx, 4
	mov ebx, 4
	outer:
		mov esi, offset array
		mov edx, ecx
		mov ecx, ebx
		dec ebx
		inner:
			mov eax, [esi]
			call writedec
			add esi, 4
		loop inner
		call crlf
		mov ecx, edx
	loop outer
	exit

main endp
end main
```
![image](https://github.com/user-attachments/assets/1e395c5d-13c0-4866-9201-a69630a37d03)



```.asm
include irvine32.inc

.data
	array dword 4,3,2,1

.code
main proc
	mov ecx, 4
	mov ebx, 4
	outer:
		;mov esi, offset array
		mov esi, sizeof array
		sub esi, 4
		mov edx, ecx
		mov ecx, ebx
		dec ebx
		inner:
			mov eax, array[esi]
			call writedec
			sub esi, 4
		loop inner
		call crlf
		mov ecx, edx
	loop outer
	exit

main endp
end main
```
![image](https://github.com/user-attachments/assets/c6708fa5-de4d-48f8-8013-d4d9026b4b5f)

#### We can also implement these four patterns in a single outer loop
```.asm
include irvine32.inc

.data
	i dword 1
	d dword 4
	space dword 1

.code
main proc
	mov ecx, 4
	outer:
		mov edx, ecx

		;first inner loop
		mov ecx, i
		inner_loop_ones:
			mov eax, 1
			call writedec
		loop inner_loop_ones
		inc i
		mov eax, 32
		call writechar

		;second inner loop
		mov ecx, d
		mov eax, 1
		inner_loop_ones_part_two:
			call writedec
		loop inner_loop_ones_part_two
		mov eax, 32
		call writechar

		;third inner loop
		mov ecx, d
		mov eax, 1
		inner_1234:
			call writedec
			inc eax
		loop inner_1234
		mov eax, 32
		call writechar


		;fourth inner loop
		mov ecx, d
		mov eax, 4
		inner_4321:
			call writedec
			dec eax
		loop inner_4321

		dec d
		mov ecx, edx
		call crlf

	loop outer

	exit

main endp
end main
```
![image](https://github.com/user-attachments/assets/6439582f-fd73-479f-9f5c-aee43eac9268)

## Question-3:



