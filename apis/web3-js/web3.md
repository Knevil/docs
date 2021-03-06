# Web3

Class

This is the main class of anything related Aion.

```javascript
var Web3 = require('web3');

> Web3.utils
> Web3.version
> Web3.givenProvider
> Web3.providers
> Web3.modules
```

-----

## Web3.modules

Property of Web3 class

```javascript
Web3.modules
```

Will return an object with the classes of all major sub modules, to be
able to instantiate them manually.

### Returns

  - `Object`: A list of modules:
    
      - `Eth` - **Function**: the Eth module for interacting with the
        Aion network see web3.eth \<eth\> for more.
      - `Net` - **Function**: the Net module for interacting with network
        properties see web3.eth.net \<eth-net\> for more.
      - `Personal` - **Function**: the Personal module for interacting
        with the Aion accounts see web3.eth.personal \<personal\>
        for more.
      - `Shh` - **Function**: the Shh module for interacting with the
        whisper protocol see web3.shh \<shh\> for more.
      - `Bzz` - **Function**: the Bzz module for interacting with the
        swarm network see web3.bzz \<bzz\> for more.

### Example

```javascript
Web3.modules
> {
    Eth: Eth function(provider),
    Net: Net function(provider),
    Personal: Personal function(provider),
    Shh: Shh function(provider),
    Bzz: Bzz function(provider),
}
```

-----

## web3 object

The instance of Web3

The web3.js object is an umbrella package to house all Aion related
modules.

```javascript
var Web3 = require('web3');

// "Web3.providers.givenProvider" will be set if in an Aion supported browser.
var web3 = new Web3(Web3.givenProvider || 'ws://some.local-or-remote.node:8546');

> web3.eth
> web3.shh
> web3.bzz
> web3.utils
> web3.version
```

-----

## version

Property of Web3 class and instance of Web3

```javascript
Web3.version
web3.version
```

Contains the version of the `web3` container object.

### Returns

`String`: The current version.

### Example

```javascript
web3.version;
> "1.0.0"
```

-----

## utils

Property of Web3 class and instance of Web3

```javascript
Web3.utils
web3.utils
```

Utility functions are also exposes on the `Web3` class object directly.

<h1>Need Help?</h1>

If you get stuck, head over to our [Gitter channels](https://gitter.im/aionnetwork/Lobby) or [StackOverflow](https://stackoverflow.com/search?q=aion) for answers to some common questions.