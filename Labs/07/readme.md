## Question-1:
```.asm
include irvine32.inc

.data
	arr1 DWORD 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
	arr2 DWORD 10 DUP(?)
.code

print proc uses eax
	
	print_l:
		mov eax, [edx]
		add edx, ebx
		call WriteDec
		mov eax, 32
		call WriteChar
		loop print_l

	ret
print endp

main proc
	mov esi, OFFSET arr1
	mov edi, OFFSET arr2
	mov ecx, LENGTHOF arr1
	l1:
		push [esi]
		pop [edi]
		add esi, TYPE arr1
		add edi, TYPE arr2
		loop l1

	mov edx, OFFSET arr2
	mov ecx, LENGTHOF arr2
	mov ebx, TYPE arr2
	call print
	exit
main endp
end main

```
![image](https://github.com/user-attachments/assets/7c22cdf1-6a4b-405b-b55c-623973efdc97)

## Question-2:
```.asm
INCLUDE Irvine32.inc

.data

.code
main proc
	mov eax, 4 ; initial value
	mov ecx, 2 

	L1:
		push eax
		add eax, 4
		loop L1

	mov ecx, 2
	L2:
		pop ebx
		add eax, ebx
		loop L2

	call WriteDec ; expected result = 4 + 8 + 12 = 

	exit
main endp
end main
```
![image](https://github.com/user-attachments/assets/3d855794-627c-4acf-bb25-c831b5f3c121)

## Question-3:
```.asm
include irvine32.inc

.data
	arr1 DWORD 1, 2, 3, 4, 5
	arr2 DWORD 6, 7, 8, 9, 10
.code

arr1_add proc
	push ecx
	push esi
	mov ecx, LENGTHOF arr1
	mov esi, OFFSET arr1
	mov eax, 0
	l1:
		add eax, [esi]
		add esi, TYPE arr1
		loop l1

	pop esi
	pop ecx
	ret
arr1_add endp

arr2_add proc
	push ecx
	push esi
	mov esi, OFFSET arr2
	mov ecx, LENGTHOF arr2
	mov ebx, 0
	l2:
		add ebx, [esi]
		add esi, TYPE arr2
		loop l2
	pop esi
	pop ecx
	ret
arr2_add endp

sum_2_arrays proc
	add eax, ebx
	ret
sum_2_arrays endp

main proc
	call arr1_add
	call arr2_add
	call sum_2_arrays

	call WriteDec
	
	exit
main endp
end main
```
![image](https://github.com/user-attachments/assets/58635a10-4b24-43d6-8208-9e95310783b1)


## Question-4:
```.asm
include irvine32.inc

.data 
	var dword 5

.code

print_asterik proc
	mov ecx, var
	mov ebx, 5
	mov edx, 1
	outer:
		push ecx
		mov ecx, ebx
		space:
			mov eax, 32
			call writechar
		loop space
		mov ecx, edx
		inner:
			mov eax, 42
			call writechar
		loop inner
		call crlf
		pop ecx
		dec ebx
		inc edx
	loop outer

	ret
print_asterik endp

main proc
	call print_asterik
	exit

main endp
end main

```
![image](https://github.com/user-attachments/assets/2cb626b9-7897-41a3-ab67-7b5bccbbb12f)

## Question-5:
```.asm
include irvine32.inc

.data 
	var dword ?
	input byte "Enter a number: ", 0
	output byte "Sum is: ", 0

.code

sum proc
	mov edx, offset input
	call writestring
	call readint
	mov var, eax

	mov ecx, var
	mov eax, 0
	outer:
		add eax, ecx
	loop outer

	mov edx, offset output
	call writestring
	call writedec

	ret
sum endp

main proc
	call sum
	call crlf
	exit

main endp
end main
```

![image](https://github.com/user-attachments/assets/36222327-3578-403f-a451-e7a487750d07)

