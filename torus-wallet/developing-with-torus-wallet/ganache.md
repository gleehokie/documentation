# Developing with Ganache

The Torus website runs on `HTTPS`. The browser security model does not allow an insecure connection to a `HTTP` endpoint over `HTTPS`. Install the following [npm package](https://www.npmjs.com/package/ganache-http-proxy) to proxy your `HTTP` traffic from Ganache through a `HTTPS` endpoint. The npm package redirects the traffic present on `https://localhost:8545` to your Ganache port \(eg. `http://localhost:8546`\)

## Install and run ganache-http-proxy

```bash
npm install -g ganache-http-proxy
ganache-http-proxy
```

## Run Ganache on port 8546

`8546` is the port where Ganache is running locally.

```bash
ganache-cli -p 8546
```

## Connect to the Ganache localhost instance in Torus

![Select localhost:8545 from in the Network selector under the Settings tab within the Torus wallet](../../.gitbook/assets/torus-ganache-localhost.png)

## 4. Accept localhost certificates in your browser

Chrome: Paste the following URL into the address bar.

```text
chrome://flags/#allow-insecure-localhost
```

