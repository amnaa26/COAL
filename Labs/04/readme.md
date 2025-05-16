## Question-1
```.asm
MOV AX 3d      ; no comma between destination and source operand 
MOV 23, AX     ; destination cannot be an imediate value
MOV CX, CH     ; source and destination should be of the same size
MOVE AX, 1h    ; MOVE is an incorrect instruction. It should be mov or MOV
ADD 2, CX      ; destination caanot be an imediate value
ADD 3, 6       ; source and destination are immediate values
INC AX, 2      ; inc only takes a single operand
```
***

## Question-2
```.asm
include irvine32.inc

.code
main proc
  mov eax, 97    ; a = 97
  mov ebx, 109   ; m = 109
  mov ecx, 110   ; n = 110
  call dumpregs
exit
main endp
end main
```
![image](https://github.com/user-attachments/assets/22681c11-a198-4171-81ea-ee9e5b89db84)


***
## Question-3
```.asm
include irvine32.inc

.data
  varB BYTE +10
  varW WORD -150
  varD DWORD 600

.code
main proc
  movzs eax, varB
  movzs ebx, varW
  mov ecx, varD
  call dumpregs
exit
main endp
end main
```
![image](https://github.com/user-attachments/assets/469f2dd6-7f1e-4662-b4c8-028124ddf6c1)


***

## Question-4
```.asm
include irvine32.inc

.data
  Val1 DWORD 25h
  Val2 BYTE 36o
  Val3 WORD 20d

.code
main proc
  ;EAX = 89 + 75Fh - 46o - 28 +1101b
  mov eax, 89
  add eax, 75Fh
  sub eax, 46o
  sub eax, 28
  add eax, 1101b
  call writeint
  call crlf

  ;EAX = Val1 + Val2 - 654h + Val3
  mov eax, Val1
  add al, Val2
  sub eax, 654h
  add ax, Val3
  call writeint
  call crlf

exit
main endp
end main
```
![image](https://github.com/user-attachments/assets/71a10eaa-2945-4e35-90bd-f4661bd8ce69)


***

## Question-6:
```.asm
include irvine32.inc

.data
	SecondsInDay = 24 * 60 * 60
.code
main proc
	mov eax, SecondsInDay
	call writedec
exit
main endp
end main
```
![image](https://github.com/user-attachments/assets/7cab9828-b2f3-4fdb-9c15-eb79645b6783)


***

## Question-7:
```.asm
include irvine32.inc

.data
	A word 0FF10h
	B word 0E10Bh
.code
main proc
	; swap
	movzx eax, A
	xchg ax, B
	mov A, ax

	; print
	movzx eax, A
	call writehex
	call crlf
	movzx eax, B
	call writehex
exit
main endp
end main
```
![image](https://github.com/user-attachments/assets/5a1550d3-6ccc-41a2-903c-1eb450721858)


***

## Question-8:
```.asm
include irvine32.inc

.data
	val1 byte 10h
	val2 word 8000h
	val3 dword 0ffffh
	val4 word 7fffh
.code
main proc
	; part i
	inc val2
	movzx eax, val2
	call writedec

	call crlf

	; part ii
	mov eax, 67279h
	sub eax, val3
	call writeint

	call crlf

	; part iii
	movzx eax, val2
	sub ax, val4
	mov val4, ax
	call writeint

exit
main endp
end main
```
![image](https://github.com/user-attachments/assets/c499ec63-f915-4258-aed3-fa48bf9b0fde)
