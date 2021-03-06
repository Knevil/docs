# web3-utils

This package provides utility functions for Aion dapps and other web3.js packages.

## randomHex

```javascript
web3.utils.randomHex(size)
```

The [randomHex](https://github.com/frozeman/randomHex) library to
generate cryptographically strong pseudo-random HEX strings from a given
byte size.

<h3>Parameters</h3>

1.  `size` - `Number`: The byte size for the HEX string, e.g. `32` will
    result in a 32 bytes HEX string with 64 characters preficed with
    "0x".

<h3>Returns</h3>

`String`: The generated random HEX string.

<h3>Example</h3>

```javascript
web3.utils.randomHex(32)
> "0xa5b9d60f32436310afebcfda832817a68921beb782fabf7915cc0460b443116a"

web3.utils.randomHex(4)
> "0x6892ffc6"

web3.utils.randomHex(2)
> "0x99d6"

web3.utils.randomHex(1)
> "0x9a"

web3.utils.randomHex(0)
> "0x"
```

## \_

```javascript
web3.utils._()
```

The [underscore](http://underscorejs.org) library for many convenience
JavaScript functions.

See the [underscore API reference](http://underscorejs.org) for details.

<h3>Example</h3>

```javascript
var _ = web3.utils._;

_.union([1,2],[3]);
> [1,2,3]

_.each({my: 'object'}, function(value, key){ ... })

...
```

## BN

```javascript
web3.utils.BN(mixed)
```

The [BN.js](https://github.com/indutny/bn.js/) library for calculating
with big numbers in JavaScript. See the [BN.js
documentation](https://github.com/indutny/bn.js/) for details.

<div class="note">

<div class="admonition-title">

Note

</div>

For safe conversion of many types, incl
[BigNumber.js](http://mikemcl.github.io/bignumber.js/) use `utils.toBN
<utils-tobn>`

</div>

<h3>Parameters</h3>

1.  `mixed` - `String|Number`: A number, number string or HEX string to
    convert to a BN object.

<h3>Returns</h3>

`Object`: The [BN.js](https://github.com/indutny/bn.js/) instance.

<h3>Example</h3>

```javascript
var BN = web3.utils.BN;

new BN(1234).toString();
> "1234"

new BN('1234').add(new BN('1')).toString();
> "1235"

new BN('0xea').toString();
> "234"
```



## isBN

```javascript
web3.utils.isBN(bn)
```

Checks if a given value is a [BN.js](https://github.com/indutny/bn.js/)
instance.

<h3>Parameters</h3>

1.  `bn` - `Object`: An [BN.js](https://github.com/indutny/bn.js/)
    instance.

<h3>Returns</h3>

`Boolean`

<h3>Example</h3>

```javascript
var number = new BN(10);

web3.utils.isBN(number);
> true
```



## isBigNumber

```javascript
web3.utils.isBigNumber(bignumber)
```

Checks if a given value is a
[BigNumber.js](http://mikemcl.github.io/bignumber.js/) instance.

<h3>Parameters</h3>

1.  `bignumber` - `Object`: A
    [BigNumber.js](http://mikemcl.github.io/bignumber.js/) instance.

<h3>Returns</h3>

`Boolean`

<h3>Example</h3>

```javascript
var number = new BigNumber(10);

web3.utils.isBigNumber(number);
> true
```



## sha3

```javascript
web3.utils.sha3(string)
web3.utils.keccak256(string) // ALIAS
```

Will calculate the sha3 of the input.

<div class="note">

<div class="admonition-title">

Note

</div>

To mimic the sha3 behaviour of solidity use `soliditySha3
<utils-soliditysha3>`

</div>

<h3>Parameters</h3>

1.  `string` - `String`: A string to hash.

<h3>Returns</h3>

`String`: the result hash.

<h3>Example</h3>

```javascript
web3.utils.sha3('234'); // taken as string
> "0xc1912fee45d61c87cc5ea59dae311904cd86b84fee17cc96966216f811ce6a79"

web3.utils.sha3(new BN('234'));
> "0xbc36789e7a1e281436464229828f817d6612f7b477d66591ff96a9e064bcc98a"

web3.utils.sha3(234);
> null // can't calculate the has of a number

web3.utils.sha3(0xea); // same as above, just the HEX representation of the number
> null

web3.utils.sha3('0xea'); // will be converted to a byte array first, and then hashed
> "0x2f20677459120677484f7104c76deb6846a2c071f9b3152c103bb12cd54d1a4a"
```



## soliditySha3

```javascript
web3.utils.soliditySha3(param1 [, param2, ...])
```

Will calculate the sha3 of given input parameters in the same way
solidity would. This means arguments will be ABI converted and tightly
packed before being hashed.

<h3>Parameters</h3>

1.  `paramX` - `Mixed`: Any type, or an object with `{type: 'uint',
    value: '123456'}` or `{t: 'bytes', v: '0xfff456'}`. Basic types are
    autodetected as follows:
    
    >   - `String` non numerical UTF-8 string is interpreted as
    >     `string`.
    >   - `String|Number|BN|HEX` positive number is interpreted as
    >     `uint256`.
    >   - `String|Number|BN` negative number is interpreted as `int256`.
    >   - `Boolean` as `bool`.
    >   - `String` HEX string with leading `0x` is interpreted as
    >     `bytes`.
    >   - `HEX` HEX number representation is interpreted as `uint256`.

<h3>Returns</h3>

`String`: the result hash.

<h3>Example</h3>

```javascript
web3.utils.soliditySha3('234564535', '0xfff23243', true, -10);
// auto detects:        uint256,      bytes,     bool,   int256
> "0x3e27a893dc40ef8a7f0841d96639de2f58a132be5ae466d40087a2cfa83b7179"


web3.utils.soliditySha3('Hello!%'); // auto detects: string
> "0x661136a4267dba9ccdf6bfddb7c00e714de936674c4bdb065a531cf1cb15c7fc"


web3.utils.soliditySha3('234'); // auto detects: uint256
> "0x61c831beab28d67d1bb40b5ae1a11e2757fa842f031a2d0bc94a7867bc5d26c2"

web3.utils.soliditySha3(0xea); // same as above
> "0x61c831beab28d67d1bb40b5ae1a11e2757fa842f031a2d0bc94a7867bc5d26c2"

web3.utils.soliditySha3(new BN('234')); // same as above
> "0x61c831beab28d67d1bb40b5ae1a11e2757fa842f031a2d0bc94a7867bc5d26c2"

web3.utils.soliditySha3({type: 'uint256', value: '234'})); // same as above
> "0x61c831beab28d67d1bb40b5ae1a11e2757fa842f031a2d0bc94a7867bc5d26c2"

web3.utils.soliditySha3({t: 'uint', v: new BN('234')})); // same as above
> "0x61c831beab28d67d1bb40b5ae1a11e2757fa842f031a2d0bc94a7867bc5d26c2"


web3.utils.soliditySha3('0x407D73d8a49eeb85D32Cf465507dd71d507100c1');
> "0x4e8ebbefa452077428f93c9520d3edd60594ff452a29ac7d2ccc11d47f3ab95b"

web3.utils.soliditySha3({t: 'bytes', v: '0x407D73d8a49eeb85D32Cf465507dd71d507100c1'});
> "0x4e8ebbefa452077428f93c9520d3edd60594ff452a29ac7d2ccc11d47f3ab95b" // same result as above


web3.utils.soliditySha3({t: 'address', v: '0x407D73d8a49eeb85D32Cf465507dd71d507100c1'});
> "0x4e8ebbefa452077428f93c9520d3edd60594ff452a29ac7d2ccc11d47f3ab95b" // same as above, but will do a checksum check, if its multi case


web3.utils.soliditySha3({t: 'bytes32', v: '0x407D73d8a49eeb85D32Cf465507dd71d507100c1'});
> "0x3c69a194aaf415ba5d6afca734660d0a3d45acdc05d54cd1ca89a8988e7625b4" // different result as above


web3.utils.soliditySha3({t: 'string', v: 'Hello!%'}, {t: 'int8', v:-23}, {t: 'address', v: '0x85F43D8a49eeB85d32Cf465507DD71d507100C1d'});
> "0xa13b31627c1ed7aaded5aecec71baf02fe123797fffd45e662eac8e06fbe4955"
```



## isHex

```javascript
web3.utils.isHex(hex)
```

Checks if a given string is a HEX string.

<h3>Parameters</h3>

1.  `hex` - `String|HEX`: The given HEX string.

<h3>Returns</h3>

`Boolean`

<h3>Example</h3>

```javascript
web3.utils.isHex('0xc1912');
> true

web3.utils.isHex(0xc1912);
> true

web3.utils.isHex('c1912');
> true

web3.utils.isHex(345);
> true // this is tricky, as 345 can be a a HEX representation or a number, be careful when not having a 0x in front!

web3.utils.isHex('0xZ1912');
> false

web3.utils.isHex('Hello');
> false
```



## isHexStrict

```javascript
web3.utils.isHexStrict(hex)
```

Checks if a given string is a HEX string. Difference to
`web3.utils.isHex()` is that it expects HEX to be prefixed with `0x`.

<h3>Parameters</h3>

1.  `hex` - `String|HEX`: The given HEX string.

<h3>Returns</h3>

`Boolean`

<h3>Example</h3>

```javascript
web3.utils.isHexStrict('0xc1912');
> true

web3.utils.isHexStrict(0xc1912);
> false

web3.utils.isHexStrict('c1912');
> false

web3.utils.isHexStrict(345);
> false // this is tricky, as 345 can be a a HEX representation or a number, be careful when not having a 0x in front!

web3.utils.isHexStrict('0xZ1912');
> false

web3.utils.isHex('Hello');
> false
```



## isAddress

```javascript
web3.utils.isAddress(address)
```

Checks if a given string is a valid Aion address. It will also check
the checksum, if the address has upper and lowercase letters.

<h3>Parameters</h3>

1.  `address` - `String`: An address string.

<h3>Returns</h3>

`Boolean`

<h3>Example</h3>

```javascript
web3.utils.isAddress('0xc1912fee45d61c87cc5ea59dae31190fffff232d');
> true

web3.utils.isAddress('c1912fee45d61c87cc5ea59dae31190fffff232d');
> true

web3.utils.isAddress('0XC1912FEE45D61C87CC5EA59DAE31190FFFFF232D');
> true // as all is uppercase, no checksum will be checked

web3.utils.isAddress('0xc1912fEE45d61C87Cc5EA59DaE31190FFFFf232d');
> true

web3.utils.isAddress('0xC1912fEE45d61C87Cc5EA59DaE31190FFFFf232d');
> false // wrong checksum
```



## toChecksumAddress

```javascript
web3.utils.toChecksumAddress(address)
```

Will convert an upper or lowercase Aion address to a checksum
address.

<h3>Parameters</h3>

1.  `address` - `String`: An address string.

<h3>Returns</h3>

`String`: The checksum
address.

<h3>Example</h3>

```javascript
web3.utils.toChecksumAddress('0xc1912fee45d61c87cc5ea59dae31190fffff2323');
> "0xc1912fEE45d61C87Cc5EA59DaE31190FFFFf232d"

web3.utils.toChecksumAddress('0XC1912FEE45D61C87CC5EA59DAE31190FFFFF232D');
> "0xc1912fEE45d61C87Cc5EA59DaE31190FFFFf232d" // same as above
```



## checkAddressChecksum

```javascript
web3.utils.checkAddressChecksum(address)
```

Checks the checksum of a given address. Will also return false on
non-checksum addresses.

<h3>Parameters</h3>

1.  `address` - `String`: An address string.

<h3>Returns</h3>

`Boolean`: `true` when the checksum of the address is valid, `false` if
its not a checksum address, or the checksum is
invalid.

<h3>Example</h3>

```javascript
web3.utils.checkAddressChecksum('0xc1912fEE45d61C87Cc5EA59DaE31190FFFFf232d');
> true
```



## toHex

```javascript
web3.utils.toHex(mixed)
```

Will auto convert any given value to HEX. Number strings will
interpreted as numbers. Text strings will be interpreted as UTF-8
strings.

<h3>Parameters</h3>

1.  `mixed` - `String|Number|BN|BigNumber`: The input to convert to HEX.

<h3>Returns</h3>

`String`: The resulting HEX string.

<h3>Example</h3>

```javascript
web3.utils.toHex('234');
> "0xea"

web3.utils.toHex(234);
> "0xea"

web3.utils.toHex(new BN('234'));
> "0xea"

web3.utils.toHex(new BigNumber('234'));
> "0xea"

web3.utils.toHex('I have 100€');
> "0x49206861766520313030e282ac"
```



## toBN

```javascript
web3.utils.toBN(number)
```

Will safly convert any given value (including
[BigNumber.js](http://mikemcl.github.io/bignumber.js/) instances) into a
[BN.js](https://github.com/indutny/bn.js/) instance, for handling big
numbers in JavaScript.

<div class="note">

<div class="admonition-title">

Note

</div>

For just the [BN.js](https://github.com/indutny/bn.js/) class use
`utils.BN <utils-bn>`

</div>

<h3>Parameters</h3>

1.  `number` - `String|Number|HEX`: Number to convert to a big number.

<h3>Returns</h3>

`Object`: The [BN.js](https://github.com/indutny/bn.js/) instance.

<h3>Example</h3>

```javascript
web3.utils.toBN(1234).toString();
> "1234"

web3.utils.toBN('1234').add(web3.utils.toBN('1')).toString();
> "1235"

web3.utils.toBN('0xea').toString();
> "234"
```



## hexToNumberString

```javascript
web3.utils.hexToNumberString(hex)
```

Returns the number representation of a given HEX value as a string.

<h3>Parameters</h3>

1.  `hexString` - `String|HEX`: A string to hash.

<h3>Returns</h3>

`String`: The number as a string.

<h3>Example</h3>

```javascript
web3.utils.hexToNumberString('0xea');
> "234"
```



## hexToNumber

```javascript
web3.utils.hexToNumber(hex)
web3.utils.toDecimal(hex) // ALIAS, deprecated
```

Returns the number representation of a given HEX value.

<div class="note">

<div class="admonition-title">

Note

</div>

This is not useful for big numbers, rather use `utils.toBN <utils-tobn>`
instead.

</div>

<h3>Parameters</h3>

1.  `hexString` - `String|HEX`: A string to hash.

<h3>Returns</h3>

`Number`

<h3>Example</h3>

```javascript
web3.utils.hexToNumber('0xea');
> 234
```



## numberToHex

```javascript
web3.utils.numberToHex(number)
web3.utils.fromDecimal(number) // ALIAS, deprecated
```

Returns the HEX representation of a given number value.

<h3>Parameters</h3>

1.  `number` - `String|Number|BN|BigNumber`: A number as string or
    number.

<h3>Returns</h3>

`String`: The HEX value of the given number.

<h3>Example</h3>

```javascript
web3.utils.numberToHex('234');
> '0xea'
```



## hexToUtf8

```javascript
web3.utils.hexToUtf8(hex)
web3.utils.hexToString(hex) // ALIAS
web3.utils.toUtf8(hex) // ALIAS, deprecated
```

Returns the UTF-8 string representation of a given HEX value.

<h3>Parameters</h3>

1.  `hex` - `String`: A HEX string to convert to a UTF-8 string.

<h3>Returns</h3>

`String`: The UTF-8 string.

<h3>Example</h3>

```javascript
web3.utils.hexToUtf8('0x49206861766520313030e282ac');
> "I have 100€"
```



## hexToAscii

```javascript
web3.utils.hexToAscii(hex)
web3.utils.toAscii(hex) // ALIAS, deprecated
```

Returns the ASCII string representation of a given HEX value.

<h3>Parameters</h3>

1.  `hex` - `String`: A HEX string to convert to a ASCII string.

<h3>Returns</h3>

`String`: The ASCII string.

<h3>Example</h3>

```javascript
web3.utils.hexToAscii('0x4920686176652031303021');
> "I have 100!"
```



## utf8ToHex

```javascript
web3.utils.utf8ToHex(string)
web3.utils.stringToHex(string) // ALIAS
web3.utils.fromUtf8(string) // ALIAS, deprecated
```

Returns the HEX representation of a given UTF-8 string.

<h3>Parameters</h3>

1.  `string` - `String`: A UTF-8 string to convert to a HEX string.

<h3>Returns</h3>

`String`: The HEX string.

<h3>Example</h3>

```javascript
web3.utils.utf8ToHex('I have 100€');
> "0x49206861766520313030e282ac"
```



## asciiToHex

```javascript
web3.utils.asciiToHex(string)
web3.utils.fromAscii(string) // ALIAS, deprecated
```

Returns the HEX representation of a given ASCII string.

<h3>Parameters</h3>

1.  `string` - `String`: A ASCII string to convert to a HEX string.

<h3>Returns</h3>

`String`: The HEX string.

<h3>Example</h3>

```javascript
web3.utils.asciiToHex('I have 100!');
> "0x4920686176652031303021"
```



## hexToBytes

```javascript
web3.utils.hexToBytes(hex)
```

Returns a byte array from the given HEX string.

<h3>Parameters</h3>

1.  `hex` - `String|HEX`: A HEX to convert.

<h3>Returns</h3>

`Array`: The byte array.

<h3>Example</h3>

```javascript
web3.utils.hexToBytes('0x000000ea');
> [ 0, 0, 0, 234 ]

web3.utils.hexToBytes(0x000000ea);
> [ 234 ]
```



## bytesToHex

```javascript
web3.utils.bytesToHex(byteArray)
```

Returns a HEX string from a byte array.

<h3>Parameters</h3>

1.  `byteArray` - `Array`: A byte array to convert.

<h3>Returns</h3>

`String`: The HEX string.

<h3>Example</h3>

```javascript
web3.utils.bytesToHex([ 72, 101, 108, 108, 111, 33, 36 ]);
> "0x48656c6c6f2125"
```

## padLeft

```javascript
web3.utils.padLeft(string, characterAmount [, sign])
web3.utils.leftPad(string, characterAmount [, sign]) // ALIAS
```

Adds a padding on the left of a string, Useful for adding paddings to
HEX strings.

<h3>Parameters</h3>

1.  `string` - `String`: The string to add padding on the left.
2.  `characterAmount` - `Number`: The number of characters the total
    string should have.
3.  `sign` - `String` (optional): The character sign to use, defaults to
    `"0"`.

<h3>Returns</h3>

`String`: The padded string.

<h3>Example</h3>

```javascript
web3.utils.padLeft('0x3456ff', 20);
> "0x000000000000003456ff"

web3.utils.padLeft(0x3456ff, 20);
> "0x000000000000003456ff"

web3.utils.padLeft('Hello', 20, 'x');
> "xxxxxxxxxxxxxxxHello"
```

## padRight

```javascript
web3.utils.padRight(string, characterAmount [, sign])
web3.utils.rightPad(string, characterAmount [, sign]) // ALIAS
```

Adds a padding on the right of a string, Useful for adding paddings to
HEX strings.

<h3>Parameters</h3>

1.  `string` - `String`: The string to add padding on the right.
2.  `characterAmount` - `Number`: The number of characters the total
    string should have.
3.  `sign` - `String` (optional): The character sign to use, defaults to
    `"0"`.

<h3>Returns</h3>

`String`: The padded string.

<h3>Example</h3>

```javascript
web3.utils.padRight('0x3456ff', 20);
> "0x3456ff00000000000000"

web3.utils.padRight(0x3456ff, 20);
> "0x3456ff00000000000000"

web3.utils.padRight('Hello', 20, 'x');
> "Helloxxxxxxxxxxxxxxx"
```

## toTwosComplement

```javascript
web3.utils.toTwosComplement(number)
```

Converts a negative numer into a two's complement.

<h3>Parameters</h3>

1.  `number` - `Number|String|BigNumber`: The number to convert.

<h3>Returns</h3>

`String`: The converted hex string.

<h3>Example</h3>

```javascript
web3.utils.toTwosComplement('-1');
> "0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff"

web3.utils.toTwosComplement(-1);
> "0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff"

web3.utils.toTwosComplement('0x1');
> "0x0000000000000000000000000000000000000000000000000000000000000001"

web3.utils.toTwosComplement(-15);
> "0xfffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff1"

web3.utils.toTwosComplement('-0x1');
> "0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff"
```

## toNAmp

```javascript
web3.utils.toNAmp(number [, unit])
```

Converts any `Aion` value value into `Amp`. `Amp` are the smallest Aion unit, and you should always make calculations in `Amp` and convert only for display reasons.

<h3>Parameters</h3>

1. `number` - **String**|**Number**: The value.
2. `unit` - **String** (optional, defaults to `aion`): The aion to convert from. Possible units are:
    - `namp`: `1`,
    - `uamp`: `1000`,
    - `mamp`: `1000000`,
    - `amp`: `1000000000`,
    - `uaion`: `1000000000000`,
    - `maion`: `1000000000000000`,
    - `caion`: `10000000000000000`,
    - `daion`: `100000000000000000`,
    - `aion`: `100000000000000000`'

<h3>Returns</h3>

`String`: If a number, or string is given it returns a number string.

<h3>Example</h3>

```javascript
web3.utils.toNAmp('3.141592654')
>'3141592654000000000'

web3.utils.toNAmp('0.000000000000000001')
>'1'

web3.utils.toNAmp('1', 'namp')
> '1'
```

## fromNAmp

```javascript
web3.utils.fromNAmp(number [, unit])
```

Converts any `Amp` value into a `Aion` value. `Amp` are the smallest `Aion` unit, and you should always make calculations in `Amp` and convert only for display reasons.

<h3>Parameters</h3>

1. `number` - **String**|**Number**: The value.
2. `unit` - **String** (optional, defaults to `aion`): The aion to convert from. Possible units are:
    - `namp`: `1`,
    - `uamp`: `1000`,
    - `mamp`: `1000000`,
    - `amp`: `1000000000`,
    - `uaion`: `1000000000000`,
    - `maion`: `1000000000000000`,
    - `caion`: `10000000000000000`,
    - `daion`: `100000000000000000`,
    - `aion`: `100000000000000000`'

<h3>Returns</h3>

`String`: If a number, or string is given it returns a number string.

<h3>Example</h3>

```javascript
web3.utils.fromNAmp('3141592654000000000')
>'3.141592654'

web3.utils.fromNAmp('1')
>'0.000000000000000001'

web3.utils.fromNAmp('1', 'namp')
> '1'
```

<h1>Need Help?</h1>

If you get stuck, head over to our [Gitter channels](https://gitter.im/aionnetwork/Lobby) or [StackOverflow](https://stackoverflow.com/search?q=aion) for answers to some common questions.