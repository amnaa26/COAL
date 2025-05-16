## Task 01:
#### Code:
````.asm
include irvine32.inc
.data
  var1 sword ?
  var2 sbyte -11
.code
main proc
 ;nothing here
exit
main endp
end main
````

## Task 02:
#### Code:
`````.asm
include irvine32.inc
.data
  var sdword -2147483648
.code
main proc
  ;nothing
exit
main endp
end main
`````

## Task 03:
#### Code:
`````.asm
include irvine32.inc
.data
  var word 2, 4, 8
.code
main proc
exit
main endp
end main
`````

## Task 04:
#### Code:
`````.asm
include irvine32.inc
.data
  A word 12
  B word 2
  C word 13
  D word 8
  E word 14
  color byte "black", 0
`````

## Task 05:
#### Code:
`````.asm
include irvine32.inc
.data
  a dword 11h
  b dword 10h
  e dword 30h
  d dword 40h
.code
main proc
  ;ebx = { (a+b) – (a-b) + c } +d
  mov ebx, a
  add ebx, b
  mov eax, a
  sub eax, b
  sub ebx, eax
  add ebx, e
  add ebx, d
  mov eax, ebx
  call WriteHex
  call Crlf
exit
main endp
end main
`````
![image](https://github.com/user-attachments/assets/e6c6a729-88b2-42ae-a641-4a2581b46b1a)



## Task 06:
#### Code:
`````.asm
include irvine32.inc
.data
  a dword 00010001b
  b dword 00010000b
  e dword 00110000b
  d dword 01000000b
.code
main proc
  ;ebx = { (a+b) – (a-b) + c } +d
  mov ebx, a
  add ebx, b
  mov eax, a
  sub eax, b
  sub ebx, eax
  add ebx, e
  add ebx, d
  mov eax, ebx
  call WriteBin
  call crlf
  call WriteInt
  call Crlf
  call dumpregs
exit
main endp
end main
`````
![image](https://github.com/user-attachments/assets/f24bf6fd-d554-4d41-8a88-f5105c5d62b9)


## Task 07:
#### Code:
`````.asm
include irvine32.inc
.data
  wArray word 2, 4, 8
.code
main proc

exit
main endp
end main
`````

## Task 08:
#### Code:
`````.asm
include irvine32.inc
.data
string BYTE 50 DUP(?)
`````

## Task 09:
#### Code:
`````.asm
include irvine32.inc
.data
string BYTE 500 DUP(“TEST”)
`````

## Task 10:
#### Code:
`````.asm
include irvine32.inc
.data
string BYTE 20 DUP(0)
`````
