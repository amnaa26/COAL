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

