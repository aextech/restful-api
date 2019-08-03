AEX RESTful API Protocol Documentation (V2)
---

**Currently V2 version only provides public data access, and does not provide user data access.**

# Table Of Contents
+ [Public Data Access](#request--response)
  + [Get all market pair information](#get-all-market-pair-information)
  + [Get specified market pair information](#get-specified-market-pair-information)
  + [Get ticker data of specified market pair](#get-ticker-data-of-specified-market-pair)
  + [Get depth of specified market pair](#get-depth-of-specified-market-pair)
  + [Get latest trade data of specified market pair](#get-the-latest-transaction-data-for-the-specified-transaction)
  + [Get historical trade data of specified market pair](#get-historical-trade-data-of-specified-market-pair)
+ User Data Access (not yet implemented)

# Error Code
Error code | Description
----- | ---------
0 | normal
1001 | System error
4001 | Invalid request
5001 | Not certified
6001 | Verified
7001 | System busy
8001 | The currency does not exist
9001 | Trading currency does not exist
10001 | Invalid trading area
11001 | The currency is not traded in the current trading zone

# Request / Response
## Get all market pair information
  Request URL
  ```
  GET /v2/allpair.php
  ```
  Request parameters: none
  
  Response (json)
  ```
  {
    "eno": 0, // error code
    "emsg":"", // error description
    "data":[
      {
        "market":"usdt", // market  
        "coin": "btc", // currency name
        "limits":{
          "PricePrecision": 0, // pending order price accuracy
          "AmtPrecision": 6, // the number of pending orders
          "AmtMax": "10000000.00000000", // the maximum number of pending orders
          "AmtMin": "0.00000100", // minimum number of pending orders
          "PriceMax": "1000000.00000000", // maximum pending order price
          "MoneyMin": "1.00000000" // Minimum pending order <= Pending order price* Pending order quantity
        }
      }
    ]
  }
  ```
## Get specified market pair information

  Request URL
  ```
  GET /v2/pair.php?market={market}&coin={coin}
  ```
  Request parameters:

  Parameter name | Description
  ----- | ---------
  Market | trading area, such as cnc
  Coin | currency name, such as btc


  Response (json)
  ```
  {
    "eno": 0, // error code
    "emsg":"", // error description
    "data":[
      {
        "market":"usdt", // market
        "coin": "btc", // currency name
        "limits":{
          "PricePrecision": 0, // pending order price accuracy
          "AmtPrecision": 6, // the number of pending orders
          "AmtMax": "10000000.00000000", // the maximum number of pending orders
          "AmtMin": "0.00000100", // minimum number of pending orders
          "PriceMax": "1000000.00000000", // maximum pending order price
          "MoneyMin": "1.00000000" // Minimum pending order <= Pending order price* Pending order quantity
        }
      }
    ]
  }
  ```
## Get ticker data of specified market pair

  Request URL
  ```
  GET /v2/tickers.php?market={market}&coin={coin}
  ```
  Request parameters:

  Parameter name | Description
  ----- | ---------
  Market | trading area, such as cnc
  Coin | currency name, such as btc


  Response (json)
  ```
  {
    "eno": 0, // error code
    "emsg":"", // error description
    "data":[
      {
        "market":"cnc", // market
        "coin": "btc", // currency name
        "ticker":{
          "high": 75501, // the highest price within 24 hours
          "low": 72231, // lowest price within 24 hours
          "last":74654, // Last 1 transaction price
          "vol":6448.69997, // 24 hour volume
          "buy":74666, // currently buy 1 price
          "sell":74728, // currently sells 1 price
          "range":0.0257 // The latest transaction price and the fluctuation ratio of the transaction price before 24 hours
        }
      }
    ]
  }
  ```
## Get depth of specified market pair

  Request URL
  ```
  GET /v2/depth.php?market={market}&coin={coin}
  ```
  Request parameters:

  Parameter name | Description
  ----- | ---------
  Market | trading area, such as cnc
  Coin | currency name, such as btc


  Response (json)
  ```
  {
    "eno": 0, // error code
    "emsg":"", // error description
    "data":{
      "bids":[
        [
          74665, // purchase price
          0.13298 // Buy
        ]
      ],
      "asks":[
        [
          74734, // Selling price
          1.198882 // Selling
        ]
      ]
    }
  }
  ```
## Get the latest transaction data for the specified transaction

  Request URL
  ```
  GET /v2/lasttrades.php?market={market}&coin={coin}&limit={limit}
  ```
  Request parameters:

  Parameter name | Description
  ----- | ---------
  Market | trading area, such as cnc
  Coin | currency name, such as btc
  Limit | number of queries, optional, default is 10, maximum is 50


  Response (json)
  ```
  {
    "eno": 0, // error code
    "emsg":"", // error description
    "data":[
      {
        "tradeid": 3428804, // deal ID
        "time": 1563413853, // transaction time, in seconds
        "type":"buy", // transaction type: buy=buy, sell=sell
        "price": 40200, // transaction price
        "amount":0.004975 // Number of deals
      }
    ]
  }
  ```
## Get historical trade data of specified market pair

  Request URL
  ```
  GET /v2/trades.php?market={market}&coin={coin}&fromid={fromTradeID}&limit={limit}
  ```
  Request parameters:

  Parameter name | Description
  ----- | ---------
  Market | trading area, such as cnc
  Coin | currency name, such as btc
  Fromid | From which transaction ID to start the query, the result contains this transaction ID
  Limit | number of queries, optional, default is 10, maximum is 50


  Response (json)
  ```
  {
    "eno": 0, // error code
    "emsg":"", // error description
    "data":[
      {
        "tradeid": 3428804, // deal ID
        "time": 1563413853, // transaction time, in seconds
        "type":"buy", // transaction type: buy=buy, sell=sell
        "price": 40200, // transaction price
        "amount":0.004975 // Number of deals
      }
    ]
  }
  ```
