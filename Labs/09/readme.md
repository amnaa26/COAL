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

