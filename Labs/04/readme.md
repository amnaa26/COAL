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

***


  
