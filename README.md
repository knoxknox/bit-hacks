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

## resources
- http://www.ml-ip.com/assets/images/bin-num-vals.gif
- https://calleerlandsson.com/2014/02/06/rubys-bitwise-operators/
