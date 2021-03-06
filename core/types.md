## Java Core

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

### Перевод из 10й в 2ю системы счисления
|    |   |    |
|-|-|-|
| 61 | 2 |    |
| 30 | 2 | - 1|  
| 15 | 2 | - 0|
| 7  | 2 | - 1|
| 3  | 2 | - 1|
| 1  | 2 | - 1|
|    |   | - 1 1 1 1 0 1|

111101 = 1·2^5 + 1·2^4 + 1·2^3 + 1·2^2 + 0·2^1 + 1·2^0 = 61

### Bitwice Operations

| & (and)  |\| (or) |~ (not) |^ (xor)
|----------|-       |-       |-
| 11001010 |11001010|11001010|11001010
| 11100010 |11100010|        |11100010
| -------- |--------|--------|--------
| 11000010 |11101010|00110101|00101000

xor - result is 1 if initial variables are different.

### Bitwice shifts
Операторы сдвига << и >> сдвигают биты в переменной влево или вправо на указанное число. При этом на освободившиеся позиции устанавливаются <b>нули</b>.
Для сдвига вправо отрицательного числа устанавливаются <b>единицы</b>.

> x >> 1 - деление на 2  
  x << 1 - умножение на 2

```
x = 7         // 00000111 (7)
x = x >> 1    // 00000011 (3)
x = x << 1    // 00000110 (6)
x = x << 5    // 11000000 (-64)
x = x >> 2    // 11110000 (-16)
```

###### Беззнакового битового сдвига вправо >>>
На освободившиеся позиции всегда устанавливаются <b>нули</b>
```
x = 7          // 00000111 (7)
x = x << 5     // 11100000 (-32)
x = x >>> 2    // 00111000 (56)
```

#### Bitwice operations example
