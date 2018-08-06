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
curl https://durex/v1/balances
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
    //BALANCE,
    OpId,
    OpType,
    OpTime
    Change,
    FreezeBalance, // UNSETTLED_INTEREST,
    AvailableBalance  // BALANCE_AVAILABLE
  ],
  ...
]
```

## Withdrawal

> Example request

```curl
curl https://durex/v1/withdraw
```

> Example Response

```json
[
  WITHDRAWAL_ID
]
```

Allow you to request a withdrawal from one of your wallet.

### HTTP REQUEST

`POST /v1/auth/w/withdraw`

### ARGUMENTS

 Parameter | Type | Required | Description
---------- | ---- | -------- | ------------
 amount | string | Required | Amount to withdraw.
 address | string | Required | Destination address for withdrawal.

## New Order

> Example request

```curl
curl https://durex/v1/order/new
```

> Example Response

```json
[
  OrderId,  // ID,
  OrderType,  // TYPE,
  CreateTime, // MTS_CREATE,
  UpdateTime, // MTS_UPDATE,
  UserId,
  Market, // SYMBOL,
  Price, // PRICE,
  Amount, // AMOUNT,
  // AMOUNT_ORIG,
  // ORDER_STATUS,
  //PRICE_AVG
  TakerFee,
  MakerFee,
  Left,
  Freeze,
  DealStock,
  DealMoney,
  DealFee
]
```

Submit a new Order

### HTTP REQUEST

`POST /v1/auth/w/order/new`

### ARGUMENTS

 Parameter | Type | Required | Description
---------- | ---- | -------- | ------------
 symbol | string | Required | The name of the symbol (see /symbols).
 amount | float | Required | Order size: how much you want to buy or sell
 price | float | Required | Price to buy or sell at. Must be positive. Use random number for market orders.
 side | string | Required | Either “buy” or “sell”.
 type | string | Required | Either “market” / “limit”

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
  CreateTime, // MTS_CREATE,
  UpdateTime, // MTS_UPDATE,
  UserId,
  Market, // SYMBOL,
  Price, // PRICE,
  Amount, // AMOUNT,
  // AMOUNT_ORIG,
  // ORDER_STATUS,
  //PRICE_AVG
  TakerFee,
  MakerFee,
  Left,
  Freeze,
  DealStock,
  DealMoney,
  DealFee
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
  CreateTime, // MTS_CREATE,
  UpdateTime, // MTS_UPDATE,
  UserId,
  Market, // SYMBOL,
  Price, // PRICE,
  Amount, // AMOUNT,
  // AMOUNT_ORIG,
  // ORDER_STATUS,
  //PRICE_AVG
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
    CreateTime, // MTS_CREATE,
    UpdateTime, // MTS_UPDATE,
    UserId,
    Market, // SYMBOL,
    Price, // PRICE,
    Amount, // AMOUNT,
    // AMOUNT_ORIG,
    // ORDER_STATUS,
    //PRICE_AVG
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
    CreateTime, // MTS_CREATE,
    UpdateTime, // MTS_UPDATE,
    UserId,
    Market, // SYMBOL,
    Price, // PRICE,
    Amount, // AMOUNT,
    // AMOUNT_ORIG,
    // ORDER_STATUS,
    //PRICE_AVG
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
