---
Title: web3-eth-personal
---

# web3-eth-personal

The `web3-eth-personal` package allows you to interact with the Aion node accounts.

Many of these functions send sensitive information, like `password`. Never call these functions over an unsecured WebSocket or HTTP provider, as your password will be sent in plain text!

```javascript
var Personal = require('web3-eth-personal');

// "Personal.providers.givenProvider" will be set if in an Aion supported browser.
var personal = new Personal(Personal.givenProvider || 'ws://some.local-or-remote.node:8546');
```

## newAccount

```javascript
web3.eth.personal.newAccount(password, [callback])
```

Creates a new account. **Never call this function over an unsecured WebSocket or HTTP provider, as your password will be sent in plain text!**

<h3>Parameters</h3>

1. `password` - **String**: The password to encrypt this account with.

<h3>Returns</h3>

`Promise` returns **String**: The address of the newly created account.

<h3>Example</h3>

```javascript
web3.eth.personal.newAccount('!@superpassword')
.then(console.log);
> '0x1234567891011121314151617181920212223456'
```

## sign

```javascript
web3.eth.personal.sign(dataToSign, address, password [, callback])
```

Signs data using a specific account. Keep in mind that sending your account password over an unsecured HTTP RPC connection is highly insecure.

<h3>Parameters</h3>

1. `dataToSign` - **String**: Data to sign. If String it will be converted using [:ref:`web3.utils.utf8ToHex <utils-utf8tohex>`](https://github.com/aionnetwork/aion_web3/blob/v1.0/docs/web3-eth-personal.rst#id2).
2. `address` - **String**: Address to sign data with.
3. `password` - **String**: The password of the account to sign data with.
4. `callback` - **Function**: (optional) Optional callback, returns an error object as first parameter and the result as second.

<h3>Returns</h3>

`Promise` returns **String** - The signature.

<h3>Example</h3>

```javascript
web3.eth.personal.sign("Hello world", "0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe", "test password!")
.then(console.log);
> "0x30755ed65396facf86c53e6217c52b4daebe72aa4941d89635409de4c9c7f9466d4e9aaec7977f05e923889b33c0d0dd27d7226b6e6f56ce737465c5cfd04be400"

// the below is the same
web3.eth.personal.sign(web3.utils.utf8ToHex("Hello world"), "0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe", "test password!")
.then(console.log);
> "0x30755ed65396facf86c53e6217c52b4daebe72aa4941d89635409de4c9c7f9466d4e9aaec7977f05e923889b33c0d0dd27d7226b6e6f56ce737465c5cfd04be400"
```

## ecRecover

```javascript
web3.eth.personal.ecRecover(dataThatWasSigned, signature [, callback])
```

Recovers the account that signed the data.

<h3>Parameters</h3>
1. **String** - Data that was signed. If String it will be converted using :ref:`web3.utils.utf8ToHex <utils-utf8tohex>`.
2. **String** - The signature.
3. **Function** - (optional) Optional callback, returns an error object as first parameter and the result as second.

<h3>Returns</h3>
`Promise` returns **String** - The account.

<h3>Example</h3>

```javascript
web3.eth.personal.ecRecover("Hello world", "0x30755ed65396facf86c53e6217c52b4daebe72aa4941d89635409de4c9c7f9466d4e9aaec7977f05e923889b33c0d0dd27d7226b6e6f56ce737465c5cfd04be400").then(console.log);
> "0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe"
```

## signTransaction

```javascript
web3.eth.personal.signTransaction(transaction, password [, callback])
```

Signs a transaction. This account needs to be unlocked. Keep in mind that sending your account password over an unsecured HTTP RPC connection is highly insecure.

<h3>Parameters</h3>

1. **Object** - The transaction data to sign.
2. **String** - The password of the account, to sign the transaction with.
3. **Function** - (optional) Optional callback, returns an error object as the first parameter and the result as second.

<h3>Returns</h3>

Promise returns Object - The RLP encoded transaction. The raw property can be used to send the transaction using `web3.eth.sendSignedTransaction`.

<h3>Example</h3>

```javascript
web3.eth.signTransaction({
    from: "0xEB014f8c8B418Db6b45774c326A0E64C78914dC0",
    gasPrice: "20000000000",
    gas: "21000",
    to: '0x3535353535353535353535353535353535353535',
    value: "1000000000000000000",
    data: ""
}, 'MyPassword!').then(console.log);
> {
    raw: '0xf86c808504a817c800825208943535353535353535353535353535353535353535880de0b6b3a76400008025a04f4c17305743700648bc4f6cd3038ec6f6af0df73e31757007b7f59df7bee88da07e1941b264348e80c78c4027afc65a87b0a5e43e86742b8ca0823584c6788fd0',
    tx: {
        nonce: '0x0',
        gasPrice: '0x4a817c800',
        gas: '0x5208',
        to: '0x3535353535353535353535353535353535353535',
        value: '0xde0b6b3a7640000',
        input: '0x',
        v: '0x25',
        r: '0x4f4c17305743700648bc4f6cd3038ec6f6af0df73e31757007b7f59df7bee88d',
        s: '0x7e1941b264348e80c78c4027afc65a87b0a5e43e86742b8ca0823584c6788fd0',
        hash: '0xda3be87732110de6c1354c83770aae630ede9ac308d9f7b399ecfba23d923384'
    }
}
```

## unlockAccount

```javascript
web3.eth.personal.unlockAccount(address, password, unlockDuraction [, callback])
```

Signs data using a specific account. Keep in mind that sending your account password over an unsecured HTTP RPC connection is highly insecure.

<h3>Parameters</h3>

1. `address` - **String**: The account address.
2. `password` - **String** - The password of the account.
3. `unlockDuration` - `Number` - The duration for the account to remain unlocked.

<h3>Example</h3>

```javascript
web3.eth.personal.unlockAccount("0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe", "test password!", 600)
.then(console.log('Account unlocked!'));
> "Account unlocked!"
```

<h1>Need Help?</h1>

If you get stuck, head over to our [Gitter channels](https://gitter.im/aionnetwork/Lobby) or [StackOverflow](https://stackoverflow.com/search?q=aion) for answers to some common questions.