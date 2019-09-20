# API Reference

## Torus

    `Class`

This is the main class of anything related to Torus

```javascript
const Torus = require("@toruslabs/torus-embed");
```

Using ES6,

```javascript
import Torus from "@toruslabs/torus-embed";
```

## torus object

    `instance`

All API's can be accessed by creating a new instance of Torus

```javascript
const torus = new Torus(options);
```

The Torus constructor takes an object with `TorusCtorArgs` as input

**Parameters**

* `options` - `TorusCtorArgs` \(optional\) : The options of the constructor
  * `buttonPosition` - `enum` \(optional\) : The position of the Torus button. Supported values are `top-left` `bottom-left` `top-right` `bottom-right`

**Returns**

* `Object`: The torus instance with all its methods and events.

**Reference**

```typescript
interface TorusCtorArgs {
  buttonPosition?: 'top-left' | 'top-right' | 'bottom-right' | 'bottom-left'
}
```

**Examples**

```javascript
const torus = new Torus();
```

```javascript
const torus = new Torus({
  buttonPosition: 'top-left' // default: 'bottom-left'
});
```

## init

Initialize the torus object after creation

```javascript
await torus.init(params)
```

**Parameters**

* `params` - `TorusParams` \(optional\) : The parameters passed to initialize torus object
  * `network` - `NetworkInterface` \(optional\) : The network options. Used for setting a default network
  * `buildEnv` - `enum` \(optional\): The build environment to use. Supported values are `production` `development` `staging` `testing`
  * `enableLogging` - `boolean` \(optional\) : Enables/disables logging. Useful for debugging
  * `showTorusButton` - `boolean` \(optional\) : Shows/Hides the Torus Button

**Returns**

* `Promise<void>` : Returns a promise which resolves to void

**Reference**

```typescript
interface TorusParams {
  network?: NetworkInterface;
  buildEnv?: 'production' | 'development' | 'staging' | 'testing';
  enableLogging?: boolean;
  showTorusButton?: boolean;
}

interface NetworkInterface {
  host: 'mainnet' | 'rinkeby' | 'ropsten' | 'kovan' | 'goerli' | 'localhost' | 'matic' | string,
  chainId?: number; 
  networkName?: string;
}
```

**Examples**

```javascript
await torus.init();
```

```javascript
await torus.init({
  network: {
    host: 'rinkeby', // default : 'mainnet'
  }
});
```

```javascript
await torus.init({
  buildEnv: 'staging', // uses staging.tor.us
  enableLogging: false, // default : false
  network: {
    host: 'kovan', // default : 'mainnet'
  },
  showTorusButton: false // default: true
});
```

```javascript
await torus.init({
  buildEnv: 'production', // default: production
  enableLogging: true, // default : false
  network: {
    host: 'https://ethboston1.skalenodes.com:10062', // mandatory
    chainId: 1, // optional
    networkName: 'Skale Network' // optional
  },
  showTorusButton: true // default: true
});
```

## getPublicAddress

This resolves an email address to an Ethereum public Address. Returns an account if it already exists on torus network. Creates, if otherwise

```javascript
const publicAddress = await torus.getPublicAddress(email);
```

**Parameters**

* `email` - `string` : Google account of user e.g. "hello@tor.us"

**Returns**

* `Promise<string>` : Returns a promise which resolves to the Ethereum address associated with the email

**Examples**

```javascript
const publicAddress = await torus.getPublicAddress('random@gmail.com')
```

## setProvider

This changes the network provider to a specified provider. Opens a popup for user's consent

```javascript
await torus.setProvider(params);
```

**Parameters**

* `params` - `NetworkInterface` : The network options. Used to specify a network provider
  * `host` - `string` : The hostname or the `HTTPS` `JSON-RPC` endpoint. Supported options for hostname are  `mainnet` `rinkeby` `ropsten` `kovan` `goerli` `localhost` `matic`
  * `chainId` - `number` \(optional\) : ChainId of the network 
  * `networkName` - `string` \(optional\) : Name of the network

**Returns**

* `Promise<void>` : Returns a promise which resolves to void

**Reference**

```typescript
interface NetworkInterface {
  host: 'mainnet' | 'rinkeby' | 'ropsten' | 'kovan' | 'goerli' | 'localhost' | 'matic' | string,
  chainId?: number; 
  networkName?: string;
}
```

**Examples**

```javascript
await torus.setProvider({
  host: 'rinkeby', // default : 'mainnet'
});
```

```javascript
await torus.setProvider({
  host: 'https://ethboston1.skalenodes.com:10062', // mandatory
  chainId: 1, // optional
  networkName: 'Skale Network' // optional
});
```

## login

Prompts the user to login. Opens the login popup

```javascript
await torus.login();
```

**Returns**

* `Promise<string[]>` : Returns a promise which resolves to the Ethereum Addresses associated with the user

**Examples**

```javascript
await torus.login();
```

## getUserInfo

Returns the logged-in user's google info including name, email, and imageUrl. Please make sure the user is logged in before calling this method. In every `session`, only the first call opens the popup for the user's consent. All subsequent requests don't open the popup

```javascript
const userInfo = await torus.getUserInfo();
```

**Returns**

* `Promise<UserInfo>` : Returns a promise which resolves to `UserInfo` object

**Reference**

```typescript
interface UserInfo {
  email: string;
  name: string;
  profileImage: string;
}
```

**Examples**

```javascript
const userInfo = await torus.getUserInfo();
```

## logout

Logs the user out of torus. Requires that a user is logged in already

```javascript
await torus.logout();
```

**Returns**

* `Promise<void>` : Returns a promise which resolves to void

**Examples**

```javascript
await torus.logout();
```

## cleanUp

This cleans up the iframe and buttons created by torus package. If the user is logged in, it logs him out first and then cleans up

```javascript
await torus.cleanUp();
```

**Returns**

* `Promise<void>` : Returns a promise which resolves to void

**Examples**

```javascript
await torus.cleanUp();
```

## showWallet

Pops up the Torus Wallet app for the user to view. This method is synchronous

```javascript
torus.showWallet(path);
```

**Parameters**

* `path` - `enum` : The route of torus website to open in the popup. Supported options are `transfer` `topup` `home` `settings` `history`

**Examples**

```javascript
torus.showWallet(); // default: 'home'
```

```javascript
torus.showWallet('transfer'); // default: 'home'
```

## showTorusButton

Shows the Torus Button to the user. This method is synchronous

**Examples**

```javascript
torus.showTorusButton();
```

## hideTorusButton

Hides the Torus default button from the user

**Examples**

```javascript
torus.hideTorusButton();
```

## web3

The associated web3 object. Please refer to web3 [documentation](https://github.com/ethereum/wiki/wiki/JavaScript-API) for more information

## ethereum

The associated ethereum object. Please refer to Metamask documentation [here](https://github.com/MetaMask/metamask-inpage-provider)

**Examples**

```javascript
await torus.ethereum.enable(); // does the same thing as `await torus.login();`
```

## provider

The associated provider object

**Reference**

```typescript
declare class Provider {
  send(payload: JsonRPCRequest, callback: Callback<JsonRPCResponse>): any;
}

interface JsonRPCResponse {
  jsonrpc: string;
  id: number;
  result?: any;
  error?: string;
}

interface JsonRPCRequest {
  jsonrpc: string;
  method: string;
  params: any[];
  id: number;
}

interface Callback<ResultType> {
  (error: Error): void;
  (error: null, val: ResultType): void;
}
```

**Examples**

```javascript
const web3 = new Web3(torus.provider);
```
