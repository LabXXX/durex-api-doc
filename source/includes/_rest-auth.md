# REST Authenticated Endpoints

## Authentication

> Example request

```curl
curl
```

> Example Response

```json
```

### HTTP REQUEST

`POST`

## Wallet Balances

> Example request

```curl
curl -X POST "https://durex/v1/balances?user_id=a"
```

See your balances

### HTTP REQUEST

`POST /v1/auth/r/balances`

> Example Response

```json
[
  [
    UserId, 
    // WALLET_TYPE,
    Asset,  // CURRENCY,
    // BALANCE,
    OpId,
    OpType,
    OpTime
    Change,
    FreezeBalance,  // UNSETTLED_INTEREST,
    AvailableBalance  // BALANCE_AVAILABLE
  ],
  [
    "a",
    "BTC",
    0,
    "deposit",
    1533593957,
    "1.3",
    "0",
    "2.7"
  ],
  ...
]
```

## Withdrawal

> Example request

```curl
curl -X POST "https://durex/v1/auth/w/balances/USD/deposit?user_id=b&amount=1000"
```

> Example Response

```json
[
  WITHDRAWAL_ID
]
```

Allow you to request a withdrawal from one of your wallet.

### HTTP REQUEST

`POST /v1/auth/w/balances/<Asset>/withdraw`

### ARGUMENTS

 Parameter | Type | Required | Description
---------- | ---- | -------- | ------------
 Asset | string | Required | Currency (USD, etc)
 amount | string | Required | Amount to withdraw.

## New Order

> Example request

```curl
curl -X POST "https://durex/v1/auth/w/order/new?type=limit&symbol=BTCUSD&user_id=a&side=1&price=10&amount=10&taker_fee=0&maker_fee=0"

curl -X POST "https://durex/v1/auth/w/order/new?type=market&symbol=BTCUSD&user_id=a&side=1&amount=10&taker_fee=0"
```

> Example Response

```json
[
  OrderId  // ID
]
```

Submit a new Order

### HTTP REQUEST

`POST /v1/auth/w/order/new`

### ARGUMENTS

 Parameter | Type | Required | Description
---------- | ---- | -------- | ------------
 type | string | Required | Either “market” / “limit”
 symbol | string | Required | The name of the symbol (see /symbols).
 side | string | Required | Either “buy” or “sell”.
 price | float | Required | Price to buy or sell at. Must be positive. No need for market orders.
 amount | float | Required | Order size: how much you want to buy or sell
 taker_fee | float | Required | Taker fee rate (0 <= taker_fee <= 1)
 maker_fee | float | Required | Maker fee rate (0 <= taker_fee <= 1)

## Cancel Order

> Example request

```curl
curl https://durex/v1/order/cancel
```

> Example Response

```json
[
  OrderId,  // ID,
  OrderType,  // TYPE,
  CreateTime,  // MTS_CREATE,
  UpdateTime,  // MTS_UPDATE,
  UserId,
  Market,  // SYMBOL,
  Price,  // PRICE,
  Amount,  // AMOUNT,
  // AMOUNT_ORIG,
  // ORDER_STATUS,
  // PRICE_AVG
  TakerFee,
  MakerFee,
  Left,
  Freeze,
  DealStock,
  DealMoney,
  DealFee
]

[
  3,
  "BTCUSD",
  1,
  2,
  "a",
  1533594155,
  1533594155,
  "10",
  "10",
  "0",
  "0",
  "10",
  "10",
  "0",
  "0",
  "0" 
]
```

Cancel an order.

### HTTP REQUEST

`POST /v1/auth/w/order/cancel`

### ARGUMENTS

 Parameter | Type | Required | Description
---------- | ---- | -------- | ------------
 order_id | int64 | Required | The order ID given by /order/new.

## Order Status

> Example request

```curl
curl https://durex/v1/order/status
```

> Example Response

```json
[
  OrderId,  // ID,
  OrderType,  // TYPE,
  CreateTime,  // MTS_CREATE,
  UpdateTime,  // MTS_UPDATE,
  UserId,
  Market,  // SYMBOL,
  Price,  // PRICE,
  Amount,  // AMOUNT,
  // AMOUNT_ORIG,
  // ORDER_STATUS,
  // PRICE_AVG
  TakerFee,
  MakerFee,
  Left,
  Freeze,
  DealStock,
  DealMoney,
  DealFee
]
```

Get the status of an order. Is it active? Was it cancelled? To what extent has it been executed? etc.

### HTTP REQUEST

`POST /v1/auth/r/order/status`

### ARGUMENTS

 Parameter | Type | Required | Description
---------- | ---- | -------- | ------------
 order_id | int64 | Required | The order ID given by /order/new.

## Active Orders

> Example request

```curl
curl https://durex/v1/auth/r/orders/tBTCUSD
```

> Example Response

```json
[
  [
    OrderId,  // ID,
    OrderType,  // TYPE,
    CreateTime,  // MTS_CREATE,
    UpdateTime,  // MTS_UPDATE,
    UserId,
    Market,  // SYMBOL,
    Price,  // PRICE,
    Amount,  // AMOUNT,
    // AMOUNT_ORIG,
    // ORDER_STATUS,
    // PRICE_AVG
    TakerFee,
    MakerFee,
    Left,
    Freeze,
    DealStock,
    DealMoney,
    DealFee
  ],
  ...
]
```

View your active orders.

### HTTP REQUEST

`POST /v1/auth/r/orders/<Symbol>`

### ARGUMENTS

 Parameter | Type | Required | Description
---------- | ---- | -------- | ------------
 Symbol | string | Required | Symbol (tBTCUSD, ...)

## Orders History

> Example request

```curl
curl https://durex/v1/auth/r/orders/tBTCUSD/hist
```

> Example Response

```json
[
  [
    OrderId,  // ID,
    OrderType,  // TYPE,
    CreateTime,  // MTS_CREATE,
    UpdateTime,  // MTS_UPDATE,
    UserId,
    Market,  // SYMBOL,
    Price,  // PRICE,
    Amount,  // AMOUNT,
    // AMOUNT_ORIG,
    // ORDER_STATUS,
    // PRICE_AVG
    TakerFee,
    MakerFee,
    Left,
    Freeze,
    DealStock,
    DealMoney,
    DealFee
  ],
  ...
]
```

Returns the most recent closed or canceled orders up to circa two weeks ago

### HTTP REQUEST

`POST /v1/auth/r/orders/<Symbol>/hist`

### ARGUMENTS

 Parameter | Type | Required | Description
---------- | ---- | -------- | ------------
 Symbol | string | Required | Symbol (tBTCUSD, ...)
 start | string | Optional | Millisecond start time
 end | string | Optional | Millisecond end time
 limit | int32 | Optional | Number of records

## Past Trades

> Example request

```curl
curl https://durex/v1/auth/r/trades/tBTCUSD/hist
```

> Example Response

```json
[
  [
    ID,
    PAIR,
    MTS_CREATE,
    ORDER_ID,
    EXEC_AMOUNT,
    EXEC_PRICE,
    ORDER_TYPE,
    ORDER_PRICE,
    MAKER,
    FEE,
    FEE_CURRENCY
  ],
  ...
]
```

View your past trades.

### HTTP REQUEST

`POST /v1/auth/r/trades/<Symbol>/hist`

### ARGUMENTS

 Parameter | Type | Required | Description
---------- | ---- | -------- | ------------
 Symbol | string | Required | Symbol (tBTCUSD, ...)
 start | string | Optional | Millisecond start time
 end | string | Optional | Millisecond end time
 limit | int32 | Optional | Number of records
