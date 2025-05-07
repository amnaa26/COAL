## Question-1:
```.asm
include irvine32.inc

.data
	string1 BYTE '127&j~3#^&*#*#45^',0
	msg1 byte "index: ", 0

.code
	Scan_String proc
		mov edi, offset string1
		mov ecx, lengthof string1
		mov eax, '#'
		repne scasb
		sub edi, offset string1 + 1
		ret
	Scan_String endp


main proc
	call Scan_String
	mov edx, offset msg1
	call writestring
	mov eax, edi
	call writedec
	call crlf

end_main:
exit
main endp
end main
```
![image](https://github.com/user-attachments/assets/14414e79-01dc-40cb-8293-07e55ba3e884)

## Question-2:
```.asm
include irvine32.inc

.data
	string1 BYTE '127&j~3#^&*#*#45^',0
	msg1 byte "index: ", 0

.code
	Scan_String proc
		enter 0, 0
		mov edi, [ebp+8]
		mov ecx, [ebp+12]
		mov eax, [ebp+16]
		repne scasb
		sub edi, [ebp+8]
		dec edi
		leave
		ret
	Scan_String endp


main proc
	push '4'			;we are searching the index where character '4' lies
	push lengthof string1
	push offset string1
	call Scan_String
	mov eax, edi
	mov edx, offset msg1
	call writestring
	call writedec
	call crlf

end_main:
exit
main endp
end main
```
![image](https://github.com/user-attachments/assets/2fa2fb03-d923-4d82-bfff-47a72d71413c)

## Question-3:
```.asm
include irvine32.inc

.data
	msg1 BYTE "Hello World",0
	msg2 BYTE "Hello Humans", 0
	msg3 BYTE "source < destination", 0
	msg4 BYTE "source > destination", 0
	msg5 BYTE "source == destination", 0
	

.code
	IsCompare proc
		mov esi, offset msg1
		mov edi, offset msg2
		mov ecx, lengthof msg1
		repe cmpsb
		ret
	IsCompare endp


main proc
	call IsCompare
	je equal_
	jl less_
	jg greater_

	equal_:
		mov edx, offset msg5
		call writestring
		call crlf
		jmp end_main
	less_:
		mov edx, offset msg3
		call writestring
		call crlf
		jmp end_main
	greater_:
		mov edx, offset msg4
		call writestring
		call crlf

end_main:
exit
main endp
end main
```
![image](https://github.com/user-attachments/assets/63a5a06b-c961-4c51-8c86-638aaff9d902)

## Question-4:
```.asm
include irvine32.inc

.data
	msg1 BYTE "Hello World",0
	
.code
	reverse_str proc
		mov esi, offset msg1
		mov ecx, lengthof msg1
		dec ecx					;ignore null terminator
		mov edi, esi
		add edi, ecx
		dec edi

		mov edx, 0
		mov eax, lengthof msg1
		mov ebx, 2
		div ebx
		mov ecx, eax
		reverse_loop:
			mov al, [esi]
			mov bl, [edi]
			mov [esi], bl
			mov [edi], al

			inc esi
			dec edi
		loop reverse_loop
		
		ret
	reverse_str endp


main proc
	mov edx, offset msg1
	call writestring
	call crlf
	call reverse_str
	mov edx, offset msg1
	call writestring
	call crlf

end_main:
exit
main endp
end main
```
![image](https://github.com/user-attachments/assets/eec026b5-d2cf-4bcc-8e29-6ca7d924485d)

## Question-5:
```.asm
include irvine32.inc

.data
	arr DWORD 1, 2, 3, 4
	
.code
	load proc
		mov esi, offset arr
		mov edi, esi
		mov ecx, lengthof arr
		mov ebx, 2

		cld
		mul_loop:
			lodsd
			mul ebx
			stosd
		loop mul_loop
		
		ret
	load endp


main proc
	mov ecx, lengthof arr
	mov esi, offset arr
	print1_loop:
		mov eax, [esi]
		call writedec
		add esi, type arr
		mov eax, 32
		call writechar
	loop print1_loop
	call crlf
	
	call load
	mov ecx, lengthof arr
	mov esi, offset arr
	print2_loop:
		mov eax, [esi]
		call writedec
		add esi, type arr
		mov eax, 32
		call writechar
	loop print2_loop

end_main:
exit
main endp
end main
```
![image](https://github.com/user-attachments/assets/e54bcc99-688f-47c9-872c-8628e736b964)
