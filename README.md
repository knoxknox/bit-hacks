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

## 3: set the n-th bit
```
x | (1<<n)
```
```
0b0010 | (1<<0) => '0011'
0b0010 | (1<<1) => '0010'
0b0010 | (1<<3) => '1010'
```

## 4: unset the n-th bit
```
x & ~(1<<n)
```
```
0b1111 & ~(1<<0) => '1110'
0b1111 & ~(1<<1) => '1101'
0b1111 & ~(1<<3) => '0111'
```

## 5: toggle the n-th bit
```
x ^ (1<<n)
```
```
0b1101 ^ (1<<0) => '1100'
0b1101 ^ (1<<1) => '1111'
0b1101 ^ (1<<3) => '0101'
```

## 6: shift-left & shift-right
```
2 << 1 => '4', the same as 2 * (2**1)
2 << 2 => '8', the same as 2 * (2**2)
8 >> 1 => '4', the same as 8 / (2**1)
8 >> 2 => '2', the same as 8 / (2**2)
9 >> 2 => '2', the same as 9 / (2**2)
9 << 4 => '144', the same as 9 * (2**4)
```

## 7: manipulation with bytes in ruby
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
'c3RyaW5n'.unpack('m0') => decoded from base64 as 'string'
```
```
# example of xor strings
sequence1, sequence2 = 'string1'.bytes, 'string2'.bytes
sequence1.zip(sequence2).map { |(x, y)| x ^ y }.pack('c*')
```

## resources
- http://2016-aalto-c.mooc.fi/en/static/pics/bit-ops.jpg
- http://2016-aalto-c.mooc.fi/en/static/pics/bit-shift.jpg
- http://2016-aalto-c.mooc.fi/en/static/pics/byte-order.jpg
- https://calleerlandsson.com/2014/02/06/rubys-bitwise-operators/
