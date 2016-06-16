### Registers

* Scalar registers are 32 bits in width.
* Vector registers are comprised of 4 scalar elements.

###### *Table 1*
| REGISTERS              | DESCRIPTION                      |
| ---------------------- | -------------------------------- |
| `A`, `B`, `C`, `D`     | general-purpose scalar registers |
| `V0`, `V1`, `V2`, `V3` | general-purpose vector registers |
| `X`, `Y`, `Z`, `W`     | scalar elements of `V0`          |
| `IP`                   | instruction pointer              |
| `SP`                   | stack pointer                    |

### Instruction Set

Instructions are represented by 1-3 bytes. The number of bytes is determined by the **operating mode** which is 2 bits in width. The first byte is as follows. Note that bit `0` refers to the least significant bit and bit `7` refers to the most significant bit. *Table 2* displays the structure of the first byte of an instruction.

###### *Table 2*
| BITS  | DESCRIPTION       |
| ----- | ----------------- |
| `0-1` | operating mode    |
| `2-4` | local opcode      |
| `5-7` | positional opcode |

Bits `0` and `1` of the **operating mode** represent the states of the second and third bytes of an instruction respectively. If bit `1` is set then bit `0` must also be set, as otherwise is reserved behaviour. *Table 3* displays the four possible operating modes.

###### *Table 3*
| OPERATING MODE | DESCRIPTION                           |
| -------------- | ------------------------------------- |
| `0b00`         | second and third bytes are **unused** |
| `0b01`         | second byte is **used**               |
| `0b11`         | second and third bytes are **used**   |
| `0b10`         | reserved                              |

The **positional opcode** represents the category assigned to an instruction. Instructions similar in operation to each other have matching positional opcodes and are distinguished by their **local opcode**. An instruction can be uniquely identified entirely by its first byte.

For brevity, the three portions of the first byte of an instruction are usually shortened to **category**, **opcode**, and **mode**. *Table 4* displays a list of categories and their meanings.

###### *Table 4*
| CATEGORY | DESCRIPTION |
| -------- | ----------- |

*Table 6*, immediately preceded by *Table 5*, displays a list of instructions and their corresponding components, with a brief description of the function of each instruction. For mnemonics with two operands representing a **source** and a **destination**, the destination is always the first operand with the source being the second operand.

*Table 5* below displays the meaning of each character used to represent operands in *Table 6*.

###### *Table 5*
| CHARACTER | DESCRIPTION              |
| --------- | ------------------------ |
| `i`       | immediate/constant value |
| `s`       | scalar register          |
| `v`       | vector register          |

###### *Table 6*
| MNEMONIC     | CATEGORY | OPCODE | MODE   | DESCRIPTION                   |
| ------------ | -------- | ------ | ------ | ----------------------------- |
| `NOP`        | `0x0`    | `0x0`  | `0x00` | no operation                  |
| `MOV s,  i`  | `0x1`    | `0x1`  | `0x01` | move immediate value into `s` |
| `MOV s2, s1` | `0x1`    | `0x2`  | `0b11` | move value at `s1` into `s2`  |
