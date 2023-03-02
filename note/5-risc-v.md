# RISC-V

## 1. Instruction
### 1.1 Instruction Type
| Type   | Usage                            |
| ------ | -------------------------------- |
| R-type | for register-register operations |
| I-type | for short immediates and loads   |
| S-type | for stores                       |
| B-type | for conditional branches         |
| U-type | for long immediates              |
| J-type | for unconditional jumps          |

### 1.2 Instruction Formats
```
 V U T S R Q P O N M L K Z I H G F E D C B A 9 8 7 6 5 4 3 2 1 0
+-----------------------+---------+-----+---------+-------------+
|    func7    |   rs2   |   rs1   |func3|   rd    |    opcode   | R-type
+-----------------------+---------+-----+---------+-------------+
+-----------------------+---------+-----+---------+-------------+
|       imm[11:0]       |   rs1   |func3|   rd    |    opcode   | I-type
+-----------------------+---------+-----+---------+-------------+
+-------------+---------+---------+-----+---------+-------------+
|  imm[11:5]  |   rs2   |   rs1   |func3|imm[4:0] |    opcode   | S-type
+-------------+---------+---------+-----+---------+-------------+
+-------------+---------+---------+-----+---------+-------------+
|i| imm[10:5] |   rs2   |   rs1   |func3|  imm  |i|    opcode   | B-type
+-------------+---------+---------+-----+---------+-------------+
+---------------------------------------+---------+-------------+
|            imm[31:12]                 |   rd    |    opcode   | U-type
+---------------------------------------+---------+-------------+
+---------------------------------------+---------+-------------+
|i|     imm[10:1]     |i|  imm[19:12]   |   rd    |    opcode   | J-type
+---------------------------------------+---------+-------------+
```
### 1.3 Instruction Domain
| Domain | Usage                                |
| ------ | ------------------------------------ |
| opcode | instruction type                     |
| rs     | source register                      |
| rd     | destination register                 |
| imm    | immediate number                     |
| funct  | support **opcode** for instruction type  |      

### 1.4 Instruction Layout
```
 V U T S R Q P O N M L K Z I H G F E D C B A 9 8 7 6 5 4 3 2 1 0
+-----------------------+---------+-----+---------+-------------+
|0 0 0 0 0 0 0|   rs2   |   rs1   |0 0 0|   rd    |0 1 1 0 0 1 1| R-add
+-----------------------+---------+-----+---------+-------------+
|0 1 0 0 0 0 0|   rs2   |   rs1   |0 0 0|   rd    |0 1 1 0 0 1 1| R-sub
+-----------------------+---------+-----+---------+-------------+
|0 0 0 0 0 0 0|   rs2   |   rs1   |0 0 1|   rd    |0 1 1 0 0 1 1| R-sll
+-----------------------+---------+-----+---------+-------------+
|0 0 0 0 0 0 0|   rs2   |   rs1   |0 1 0|   rd    |0 1 1 0 0 1 1| R-slt
+-----------------------+---------+-----+---------+-------------+
|0 0 0 0 0 0 0|   rs2   |   rs1   |0 1 1|   rd    |0 1 1 0 0 1 1| R-sltu
+-----------------------+---------+-----+---------+-------------+
|0 0 0 0 0 0 0|   rs2   |   rs1   |1 0 0|   rd    |0 1 1 0 0 1 1| R-xor
+-----------------------+---------+-----+---------+-------------+
|0 0 0 0 0 0 0|   rs2   |   rs1   |1 0 1|   rd    |0 1 1 0 0 1 1| R-srl
+-----------------------+---------+-----+---------+-------------+
|0 1 0 0 0 0 0|   rs2   |   rs1   |1 0 1|   rd    |0 1 1 0 0 1 1| R-sra
+-----------------------+---------+-----+---------+-------------+
|0 0 0 0 0 0 0|   rs2   |   rs1   |1 1 0|   rd    |0 1 1 0 0 1 1| R-or
+-----------------------+---------+-----+---------+-------------+
|0 0 0 0 0 0 0|   rs2   |   rs1   |1 1 1|   rd    |0 1 1 0 0 1 1| R-and
+-----------------------+---------+-----+---------+-------------+
+-----------------------+---------+-----+---------+-------------+
|       imm[11:0]       |   rs1   |0 0 0|   rd    |1 1 0 0 1 1 1| I-jalr
+-----------------------+---------+-----+---------+-------------+
|       imm[11:0]       |   rs1   |0 0 0|   rd    |0 0 0 0 0 1 1| I-lb
+-----------------------+---------+-----+---------+-------------+
|       imm[11:0]       |   rs1   |0 0 1|   rd    |0 0 0 0 0 1 1| I-lh
+-----------------------+---------+-----+---------+-------------+
|       imm[11:0]       |   rs1   |0 1 0|   rd    |0 0 0 0 0 1 1| I-lw
+-----------------------+---------+-----+---------+-------------+
|       imm[11:0]       |   rs1   |1 0 0|   rd    |0 0 0 0 0 1 1| I-lbu
+-----------------------+---------+-----+---------+-------------+
|       imm[11:0]       |   rs1   |1 0 1|   rd    |0 0 0 0 0 1 1| I-lhu
+-----------------------+---------+-----+---------+-------------+
|       imm[11:0]       |   rs1   |0 0 0|   rd    |0 0 1 0 0 1 1| I-addi
+-----------------------+---------+-----+---------+-------------+
|       imm[11:0]       |   rs1   |0 1 0|   rd    |0 0 1 0 0 1 1| I-slti
+-----------------------+---------+-----+---------+-------------+
|       imm[11:0]       |   rs1   |0 1 1|   rd    |0 0 1 0 0 1 1| I-sltiu
+-----------------------+---------+-----+---------+-------------+
|       imm[11:0]       |   rs1   |1 0 0|   rd    |0 0 1 0 0 1 1| I-xori
+-----------------------+---------+-----+---------+-------------+
|       imm[11:0]       |   rs1   |1 1 0|   rd    |0 0 1 0 0 1 1| I-ori
+-----------------------+---------+-----+---------+-------------+
|       imm[11:0]       |   rs1   |1 1 1|   rd    |0 0 1 0 0 1 1| I-andi
+-----------------------+---------+-----+---------+-------------+
|0 0 0 0 0 0 0|  shamt  |   rs1   |0 0 1|   rd    |0 0 1 0 0 1 1| I-slli
+-----------------------+---------+-----+---------+-------------+
|0 0 0 0 0 0 0|  shamt  |   rs1   |1 0 1|   rd    |0 0 1 0 0 1 1| I-srli
+-----------------------+---------+-----+---------+-------------+
|0 1 0 0 0 0 0|  shamt  |   rs1   |1 0 1|   rd    |0 0 1 0 0 1 1| I-srai
+-----------------------+---------+-----+---------+-------------+
|0 0 0 0| pred  | succ  |0 0 0 0 0|0 0 0|0 0 0 0 0|0 0 0 1 1 1 1| I-fence
+-----------------------+---------+-----+---------+-------------+
|0 0 0 0|0 0 0 0|0 0 0 0|0 0 0 0 0|0 0 1|0 0 0 0 0|0 0 0 1 1 1 1| I-fence.i
+-----------------------+---------+-----+---------+-------------+
|0 0 0 0 0 0 0 0 0 0 0 0|0 0 0 0 0| 0 0 |0 0 0 0 0|1 1 1 0 0 1 1| I-ecall
+-----------------------+---------+-----+---------+-------------+
|0 0 0 0 0 0 0 0 0 0 0 0|0 0 0 0 0|0 0 0|0 0 0 0 0|1 1 1 0 0 1 1| I-ebreak
+-----------------------+---------+-----+---------+-------------+
|          csr          |   rs1   |0 0 1|   rd    |1 1 1 0 0 1 1| I-csrrw
+-----------------------+---------+-----+---------+-------------+
|          csr          |   rs1   |0 1 0|   rd    |1 1 1 0 0 1 1| I-csrrs
+-----------------------+---------+-----+---------+-------------+
|          csr          |   rs1   |0 1 1|   rd    |1 1 1 0 0 1 1| I-csrrc
+-----------------------+---------+-----+---------+-------------+
|          csr          |  zimm   |1 0 1|   rd    |1 1 1 0 0 1 1| I-csrrwi
+-----------------------+---------+-----+---------+-------------+
|          csr          |  zimm   |1 1 0|   rd    |1 1 1 0 0 1 1| I-csrrsi
+-----------------------+---------+-----+---------+-------------+
|          csr          |  zimm   |1 1 1|   rd    |1 1 1 0 0 1 1| I-csrrci
+-----------------------+---------+-----+---------+-------------+
+-------------+---------+---------+-----+---------+-------------+
|  imm[11:5]  |   rs2   |   rs1   |0 0 0|imm[4:0] |0 1 0 0 0 1 1| S-sb
+-------------+---------+---------+-----+---------+-------------+
|  imm[11:5]  |   rs2   |   rs1   |0 0 1|imm[4:0] |0 1 0 0 0 1 1| S-sh
+-------------+---------+---------+-----+---------+-------------+
|  imm[11:5]  |   rs2   |   rs1   |0 1 0|imm[4:0] |0 1 0 0 0 1 1| S-sw
+-------------+---------+---------+-----+---------+-------------+
+-------------+---------+---------+-----+---------+-------------+
|i| imm[10:5] |   rs2   |   rs1   |0 0 0|  imm  |i|1 1 0 0 0 1 1| B-beq
+-------------+---------+---------+-----+---------+-------------+
|i| imm[10:5] |   rs2   |   rs1   |0 0 1|  imm  |i|1 1 0 0 0 1 1| B-bne
+-------------+---------+---------+-----+---------+-------------+
|i| imm[10:5] |   rs2   |   rs1   |1 0 0|  imm  |i|1 1 0 0 0 1 1| B-blt
+-------------+---------+---------+-----+---------+-------------+
|i| imm[10:5] |   rs2   |   rs1   |1 0 1|  imm  |i|1 1 0 0 0 1 1| B-bge
+-------------+---------+---------+-----+---------+-------------+
|i| imm[10:5] |   rs2   |   rs1   |1 1 0|  imm  |i|1 1 0 0 0 1 1| B-bltu
+-------------+---------+---------+-----+---------+-------------+
|i| imm[10:5] |   rs2   |   rs1   |1 1 1|  imm  |i|1 1 0 0 0 1 1| B-bgeu
+-------------+---------+---------+-----+---------+-------------+
+---------------------------------------+---------+-------------+
|            imm[31:12]                 |   rd    |0 1 1 0 1 1 1| U-lui
+---------------------------------------+---------+-------------+
|            imm[31:12]                 |   rd    |0 0 1 0 1 1 1| U-auipc
+---------------------------------------+---------+-------------+
+---------------------------------------+---------+-------------+
|i|     imm[10:1]     |i|  imm[19:12]   |   rd    |1 1 0 1 1 1 1| J-jal
+---------------------------------------+---------+-------------+
```

### 1.5 Instruction Operation
| Category    | Format | Instruction           | Full Name                            |Function                                                      |
| ----------- | ------ |---------------------- | ------------------------------------ | ------------------------------------------------------------ |
| shifts      | R      | sll    rd, rs1, rs2   | Shift Left Logical                   | x[rs1] shift left logical x[rs2] bits, fill the empty bits with zero, write to x[rd] |
|             | I      | slli   rd, rs1, shamt | Shift Left Logical Immediate         | x[rs1] shift left logical shamt bits, fill the empty bits with zero, write to x[rd] |
|             | R      | srl    rd, rs1, rs2   | Shift Right Logical                  | x[rs1] shift right logical x[rs2] bits, fill the empty bits with zero, write tox[rd] |
|             | I      | srli   rd, rs1, shamt | Shift Right Logical Immediate        | x[rs1] shift right logical shamt bits, fill the empty bits with zero, write to x[rd] |
|             | R      | sra    rd, rs1, rs2   | Shift Right Arithmetic               | x[rs1] shift right arithmetic x[rs2] bits, fill the empty with highest bit of rs1, write to x[rd] |
|             | I      | srai   rd, rs1, shamt | Shift Right Arithmetic Immediate     | x[rs1] shift right arithmetic shamt bits, fill the empty with highest bit of rs1, write to x[rd] |
| Arithmetic  | R      | add    rd, rs1, rs2   | Add                                  | x[rs1] add x[rs2], write to x[rd] |
|             | I      | addi   rd, rs1, imm   | Add Immediate                        | x[rs1] add imm, write to x[rd] |
|             | R      | sub    rd, rs1, rs2   | Subtract                             | x[rs1] subtract x[rs2], write to x[rd] |
|             | U      | lui    rd, imm        | Load Upper Immediate                 | a 20-bit imm shift left 12 bits, fill the empty 12 bits with zero, write to x[rd] |
|             |  U      | auipc  rd, imm        | Add Upper Immediate to PC            | a 20-bit imm shift left 12 bits, add x[pc], write to x[rd] |
| Logical     | R      | xor    rd, rs1, rs2   | Exclusive-OR                         | x[rs1] xor x[rs2], write to x[rd] |
|             | I      | xori   rd, rs1, imm   | Exclusive-OR Immediate               | x[rs1] xor imm, write to x[rd] |
|             | R      | or     rd, rs1, rs2   | OR                                   | x[rs1] or x[rs2], write to x[rd] |
|             | I      | ori    rd, rs1, imm   | OR Immediate                         | x[rs1] or imm, write to x[rd] |
|             | R      | and    rd, rs1, rs2   | And                                  | x[rs1] and x[rs2], write to x[rd] |
|             | I      | andi   rd, rs1, imm   | And Immediate                        | x[rs1] and imm, write to x[rd] |
| Compare     | R      | slt    rd, rs1, rs2   | Set if Less Than                     | compare x[rs1] and x[rs2], if x[rs1] less, write 1 into x[rd], else write 0 into x[rd] |
|             | I      | slti   rd, rs1, imm   | Set if Less Than Immediate           | compare x[rs1] and imm, if x[rs1] less, write 1 into x[rd], else write 0 into x[rd] |
|             | R      | sltu   rd, rs1, rs2   | Set if Less Than, Unsigned       | compare x[rs1] and x[rs2] consider as unsigned, if x[rs1] less, write 1 into x[rd], else write 0 into x[rd] |
|             | I      | sltiu  rd, rs1, imm   | Set if Less Than Immediate, Unsigned | compare x[rs1] and imm consider as unsigned, if x[rs1] less, write 1 into x[rd], else write 0 into x[rd] |
| Branch      | B      | beq    rs1, rs2, imm  | Branch if Equal                      | if x[rs1] equal x[rs2], x[pc] += sext(imm) |
|             | B      | bne    rs1, rs2, imm  | Branch if Not Equal                  | if x[rs1] not equal x[rs2], x[pc] += sext(imm) |
|             | B      | blt    rs1, rs2, imm  | Branch if Less Than                  | if x[rs1] less than x[rs2], x[pc] += sext(imm) |
|             | B      | bge    rs1, rs2, imm  | Branch if Greater Than or Equal      | if x[rs1] greater than or equal x[rs2], x[pc] += sext(imm) |
|             | B      | bltu   rs1, rs2, imm  | Branch if Less Than, Unsigned        | if x[rs1] less than x[rs2] consider as unsigned, x[pc] += sext(imm) |
|             | B      | bgeu   rs1, rs2, imm  | Branch if Greater Than or Equal, Unsigned | if x[rs1] greater than or equal x[rs2] consider as unsigned, x[pc] += sext(imm) |
| Jump & Link | J      | jal    rd, imm        | Jump and Link                        | x[rd] = x[pc] + 4; pc += sext(imm) |
|             | I      | jalr   rd, rs1, imm   | Jump and Link Register               | t = x[pc] + 4; x[pc] = (x[rs1] + sext(imm))&~1; x[rd] = t |
| Synch       | I      | fence                 | Fence Memory and I/O                 | synchronize thread |
|             | I      | fence.i               | Fence Instruction Stream             | synchronize instruction and date |
| Environment | I      | ecall                 | Environment Call                     | makes a request of the execution environment by raising an Environment Call exception |
|             | I      | ebreak                | Environment Breakpoint               | makes a request of the debugger by raising a Breakpoint exceptionW |
| Control(CSR) | I      | csrrw    rd, csr, rs1 | Control and Status Register Read and Write           | |
|              | I      | csrrs    rd, csr, rs1 | Control and Status Register Read and Set             | |
|              | I      | csrrc    rd, csr, rs1 | Control and Status Register Read and Clear           | |
|              | I      | csrrwi   rd, csr, imm | Control and Status Register Read and Write Immediate | |
|              | I      | csrrsi   rd, csr, imm | Control and Status Register Read and Set Immediate   | |
|              | I      | csrrci   rd, csr, imm | Control and Status Register Read and Clear Immediate | |
| Loads        | I      | lb    rd, rs1, imm   | Load Byte                            | loads one bytes from memory at address x[rs1] + sext(imm) and writes them to x[rd], sext(result)|
|              | I      | lh    rd, rs1, imm   | Load Halfword                        | loads tow bytes from memory at address x[rs1] + sext(imm) and writes them to x[rd], sext(result)|
|              | I      | lbu   rd, rs1, imm   | Load Byte, Unsigned                  | loads one bytes from memory at address x[rs1] + sext(imm) and writes them to x[rd], zext(result)|
|              | I      | lhu   rd, rs1, imm   | Load Halfword, Unsigned              | loads two bytes from memory at address x[rs1] + sext(imm) and writes them to x[rd], zext(result)|
|              | I      | lw    rd, rs1, imm   | Load Word                            | loads four bytes from memory at address x[rs1] + sext(imm) and writes them to x[rd], sext(result)|
| Stores       | S      | sb    rs1, rs2, imm  | Store Byte                           | stores the least-significant byte in x[rs2] at address x[rs1] + sext(imm) |
|              | S      | sh    rs1, rs2, imm  | Store Halfword                       | stores the two least-significant byte in x[rs2] at address x[rs1] + sext(imm) |
|              | S      | sw    rs1, rs2, imm  | Store Word                           | stores the four least-significant byte in x[rs2] at address x[rs1] + sext(imm) |

* sext: sign-extend
* zext: zero-extend

### 1.6 寄存器对照表

## 2. Features
| NO | Features                                  | Advantages |
| -- | ----------------------------------------- | ---------- |
| 1  | only six formats and length fixed 32 bits | simplify instructions decoding |
| 2  | three register operands                   | reduce the number of instructions |
| 3  | the specifiers of the registers to read and written are always in the same location in all instructions | the register aceesees can begin before decoding the instruction |
| 4  | immediate fields are always sign extended, and the sign bit always in the most significant bit of the instruction | sign extension of the immediate before decoding the instruction |
