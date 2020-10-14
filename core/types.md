# Java Core

|Type   |Default|Size   |Range
|-------|-------|-------|-----
|boolean|false  |1 bit  |
|char   |\u0000 |16 bit |\u0000 - \uFFFF
|byte   |0      |8 bit  |-128 to 127
|short  |0      |16 bit |-32,768 to 32,767
|int    |0      |32 bit |-2*10^9 to 2*10^9
|long   |0      |64 bit |-9*10^18 to 9*10^18
|float  |0.0    |32 bit |upto 7 decimal digits
|double |0.0    |64 bit |upto 16 decimal digits

![](/notes/images/type-conv.png)

![](/notes/images/boxing.jpg)

### Bitwice Operations
|Operator |	Description |	Example |
|-|-|-|
| & (bitwise and) |	Binary AND Operator copies a bit to the result if it exists in both operands. |	(A & B) will give 12 which is 0000 1100 |
| : (bitwise or) |	Binary OR Operator copies a bit if it exists in either operand. |	(A : B) will give 61 which is 0011 1101|
|^ (bitwise XOR) | Binary XOR Operator copies the bit if it is set in one operand but not both. | (A ^ B) will give 49 which is 0011 0001|
|~ (bitwise compliment) |	Binary Ones Complement Operator is unary and has the effect of 'flipping' bits. |	(~A ) will give -61 which is 1100 0011 in 2's complement form due to a signed binary number.|
|<< (left shift) | Binary Left Shift Operator. The left operands value is moved left by the number of bits specified by the right operand.|	A << 2 will give 240 which is 1111 0000|
|>> (right shift) |	Binary Right Shift Operator. The left operands value is moved right by the number of bits specified by the right operand. |	A >> 2 will give 15 which is 1111|
|>>> (zero fill right shift) | Shift right zero fill operator. The left operands value is moved right by the number of bits specified by the right operand and shifted values are filled up with zeros. |	A >>>2 will give 15 which is 0000 1111|
|<<= | Left shift AND assignment operator. | C <<= 2 is same as C = C << 2|
|>>= |	Right shift AND assignment operator. |	C >>= 2 is same as C = C >> 2|
|&= |	Bitwise AND assignment operator. |	C &= 2 is same as C = C & 2|
|^= |	bitwise exclusive OR and assignment operator.|	C ^= 2 is same as C = C ^ 2|
|:= |	bitwise inclusive OR and assignment operator. |	C := 2 is same as C = C : 2|
