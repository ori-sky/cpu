### Registers

* Scalar registers are 32 bits in width.
* Vector registers are comprised of 4 scalar elements.

| REGISTERS              | DESCRIPTION                      |
| ---------------------- | -------------------------------- |
| `A`, `B`, `C`, `D`     | general-purpose scalar registers |
| `V0`, `V1`, `V2`, `V3` | general-purpose vector registers |
| `X`, `Y`, `Z`, `W`     | scalar elements of `V0`          |
| `IP`                   | instruction pointer              |
| `SP`                   | stack pointer                    |

### Instruction Set

Instructions are represented by 1-3 bytes. The number of bytes is determined by the **operating mode** which is 2 bits in width. The first byte is as follows.

| BITS  | DESCRIPTION       |
| ----- | ----------------- |
| `0-1` | operating mode    |
| `2-4` | positional opcode |
| `5-7` | local opcode      |

Bits `0` and `1` of the **operating mode** represent the states of the second and third bytes of an instruction respectively. If bit `1` is set then bit `0` must also be set as this operating mode is reserved.

| OPERATING MODE | DESCRIPTION                           |
| -------------- | ------------------------------------- |
| `0b00`         | second and third bytes are **unused** |
| `0b10`         | second byte is **used**               |
| `0b11`         | second and third bytes are **used**   |
| `0b01`         | reserved                              |
