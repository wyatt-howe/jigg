# JIGG
 JavaScript implementation of garbled gates and 2PC boolean circuit  protocols

 ## Installation and Setup

 The entirety of this project is written in JavaScript.  Running the server requires [Node](https://nodejs.org/en/), [npm](https://www.npmjs.com/), and [Socket.IO](https://socket.io/).

 Run `npm` to install all JIGC dependencies inside the `lib/.dep` directory:
 ```shell
 npm install --prefix lib/.dep
 ```

 ## Running the Prototype

 ### As a Server
 Start the server from server.js with the command below and specify a port number such as:
 ```shell
 node server 3000
 ```

 ### As a Party
 Parties can go to `http(s)://localhost:3000/client.html` in a web browser supporting JavaScript to begin communications.  This is a strictly 2-party protocol.
 
 ### Demos
 The current circuit in `base.js` is just a small 4-gate test.  SHA256 coming soon.
 
 ### Circuit Format
 JIGG can evaluate a boolean circuit in either of the following formats:

In JavaScript as a circuit object
```javascript
const circuit = {
  wires: 8, gates: 4,
  input: [1, 2, 3, 4], output: [5, 7, 8],
  gate: [
    {wirein: [1,2], wireout: 5, type: 'and'},
    {wirein: [3,4], wireout: 6, type: 'xor'},
    {wirein: [6], wireout: 7, type: 'not'},
    {wirein: [5,7], wireout: 8, type: 'and'}
  ]
};
```

As a circuit in the standardized '[Bristol](https://homes.esat.kuleuven.be/~nsmart/MPC/) [Format](https://homes.esat.kuleuven.be/~nsmart/MPC/old-circuits.html)' which is supported by several compiled MPC libraries such as SHARE-MAMBA.
```ada
4 8
1 4
1 3
2 1 1 2 5 AND
2 1 3 4 6 XOR
1 1 6 7 INV
2 1 5 7 8 AND
```

## To Do
 - Replace encryption with AES
 - Write point-and-permute
 - Change current oblivious transfer to use RSA
 - a lot of optimizations (free xor, 4-3 row trick, etc.)
 - Complete web UI
