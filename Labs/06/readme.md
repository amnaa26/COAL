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
```.asm
include irvine32.inc

.data
	buffer_size=20
	employee_count=5

	employee_id DWORD employee_count DUP (?)
	employee_names BYTE employee_count * buffer_size DUP(0)
	birth_year DWORD employee_count DUP(?)
	salary DWORD employee_count DUP(?)

	id_input BYTE "Enter employee ids:", 0
	names_input BYTE "Enter employee name:", 0
	year_input BYTE "Enter employee year of birth:", 0
	salary_input BYTE "Enter employee salary:", 0
	total_salary BYTE "Sum of all salaries: ", 0
	print_output BYTE "ID  NAME  YEAR  SALARY",0

.code

read_name proc uses edx ecx edi
	push edx
	push ecx
	push edi

	mov edx, offset employee_names
	mov edi, esi
	imul edi, buffer_size
	add edx, edi
	mov ecx, buffer_size
	call readstring

	pop edi
	pop ecx
	pop edx
	ret
read_name endp


main proc
	;reading id
	mov edx, offset id_input
	call writestring
	call crlf
	mov ecx, employee_count
	mov esi, 0
	id_loop:
		call readint
		mov employee_id[esi * type employee_id], eax
		inc esi
	loop id_loop

	call crlf
	;reading employees names
	mov edx, offset names_input
	call writestring
	call crlf
	mov ecx, employee_count
	mov esi, 0
	name_loop:
		call read_name
		inc esi
	loop name_loop

	call crlf
	;reading birth year
	mov edx, offset year_input
	call writestring
	call crlf
	mov ecx, employee_count
	mov esi, 0
	year_loop:
		call readint
		mov birth_year[esi * type birth_year], eax
		inc esi
	loop year_loop

	call crlf
	;reading salary
	mov edx, offset salary_input
	call writestring
	call crlf
	mov ecx, employee_count
	mov esi, 0
	salary_loop:
		call readint
		mov salary[esi * type salary], eax
		inc esi
	loop salary_loop

	call crlf
	;adding salaries
	mov esi, 0
	mov ecx, employee_count
	mov eax, 0
	sum_loop:
		add eax, salary[esi * type salary]
		inc esi
	loop sum_loop

	;writing total salary
	mov edx, offset total_salary
	call writestring
	call writedec
	call crlf
	call crlf


	mov edx, offset print_output
	call writestring
	call crlf
	mov ecx, employee_count
	mov esi, 0
	output:
		;writing ids
		mov eax, employee_id[esi * type employee_id]
		call writedec
		mov eax, 32
		call writechar
		call writechar
		
		;writing names
		mov edx, offset employee_names
		mov edi, esi
		imul edi, buffer_size
		add edx, edi
		call writestring
		call writechar
		call writechar

		;writing birth year
		mov eax, birth_year[esi * type birth_year]
		call writedec
		mov eax, 32
		call writechar
		call writechar

		;writing salary
		mov eax, salary[esi * type salary]
		call writedec
	
		call crlf
		inc esi
	loop output
	

	exit

main endp
end main
```
![image](https://github.com/user-attachments/assets/003d74c2-8931-49d9-8de1-5fba499e226d)

## Question-4:
```.asm
include irvine32.inc

.data
	source BYTE "string to be copied", 0
	target BYTE lengthof source - 1 DUP(?), 0

.code
main proc
	mov esi, 0
	mov ecx, lengthof source
	copy_loop:
		mov al, source[esi]
		mov target[esi], al
		inc esi
	loop copy_loop

	mov edx, offset target
	call writestring
	call crlf

	exit

main endp
end main
```
![image](https://github.com/user-attachments/assets/b2df1044-0643-4128-a1d4-8b96bf9e0300)


## Question-5:
```.asm
include irvine32.inc

.data
	source DWORD 12, 13, 14, 15, 16, 17

.code
main proc
	mov esi, 0
	mov ecx, lengthof source / 2
	mov edi, lengthof source - 1
	reverse:
		mov eax, source[esi * type source]
		xchg eax, source[edi * type source]
		mov source[esi * type source], eax

		inc esi
		dec edi
	loop reverse

	mov esi, 0
	mov ecx, lengthof source
	print:
		mov eax, source[esi * type source]
		call writedec
		mov eax, 32
		call writechar
		inc esi
	loop print

	exit
```
![image](https://github.com/user-attachments/assets/e35450ce-7e28-493a-ab9e-af2ebcf3d286)


## Question-6:
```.asm
include irvine32.inc

.data
	source DWORD 8, 5, 1, 2, 6

.code
main proc
	mov ecx, lengthof source
	outer_loop:
		mov esi, 0
		mov edi, 1
		mov edx, ecx
		mov ecx, lengthof source - 1
		inner_loop:
			mov eax, source[esi * type source]
			cmp eax, source[edi * type source]
			jl no_swap

			xchg eax, source[edi * type source]
			mov source[esi * type source], eax

			no_swap:
				inc esi
				inc edi
				loop inner_loop
		mov ecx, edx
		loop outer_loop

		mov esi, 0
		mov ecx, lengthof source
		print:
			mov eax, source[esi * type source]
			call writedec
			mov eax, 32
			call writechar
			inc esi
		loop print

	exit

main endp
end main
```
![image](https://github.com/user-attachments/assets/4016eba3-6ed5-4f78-893d-6cbdc1e7ef8a)


