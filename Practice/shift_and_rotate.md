![image](https://github.com/user-attachments/assets/9aa6bec0-e970-400a-b2d5-89cd6eaf0b54)


```.asm
include irvine32.inc

.data

.code
main proc
	mov eax, 12438765h
	mov dx, 0000h
	rol eax, 16		;eax = 87651243
	rol ax, 8		;eax = 87654312
	shl al, 1		;eax = 87654324
	mov bl, al		;bl = 24
	and bl, 04h		;bl = 04
	mov ecx, 2
	loop_:
		shr bl, 1
	loop loop_

	;bl = 01

	and al, 20h		;al = 20
	or al, bl		;al = 21

	call writehex	;eax = 87654321

	exit
main endp
end main
```

![image](https://github.com/user-attachments/assets/552e271f-eefc-4922-8449-781c972fd92b)
