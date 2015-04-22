shapeshift.io
=============

A JavaScript component for the crypto currency buying and selling shapeshift.io service. API
documentation here: https://shapeshift.io/api.html


Usage
-----

### Installation

    npm i --save shapeshift.io


### Methods

- [coins()](#coins)
- [depositLimit()](#depositLimit)
- [depositStatus()](#depositStatus)
- [exchangeRate()](#exchangeRate)
- [recent()](#recent)


#### coins()

Get a map of supported coins.

Reference: https://shapeshift.io/api.html#getcoins

**Example:**

```js
var shapeshift = require('shapeshift.io')

shapeshift.coins(function (err, coinData) {
  console.dir(coinData) // =>
  /*
    { BTC:
     { name: 'Bitcoin',
       symbol: 'BTC',
       image: 'https://shapeshift.io/images/coins/bitcoin.png',
       status: 'available' },

       ...

    VRC:
     { name: 'Vericoin',
       symbol: 'VRC',
       image: 'https://shapeshift.io/images/coins/vericoin.png',
       status: 'available' } }
  */
})
```


#### depositLimit()

Get the deposit limit before you purchase.

Reference: https://shapeshift.io/api.html#deposit-limit

**Example:**

```js
var shapeshift = require('shapeshift.io')

var pair = 'btc_ltc'
shapeshift.depositLimit(pair, function (err, limit) {
  console.dir(limit) // => '4.41101872'
})
```


### depositStatus()

Get the status of most recent deposit transaction to the address.

Reference: https://shapeshift.io/api.html#status-deposit

**Example:**

```js
var shapeshift = require('shapeshift.io')

var address = '1LMd3fBqUqZScPSKkjGscwji4EZecCuS48'
shapeshift.depositStatus(address, function (err, status, data) {
  console.dir(data) // =>

  /*
    {
      status : "complete",
      address: <address>,
      withdraw: <withdrawal address>,
      incomingCoin: <amount deposited>,
      incomingType: <coin type of deposit>,
      outgoingCoin: <amount sent to withdrawal address>,
      outgoingType: <coin type of withdrawal>,
      transaction: <transaction id of coin sent to withdrawal address>
    }
  */
})
```


#### exchangeRate()

Get the exchange rate. Note, the `rate` is returned as a type of
`string`; this is to ensure precision matches the API exactly.

Reference: https://shapeshift.io/api.html#rate

**Example:**

```js
var shapeshift = require('shapeshift.io')

var pair = 'btc_ltc'
shapeshift.exchangeRate(pair, function (err, rate) {
  console.dir(rate) // => '158.71815287'
})
```


#### recent()

Get a list of recent transactions / purchases.

Reference: https://shapeshift.io/api.html#recent-list

**Example:**

```js
var shapeshift = require('shapeshift.io')

shapeshift.recent(function (err, recent) {
  console.dir(recent) // =>

  /*
  [ { curIn: 'DOGE',
      curOut: 'BTC',
      timestamp: Tue Apr 14 2015 00:29:50 GMT-0500 (CDT),
      amount: 417 },
    { curIn: 'DOGE',
      curOut: 'BTC',
      timestamp: Tue Apr 14 2015 00:26:57 GMT-0500 (CDT),
      amount: 417 },
    ...
  */
})
```



### Intercept HTTP

You can intercept/modify http methods. This may be useful if you want to use an alternative http
library.


#### http.get

**Example:**

```js
var shapeshift = require('shapeshift.io')

var oldGet = shapeshift.http.get
shapeshift.http.get = function (url, callback) {
  // log urls?
  // use another http library?
}
```


### CORS

ShapeShift supports CORS so that you can do cross-domain requests in the browser. See
https://shapeshift.io/api.html#cors for more details.

**Example:**

```js
var shapeshift = require('shapeshift.io')
shapeshift.cors = true
```


License
-------

MIT





