## Question-1:
```.asm
include irvine32.inc

.data

.code

main proc
    ; 21 = 2^4 + 2^2 + 2^1

    call readint
    mov ebx, eax        ; Copy EAX to EBX
    shl eax, 4          ; EAX = EAX * 16
    mov ecx, ebx
    shl ecx, 2          ; ECX = EAX * 4
    add eax, ecx        ; EAX = EAX * 16 + EAX * 4
    add eax, ebx        ; EAX = EAX + previous = EAX * 21

    call writedec
    exit

main endp
end main
```
![image](https://github.com/user-attachments/assets/5491b59b-c399-47c9-a45b-fbb0ffce3ae0)

## Question-2:
```.asm
include irvine32.inc

.data
.code
main proc
    mov ax, -128
    movsx eax, ax
    shl eax, 16
    sar eax, 16
    call WriteInt
    exit
main ENDP
END main
```
![image](https://github.com/user-attachments/assets/fd013a6d-5645-4e0d-aeb8-1634df0e12e2)


## Question-3:
```.asm
include irvine32.inc

.data
.code
main proc
    mov ax, 728h
    mov cx, ax
    and cx, 1           ; Isolate LSB of AX
    shl cx, 15          ; Move to MSB position
    and bx, 7FFFh       ; Clear MSB of BX
    or bx, cx           ; Set new MSB based on AX's LSB
    movzx eax, bx
    call WriteHex ; without shrd
    call crlf

    ; Move lowest bit of AX into highest of BX using SHRD
    mov ax, 728h
    mov dx, ax
    shrd bx, dx, 1      ; Shift BX right 1 bit, filling MSB from LSB of DX
    shl bx, 1           ; Restore position (if needed)
    movzx eax, bx
    call WriteHex ; with shrd
    exit

main ENDP
END main
```
![image](https://github.com/user-attachments/assets/29941fe0-65eb-4b01-ae29-7c14d20966bb)

## Question-4:
```.asm
include irvine32.inc

.data
    val1 DWORD 12
    val2 DWORD 4
    val3 DWORD 2
.code
main proc
    mov eax, val2       ; EAX = val2
    cdq                 ; Sign extend to EDX:EAX
    idiv val3           ; EAX = val2 / val3
    mov esi, eax        ; Save result in ESI

    mov eax, val1       ; EAX = val1
    cdq
    idiv val2           ; EAX = val1 / val2
    imul eax, esi       ; EAX = (val2 / val3) * (val1 / val2)

    call writedec
    exit

main ENDP
END main
```
![image](https://github.com/user-attachments/assets/2252f0aa-46ea-4450-9fe9-81f481a4ea68)

## Question-5:
```.asm
INCLUDE Irvine32.inc

.code

Add64 PROC
    enter 0, 0
    mov eax, [ebp + 8]      ; a_low
    add eax, [ebp + 16]     ; + b_low
    mov edx, [ebp + 12]     ; a_high
    adc edx, [ebp + 20]     ; + b_high + carry

    leave
    ret 16
Add64 ENDP

main PROC
    mov eax, 00000005h      ; a_high
    call WriteHex
    mov eax, 12345678h      ; a_low
    call WriteHex
    call Crlf

    mov eax, 00000003h      ; b_high
    call WriteHex
    mov eax, 87654321h      ; b_low
    call WriteHex
    call Crlf

    push 00000005h
    push 12345678h
    push 00000003h
    push 87654321h

    call Add64

    ; Print result EDX:EAX
    push eax
    mov eax, edx
    call WriteHex
    pop eax
    call WriteHex
    call Crlf

    exit
main ENDP

END main

```
![image](https://github.com/user-attachments/assets/79dbaeb3-78a5-47d4-a276-18d5854fe113)

