# riscv-32-cpu
riscv-32-cpu implemented in Digital software 

![img](https://github.com/NikosMouzakitis/riscv-32-cpu/blob/main/rv_status.png)
```
Status of what is implemented so far.
#	Instruction	Type	Functionality	Explanation
1	lb	Load	Load Byte		Load 8-bit byte from memory into register (sign-extended).
2	lh	Load	Load Halfword		Load 16-bit halfword from memory (sign-extended).
✅	lw	Load	Load Word		Load 32-bit word from memory.
4	lbu	Load	Load Byte Unsigned	Load 8-bit byte, zero-extended.
5	lhu	Load	Load Halfword Unsigned	Load 16-bit halfword, zero-extended.
6	sb	Store	Store Byte		Store 8-bit value from register into memory.
7	sh	Store	Store Halfword		Store 16-bit value into memory.
✅	sw	Store	Store Word		Store 32-bit value into memory.
✅	add	ALU	Add	rd = rs1 + rs2 (Signed integer addition).
✅	sub	ALU	Subtract	rd = rs1 - rs2 (Signed integer subtraction).
✅	sll	ALU	Shift Left Logical	rd = rs1 << rs2 (Shift bits left, zero-fill).
✅	slt	ALU	Set Less Than	rd = (rs1 < rs2) ? 1 : 0 (Signed).
✅	sltu	ALU	Set Less Than Unsigned	rd = (rs1 < rs2) ? 1 : 0 (Unsigned).
✅	xor	ALU	XOR	rd = rs1 ^ rs2 (Bitwise XOR).
✅	srl	ALU	Shift Right Logical	rd = rs1 >> rs2 (Logical shift right, zero-fill).
✅	sra	ALU	Shift Right Arithmetic	rd = rs1 >> rs2 (Signed shift right, sign-extend).
✅	or	ALU	OR	`rd = rs1
✅	and	ALU	AND	rd = rs1 & rs2 (Bitwise AND).
✅	addi	ALU	Add Immediate	rd = rs1 + imm (Add constant to register).
20	slli	ALU	Shift Left Logical Immediate	rd = rs1 << imm (Shift left by imm bits).
21	slti	ALU	Set Less Than Immediate	rd = (rs1 < imm) ? 1 : 0 (Signed).
22	sltiu	ALU	Set Less Than Immediate Unsigned	rd = (rs1 < imm) ? 1 : 0 (Unsigned).
23	xori	ALU	XOR Immediate	rd = rs1 ^ imm (Bitwise XOR with constant).
24	srli	ALU	Shift Right Logical Immediate	rd = rs1 >> imm (Logical shift right by imm bits).
25	srai	ALU	Shift Right Arithmetic Immediate	rd = rs1 >> imm (Arithmetic shift right, sign-extended).
26	ori	ALU	OR Immediate	`rd = rs1
27	andi	ALU	AND Immediate	rd = rs1 & imm (Bitwise AND with constant).
28	beq	Branch	Branch if Equal	If rs1 == rs2, jump to target address.
29	bne	Branch	Branch if Not Equal	If rs1 != rs2, jump to target.
30	blt	Branch	Branch if Less Than	If rs1 < rs2, jump (Signed).
31	bge	Branch	Branch if Greater or Equal	If rs1 >= rs2, jump (Signed).
32	bltu	Branch	Branch if Less Than Unsigned	If rs1 < rs2, jump (Unsigned).
33	bgeu	Branch	Branch if Greater or Equal Unsigned	If rs1 >= rs2, jump (Unsigned).
34	jal	Jump	Jump and Link	Jump to target and save return address.
35	jalr	Jump	Jump and Link Register	Jump to rs1 + offset and save return address.
36	lui	Upper Imm	Load Upper Immediate	Load 20-bit immediate into upper 20 bits of rd.
37	auipc	Upper Imm	Add Upper Immediate to PC	rd = PC + (imm << 12), useful for position-independent code.
38	ecall	System	Environment Call	Call OS services (syscall).
39	ebreak	System	Breakpoint	Debugging breakpoint.
40	fence	Memory	Fence	Ensure memory operations complete in order.
41	csrrw	CSR	CSR Read and Write	Swap CSR register with rs1.
42	csrrs	CSR	CSR Read and Set	Read CSR and set bits defined by rs1.
43	csrrc	CSR	CSR Read and Clear	Read CSR and clear bits defined by rs1.
44	csrrwi	CSR	CSR Read and Write Immediate	Swap CSR register with immediate value.
45	csrrsi	CSR	CSR Read and Set Immediate	Read CSR and set bits defined by immediate.
46	csrrci	CSR	CSR Read and Clear Immediate	Read CSR and clear bits defined by immediate.
47	wfi	System	Wait for Interrupt	Low-power wait for an interrupt.
	
	
	
	
	
1. Basic Arithmetic & Logical Operations (R-Type)
✅	add rd, rs1, rs2 (Already implemented)
✅	sub rd, rs1, rs2 (Already implemented)
✅	sll rd, rs1, rs2 (Shift Left Logical)
✅	srl rd, rs1, rs2 (Shift Right Logical)
✅	sra rd, rs1, rs2 (Shift Right Arithmetic)
✅	xor rd, rs1, rs2 (Bitwise XOR)
✅	or rd, rs1, rs2 (Bitwise OR)
✅	and rd, rs1, rs2 (Bitwise AND)
✅	slt rd, rs1, rs2 (Set Less Than - Signed)
✅	sltu rd, rs1, rs2 (Set Less Than - Unsigned)

2. Immediate Operations (I-Type)
These perform operations with an immediate value instead of a second register.
✅      addi rd, rs1, imm (Add Immediate)
➡️ slti rd, rs1, imm (Set Less Than Immediate - Signed)
➡️ sltiu rd, rs1, imm (Set Less Than Immediate - Unsigned)
➡️ xori rd, rs1, imm (Bitwise XOR with Immediate)
➡️ ori rd, rs1, imm (Bitwise OR with Immediate)
➡️ andi rd, rs1, imm (Bitwise AND with Immediate)
➡️ slli rd, rs1, shamt (Shift Left Logical Immediate)
➡️ srli rd, rs1, shamt (Shift Right Logical Immediate)
➡️ srai rd, rs1, shamt (Shift Right Arithmetic Immediate)

3. Load and Store Operations (I-Type & S-Type)
✅	lw rd, imm(rs1) (Load Word)
✅	sw rs2, imm(rs1) (Store Word)
➡️ lb rd, imm(rs1) (Load Byte - Sign-Extended)
➡️ lbu rd, imm(rs1) (Load Byte - Zero-Extended)
➡️ lh rd, imm(rs1) (Load Halfword - Sign-Extended)
➡️ lhu rd, imm(rs1) (Load Halfword - Zero-Extended)
➡️ sb rs2, imm(rs1) (Store Byte)
➡️ sh rs2, imm(rs1) (Store Halfword)

4. Control Flow (Branch & Jump)
➡️ beq rs1, rs2, offset (Branch if Equal)
➡️ bne rs1, rs2, offset (Branch if Not Equal)
➡️ blt rs1, rs2, offset (Branch if Less Than - Signed)
➡️ bge rs1, rs2, offset (Branch if Greater or Equal - Signed)
➡️ bltu rs1, rs2, offset (Branch if Less Than - Unsigned)
➡️ bgeu rs1, rs2, offset (Branch if Greater or Equal - Unsigned)
➡️ jal rd, offset (Jump and Link)
➡️ jalr rd, rs1, offset (Jump and Link Register)

5. Multiplication and Division (M Extension - Optional)
✅ mul rd, rs1, rs2 (Multiply)
➡️ mulh rd, rs1, rs2 (Multiply High - Signed)
➡️ mulhu rd, rs1, rs2 (Multiply High - Unsigned)
➡️ div rd, rs1, rs2 (Divide - Signed)
➡️ divu rd, rs1, rs2 (Divide - Unsigned)
➡️ rem rd, rs1, rs2 (Remainder - Signed)
➡️ remu rd, rs1, rs2 (Remainder - Unsigned)
```
