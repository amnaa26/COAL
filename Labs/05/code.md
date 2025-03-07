## Question-3:

if ```arrB``` were ```WORD``` or ```DWORD```, we would change registers from ```al``` to ```ax``` or ```eax``` respectively.

```.asm
include irvine32.inc

.data
	arrB BYTE 61, 43, 11, 52, 25
	newarrB BYTE 5 dup(?)

.code
main proc
	mov esi, offset newarrB
	mov al, arrB[2]
	mov [esi], al
	inc esi

	mov al, arrB[4]
	mov [esi], al
	inc esi

	mov al, arrB[1]
	mov [esi], al
	inc esi

	mov al, arrB[3]
	mov [esi], al
	inc esi

	mov al, arrB[0]
	mov [esi], al
	
	mov ecx, lengthof newarrB
	mov esi, offset newarrB
	l1:
		movzx eax, BYTE PTR [esi]
		call WriteInt
		call crlf
		inc esi
		loop l1
		

exit
main endp
end main
```
![image](https://github.com/user-attachments/assets/f941b783-7478-455e-ab69-2ced8826d24c)

## Question-4:
```.asm
include irvine32.inc

.data
	arrayB BYTE 10, 20, 30 
	arrayW WORD 150, 250, 350 
	arrayD DWORD 600, 1200, 1800
	SUM1 DWORD ?
	SUM2 DWORD ?
	SUM3 DWORD ?						


.code
main proc
	movzx eax, arrayB[0]
	movzx ebx, arrayW[0]
	add eax, ebx
	add eax, arrayD[0]
	mov SUM1, eax
	call WriteInt
	call crlf

	movzx eax, arrayB[1]
	movzx ebx, arrayW[2]
	add eax, ebx
	add eax, arrayD[4]
	mov SUM2, eax
	call WriteInt
	call crlf

	movzx eax, arrayB[2]
	movzx ebx, arrayW[4]
	add eax, ebx
	add eax, arrayD[8]
	mov SUM2, eax
	call WriteInt
	call crlf

exit
main endp
end main
```
![image](https://github.com/user-attachments/assets/bfa5eb6a-716f-4414-b72f-55a6f0e81f93)

## Question-5:
```.asm
include irvine32.inc

.data
	array1 BYTE 10, 20, 30, 40
	array2 BYTE 4 DUP (?)					


.code
main proc
	mov esi, offset array1+3
	mov edi, offset array2

	mov al, [esi]
	dec esi
	mov [edi], al
	inc edi
	
	mov al, [esi]
	dec esi
	mov [edi], al
	inc edi

	mov al, [esi]
	dec esi
	mov [edi], al
	inc edi

	mov al, [esi]
	mov [edi], al

	mov ecx, lengthof array2
	mov esi, offset array2
	l1:
		movzx eax, BYTE PTR [esi]
		call WriteInt
		call crlf
		inc esi
		loop l1
exit
main endp
end main
```
![image](https://github.com/user-attachments/assets/86f1c942-7d65-44fa-b60c-75f90addd72c)

## Question-6:
```.asm
include irvine32.inc

.data
	array1 DWORD 85, 23, 15, 10, 5

.code
main proc
	mov esi, offset array1
	mov eax, [esi] ;eax = 45
	add esi, TYPE array1
	sub eax, [esi] ; 45-79
	call WriteInt
	call crlf

	add esi, TYPE array1
	sub eax, [esi] ; 45-79
	call WriteInt
	call crlf

	add esi, TYPE array1
	sub eax, [esi] ; 45-79
	call WriteInt
	call crlf

	add esi, TYPE array1
	sub eax, [esi] ; 45-79
	

	call WriteInt
	call crlf
exit
main endp
end main
```
![image](https://github.com/user-attachments/assets/4672c495-8c20-4242-9bfa-ad39733c7a5e)

## Question-7:
```.asm
include irvine32.inc

.data
	arrayB BYTE 60, 70, 80
	arrayW WORD 150, 250, 350
	arrayD DWORD 600, 1200, 1800

.code
main proc
	mov esi, offset arrayB
	movzx eax, BYTE PTR [esi]
	add esi, (2 * TYPE arrayB)
	add al, [esi]
	call WriteInt
	call crlf

	mov esi, offset arrayW
	movzx ebx, WORD PTR [esi]
	add esi, (2 * TYPE arrayW)
	add bx, [esi]
	mov ax, bx
	call WriteInt
	call crlf

	mov esi, offset arrayD
	mov ecx, DWORD PTR [esi]
	add esi, (2 * TYPE arrayD)
	add ecx, [esi]
	mov eax, ecx
	call WriteInt
	call crlf
	
exit
main endp
end main
```
![image](https://github.com/user-attachments/assets/671279cf-75a8-401e-b8a9-d3d36771af75)
