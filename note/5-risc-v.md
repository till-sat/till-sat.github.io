# RISC-V

## Instruction formats
| Type   | Usage                            |
| ------ | -------------------------------- |
| R-type | for register-register operations |
| I-type | for short immediates and loads   |
| S-type | for stores                       |
| B-type | for conditional branches         |
| U-type | for long immediates              |
| J-type | for unconditional jumps          |

```
 T S R Q P O N M L K Z I H G F E D C B A 9 8 7 6 5 4 3 2 1 0
+-------------+---------+-----+-----+---------+------------+  
|    func7    |   rs2   | rs1 |func3|   rd    |   opcode   | R-type  
+-------------+---------+-----+-----+---------+------------+  
+-----------------------+-----+-----+---------+------------+
|      imm[11:0]        | rs1 |func3|   rd    |   opcode   | I-type
+-----------------------+-----+-----+---------+------------+
+-----------------------+-----+-----+---------+------------+
|  imm[11:5]  |   rs2   | rs1 |func3|imm[4:0] |   opcode   | S-type
+-----------------------+-----+-----+---------+------------+
+-----------------------+-----+-----+-------+-+------------+
|i| imm[10:5] |   rs2   | rs1 |func3|  imm  |i|   opcode   | B-type
+-----------------------+-----+-----+-------+-+------------+
+-----------------------+-----+-----+---------+------------+
|            imm[31:12]             |   rd    |   opcode   | U-type
+-----------------------+-----+-----+---------+------------+
+-----------------+-+---------------+---------+------------+
|i|   imm[10:1]   |i|  imm[19:12]   |   rd    |   opcode   | J-type
+-----------------+-+---------------+---------+------------+
```

## Features
| NO | Features                                  | Advantages |
| -- | ----------------------------------------- | ---------- |
| 1  | only six formats and fixed length 32 bits | simplify instructions decoding |
| 2  | three register operands                   | reduce the number of instructions |
| 3  | the specifiers of the registers to read and written are always in the same location in all instructions | the register aceesees can begin before decoding the instruction |
| 4  | immediate fields are always sign extended, and the sign bit always in the most significant bit of the instruction | sign extension of the immediate before decoding the instruction |
