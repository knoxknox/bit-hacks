# bit-hacks

## notation
```
|   -  bitwise or
&   -  bitwise and
~   -  bitwise not
^   -  bitwise xor
<<  -  bitwise shift left
>>  -  bitwise shift right
```

## operations
```
not(0) = 1 => ~0
not(1) = 0 => ~1

0 or 0 = 0 => 0|0
0 or 1 = 1 => 0|1
1 or 0 = 1 => 1|0
1 or 1 = 1 => 1|1

0 and 0 = 0 => 0&0
0 and 1 = 0 => 0&1
1 and 0 = 0 => 1&0
1 and 1 = 1 => 1&1

0 xor 0 = 0 => 0^0
0 xor 1 = 1 => 0^1
1 xor 0 = 1 => 1^0
1 xor 1 = 0 => 1^1
```
```
x & x = x   => 1010 & 1010 == 1010
x & 0s = 0  => 1010 & 0000 == 0000
x & 1s = x  => 1010 & 1111 == 1010

x | x = x   => 1010 | 1010 == 1010
x | 0s = x  => 1010 | 0000 == 1010
x | 1s = 1s => 1010 | 1111 == 1111

x ^ x = 0   => 1010 ^ 1010 == 0000
x ^ 0s = x  => 1010 ^ 0000 == 1010
x ^ 1s = ~x => 1010 ^ 1111 == 0101
```

## 1: odd or even
```
((x & 1) != 0) ? 'odd' : 'even'
```
```
((1 & 1) != 0) ? 'odd' : 'even' => 'odd'
((5 & 1) != 0) ? 'odd' : 'even' => 'odd'
((8 & 1) != 0) ? 'odd' : 'even' => 'even'
```

## 2: check n-th bit
```
(x & (1<<n) != 0) ? 'set' : 'not set'
```
```
(0b0010 & (1<<1) != 0) ? 'set' : 'not set' => 'set'
(0b0010 & (1<<3) != 0) ? 'set' : 'not set' => 'not set'
```

## 3: get the n-th bit
```
(x>>n) & 1
```
```
(0b1001>>0) & 1 => '1'
(0b1001>>1) & 1 => '0'
(0b1001>>3) & 1 => '1'
```

## 4: set the n-th bit
```
x | (1<<n)
```
```
0b0010 | (1<<0) => '0011'
0b0010 | (1<<1) => '0010'
0b0010 | (1<<3) => '1010'
```

## 5: unset the n-th bit
```
x & ~(1<<n)
```
```
0b1111 & ~(1<<0) => '1110'
0b1111 & ~(1<<1) => '1101'
0b1111 & ~(1<<3) => '0111'
```

## 6: toggle the n-th bit
```
x ^ (1<<n)
```
```
0b1101 ^ (1<<0) => '1100'
0b1101 ^ (1<<1) => '1111'
0b1101 ^ (1<<3) => '0101'
```

## 7: shift-left & shift-right
```
2 << 1 => '4', the same as 2 * (2**1)
2 << 2 => '8', the same as 2 * (2**2)
8 >> 1 => '4', the same as 8 / (2**1)
8 >> 2 => '2', the same as 8 / (2**2)
9 >> 2 => '2', the same as 9 / (2**2)
9 << 4 => '144', the same as 9 * (2**4)
```

## 8: manipulation with bytes in ruby
```
97         => dec (97)
0x61       => hex (97)
0141       => octal (97)
0b01100001 => binary (97)
```
```
97.to_s(2)  => base 2 (bin)
97.to_s(8)  => base 8 (oct)
97.to_s(10) => base 10 (dec)
97.to_s(16) => base 16 (hex)
```
```
97.chr => 'a'
'a'.ord => 97
[97, 0x61, 0141, 0b01100001] => [97, 97, 97, 97]
'string'.bytes => [115, 116, 114, 105, 110, 103]
```
```
# bytes to string
bytes = 'string'.bytes
bytes.pack('c*') => 'string' (pack as 8-bit signed int)
bytes.pack('C*') => 'string' (pack as 8-bit unsigned int)
['string'].pack('m0') => 'c3RyaW5n' (base64 encoded string)
```
```
# string to bytes
'string'.unpack('c*') => [115, 116, 114, 105, 110, 103]
'string'.unpack('C*') => [115, 116, 114, 105, 110, 103]
'c3RyaW5n'.unpack('m0') => 'string' (base64 decoded string)
```
```
# example of decoding
=> b - bit string (LSB first)
=> B - bit string (MSB first)
=> h - hex string (low nibble first)
=> H - hex string (high nibble first)

'string'.unpack('H*').first => '737472696e67'
'string'.bytes.map { |x| x.to_s(16) }.join => '737472696e67'

'string'.unpack('B*').first => 011100...100111
'string'.bytes.map { |x| x.to_s(02) }.join => 011100...100111
```

## resources
- https://calleerlandsson.com/rubys-bitwise-operators
- http://2016-aalto-c.mooc.fi/en/static/pics/bit-ops.jpg
- http://2016-aalto-c.mooc.fi/en/static/pics/bit-shift.jpg
- http://2016-aalto-c.mooc.fi/en/static/pics/byte-order.jpg
