![image](https://github.com/user-attachments/assets/f37bc881-2ac0-40af-a7d5-813b43778e19)

```.asm
include irvine32.inc

.data
	bintodec BYTE 0,0,1,0,1,0,0,0
	val BYTE 128, 64, 32, 16, 8, 4, 2, 1
	ans dword 0

.code

convertBINtoDEC proc
	mov esi, offset bintodec
	mov edi, offset val
	mov ecx, lengthof bintodec
	
	loop_1:
		movzx eax, byte ptr [esi]
		movzx ebx, byte ptr [edi]
		mul ebx
		add ans, eax
		mov eax, ans
		inc esi
		inc edi
	loop loop_1

	mov eax, ans
	ret
convertBINtoDEC endp

main proc
	call convertBINtoDEC
	call writedec

	exit
main endp
end main
```

![image](https://github.com/user-attachments/assets/bd77555a-3111-4462-90e2-32a4da69f0b5)
