## Question-1:
Count number of alphabets present in your roll number.
```.asm
include irvine32.inc

.data
	rollno BYTE "23k-0066check", 0

.code
main proc
	mov ecx, lengthof rollno - 1
	mov esi, offset rollno
	mov eax, 0
	count:
		mov bl, [esi]
		inc esi

		cmp bl, 'A'
		jl not_alpha
		cmp bl, 'Z'
		jle is_alpha

		cmp bl, 'a'
		jl not_alpha
		cmp bl, 'z'
		jle is_alpha

		is_alpha:
			inc eax

		not_alpha:
			loop count

	call writeint
	call crlf
	exit

main endp
end main
```
![image](https://github.com/user-attachments/assets/c8d9eb04-9484-42d4-a86f-725f66d69f04)


