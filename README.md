# ethereum-hdwallet

> Ethereum HD Wallet derivations from mnemonic

## Install

```bash
npm install ethereum-hdwallet
```

## Getting Started

```js
const HDWallet = require('ethereum-hdwallet')

const mnemonic = 'tag volcano eight thank tide danger coast health above argue embrace heavy'
const hdwallet = new HDWallet(mnemonic)
console.log(hdwallet.hdpath()) // m/44'/60'/0'/0/
```

Deriving wallets given account index:

```js
const hdwallet = new HDWallet(mnemonic)

console.log('0x' + hdwallet.derive(0).getAddress().toString('hex')) // 0xc49926c4124cee1cba0ea94ea31a6c12318df947
console.log(hdwallet.derive(0).getPrivateKey().toString('hex')) // 63e21d10fd50155dbba0e7d3f7431a400b84b4c2ac1ee38872f82448fe3ecfb9

console.log('0x' + hdwallet.derive(1).getAddress().toString('hex')) // 0x8230645ac28a4edd1b0b53e7cd8019744e9dd559
console.log('0x' + hdwallet.derive(2).getAddress().toString('hex')) // 0x65c150b7ef3b1adbb9cb2b8041c892b15edde05a
console.log('0x' + hdwallet.derive(2).getAddress().toString('hex')) // 0x1aebbe69459b80d4975259378577bc01d2924cf4
```

Signing transaction:

```js
const signedRawTx = hdwallet.derive(0).signTransaction({
  to: '0x0000000000000000000000000000000000000000',
  value: '0x0',
  data: '0x0'
})

console.log(signedTx.toString('hex')) // 0xf85d80808094000000000000000000000000000000000000000080001ca0de4b34f17bf51d0b783082090c10d133dcc867c7e981c07cda5ddd1e3211f44ca02125dff6879141708899838356bc42df8815220069ce10507ae4ea980791dac4
```

The default HD path is `m/44'/60'/0'/0/` but you may pass a custom path to the constructor:

```js
const hdwallet = new HDWallet(mnemonic, hdpath)
console.log(hdwallet.hdpath()) // m/44'/100'/0'/0/
```

## CLI

### Install

```bash
npm install ethereum-hdwallet -g
```

### Usage

```bash
$ ethereum_hdwallet --help

  Usage
$ ethereum_hdwallet [options]

  Options
    -i, --index Account Index (e.g. 4)
    -p, --property Property to display (e.g. address, publickey, privatekey, hdpath)
    -r, --range Account Index Range (e.g 1-100)
    -m, --mnemonic Mnemonic

  Examples
    $ ethereum_hdwallet -m "tag volcano eight thank tide danger coast health ab
ove argue embrace heavy" -r 0-10
```

### Examples

Display the address at a particular account index:

```bash
$ ethereum_hdwallet -m "tag volcano eight thank tide danger coast health above argue embrace heavy" -i 4
╔═══════════════╤════════════════════════════════════════════╗
║ account index │ address                                    ║
╟───────────────┼────────────────────────────────────────────╢
║ 4             │ 0x32f48bf54dbbfce73172e69fe563c130d536cd5f ║
╚═══════════════╧════════════════════════════════════════════╝
```

Display the account address derived from a range of account indexes:

```bash
$ ethereum_hdwallet -m "tag volcano eight thank tide danger coast health above argue embrace heavy" -r 5-10
╔═══════════════╤════════════════════════════════════════════╗
║ account index │ address                                    ║
╟───────────────┼────────────────────────────────────────────╢
║ 5             │ 0x1c255db352e8b3cc16efd721c61d7b1b5952b2bb ║
╟───────────────┼────────────────────────────────────────────╢
║ 6             │ 0x1a41029aeb54a8c09211539b92b2a3fd92ea8270 ║
╟───────────────┼────────────────────────────────────────────╢
║ 7             │ 0x54c0897a1e281b107eee25d4f8eee5f6ae13f9d9 ║
╟───────────────┼────────────────────────────────────────────╢
║ 8             │ 0x3d503e7c3799ab9478b6c04623275fdc0ad09b1e ║
╟───────────────┼────────────────────────────────────────────╢
║ 9             │ 0x2d69b45301b9b3e01c4797c7a48bbc7e7f9b355b ║
╟───────────────┼────────────────────────────────────────────╢
║ 10            │ 0x5e611cbdd26f78a4c837759378a7b41caa17b41b ║
╚═══════════════╧════════════════════════════════════════════╝
```

Display the private key of the account:

```bash
$ ethereum_hdwallet -m "tag volcano eight thank tide danger coast health above argue embrace heavy" -i 3 -p privatekey
╔═══════════════╤══════════════════════════════════════════════════════════════════╗
║ account index │ private key                                                      ║
╟───────────────┼──────────────────────────────────────────────────────────────────╢
║ 3             │ f466f6f4d2d61a11eddd10eb80aae500c7601539d08d1d55f9e5efe25ecf95bc ║
╚═══════════════╧══════════════════════════════════════════════════════════════════╝
```

Display the HD path of the account:

```bash
$ bin/ethereum_hdwallet -m "tag volcano eight thank tide danger coast health above argue embrace heavy" -i 3 -p hdpath
╔═══════════════╤══════════════════╗
║ account index │ hd path          ║
╟───────────────┼──────────────────╢
║ 3             │ m/44'/60'/0'/0/3 ║
╚═══════════════╧══════════════════╝
```

## Test

```bash
npm test
```

## License

MIT
