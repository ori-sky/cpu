### Registers

* Scalar registers are 32 bits in width.
* Vector registers are comprised of 4 scalar elements.

###### *Table 1*
| REGISTERS              | DESCRIPTION                                     |
| ---------------------- | ----------------------------------------------- |
| `A`, `B`, `C`, `D`     | general-purpose scalar registers                |
| `V0`, `V1`, `V2`, `V3` | general-purpose vector registers                |
| `X`, `Y`, `Z`, `W`     | scalar elements of the *active vector register* |
| `IP`                   | instruction pointer                             |
| `SP`                   | stack pointer                                   |

### Instruction Set

Instructions are represented by 1 or more bytes. The number of bytes is determined by the operands that an instruction takes. The first byte is as follows. Note that bit `0` refers to the least significant bit and bit `7` refers to the most significant bit. *Table 2* displays the structure of the first byte of an instruction.

###### *Table 2*
| BITS  | DESCRIPTION       |
| ----- | ----------------- |
| `0-4` | local opcode      |
| `5-7` | positional opcode |

The **positional opcode** represents the category assigned to an instruction. Instructions similar in operation to each other have matching positional opcodes and are distinguished by their **local opcode**. An instruction can be uniquely identified entirely by its first byte.

For brevity, the two portions of the first byte of an instruction are usually shortened to **category** and **opcode**. *Table 4* displays a list of categories and their meanings.

###### *Table 4*
| CATEGORY | DESCRIPTION |
| -------- | ----------- |

*Table 6*, immediately preceded by *Table 5*, displays a list of instructions and their corresponding components, with a brief description of the function of each instruction. For mnemonics with two operands representing a **source** and a **destination**, the destination is always the first operand with the source being the second operand.

*Table 5* below displays the meaning of each character used to represent operands in *Table 6*.

###### *Table 5*
| CHARACTER | DESCRIPTION              |
| --------- | ------------------------ |
| `s`       | scalar register          |
| `v`       | vector register          |
| `i`       | immediate/constant value |

###### *Table 6*
| MNEMONIC        | CATEGORY | OPCODE | DESCRIPTION                                      |
| --------------- | -------- | ------ | ------------------------------------------------ |
| `NOP`           | `0x0`    | `0x0`  | no operation                                     |
| `MOV    s1, s0` | `0x1`    | `0x0`  | move value at `s0` into `s1`                     |
| `MOV    s,  i`  | `0x1`    | `0x1`  | move immediate value into `s`                    |
| `VMOV   v1, v0` | `0x1`    | `0x2`  | move value at `v0` into `v1`                     |
| `VMOVVX v,  s`  | `0x1`    | `0x3`  | move value at `s` into `v` by value-extension    |
| `VMOVVX v,  i`  | `0x1`    | `0x4`  | move immediate value into `v` by value-extension |
| `VMOVZX v,  s`  | `0x1`    | `0x5`  | move value at `s` into `v` by zero-extension     |
| `VMOVZX v,  i`  | `0x1`    | `0x6`  | move immediate value into `v` by zero-extension  |
| `VMOV1X v,  s`  | `0x1`    | `0x7`  | move value at `s` into `v` by one-extension      |
| `VMOV1X v,  i`  | `0x1`    | `0x8`  | move immediate value into `v` by one-extension   |
| `AVR0`          | `0x2`    | `0x0`  | activate vector register 0                       |
| `AVR1`          | `0x2`    | `0x1`  | activate vector register 1                       |
| `AVR2`          | `0x2`    | `0x2`  | activate vector register 2                       |
| `AVR3`          | `0x2`    | `0x3`  | activate vector register 3                       |
