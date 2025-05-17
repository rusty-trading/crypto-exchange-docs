[docs_cdp_coinbase_com_exchange_docs_fix_msg_oe_tpsl.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-tpsl#__docusaurus_skipToContent_fallback)

Take Profit Stop Loss (TPSL) orders are supported in [FIX 4.2](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#new-order-single-d) and [FIX 5.0](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#newordersingle-35d) with New Order Single (35=D) and the [Create a new order](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postorders) REST API.

TPSL orders allow users to set predefined profit and loss levels simultaneously for their position.

When an asset price reaches one of the target prices, the position is closed with a limit order. If one of the orders is triggered, the other order is canceled automatically. An order can only have one TP/SL on one side.

## Parameters [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-tpsl\#parameters "Direct link to Parameters")

These parameters are required for TPSL orders:

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 40 | OrdType | Char | Y | Order Type must be `O` (the letter Oh) |
| 44 | Price | Decimal | Y | Take profit price (in this context)<br>_See Price Rules below._ |
| 99 | StopPx | Decimal | Y | Stop loss trigger price |
| 3040 | StopLimitPx | Decimal | Y | Limit order price if stop loss triggers |



Price Rules

- Sell TPSL: `Price` must be > `StopPx` and `StopPx` must be > `StopLimitPx`
- Buy TPSL: `Price` must be < `StopPx` and `StopPx` must be < `StopLimitPx`

## Caveats [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-tpsl\#caveats "Direct link to Caveats")

- Only GTC and GTD are supported for `TimeInForce`
- Like Stop orders, TPSL orders cannot be modified.
- TPSL orders cannot be submitted during auction mode.
- The Post-Only tag is not supported. It cannot be populated or must be false.
- The Iceberg tag is not supported.
- Batch orders are not supported.



Auction Mode Transition

Existing TPSL orders will be canceled if a product is transitioned to auction mode.

## Samples [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-tpsl\#samples "Direct link to Samples")

### TPSL Sell Order [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-tpsl\#tpsl-sell-order "Direct link to TPSL Sell Order")

This TPSL sell order for BTC-USD places a **_live_** sell limit order at price 9785

`Side=2|Price=9785|StopLimitPx=8245|StopPx=8500`

- If the price falls below 8500 and no part of this limit order has been filled, it will be repriced from 9785 to 8245.
- If this limit order is filled or partially filled at 9785, then it will never be repriced.

This differs from regular stop orders where a stop order is NOT live until the price is traded through the StopPx. The direction of the trigger is determined by the Side of the order and thus, `TriggerPriceDirection` is NOT accepted.

### Message Flow [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-tpsl\#message-flow "Direct link to Message Flow")

> TPSL Order Example

`-> OrdType=O|Side=2|Price=9785|StopLimitPx=8245|StopPx=8500...`

> Execution Report Example

`<- MsgType=8|OrdType=O|Side=2|Price=9785|StopLimitPx=8245|StopPx=8500...`

> Repricing Example

If the stop is triggered and the order is repriced, an ExecutionReport is returned with a RestatementReason of `3` for "Repricing of order":

`<- MsgType=8|OrdType=O|ExecType=D|ExecRestatementReason=3|Price=8245...`

### WebSocket User Channel [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-tpsl\#websocket-user-channel "Direct link to WebSocket User Channel")

If the stop is triggered and the order is repriced, a change message is published, for example:

```codeBlockLines_p187
{
    "new_price": "8245",
    "order_id": "...",
    "type": "change",
    "side": "sell",
    "old_price": "9785",
    "reason": "tpsl_triggered"
}

```

Only the user channel with your TPSL order displays with `tpsl_triggered`. Other clients will receive change reason, `modify_order`.

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Parameters](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-tpsl#parameters)
- [Caveats](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-tpsl#caveats)
- [Samples](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-tpsl#samples)
  - [TPSL Sell Order](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-tpsl#tpsl-sell-order)
  - [Message Flow](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-tpsl#message-flow)
  - [WebSocket User Channel](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-tpsl#websocket-user-channel)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_websocket_overview.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview#__docusaurus_skipToContent_fallback)

The WebSocket feed is publicly available and provides real-time market data updates for orders and trades. Two endpoints are supported in both production and sandbox:

- **Coinbase Market Data** is our traditional feed which is available without authentication.
- **Coinbase Direct Market Data** has direct access to Coinbase Exchange servers and requires [Authentication](https://docs.cdp.coinbase.com/exchange/docs/websocket-auth).



Tip

You can subscribe to both endpoints, but if `ws-direct` is your primary connection, we recommend using `ws-feed` as a failover.



Info

**Coinbase Market Data**

production = wss://ws-feed.exchange.coinbase.com

sandbox = wss://ws-feed-public.sandbox.exchange.coinbase.com

**Coinbase Direct Market Data**

production = wss://ws-direct.exchange.coinbase.com

sandbox = wss://ws-direct.sandbox.exchange.coinbase.com

## Protocol [](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview\#protocol "Direct link to Protocol")

The WebSocket feed uses a bidirectional protocol that encodes all messages as JSON objects. All messages have a `type` attribute that can be used to handle the message appropriately.



Tip

New message types can be added at any time. Clients are expected to ignore messages they do not support.

## Subscribe [](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview\#subscribe "Direct link to Subscribe")

To begin receiving feed messages, you must send a `subscribe` message to the server indicating which channels and products to receive. This message is mandatory—you are disconnected if no `subscribe` has been received within 5 seconds.



Caution

To receive feed messages, you must send a `subscribe` message or you are disconnected in 5 seconds.

```codeBlockLines_p187
// Request
// Subscribe to ETH-USD and ETH-EUR with the level2, heartbeat and ticker channels,
// plus receive the ticker entries for ETH-BTC and ETH-USD
{
  "type": "subscribe",
  "product_ids": ["ETH-USD", "ETH-EUR"],
  "channels": [\
    "level2",\
    "heartbeat",\
    {\
      "name": "ticker",\
      "product_ids": ["ETH-BTC", "ETH-USD"]\
    }\
  ]
}

```

You receive a `subscriptions` message as a response to an `subscribe` message.

### Unsubscribe [](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview\#unsubscribe "Direct link to Unsubscribe")

To unsubscribe from channel/product pairs, send an `unsubscribe` message. The structure is equivalent to `subscribe` messages.



Tip

You can also unsubscribe from a channel entirely by providing no product IDs.

```codeBlockLines_p187
// Request
{
  "type": "unsubscribe",
  "channels": ["heartbeat"]
}

```

You receive a `subscriptions` message as a response to an `unsubscribe` message.

### Specifying Product IDs [](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview\#specifying-product-ids "Direct link to Specifying Product IDs")

There are two ways to specify the product IDs to listen for within each channel:

- You can define product IDs for an individual channel.
- You can define product IDs at the root of the object—this adds them to all the channels you subscribe to.

```codeBlockLines_p187
// Request
{
  "type": "unsubscribe",
  "product_ids": ["ETH-USD", "ETH-EUR"],
  "channels": ["ticker"]
}

```

### Subscriptions Message [](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview\#subscriptions-message "Direct link to Subscriptions Message")

A `subscriptions` message is sent in response to both [subscribe](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview#subscribe) and [unsubscribe](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview#unsubscribe) messages.

In response to a `subscribe` message, the `subscriptions` message lists all channels you are subscribed to. Subsequent subscribe messages add to the list of subscriptions. If you subscribed to a channel without being authenticated, you will remain in the unauthenticated channel.

```codeBlockLines_p187
// Response
{
  "type": "subscriptions",
  "channels": [\
    {\
      "name": "level2",\
      "product_ids": ["ETH-USD", "ETH-EUR"]\
    },\
    {\
      "name": "heartbeat",\
      "product_ids": ["ETH-USD", "ETH-EUR"]\
    },\
    {\
      "name": "ticker",\
      "product_ids": ["ETH-USD", "ETH-EUR", "ETH-BTC"]\
    }\
  ]
}

```

## Websocket Compression Extension [](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview\#websocket-compression-extension "Direct link to Websocket Compression Extension")

Websocket compression, defined in RFC7692, compresses the payload of WebSocket messages which can increase total throughput and potentially reduce message delivery latency. The **permessage-deflate extension** can be enabled by adding the extension header. Currently, it is not possible to specify the compression level.

From [RFC7692](https://datatracker.ietf.org/doc/html/rfc7692#section-7.1.3):

The simplest "Sec-WebSocket-Extensions" header in a client (or server's) opening handshake to offer (or accept) use of the "permessage-deflate" extension looks like this:

```codeBlockLines_p187
    GET wss://ws-feed.exchange.coinbase.com
       Sec-WebSocket-Extensions: permessage-deflate

```

## Sequence Numbers [](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview\#sequence-numbers "Direct link to Sequence Numbers")

Most feed messages contain a sequence number. Sequence numbers are increasing integer values for each product, with each new message being exactly one sequence number greater than the one before it.

Sequence numbers that are _greater than one integer value_ from the previous number indicate that a message has been dropped. Sequence numbers that are _less_ than the previous number can be ignored or represent a message that has arrived out of order.

In either situation you may need to perform logic to make sure your system is in the correct state.



Caution

Even though a WebSocket connection is over TCP, the WebSocket servers receive market data in a manner that can result in dropped messages. Your feed consumer should be designed to handle sequence gaps and out of order messages, or should use channels that guarantee delivery of messages.



Tip

To guarantee that messages are delivered and your order book is in sync, consider using the [level2 channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#level2-channel).

## End-to-end Example [](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview\#end-to-end-example "Direct link to End-to-end Example")

Below is an end-to-end example for Python that handles authentication and connection to the Exchange WebSocket. This code sample can be cloned at [Coinbase Samples](https://github.com/coinbase-samples/exchange-scripts-py/tree/main/websocket).

```codeBlockLines_p187

import asyncio, base64, hashlib, hmac, json, os, time, websockets

API_KEY = str(os.environ.get('API_KEY'))
PASSPHRASE = str(os.environ.get('PASSPHRASE'))
SECRET_KEY = str(os.environ.get('SECRET_KEY'))

URI = 'wss://ws-feed.exchange.coinbase.com'
SIGNATURE_PATH = '/users/self/verify'

channel = 'level2'
product_ids = 'ETH-USD'

async def generate_signature():
    timestamp = str(time.time())
    message = f'{timestamp}GET{SIGNATURE_PATH}'
    hmac_key = base64.b64decode(SECRET_KEY)
    signature = hmac.new(
        hmac_key,
        message.encode('utf-8'),
        digestmod=hashlib.sha256).digest()
    signature_b64 = base64.b64encode(signature).decode().rstrip('\n')
    return signature_b64, timestamp

async def websocket_listener():
    signature_b64, timestamp = await generate_signature()
    subscribe_message = json.dumps({
        'type': 'subscribe',
        'channels': [{'name': channel, 'product_ids': [product_ids]}],
        'signature': signature_b64,
        'key': API_KEY,
        'passphrase': PASSPHRASE,
        'timestamp': timestamp
    })

    while True:
        try:
            async with websockets.connect(URI, ping_interval=None) as websocket:
                await websocket.send(subscribe_message)
                while True:
                    response = await websocket.recv()
                    json_response = json.loads(response)
                    print(json_response)

        except (websockets.exceptions.ConnectionClosedError, websockets.exceptions.ConnectionClosedOK):
            print('Connection closed, retrying..')
            await asyncio.sleep(1)

if __name__ == '__main__':
    try:
        asyncio.run(websocket_listener())
    except KeyboardInterrupt:
        print("Exiting WebSocket..")

```

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Protocol](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview#protocol)
- [Subscribe](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview#subscribe)
  - [Unsubscribe](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview#unsubscribe)
  - [Specifying Product IDs](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview#specifying-product-ids)
  - [Subscriptions Message](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview#subscriptions-message)
- [Websocket Compression Extension](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview#websocket-compression-extension)
- [Sequence Numbers](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview#sequence-numbers)
- [End-to-end Example](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview#end-to-end-example)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_fix_msg_order_entry_50.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#__docusaurus_skipToContent_fallback)

About this API:

- **Baseline**: [FIX 5.0 SP2 specification](https://www.onixs.biz/fix-dictionary/5.0.sp2/index.html).
- **Environments**: Production, Sandbox



Environment URLs

- Production: `tcp+ssl://fix-ord.exchange.coinbase.com:6121 `

- Sandbox: `tcp+ssl://fix-ord.sandbox.exchange.coinbase.com:6121 `



FIX5 Resets Saturdays at 1PM ET

FIX5 Order Entry and Market Data customers will be logged out every Saturday at 1PM ET (6PM UTC).

## Components [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#components "Direct link to Components")

### Standard Header [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#standard-header "Direct link to Standard Header")

Fields that go at the beginning of every message. This exists for all messages sent and received.

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 8 | BeginString | String | Y | Must be set to `FIXT.1.1` and be the first field in the message.<br>(Since FIX version 5.0 this field now represents the session version. The application version gets specified in [Logon](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#logon-35a) message's `DefaultApplVerID (1137)` tag.) |
| 9 | BodyLength | Int | Y | Message length in bytes up to the checksum field (tags after `BodyLength (9)` and before `Checksum (10)`). This must be the second field in message. |
| 35 | MsgType | String | Y | The type of message proceeding the header, must be the third field in the message.<br>**Supported values include:**<br>Admin Messages<br>`A` = Logon<br>`0` = Heartbeat<br>`1` = TestRequest<br>`3` = Reject<br>`5` = Logout<br>Application Messages<br>`D` = NewOrderSingle<br>`F` = OrderCancelRequest<br>`G` = OrderCancelReplaceRequest<br>`H` = OrderStatusRequest<br>`j` = BusinessMessageReject<br>`8` = ExecutionReport<br>`9` = OrderCancelReject<br>`U4` = OrderCancelBatch<br>`U5` = OrderCancelBatchReject<br>`U6` = NewOrderBatch<br>`U7` = NewOrderBatchReject |
| 49 | SenderCompID | String | Y | Client API key (on messages from the client). |
| 56 | TargetCompID | String | Y | Must be `Coinbase` (on messages from client). |
| 34 | MsgSeqNum | Int | Y | Monotonically increasing sequence number of the message. |
| 43 | PossDupFlag | Boolean | C | Indicates that the message was sent in response to a ResendRequest.<br>\- `Y` \- Sent in response to ResendRequest. Should be ignored unless message was not previously processed<br>\- `N` or null - Normal transmission |
| 52 | SendingTime | UTCTimestamp | Y | UTC time that the order was sent down to millisecond resolution in the format `YYYYMMDD-HH:MM:SS.sss` |
| 83 | RptSeq | Int | C | The feed sequence number of the message corresponding to the `RptSeq` in FIX 5.0 Market Data |

### Standard Trailer [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#standard-trailer "Direct link to Standard Trailer")

Fields that go at the end of every message.

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 10 | CheckSum | String | Y | Three byte checksum calculated by summing every byte in the message up to and not including the checksum field itself. This value is then moduloed by `256` and written with prefixed `0` s (if necessary) to meet the 3 byte requirement. |

## Administrative [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#administrative "Direct link to Administrative")

### Logon (35=A) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#logon-35a "Direct link to Logon (35=A)")

First message that is required immediately upon connection to authenticate the connection. `MsgSeqNum` always equals 1 ( `34=1`) on this message in both directions.

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 98 | EncryptMethod | Int | N | Must be `0` (None) |
| 108 | HeartBtInt | Int | O | Must be ≤ `30` (secs). Server sends [Test Request](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#testrequest-351) if client messages are not received in approximately ( `HeartBtInt` x `1.5`) seconds. Server terminates session if client messages are not received in approximately ( `HeartBtInt` x `2`) seconds. Defaults to `10` seconds if not value provided. |
| 141 | ResetSeqNumFlag | Boolean | Y | Resets the sequence number. Defaults to `Y`. <br>Sequence numbers from Customer => Coinbase always get reset after a disconnect.<br>Sequence numbers from Coinbase => Customer are reset after a disconnect if either of these are true: <br>1\. ResetSeqNumFlag not set<br>2\. ResetSeqNumFlag = `Y`<br>3\. Customer was not logged on using same API key more than 1 day. <br>The max possible MsgSeqNum is 2147483647 and customers are responsible for resetting their sessions to avoid breaching this limit. |
| 553 | Username | String | Y | Client API Key. |
| 554 | Password | String | Y | Passphrase for Client API key. |
| 95 | RawDataLength | Int | Y | Number of bytes in `RawData` field. |
| 96 | RawData | String | Y | Client message signature (see [Signing a message](https://docs.cdp.coinbase.com/exchange/docs/rest-auth#signing-a-message)) |
| 1137 | DefaultApplVerID | String | Y | Contains the version of the FIX protocol the exchange uses. Only FIX50SP2 is supported.<br>**Supported values:**<br>`9` = FIX50SP2 |
| 8001 | DefaultSelfTradePreventionStrategy | Char | N | The default SelfTradePreventionStrategy applied to all orders sent on the session unless overridden on a per order basis using the SelfTradeType (7928) in the order request message.<br>The following values specify what to do when two orders submitted by the same portfolio attempt to match:<br>`N` = Cancel aggressing order<br>`Q` = Cancel both orders<br>Default if not specified is Cancel both orders ( `Q`). |
| 8013 | CancelOrdersOnDisconnect | Char | N | `S` = Cancel all session orders on disconnect<br>`Y` = Cancel all profile orders on disconnect **(recommended)** |
| 9406 | DropCopyFlag | Char | N | `N` = Normal order-entry session<br>`Y` = Drop Copy Session that only returns fills (Execution Report - Filled and Execution Report - Partially Filled) |

#### FIX 5.0 Logon Details: [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#fix-50-logon-details "Direct link to FIX 5.0 Logon Details:")

FIX 5.0 is separated into two different layers an application layer and a session layer. The application layer is version 5.0 and the session layer is version T1.1.

- For all LOGON messages use MsgSeqNum 1, set 553 Username to the api key, and only create one session per API Key.
- The begin string will use the session layer version 8=FIXT.1.1
- The application layer version will be specified on the DefaultAppVerID which is tag 1137. This should be set to 9 (This represents version 5.0).
- Sequence numbers must not include leading zeros (e.g., "0001" is invalid, whereas "1" is valid). Using sequence numbers with leading zeros will result in an invalid signature error.
- Fractional seconds must be specified using exactly three digits. For example, 52=20230822-20:43:30.000 is supported, while both 52=20230822-20:43:30 (no fractional seconds) and 52=20230822-20:43:30.123456789 (excessive precision) will result in a signature calculation error.

The Logon message sent by the client must be signed for security. The signing method is shown below. The prehash string is the following fields joined:

`SendingTime, MsgType, MsgSeqNum, SenderCompID (API KEY), TargetCompID, Passphrase`..

There is no trailing separator. The `RawData` field should be a base64 encoding of the HMAC signature.

```codeBlockLines_p187
"""Example Python QuickFIX Application.py logon message setup"""
class Application(fix.Application):
    PASSPHRASE = [ENTER PASSPHRASE]
    API_KEY = [ENTER API_KEY]
    SECRET = [ENTER SECRET]

"""Setup the Logon message & call sign function"""
def toAdmin(self, message, sessionID):
    rawData = self.sign(message.getHeader().getField(52), message.getHeader().getField(35),
                                message.getHeader().getField(34), self.API_KEY, message.getHeader().getField(56),
                                self.PASSPHRASE)
    message.setField(fix.StringField(554, self.PASSPHRASE))
    message.setField(fix.StringField(96, rawData))
    message.setField(fix.StringField(8013, "Y"))
    message.setField(fix.StringField(553, self.API_KEY))
    message.setField(fix.IntField(95, len(rawData.encode('utf-8'))))

"""Create base64 encoded signature"""
def sign(self, timestamp, msg_type, seq_num, api_key, target_comp_id, passphrase):
    message = '\x01'.join([timestamp, msg_type, seq_num, api_key, target_comp_id, passphrase]).encode("utf-8")
    hmac_key = base64.b64decode(self.SECRET)
    signature = hmac.new(hmac_key, message, hashlib.sha256)
    sign_b64 = base64.b64encode(signature.digest()).decode()
    return sign_b64

```



Caution

To establish multiple FIX connections, a unique API key must be generated for each connection. A maximum of 75 connections is allowed per profile. Reusing a single API key for simultaneous connections will result in an error.

#### FIX 5.0 How to resume a session: [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#fix-50-how-to-resume-a-session "Direct link to FIX 5.0 How to resume a session:")

To do a full resume of all data from the last session:

After session disconnect:

- Client LOGON with MsgSeqNum 1 and 141 (ResetSeqNumFlag) = N
- Server responds with a LOGON with MsgSeqNum 1 followed by a Sequence Reset with 36 (NewSeqNo) that the server sends just to communicate the last seqnum from the last session
- Client sends a Resend Request as MsgSeqNum 2 asking for 7 (BeginSeqNo) = 2 and 16 (EndSeqNo) = NewSeqNo from above OR
- If NewSeqNo > 1000 ask for 7 (BeginSeqNo) = 2 and 16 (EndSeqNo) = 1000 with an intent to page all of the Sequence Numbers in blocks of 1000.
  - so the next block would be 7 (BeginSeqNo) = 1001 to 16 (EndSeqNo) = 1999 or NewSeqNo if less than 2000
- We don't replay admin messages or messages older than 1 hour so for any gaps we send a Sequence Reset
- Wait for completed resend before requesting the next page

### Heartbeat (35=0) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#heartbeat-350 "Direct link to Heartbeat (35=0)")

Sent at a prearranged interval from both sides to indicate liveness of the connections and used in response to a [TestRequest](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#testrequest-351) message (35=1).

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 112 | TestReqID | String | C | Conditionally required when the heartbeat message is sent in response to a [TestRequest](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#testrequest-351) (35=1) message. |

### TestRequest (35=1) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#testrequest-351 "Direct link to TestRequest (35=1)")

This message forces the other side of the connection to send a [Heartbeat](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#heartbeat-350) message (35=0) with the `TestReqID` (tag 112) populated with the same value provided on this message.

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 112 | TestReqID | String | Y | A unique identifier used to track the response to a test request. |

### ResendRequest (35=2) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#resendrequest-352 "Direct link to ResendRequest (35=2)")

Sent by the customer to Coinbase to request the retransmission of a range of messages on a given FIX session.

The Coinbase FIX gateway keeps a 4 hour history of messages sent to customers:

- Administrative messages are always replaced by [SequenceReset-GapFill](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#sequencereset-354) messages during retransmission.
- Older non-administrative messages are also replaced by SequenceReset-GapFill messages.
- Retransmitted messages, including SequenceReset-GapFill messages, have PossDupFlag enabled ( `43=Y`) in the header.



Info

The maximum allowed range per request is 1000 messages and only 1 ResendRequest can be processed at a time per session.

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 7 | BeginSeqNo | Int | Y | Sequence number of first message in range to be resent. Must be >= 1 |
| 16 | EndSeqNo | Int | Y | Sequence number of last message in range to be resent. Must be >= 1 and >= BeginSeqNo |

### SequenceReset (35=4) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#sequencereset-354 "Direct link to SequenceReset (35=4)")

Used to skip messages during retransmission. Coinbase only supports "GapFill" mode where GapFillFlag is always true.

Coinbase sends SequenceReset-GapFill messages to customers with or without PossDupFlag (43) in the header:

- Without PossDupFlag: Coinbase sends immediately after logon to reset the Coinbase sequence number to the next outbound sequence number stored for the session.
- With PossDupFlag=Y: Coinbase sends in response to a [ResendRequest](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#resendrequest-352) for all administrative messages, irrespective of time sent, as well as non-administrative messages older than 4 hours.

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 123 | GapFillFlag | Boolean | Y | Always true ( `123=Y`) |
| 36 | NewSeqNo | Int | Y | Must be > 1 |

### Reject (35=3) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#reject-353 "Direct link to Reject (35=3)")

A session level reject message sent when the FIX session can't process a message.

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 45 | RefSeqNum | Int | Y | The `MsgSeqNum` of the referenced message that was rejected. |
| 371 | RefTagID | Int | N | The tag number of the FIX field referenced in the reject. |
| 372 | RegMsgType | String | N | The `MsgType` of the FIX message referenced in the reject. |
| 373 | SessionRejectReason | Int | N | A code to quickly identify common reasons for a reject.<br>**Supported values:**<br>`0` = Invalid Tag Number<br>`1` = Required Tag Missing<br>`2` = Tag not defined for this message type<br>`3` = Undefined tag<br>`4` = Tag specified without a value<br>`5` = Value is incorrect (out of range) for this tag<br>`6` = Incorrect data format for value<br>`8` = Signature problem<br>`9` = `CompID` problem<br>`10` = `SendingTime` Accuracy Problem<br>`11` = Invalid `MsgType`<br>`13` = Tag appears more than once<br>`14` = Tag specified out of required order<br>`15` = Repeating group fields out of order<br>`16` = Incorrect `NumInGroup` count for repeating group<br>`17` = Non "Data" value includes field delimiter (<SOH> character)<br>`18` = Invalid/Unsupported Application Version<br>`99` = Other |
| 58 | Text | String | N | A message explaining why the message was rejected. |

### Logout (35=5) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#logout-355 "Direct link to Logout (35=5)")

Sent by either side to initiate session termination. The side which receives this message first should reply with the same message type to confirm session termination.

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 58 | Text | String | N | Description of the disconnection reason. |

## Trading [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#trading "Direct link to Trading")

### NewOrderSingle (35=D) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#newordersingle-35d "Direct link to NewOrderSingle (35=D)")

Used to submit a new spot order to the Exchange matching engine.



Info

For more information on specific order variants see [Iceberg Orders](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-iceberg), [TPSL Orders](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-tpsl), and [Limit With Funds Orders](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-lwf).

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 11 | ClOrdID | UUID | Y | An identifier specified by the sender to uniquely identify other messages correlating to this request. It must be a variant 1 UUIDv4 that follows the standard format. This means all lowercase and hyphens that group the characters in sequences of 8, 4, 4, 4, 12 (e.g. `1985ca2d-61ef-49f1-bfce-6c39d8462914`). Failure to follow this formatting will result in a reject. <br>This shouldn't match the ClOrdID of any open orders. |
| 18 | ExecInst | Char | N | The execution instruction flags for the order.<br>**Supported values:**<br>`A` = Add Liquidity Only (Post Only) |
| 38 | OrderQty | Decimal | C | The amount of the base asset to be transacted. Required except unless `CashOrderQty` is specified. |
| 1138 | DisplayQty | Decimal | C | Maximum size within an order to be displayed. Must be > 10% of OrderQty |
| 152 | CashOrderQty | Decimal | C | Order size in quote units (e.g., USD) (Market or [Limit order](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-lwf) only). |
| 40 | OrdType | Char | Y | The type of order for the request which can be.<br>**Supported values:**<br>`1` = Market<br>`2` = Limit<br>`4` = Stop Limit<br>`O` = [Take Profit Stop Loss](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-tpsl) |
| 44 | Price | Decimal | C | The limit price for limit orders of the quote asset. The decimal precision must fall within the requirements for each market, see the REST API for precision and decimal limits. |
| 54 | Side | Char | Y | Side of the order.<br>**Supported values:**<br>`1` = Buy<br>`2` = Sell |
| 55 | Symbol | String | Y | Symbol of the instrument being traded (e.g. `BTC-USDC`) |
| 59 | TimeInForce | Char | Y | Specifies how long the order remains in effect.<br>**Supported values:**<br>`1` = Good Till Cancel (GTC)<br>`3` = Immediate Or Cancel (IOC)<br>`4` = Fill Or Kill (FOK)<br>`6` = Good Till Date (GTD) |
| 126 | ExpireTime | UTCTimestamp | C | Required when `TimeInForce` (59) is set to `GTD` (6). Specifies the time when a GTD order expires. Required for GTD orders and should not be set for other orders. The order expires within one second after the specified time. |
| 99 | StopPx | Decimal | C | Specifies the quote price at which the order activates for Stop Limit order types (40=4) |
| 1109 | TriggerPriceDirection | Char | N | **Supported values:**<br>`U` = Trigger if market price goes UP to or through `StopPx` (default if `StopPx` is greater than current market price)<br>`D` = Trigger if market price goes DOWN to or through `StopPx` (default if `StopPx` is less than current market price)<br>_For stop-limit orders, this field is optional but recommended._ |
| 7928 | SelfTradeType | Char | N | The following values specify what to do when two orders are submitted by the same user attempt to match:<br>`D` = Decrement and Cancel (default if not specified)<br>`O` = Cancel Oldest (resting order)<br>`N` = Cancel Newest (aggressing order)<br>`B` = Cancel Both |

### NewOrderBatch (35=U6) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#neworderbatch-35u6 "Direct link to NewOrderBatch (35=U6)")

Used to submit new spot orders to the Exchange matching engine. Clients should use this message to submit multiple orders to the Exchange matching engine at the same time. Currently, all the orders submitted in a batch must be for the same symbol.

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 8014 | BatchID | UUID | Y | An identifier specified by the sender to uniquely identify other messages correlating to this request. It must be a variant 1 UUIDv4 that follows the standard format. This means all lowercase and hyphens that group the characters in sequences of 8, 4, 4, 4, 12 (e.g. `1985ca2d-61ef-49f1-bfce-6c39d8462914`). Failure to follow this formatting will result in a reject. |
| 73 | NoOrders | Int | Y | Number of orders in the request. |
| =>11 | ClOrdID | UUID | Y | An identifier specified by the sender to uniquely identify other messages correlating to this request. It must be a variant 1 UUIDv4 that follows the standard format. This means all lowercase and hyphens that group the characters in sequences of 8, 4, 4, 4, 12 (e.g. `1985ca2d-61ef-49f1-bfce-6c39d8462914`). Failure to follow this formatting will result in a reject. <br>This shouldn't match the ClOrdID of any open orders. Additionally, it shouldn't match any other ClOrdIDs in this batch. |
| =>18 | ExecInst | Char | N | The execution instruction flags for the order.<br>**Supported values:**<br>`A` = Add Liquidity Only (Post Only) |
| =>38 | OrderQty | Decimal | C | The amount of the base asset to be transacted. Required except for market orders with `CashOrderQty` specified. |
| =>152 | CashOrderQty | Decimal | C | The order size in quote units (e.g., USD) (Market order only). |
| =>40 | OrdType | Char | Y | The type of order for the request which can be.<br>**Supported values:**<br>`1` = Market<br>`2` = Limit<br>`4` = Stop Limit |
| =>44 | Price | Decimal | C | The limit price for limit orders of the quote asset. The decimal precision must fall within the requirements for each market, see the REST API for precision and decimal limits. |
| =>54 | Side | Char | Y | Side of the order.<br>**Supported values:**<br>`1` = Buy<br>`2` = Sell |
| =>55 | Symbol | String | Y | Symbol of the instrument being traded (e.g. `BTC-USDC`) |
| =>59 | TimeInForce | Char | Y | Specifies how long the order remains in effect.<br>**Supported values:**<br>`1` = Good Till Cancel (GTC)<br>`3` = Immediate Or Cancel (IOC)<br>`4` = Fill Or Kill (FOK)<br>`6` = Good Till Date (GTD) |
| =>126 | ExpireTime | UTCTimestamp | C | Required when `TimeInForce` (59) is set to GTD (6). Specifies the time when a GTD order expires. Required for GTD orders and should not be set for other orders. The order expires within one second after the specified time. |
| =>99 | StopPx | Decimal | C | Specifies the quote price at which the order activates for Stop Limit order types (40=4). |
| =>7928 | SelfTradeType | Char | N | Represents type of cancel instruction when two orders submitted by the same user attempt to match.<br>**Supported values:**<br>`D` =Decrement and Cancel (default if not specified)<br>`O` =Cancel Oldest (resting order)<br>`N` =Cancel Newest (aggressing order)<br>`B` =Cancel Both |

### NewOrderBatchReject (35=U7) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#neworderbatchreject-35u7 "Direct link to NewOrderBatchReject (35=U7)")

This message is sent by Coinbase Exchange back to clients when all the orders in a [New Order Batch](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#neworderbatch-35u6) (35=U6) Request are rejected. When only some of the orders are rejected, Execution Report - Rejected messages are sent out for each of the orders individually.

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 8014 | BatchID | UUID | Y | Client-supplied ID identifying the new order batch request. |
| 58 | Text | String | Y | The reason the batch of orders was rejected. |

### OrderCancelRequest (35=F) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#ordercancelrequest-35f "Direct link to OrderCancelRequest (35=F)")



Coinbase Recommends

For order cancel requests, Coinbase recommends that you use the same FIX connection that was used to place the order.

Used to cancel an order that is still live on the Exchange matching engine.

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 11 | ClOrdID | UUID | Y | An identifier specified by the sender to uniquely identify other messages correlating to this request. It must be a variant 1 UUIDv4 that follows the standard format. This means all lowercase and hyphens that group the characters in sequences of 8, 4, 4, 4, 12 (e.g. `1985ca2d-61ef-49f1-bfce-6c39d8462914`). Failure to follow this formatting will result in a reject. |
| 37 | OrderID | UUID | Y | The exchange order ID of the order to be canceled. |
| 41 | OrigClOrdID | UUID | Y | The client order ID of the order to be canceled.<br>At least one of `OrigClOrdID` or `OrderID` must be specified. |
| 55 | Symbol | String | Y | Must match the message that the `OrigClOrdID` references. |

### OrderCancelReject (35=9) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#ordercancelreject-359 "Direct link to OrderCancelReject (35=9)")

This message is sent by Coinbase Exchange back to clients to reflect that an order could not be canceled on the matching engine in the following situations:

- When an [Order Cancel Request](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#ordercancelrequest-35f) (35=F) is rejected (CxlRejResponseTo 434=1)
- When an [Order Cancel/Replace Request](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#ordercancelreplacerequest-35g) (35=G) is rejected (CxlRejResponseTo 434=2)
- When an [Order Cancel Batch](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#ordercancelbatch-35u4) (35=U4) is partially rejected (CxlRejResponseTo 434=1)

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 11 | ClOrdID | UUID | Y | Echoed back from the client request. |
| 37 | OrderID | UUID | C | Echoed back from the client request. |
| 41 | OrigClOrdID | UUID | Y | Echoed back from the client request. |
| 58 | Text | String | N | Description of why the order could not be canceled. |
| 39 | OrdStatus | Char | Y | **Always:**<br>`8` = Rejected |
| 102 | CxlRejReason | Int | N | **Supported values:**<br>`1` = Unknown Order<br>`2` = Broker |
| 434 | CxlRejResponseTo | Char | Y | **Supported values:**<br>`1` = Order Cancel Request<br>`2` = Order Cancel/Replace Request |

### OrderCancelBatch (35=U4) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#ordercancelbatch-35u4 "Direct link to OrderCancelBatch (35=U4)")



Coinbase Recommends

For order cancel batch requests, Coinbase recommends that you use the same FIX connection that was used to place the order.

Clients should use this message to cancel multiple orders on the Exchange matching engine at the same time. Currently, all the orders canceled in a batch must be for the same symbol.

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 8014 | BatchID | UUID | Y | Client-supplied ID identifying the order cancel batch request. |
| 73 | NoOrders | Int | Y | Number of orders in the request. |
| =>11 | ClOrdID | UUID | Y | Client-supplied ID identifying the order cancel request. |
| =>37 | OrderID | UUID | Y | The exchange order ID of the order to be canceled. |
| =>41 | OrigClOrdID | UUID | Y | The client order ID of the order to be canceled.<br>At least one of `OrigClOrdID` or `OrderID` must be specified. |
| =>55 | Symbol | String | Y | Must match the message that the `OrigClOrdID` references. |

### OrderCancelBatchReject (35=U5) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#ordercancelbatchreject-35u5 "Direct link to OrderCancelBatchReject (35=U5)")

This message is sent by Coinbase Exchange back to clients when all the orders in an [Order Cancel Batch](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#ordercancelbatch-35u4) (35=U4) Request could not be canceled. When only some of the orders could not be canceled, [Order Cancel Reject](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#ordercancelreject-359) (35=9) messages are sent out for the orders individually.

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 8014 | BatchID | UUID | Y | Client-supplied ID identifying the order cancel batch request. |
| 58 | Text | String | N | The reason the order cancel batch request was rejected. |

### OrderCancelReplaceRequest (35=G) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#ordercancelreplacerequest-35g "Direct link to OrderCancelReplaceRequest (35=G)")



Use Original FIX Connection

You must send order cancel replace requests via the same FIX connection through which the original order was placed.

Clients should use this message to modify a single order on the Exchange matching engine (only order price and order size can be modified). If order quantity is increased or order price is modified, queue priority is lost. Queue priority is maintained when order quantity is decreased.

Modified orders share the same exchange `OrderID`(37) as the parent order.

Orders are modified with "in-flight mitigation" - i.e. any partially filled quantity on the parent order is carried over to the child order and is reflected in the new order's remaining quantity `LeavesQty`(151).

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 11 | ClOrdID | UUID | Y | The client order ID of the new order (that will replace an existing order). <br>This shouldn't match the ClOrdID of any open orders. |
| 37 | OrderID | UUID | Y | An identifier matching the `OrderID` from the [NewOrderSingle](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#newordersingle-35d), [NewOrderBatch](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#neworderbatch-35u6), or [OrderCancelReplaceRequest](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#ordercancelreplacerequest-35g) that this request applies to. |
| 41 | OrigClOrdID | String | Y | An identifier matching the `ClOrdID` from the [NewOrderSingle](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#newordersingle-35d), [NewOrderBatch](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#neworderbatch-35u6), or [OrderCancelReplaceRequest](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#ordercancelreplacerequest-35g) that this request applies to. |
| 38 | OrderQty | Decimal | Y | The new amount of the base asset to be transacted. |
| 44 | Price | Decimal | Y | The new desired limit price of the order. |
| 55 | Symbol | String | Y | Must match the symbol on the message that the `OrigClOrdID` references. |
| 40 | OrdType | Char | Y | **Must be:**<br>`2` = Limit |

### OrderMassCancelRequest (35=q) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#ordermasscancelrequest-35q "Direct link to OrderMassCancelRequest (35=q)")

Sent by customer to Coinbase to request mass cancellation of all orders on a FIX session previously submitted by customer.



Info

At this time, only mass cancels for Trading Sessions are supported ( `530=6`).

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 11 | ClOrdID | UUID | Y | Identifier of the Mass Cancel request (not the order ID to be canceled) |
| 530 | MassCancelRequestType | Char | Y | Type of orders to be canceled: <br>- `6` \- Cancel Orders for a Trading Session |
| 60 | TransactTime | UTCTimestamp | Y | Request timestamp |



Not guaranteed

Like [Cancel on Disconnect](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#:~:text=8013,CancelOrdersOnDisconnect), orders that were sent by the customer, but not yet acknowledged by the exchange, are not guaranteed to be canceled.

### OrderMassCancelReport (35=r) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#ordermasscancelreport-35r "Direct link to OrderMassCancelReport (35=r)")

Sent by Coinbase to the customer as an acknowledgement of an Order Mass Cancel Request for processing or a rejection of the request.

Receipt of a successful Order Mass Cancel Report does not imply that orders were canceled until "Execution Report - Canceled" is sent to customer.

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 11 | ClOrdID | UUID | Y | ID echoed from the Order Mass Cancel Request |
| 530 | MassCancelRequestType | Char | Y | Echoed from the Order Mass Cancel Request: `6` \- Cancel Orders for a Trading Session |
| 531 | MassCancelResponse | Char | Y | If the Order Mass Cancel Request was rejected: <br>- `0` \- Request Rejected<br>If successful, echoed from the request: <br>- `3` \- Cancel Orders for a Product on Profile<br>- `6` \- Cancel Orders for a Trading Session<br>- `7` \- Cancel All Orders on Profile |
| 58 | Text | String | N | A message explaining why the request was rejected |

### ExecutionReport (35=8) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#executionreport-358 "Direct link to ExecutionReport (35=8)")

This message is sent by Coinbase Exchange back to clients to reflect changes to an order's state (accepted, replaced, restated, partially filled, filled, expired, or canceled).

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 11 | ClOrdID | UUID | Y | The client order ID of the (new) order. |
| 37 | OrderID | UUID | Y | A unique identifier assigned by the exchange for the order. |
| 41 | OrigClOrdID | String | C | The client order ID of the parent order for [Order Cancel/Replace Requests](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#ordercancelreplacerequest-35g). |
| 6 | AvgPx | Decimal | C | The volume-weighted average price of all fills on the order. |
| 14 | CumQty | Decimal | C | The cumulative base quantity (e.g. in BTC) filled on the order. |
| 151 | LeavesQty | Decimal | C | The remaining base quantity (e.g. in BTC) on the order.<br>Not sent for market orders that were sent using `CashOrderQty`. |
| 17 | ExecID | UUID | Y | ID identifying this execution report. |
| 39 | OrdStatus | Char | Y | **Supported values:**<br>`0` = New<br>`1` = Partially Filled<br>`2` = Filled<br>`4` = Canceled<br>`5` = Replaced<br>`8` = Rejected<br>`C` = Expired (For IOC expirations) |
| 150 | ExecType | Char | Y | **Supported values:**<br>`0` = New<br>`4` = Canceled<br>`5` = Replaced<br>`8` = Rejected<br>`C` = Expired (For IOC expirations)<br>`D` = Restated (in cases where orders are partially canceled unsolicited due to self-trade prevention)<br>`F` = Trade<br>`I` = Order Status (in response to Order Status Requests) |
| 55 | Symbol | String | Y | The symbol of the order (e.g. BTC-USD). |
| 54 | Side | Char | C | **Supported values:**<br>`1` = Buy<br>`2` = Sell |
| 40 | OrdType | Char | C | **Supported values:**<br>`1` = Market<br>`2` = Limit<br>`4` = Stop Limit |
| 32 | LastQty | Char | C | The base quantity (e.g. in BTC) of the most recent fill on the order when `ExecType` is `F` (Trade). |
| 31 | LastPx | Decimal | C | The price of the most recent fill on the order when `ExecType` is `F` (Trade). |
| 44 | Price | Decimal | C | The limit price of the order. |
| 38 | OrderQty | Decimal | C | The base quantity (e.g. in BTC) of the order. |
| 1138 | DisplayQty | Decimal | C | Maximum size within an order to be displayed. Must be > 10% of OrderQty |
| 198 | SecondaryOrderID | String | C | Assigned by party that accepts the order. Can be used to provide the OrderID (37) used by an exchange or executing system. |
| 152 | CashOrderQty | Decimal | C | The quote quantity (e.g. in USD) of the order.<br>For market orders that were submitted using `CashOrderQty` instead of `OrderQty`, this is the remaining quote quantity of the order. |
| 58 | Text | String | N | Description of why the order was rejected, canceled, or expired. |
| 60 | TransactTime | UTCTimestamp | Y | Matching engine timestamp. |
| 103 | OrdRejReason | Int | N | **Supported values:**<br>`0` = Broker<br>`1` = Unknown Symbol<br>`5` = Unknown Order |
| 378 | ExecRestatementReason | Int | N | **Supported values:**<br>`5` = Partial Decline of `OrderQty` (in cases where orders are partially canceled unsolicited due to self-trade prevention). |
| 1003 | TradeID | String | C | Trade ID for a given fill used for reporting. |
| 1057 | AggressorIndicator | Boolean | C | **Supported values:**<br>`Y` = Taker (if aggressor or auction trade)<br>`N` = Maker |
| 59 | TimeInForce | Char | C | **Supported values:**<br>`1` = GTC<br>`3` = IOC<br>`4` = FOK<br>`6` = GTD |
| 99 | StopPx | Decimal | C | For stop-limit orders, the stop price of the order. |
| 1109 | TriggerPriceDirection | Char | N | For stop-limit orders.<br>**Supported values:**<br>`U` = Trigger if market price goes UP to or through `StopPx`<br>`D` = Trigger if market price goes DOWN to or through `StopPx` |
| 18 | ExecInst | Char | N | **Supported values:**<br>`A` = Add Liquidity Only. |
| 7928 | SelfTradeType | Char | N | **Supported values:**<br>`D` = Decrement and Cancel (default if not specified)<br>`O` = Cancel Oldest (resting order)<br>`N` = Cancel Newest (aggressing order)<br>`B` = Cancel Both |
| 126 | ExpireTime | UTCTimestamp | C | Timestamp at which a GTD order would expire. |
| 136 | NoMiscFees | Int | C | Repeating group for fees charged.<br>Always `1` on an order partial fill or fill. |
| =>137 | MiscFeeAmt | Decimal | C | See `MiscFeeBasis`. |
| =>138 | MiscFeeCurr | String | C | The currency that the fee is charged in. |
| =>139 | MiscFeeType | String | C | **Always:**<br>`4` = Exchange Fees. |
| =>891 | MiscFeeBasis | Int | C | **Supported values:**<br>`0` = Absolute ( `MiscFeeAmt` is in `MiscFeeCurr` terms)<br>`2` = Percentage ( `MiscFeeAmt` should be multiplied by the fill quantity in `MiscFeeCurr` terms to calculate the fee in `MiscFeeCurr` terms) |

### BusinessMessageReject (35=j) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#businessmessagereject-35j "Direct link to BusinessMessageReject (35=j)")

An application level reject message sent when the FIX session can't process a message.

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 45 | RefSeqNum | Int | N | The `MsgSeqNum` of the referenced message that was rejected. |
| 372 | RefMsgType | Int | Y | The message type that this reject message applies to.<br>**Supported values include:**<br>Admin Messages<br>`A` = Logon<br>`0` = Heartbeat<br>`1` = TestRequest<br>`3` = Reject<br>`5` = Logout<br>Application Messages<br>`D` = NewOrderSingle<br>`F` = OrderCancelRequest<br>`G` = OrderCancelReplaceRequest<br>`H` = OrderStatusRequest<br>`j` = BusinessMessageReject<br>`8` = ExecutionReport<br>`9` = OrderCancelReject<br>`U4` = OrderCancelBatch<br>`U5` = OrderCancelBatchReject<br>`U6` = NewOrderBatch<br>`U7` = NewOrderBatchReject |
| 379 | BusinessRejectRefID | String | N | The `ClOrdID`, `OrderID`, `BatchID`, or other identifying ID on the failed request. |
| 380 | BusinessRejectReason | Int | N | A code to quickly identify common reasons for a reject.<br>**Supported values include:**<br>`1` = Other<br>`2` = Unsupported Message Type |
| 58 | Text | String | N | A message explaining why the message was rejected. |

## RFQ [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#rfq "Direct link to RFQ")

### Quote Request (R) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#quote-request-r "Direct link to Quote Request (R)")

A Quote Request (R) is the start of the RFQ process. Coinbase sends a Quote Request to Liquidity Providers (LPs) on behalf of a customer looking to participate in an RFQ trade. LPs respond to a Quote Request with a [Quote](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#quote-s).

| Tag | Name | Type | Required | Notes |
| --- | --- | --- | --- | --- |
| 131 | QuoteReqID | UUID | Y | Unique identifier for RFQ |
| 146 | NoRelatedSym | NumInGroup | Y | Always 1 |
| 55 | Symbol | String32 | Y | Example: `BTC-AVAX` |
| 38 | OrderQty | Float64 | Y | The quantity the customer is looking to trade via RFQ |
| 62 | ValidUntilTime | UTCTimestamp | Y | The time by which quotes must be submitted for the RFQ |
| 126 | ExpireTime | UTCTimestamp | Y | The time by which the RFQ expires if there is no match |
| 136 | NoMiscFees | NumInGroup | Y | Always 1 |
| 137 | MiscFeeAmt | Float64 | Y | Fee as a percentage that Liquidity Providers are charged on a winning Quote. <br>The fee is charged in the currency the LP receives (e.g., in BTC if LP is buying BTC-AVAX, or in AVAX if LP is selling BTC-AVAX). <br>Example: 0.0005 (5 bps) |
| 139 | MiscFeeType | Int32 | Y | Always 4 = Exchange Fees |
| 891 | MiscFeeBasis | Int32 | Y | Always 2 = Percentage |
| 528 | OrderCapacity | Char | Y | A = Agency (default) <br>C = Corporate |

### Quote (S) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#quote-s "Direct link to Quote (S)")

Quote (S) messages are submitted by Liquidity Providers (LP) in response to a [Quote Request](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#quote-request-r) in order to participate in the competitive RFQ auction.

Quotes can be submitted as either a one-way or two-way quote, and must be received by the `ValidUntilTime (62)` specified in the Quote Request. Only one side is traded if the Liquidity Provider wins the RFQ.

| Tag | Name | Type | Required | Notes |
| --- | --- | --- | --- | --- |
| 131 | QuoteReqID | UUID | Y | Unique identifier for RFQ echoed from Quote Request |
| 117 | QuoteID | UUID | Y | Unique identifier for Quote specified by Liquidity Provider |
| 55 | Symbol | String32 | Y | Example: `BTC-AVAX` |
| 132 | BidPx | Float64 | C | Required if submitting bid |
| 133 | OfferPx | Float64 | C | Required if submitting offer |
| 134 | BidSize | String32 | C | Required if submitting bid. Must match `OrderQty (38)` from Quote Request |
| 135 | OfferSize | String32 | C | Required if submitting offer. Must match `OrderQty (38)` from Quote Request |

### Quote Status Report (AI) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#quote-status-report-ai "Direct link to Quote Status Report (AI)")

Quote Status Reports are sent to Liquidity Providers with [Quote](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#quote-s) statuses and expired [Quote Requests](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#quote-request-r).

- If the [Quote](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#quote-s) is rejected b/c validation checks failed or it was sent too late, the response to the quoter is `297=5` (QuoteStatus = Rejected).
- If the [Quote](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#quote-s) is accepted and eligible to participate in an RFQ auction, the response to the quoter is `297=16` (QuoteStatus = Active).
- If the [Quote](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#quote-s) is accepted but not selected for execution, the response to the quoter is `297=17` (QuoteStatus = Canceled).
- If the [Quote](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#quote-s) is accepted and selected for execution, the response to the quoter is `297=19` (QuoteStatus = Pending End Trade), followed by Execution Report - Filled.
- If the [Quote Request](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#quote-request-r) is unmatched by `ExpireTime (126)` on the Quote Request, `297=7` (QuoteStatus = Expired) is broadcast to all LPs.

| Tag | Name | Type | Required | Notes |
| --- | --- | --- | --- | --- |
| 131 | QuoteReqID | UUID | Y | Unique identifier for RFQ echoed from Quote Request |
| 117 | QuoteID | UUID | C | Unique identifier for Quote specified unless QuoteStatus = Expired ( `297=7`) |
| 55 | Symbol | String32 | Y | Example: `BTC-AVAX` |
| 54 | Side | Char | C | Buy: `54=1`, Sell: `54=2`<br>Specified if QuoteStatus=Pending End Trade ( `297=19`) |
| 38 | OrderQty | Float64 | Y | Echoed from Quote Request |
| 132 | BidPx | Float64 | C | Echoed from Quote |
| 133 | OfferPx | Float64 | C | Echoed from Quote |
| 134 | BidSize | Float64 | C | Echoed from Quote |
| 135 | OfferSize | Float64 | C | Echoed from Quote |
| 62 | ValidUntilTime | UTCTimestamp | Y | Echoed from Quote Request |
| 126 | ExpireTime | UTCTimestamp | Y | Echoed from Quote Request |
| 297 | QuoteStatus | Int32 | Y | `5` = **Rejected**: Quote failed validation checks or was sent too late<br>`7` = **Expired**: Quote Request expired w/no match<br>`16` = **Active**: Quote was acknowledged<br>`17` = **Canceled**: Quote not selected b/c LP did not win auction or had insufficient funds<br>`19` = **Pending End Trade**: Quote selected for execution |
| 58 | Text | String | C | Reason the Quote was rejected if QuoteStatus=5<br>Can also be “Unable to hold funds” if QuoteStatus=17 |

### RFQ Request (AH) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50\#rfq-request-ah "Direct link to RFQ Request (AH)")

Request For Quote (RFQ) allows Liquidity Providers to respond to, and interact with, real-time RFQ requests. The RFQ process begins with [Quote Request (R)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#quote-request-r).

RFQ is enabled for users who have been approved by Coinbase as a Liquidity Provider. Once approved, clients must send an RFQ Request message ( `35=AH`) after each successful Logon message ( `35=A`) for any session in which they are interested in receiving Quote Requests.

| Tag | Name | Type | Required | Notes |
| --- | --- | --- | --- | --- |
| 644 | RFQReqID | UUID | Y | Unique identifier for RFQ Request |



Tip

_Not_ receiving a response is expected and indicative of a successful RFQ Request.

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Components](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#components)
  - [Standard Header](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#standard-header)
  - [Standard Trailer](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#standard-trailer)
- [Administrative](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#administrative)
  - [Logon (35=A)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#logon-35a)
  - [Heartbeat (35=0)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#heartbeat-350)
  - [TestRequest (35=1)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#testrequest-351)
  - [ResendRequest (35=2)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#resendrequest-352)
  - [SequenceReset (35=4)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#sequencereset-354)
  - [Reject (35=3)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#reject-353)
  - [Logout (35=5)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#logout-355)
- [Trading](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#trading)
  - [NewOrderSingle (35=D)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#newordersingle-35d)
  - [NewOrderBatch (35=U6)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#neworderbatch-35u6)
  - [NewOrderBatchReject (35=U7)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#neworderbatchreject-35u7)
  - [OrderCancelRequest (35=F)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#ordercancelrequest-35f)
  - [OrderCancelReject (35=9)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#ordercancelreject-359)
  - [OrderCancelBatch (35=U4)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#ordercancelbatch-35u4)
  - [OrderCancelBatchReject (35=U5)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#ordercancelbatchreject-35u5)
  - [OrderCancelReplaceRequest (35=G)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#ordercancelreplacerequest-35g)
  - [OrderMassCancelRequest (35=q)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#ordermasscancelrequest-35q)
  - [OrderMassCancelReport (35=r)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#ordermasscancelreport-35r)
  - [ExecutionReport (35=8)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#executionreport-358)
  - [BusinessMessageReject (35=j)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#businessmessagereject-35j)
- [RFQ](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#rfq)
  - [Quote Request (R)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#quote-request-r)
  - [Quote (S)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#quote-s)
  - [Quote Status Report (AI)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#quote-status-report-ai)
  - [RFQ Request (AH)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#rfq-request-ah)

[docs_cdp_coinbase_com_exchange_docs_websocket_best_practices.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/websocket-best-practices#__docusaurus_skipToContent_fallback)

- You can subscribe to both `ws-feed` (Coinbase Market Data) and `ws-direct` (Coinbase Direct Market Data), but if `ws-direct` is your primary connection, we recommend using `ws-feed` as a failover.

- Remember [WebSocket rate limits](https://docs.cdp.coinbase.com/exchange/docs/websocket-rate-limits).

- Spread subscriptions (especially full channel subscriptions) over more than one websocket client connection. For example, do not subscribe to BTC-USD and ETH-USD on the same channel if possible. Instead, open up two separate websocket connections to help load balance those inbound messages across separate connections.

- Websocket clients should authenticate to help troubleshoot issues if necessary. Authenticating is optional and does not impact web socket performance.

- Connected clients should increase their web socket receive buffer to the largest configurable amount possible (given any client library or infrastructure limitations), due to the potential volume of data for any given product.

- Include the following header in the opening handshake to allow for compression, which will lower bandwidth consumption with minimal impact to CPU / memory: `Sec-WebSocket-Extensions: permessage-deflate`. See [Websocket Compression Extension](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview#websocket-compression-extension)

- Use less verbose subscriptions where possible (e.g., Level 2 over Full/Level 3).

- Use alternative batch channels like “level2\_batch” instead of “level2” and “ticket\_batch” instead of “ticket” which deliver a batched version of the respective data on a set interval reducing overall traffic.

- Mitigate error messages which are returned when the client is actively disconnected for any of these reasons:


  - The client has too many backed up messages ( `ErrSlowConsume`)

Limit the use of I/O operations and in-memory lock-free constructs when processing any websocket client callbacks. Queuing messages and processing them off-thread is another strategy that can prevent slow consumer errors.

  - The client is sending too many messages ( `ErrSlowRead`)

Space out websocket requests to adhere to the above rate limits.

  - The message size is too large ("Message too big").

Break up your subscription messages into smaller requests abiding by the rate limits.

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_fix_downloads.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/fix-downloads#__docusaurus_skipToContent_fallback)

![](https://img.shields.io/badge/Tarball%20updated-2024%20FEB%2023-0a639a)

A tarball of the Coinbase Exchange FIX dictionaries is available for download:

- [cb\_exch\_fix\_dictionaries-latest.tar.gz](https://docs.cdp.coinbase.com/downloads/exchange/cb_exch_fix_dictionaries-latest.tar.gz)

```codeBlockLines_p187
% tree cb_exch_fix_dictionaries-latest
cb_exch_fix_dictionaries-latest
├── market-data
│   ├── FIX50-prod-sand.xml
│   └── FIXT11-prod-sand.xml
└── order-entry
    ├── FIX42-prod-sand.xml
    ├── FIX50-prod-sand.xml
    └── FIXT11-prod-sand.xml

```



Unzip tar.gz file

- Mac: Double-click file
- Linux: `tar -xzf cb_exch_fix_dictionaries-latest.tar.gz`

## Archive [](https://docs.cdp.coinbase.com/exchange/docs/fix-downloads\#archive "Direct link to Archive")

- 2023-OCT-06: [cb\_exch\_fix\_dictionaries-20231006.tar.gz](https://docs.cdp.coinbase.com/downloads/exchange/archive/cb_exch_fix_dictionaries-20231006.tar.gz)
- 2023-AUG-03: [cb\_exch\_fix\_dictionaries-20230803.tar.gz](https://docs.cdp.coinbase.com/downloads/exchange/archive/cb_exch_fix_dictionaries-20230803.tar.gz)

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Archive](https://docs.cdp.coinbase.com/exchange/docs/fix-downloads#archive)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_fix_connectivity.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/fix-connectivity#__docusaurus_skipToContent_fallback)

[Financial Information eXchange](http://en.wikipedia.org/wiki/Financial_Information_eXchange), or FIX, is a standard protocol which can be used to enter orders, submit cancel requests, and receive fills. FIX API users typically have existing software that runs FIX for order management.

The baseline specification for the Exchange FIX API is mixed:

- Order Entry: [FIX 4.2 SP2](https://www.onixs.biz/fix-dictionary/4.2/index.html)
- Market Data: [FIX 5.0 SP2](https://www.onixs.biz/fix-dictionary/5.0/index.html)



FIX5 Resets Saturdays at 1PM ET

FIX5 Order Entry and Market Data customers will be logged out every Saturday at 1PM ET (6PM UTC).



Info

Changes are deployed every Monday and Thursday at or near `2PM EST (7PM UTC)`. At that time, a **logout** message is sent from the server to indicate the session is ending. We do not deploy on US federal holidays.

## Supported Endpoints [](https://docs.cdp.coinbase.com/exchange/docs/fix-connectivity\#supported-endpoints "Direct link to Supported Endpoints")



Info

**Production**

Order Entry (FIX42): `tcp+ssl://fix.exchange.coinbase.com:4198 `

Order Entry (FIX50): `tcp+ssl://fix-ord.exchange.coinbase.com:6121 `

Market Data (FIX50): `tcp+ssl://fix-md.exchange.coinbase.com:6121 `

**Sandbox**

Order Entry (FIX42): `tcp+ssl://fix-public.sandbox.exchange.coinbase.com:4198 `

Order Entry (FIX50): `tcp+ssl://fix-ord.sandbox.exchange.coinbase.com:6121 `

Market Data (FIX50): `tcp+ssl://fix-md.sandbox.exchange.coinbase.com:6121 `



Resend Requests

Resend requests are not supported. Every connection establishes a new session and a new set of session sequence numbers.

## FIX Gateway [](https://docs.cdp.coinbase.com/exchange/docs/fix-connectivity\#fix-gateway "Direct link to FIX Gateway")

Before logging onto a FIX session, clients must establish a secure connection to the FIX gateway. See the [available endpoints](https://docs.cdp.coinbase.com/exchange/docs/fix-connectivity#supported-endpoints) above.

**TCP SSL**

If your FIX implementation does not support establishing a **native TCP SSL connection**, you must setup a local proxy such as [stunnel](https://www.stunnel.org/) to establish a secure connection to the FIX gateway.

**Static IP**

Coinbase Exchange **does not** support static IP addresses. If your firewall rules require a static IP address, you must create a TCP proxy server with a static IP address which is capable of resolving an IP address using DNS.

**AWS IP**

If connecting from servers **outside of AWS** which require firewall rules, use the [AWS provided resources](https://docs.aws.amazon.com/general/latest/gr/aws-ip-ranges.html) to determine how best to whitelist AWS IP ranges.



Info

Changes are deployed every Monday and Thursday at or near `2PM EST (7PM UTC)`. At that time, a **logout** message is sent from the server to indicate the session is ending. We do not deploy on US federal holidays.

## Ciphers [](https://docs.cdp.coinbase.com/exchange/docs/fix-connectivity\#ciphers "Direct link to Ciphers")

Coinbase Exchange supports **TLSv1.2** with the following server ciphers:

| Recommend | Length | Cipher Suite | Elliptic Curve |
| --- | --- | --- | --- |
| Preferred | 128 bits | ECDHE-RSA-AES128-GCM-SHA256 | Curve P-256 DHE 256 |
| Accepted | 128 bits | ECDHE-RSA-AES128-SHA256 | Curve P-256 DHE 256 |
| Accepted | 256 bits | ECDHE-RSA-AES256-GCM-SHA384 | Curve P-256 DHE 256 |
| Accepted | 256 bits | ECDHE-RSA-AES256-SHA384 | Curve P-256 DHE 256 |

## SSL Tunnels [](https://docs.cdp.coinbase.com/exchange/docs/fix-connectivity\#ssl-tunnels "Direct link to SSL Tunnels")

[Exchange FIX API endpoints](https://docs.cdp.coinbase.com/exchange/docs/fix-connectivity#supported-endpoints) only accept TCP connections secured by SSL. If your FIX client library cannot establish an SSL connection natively, you must run a local proxy that establishes a secure connection and allows unencrypted local connections.

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Supported Endpoints](https://docs.cdp.coinbase.com/exchange/docs/fix-connectivity#supported-endpoints)
- [FIX Gateway](https://docs.cdp.coinbase.com/exchange/docs/fix-connectivity#fix-gateway)
- [Ciphers](https://docs.cdp.coinbase.com/exchange/docs/fix-connectivity#ciphers)
- [SSL Tunnels](https://docs.cdp.coinbase.com/exchange/docs/fix-connectivity#ssl-tunnels)

[docs_cdp_coinbase_com_exchange_docs_fix_msg_oe_lwf.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-lwf#__docusaurus_skipToContent_fallback)

Limit With Funds (LWF) orders allow users to fully execute an order up to a notional value specified in the product quote currency.



Info

LWF orders are supported in [FIX 4.2](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#new-order-single-d) and [FIX 5.0](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#newordersingle-35d).

## Parameters [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-lwf\#parameters "Direct link to Parameters")

| Tag | Name | Type | Required | Description |
| --- | --- | --- | --- | --- |
| 40 | OrdType | Char | Y | Order Type must be `2` (Limit) |
| 152 | CashOrderQty | Decimal | Y | The notional value you wish to trade |

All values for `TimeInForce`, `SelfTradePrevention`, and `PostOnly` are supported.



Caution

You must not define `OrderQty` when submitting a limit order with `CashOrderQty`.

## Summary [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-lwf\#summary "Direct link to Summary")



Note

`CashOrderQty` on limit orders is available for both buy and sell orders despite the following example featuring a buy order.

Today, if you want to trade $30,000 worth of BTC, you might submit a market order:

`OrdType=1|Side=1|CashOrderQty=30000`

However, a market order leaves the executed price out of the client's control.

With the following market state:

| Bid Size | Bid | Ask | Ask Size |
| --- | --- | --- | --- |
|  |  | 60,000 | 10 |
| 10 | 59,000 |  |  |

You can try to trade $30,000 of BTC by placing a limit buy order. To do this you must perform the `notional/price` division to calculate the necessary `OrderQty`. The resulting order would look like:

`OrdType=2|Side=1|Price=60000|OrderQty=0.5`

If this order is filled at $2,000, then everything works as intended. In actuality, the market may change from the time in between when the user submits the order and when it is received by the exchange.

To illustrate, consider the case where the market state has changed to the following at the time when the exchange receives your order:

| Bid Size | Bid | Ask | Ask Size |
| --- | --- | --- | --- |
|  |  | 59,000 | 10 |
| 10 | 58,999 |  |  |

Your order now fills at $59,000 for quantity `0.5`. The resulting notional for this trade is $29,500, which is less than what you originally wanted.

To solve this issue, you can specify `CashOrderQty` instead of `OrderQty`:

`OrdType=2|Side=1|Price=60000|CashOrderQty=30000`

Given the same market state:

| Bid Size | Bid | Ask | Ask Size |
| --- | --- | --- | --- |
|  |  | 59,000 | 10 |
| 10 | 58,999 |  |  |

The order will be filled as taker with quantity `0.50847457`, making the total notional of this order $29,999.9996.

In a separate example, with the following market state:

| Bid Size | Bid | Ask | Ask Size |
| --- | --- | --- | --- |
|  |  | 60,500 | 1 |
|  |  | 59,500 | 0.3 |
| 10 | 59,999 |  |  |

Your order will fill as a taker at price $59,500 with quantity `0.3`. Thus only $17850 notional will be filled. The remaining $12,150 notional will then rest on the book at price $60,000 with quantity `0.2025`.

## Caveats [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-lwf\#caveats "Direct link to Caveats")

- Orders may be filled at less than the notional specified due to fees and truncation of product base increment.
- [TPSL](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-tpsl) / [Iceberg](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-iceberg) / [Stop](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postorders/#stop-orders) / [Batch](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#neworderbatch-35u6) orders are not be supported with this feature.
- [OrderCancelReplaceRequest](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#ordercancelreplacerequest-35g) with `CashOrderQty` is not supported.

## Market Data [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-lwf\#market-data "Direct link to Market Data")

- `OrderQty`/ `CumQty`/ `LeavesQty` is supplied in all Execution Reports. In particular `OrderQty` is calculated after the order has been processed as a taker (i.e., it is **NOT** calculated with `CashOrderQty / Price`), such that all quantity tags are consistent with one another.
- `Size` field is populated in all WebSocket feed messages. No changes are expected from the perspective of a WebSocket consumer.

## Examples [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-lwf\#examples "Direct link to Examples")

In the following examples, all irrelevant tags are omitted.

**Example 1 - A buy GTC order partially fills before resting**

```codeBlockLines_p187
$> -> BeginString=FIX.4.2 MsgType=ORDER_SINGLE OrdType=LIMIT Price=2952 Side=BUY Symbol=ETH-USD TimeInForce=GOOD_TILL_CANCEL CashOrderQty=1000 CheckSum=026

$> <- BeginString=FIX.4.2 MsgType=EXECUTION_REPORT CumQty=0 ExecID=07debc62-aa75-4734-b1b5-91eb9ce8d49c ExecTransType=NEW OrderID=fa5d17b0-8344-4237-ab33-8c658595f960 OrderQty=0.33740512 OrdStatus=NEW Price=2952 Side=BUY Symbol=ETH-USD TransactTime=20240529-20:59:24.039 ExecType=NEW LeavesQty=0.33740512 CashOrderQty=996.01591424 CheckSum=091

```

Note that the value of `CashOrderQty` in the ExecutionReport is not $1,000 due to fees and base increment truncation.

```codeBlockLines_p187
$> <- BeginString=FIX.4.2 MsgType=EXECUTION_REPORT AvgPx=2951.81 CumQty=0.01 ExecID=d7b9d643-5567-5ba1-ae59-eca93bc15723 ExecTransType=NEW LastPx=2951.81 LastShares=0.01 OrderID=fa5d17b0-8344-4237-ab33-8c658595f960 OrderQty=0.33740512 OrdStatus=PARTIALLY_FILLED Price=2951.81 Side=BUY Symbol=ETH-USD TransactTime=20240529-20:59:24.039 ExecType=PARTIAL_FILL LeavesQty=0.32740512 1003=1267476 AggressorIndicator=YES

$> <- BeginString=FIX.4.2 MsgType=EXECUTION_REPORT AvgPx=2951.8666666666666667 CumQty=0.03 ExecID=83a0385b-96f4-532b-a704-cc8fbcbfecd8 ExecTransType=NEW LastPx=2951.92 LastShares=0.006 OrderID=fa5d17b0-8344-4237-ab33-8c658595f960 OrderQty=0.33740512 OrdStatus=PARTIALLY_FILLED Price=2951.92 Side=BUY Symbol=ETH-USD TransactTime=20240529-20:59:24.039 NoMiscFees=1 MiscFeeAmt=0.004 MiscFeeCurr=USD MiscFeeType=EXCHANGE_FEES ExecType=PARTIAL_FILL LeavesQty=0.30740512 MiscFeeBasis=Percentage 1003=1267479 AggressorIndicator=YES CheckSum=124

```

Your order fills as a taker with a notional of `0.03 * $2951.86666... = $88.556`.

The remaining notional of `$996.01591412 - $88.556 = $907.45991412` will rest on the book with a quantity of `$907.45991412 / $2952 = 0.30740512`.

Note that `OrderQty = CumQty + LeavesQty`. In the case of this specific order we have: `0.03 + 0.30740512 = 0.33740512`.

The order is now rested on the book and be filled as passive.

```codeBlockLines_p187
$> <- BeginString=FIX.4.2 MsgType=EXECUTION_REPORT AvgPx=2951.9 CumQty=0.04 ExecID=ef6a5354-e928-5815-b55b-46361fea6423 ExecTransType=NEW LastPx=2952 LastShares=0.01 OrderID=fa5d17b0-8344-4237-ab33-8c658595f960 OrderQty=0.33740512 OrdStatus=PARTIALLY_FILLED Price=2952 Side=BUY Symbol=ETH-USD TransactTime=20240529-20:59:51.230 NoMiscFees=1 MiscFeeAmt=0.0025 MiscFeeCurr=USD MiscFeeType=EXCHANGE_FEES ExecType=PARTIAL_FILL LeavesQty=0.29740512 MiscFeeBasis=Percentage AggressorIndicator=NO

```

**Example 2 - A buy IOC order that results in no fills**

```codeBlockLines_p187
$> -> BeginString=FIX.4.2 MsgType=ORDER_SINGLE ClOrdID=a79d33c4-7cc1-4948-b318-b878b5fbcc72 OrdType=LIMIT Price=1 Side=BUY Symbol=ETH-USD TimeInForce=IMMEDIATE_OR_CANCEL TransactTime=20240530-14:40:07.180 CashOrderQty=1000

$> <- BeginString=FIX.4.2 MsgType=EXECUTION_REPORT ClOrdID=a79d33c4-7cc1-4948-b318-b878b5fbcc72 CumQty=0 ExecID=087c5712-6805-4e66-83b6-81c9fc92a78e ExecTransType=NEW OrderID=34cf5775-eee6-462b-8db0-9ec51f212663 OrderQty=0 OrdStatus=NEW Price=1 Side=BUY Symbol=ETH-USD TransactTime=20240530-14:40:07.245 ExecType=NEW LeavesQty=0 CashOrderQty=0 CheckSum=003

$> <- BeginString=FIX.4.2 MsgType=EXECUTION_REPORT SenderCompID=Coinbase SendingTime=20240530-14:40:07.247 CumQty=0 ExecID=fcce5dea-9e83-492a-909c-30253e0b0d2f ExecTransType=NEW OrderID=34cf5775-eee6-462b-8db0-9ec51f212663 OrderQty=0 OrdStatus=CANCELED Price=1 Side=BUY Symbol=ETH-USD Text=101:Time In Force TransactTime=20240530-14:40:07.245 ExecType=CANCELED LeavesQty=0 CheckSum=214

```

Note that `OrderQty` is `0` in this case and this order will not be published in public WebSocket channels. It appears in the user channel only for this particular client.

**Example 3 - A sell GTC order with Self Trade Prevention (decrement and cancel)**

```codeBlockLines_p187
$> -> BeginString=FIX.4.2 MsgType=ORDER_SINGLE MsgSeqNum=41 ClOrdID=26dbf769-d812-4b0a-892a-bdf226387c0c OrdType=LIMIT Price=39944 Side=SELL Symbol=BTC-USD TimeInForce=GOOD_TILL_CANCEL TransactTime=20240531-14:24:32.566 CashOrderQty=10000 SelfTradePrevention=DECREMENT_AND_CANCEL CheckSum=225

$> <- BeginString=FIX.4.2 BodyLength=367 MsgType=EXECUTION_REPORT MsgSeqNum=48 SenderCompID=Coinbase SendingTime=20240531-14:24:32.705 ClOrdID=26dbf769-d812-4b0a-892a-bdf226387c0c CumQty=0 ExecID=f4054875-f834-409b-824a-2466bd3c066c ExecTransType=NEW OrderID=e19138ee-f97b-4bce-8cbe-ac8f6105ce30 OrderQty=0.2503 OrdStatus=NEW Price=39944 Side=SELL Symbol=BTC-USD TransactTime=20240531-14:24:32.702 ExecType=NEW LeavesQty=0.2503 CashOrderQty=9998.273235 CheckSum=061

$> <- BeginString=FIX.4.2 MsgType=EXECUTION_REPORT MsgSeqNum=49 AvgPx=39949.3007 CumQty=0.05 ExecID=0aaee39c-fc85-5d82-b6f2-07d9b5b9d02a ExecTransType=NEW LastPx=39949.3007 LastShares=0.05 OrderID=e19138ee-f97b-4bce-8cbe-ac8f6105ce30 OrderQty=0.2503 OrdStatus=PARTIALLY_FILLED Price=39949.3007 Side=SELL Symbol=BTC-USD TransactTime=20240531-14:24:32.702 ExecType=PARTIAL_FILL LeavesQty=0.2003 MiscFeeBasis=Percentage 1003=23863011 AggressorIndicator=YES CheckSum=130

$> <- BeginString=FIX.4.2 MsgType=EXECUTION_REPORT MsgSeqNum=50 AvgPx=39949.3007 CumQty=0.05 ExecID=30e4d848-a18b-469e-925a-1dbc83c17aea ExecTransType=NEW OrderID=e19138ee-f97b-4bce-8cbe-ac8f6105ce30 OrderQty=0.2253 OrdStatus=PARTIALLY_FILLED Price=39945 Side=SELL Symbol=BTC-USD TransactTime=20240531-14:24:32.702 ExecType=RESTATED LeavesQty=0.1753 ExecRestatementReason=PARTIAL_DECLINE_OF_ORDERQTY CheckSum=044

```

And this is the buy order with `LeavesQty` of `0.025` that was self trade cancelled:

```codeBlockLines_p187
$> <- BeginString=FIX.4.2 MsgType=EXECUTION_REPORT MsgSeqNum=51 CumQty=0 ExecID=0f4f96ad-160a-49a3-add0-eb25196fed70 ExecTransType=NEW OrderID=ca7e5097-cb6f-4381-8da8-629bc2656217 OrderQty=0.025 OrdStatus=CANCELED Price=39945 Side=BUY Symbol=BTC-USD Text=102:Self Trade Prevention TransactTime=20240531-14:24:32.702 ExecType=CANCELED LeavesQty=0 CheckSum=055

```

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Parameters](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-lwf#parameters)
- [Summary](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-lwf#summary)
- [Caveats](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-lwf#caveats)
- [Market Data](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-lwf#market-data)
- [Examples](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-lwf#examples)

[docs_cdp_coinbase_com_exchange_docs_websocket_auth.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/websocket-auth#__docusaurus_skipToContent_fallback)

The following WebSocket feeds require authentication:

- [Full channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#full-channel)
- [User channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#user-channel)
- [Level2 channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#level2-channel)
- [Level3 channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#level3-channel)

To authenticate, send a `subscribe` message and pass in fields to `GET /users/self/verify`, just as if you were [signing a request](https://docs.cdp.coinbase.com/exchange/docs/rest-auth#signing-a-message). To get the necessary parameters, go through the same process as you would to make [authenticated calls to the API](https://docs.cdp.coinbase.com/exchange/docs/rest-auth#signing-requests).



Caution

Authenticated feed messages do not increment the [sequence number](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview#sequence-numbers), which means that it is currently not possible to detect if an authenticated feed message was dropped.

## Examples [](https://docs.cdp.coinbase.com/exchange/docs/websocket-auth\#examples "Direct link to Examples")

A Python example of authenticating a WebSocket connection is shown below. This code sample can be cloned at [Coinbase Samples](https://github.com/coinbase-samples/exchange-scripts-py/tree/main/websocket).

```codeBlockLines_p187
API_KEY = str(os.environ.get('API_KEY'))
PASSPHRASE = str(os.environ.get('PASSPHRASE'))
SECRET_KEY = str(os.environ.get('SECRET_KEY'))

URI = 'wss://ws-feed.exchange.coinbase.com'
SIGNATURE_PATH = '/users/self/verify'

channel = 'level2'
product_ids = 'ETH-USD'

async def generate_signature():
    timestamp = str(time.time())
    message = f'{timestamp}GET{SIGNATURE_PATH}'
    hmac_key = base64.b64decode(SECRET_KEY)
    signature = hmac.new(
        hmac_key,
        message.encode('utf-8'),
        digestmod=hashlib.sha256).digest()
    signature_b64 = base64.b64encode(signature).decode().rstrip('\n')
    return signature_b64, timestamp

async def websocket_listener():
    signature_b64, timestamp = await generate_signature()
    subscribe_message = json.dumps({
        'type': 'subscribe',
        'channels': [{'name': channel, 'product_ids': [product_ids]}],
        'signature': signature_b64,
        'key': API_KEY,
        'passphrase': PASSPHRASE,
        'timestamp': timestamp
    })

```

Further examples are shown below:

```codeBlockLines_p187
// Authenticated feed messages add user_id and
// profile_id for messages related to your user
{
  "type": "open", // "received" | "open" | "done" | "match" | "change" | "activate"
  "user_id": "5844eceecf7e803e259d0365",
  "profile_id": "765d1549-9660-4be2-97d4-fa2d65fa3352"
  /* ... */
}

```

Here's an example of an authenticated `subscribe` request:

```codeBlockLines_p187
// Request
{
  "type": "subscribe",
  "product_ids": ["BTC-USD"],
  "channels": ["full"],
  "signature": "...",
  "key": "...",
  "passphrase": "...",
  "timestamp": "..."
}

```

## Benefits [](https://docs.cdp.coinbase.com/exchange/docs/websocket-auth\#benefits "Direct link to Benefits")

Coinbase recommends that you authenticate _all_ WebSocket channels, but only those listed above are enforced. You can authenticate yourself when [subscribing](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview#subscribe) to the WebSocket Feed. The benefits of authenticating are:

- Messages (in which you are of the parties) are expanded and have more useful fields.
- You receive private messages, such as lifecycle information about stop orders you placed.

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Examples](https://docs.cdp.coinbase.com/exchange/docs/websocket-auth#examples)
- [Benefits](https://docs.cdp.coinbase.com/exchange/docs/websocket-auth#benefits)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_fix_msg_market_data.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data#__docusaurus_skipToContent_fallback)

The FIX market data API provides an L3 feed only with direct, low-latency, deterministic access.

About this API:

- **Baseline**: [FIX 5.0 SP2 specification](https://www.onixs.biz/fix-dictionary/5.0.sp2/index.html).
- **Environments**: Production, Sandbox



Environment URLs

- Production Snapshot Enabled Gateway: `tcp+ssl://fix-md.exchange.coinbase.com:6121 `
- Production Snapshot Disabled Gateway: `tcp+ssl://fix-md.exchange.coinbase.com:6122 `
- Sandbox Snapshot Enabled Gateway: `tcp+ssl://fix-md.sandbox.exchange.coinbase.com:6121 `
- Sandbox Snapshot Disabled Gateway: `tcp+ssl://fix-md.sandbox.exchange.coinbase.com:6122`

You can connect with the same authentication as our existing FIX order entry system. Connectivity is limited to a single connection per API key—Order Entry [rate limits](https://docs.cdp.coinbase.com/exchange/docs/fix-rate-limits) _do not apply_ (connections, rps, burst rps).



FIX5 Resets Saturdays at 1PM ET

FIX5 Order Entry and Market Data customers will be logged out every Saturday at 1PM ET (6PM UTC).

A standard header must be present at the start of every message in both directions.

| Tag | FieldName | Type | Required | Notes |
| --- | --- | --- | --- | --- |
| 8 | BeginString | String | Y | Must be `FIXT.1.1` |
| 49 | SenderCompID | String | Y | Client API key (on messages from the client) |
| 56 | TargetCompID | String | Y | Must be `Coinbase` (on messages from client) |
| 52 | SendingTime | UTCTimestamp | Y | UTC time down to millisecond resolution in the format `YYYYMMDD-HH:MM:SS.sss` |

## Logon (35=A) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data\#logon-35a "Direct link to Logon (35=A)")

| Tag | FieldName | Type | Required | Notes |
| --- | --- | --- | --- | --- |
| 34 | MsgSeqNum | Int | Y | Must be `1` |
| 98 | EncryptMethod | Int | Y | Must be `0` (None) |
| 108 | HeartBtInt | Int | Y | Heartbeat interval is capped at 300s, defaults to 10s |
| 141 | ResetSeqNumFlag | Boolean | Y | Resets the sequence number. Can be `Y`/ `N` |
| 553 | Username | String | Y | Client API Key |
| 554 | Password | String | Y | Client API passphrase |
| 95 | RawDataLength | Int | Y | Number of bytes in RawData field |
| 96 | RawData | String | Y | [Client message signature](https://docs.cdp.coinbase.com/exchange/docs/rest-auth#signing-a-message) |
| 1137 | DefaultApplVerID | String | Y | Must be `9` (FIX 5.0 SP2) |

## Market Data Request (35=V) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data\#market-data-request-35v "Direct link to Market Data Request (35=V)")

Clients should use this message to subscribe to or unsubscribe from market data for one or more symbols.

| Tag | FieldName | Type | Required | Notes |
| --- | --- | --- | --- | --- |
| 262 | MDReqID | String | Y | Client identifier for the market data request |
| 263 | SubscriptionRequestType | Int | Y | 1=Subscribe<br>2=Unsubscribe |
| 146 | NoRelatedSym | Int | Y | How many symbols are in the request |
| =>55 | Symbol | String | Y | Repeating group of symbols for which the client requests market data |

#### Market Data Request Reject (35=Y) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data\#market-data-request-reject-35y "Direct link to Market Data Request Reject (35=Y)")

This message is sent to clients to reject an invalid market data request.

| Tag | FieldName | Type | Required | Notes |
| --- | --- | --- | --- | --- |
| 262 | MDReqID | String | Y | Client identifier for the market data request |
| 281 | MDReqRejReason | Char | Y | 0=Unknown symbol<br>1=Duplicate MDReqID<br>7=Other |
| 58 | Text | String | N | Error description |

## Security Status (35=f) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data\#security-status-35f "Direct link to Security Status (35=f)")

This message is streamed to clients together with the incremental updates for subscribed symbols and reflects changes in the trading status, tick size, or other attributes of an instrument.

| Tag | FieldName | Type | Required | Notes |
| --- | --- | --- | --- | --- |
| 262 | MDReqID | String | Y | Client identifier for the market data request |
| 83 | RptSeq | Long | Y | Public sequence number by symbol |
| 55 | Symbol | String | Y | Repeating group of symbols for which the client requests market data |
| 1682 | MDSecurityTradingStatus | String | Y | `trading_disabled`<br>`cancel_only`<br>`post_only`<br>`limit_only`<br>`full_trading`<br>`auction_mode` |
| 969 | MinPriceIncrement | Decimal | Y | Minimum increment for quote currency (e.g., 0.01 USD for BTC-USD) |
| 29003 | MinSizeIncrement | Decimal | Y | Minimum increment for base currency (e.g., 0.00000001 BTC for BTC-USD) |

## Market Data Incremental Refresh (35=X) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data\#market-data-incremental-refresh-35x "Direct link to Market Data Incremental Refresh (35=X)")

Coinbase Exchange sends L3 order-by-order updates so clients can build a full book of all open orders, plus acknowledgements of orders by the matching engine with the order’s client order ID (ClOrdID) before matching. This helps clients immediately identify which orders and trades in the book (both aggressive and passive) are theirs, as well gain advance knowledge of orders that are pending processing by the matching engine. These acks correspond to the `Received` message in the web-socket feed.

- When `MDEntryID` is not present, the message is the acknowledgement of an order prior to matching.
- When `MDEntryID` is present, the message should be used for book-building. You can ignore Change messages with an MDEntryID for which you never received a New message.



Info

When book-building, Change messages received before a corresponding New message can be ignored. Users may occasionally receive Change messages with `MDUpdateAction=1` and an MDEntryID with `Text=CHANGE_REASON_STP` when the quantity on the original received order was reduced due to Self-trade Prevention (prior to the order being placed on the order book).



Info

To maintain an up-to-date L3 order book when subscribing to the Snapshot Disabled Gateway:

1. Send a `SubscriptionRequestType=1` Market Data Request (35=V) message for the product(s) of interest.
2. Queue any Market Data Incremental Refresh (35=X) messages received over the FIX session.
3. Make a [REST request](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getproductbook#levels) for the order book snapshot from the REST API.
4. Playback queued messages, discarding sequence numbers before or equal to the snapshot sequence number.
5. Apply playback messages to the snapshot as needed.
6. After playback is complete, apply real-time Market Data Incremental Refresh (35=X) messages as they arrive.

| Tag | FieldName | Type | Required | Notes |
| --- | --- | --- | --- | --- |
| 262 | MDReqID | String | Y | Client identifier for the market data request |
| 268 | NoMDEntries | Int | Y | Always `1` |
| =>279 | MDUpdateAction | Char | Y | 0=New<br>1=Change<br>2=Delete |
| =>269 | MDEntryType | Char | Y | 0=Bid<br>1=Offer<br>2=Trade |
| =>278 | MDEntryID | String | N | If present, this ID is the order ID that should be used for book-building<br>If not present, this message is the initial ack and should not be used to build the book |
| =>83 | RptSeq | Long | Y | Public sequence number by symbol |
| =>55 | Symbol | String | Y | Repeating group of symbols for which the client requests market data |
| =>270 | MDEntryPx | Decimal | Y | The price of the order |
| =>271 | MDEntrySize | Decimal | Y | The quantity remaining of the order |
| =>60 | TransactTime | UTCTimestamp | Y | The engine timestamp of the order in microseconds |
| =>40 | OrdType | Char | N | Sent only if the message represents the initial ack of an order:<br>1=Market<br>2=Limit |
| =>11 | ClOrdID | String | N | The client order ID on the initial ack of an order |
| =>37 | OrderID | String | N | The exchange order ID on the initial ack of an order<br>OR<br>If MDEntryType=2, then this is the aggressive Order ID |
| =>58 | Text | String | N | If MDUpdateAction=1, then the possible values are:<br>`CHANGE_REASON_STP`<br>`CHANGE_REASON_MODIFY_ORDER`<br>`CHANGE_REASON_REMAINDER_AFTER_MODIFICATION`<br>If MDUpdateAction=2, then the possible values are:<br>`CANCELED`<br>`FILLED` |
| =>5797 | AggressorSide | Int | N | Sent only on trades MDEntryType=2<br>1=Buy<br>2=Sell |
| =>29004 | Funds | Decimal | N | Market orders may have an optional funds field which indicates how much quote currency is used to buy or sell |

## Market Data Snapshot Full Refresh (35=W) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data\#market-data-snapshot-full-refresh-35w "Direct link to Market Data Snapshot Full Refresh (35=W)")



Only Available On Snapshot Enabled Gateway

The Market Data Snapshot Full Refresh (35=W) message is only supported on the Snapshot Enabled Gateway.

This message provides a full snapshot of all orders in the order book, including those placed before the client subscribed to incremental market data.

A snapshot is requested automatically when a successful Market Data Request from the client is processed for a given symbol. Clients should queue up incremental updates and process only the incremental updates with sequence number RptSeq greater than the RptSeq in the initial MD Snapshot Full Refresh snapshot message.

If clients are already subscribed to a symbol and send another Market Data Request to subscribe, they will not receive a new snapshot for that symbol. Clients must unsubscribe and subscribe to the market data again for a given symbol to receive a new snapshot.

| Tag | FieldName | Type | Required | Notes |
| --- | --- | --- | --- | --- |
| 262 | MDReqID | String | Y | Client identifier for the market data request |
| 83 | RptSeq | Long | Y | Public sequence number for the final update in the snapshot by symbol |
| 893 | LastFragment | Char | Y | Is this the last message in the snapshot for a given symbol<br>Y=Yes<br>N=No |
| 55 | Symbol | String | Y | Repeating group of symbols for which the client requests market data |
| 268 | NoMDEntries | Int | Y | Number of orders to be added to the book in this snapshot message |
| 1682 | MDSecurityTradingStatus | String | Y | `trading_disabled`<br>`cancel_only`<br>`post_only`<br>`limit_only`<br>`full_trading`<br>`auction_mode` |
| =>269 | MDEntryType | Char | Y | 0=Bid<br>1=Offer |
| =>278 | MDEntryID | String | Y | The order ID that should be added to the book |
| =>270 | MDEntryPx | Decimal | Y | The price of the order |
| =>271 | MDEntrySize | Decimal | Y | The quantity remaining of the order |

## Security List Request (35=x) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data\#security-list-request-35x "Direct link to Security List Request (35=x)")

This message is sent by clients to request a full list of instruments that Coinbase Exchange supports together with each instrument’s trading status, tick size, minimum order quantity, and any other descriptive fields.

| Tag | FieldName | Type | Required | Notes |
| --- | --- | --- | --- | --- |
| 320 | SecurityReqID | String | Y | Client identifier for the request |
| 559 | SecurityListRequestType | Int | Y | Always 4=All Securities |

## Security List (35=y) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data\#security-list-35y "Direct link to Security List (35=y)")

Instrument definition messages are returned in response to a client’s Security List Request.

| Tag | FieldName | Type | Required | Notes |
| --- | --- | --- | --- | --- |
| 320 | SecurityReqID | String | Y | Client identifier for the request |
| 322 | SecurityResponseID | String | Y | Response ID for the Security List Request |
| 560 | SecurityRequestResult | Int | Y | 0=Valid Request<br>1=Invalid Request |
| 893 | LastFragment | Char | Y | Is this the last instrument definition message in response to the original request<br>Y=Yes<br>N=No |
| 393 | TotNoRelatedSym | Int | Y | Total number of symbols that will be sent cumulatively |
| 146 | NoRelatedSym | Int | Y | How many symbols are in this FIX message |
| 1682 | MDSecurityTradingStatus | String | Y | `trading_disabled`<br>`cancel_only`<br>`post_only`<br>`limit_only`<br>`full_trading`<br>`auction_mode` |
| =>55 | Symbol | String | Y | Repeating group of symbols for which the client requests market data |
| =>15 | Currency | String | Y | The quote currency for the symbol (e.g., USD if 55=BTC-USD) |
| =>562 | MinTradeVol | Decimal | Y | The minimum notional amount in quote currency terms for an order |
| =>969 | MinPriceIncrement | Decimal | Y | Minimum increment for quote currency (e.g., 0.01 USD for BTC-USD) |
| =>29003 | MinSizeIncrement | Decimal | Y | Minimum increment for base currency (e.g., 0.00000001 BTC for BTC-USD) |

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Header](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data#header)
- [Logon (35=A)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data#logon-35a)
- [Market Data Request (35=V)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data#market-data-request-35v)
- [Security Status (35=f)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data#security-status-35f)
- [Market Data Incremental Refresh (35=X)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data#market-data-incremental-refresh-35x)
- [Market Data Snapshot Full Refresh (35=W)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data#market-data-snapshot-full-refresh-35w)
- [Security List Request (35=x)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data#security-list-request-35x)
- [Security List (35=y)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data#security-list-35y)

[docs_cdp_coinbase_com_exchange_docs_fix_changelog.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/fix-changelog#__docusaurus_skipToContent_fallback)

This page documents Exchange FIX dictionary releases. For detailed FIX updates, follow the general Exchange [Changelog](https://docs.cdp.coinbase.com/exchange/docs/changelog).

## Order Entry Gateway [](https://docs.cdp.coinbase.com/exchange/docs/fix-changelog\#order-entry-gateway "Direct link to Order Entry Gateway")

### Coinbase Exchange FIX 5.0 [](https://docs.cdp.coinbase.com/exchange/docs/fix-changelog\#coinbase-exchange-fix-50 "Direct link to Coinbase Exchange FIX 5.0")

| Date | Baseline | Environments | Notes |
| --- | --- | --- | --- |
| 2023-07-21 | FIX 5.0 SP2 | Production, Sandbox | Initial release |

### Coinbase Exchange FIX 4.2 [](https://docs.cdp.coinbase.com/exchange/docs/fix-changelog\#coinbase-exchange-fix-42 "Direct link to Coinbase Exchange FIX 4.2")

| Date | Baseline | Environments | Notes |
| --- | --- | --- | --- |
| 2023-06-06 | FIX 4.2 SP2 | Production, Sandbox | Update |
| 2021-12-07 | FIX 4.2 SP2 | Production, Sandbox | Initial release |

## Market Data Gateway [](https://docs.cdp.coinbase.com/exchange/docs/fix-changelog\#market-data-gateway "Direct link to Market Data Gateway")

### Coinbase Exchange FIX 5.0 [](https://docs.cdp.coinbase.com/exchange/docs/fix-changelog\#coinbase-exchange-fix-50-1 "Direct link to Coinbase Exchange FIX 5.0")

| Date | Baseline | Environments | Notes |
| --- | --- | --- | --- |
| 2023-02-23 | FIX 5.0 SP2 | Production, Sandbox | Initial release |

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Order Entry Gateway](https://docs.cdp.coinbase.com/exchange/docs/fix-changelog#order-entry-gateway)
  - [Coinbase Exchange FIX 5.0](https://docs.cdp.coinbase.com/exchange/docs/fix-changelog#coinbase-exchange-fix-50)
  - [Coinbase Exchange FIX 4.2](https://docs.cdp.coinbase.com/exchange/docs/fix-changelog#coinbase-exchange-fix-42)
- [Market Data Gateway](https://docs.cdp.coinbase.com/exchange/docs/fix-changelog#market-data-gateway)
  - [Coinbase Exchange FIX 5.0](https://docs.cdp.coinbase.com/exchange/docs/fix-changelog#coinbase-exchange-fix-50-1)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_rest_requests.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/rest-requests#__docusaurus_skipToContent_fallback)

All requests and responses are `application/json` content type and follow typical HTTP response status codes for success and failure.

Note: Request URLs must be lowercase as URLs are [case-sensitive](https://www.w3.org/TR/WD-html40-970708/htmlweb.html).

## Errors [](https://docs.cdp.coinbase.com/exchange/docs/rest-requests\#errors "Direct link to Errors")

```codeBlockLines_p187
{
  "message": "Invalid Price"
}

```

Unless otherwise stated, errors to bad requests respond with HTTP 4xx or status codes. The body also contains a `message` parameter indicating the cause. Your language's http library should be configured to provide message bodies for non-2xx requests so that you can read the message field from the body.

### Common Error Codes [](https://docs.cdp.coinbase.com/exchange/docs/rest-requests\#common-error-codes "Direct link to Common Error Codes")

| Status Code | Reason |
| --- | --- |
| 400 | Bad Request -- Invalid request format |
| 401 | Unauthorized -- Invalid API Key |
| 403 | Forbidden -- You do not have access to the requested resource |
| 404 | Not Found |
| 500 | Internal Server Error -- We had a problem with our server |

## Success [](https://docs.cdp.coinbase.com/exchange/docs/rest-requests\#success "Direct link to Success")

A successful response is indicated by HTTP status code 200 and may contain an optional body. If the response has a body it is documented under each resource below.

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Errors](https://docs.cdp.coinbase.com/exchange/docs/rest-requests#errors)
  - [Common Error Codes](https://docs.cdp.coinbase.com/exchange/docs/rest-requests#common-error-codes)
- [Success](https://docs.cdp.coinbase.com/exchange/docs/rest-requests#success)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_websocket_channels.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#__docusaurus_skipToContent_fallback)

## Heartbeat Channel [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#heartbeat-channel "Direct link to Heartbeat Channel")

To receive heartbeat messages for specific products every second, subscribe to the `heartbeat` channel. Heartbeats include [sequence numbers](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview#sequence-numbers) and last trade IDs that can be used to verify that no messages were missed.

```codeBlockLines_p187
// Request
{
    "type": "subscribe",
    "channels": [\
        {\
            "name": "heartbeat",\
            "product_ids": [\
                "ETH-EUR"\
            ]\
        }\
    ]
}

```

```codeBlockLines_p187
// Heartbeat message
{
  "type": "heartbeat",
  "sequence": 90,
  "last_trade_id": 20,
  "product_id": "BTC-USD",
  "time": "2014-11-07T08:19:28.464459Z"
}

```

## Status Channel [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#status-channel "Direct link to Status Channel")



Order Size Properties Removed

The properties `base_max_size`, `base_min_size`, `max_market_funds` were removed on June 30. The property, `min_market_funds`, has been repurposed as the notional minimum size for limit orders. See the [Changelog](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-jun-30).

The `status` channel sends all products and currencies on a preset interval.

```codeBlockLines_p187
// Request
{
  "type": "subscribe",
  "channels": [{ "name": "status"}]
}

```

```codeBlockLines_p187
// Status Message
{
  "type": "status",
  "products": [\
    {\
      "id": "BTC-USD",\
      "base_currency": "BTC",\
      "quote_currency": "USD",\
      "base_increment": "0.00000001",\
      "quote_increment": "0.01",\
      "display_name": "BTC-USD",\
      "status": "online",\
      "status_message": null,\
      "min_market_funds": "10",\
      "post_only": false,\
      "limit_only": false,\
      "cancel_only": false,\
      "fx_stablecoin": false\
    }\
  ],
  "currencies": [\
    {\
      "id": "USD",\
      "name": "United States Dollar",\
      "display_name": "USD",\
      "min_size": "0.01000000",\
      "status": "online",\
      "status_message": null,\
      "max_precision": "0.01",\
      "convertible_to": ["USDC"],\
      "details": {},\
      "default_network": "",\
      "supported_networks": []\
    },\
    {\
      "id": "USDC",\
      "name": "USD Coin",\
      "display_name": "USDC",\
      "min_size": "0.00000100",\
      "status": "online",\
      "status_message": null,\
      "max_precision": "0.000001",\
      "convertible_to": ["USD"],\
      "details": {},\
      "default_network": "ethereum",\
      "supported_networks": [\
        {\
          "id": "ethereum",\
          "name": "Ethereum",\
          "status": "online",\
          "contract_address": "",\
          "crypto_address_link": "https://etherscan.io/token/0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48?a={{address}}",\
          "crypto_transaction_link": "https://etherscan.io/tx/0x{{txId}}",\
          "min_withdrawal_amount": 0.001,\
          "max_withdrawal_amount": 300000000,\
          "network_confirmations": 14,\
          "processing_time_seconds": 0,\
          "destination_tag_regex": ""\
        }\
      ]\
    },\
    {\
      "id": "BTC",\
      "name": "Bitcoin",\
      "display_name": "BTC",\
      "min_size":" 0.00000001",\
      "status": "online",\
      "status_message": null,\
      "max_precision": "0.00000001",\
      "convertible_to": [],\
      "details": {},\
      "default_network": "bitcoin",\
      "supported_networks": [\
        {\
          "id": "bitcoin",\
          "name": "Bitcoin",\
          "status": "online",\
          "contract_address": "",\
          "crypto_address_link": "https://live.blockcypher.com/btc/address/{{address}}",\
          "crypto_transaction_link": "https://live.blockcypher.com/btc/tx/{{txId}}",\
          "min_withdrawal_amount": 0.0001,\
          "max_withdrawal_amount": 2400,\
          "network_confirmations": 2,\
          "processing_time_seconds": 0,\
          "destination_tag_regex": ""\
        }\
      ]\
    }\
  ]
}

```

## Auction Channel [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#auction-channel "Direct link to Auction Channel")

The `auction` channel sends information about the auction while the product is in auction mode.

Auction messages provide the most recent indicative quote disseminated during the auction. Indicative quote messages are sent on an interval basis (about once a second) during the collection phase of an auction. The indicative quote includes information about the tentative price and size affiliated with the completion.

The open price and size indicate the aggregate size of all the orders eligible for crossing, along with the price used for matching all the orders as the auction enters the opening state. The best bid and ask price and size fields indicate the anticipated BBO upon entering full trading or limit only after the matching has completed.

Because indicative quotes are sent on an interval, values are not firm. The price may change in between two quote updates: (1) in between two normal quote update intervals, or (2) in between the last normal quote update interval and the final indicative quote that occurs when the book transitions from auction mode to full trading.

See [Get Product Book](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getproductbook) in the API Reference for more details on the level 1 book and products in auction mode.

```codeBlockLines_p187
// Request
{
  "type": "subscribe",
  "channels": [{ "name": "auctionfeed", "product_ids": ["LTC-USD"] }]
}

```

```codeBlockLines_p187
// Auction Message
{
    "type": "auction",
    "product_id": "LTC-USD",
    "sequence": 3262786978,
    "auction_state": "collection",
    "best_bid_price": "333.98",
    "best_bid_size": "4.39088265",
    "best_ask_price": "333.99",
    "best_ask_size": "25.23542881",
    "open_price": "333.99",
    "open_size": "0.193",
    "can_open": "yes",
    "timestamp": "2015-11-14T20:46:03.511254Z"
}

```

## Matches Channel [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#matches-channel "Direct link to Matches Channel")

If you are only interested in [match](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#match) messages, you can subscribe to the matches channel. This is useful when you're consuming the remaining feed using the [level2 channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#level2-channel).

After subscribing to the matches channel, the message `type` of the first message returned (and only the first message) is `last_match`, for example, `"type": "last_match",`



Caution

Messages can be dropped from this channel. Use the [heartbeat channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#heartbeat-channel) to track the last trade ID and fetch trades that you missed from the REST API.

## RFQ Matches Channel [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#rfq-matches-channel "Direct link to RFQ Matches Channel")

The subscription message for the Request For Quote or `rfq_matches` channel does not require the `product_ids` field; otherwise, it is the same as all other WebSocket feed channels.

- If `product_ids` is not sent, or sent as an empty string "", or sent as "ALL", the user receives `rfq_matches` for all products.
- If `product_ids` is defined, the subscriber only receives `rfq_matches` for that product. The product specified must be a valid Coinbase product ID.



Tip

Coinbase recommends submitting an empty list in the subscription request (and not specifying `product_ids`) to ensure you get all RFQ matches.



Caution

If the user has an "ALL" subscription and subscribes to a specific product, that new subscription is denied.

```codeBlockLines_p187
// Subscription Request
{
  "type": "subscriptions",
  "channels": [\
    {\
      "name": "rfq_matches",\
      "product_ids": [\
        "",\
      ],\
    },\
  ]
}

```



Caution

The subscription message uses the plural `product_ids`, whereas RFQ messages use the singular, `product_id`.

```codeBlockLines_p187
// RFQ Request
{
  "type": "rfq_match",
  "maker_order_id": "ac928c66-ca53-498f-9c13-a110027a60e8",
  "taker_order_id": "132fb6ae-456b-4654-b4e0-d681ac05cea1",
  "time": "2014-11-07T08:19:27.028459Z",
  "trade_id": 30,
  "product_id": "BTC-USD",
  "size": "5.23512",
  "price": "400.23",
  "side": "sell"
}

```



Info

See also the new [FIX Request For Quote messages](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#rfq-request-ah).

## Ticker Channel [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#ticker-channel "Direct link to Ticker Channel")

The `ticker` channel provides real-time price updates every time a match happens. It batches updates in case of cascading matches, greatly reducing bandwidth requirements.

```codeBlockLines_p187
// Request
{
    "type": "subscribe",
    "product_ids": [\
        "ETH-USD",\
        "BTC-USD"\
    ],
    "channels": ["ticker"]
}

```

```codeBlockLines_p187
// Ticker message
{
  "type": "ticker",
  "sequence": 37475248783,
  "product_id": "ETH-USD",
  "price": "1285.22",
  "open_24h": "1310.79",
  "volume_24h": "245532.79269678",
  "low_24h": "1280.52",
  "high_24h": "1313.8",
  "volume_30d": "9788783.60117027",
  "best_bid": "1285.04",
  "best_bid_size": "0.46688654",
  "best_ask": "1285.27",
  "best_ask_size": "1.56637040",
  "side": "buy",
  "time": "2022-10-19T23:28:22.061769Z",
  "trade_id": 370843401,
  "last_size": "11.4396987"
}

```

## Ticker Batch Channel [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#ticker-batch-channel "Direct link to Ticker Batch Channel")

The `ticker_batch` channel provides latest price updates **every 5000 milliseconds** (5 seconds) if there is a change. It has the same JSON message schema as the [ticker channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#ticker-channel).



Info

The `ticker_1000` channel was renamed ticker\_batch but you can use either name when subscribing.

```codeBlockLines_p187
// Request
{
    "type": "subscribe",
    "product_ids": [\
        "ETH-USD",\
        "BTC-USD"\
    ],
    "channels": ["ticker_batch"]
}

```

## Full Channel [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#full-channel "Direct link to Full Channel")

[![](https://img.shields.io/badge/Full%20Channel-Authentication%20Required-0a639a)](https://docs.cdp.coinbase.com/exchange/docs/websocket-auth)

The `full` channel provides real-time updates on orders and trades. These updates can be applied to a level3 order book snapshot to maintain an accurate and up-to-date copy of the exchange order book.

To maintain an up-to-date level3 order book:

1. Send a `subscribe` message for the product(s) of interest and the `full` channel.
2. Queue any messages received over the websocket stream.
3. Make a REST request for the order book snapshot from the REST feed.
4. Playback queued messages, discarding sequence numbers before or equal to the snapshot sequence number.
5. Apply playback messages to the snapshot as needed (see below).
6. After playback is complete, apply real-time stream messages as they arrive.



Info

All `open` and `match` messages always result in a change to the order book. Not all `done` or `change` messages result in changing the order book. These messages are sent for received orders which are not yet on the order book. Do not alter the order book for such messages, otherwise your order book will be incorrect.

The following messages are sent over the websocket stream in JSON format when subscribing to the full channel:

### Received [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#received "Direct link to Received")

_A valid order has been received and is now active._

This message is emitted for every single valid order as soon as the matching engine receives it, whether it fills immediately or not.

The `received` message does not indicate a resting order on the order book. The `received` message indicates that a new incoming order has been accepted by the matching engine for processing. Received orders may cause `match` message to follow if they are able to begin being filled (taker behavior).

[Self-trade prevention](https://docs.cdp.coinbase.com/exchange/docs/matching-engine#self-trade-prevention) may also trigger `change` messages to follow if the order size needs to be adjusted. Orders that are not fully filled or that are canceled due to self-trade prevention, result in an `open` message and become resting orders on the order book.

Market orders (indicated by the `order_type` field) may have an optional `funds` field which indicates how much quote currency is used to buy or sell. For example, a `funds` field of `100.00` for the `BTC-USD` product would indicate a purchase of up to `100.00 USD` worth of bitcoin.



Caution

`client_oid` is only available in the **authenticated** `full` channel and the [user channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#user-channel) (which is also authenticated). You can only see your own `client_oid`.

Received message for limit order:

```codeBlockLines_p187
{
  "type": "received",
  "time": "2014-11-07T08:19:27.028459Z",
  "product_id": "BTC-USD",
  "sequence": 10,
  "order_id": "d50ec984-77a8-460a-b958-66f114b0de9b",
  "size": "1.34",
  "price": "502.1",
  "side": "buy",
  "order_type": "limit",
  "client_oid": "d50ec974-76a2-454b-66f135b1ea8c"
}

```

Received message for market order:

```codeBlockLines_p187
{
  "type": "received",
  "time": "2014-11-09T08:19:27.028459Z",
  "product_id": "BTC-USD",
  "sequence": 12,
  "order_id": "dddec984-77a8-460a-b958-66f114b0de9b",
  "funds": "3000.234",
  "side": "buy",
  "order_type": "market",
  "client_oid": "d50ec974-76a2-454b-66f135b1ea8c"
}

```

### Open [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#open "Direct link to Open")

_The order is now open on the order book._

This message is only sent for orders that are not fully filled immediately. `remaining_size` indicates how much of the order is unfilled and going on the book.



Info

There is no `open` message for orders that are filled immediately. And there is no `open` message for market orders since they are filled immediately.

```codeBlockLines_p187
{
  "type": "open",
  "time": "2014-11-07T08:19:27.028459Z",
  "product_id": "BTC-USD",
  "sequence": 10,
  "order_id": "d50ec984-77a8-460a-b958-66f114b0de9b",
  "price": "200.2",
  "remaining_size": "1.00",
  "side": "sell"
}

```

### Done [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#done "Direct link to Done")

_The order is no longer on the order book._

This message is sent for all orders for which there was a received message and can result from an order being canceled or filled.

There are no more messages for an `order_id` after a done message. `remaining_size` indicates how much of the order went unfilled; this is `0` for `filled` orders.

`market` orders do not have a `remaining_size` or `price` field as they are never on the open order book at a given price.



Info

A `done` message is sent for received orders that are fully filled or canceled due to self-trade prevention. There are no `open` messages for such orders. `done` messages for orders that are not on the book should be ignored when maintaining a real-time order book.

```codeBlockLines_p187
{
  "type": "done",
  "time": "2014-11-07T08:19:27.028459Z",
  "product_id": "BTC-USD",
  "sequence": 10,
  "price": "200.2",
  "order_id": "d50ec984-77a8-460a-b958-66f114b0de9b",
  "reason": "filled", // or "canceled"
  "side": "sell",
  "remaining_size": "0"
}

```

#### Cancel Reason [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#cancel-reason "Direct link to Cancel Reason")

Done messages with `reason=canceled` (that are authenticated and that originated with you the user) return the reason in the `cancel_reason` field:

Supported cancel reasons are:

```codeBlockLines_p187
101:Time In Force
102:Self Trade Prevention
103:Admin
104:Price Bound Order Protection
105:Insufficient Funds
106:Insufficient Liquidity
107:Broker

```

### Match [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#match "Direct link to Match")

_A trade occurred between two orders._

The aggressor or `taker` order is the one executing immediately after being received and the `maker` order is a resting order on the book.

The `side` field indicates the maker order side. If the side is `sell` this indicates the maker was a sell order and the `match` is considered an up-tick. A `buy` side match is a down-tick.

```codeBlockLines_p187
{
  "type": "match",
  "trade_id": 10,
  "sequence": 50,
  "maker_order_id": "ac928c66-ca53-498f-9c13-a110027a60e8",
  "taker_order_id": "132fb6ae-456b-4654-b4e0-d681ac05cea1",
  "time": "2014-11-07T08:19:27.028459Z",
  "product_id": "BTC-USD",
  "size": "5.23512",
  "price": "400.23",
  "side": "sell"
}

```

If authenticated, and you were the taker, the message would also have the following fields:

```codeBlockLines_p187
{
  ...
  "taker_user_id": "5844eceecf7e803e259d0365",
  "user_id": "5844eceecf7e803e259d0365",
  "taker_profile_id": "765d1549-9660-4be2-97d4-fa2d65fa3352",
  "profile_id": "765d1549-9660-4be2-97d4-fa2d65fa3352",
  "taker_fee_rate": "0.005"
}

```

Similarly, if you were the maker, the message would have the following:

```codeBlockLines_p187
{
  ...
  "maker_user_id": "5f8a07f17b7a102330be40a3",
  "user_id": "5f8a07f17b7a102330be40a3",
  "maker_profile_id": "7aa6b75c-0ff1-11eb-adc1-0242ac120002",
  "profile_id": "7aa6b75c-0ff1-11eb-adc1-0242ac120002",
  "maker_fee_rate": "0.001"
}

```

### Change [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#change "Direct link to Change")

_An order has changed._

A `change` message can be the result of either a [Self-trade Prevention (STP)](https://docs.cdp.coinbase.com/exchange/docs/matching-engine#self-trade-prevention) or a Modify Order Request:



Info

Modify Order Request adds three new fields: `new_price`, `old_price`, `reason`. See also [FIX Modify Order Request (G)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#modify-order-request-g).

- A Self-trade Prevention adjusts the order size or available funds (and can only decrease).
- A Modify Order Request adjusts the order size or price.

`change` messages are sent anytime an order changes in size or price. This includes:

- Orders that are open (resting)
- Orders that are received but not yet open.
- Market orders with `funds` changed from a Self-trade Prevention control.



Info

If you are building a real-time order book, you can ignore `change` messages for received but not yet open orders.

> If you are building from a level2 book, the `side` and `price` fields to indicate whether the change message is relevant. STP Change messages for limit orders always have a price specified. STP change messages for market orders have no price ( `null`) and a decrease in order size.

Example of a change message from a Self-trade Prevention action:

> STP messages have a new `reason` field and continue to use the `price` field (not `new_price` and `old_price`).

```codeBlockLines_p187
{
  "type": "change",
  "reason":"STP",
  "time": "2014-11-07T08:19:27.028459Z",
  "sequence": 80,
  "order_id": "ac928c66-ca53-498f-9c13-a110027a60e8",
  "side": "sell",
  "product_id": "BTC-USD",
  "old_size": "12.234412",
  "new_size": "5.23512",
  "price": "400.23"
}

```

Example of a change message from a Modify Order Request:

> Modify Order messages add three new fields: `new_price`, `old_price`, `reason`.

```codeBlockLines_p187
{
  "type": "change",
  "reason":"modify_order",
  "time": "2022-06-06T22:55:43.433114Z",
  "sequence": 24753,
  "order_id": "c3f16063-77b1-408f-a743-88b7bc20cdcd",
  "side": "buy",
  "product_id": "ETH-USD",
  "old_size": "80",
  "new_size": "80",
  "old_price": "7",
  "new_price": "6"
}

```

### Activate [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#activate "Direct link to Activate")

_An activate message is sent when a stop order is placed._

When the stop is triggered the order is placed and goes through the [order lifecycle](https://docs.cdp.coinbase.com/exchange/docs/matching-engine#order-lifecycle).

```codeBlockLines_p187
{
  "type": "activate",
  "product_id": "test-product",
  "timestamp": "1483736448.299000",
  "user_id": "12",
  "profile_id": "30000727-d308-cf50-7b1c-c06deb1934fc",
  "order_id": "7b52009b-64fd-0a2a-49e6-d8a939753077",
  "stop_type": "entry",
  "side": "buy",
  "stop_price": "80",
  "size": "2",
  "funds": "50",
  "private": true
}

```

## User Channel [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#user-channel "Direct link to User Channel")

[![](https://img.shields.io/badge/User%20Channel-Authentication%20Required-0a639a)](https://docs.cdp.coinbase.com/exchange/docs/websocket-auth)

The `user` channel is a version of the [full channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#full-channel) and only contains messages that include the authenticated user. Consequently, you need to be [authenticated](https://docs.cdp.coinbase.com/exchange/docs/websocket-auth#authentication) to receive any messages.



Caution

Modify Order Request is a new feature that affects the [Full Channel, Change](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#change) message, and by extension, the User channel.

## Level2 Channel [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#level2-channel "Direct link to Level2 Channel")

[![](https://img.shields.io/badge/Level2%20Channel-Authentication%20Required-0a639a)](https://docs.cdp.coinbase.com/exchange/docs/websocket-auth)

The `level2` channel guarantees delivery of all updates and is the easiest way to keep a snapshot of the order book. This channel also reduces the overhead required when consuming the [full channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#full-channel).

```codeBlockLines_p187
// Request
{
    "type": "subscribe",
    "channels": ["level2"],
    "product_ids": [\
        "ETH-USD",\
        "BTC-USD"\
    ]
}

```



Tip

The [Level2 Batch Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#level2-batch-channel) does not require authentication and delivers Level 2 data in batches every 50 milliseconds.

The `level2` channel sends a message with the type `snapshot` and the corresponding `product_id`. The properties `bids` and `asks` are arrays of `[price, size]` tuples and represent the entire order book.

```codeBlockLines_p187
{
  "type": "snapshot",
  "product_id": "BTC-USD",
  "bids": [["10101.10", "0.45054140"]],
  "asks": [["10102.55", "0.57753524"]]
}

```

Subsequent updates have the type `l2update`. The `changes` property of `l2update` s is an array with `[side, price, size]` tuples. The `time` property of `l2update` is the time of the event as recorded by our trading engine.

##### Single `changes` Array [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#single-changes-array "Direct link to single-changes-array")

```codeBlockLines_p187
{
  "type": "l2update",
  "product_id": "BTC-USD",
  "time": "2019-08-14T20:42:27.265Z",
  "changes": [\
    [\
      "buy",\
      "10101.80000000",\
      "0.162567"\
    ]\
  ]
}

```

##### Multiple `changes` Arrays [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#multiple-changes-arrays "Direct link to multiple-changes-arrays")

```codeBlockLines_p187
{
  "type": "l2update",
  "product_id": "BTC-USD",
  "changes": [\
    [\
      "buy",\
      "22356.270000",\
      "0.00000000"\
    ],\
    [\
      "buy",\
      "22356.300000",\
      "1.00000000"\
    ]\
  ],
  "time": "2022-08-04T15:25:05.010758Z"
}

```



Info

The `size` property is the updated size at the price level, not a delta. A size of `"0"` indicates the price level can be removed.

## Level2 Batch Channel [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#level2-batch-channel "Direct link to Level2 Batch Channel")

The `level2_batch` channel sends batches of `level2` messages **every 50 milliseconds** (0.05 seconds). It has the same JSON message schema as the [`level2` channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#level2-channel). The time field correlates to the most recent message in the batch.



Tip

The `level2_batch` channel lets you receive [`level2`](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#level2-channel) data _without authenticating_. You get the same benefits while minimizing traffic.

```codeBlockLines_p187
// Request
{
    "type": "subscribe",
    "product_ids": [\
        "ETH-USD",\
        "BTC-USD"\
    ],
    "channels": ["level2_batch"]
}

```



Info

The `level2_50` channel was renamed `level2_batch` but you can use either when subscribing.

## Level3 Channel [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#level3-channel "Direct link to Level3 Channel")

[![](https://img.shields.io/badge/Level3%20Channel-Authentication%20Required-0a639a)](https://docs.cdp.coinbase.com/exchange/docs/websocket-auth)

The `level3` channel is a compact version of the Full channel. It conveys all of the same data in a compact message structure that requires less bandwidth with potentially more efficient client side parsing.

```codeBlockLines_p187
// Subscribe request
{
    "type": "subscribe",
    "channels": ["level3"],
    "product_ids": [\
        "ETH-USD",\
        "BTC-USD"\
    ]
}

```

### L3 Schema [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#l3-schema "Direct link to L3 Schema")

On subscribe, the first response returns a level3 schema with the structure for each message type. The schema is not repeated.



Level3 Message Structures

You should process level3 message structures before parsing the subsequent messages. While the schema should not change, it may.

**Expand to view the full level3 schema**

```codeBlockLines_p187
{
  "type": "level3",
  "schema": {
    "change": [\
      "type",\
      "product_id",\
      "sequence",\
      "order_id",\
      "price",\
      "size",\
      "time"\
    ],
    "done": [\
      "type",\
      "product_id",\
      "sequence",\
      "order_id",\
      "time"\
    ],
    "match": [\
      "type",\
      "product_id",\
      "sequence",\
      "maker_order_id",\
      "taker_order_id",\
      "price",\
      "size",\
      "time"\
    ],
    "noop": [\
      "type",\
      "product_id",\
      "sequence",\
      "time"\
    ],
    "open": [\
      "type",\
      "product_id",\
      "sequence",\
      "order_id",\
      "side",\
      "price",\
      "size",\
      "time"\
    ]
  }
}

```

Subsequent messages for each type pack the data into an array with a structure as defined in the initial response, for example:

```codeBlockLines_p187
[\
  "open",\
  "BTC-USD",\
  "57560479456",\
  "12aca6e0-7400-418a-9e59-c0020a3bf8cc",\
  "buy",\
  "27268.09",\
  "0.02",\
  "2023-03-28T23:24:03.185394Z"\
]

```

## Balance Channel [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#balance-channel "Direct link to Balance Channel")

[![](https://img.shields.io/badge/Balance%20Channel-Authentication%20Required-0a639a)](https://docs.cdp.coinbase.com/exchange/docs/websocket-auth)

The `balance` channel tracks account balance updates, which is useful for checking the holds and available balance on your account. It does _not_ track every update. Authentication is required.

#### Fields [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#fields "Direct link to Fields")

A response from the channel includes the following fields:

```codeBlockLines_p187
{
  "type": "balance",
  "account_id": "d50ec984-77a8-460a-b958-66f114b0de9b",
  "currency": "USD",
  "holds": "1000.23",                      // funds locked in account
  "available": "102030.99",                // balance available for trading
  "updated": "2023-10-10T20:42:27.265Z",   // when last balance change is observed
  "timestamp": "2023-10-10T20:42:29.265Z"  // when message is sent from websocket
}

```

#### Subscribe [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#subscribe "Direct link to Subscribe")

Clients can subscribe to this channel using the following subscribe messages:

##### Example 1 [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#example-1 "Direct link to Example 1")

```codeBlockLines_p187
{
  "type": "subscribe",
  "channels": [\
    {\
      "name": "balance",\
      "account_ids": [\
        "d50ec984-77a8-460a-b958-66f114b0de9b",\
        "d50ec984-77a8-460a-b958-66f114b0de9a"\
      ]\
    }\
  ]
}

```

##### Example 2 [](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels\#example-2 "Direct link to Example 2")

```codeBlockLines_p187
{
  "type": "subscribe",
  "channels": [\
    "balance"\
  ],
  "account_ids": [\
    "d50ec984-77a8-460a-b958-66f114b0de9b",\
    "d50ec984-77a8-460a-b958-66f114b0de9a"\
  ]
}

```

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Heartbeat Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#heartbeat-channel)
- [Status Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#status-channel)
- [Auction Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#auction-channel)
- [Matches Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#matches-channel)
- [RFQ Matches Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#rfq-matches-channel)
- [Ticker Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#ticker-channel)
- [Ticker Batch Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#ticker-batch-channel)
- [Full Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#full-channel)
  - [Received](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#received)
  - [Open](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#open)
  - [Done](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#done)
  - [Match](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#match)
  - [Change](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#change)
  - [Activate](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#activate)
- [User Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#user-channel)
- [Level2 Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#level2-channel)
- [Level2 Batch Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#level2-batch-channel)
- [Level3 Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#level3-channel)
  - [L3 Schema](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#l3-schema)
- [Balance Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#balance-channel)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_getting_started.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/getting-started#__docusaurus_skipToContent_fallback)

This quickstart walks through creating an API key, setting up the Exchange Go SDK, and making your first few REST API calls.

## Initial Setup [](https://docs.cdp.coinbase.com/exchange/docs/getting-started\#initial-setup "Direct link to Initial Setup")

1. **Create a Coinbase Exchange Account:** Sign up at [Coinbase Exchange](https://exchange.coinbase.com/).
2. **Generate an API Key:** From the web UI, navigate to [API](https://exchange.coinbase.com/apikeys).
3. **Authenticate:** Ensure you authenticate all API requests. Detailed guidance is available at [API Authentication](https://docs.cdp.coinbase.com/exchange/docs/rest-auth).



REST API URL

`https://api.exchange.coinbase.com`

## Using the Exchange Go SDK [](https://docs.cdp.coinbase.com/exchange/docs/getting-started\#using-the-exchange-go-sdk "Direct link to Using the Exchange Go SDK")

### Setting up the SDK [](https://docs.cdp.coinbase.com/exchange/docs/getting-started\#setting-up-the-sdk "Direct link to Setting up the SDK")

First, initialize a new Go module, install the Exchange Go SDK, and tidy dependencies. Run the following commands in your project directory, replacing example.com/test with your desired project path:

```codeBlockLines_p187
go mod init example.com/test
go get github.com/coinbase-samples/exchange-sdk-go
go mod tidy
go build

```

Next, initialize the `Credentials` struct and create a new client. The Credentials struct is JSON enabled. Ensure that Exchange API credentials are stored in a secure manner.

```codeBlockLines_p187
credentials, err := credentials.ReadEnvCredentials("EXCHANGE_CREDENTIALS")
if err != nil {
    panic(fmt.Sprintf("unable to read exchange credentials: %v", err))
}

httpClient, err := core.DefaultHttpClient()
if err != nil {
    panic(fmt.Sprintf("unable to load default http client: %v", err))
}

client := client.NewRestClient(credentials, httpClient)

```

There are convenience functions to read the credentials as an environment variable (credentials.ReadEnvCredentials) and to deserialize the JSON structure (credentials.UnmarshalCredentials) if pulled from a different source.

To set up your credentials, add the `EXCHANGE_CREDENTIALS` environment variable to your `~/.zshrc` file:

```codeBlockLines_p187
export EXCHANGE_CREDENTIALS='{
    "apiKey":"YOUR_API_KEY",
    "passphrase":"YOUR_PASSPHRASE",
    "signingKey":"YOUR_SIGNING_KEY"
}'

```

After adding this line, run source ~/.zshrc to load the environment variable into your current shell session.

## Making your first API call [](https://docs.cdp.coinbase.com/exchange/docs/getting-started\#making-your-first-api-call "Direct link to Making your first API call")

After initializing the client, you need to set up the appropriate service to access specific API endpoints. Specific examples are provided below.

### Listing Accounts [](https://docs.cdp.coinbase.com/exchange/docs/getting-started\#listing-accounts "Direct link to Listing Accounts")

Account IDs are needed in order to track asset-level events, e.g. transfers and ledger. To list all accounts, initialize the accounts service, pass in the request object, check for an error, and, if nil, process the response.

```codeBlockLines_p187
func main() {
    credentials, err := credentials.ReadEnvCredentials("EXCHANGE_CREDENTIALS")
    if err != nil {
        panic(fmt.Sprintf("unable to read exchange credentials: %v", err))
    }

    httpClient, err := core.DefaultHttpClient()
    if err != nil {
        panic(fmt.Sprintf("unable to load default http client: %v", err))
    }

    client := client.NewRestClient(credentials, httpClient)

    accountsSvc := accounts.NewAccountsService(client)
    request := &accounts.ListAccountsRequest{}

    response, err := accountsSvc.ListAccounts(context.Background(), request)
    if err != nil {
        panic(fmt.Sprintf("unable to list accounts: %v", err))
    }

    jsonResponse, err := json.MarshalIndent(response, "", "  ")
    if err != nil {
        panic(fmt.Sprintf("error marshaling response to JSON: %v", err))
    }
    fmt.Println(string(jsonResponse))
}

```

### Get Account Transfers [](https://docs.cdp.coinbase.com/exchange/docs/getting-started\#get-account-transfers "Direct link to Get Account Transfers")

You can use account IDs to track historical transfers. To get a specific account's transfer history, initialize the accounts service if you haven't already, pass in the request object with account ID, check for an error, and, if nil, process the response.

```codeBlockLines_p187
func main() {
    credentials, err := credentials.ReadEnvCredentials("EXCHANGE_CREDENTIALS")
    if err != nil {
        panic(fmt.Sprintf("unable to read exchange credentials: %v", err))
    }

    httpClient, err := core.DefaultHttpClient()
    if err != nil {
        panic(fmt.Sprintf("unable to load default http client: %v", err))
    }

    client := client.NewRestClient(credentials, httpClient)

    accountsSvc := accounts.NewAccountsService(client)
    request := &accounts.GetAccountTransfersRequest{
        AccountId: "account_id_here",
    }

    response, err := accountsSvc.GetAccountTransfers(context.Background(), request)
    if err != nil {
        panic(fmt.Sprintf("unable to get account transfers: %v", err))
    }

    jsonResponse, err := json.MarshalIndent(response, "", "  ")
    if err != nil {
        panic(fmt.Sprintf("error marshaling response to JSON: %v", err))
    }
    fmt.Println(string(jsonResponse))
}

```

### Listing Profiles [](https://docs.cdp.coinbase.com/exchange/docs/getting-started\#listing-profiles "Direct link to Listing Profiles")

Certain requests require that you know your Profile ID. To list all profile IDs associated with your Exchange account, initialize the profiles service, pass in the request object, check for an error, and, if nil, process the response.

```codeBlockLines_p187
func main() {
    credentials, err := credentials.ReadEnvCredentials("EXCHANGE_CREDENTIALS")
    if err != nil {
        panic(fmt.Sprintf("unable to read exchange credentials: %v", err))
    }

    httpClient, err := core.DefaultHttpClient()
    if err != nil {
        panic(fmt.Sprintf("unable to load default http client: %v", err))
    }

    client := client.NewRestClient(credentials, httpClient)

    profilesSvc := profiles.NewProfilesService(client)
    request := &profiles.ListProfilesRequest{}

    response, err := profilesSvc.ListProfiles(context.Background(), request)
    if err != nil {
        panic(fmt.Sprintf("unable to list profiles: %v", err))
    }

    jsonResponse, err := json.MarshalIndent(response, "", "  ")
    if err != nil {
        panic(fmt.Sprintf("error marshaling response to JSON: %v", err))
    }
    fmt.Println(string(jsonResponse))
}

```

### Get Product Details [](https://docs.cdp.coinbase.com/exchange/docs/getting-started\#get-product-details "Direct link to Get Product Details")

To get product details, initialize the products service, pass in the request object with the Product ID (e.g. `BTC-USD`) you want data for, check for an error, and if nil, process the response.

```codeBlockLines_p187
func main() {
    credentials, err := credentials.ReadEnvCredentials("EXCHANGE_CREDENTIALS")
    if err != nil {
        panic(fmt.Sprintf("unable to read exchange credentials: %v", err))
    }

    httpClient, err := core.DefaultHttpClient()
    if err != nil {
        panic(fmt.Sprintf("unable to load default http client: %v", err))
    }

    client := client.NewRestClient(credentials, httpClient)

    productsSvc := products.NewProductsService(client)

    request := &products.GetProductRequest{
        ProductId: "BTC-USD",
    }

    response, err := productsSvc.GetProduct(context.Background(), request)
    if err != nil {
        panic(fmt.Sprintf("unable to get product: %v", err))
    }

    jsonResponse, err := json.MarshalIndent(response, "", "  ")
    if err != nil {
        panic(fmt.Sprintf("error marshaling response to JSON: %v", err))
    }
    fmt.Println(string(jsonResponse))
}

```

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Initial Setup](https://docs.cdp.coinbase.com/exchange/docs/getting-started#initial-setup)
- [Using the Exchange Go SDK](https://docs.cdp.coinbase.com/exchange/docs/getting-started#using-the-exchange-go-sdk)
  - [Setting up the SDK](https://docs.cdp.coinbase.com/exchange/docs/getting-started#setting-up-the-sdk)
- [Making your first API call](https://docs.cdp.coinbase.com/exchange/docs/getting-started#making-your-first-api-call)
  - [Listing Accounts](https://docs.cdp.coinbase.com/exchange/docs/getting-started#listing-accounts)
  - [Get Account Transfers](https://docs.cdp.coinbase.com/exchange/docs/getting-started#get-account-transfers)
  - [Listing Profiles](https://docs.cdp.coinbase.com/exchange/docs/getting-started#listing-profiles)
  - [Get Product Details](https://docs.cdp.coinbase.com/exchange/docs/getting-started#get-product-details)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_matching_engine.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/matching-engine#__docusaurus_skipToContent_fallback)

Coinbase Exchange operates a continuous first-come, first-serve order book. Orders are executed in price-time priority as received by the matching engine.

## Self-Trade Prevention [](https://docs.cdp.coinbase.com/exchange/docs/matching-engine\#self-trade-prevention "Direct link to Self-Trade Prevention")

Self-trading is not allowed on Coinbase Exchange. When two orders from the same user cross, they do not fill one another.



Caution

The STP instruction on the taker order (latest order) takes precedence over the older/resting order.

You can define your self-trade prevention behavior when [placing an order](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postorders#self-trade-prevention) with the STP flag:

| Self-Trade Prevention Option | STP Flag | Description |
| --- | --- | --- |
| Decrement & cancel (default) | `dc` | Cancel smaller order and decrement larger order by the smaller size. If the same size, cancel both. |
| Cancel oldest | `co` | Cancel older (resting) order in full. Continue to execute the newer taking order. |
| Cancel newest | `cn` | Cancel newer (taking) order in full. Let the old resting order remain on the order book. |
| Cancel both | `cb` | Cancel both orders immediately. |

## Market Orders [](https://docs.cdp.coinbase.com/exchange/docs/matching-engine\#market-orders "Direct link to Market Orders")

When a `market` order using decrement and cancel ( `dc` ) self-trade prevention encounters an open limit order, the behavior depends on which fields were specified for the market order.

- If `funds` and `size` are specified:
  - For a market buy order, size is decremented internally within the matching engine and funds remain unchanged. The intent is to offset your target size without limiting your buying power.
- If `funds` is specified (and not `size`):
  - For a market buy order, funds are decremented.
  - For a market sell order, size is decremented when encountering existing limit orders.

## Price Improvement [](https://docs.cdp.coinbase.com/exchange/docs/matching-engine\#price-improvement "Direct link to Price Improvement")

Orders are matched against existing order book orders at the price of the order _on the book_, not at the price of the taker order.

**Example**

User A places a buy order for 1 BTC at 100 USD. Then User B places a sell order for 1 BTC at 80 USD. The result is that the trade occurs at 100 USD because User A's order was first to the trading engine and User A has price priority.

## Order Lifecycle [](https://docs.cdp.coinbase.com/exchange/docs/matching-engine\#order-lifecycle "Direct link to Order Lifecycle")

| Order State | Description |
| --- | --- |
| `received` | Valid orders that are sent to the matching engine and **confirmed** immediately. |
| `open` | Any part of the order **not filled** immediately. Orders stay open until canceled or filled by new orders. |
| `done` | An full order **executed** against another order immediately. A partial order filled or canceled (and no longer eligible for matching) |

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Self-Trade Prevention](https://docs.cdp.coinbase.com/exchange/docs/matching-engine#self-trade-prevention)
- [Market Orders](https://docs.cdp.coinbase.com/exchange/docs/matching-engine#market-orders)
- [Price Improvement](https://docs.cdp.coinbase.com/exchange/docs/matching-engine#price-improvement)
- [Order Lifecycle](https://docs.cdp.coinbase.com/exchange/docs/matching-engine#order-lifecycle)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_runbook.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/runbook#__docusaurus_skipToContent_fallback)

## Deployment [](https://docs.cdp.coinbase.com/exchange/docs/runbook\#deployment "Direct link to Deployment")

The deployment schedules for different components vary and may change without notice.

| API | Schedule |
| --- | --- |
| FIX | Monday, Thursday at 2PM ET |
| WebSocket | Monday, Wednesday, Thursday at 2PM ET |
| REST | Monday, Wednesday, Thursday at 2PM ET |

## Production URLs [](https://docs.cdp.coinbase.com/exchange/docs/runbook\#production-urls "Direct link to Production URLs")

Use the following URLs to connect to Coinbase Exchange production APIs. See [Sandbox URLs](https://docs.cdp.coinbase.com/exchange/docs/sandbox) for testing.

| API | URL |
| --- | --- |
| REST API | `https://api.exchange.coinbase.com ` |
| Websocket Feed | `wss://ws-feed.exchange.coinbase.com ` |
| Websocket Direct Feed | `wss://ws-direct.exchange.coinbase.com ` |
| FIX API - Order Entry 4.2 | `tcp+ssl://fix.exchange.coinbase.com:4198 ` |
| FIX API - Order Entry 5.0 SP2 | `tcp+ssl://fix-ord.exchange.coinbase.com:6121 ` |
| FIX API - Market Data 5.0 SP2 | `tcp+ssl://fix-md.exchange.coinbase.com:6121 ` |

## Availability Zones [](https://docs.cdp.coinbase.com/exchange/docs/runbook\#availability-zones "Direct link to Availability Zones")

The infrastructure for the US Spot Exchange is hosted in **US-EAST-1 (AWS)** within multiple availability zones.



Caution

The following information is subject to change without notification, and there is no guarantee that it will remain static over time.

| Product | Availability Zone ID |
| --- | --- |
| FIX Order Gateways | use1-az4 |
| Order Entry Gateway | use1-az4 |
| Trade Engine | use1-az4 |
| Web Socket Market Data | use1-az4 |
| FIX Market Data | use1-az4 |

## System Components [](https://docs.cdp.coinbase.com/exchange/docs/runbook\#system-components "Direct link to System Components")

### REST Entry Gateways [](https://docs.cdp.coinbase.com/exchange/docs/runbook\#rest-entry-gateways "Direct link to REST Entry Gateways")

- Requests are routed through Cloudflare.
- Requests are processed on a FIFO basis with no queuing.
- REST requires additional authentication because it's stateless (as opposed to FIX order gateways, which authenticate during login).

### FIX Order Gateways [](https://docs.cdp.coinbase.com/exchange/docs/runbook\#fix-order-gateways "Direct link to FIX Order Gateways")

- Each instance contains a per-user product based queue.
- Each per-user product-based queue can hold a maximum of 50 queued requests before requests are rejected.
- Each per-user product-based queue is processed on a FIFO basis.

### Order Entry Gateway (Risk System) [](https://docs.cdp.coinbase.com/exchange/docs/runbook\#order-entry-gateway-risk-system "Direct link to Order Entry Gateway (Risk System)")

- Each instance processes requests from FIX Order Gateways and REST in real time with no queuing.
- System performs real-time risk checks and account collateralization.

### Trade Engine [](https://docs.cdp.coinbase.com/exchange/docs/runbook\#trade-engine "Direct link to Trade Engine")

- Clustered service that guarantees FIFO sequencing at a product level.
- Processes all requests from Order Entry Gateway.
- Publishes market data to WebSocket / FIX Market Data.

### Market Data (Websocket & FIX) [](https://docs.cdp.coinbase.com/exchange/docs/runbook\#market-data-websocket--fix "Direct link to Market Data (Websocket & FIX)")

- Each instance can process all market data requests across all products.
- Messages are distributed to customers randomly, and there is no intended benefit to being “first to subscribe”.

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Deployment](https://docs.cdp.coinbase.com/exchange/docs/runbook#deployment)
- [Production URLs](https://docs.cdp.coinbase.com/exchange/docs/runbook#production-urls)
- [Availability Zones](https://docs.cdp.coinbase.com/exchange/docs/runbook#availability-zones)
- [System Components](https://docs.cdp.coinbase.com/exchange/docs/runbook#system-components)
  - [REST Entry Gateways](https://docs.cdp.coinbase.com/exchange/docs/runbook#rest-entry-gateways)
  - [FIX Order Gateways](https://docs.cdp.coinbase.com/exchange/docs/runbook#fix-order-gateways)
  - [Order Entry Gateway (Risk System)](https://docs.cdp.coinbase.com/exchange/docs/runbook#order-entry-gateway-risk-system)
  - [Trade Engine](https://docs.cdp.coinbase.com/exchange/docs/runbook#trade-engine)
  - [Market Data (Websocket & FIX)](https://docs.cdp.coinbase.com/exchange/docs/runbook#market-data-websocket--fix)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_websocket_rate_limits.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/websocket-rate-limits#__docusaurus_skipToContent_fallback)

Coinbase Exchange real-time WebSocket market data updates provide fast insight into order flow and trades. This means that you are responsible for reading the message stream and using the message relevant for your needs—this can include building real-time order books or tracking real-time trades.

The WebSocket API has two forms of rate limits—subscription limits and inbound message limits highlighted below. See also [Market Data Connections](https://help.coinbase.com/en/exchange/managing-my-account/market-data-connections) in the Help docs.

## Limits [](https://docs.cdp.coinbase.com/exchange/docs/websocket-rate-limits\#limits "Direct link to Limits")

### Subscription Limits [](https://docs.cdp.coinbase.com/exchange/docs/websocket-rate-limits\#subscription-limits "Direct link to Subscription Limits")

- Exchange accounts are limited to **10** WebSocket subscriptions on a per product, per channel basis. Users can purchase higher subscription limits if desired. Navigate to [Coinbase Developer Platform](https://portal.cdp.coinbase.com/products/exchange) to change your subscription.
- If a user attempts to exceed **10** subscriptions per product, per channel, and is not a member of a paid subscription tier, the new subscription will be rejected.

### What is a subscription? [](https://docs.cdp.coinbase.com/exchange/docs/websocket-rate-limits\#what-is-a-subscription "Direct link to What is a subscription?")

- A subscription is defined on a per product, per channel basis.
- Below is an example of a total of 4 subscriptions for BTC-USD full
  - User123: BTC-USD Full Channel (unique)
  - User123: BTC-USD Full Channel (duplicate)
  - User123: BTC-USD Full Channel (duplicate)
  - User123: BTC-USD Full Channel (duplicate)
  - User123: BTC-USD Level 2 (unique)
  - User123: BTC-USD Level 3 (unique)
- In this case, User123 has 6 remaining subscriptions to BTC-USD full channel, and 9 remaining subscriptions to BTC-USD Level 2 and Level 3 channels.

### Inbound Message Limits [](https://docs.cdp.coinbase.com/exchange/docs/websocket-rate-limits\#inbound-message-limits "Direct link to Inbound Message Limits")

- All WebSocket inbound messages are subject to a rate limit of **10** RPS / **1000** burst RPS.

### What is an inbound message limit? [](https://docs.cdp.coinbase.com/exchange/docs/websocket-rate-limits\#what-is-an-inbound-message-limit "Direct link to What is an inbound message limit?")

- When a user sends any message (subscribing to a WebSocket channel, unsubscribing to a WebSocket channel, etc.) it is counted towards their inbound message limit.
- Users can subscribe/unsubscribe to multiple channels and products within a single inbound message.
- Limits are enforced using a **lazy-fill token bucket** implementation. More information, including examples, can be found at [How Rate Limits Work](https://docs.cdp.coinbase.com/exchange/docs/rate-limits#how-rate-limits-work).

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Limits](https://docs.cdp.coinbase.com/exchange/docs/websocket-rate-limits#limits)
  - [Subscription Limits](https://docs.cdp.coinbase.com/exchange/docs/websocket-rate-limits#subscription-limits)
  - [What is a subscription?](https://docs.cdp.coinbase.com/exchange/docs/websocket-rate-limits#what-is-a-subscription)
  - [Inbound Message Limits](https://docs.cdp.coinbase.com/exchange/docs/websocket-rate-limits#inbound-message-limits)
  - [What is an inbound message limit?](https://docs.cdp.coinbase.com/exchange/docs/websocket-rate-limits#what-is-an-inbound-message-limit)

[docs_cdp_coinbase_com_exchange_docs_changelog.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/changelog#__docusaurus_skipToContent_fallback)

These release notes list changes to Coinbase Exchange.

### 2025-MAY-09 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2025-may-09 "Direct link to 2025-MAY-09")

We will be temporarily removing support for the [Iceberg Order Type](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-iceberg) on 05/27/25. This applies to both FIX4.2 and FIX5.
We continue to monitor client needs and hope to reintroduce an enhanced version of this order type with broader support in the future.

### 2025-APR-22 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2025-apr-22 "Direct link to 2025-APR-22")

Added functionality for users to redeem CBETH to ETH via Web & API:

- [Create a new redeem](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postwrappedassetredeem)

`POST https://api.exchange.coinbase.com/wrapped-assets/redeem`

- [List all redeems](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_listwrappedassetredeems)

`GET https://api.exchange.coinbase.com/wrapped-assets/redeem`

- [Get a single redeem](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getwrappedassetredeem)

`GET https://api.exchange.coinbase.com/wrapped-assets/redeem/{redeem_id}`


### 2025-JAN-28 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2025-jan-28 "Direct link to 2025-JAN-28")

Rolled out a restriction requiring the ClOrdID of any new order or modification request to not match the ClOrdID of any open orders. This is applicable to both FIX4.2 and FIX5.

### 2025-JAN-01 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2025-jan-01 "Direct link to 2025-JAN-01")

We have deprecated the Coinbase Price Oracle API.

### 2024-DEC-2 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2024-dec-2 "Direct link to 2024-DEC-2")

A new [Get All Conversions](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getallconversions)
endpoint has been added to the REST API. This endpoint returns all conversions associated with the profile tied to the API key used to make the request.

`GET https://api.exchange.coinbase.com/conversions`

### 2024-OCT-16 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2024-oct-16 "Direct link to 2024-OCT-16")

FIX Market Data Snapshot Enabled Gateway deprecation has been postponed until further notice.

### 2024-SEP-19 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2024-sep-19 "Direct link to 2024-SEP-19")

`trade_id` has been added to the [RFQ Matches Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#rfq-matches-channel).

### 2024-SEP-11 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2024-sep-11 "Direct link to 2024-SEP-11")

The Pro API ( [https://api.pro.coinbase.com](https://api.pro.coinbase.com/)) has been deprecated. For REST API access, leverage the [Exchange API](https://docs.cdp.coinbase.com/exchange/reference)

### 2024-AUG-21 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2024-aug-21 "Direct link to 2024-AUG-21")

We released Snapshot Disabled [FIX Market Data Gateway](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data) to production. It is based on the [FIX 5.0 SP2 specification](https://www.onixs.biz/fix-dictionary/5.0.sp2/index.html) and will only provide incremental messages.



Info

- Sandbox Snapshot Disabled Gateway: `tcp+ssl://fix-md.sandbox.exchange.coinbase.com:6122 `
- Production Snapshot Disabled Gateway: `tcp+ssl://fix-md.exchange.coinbase.com:6122 `

### 2024-AUG-01 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2024-aug-01 "Direct link to 2024-AUG-01")

- Modified permission requirement for [Update settlement preference](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postuserlevelsettlementpreferences) to `MANAGE`
- Updated WebSocket subscription and rate limits. Users can now purchase additional subscriptions to facilitate their needs. See [WebSocket Rate Limits](https://docs.cdp.coinbase.com/exchange/docs/websocket-rate-limits/).

### 2024-JUN-27 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2024-jun-27 "Direct link to 2024-JUN-27")

Added support for [Limit With Funds orders](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-lwf) in FIX 5.0, FIX 4.2, and REST.

### 2024-APR-22 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2024-apr-22 "Direct link to 2024-APR-22")

Added the following rule for the [Get a single account's ledger](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getaccountledger) API—if neither `start_date` nor `end_date` is set, the endpoint returns ledger activity for the past 1 day only.

### 2024-APR-02 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2024-apr-02 "Direct link to 2024-APR-02")

- Added new endpoint, [Get user trading volumes](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getusertradingvolumes) to list a single user's aggregated and individual trading volumes.

`GET https://api.exchange.coinbase.com/users/{user_id}/trading-volumes`

### 2024-MAR-21 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2024-mar-21 "Direct link to 2024-MAR-21")

Added support for [Take Profit Stop Loss orders](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-tpsl) in FIX 5.0 and FIX 4.2.

### 2024-MAR-19 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2024-mar-19 "Direct link to 2024-MAR-19")

Added new Loan Interest endpoints:

- [Get all interest summaries](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getinterestsummary)
- [Get a single loan's interest rate history](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getinteresthistory)
- [Get a single loan's interest charges](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getinterestcharges)

### 2024-MAR-18 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2024-mar-18 "Direct link to 2024-MAR-18")

Removed all properties, except `exchange_withdraw`, from [Get user exchange limits](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getuserexchangelimits):

```codeBlockLines_p187
buy
sell
ach
ach_no_balance
credit_debit_card
secure3d_buy
paypal_buy
paypal_withdrawal
ideal_deposit
sofort_deposit
instant_ach_withdrawal

```

### 2024-MAR-06 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2024-mar-06 "Direct link to 2024-MAR-06")

Added the following response properties to [Get product stats](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getproductstats):

- `rfq_volume_24hour`
- `conversions_volume_24hour`
- `rfq_volume_30day`
- `conversions_volume_30day`

```codeBlockLines_p187
// Example
"apiProductStats": {
  "type": "object",
  "example": {
    "open": "5414.18000000",
    "high": "6441.37000000",
    "low": "5261.69000000",
    "volume": "53687.76764233",
    "last": "6250.02000000",
    "volume_30day": "786763.72930864",
    "rfq_volume_24hour": "78.23",
    "conversions_volume_24hour": "0.000000",
    "rfq_volume_30day": "0.000000",
    "conversions_volume_30day": "0.000000"
  }
}

```

### 2024-FEB-27 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2024-feb-27 "Direct link to 2024-FEB-27")

- Added FIX 5.0 support for Iceberg Orders (in addition to FIX 4.2).
- Moved documentation for [Iceberg Orders](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-iceberg) to a dedicated page.

### 2024-FEB-23 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2024-feb-23 "Direct link to 2024-FEB-23")

Added support for OrderMassCancelRequest (by **Trading Session** only):

- [OrderMassCancelRequest (35=q)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#ordermasscancelrequest-35q): Sent by customer to Coinbase to request mass cancellation of all orders on a FIX session previously submitted by customer.

- [OrderMassCancelReport (35=r)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#ordermasscancelreport-35r): Sent by Coinbase to the customer as an acknowledgement of an Order Mass Cancel Request for processing or a rejection of the request.


### 2024-FEB-07 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2024-feb-07 "Direct link to 2024-FEB-07")

- Added `fee_amount` to existing endpoint, [/conversions](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postconversion) response.

- Added new endpoint, [/conversions/fees/](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getconversionfees) to help monitor current L30d net conversion volume and calculate expected fees.


### 2024-FEB-05 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2024-feb-05 "Direct link to 2024-FEB-05")

Added the `display_name` to:

- The top level of the [Account](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getaccounts) and [Currency](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getcurrencies) response objects (but did not remove from the lower level `details` object as originally planned).
- The WebSocket [Status Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#status-channel) `currencies` object.

```codeBlockLines_p187
{
    "id": "BTC",
    "name": "Bitcoin",
    "details":

    {
        "type": "crypto",
        "symbol": null,
        ...
        "display_name": null
    },
    "default_network": "bitcoin",
    "supported_networks":

        [{...}],
    "display_name": "BTC"  // UI only
}

```

### 2024-JAN-24 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2024-jan-24 "Direct link to 2024-JAN-24")

Added `account_ids` to the WebSocket [subscriptions](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview#subscriptions-message) message, in support of the [Balance Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#balance-channel). Users not subscribing to this channel can ignore this field.

```codeBlockLines_p187
{
   "type": "subscriptions",
   "channels": [\
      {\
         "name": "balance",\
         "product_ids": null,\
         "account_ids": [\
            "826863ab-ce92-47a0-86f6-30b4776190c1"\
         ]\
      }\
   ]
}

```

### 2024-JAN-16 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2024-jan-16 "Direct link to 2024-JAN-16")

Added a new WebSocket [Balance Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#balance-channel) to track account balance updates. It is recommended for accounts with frequent balance changes. Authentication is required.



Info

The Balance Channel `subscribe` message includes the new field, `account_ids`.

```codeBlockLines_p187
// Balance Channel subscribe message
{
  "type": "subscribe",
  "channels": [\
    {\
      "name": "balance",\
      "account_ids": [\
        "d50ec984-77a8-460a-b958-66f114b0de9b",\
        "d50ec984-77a8-460a-b958-66f114b0de9a"\
      ]\
    }\
  ]
}

```

#### FIX 4.2 Execution Report [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#fix-42-execution-report "Direct link to FIX 4.2 Execution Report")

Updated the [FIX 4.2 Execution Report](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#execution-report-8) as follows:

- `LeavesQty` and `CumQty` are now additionally populated in the Execution Report when `OrdStatus` is New or Replaced. In sum, they populate it when:
  - `39=0` ⇒ OrdStatus = New
  - `39=1` ⇒ OrdStatus = Partially filled
  - `39=3` ⇒ OrdStatus = Done for day
  - `39=5` ⇒ OrdStatus = Replaced
- `AvgPx` only populates Execution Report if CumQty > 0.

- `OrderQty` now represents the original order quantity when `OrdStatus` is Canceled or Done for day.


### 2024-JAN-09 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2024-jan-09 "Direct link to 2024-JAN-09")

Added [Travel Rule](https://docs.cdp.coinbase.com/exchange/docs/travel-rule-withdrawals) support:

- Added support for providing Travel Rule data when withdrawing to a crypto address.
- Added support for Coinbase to act as intermediary VASP for crypto withdrawals.
- [Withdraw to crypto address](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postwithdrawcrypto) accepts new optional parameters as part of its `POST` request:

  - `travel_rule_data`: Data necessary to satisfy Travel Rule data requirements.
  - `is_intermediary`: Flag to create transfer with Coinbase as intermediary VASP.

    - If `true`, `intermediary_jurisdiction` must be provided.
    - Parameter `travel_rule_data` may be necessary if the jurisdiction requires data.
  - `intermediary_jurisdiction`: Jurisdiction (ISO 3166-1 alpha-2) for Travel Rule data validation.

### 2023-DEC-22 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-dec-22 "Direct link to 2023-DEC-22")

Added [RFQ](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#rfq) support to FIX 5.0 Order Entry.

### 2023-DEC-20 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-dec-20 "Direct link to 2023-DEC-20")

Released [ResendRequest (35=2)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#resendrequest-352) and [SequenceReset-GapFill](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#sequencereset-354) to production for [FIX 5.0 Order Entry](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50).

### 2023-NOV-27 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-nov-27 "Direct link to 2023-NOV-27")

Added Iceberg Orders to FIX 5.0 production:

- [NewOrderSingle (35=D)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#newordersingle-35d)
- [ExecutionReport (35=8)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#executionreport-358)

See [Iceberg Orders](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#iceberg-orders) in 4.2 for conceptual details.

### 2023-NOV-21 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-nov-21 "Direct link to 2023-NOV-21")

Added **[Loan APIs](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getloans)** for underwritten users to view and monitor loan/collateral metrics, initiate loan opens and initiate loan repayments.



Info

See [Coinbase Exchange Loans Program](https://coinbase.bynder.com/m/47c334b9a63ed3e4/original/Coinbase-Exchange-Loans-Program.pdf) for info on program structure, process, and eligibility.

- [List loans](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getloans)

`GET https://api.exchange.coinbase.com/loans`

- [List loan assets](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getloanassets)

`GET https://api.exchange.coinbase.com/loans/assets`

- [Get lending overview](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getloanlendingoverview)

`GET https://api.exchange.coinbase.com/loans/lending-overview`

- [Get new loan preview](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getloanpreview)

`GET https://api.exchange.coinbase.com/loans/loan-preview`

- [Open new loan](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_openloan)

`POST https://api.exchange.coinbase.com/loans/open`

- [List new loan options](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getnewloanoptions)

`GET https://api.exchange.coinbase.com/loans/options`

- [Repay loan principal](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_repayprincipal)

`POST https://api.exchange.coinbase.com/loans/repay-principal`

- [Get principal repayment preview](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getrepaymentpreview)

`GET https://api.exchange.coinbase.com/loans/repayment-preview`


### 2023-NOV-02 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-nov-02 "Direct link to 2023-NOV-02")

Added [Iceberg Orders](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#iceberg-orders) to FIX 4.2 production and the REST API.

- FIX 4.2 [New Order Single (D)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#new-order-single-d) and [Execution Report (8)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#execution-report-8)
- REST API [Create a new order](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postorders).

### 2023-OCT-30 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-oct-30 "Direct link to 2023-OCT-30")

In FIX 4.2, disabled `DropCopyFlag` by default by setting `9406=N` (from Y). See [Logon (A)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#logon-a).

To ensure a session continues to receive Drop Copy reports, explicitly enable `DropCopyFlag` by setting `9406=Y`. See [Drop Copy Session](https://docs.cdp.coinbase.com/exchange/docs/fix-best-practices#drop-copy-session) in _Best Practices_ for more.



Note

Previously, `DropCopyFlag` was enabled by default in FIX 4.2. (It was always disabled in [FIX 5.0](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#logon-35a)).

### 2023-OCT-24 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-oct-24 "Direct link to 2023-OCT-24")

Added `destination_tag_regex` field to the `supported_networks` of the `currencies` object in [Status message](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#status-channel)

### 2023-OCT-02 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-oct-02 "Direct link to 2023-OCT-02")

[FIX Order Entry on the FIX 5.0 SP2 protocol](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50) was released to production.

### 2023-SEP-19 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-sep-19 "Direct link to 2023-SEP-19")

Added Iceberg orders to the FIX 4.2 Sandbox. See [Upcoming Changes](https://docs.cdp.coinbase.com/exchange/docs/upcoming-changes) for details.

### 2023-SEP-07 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-sep-07 "Direct link to 2023-SEP-07")

Added the following RFQ feature to production:

- [RFQ Request (AH)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#rfq-request-ah) enables users to submit subscription requests based on specific assets, ensuring that only these particular requests are forwarded. For example, if subscribing to "ETH-USD" with both products present, a quote request message and quote status report for both "ETH-USD" and "USD-ETH" are returned as responses.

### 2023-SEP-01 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-sep-01 "Direct link to 2023-SEP-01")

Added Travel Rule APIs for users to provide and manage their travel rule deposit information. Additionally, for users in certain jurisdictions, either `vasp_id` or `is_verified_self_hosted_wallet` must be provided when creating address book entries.

- [Get all travel rule information](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_gettravelrules)

`GET https://api.exchange.coinbase.com/travel-rules`

- [Create travel rule entry](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_posttravelrule)

`POST https://api.exchange.coinbase.com/travel-rules`

- [Delete existing travel rule entry](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_deletetravelrule)

`DELETE https://api.exchange.coinbase.com/travel-rules/{travel_rule_id}`

- [Submit travel information for a transfer](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_posttransfertravelrule)

`POST https://api.exchange.coinbase.com/transfers/{transfer_id}/travel-rules`

- [Add addresses](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postaddressbook)

`POST https://api.exchange.coinbase.com/address-book`


### 2023-AUG-28 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-aug-28 "Direct link to 2023-AUG-28")

Exchange began enforcing the following validation logic:

- **REST & FIX**: Extra leading zeros on quantities and prices are not accepted. They must be in standard form.
- **FIX only**: When sending market orders, only `CashOrderQty` or `OrderQty` can be included on the order, not both.
- **REST only**: When sending market orders, only `size` or `funds` can be included on the order, not both.

### 2023-AUG-14 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-aug-14 "Direct link to 2023-AUG-14")

Added the following RFQ features to production:

#### FIX [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#fix "Direct link to FIX")

- [Quote (S)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#quote-s): The response was reduced to 250ms (from 1000ms).
- [MiscFeeAmt (137)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#quote-request-r): Fees are returned on MiscFeeAmt (137) per product.

  - Fees published on tag `137` match what is available on the REST endpoint.
  - Fees may be published at a rate lower than 5bps on a per-pair basis.

#### REST [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#rest "Direct link to REST")

- `/rfq/products` (unauthenticated) returns all currently supported and eligible RFQ product pairs and their associated fee rates ( `maker_fee_bps`), plus additional metadata.

```codeBlockLines_p187
GET https://api-public.exchange.coinbase.com/rfq/products

```

```codeBlockLines_p187
## Sample Response
{
   "id": "AAVE-BCH",
   "base_currency": "AAVE",
   "quote_currency": "BCH",
   "enabled": true,
   "maker_fee_bps": "5",
   "rfq_tier": 2
}

```

See [Upcoming Changes](https://docs.cdp.coinbase.com/exchange/docs/upcoming-changes#rfq-updates) for RFQ features available in the sandbox.

### 2023-AUG-03 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-aug-03 "Direct link to 2023-AUG-03")

Added the ability to [download FIX specifications](https://docs.cdp.coinbase.com/exchange/docs/fix-downloads).

### 2023-AUG-01 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-aug-01 "Direct link to 2023-AUG-01")

The following WebSocket feeds now enforce authentication (in addition to the [User channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#user-channel)):

- [Full channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#full-channel)
- [Level2 channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#level2-channel)
- [Level3 channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#level3-channel)

See [WebSocket Authentication](https://docs.cdp.coinbase.com/exchange/docs/websocket-auth) for instructions.



All Channels

Coinbase recommends that you authenticate _all_ WebSocket channels, but only those noted above are enforced.



Level2 Batch Channel

To continue receiving Level 2 data without authentication, you can use the [Level2 Batch Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#level2-batch-channel), which delivers Level 2 data in batches every 50 milliseconds.

### 2023-JUL-21 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-jul-21 "Direct link to 2023-JUL-21")

Added the Exchange FIX 5.0 SP2 specification for Order Entry (sandbox only):

- Exchange FIX 5.0 SP2 [Order Entry (Sandbox Only)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50)

### 2023-JUN-14 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-jun-14 "Direct link to 2023-JUN-14")

#### API Manage Permission Type [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#api-manage-permission-type "Direct link to API Manage Permission Type")

Introduced new `MANAGE` API key permission type to manage user settings and preferences.

#### Address Book API [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#address-book-api "Direct link to Address Book API")

Added functionality for users to manage their Address Books via API:

- [Add new crypto address to address book](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postaddressbook)

`POST https://api.exchange.coinbase.com/address-book`

- [Delete an address from address book](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_deleteaddressbookentry)

`DELETE https://api.exchange.coinbase.com/address-book/{address_book_id}`


### 2023-JUN-13 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-jun-13 "Direct link to 2023-JUN-13")

Added documentation on [Systems & Operations](https://docs.cdp.coinbase.com/exchange/docs/runbook)

### 2023-JUN-06 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-jun-06 "Direct link to 2023-JUN-06")

Updated the Exchange [FIX 4.2 specification](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry)

### 2023-MAY-01 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-may-01 "Direct link to 2023-MAY-01")

[FIX Resend Requests](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#resend-request-2) (or FIX "Replay") is live in production. Resend requests are sent by the receiving application to initiate the retransmission of messages.

| Tag | Name | Description |
| --- | --- | --- |
| 7 | [BeginSeqNo](https://www.onixs.biz/fix-dictionary/4.2/tagnum_7.html) | Sequence number of first message in range to be resent |
| 16 | [EndSeqNo](https://www.onixs.biz/fix-dictionary/4.2/tagnum_16.html) | Sequence number of last message in range to be resent |

### 2023-APR-24 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-apr-24 "Direct link to 2023-APR-24")

We added USD ⟨⟩ USDC unification which lets Coinbase Exchange users update their settlement preference to be either the stable coin counterpart for a fiat currency, or the fiat currency itself.

- [Update settlement preference](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postuserlevelsettlementpreferences)

`POST https://api.exchange.coinbase.com/users/{user_id}/settlement-preferences`


### 2023-APR-19 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-apr-19 "Direct link to 2023-APR-19")

Added functionality for users to stake-wrap ETH to CBETH via Web & API:

- [Create a new stake-wrap](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postwrappedassetstakewrap)

`POST https://api.exchange.coinbase.com/wrapped-assets/stake-wrap`

- [Get all stake-wraps](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getallwrappedassetstakewraps)

`GET https://api.exchange.coinbase.com/wrapped-assets/stake-wrap`

- [Get a single stake-wrap](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getwrappedassetstakewrap)

`GET https://api.exchange.coinbase.com/wrapped-assets/stake-wrap/{stake_wrap_id}`


Learn more at [Coinbase Exchange CBETH Stake Wrap Instructions](https://coinbase.bynder.com/m/5d3cff1b03f8aeb0/original/Coinbase-Exchange-CBETH-Stake-Wrap-Instructions.pdf).

### 2023-MAR-29 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-mar-29 "Direct link to 2023-MAR-29")

We added a new [Level3 WebSocket channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#level3-channel) which is a compact, low bandwidth, and easier to parse version of the Full channel.

### 2023-MAR-15 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-mar-15 "Direct link to 2023-MAR-15")

Added new `apy` field to [Get Wrapped Asset Details](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getwrappedasset).

Implied APY is the current annualized percentage yield earned as the net rewards by the staked ETH underlying cbETH. This estimate is based on the past 7 days of staking performance and is updated daily. For more details, refer to the "rate calculation" section of the [cbETH whitepaper](https://www.coinbase.com/cbeth/whitepaper).

### 2023-MAR-02 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-mar-02 "Direct link to 2023-MAR-02")

We added a `time` property that denotes the last time our system processed an update.

**REST API**

[Get product book](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getproductbook) now returns `time` as a property when passing in "level=L1" / "level=L2" / "level=L3" on the `/products/{product_id}/book/` endpoint.

**Websocket API**

[Level2 Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#level2-channel) now includes the `time` property on the level2 snapshot message.

### 2023-MAR-01 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-mar-01 "Direct link to 2023-MAR-01")

We updated the Market Data feed: `client-oid` was removed from the **unauthenticated** [Full Channel Received message](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#received).

The `client-oid` field will still be available in the authenticated Full Channel, and also the [User Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#user-channel) (which also requires authentication). You can only see your own `client-oid`.

### 2023-FEB-23 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-feb-23 "Direct link to 2023-FEB-23")

#### FIX Execution Report ExecID [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#fix-execution-report-execid "Direct link to FIX Execution Report ExecID")

We released a change to how we publish the FIX tag, `ExecID (Tag=17)`. `ExecID` will now be consistent across sessions for the same underlying [Execution Report](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#execution-report-8). This should allow users the **ability to join Execution Reports** between their trading session and their drop-copy session for the same profile ID.

#### FIX Market Data Gateway [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#fix-market-data-gateway "Direct link to FIX Market Data Gateway")

We released [FIX Market Data gateway](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data) ( **beta**) to production. It is based on the [FIX 5.0 SP2 specification](https://www.onixs.biz/fix-dictionary/5.0.sp2/index.html).



Info

- Sandbox URL: `tcp+ssl//fix-md.sandbox.exchange.coinbase.com:6121`
- Production URL: `tcp+ssl//fix-md.exchange.coinbase.com:6121`

This new offering provides an L3 feed only with direct, low-latency, deterministic access. Users must connect with the same authentication as our existing FIX order-entry system.

- [Header](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data#header)
- [Logon (35=A)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data#logon-35a)
- [Market Data Request (35=V)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data#market-data-request-35v)
- [Market Data Request Reject (35=Y)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data#market-data-request-reject-35y)
- [Security Status (35=f)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data#security-status-35f)
- [Market Data Incremental Refresh (35=X)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data#market-data-incremental-refresh-35x)
- [Market Data Snapshot Full Refresh (35=W)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data#market-data-snapshot-full-refresh-35w)
- [Security List Request (35=x)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data#security-list-request-35x)
- [Security List (35=y)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data#security-list-35y)

### 2023-JAN-30 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-jan-30 "Direct link to 2023-JAN-30")

#### Expire Time Tag [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#expire-time-tag "Direct link to Expire Time Tag")

Added FIX message tag `ExpireTime` to [Quote Request (R)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#quote-request-r) and [Quote Status Report (AI)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#quote-status-report-ai).

#### High Bid Limit Percentage [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#high-bid-limit-percentage "Direct link to High Bid Limit Percentage")

Added new `high_bid_limit_percentage` field to our products endpoint.

As described in our [Trading Rules](https://www.coinbase.com/legal/trading_rules), the **High Bid Limit** (HBL) order control limits how high a Buy Limit Order can be filled based on the last sale price or the current best bid price.

Currently, the High Bid Limit is calculated as follows:

- **Last execution price + `high_bid_limit_percentage`** if the current best bid price is < 95% of the last execution execution.
- **Current best bid price + `high_bid_limit_percentage`** otherwise.

HBL is only enforced for specific trading pairs. You can see which trading pairs have an HBL set by looking at the `high_bid_limit_percentage` field of our [/products](https://api.exchange.coinbase.com/products) endpoint.

For example, the following value represents a 3% high bid limit.

```codeBlockLines_p187
{
  "high_bid_limit_percentage":"0.03000000"
}

```

### 2023-JAN-26 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-jan-26 "Direct link to 2023-JAN-26")

We made a breaking change to **[Get all wrapped assets](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getwrappedassets)**. Specifically, `GET /wrapped-assets/` now returns a list of json objects instead of a list of strings.

### 2023-JAN-06 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2023-jan-06 "Direct link to 2023-JAN-06")

Added new [Get Wrapped Asset Details](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getwrappedasset) endpoint: `/wrapped-assets/{wrapped_asset_id}/`

Get Wrapped Asset Details returns the following properties:

- `circulating_supply`: Customer held wrapped assets, not pre-minted or held in abeyance.
- `total_supply`: Wrapped assets that have been minted and exist on-chain.
- `conversion_rate`: Underlying staked units that can be exchanged for 1 wrapped asset.

For example:

```codeBlockLines_p187
{
  "wrapped_assets":[\
    {\
      "id":"CBETH",\
      "circulating_supply":"314666.9334401934801646",\
      "total_supply":"1067354.0841178434801646",\
      "conversion_rate":"1.0241755005866786"\
    }\
  ]
}

```

You can test for cbETH in the sandbox at `https://api-public.sandbox.exchange.coinbase.com/wrapped-assets/CBETH/`

### 2022-DEC-09 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-dec-09 "Direct link to 2022-DEC-09")

Request For Quote on Coinbase Exchange is live in production. RFQ allows liquidity providers to respond and interact with real-time RFQ requests.

**New FIX Messages:**

- [RFQ Request (AH)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#rfq-request-ah)
- [Quote Request (R)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#quote-request-r)
- [Quote (S)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#quote-s)
- [Quote Status Report (AI)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#quote-status-report-ai)

**New WebSocket Channel:** [RFQ Matches Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#rfq-matches-channel).

**Updated REST API:**

- Order and fill information for RFQ can be queried with new `market_type` query parameter.
- New report type option, `rfq-fills`, can be used to generate reports for RFQ fills.

### 2022-NOV-22 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-nov-22 "Direct link to 2022-NOV-22")

We released [Coinbase Direct Market Data](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview), a WebSocket endpoint with direct access to Coinbase Exchange servers. [Authentication](https://docs.cdp.coinbase.com/exchange/docs/websocket-auth) is required. You can subscribe to both endpoints, but if `ws-direct` becomes your primary connection, we recommend using the existing `ws-feed` as a failover connection.

**Coinbase Direct Market Data endpoint:** `wss://ws-direct.exchange.coinbase.com`

### 2022-OCT-26 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-oct-26 "Direct link to 2022-OCT-26")

Updated **[Get all fills](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getfills)** with new response property, `market_type`, in preparation for the upcoming Request For Quote (RFQ) feature.

### 2022-OCT-17 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-oct-17 "Direct link to 2022-OCT-17")

Added two new fields to the [Ticker Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#ticker-channel): `best_bid_size` and `best_ask_size`.

### 2022-OCT-04 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-oct-04 "Direct link to 2022-OCT-04")

[Modify Order Request (G)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#modify-order-request-g) is live in production. See [2022-JUN-27](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-jun-27) for release details.

### 2022-SEP-22 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-sep-22 "Direct link to 2022-SEP-22")

[FIX Logon (A) messages](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#logon-a) now require that MsgSeqNum (34) be equal to `1`. Any other value is rejected.

### 2022-SEP-19 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-sep-19 "Direct link to 2022-SEP-19")

Added **[Balance Statement Reports](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postreports#balance-reports)** for historical and current crypto/fiat balances, with the Exchange REST API and in the Exchange UI at [`exchange.coinbase.com/profile/statements`](https://exchange.coinbase.com/profile/statements).

- [Create Balance Statement Report](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postreports)
- [Get Balance Statement Reports](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getreports)

The Balance Report API:

- Leverages the existing `/reports` endpoint.
- Adds a new report type of `balance`.
- Adds a `balance` object to the request with `datetime` (and `group_by_portfolio_id` for the UI only).
- Keeps the same response schema (with the possibility that `"type"="balance"`).

_Example of Balance Report API Request_

```codeBlockLines_p187
// Create balance statement for the portfolio tied to the API key
{
  "balance": {
    "datetime": "2022-02-25T05:00:00.000Z"
  },
  "email": "user1@example.com",
  "format": "csv",
  "type": "balance"
}

```

### 2022-AUG-24 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-aug-24 "Direct link to 2022-AUG-24")

Added a new Wrapped Asset API, comprised of two endpoints:

- [Get all wrapped assets](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getwrappedassets): Returns a list of all Coinbase supported wrapped asset IDs.







```codeBlockLines_p187
/wrapped-assets

```

- [Get conversion rate of wrapped asset](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getwrappedassetconversionrate): Returns the conversion rate of a wrapped asset to its corresponding staked asset.







```codeBlockLines_p187
/wrapped-assets/{wrapped_asset_id}/conversion-rate

```


### 2022-AUG-16 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-aug-16 "Direct link to 2022-AUG-16")

Added a `reason` field to the WebSocket Full Channel [Change message](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#change):

- `"reason":"STP"` for Self-Trade Prevention message
- `"reason":"modify_order"` for Modify Order Request (See [2022-JUN-27](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-jun-27) entry for more.)

```codeBlockLines_p187
{
  "type": "change",
  "reason": "STP",
  "time": "2014-11-07T08:19:27.028459Z",
  "sequence": 80,
  "order_id": "ac928c66-ca53-498f-9c13-a110027a60e8",
  "side": "sell",
  "product_id": "BTC-USD",
  "old_size": "12.234412",
  "new_size": "5.23512",
  "price": "400.23"
}

```

### 2022-JUL-27 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-jul-27 "Direct link to 2022-JUL-27")

We added support for multiple blockchain networks. Users can now withdraw USDC on Solana, and ETH, USDC, and MATIC on Polygon.

A new `network` field was added for select endpoints and in the UI. Affected API endpoints are:

- `/withdrawals/crypto` accepts an optional network parameter as part of its `POST` request parameters.

This parameter designates which network the currency will be sent on. For example, if the user withdraws USDC on Solana or Ethereum, the withdrawal address is validated against the network, the appropriate fee is calculated based on the network, and the currency is sent over the network. If no network is specified in the `POST` request, the default network (Ethereum) is used.

- `/address-book` validates new addresses against all supported networks for the currency.

- `/address-validation` accepts an optional `network` parameter in the `address_info` object or `source` parameter in the body as part of its `POST` request parameters.

The address validator uses the `network` parameter to verify that the address is valid for the designated network. If no `network` is specified in the `POST` request, the default network is used.

The `source` parameter currently only accepts the value `address_book`. When `source` has the value `address_book`, the address is validated against all supported networks for the currency.


```codeBlockLines_p187
"id": "ATOM",
"name": "Cosmos",
"min_size": "1",
"status": "online",
"message": "",
"max_precision": "0.000001",
"convertible_to": [\
\
],
"details": {
  "type": "crypto",
  "symbol": null,
  "network_confirmations": null,
  "sort_order": 51,
  "crypto_address_link": "https://cosmos.bigdipper.live/account/{{address}}",
  "crypto_transaction_link": "https://cosmos.bigdipper.live/transactions/{{txId}}",
  "push_payment_methods": [\
    "crypto"\
  ],
  "group_types": [\
  ],
  "display_name": null,
  "processing_time_seconds": 5,
  "min_withdrawal_amount": 0.1,
  "max_withdrawal_amount": 302000
},
"default_network": "cosmos",
"supported_networks": [\
  "id": "ETH",\
  "name": "ethereum",\
  "status": "offline",\
  "contract_address": "0x..",\
  "crypto_address_link": "address_link",\
  "crypto_transaction_link": "tx_link",\
  "network_confirmations": 15,\
  "min_withdrawal_amount": 0.001,\
  "max_withdrawal_amount": 250\
]

```

### 2022-JUL-25 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-jul-25 "Direct link to 2022-JUL-25")

We increased the order size for two FIX batched messages from 10 to 15:

- [New Order Batch (U6)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#new-order-batch-u6)
- [Order Cancel Batch Request (U4)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#order-cancel-batch-request-u4)

### 2022-JUN-30 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-jun-30 "Direct link to 2022-JUN-30")

The following API parameters were removed per the lifting of [maximum and minimum order size limits](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-jun-02):

| API Parameter | Description |
| --- | --- |
| base\_max\_size | Base order size max (limit orders) |
| base\_min\_size | Base order size min (limit orders) |
| max\_market\_funds | Quote order size max (market orders) |

Affected features are:

- REST API: [Get all known trading pairs](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getproducts)
- REST API: [Create a new order](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postorders#size)
- Websocket API [Status Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#status-channel)

### 2022-JUN-27 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-jun-27 "Direct link to 2022-JUN-27")

[Modify Order Request (G)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#modify-order-request-g) is now **available for testing** in the [public sandbox](https://docs.cdp.coinbase.com/exchange/docs/sandbox). It will go to production in a few weeks.

Modify Order Request is an implementation of the [Order Replace Request](https://www.onixs.biz/fix-dictionary/4.2/msgtype_g_71.html) outlined in the FIX 4.2 protocol. You can send a single request to modify the price or size of an existing order using the FIX API.

[WebSocket Full channel "Change"](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#change) messages (and by extension the [User channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#user-channel)) are also affected. Three fields are being added ( `new_price`, `old_price`, `reason`).



Info

Modify Order Requests that amend size down will retain queue priority in the Exchange order book.

**FIX API**

Example FIX Request:

```codeBlockLines_p187
BeginString=FIX.4.2 BodyLength=265 MsgType=ORDER_CANCEL_REPLACE_REQUEST MsgSeqNum=17 SenderCompID=00000000100000000000000000000003 SendingTime=20220609-04:01:48.757 TargetCompID=Coinbase ClOrdID=907b6ae6-bcbe-441a-b7bb-d932afdb9edb OrderID=71de0cdf-938f-495b-9fad-108837bde704 OrderQty=2 OrdType=LIMIT OrigClOrdID=907b6ae6-bcbe-441a-b7bb-d932afdb9eda Price=100.00 Side=BUY Symbol=ETH-USD TransactTime=20220609-04:01:48.757 CheckSum=107

```

| Tag | Name | Description |
| --- | --- | --- |
| 37 | OrderID | Unique identifier of most recent order as assigned by broker |
| 41 | OrigClOrdID | `ClOrdID <11>` of previous order (NOT initial order of the day) when canceling or replacing an order |
| 11 | ClOrdID | Unique identifier of replacement order as assigned by institution. |
| 55 | Symbol | Must match original order |
| 54 | Side | Must match original side |
| 38 | OrderQty | Total Intended Order Quantity (including the amount already executed for this chain of orders) |
| 60 | TransactTime | Time this order request was initiated/released by the trader or trading system |
| 40 | OrdType | Only limit orders are supported for now (2) |
| 44 | Price | Price per share |

**Websocket Full Channel Change Message**

Example of a change message from a Modify Order Request:



Caution

The fields `new_price`, `old_price`, and `reason` are being added. (The `reason` field was added on [2022-AUG-16](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-aug-16).

```codeBlockLines_p187
{
  "type": "change",
  "reason": "modify_order",
  "time": "2022-06-06T22:55:43.433114Z",
  "sequence": 24753,
  "order_id": "c3f16063-77b1-408f-a743-88b7bc20cdcd",
  "side": "buy",
  "product_id": "ETH-USD",
  "old_size": "80",
  "new_size": "80",
  "old_price": "7",
  "new_price": "6"
}

```

### 2022-JUN-02 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-jun-02 "Direct link to 2022-JUN-02")

Lifted maximum and minimum order size limits. With this change:

- Market orders are no longer subject to max or min size checks unless market funds are specified.
- Limit orders are now subject to **notional minimum size checks only**. We repurposed the existing API parameter, `min_market_funds`, to represent this value.

Price Protection Points serve as a dynamic and real-time protection against slippage for large-sized orders.

The following API parameters have been deprecated (and will be removed June 30):

| API Parameter | Description |
| --- | --- |
| base\_max\_size | Base order size max (limit orders) |
| base\_min\_size | Base order size min (limit orders) |
| max\_market\_funds | Quote order size max (market orders) |

Affected APIs are [Get all known trading pairs](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getproducts) and [Create a new order](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postorders#size).

### 2022-MAY-25 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-may-25 "Direct link to 2022-MAY-25")

Changes were made to Coinbase Pro:

- We disabled the Coinbase Pro API, [Deposit from Coinbase account](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postdepositcoinbaseaccount), which lets you deposit funds from a Coinbase retail account into Coinbase Pro. The endpoint `/deposits/coinbase-account` now returns a `403` when called from a Coinbase Pro account.

All other payment methods into Coinbase Pro remain the same and Coinbase Exchange is not affected.

- Creating a new API Key on Coinbase Pro with the Transfer permission has new requirements (the use of old API keys will remain the same):


  - You must enable non-SMS 2FA.
  - You must allowlist all receive addresses for your transfers.

Creating new API Keys on Coinbase Exchange is not affected by this change.

### 2022-MAY-05 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-may-05 "Direct link to 2022-MAY-05")

- Added cancel reason to the FIX and websocket feeds.

- For FIX, we enhanced the [Execution Report](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#execution-report-8) to include the cancel reason using the [Text field](https://www.onixs.biz/fix-dictionary/4.2/tagNum_58.html).
- For the websocket feed, we added a new `cancel_reason` field for authenticated messages by the user, accessible in the [Full](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#full-channel) and [User](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#user-channel) channels.

Supported cancel reasons are:

```codeBlockLines_p187
101:Time In Force
102:Self Trade Prevention
103:Admin
104:Price Bound Order Protection
105:Insufficient Funds"
106:Insufficient Liquidity
107:Broker

```

### 2022-MAY-02 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-may-02 "Direct link to 2022-MAY-02")

We enabled new TLS/SSL features on the FIX servers for Exchange/Pro to increase security and performance. This includes limiting the supported ciphers and a new SSL certificate. Please check that your FIX SSL client:

- Can support the new ciphers listed below.
- Is not validating a specific SSL server certificate. If it is, you must update to the new certificate.

The new infrastructure will support only **TLSv1.2** with the following Supported Server Ciphers:

| Recommend | Length | Cipher Suite | Elliptic Curve |
| --- | --- | --- | --- |
| Preferred | 128 bits | ECDHE-RSA-AES128-GCM-SHA256 | Curve P-256 DHE 256 |
| Accepted | 128 bits | ECDHE-RSA-AES128-SHA256 | Curve P-256 DHE 256 |
| Accepted | 256 bits | ECDHE-RSA-AES256-GCM-SHA384 | Curve P-256 DHE 256 |
| Accepted | 256 bits | ECDHE-RSA-AES256-SHA384 | Curve P-256 DHE 256 |

Affected Endpoints:

- In sandbox







```codeBlockLines_p187
fix-public.sandbox.pro.coinbase.com:4198
fix-public.sandbox.exchange.coinbase.com:4198

```

- In production







```codeBlockLines_p187
fix.pro.coinbase.com:4198
fix.exchange.coinbase.com:4198

```


New Production FIX Server SSL Certificate:

```codeBlockLines_p187
-----BEGIN CERTIFICATE-----
MIIEezCCA2OgAwIBAgIQB4BoKHs2w7hI3RLss1nw7DANBgkqhkiG9w0BAQsFADBG
MQswCQYDVQQGEwJVUzEPMA0GA1UEChMGQW1hem9uMRUwEwYDVQQLEwxTZXJ2ZXIg
Q0EgMUIxDzANBgNVBAMTBkFtYXpvbjAeFw0yMjAzMzEwMDAwMDBaFw0yMzA0Mjky
MzU5NTlaMCIxIDAeBgNVBAMMFyouZXhjaGFuZ2UuY29pbmJhc2UuY29tMIIBIjAN
BgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAnmFkdVt+0k/d+HkZaX/kgjtCU6Ts
5TePVbYCGOjT05ClT7GHu7fSzUjO/BNCkBItp5WwFRdOOkWV8Zeg2WSHpDBOZNJt
cXiQx6BSTRD/myjv0NBxVsKby9BbKmj8df3C1PehakUQPdsiP7DkviYUpXz+T4FQ
PAg8M6PXu7sT7Rfbc6gY49VyyRU6slcij/Xwn4WSVWK+GMYPlsu7M2Vp0rr+sCIZ
uLHh/23TNzlGiYzXgypoZ/F57AIi+ToeRvnLe++ZfIKP37uhNxYfYrr4c3wPBoGc
LIWgSNMK9/Oue6VUCG7AVioCy2yL0CEiTmvS4Eb2urbt3iDWI+6wySW9LwIDAQAB
o4IBhzCCAYMwHwYDVR0jBBgwFoAUWaRmBlKge5WSPKOUByeWdFv5PdAwHQYDVR0O
BBYEFOlcV+BjGTnleq713Nzl4UifIPZCMDkGA1UdEQQyMDCCFyouZXhjaGFuZ2Uu
Y29pbmJhc2UuY29tghVleGNoYW5nZS5jb2luYmFzZS5jb20wDgYDVR0PAQH/BAQD
AgWgMB0GA1UdJQQWMBQGCCsGAQUFBwMBBggrBgEFBQcDAjA9BgNVHR8ENjA0MDKg
MKAuhixodHRwOi8vY3JsLnNjYTFiLmFtYXpvbnRydXN0LmNvbS9zY2ExYi0xLmNy
bDATBgNVHSAEDDAKMAgGBmeBDAECATB1BggrBgEFBQcBAQRpMGcwLQYIKwYBBQUH
MAGGIWh0dHA6Ly9vY3NwLnNjYTFiLmFtYXpvbnRydXN0LmNvbTA2BggrBgEFBQcw
AoYqaHR0cDovL2NydC5zY2ExYi5hbWF6b250cnVzdC5jb20vc2NhMWIuY3J0MAwG
A1UdEwEB/wQCMAAwDQYJKoZIhvcNAQELBQADggEBADemhPMMlRRLMlnSvaVaaSCF
ncdehfDVg3Lmr2UjcMCq2MJxriz8elgu7M6TqVGwiRVrMb4j2kD+3EUc/+V+W1dE
uX8aEzxuV01MKTFEh4R/WihCKM2l0NCfg6O8jYmtKPE9gkHe+5hW4igsM90mK+hA
GlhH7hGSouHDjkwbvlN0yrNFJXaTZE8wHd1VTDtYmzTQXkn8hAR4muesAgEtc22W
B8vbLCt6ZOeoMH/SKh2vsAmWE/3DR7+TIh9Dm+54jEwuUID+nmETaacY2wDT1XU9
eWR4xJMa8QuK1sGuO3TgvYZPCyzAXoXCjR5mVYit8PteMVwfJnTm1nLc73rAiWA=
-----END CERTIFICATE-----

```

New Sandbox FIX Server SSL Certificate:

```codeBlockLines_p187
-----BEGIN CERTIFICATE-----
MIIEdDCCA1ygAwIBAgIQD03L1cHVypYSDFuvcnpAHzANBgkqhkiG9w0BAQsFADBG
MQswCQYDVQQGEwJVUzEPMA0GA1UEChMGQW1hem9uMRUwEwYDVQQLEwxTZXJ2ZXIg
Q0EgMUIxDzANBgNVBAMTBkFtYXpvbjAeFw0yMjAzMjcwMDAwMDBaFw0yMzA0MjUy
MzU5NTlaMCoxKDAmBgNVBAMMHyouc2FuZGJveC5leGNoYW5nZS5jb2luYmFzZS5j
b20wggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQC8LYRdqMoVNa/0M4MF
+Wkr8SiybZ95JycTE+0ZVmf92DKo4I8m/8fBtOrH0jgrhvamVSJ0lI6VFiAzlTd1
doUbliQ9Xm1aE/YHQO9J64AIP97peysgHBd+g3/Vhz33aaaU2vyHH5kPHiekU8n/
ObXPPoFd/Awul8uxxlXsVFx8oBWL2MeMjLNLLWNiGWq+lQloGKsQYVR/fQZizvpP
vyZO6pCLRId6+Wq3Tcb7NHQZc6+tePVi+5fovE+lm/yQrhjGqDzI7P4rWjJqCPrA
sYJeYFcVJhdSuFY2Ngm8eKeDP14TVEs9pkIWvyMGmB17QBPbRJipdoKu1N6fsx54
N9JDAgMBAAGjggF4MIIBdDAfBgNVHSMEGDAWgBRZpGYGUqB7lZI8o5QHJ5Z0W/k9
0DAdBgNVHQ4EFgQUa5RZ0yvv71YteSuqO1VRvmGGKv0wKgYDVR0RBCMwIYIfKi5z
YW5kYm94LmV4Y2hhbmdlLmNvaW5iYXNlLmNvbTAOBgNVHQ8BAf8EBAMCBaAwHQYD
VR0lBBYwFAYIKwYBBQUHAwEGCCsGAQUFBwMCMD0GA1UdHwQ2MDQwMqAwoC6GLGh0
dHA6Ly9jcmwuc2NhMWIuYW1hem9udHJ1c3QuY29tL3NjYTFiLTEuY3JsMBMGA1Ud
IAQMMAowCAYGZ4EMAQIBMHUGCCsGAQUFBwEBBGkwZzAtBggrBgEFBQcwAYYhaHR0
cDovL29jc3Auc2NhMWIuYW1hem9udHJ1c3QuY29tMDYGCCsGAQUFBzAChipodHRw
Oi8vY3J0LnNjYTFiLmFtYXpvbnRydXN0LmNvbS9zY2ExYi5jcnQwDAYDVR0TAQH/
BAIwADANBgkqhkiG9w0BAQsFAAOCAQEATpjyCMwAOSFKFTA67UaVkDCjz/ULBY6P
L4JwTJ+7kmT+HMvGimx15CsVjne64bT5twWlzqA/l4h25HGj0hD0TU2ktqmFhfAm
DpjGVp4KgIcZpvv7oRIU4e5I422Y++2UVuATwLWdELgpnm4AVq1aqI10XrQlJeHL
gRVfV5qkr9Vsc+fk7HY7YwbNQk2jXbRaj22f6GxiJ/6VmUcCD7zZ1GZtUipv0JEy
PtWD/BbSKNx1GJnLZ6L+QytPs+MW+FEetlU/oqPuyYRhmJUBUiwKkm6yKWRj9tQf
sq0a4uLI3SUgsBv/CQ/Qa9LnRdNjvlWSKLzeIX2LU9rE/3F3oQh7HQ==
-----END CERTIFICATE-----

```

### 2022-APR-14 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-apr-14 "Direct link to 2022-APR-14")

- Updated the maximum number of portfolios (or profiles) to 25.

### 2022-MAR-21 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-mar-21 "Direct link to 2022-MAR-21")

- Updated the maximum number of portfolios (or profiles) to 15.

### 2022-MAR-17 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-mar-17 "Direct link to 2022-MAR-17")

- Added FIX message tags: `cumQty`, `leaveQty`, `AvgPx`

### 2022-FEB-22 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-feb-22 "Direct link to 2022-FEB-22")

- REST API will enforce case sensitivity for all URLs.
  - Example: [https://api.exchange.coinbase.com/products/BTC-USD/Ticker](https://api.exchange.coinbase.com/products/BTC-USD/Ticker) should be [https://api.exchange.coinbase.com/products/BTC-USD/ticker](https://api.exchange.coinbase.com/products/BTC-USD/ticker). Note the lowercase `t` in `ticker`.
  - This does not apply to URL parameters, just the URL itself: `https://api.exchange.coinbase.com/orders?product_id=BTC-USD&sortedBy=created_at&sorting=desc&limit=100` is valid as the the URL is lowercase. Query parameters such as `product_id` can have values with capitals. However `https://api.exchange.coinbase.com/Orders?product_id=BTC-USD&sortedBy=created_at&sorting=desc&limit=100` would be invalid as the `O` in `/Orders` is not the same URL as specified in its [docs](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getorders).

### 2022-JAN-31 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-jan-31 "Direct link to 2022-JAN-31")

- Web Socket API users are notified when the client is actively disconnected for having a full buffer, or for being too slow to consume or read messages.

### 2022-JAN-25 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2022-jan-25 "Direct link to 2022-JAN-25")

- `GET` and `POST` responses for the `/orders` endpoint will return client order id as `client_oid` if exists.

### 2021-OCT-25 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2021-oct-25 "Direct link to 2021-OCT-25")

- FIX API will now enforce CheckSum validations for incoming FIX messages.

### 2021-SEP-21 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2021-sep-21 "Direct link to 2021-SEP-21")

- All reports can be generated in parallel. Clients are no longer restricted to only have 3 reports being created at a time. Now clients can have up to 3 accounts reports and 3 fills reports _per_ product generating at a time.

### 2021-SEP-09 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2021-sep-09 "Direct link to 2021-SEP-09")

- Return the full aggregated order book for Level 2 queries under the `GET /products/<product-id>/book` endpoint.

### 2021-AUG-23 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2021-aug-23 "Direct link to 2021-AUG-23")

- Reduced the set of fields returned by orders in "pending" status for `GET /orders`, `GET /orders/<id>`, and `GET /orders/client:<client_oid>` APIs. See `List Orders` documentation for more details. Orders with non-pending statuses will be unaffected by this change.

### 2021-AUG-17 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2021-aug-17 "Direct link to 2021-AUG-17")

- Return client order ID rather than order ID in successful cancel order response for REST API endpoint `DELETE /orders/client:<client_oid>`.

### 2021-AUG-12 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2021-aug-12 "Direct link to 2021-AUG-12")

- Require the field Symbol(55) on the following FIX API messages: OrderCancelRequest(F) and OrderStatusRequest(H). Messages (F) and (H) without Symbol(55) will be rejected.

### 2021-AUG-06 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2021-aug-06 "Direct link to 2021-AUG-06")

- Add pagination support for the `GET /fills` endpoint.

### 2021-AUG-01 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2021-aug-01 "Direct link to 2021-AUG-01")

- Increased the maximum number of FIX connections allowed per profile from 5 to 7.

### 2021-JUL-01 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2021-jul-01 "Direct link to 2021-JUL-01")

- Added sendingTime 5 minute validation.

### 2021-JUN-22 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2021-jun-22 "Direct link to 2021-JUN-22")

- Added fx\_stablecoin to products.

### 2021-JUN-21 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2021-jun-21 "Direct link to 2021-JUN-21")

- Order Cancel Batch Request(U4) will accept optional ClOrdID(11) field for each cancel request. The provided ClOrdID(11) will be included in Order Cancel Reject(9) for partial reject.

### 2021-JUN-14 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2021-jun-14 "Direct link to 2021-JUN-14")

- Order Cancel Batch Request(U4) will now return Order Cancel Reject(9) for partial rejected cancel request.

### 2021-JUN-10 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2021-jun-10 "Direct link to 2021-JUN-10")

- Added failed status to reports.

### 2021-JUN-03 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2021-jun-03 "Direct link to 2021-JUN-03")

- Our API endpoints were moved to `exchange.coinbase.com` from `prime.coinbase.com`.

**_Production URLs_**

| Product | Old URL | New URL |
| --- | --- | --- |
| Website | [https://prime.coinbase.com](https://prime.coinbase.com/) | [https://exchange.coinbase.com](https://exchange.coinbase.com/) |
| REST API | [https://api.prime.coinbase.com](https://api.prime.coinbase.com/) | [https://api.exchange.coinbase.com](https://api.exchange.coinbase.com/) |
| FIX API | tcp+ssl://fix.prime.coinbase.com:4198 | tcp+ssl://fix.exchange.coinbase.com:4198 |
| Web Socket API | wss://ws-feed.prime.coinbase.com | wss://ws-feed.exchange.coinbase.com |

**_Sandbox URLs_**

| Product | Old URL | New URL |
| --- | --- | --- |
| Website | [https://public.sandbox.prime.coinbase.com](https://public.sandbox.prime.coinbase.com/) | [https://public.sandbox.exchange.coinbase.com](https://public.sandbox.exchange.coinbase.com/) |
| REST API | [https://api-public.sandbox.prime.coinbase.com](https://api-public.sandbox.prime.coinbase.com/) | [https://api-public.sandbox.exchange.coinbase.com](https://api-public.sandbox.exchange.coinbase.com/) |
| FIX API | tcp+ssl://fix-public.sandbox.prime.coinbase.com:4198 | tcp+ssl://fix-public.sandbox.exchange.coinbase.com:4198 |
| Web Socket API | wss://ws-feed-public.sandbox.prime.coinbase.com | wss://ws-feed-public.sandbox.exchange.coinbase.com |

### 2021-MAY-27 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2021-may-27 "Direct link to 2021-MAY-27")

- API FIX - Order Cancel Request (F) endpoint requires the Symbol field now.

### 2021-MAY-20 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2021-may-20 "Direct link to 2021-MAY-20")

- `/fills` custom rate limit.

### 2021-MAY-14 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2021-may-14 "Direct link to 2021-MAY-14")

- Increased public and private rate limits.

### 2021-APR-22 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2021-apr-22 "Direct link to 2021-APR-22")

- Increase pagination limit from 100 to 1000.

### 2021-APR-05 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2021-apr-05 "Direct link to 2021-APR-05")

- Updated max profiles to 10 and max API keys to 200.

### 2021-FEB-04 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2021-feb-04 "Direct link to 2021-FEB-04")

- The Trailing Volume endpoint has been deprecated in favor of the Fees endpoint to get the latest volumes.

### 2021-JAN-15 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2021-jan-15 "Direct link to 2021-JAN-15")

- Now recommending that clients opt to batch cancel orders by profile rather than session due to recent performance optimizations.

### 2020-DEC-23 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2020-dec-23 "Direct link to 2020-DEC-23")

- `HandlInst` in API FIX is no longer required.

### 2020-NOV-16 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2020-nov-16 "Direct link to 2020-NOV-16")

- Addition of `max_withdrawal_amount` field in the `/currencies` endpoint.

### 2020-OCT-05 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2020-oct-05 "Direct link to 2020-OCT-05")

- Authed users subscribed to the Websocket [Full](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#full-channel) or [User](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#user-channel) channel will now receive their order fee rates on match messages. Details can be found in documentation for the Full channel.

### 2020-OCT-02 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2020-oct-02 "Direct link to 2020-OCT-02")

- Addition of cancel\_code field on canceled withdrawals.

### 2020-SEP-17 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2020-sep-17 "Direct link to 2020-SEP-17")

- Addition of an endpoint to provide estimates of network fees for crypto withdrawals.
- Addition of a parameter for crypto withdrawals to specify if the network fee should be added / deducted from the requested amount.
- 'fee' and 'subtotal' fields added to responses for crypto withdrawals.

### 2020-SEP-14 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2020-sep-14 "Direct link to 2020-SEP-14")

- The candles endpoint no longer has custom rate limits. It now shares the same rate limit with every other public endpoint.

### 2020-SEP-03 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2020-sep-03 "Direct link to 2020-SEP-03")

- The maximum number of open orders (i.e. limit orders + stop orders) per product per profile will be 500. Profiles that exceed this threshold will be unable to place new orders on that product until the number of open orders is below 500.

### 2020-JUN-18 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2020-jun-18 "Direct link to 2020-JUN-18")

- Users can retrieve historical [deposits](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_gettransfers) and [withdrawals](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_gettransfers).

### 2020-JUN-17 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2020-jun-17 "Direct link to 2020-JUN-17")

- Generate an address for crypto deposits. See reference [here](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postcoinbaseaccountaddresses).

### 2020-JUN-15 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2020-jun-15 "Direct link to 2020-JUN-15")

- Expose `min_market_funds`, `max_market_funds` fields in the `/products` endpoint.

### 2020-JUN-12 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2020-jun-12 "Direct link to 2020-JUN-12")

- Users can retrieve information regarding their transfer, buy, and sell limits at `/users/self/exchange-limits`. Refer to the [Limits](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getuserexchangelimits) API for more information.

### 2020-APR-27 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2020-apr-27 "Direct link to 2020-APR-27")

- Fill execution reports will show fee rates associated with the user's order. Refer to the [FIX ExecutionReport API](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#execution-report-8) for details on format.

### 2020-FEB-20 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2020-feb-20 "Direct link to 2020-FEB-20")

- Execution Reports from Order Status Requests will return `ClOrdID`, if it is supplied, even if the order isn't found.

### 2020-FEB-10 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2020-feb-10 "Direct link to 2020-FEB-10")

- Activate messages on the Websocket feed will no longer expose `taker_fee_rate`.

### 2019-DEC-16 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2019-dec-16 "Direct link to 2019-DEC-16")

- Rate limiting changing from a per user basis to per profile basis.

### 2019-SEP-30 [](https://docs.cdp.coinbase.com/exchange/docs/changelog\#2019-sep-30 "Direct link to 2019-SEP-30")

- Order Status Request no longer allows the wildcard option.
- Order Status Request returns pending and done orders when you use OrderID or ClOrdID.
- Scheduled disconnects are on Mondays and Thursdays at 11 AM Pacific Time.

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [2025-MAY-09](https://docs.cdp.coinbase.com/exchange/docs/changelog#2025-may-09)
- [2025-APR-22](https://docs.cdp.coinbase.com/exchange/docs/changelog#2025-apr-22)
- [2025-JAN-28](https://docs.cdp.coinbase.com/exchange/docs/changelog#2025-jan-28)
- [2025-JAN-01](https://docs.cdp.coinbase.com/exchange/docs/changelog#2025-jan-01)
- [2024-DEC-2](https://docs.cdp.coinbase.com/exchange/docs/changelog#2024-dec-2)
- [2024-OCT-16](https://docs.cdp.coinbase.com/exchange/docs/changelog#2024-oct-16)
- [2024-SEP-19](https://docs.cdp.coinbase.com/exchange/docs/changelog#2024-sep-19)
- [2024-SEP-11](https://docs.cdp.coinbase.com/exchange/docs/changelog#2024-sep-11)
- [2024-AUG-21](https://docs.cdp.coinbase.com/exchange/docs/changelog#2024-aug-21)
- [2024-AUG-01](https://docs.cdp.coinbase.com/exchange/docs/changelog#2024-aug-01)
- [2024-JUN-27](https://docs.cdp.coinbase.com/exchange/docs/changelog#2024-jun-27)
- [2024-APR-22](https://docs.cdp.coinbase.com/exchange/docs/changelog#2024-apr-22)
- [2024-APR-02](https://docs.cdp.coinbase.com/exchange/docs/changelog#2024-apr-02)
- [2024-MAR-21](https://docs.cdp.coinbase.com/exchange/docs/changelog#2024-mar-21)
- [2024-MAR-19](https://docs.cdp.coinbase.com/exchange/docs/changelog#2024-mar-19)
- [2024-MAR-18](https://docs.cdp.coinbase.com/exchange/docs/changelog#2024-mar-18)
- [2024-MAR-06](https://docs.cdp.coinbase.com/exchange/docs/changelog#2024-mar-06)
- [2024-FEB-27](https://docs.cdp.coinbase.com/exchange/docs/changelog#2024-feb-27)
- [2024-FEB-23](https://docs.cdp.coinbase.com/exchange/docs/changelog#2024-feb-23)
- [2024-FEB-07](https://docs.cdp.coinbase.com/exchange/docs/changelog#2024-feb-07)
- [2024-FEB-05](https://docs.cdp.coinbase.com/exchange/docs/changelog#2024-feb-05)
- [2024-JAN-24](https://docs.cdp.coinbase.com/exchange/docs/changelog#2024-jan-24)
- [2024-JAN-16](https://docs.cdp.coinbase.com/exchange/docs/changelog#2024-jan-16)
- [2024-JAN-09](https://docs.cdp.coinbase.com/exchange/docs/changelog#2024-jan-09)
- [2023-DEC-22](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-dec-22)
- [2023-DEC-20](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-dec-20)
- [2023-NOV-27](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-nov-27)
- [2023-NOV-21](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-nov-21)
- [2023-NOV-02](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-nov-02)
- [2023-OCT-30](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-oct-30)
- [2023-OCT-24](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-oct-24)
- [2023-OCT-02](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-oct-02)
- [2023-SEP-19](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-sep-19)
- [2023-SEP-07](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-sep-07)
- [2023-SEP-01](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-sep-01)
- [2023-AUG-28](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-aug-28)
- [2023-AUG-14](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-aug-14)
- [2023-AUG-03](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-aug-03)
- [2023-AUG-01](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-aug-01)
- [2023-JUL-21](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-jul-21)
- [2023-JUN-14](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-jun-14)
- [2023-JUN-13](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-jun-13)
- [2023-JUN-06](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-jun-06)
- [2023-MAY-01](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-may-01)
- [2023-APR-24](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-apr-24)
- [2023-APR-19](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-apr-19)
- [2023-MAR-29](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-mar-29)
- [2023-MAR-15](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-mar-15)
- [2023-MAR-02](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-mar-02)
- [2023-MAR-01](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-mar-01)
- [2023-FEB-23](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-feb-23)
- [2023-JAN-30](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-jan-30)
- [2023-JAN-26](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-jan-26)
- [2023-JAN-06](https://docs.cdp.coinbase.com/exchange/docs/changelog#2023-jan-06)
- [2022-DEC-09](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-dec-09)
- [2022-NOV-22](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-nov-22)
- [2022-OCT-26](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-oct-26)
- [2022-OCT-17](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-oct-17)
- [2022-OCT-04](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-oct-04)
- [2022-SEP-22](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-sep-22)
- [2022-SEP-19](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-sep-19)
- [2022-AUG-24](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-aug-24)
- [2022-AUG-16](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-aug-16)
- [2022-JUL-27](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-jul-27)
- [2022-JUL-25](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-jul-25)
- [2022-JUN-30](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-jun-30)
- [2022-JUN-27](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-jun-27)
- [2022-JUN-02](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-jun-02)
- [2022-MAY-25](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-may-25)
- [2022-MAY-05](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-may-05)
- [2022-MAY-02](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-may-02)
- [2022-APR-14](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-apr-14)
- [2022-MAR-21](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-mar-21)
- [2022-MAR-17](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-mar-17)
- [2022-FEB-22](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-feb-22)
- [2022-JAN-31](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-jan-31)
- [2022-JAN-25](https://docs.cdp.coinbase.com/exchange/docs/changelog#2022-jan-25)
- [2021-OCT-25](https://docs.cdp.coinbase.com/exchange/docs/changelog#2021-oct-25)
- [2021-SEP-21](https://docs.cdp.coinbase.com/exchange/docs/changelog#2021-sep-21)
- [2021-SEP-09](https://docs.cdp.coinbase.com/exchange/docs/changelog#2021-sep-09)
- [2021-AUG-23](https://docs.cdp.coinbase.com/exchange/docs/changelog#2021-aug-23)
- [2021-AUG-17](https://docs.cdp.coinbase.com/exchange/docs/changelog#2021-aug-17)
- [2021-AUG-12](https://docs.cdp.coinbase.com/exchange/docs/changelog#2021-aug-12)
- [2021-AUG-06](https://docs.cdp.coinbase.com/exchange/docs/changelog#2021-aug-06)
- [2021-AUG-01](https://docs.cdp.coinbase.com/exchange/docs/changelog#2021-aug-01)
- [2021-JUL-01](https://docs.cdp.coinbase.com/exchange/docs/changelog#2021-jul-01)
- [2021-JUN-22](https://docs.cdp.coinbase.com/exchange/docs/changelog#2021-jun-22)
- [2021-JUN-21](https://docs.cdp.coinbase.com/exchange/docs/changelog#2021-jun-21)
- [2021-JUN-14](https://docs.cdp.coinbase.com/exchange/docs/changelog#2021-jun-14)
- [2021-JUN-10](https://docs.cdp.coinbase.com/exchange/docs/changelog#2021-jun-10)
- [2021-JUN-03](https://docs.cdp.coinbase.com/exchange/docs/changelog#2021-jun-03)
- [2021-MAY-27](https://docs.cdp.coinbase.com/exchange/docs/changelog#2021-may-27)
- [2021-MAY-20](https://docs.cdp.coinbase.com/exchange/docs/changelog#2021-may-20)
- [2021-MAY-14](https://docs.cdp.coinbase.com/exchange/docs/changelog#2021-may-14)
- [2021-APR-22](https://docs.cdp.coinbase.com/exchange/docs/changelog#2021-apr-22)
- [2021-APR-05](https://docs.cdp.coinbase.com/exchange/docs/changelog#2021-apr-05)
- [2021-FEB-04](https://docs.cdp.coinbase.com/exchange/docs/changelog#2021-feb-04)
- [2021-JAN-15](https://docs.cdp.coinbase.com/exchange/docs/changelog#2021-jan-15)
- [2020-DEC-23](https://docs.cdp.coinbase.com/exchange/docs/changelog#2020-dec-23)
- [2020-NOV-16](https://docs.cdp.coinbase.com/exchange/docs/changelog#2020-nov-16)
- [2020-OCT-05](https://docs.cdp.coinbase.com/exchange/docs/changelog#2020-oct-05)
- [2020-OCT-02](https://docs.cdp.coinbase.com/exchange/docs/changelog#2020-oct-02)
- [2020-SEP-17](https://docs.cdp.coinbase.com/exchange/docs/changelog#2020-sep-17)
- [2020-SEP-14](https://docs.cdp.coinbase.com/exchange/docs/changelog#2020-sep-14)
- [2020-SEP-03](https://docs.cdp.coinbase.com/exchange/docs/changelog#2020-sep-03)
- [2020-JUN-18](https://docs.cdp.coinbase.com/exchange/docs/changelog#2020-jun-18)
- [2020-JUN-17](https://docs.cdp.coinbase.com/exchange/docs/changelog#2020-jun-17)
- [2020-JUN-15](https://docs.cdp.coinbase.com/exchange/docs/changelog#2020-jun-15)
- [2020-JUN-12](https://docs.cdp.coinbase.com/exchange/docs/changelog#2020-jun-12)
- [2020-APR-27](https://docs.cdp.coinbase.com/exchange/docs/changelog#2020-apr-27)
- [2020-FEB-20](https://docs.cdp.coinbase.com/exchange/docs/changelog#2020-feb-20)
- [2020-FEB-10](https://docs.cdp.coinbase.com/exchange/docs/changelog#2020-feb-10)
- [2019-DEC-16](https://docs.cdp.coinbase.com/exchange/docs/changelog#2019-dec-16)
- [2019-SEP-30](https://docs.cdp.coinbase.com/exchange/docs/changelog#2019-sep-30)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_travel_rule_withdrawals.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/travel-rule-withdrawals#__docusaurus_skipToContent_fallback)

The Travel Rule requires financial institutions, including custodial cryptocurrency exchanges, to share basic information about their customers when sending funds over a certain amount.

VASPs (Virtual Asset Service Providers) like Coinbase that are part of the TRUST (Travel Rule Universal Solution Technology) consortium use the [TRUST solution](https://www.coinbase.com/travelrule) when sharing PII (Personally Identifiable Information) in order to satisfy the Travel Rule data requirements.

The [Withdraw to crypto address](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postwithdrawcrypto) endpoint supports the Travel Rule as follows:

**Coinbase as a VASP**

Depending on the jurisdiction, you may be required to provide data related to the beneficiary of the withdrawal.

Users in travel-rule jurisdictions can only withdraw to addresses that have been added to their address-book. In such cases, the `travel_rule_data` is obtained from the address-book.
Please note that [`post /address-book`](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postaddressbook)) has fields to support this.

Example request:

```codeBlockLines_p187
curl -L -X POST 'https://api.exchange.coinbase.com/withdrawals/crypto' \
-H "Content-Type: application/json" \
-d "@data.json"

```

`data.json` content:

```codeBlockLines_p187
{
  "amount": "1.0",
  "currency": "BTC",
  "crypto_address": "1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa"
}

```

**Coinbase as an intermediary VASP**

Customers can reach out to client-services to use coinbase as an intermediary VASP.

When Coinbase is used as an intermediary VASP to send crypto on behalf of your customer, you must provide the `is_intermediary` parameter with a value of `true`.
It is also necessary to provide the `travel_rule_data` parameter with the data necessary to satisfy the Travel Rule data requirements.

You must attest that you have verified the ownership of the wallet address being withdrawn to, and that you are sending the funds on behalf of your customer by sending: `attest_verified_wallet_ownership = true`

Example of a request with Travel Rule data when Coinbase is an intermediary VASP:

```codeBlockLines_p187
curl -L -X POST 'https://api.exchange.coinbase.com/withdrawals/crypto' \
-H "Content-Type: application/json" \
-d "@data.json"

```

`data.json` content:

```codeBlockLines_p187
{
  "amount": "1.00",
  "currency": "ETH",
  "crypto_address": "0x111111111117dc0aa78b770fa6a738034120c000",
  "travel_rule_data": {
    "originator_name": "customer name",
    "originator_personal_id": "customer personal id",
    "originator_address": {
      "address_1": "customer address 1",
      "city": "San Francisco",
      "state": "CA",
      "country": "US",
      "postal_code": "94102"
    },
    "originator_account": "customer accountID",
    "originator_account_number": "12345",
    "beneficiary_name": "beneficiary name",
    "beneficiary_address": {
      "country": "US"
    },
    "is_self": "true",
    "wallet_type": "WALLET_TYPE_SELF_HOSTED",
    "originating_vasp_for_intermediary": {
      "attest_verified_wallet_ownership": "true"
    }
  }
}

```

**Error responses for missing Travel Rule data**

When the required Travel Rule data has not been provided for a given jurisdiction, an error response will be received, such as the following (HTTP status code 400):

```codeBlockLines_p187
{
  "message": "missing fields to satisfy travel rule requirements",
  "missing_fields": ["beneficiary_name", "beneficiary_address", "originator_name"]
}

```

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_rest_rate_limits.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/rest-rate-limits#__docusaurus_skipToContent_fallback)

Public endpoints are throttled by IP and private endpoints by profile ID. Some endpoints (like `/fills`) may have custom rate limits.

When a REST API rate limit is exceeded, a status of `429 Too Many Requests` is returned.

#### Public Endpoints [](https://docs.cdp.coinbase.com/exchange/docs/rest-rate-limits\#public-endpoints "Direct link to Public Endpoints")

- Requests per second per IP: 10
- Requests per second per IP in bursts: Up to 15

#### Private Endpoints [](https://docs.cdp.coinbase.com/exchange/docs/rest-rate-limits\#private-endpoints "Direct link to Private Endpoints")

Private endpoints are authenticated.

- Requests per second per profile: 15
- Requests per second per profile in bursts: Up to 30

#### Private `/fills` Endpoint [](https://docs.cdp.coinbase.com/exchange/docs/rest-rate-limits\#private-fills-endpoint "Direct link to private-fills-endpoint")

- Requests per second per profile: 10
- Requests per second per profile in bursts: Up to 20

#### Private `/loans` Endpoint [](https://docs.cdp.coinbase.com/exchange/docs/rest-rate-limits\#private-loans-endpoint "Direct link to private-loans-endpoint")

- Requests per second per profile: 10



Info

Rate limits do not apply to [List loan assets](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getloanassets) ( `/loans/assets`) which is not private.

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_welcome.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/welcome#__docusaurus_skipToContent_fallback)



FIX 4.2 Order Entry Gateway Deprecation

FIX 4.2 Order Entry Gateway will be deprecated on **June 3rd, 2025**. For FIX based order entry, **leverage the newer, more performant** [FIX 5 Order Entry Gateway](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50).

Welcome to Coinbase Exchange API documentation for traders and developers! The APIs are separated into two categories, trading and market data:

- **Trading APIs** require authentication and let you place orders and access account information.
- **Market Data APIs** provide market data and are public.

Coinbase Exchange offers multiple connectivity options tailored to your trading and data needs:

- [REST API](https://docs.cdp.coinbase.com/exchange/docs/rest-requests) for lower-frequency trading and general requests.
- [FIX Order Entry API](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50) for higher-frequency trading.
- [WebSocket Feed](https://docs.cdp.coinbase.com/exchange/docs/websocket-overview) for market data.
- [FIX Market Data API](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data) for latency sensitive market data feeds.

Exchange's developer docs are part of [Coinbase Developer Platform](https://docs.cdp.coinbase.com/), the single portal from which to access Coinbase's full suite of APIs and blockchain infrastructure products.



Info

By accessing the Exchange Market Data API, you agree to be bound by the [Market Data Terms of Use](https://www.coinbase.com/legal/market_data).

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_types.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/types#__docusaurus_skipToContent_fallback)

## Timestamps [](https://docs.cdp.coinbase.com/exchange/docs/types\#timestamps "Direct link to Timestamps")

```codeBlockLines_p187
2014-11-06T10:34:47.123456Z

```

Unless otherwise specified, all timestamps from API are returned in [ISO 8601](http://en.wikipedia.org/wiki/ISO_8601) with microseconds. Make sure you can parse the following ISO 8601 format. Most modern languages and libraries handle this without issues.

## Numbers [](https://docs.cdp.coinbase.com/exchange/docs/types\#numbers "Direct link to Numbers")

Decimal numbers are returned as strings to preserve full precision across platforms. When making a request, it is recommended that you also convert your numbers to strings to avoid truncation and precision errors.

Integer numbers (such as trade id and sequence) are unquoted.

## IDs [](https://docs.cdp.coinbase.com/exchange/docs/types\#ids "Direct link to IDs")

Most identifiers are UUID unless otherwise specified. When making a request which requires a UUID, both forms (with and without dashes) are accepted.

`132fb6ae-456b-4654-b4e0-d681ac05cea1` or `132fb6ae456b4654b4e0d681ac05cea1`

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Timestamps](https://docs.cdp.coinbase.com/exchange/docs/types#timestamps)
- [Numbers](https://docs.cdp.coinbase.com/exchange/docs/types#numbers)
- [IDs](https://docs.cdp.coinbase.com/exchange/docs/types#ids)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_fix_best_practices.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/fix-best-practices#__docusaurus_skipToContent_fallback)

## Optimize Traffic [](https://docs.cdp.coinbase.com/exchange/docs/fix-best-practices\#optimize-traffic "Direct link to Optimize Traffic")

To optimize your FIX set up, spread traffic over as many portfolios as possible to minimize order-entry latencies.

You should adhere to the following:

- 1 API key per session/connection to guarantee a connection
- 75 maximum connections per profile
- 175 maximum connections per user across all profiles

## Batch Messages [](https://docs.cdp.coinbase.com/exchange/docs/fix-best-practices\#batch-messages "Direct link to Batch Messages")

We strongly recommend batch messages for both order entry and cancellation.

Batch Requests:

- Can have up to 15 orders / cancels per request.
- Only count for a single message for the purposes of rate limiting.
- Can be more efficient to process compared to the equivalent individual requests.

Available batch messages are:

- [New Order Batch (U6)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#new-order-batch-u6)
- [Order Cancel Batch Request (U4)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#order-cancel-batch-request-u4)
- [New Order Batch Reject (U7)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#new-order-batch-reject-u7)
- [Order Cancel Batch Reject (U5)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#order-cancel-batch-reject-u5)

## Modify Order Requests [](https://docs.cdp.coinbase.com/exchange/docs/fix-best-practices\#modify-order-requests "Direct link to Modify Order Requests")

We strongly recommend [Modify Order Requests](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#modify-order-request-g) where applicable.

Modify Order Requests:

- Keep your place in the order book queue when size is amended down.
- Result in 50% fewer messages when compared to canceling an existing order and placing a new one.
- Reduce your overall rate limit usage when compared to sending a cancellation followed by a new order.
- Can be more efficient to process compared to the equivalent individual cancel and new order requests.

For rate limits, see [FIX API Rate Limits](https://docs.cdp.coinbase.com/exchange/docs/fix-rate-limits).

## Drop Copy Session [](https://docs.cdp.coinbase.com/exchange/docs/fix-best-practices\#drop-copy-session "Direct link to Drop Copy Session")

Enabling DropCopyFlag="Yes" ( `9406=Y`) configures your session to receive execution reports across all active sessions for the same profile.

We recommend that you enable DropCopyFlag on a **separate, read-only session**:

- Execution latencies are higher for Drop Copy sessions because the same connection handles more read traffic.
- Multiple Drop Copy sessions produce multiple copies of redundant data.

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Optimize Traffic](https://docs.cdp.coinbase.com/exchange/docs/fix-best-practices#optimize-traffic)
- [Batch Messages](https://docs.cdp.coinbase.com/exchange/docs/fix-best-practices#batch-messages)
- [Modify Order Requests](https://docs.cdp.coinbase.com/exchange/docs/fix-best-practices#modify-order-requests)
- [Drop Copy Session](https://docs.cdp.coinbase.com/exchange/docs/fix-best-practices#drop-copy-session)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_rest_auth.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/rest-auth#__docusaurus_skipToContent_fallback)

This page explains how to sign and authenticate REST API endpoints with API keys that let you control authorization.



Note

See [FIX API Connectivity](https://docs.cdp.coinbase.com/exchange/docs/fix-connectivity) for FIX API authentication.

## Private Endpoints [](https://docs.cdp.coinbase.com/exchange/docs/rest-auth\#private-endpoints "Direct link to Private Endpoints")

Private endpoints are available for order management and account management. Every private request must be signed using the described authentication scheme.



Info

Private endpoints require authentication using your Coinbase Exchange API key. You can generate API keys [here](https://exchange.coinbase.com/profile/api).

## API Keys [](https://docs.cdp.coinbase.com/exchange/docs/rest-auth\#api-keys "Direct link to API Keys")

To sign a request, you must create an API key via the Coinbase Exchange website. The API key is scoped to a specific profile. Each user can generate a max of 300 API keys.

### Generating an API Key [](https://docs.cdp.coinbase.com/exchange/docs/rest-auth\#generating-an-api-key "Direct link to Generating an API Key")

When creating a key, you must remember (and should write down) your (1) key, (2) secret, and (3) passphrase. The key and secret are randomly generated and provided by Coinbase Exchange -- you choose a passphrase to further secure your API access.



Warning

Coinbase Exchange stores the salted hash of your passphrase for verification and cannot be recovered if you forget it.

### API Key Permissions [](https://docs.cdp.coinbase.com/exchange/docs/rest-auth\#api-key-permissions "Direct link to API Key Permissions")

You can control access by restricting the functionality of API keys. Before creating the key, you must choose what permissions you would like the key to have:

| Permission | Description |
| --- | --- |
| View | Key has read permissions for all endpoints (including GET) |
| Transfer | Key can transfer value for accounts, including deposits/withdrawals (and bypasses 2FA) |
| Trade | Key can post orders and get data |
| Manage | Key can manage user settings and preferences such as address books entries |

Refer to the documentation below to see what API key permissions are required for a specific route.

## Signing Requests [](https://docs.cdp.coinbase.com/exchange/docs/rest-auth\#signing-requests "Direct link to Signing Requests")

All REST requests must contain the following headers:

| Header | Description |
| --- | --- |
| `CB-ACCESS-KEY` | API key as a string |
| `CB-ACCESS-SIGN` | base64-encoded signature (see [Signing a Message](https://docs.cdp.coinbase.com/exchange/docs/rest-auth#signing-a-message)) |
| `CB-ACCESS-TIMESTAMP` | Timestamp for your request |
| `CB-ACCESS-PASSPHRASE` | Passphrase you specified when creating the API key |

All request bodies should have content type `application/json` and be valid JSON.

### Selecting a Timestamp [](https://docs.cdp.coinbase.com/exchange/docs/rest-auth\#selecting-a-timestamp "Direct link to Selecting a Timestamp")

The `CB-ACCESS-TIMESTAMP` header MUST be number of seconds since [Unix Epoch](http://en.wikipedia.org/wiki/Unix_time) in UTC. Decimal values are allowed.

Your timestamp must be within 30 seconds of the API service time or your request is considered expired and rejected. We recommend using the [time](https://api.exchange.coinbase.com/time) endpoint to query for the API server time if you believe there is a time difference between your server and the API servers.

### Signing a Message [](https://docs.cdp.coinbase.com/exchange/docs/rest-auth\#signing-a-message "Direct link to Signing a Message")

The `CB-ACCESS-SIGN` header is generated by creating a sha256 HMAC using the base64-decoded secret key on the prehash string `timestamp + method + requestPath + body` (where `+` represents string concatenation) and base64-encode the output.



Info

Remember to base64-decode the alphanumeric secret string (resulting in 64 bytes) before using it as the key for HMAC. Also, base64-encode the digest output before sending in the header.

- `timestamp` is the same as the `CB-ACCESS-TIMESTAMP` header.

- `method` should be UPPER CASE e.g., `GET` or `POST`.

- `requestPath` should only include the path of the API endpoint.

- `body` is the request body string or omitted if there is no request body (typically for `GET` requests).


### Signature Example [](https://docs.cdp.coinbase.com/exchange/docs/rest-auth\#signature-example "Direct link to Signature Example")

The following example demonstrates how to generate a signature in Javascript:

```codeBlockLines_p187
// import crypto library
var crypto = require("crypto");

// create the json request object
var cb_access_timestamp = Date.now() / 1000; // in ms
var cb_access_passphrase = "...";
var secret = "PYPd1Hv4J6/7x...";
var requestPath = "/orders";
var body = JSON.stringify({
  price: "1.0",
  size: "1.0",
  side: "buy",
  product_id: "BTC-USD",
});
var method = "POST";

// create the prehash string by concatenating required parts
var message = cb_access_timestamp + method + requestPath + body;

// decode the base64 secret
var key = Buffer.from(secret, "base64");

// create a sha256 hmac with the secret
var hmac = crypto.createHmac("sha256", key);

// sign the require message with the hmac and base64 encode the result
var cb_access_sign = hmac.update(message).digest("base64");

```

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Private Endpoints](https://docs.cdp.coinbase.com/exchange/docs/rest-auth#private-endpoints)
- [API Keys](https://docs.cdp.coinbase.com/exchange/docs/rest-auth#api-keys)
  - [Generating an API Key](https://docs.cdp.coinbase.com/exchange/docs/rest-auth#generating-an-api-key)
  - [API Key Permissions](https://docs.cdp.coinbase.com/exchange/docs/rest-auth#api-key-permissions)
- [Signing Requests](https://docs.cdp.coinbase.com/exchange/docs/rest-auth#signing-requests)
  - [Selecting a Timestamp](https://docs.cdp.coinbase.com/exchange/docs/rest-auth#selecting-a-timestamp)
  - [Signing a Message](https://docs.cdp.coinbase.com/exchange/docs/rest-auth#signing-a-message)
  - [Signature Example](https://docs.cdp.coinbase.com/exchange/docs/rest-auth#signature-example)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_fix_msg_order_entry.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#__docusaurus_skipToContent_fallback)



FIX 4.2 Order Entry Gateway Deprecation

FIX 4.2 Order Entry Gateway will be deprecated on **June 3rd, 2025**. For FIX based order entry, **leverage the newer, more performant** [FIX 5 Order Entry Gateway](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50).

About this API:

- **Baseline**: [FIX 4.2 SP2 specification](https://www.onixs.biz/fix-dictionary/4.2/index.html). Includes tags from later FIX versions plus custom tags in the high number range as allowed by the standard.
- **Environments**: Production, Sandbox



Environment URLs

- Production: `tcp+ssl://fix.exchange.coinbase.com:4198`
- Sandbox: `tcp+ssl://fix-public.sandbox.exchange.coinbase.com:4198`

A standard header must be present at the start of every message in both directions.

| Tag | Name | Description |
| --- | --- | --- |
| 8 | BeginString | Must be `FIX.4.2` |
| 49 | SenderCompID | Client API key (on messages from the client) |
| 56 | TargetCompID | Must be `Coinbase` (on messages from the client) |
| 999 | CoinbaseProductSeq | Response header only (returned on [Execution Reports](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#execution-report-8)). Represents market sequence. |



Caution

[New orders](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#new-order-single-d) can only be placed when the number of open orders is below 500 for that given product.

## Logon (A) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#logon-a "Direct link to Logon (A)")

Sent by the client to initiate a session and by the server as an acknowledgement. Only one session may exist per connection; sending a Logon message within an established session is an error.

| Tag | Name | Description |
| --- | --- | --- |
| 34 | MsgSeqNum | Must be `1` |
| 98 | EncryptMethod | Must be `0` (None) |
| 108 | HeartBtInt | Must be ≤ `30` (secs). Values greater are capped at `30`. Server sends Test Request if client messages are not received in approximately (HeartBtInt x 1.5) seconds. Server terminates session if client messages are not received in approximately (HeartBtInt x 2 seconds). |
| 141 | ResetSeqNumFlag | If set to `Y`, reset sequence numbers for both sides of the FIX session. |
| 554 | Password | Client API passphrase |
| 96 | RawData | Client message signature (see below) |
| 8013 | CancelOrdersOnDisconnect | `S`: Batch cancel all open orders placed during session; `Y`: Batch cancel all open orders for the current profile. The latter is more performant and recommended. |
| 9406 | DropCopyFlag | If set to `Y`, execution reports are generated for all user orders (defaults to `Y`). |

The Logon message sent by the client must be signed for security. The signing method is described in [Signing a Message](https://docs.cdp.coinbase.com/exchange/docs/rest-auth#signing-a-message). The prehash string is the following fields joined by the FIX field separator (ASCII code 1):

`SendingTime, MsgType, MsgSeqNum, SenderCompID, TargetCompID, Password`.

There is no trailing separator. The `RawData` field should be a base64 encoding of the HMAC signature.

```codeBlockLines_p187
// create a new Logon message
var logon = new Msgs.Logon();
logon.SendingTime = new Date();
logon.HeartBtInt = 30;
logon.EncryptMethod = 0;
logon.passphrase = "...";

var presign = [\
  logon.SendingTime,\
  logon.MsgType,\
  session.outgoing_seq_num,\
  session.sender_comp_id,\
  session.target_comp_id,\
  passphrase,\
].join("\x01");

// add the presign string to the RawData field of the Logon message
logon.RawData = sign(presign, secret);

// send the logon message to the server
session.send(logon);

function sign(what, secret) {
  var key = Buffer.from(secret, "base64");
  var hmac = crypto.createHmac("sha256", key);
  return hmac.update(what).digest("base64");
}

```



Caution

To establish multiple FIX connections, generate a new API key for each one. The maximum is 75 connections per profile. Do not use a single API key for multiple connections at the same time.



Caution

The value of `SendingTime` must be within 5 minutes of server time in UTC.

## Logout (5) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#logout-5 "Direct link to Logout (5)")

Sent by either side to initiate session termination. The side which receives this message first should reply with the same message type to confirm session termination.



Caution

Do not close a connection without logging out of the session first or it triggers an error.

## New Order Single (D) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#new-order-single-d "Direct link to New Order Single (D)")

Sent by the client to enter an order. Each profile can place a maximum of 500 open orders on a product. Once reached, the profile cannot place any new orders until the total number of open orders is below 500 .

| Tag | Name | Description |
| --- | --- | --- |
| 11 | ClOrdID | UUID selected by client to identify the order <br>This shouldn't match the ClOrdID of any open orders. |
| 55 | Symbol | Required symbol to identify the new order, e.g., `BTC-USD` |
| 54 | Side | Must be `1` to buy or `2` to sell |
| 44 | Price | Limit price (e.g., in USD) (Limit order only) |
| 38 | OrderQty | Order size in base units (e.g., BTC) |
| 152 | CashOrderQty | Order size in quote units (e.g., USD) (Market or [Limit order](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-lwf) only) |
| 40 | OrdType | Must be `1` for Market, `2` for Limit, `4` for Stop Limit, `O` for [Take Profit Stop Loss](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-tpsl) |
| 99 | StopPx | Stop price for order |
| 59 | TimeInForce | Must be a valid TimeInForce value. See the table below (Limit order only) |
| 111 | MaxFloor | Maximum size within an order to be displayed. Must be > 10% of OrderQty |
| 126 | ExpireTime | Time/Date (in UTC) of order expiration for Good Till Date (GTD) only. The order expires within one second after the specified time. |
| 1109 | TriggerPriceDirection | The side from which the trigger price (or **last trade price**) is reached. <br>Valid values: <br>- U = Trigger if price goes UP to or through specified Trigger Price.<br>- D = Trigger if price goes DOWN to or through specified Trigger Price.<br>**Note:** If OrdType = 4, 1109 is highly recommended. If OrdType != 4, 1109 is not needed. |
| 7928 | SelfTradePrevention | Optional, see the table below |

### SelfTradePrevention Values [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#selftradeprevention-values "Direct link to SelfTradePrevention Values")

| Value | Description |
| --- | --- |
| `D` | Decrement and cancel (the default) |
| `O` | Cancel resting order |
| `N` | Cancel incoming order |
| `B` | Cancel both orders |

If an order is decremented due to self-trade prevention, an Execution Report is sent to the client with `ExecType=D` indicating unsolicited `OrderQty` reduction (i.e., partial cancel).

See the [self-trade prevention](https://docs.cdp.coinbase.com/exchange/docs/matching-engine#self-trade-prevention) documentation for more details about this field.

### Time In Force Values [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#time-in-force-values "Direct link to Time In Force Values")

| Value | Policy | Abbr |
| --- | --- | --- |
| `1` | Good Till Cancel | GTC |
| `3` | Immediate or Cancel | IOC |
| `4` | Fill or Kill | FOK |
| `6` | Good Till Date (90-day hard limit) | GTD |
| `P` | Post-Only (GTC & make liquidity only) |  |



Post-Only

The post-only flag ( `P`) indicates that the order should only make liquidity. If any part of the order results in taking liquidity, the order is rejected and no part of it executes. Open Post-Only orders are treated as Good Till Cancel.

See the [Time In Force](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postorders#time-in-force) documentation for more details about these values.

### Errors [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#errors "Direct link to Errors")

If a trading error occurs (for example, the user has insufficient funds), an Execution Report with `ExecType=8` is sent back, signifying that the order was rejected.

### Iceberg Orders [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#iceberg-orders "Direct link to Iceberg Orders")

See [Iceberg Orders](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-iceberg).

### Take Profit Stop Loss Orders [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#take-profit-stop-loss-orders "Direct link to Take Profit Stop Loss Orders")

See [TPSL Orders](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-tpsl).

### Limit With Funds Orders [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#limit-with-funds-orders "Direct link to Limit With Funds Orders")

See [Limit With Funds Orders](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-lwf).

## New Order Batch (U6) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#new-order-batch-u6 "Direct link to New Order Batch (U6)")

Sent by the client to create multiple orders. Maximum of 15 orders per message. All orders must have the same symbol.

Each profile can place a maximum of 500 open orders on a product. Once reached, the profile cannot place any new orders until the total number of open orders is below 500 . If the total number of open orders in the batch causes the profile to exceed the 500 maximum, the entire batch is rejected.

| Tag | Name | Description |
| --- | --- | --- |
| 8014 | BatchID | UUID selected by client to identify this New Order Batch request |
| 73 | NoOrders | Number of orders in this message (number of repeating groups to follow). Must be less than or equal to 15. |
| 11 | ClOrdID | UUID selected by client for the order. Must be the first field in the repeating group. <br>This shouldn't match the ClOrdID of any open orders. Additionally, it shouldn't match any other ClOrdIDs in this batch. |
| 55 | Symbol | Required symbol to identify the new order (e.g., `BTC-USD`) |
| 54 | Side | Must be `1` to buy or `2` to sell |
| 44 | Price | Limit price (e.g., in USD) |
| 38 | OrderQty | Order size in base units (e.g., BTC) |
| 40 | OrdType | Must be `2` for Limit |
| 59 | TimeInForce | Must be a valid [TimeInForce value](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#time-in-force-values) |
| 126 | ExpireTime | Time/Date (in UTC) of order expiration for Good Till Date (GTD) only. The order expires within one second after the specified time. |
| 7928 | SelfTradePrevention | Optional, see the table above |

## Order Cancel Request (F) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#order-cancel-request-f "Direct link to Order Cancel Request (F)")

Sent by the client to cancel an order.

| Tag | Name | Description |
| --- | --- | --- |
| 11 | ClOrdID | UUID selected by client to identify this cancel request |
| 37 | OrderID | OrderID from the ExecutionReport with OrdStatus=New (39=0) |
| 41 | OrigClOrdID | ClOrdID from the New Order Single. When supplying this value, you do not need to supply an OrderID. |
| 55 | Symbol | Required symbol of the order to cancel (must match Symbol of the Order). |
| 58 | Text | Free format text string |

## Order Status Request (H) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#order-status-request-h "Direct link to Order Status Request (H)")

Sent by the client to obtain information about pending and done orders.

| Tag | Name | Description |
| --- | --- | --- |
| 37 | OrderID | OrderID of order to be sent back. |
| 11 | ClOrdID | ClOrdID of order to be sent back. When supplying this value, you do not need to supply an OrderID. |
| 55 | Symbol | Required symbol to identify the order, e.g., `BTC-USD` |

### Response [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#response "Direct link to Response")

The response to an Order Status Request is an ExecutionReport with `ExecType=I`. The ExecutionReport contains the `ClOrdID` if the value is supplied. If the order cannot be found, the ExecutionReport has `OrderID=0`.

## Order Cancel Batch Request (U4) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#order-cancel-batch-request-u4 "Direct link to Order Cancel Batch Request (U4)")

Sent by the client to cancel multiple orders. Maximum of 15 orders per message. All orders must have the same symbol.

| Tag | Name | Description |
| --- | --- | --- |
| 8014 | BatchID | UUID selected by client to identify this Order Batch Cancel Request |
| 73 | NoOrders | Number of orders in this message (number of repeating groups to follow). Must be less than or equal to 15. |
| 41 | OrigClOrdID | UUID selected by client for the order. Must be the first field in the repeating group. |
| 55 | Symbol | Required symbol of the order to cancel (must match Symbol of the Order) |
| 37 | OrderID | OrderID from the ExecutionReport with OrdStatus=New (39=0). If present, this field takes precedence over OrigClOrdID to identify the order (optional). |
| 11 | ClOrdID | UUID selected by client to identify this cancel request |

### Response [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#response-1 "Direct link to Response")

When the message is invalid or an unexpected error occurs, an Order Cancel Batch Reject (U5) message is sent. When orders are cancelled, an Execution Report (8) is sent for each order canceled. When Order Cancel Batch Request (U4) is partially rejected (i.e., some orders are filled or already canceled), Order Cancel Reject (9) is sent for each rejected cancel.

## Execution Report (8) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#execution-report-8 "Direct link to Execution Report (8)")

Sent by the server when an order is accepted, rejected, filled, or canceled. Also sent when the user sends an `OrderStatusRequest`.

| Tag | Name | Description |
| --- | --- | --- |
| 6 | AvgPx | Calculated average price of all fills on this order. Only populates Exec Report if CumQty > 0 |
| 11 | ClOrdID | Only present on order acknowledgements, ExecType=New (150=0) |
| 14 | CumQty | Currently executed quantity for chain of orders. Populates Exec Report when: <br>- `39=0` ⇒ OrdStatus = New<br>- `39=1` ⇒ OrdStatus = Partially filled<br>- `39=3` ⇒ OrdStatus = Done for day<br>- `39=5` ⇒ OrdStatus = Replaced |
| 17 | ExecID | Unique identifier of execution message as assigned by broker |
| 37 | OrderID | OrderID from the ExecutionReport with ExecType=New (150=0) |
| 39 | OrdStatus | Order status as of the current message |
| 55 | Symbol | Symbol of the original order |
| 54 | Side | Must be `1` to buy or `2` to sell |
| 32 | LastShares | Amount filled (if ExecType=1). Also called LastQty as of FIX 4.3 |
| 44 | Price | Price of the fill if ExecType indicates a fill, otherwise the order price |
| 38 | OrderQty | OrderQty as accepted (may be less than requested upon self-trade prevention). Represents original order quantity when `OrdStatus` is Canceled or Done for day. |
| 111 | MaxFloor | Maximum size within an order to be displayed. Must be > 10% of OrderQty |
| 198 | SecondaryOrderID | Assigned by the party that accepts the order. Can be used to provide the OrderID (37) used by an exchange or executing system. |
| 58 | Text | Human-readable description of the reject or cancel (optional) <br>- 101:Time In Force<br>- 102:Self-trade Prevention<br>- 103:Admin<br>- 104:Price Bound Order Protection<br>- 105:Insufficient Funds<br>- 106:Insufficient Liquidity<br>- 107:Broker<br>- 109:High Bid Limit Order Protection |
| 60 | TransactTime | Time the event occurred |
| 103 | OrdRejReason | Insufficient funds= `3`, Post-only= `8`, Unknown error= `0` |
| 136 | NoMiscFees | `1` (Order Status Request responses and fill reports) |
| 137 | MiscFeeAmt | Fee amount (absolute value for Order Status Request responses, percentage value for fill reports) |
| 138 | MiscFeeCurr | Fee currency |
| 139 | MiscFeeType | `4` (Exchange fees) (Order Status Request responses and fill reports) |
| 150 | ExecType | May be `1` (Partial fill) for fills, `D` for self-trade prevention, etc. |
| 151 | LeavesQty | Quantity open for further execution. Populates Exec Report when: <br>- `39=0` ⇒ OrdStatus = New<br>- `39=1` ⇒ OrdStatus = Partially filled<br>- `39=3` ⇒ OrdStatus = Done for day<br>- `39=5` ⇒ OrdStatus = Replaced |
| 152 | CashOrderQty | Order size in quote units (e.g., USD) (Market order only) |
| 891 | MiscFeeBasis | `2` (Percentage fee basis) (fill report only) |
| 1003 | TradeID | Product unique trade id |
| 1057 | AggressorIndicator | `Y` for taker orders, `N` for maker orders |

### ExecType Values [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#exectype-values "Direct link to ExecType Values")

| ExecType | Description |
| --- | --- |
| `0` | New Order |
| `1` | Partial Fill |
| `3` | Done |
| `4` | Canceled |
| `7` | Stopped |
| `8` | Rejected |
| `D` | Restated (Order Changed due to STP) |
| `I` | Order Status |

## New Order Batch Reject (U7) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#new-order-batch-reject-u7 "Direct link to New Order Batch Reject (U7)")

Sent by the server when a New Order Batch message is rejected.

| Tag | Name | Description |
| --- | --- | --- |
| 8014 | BatchID | BatchID from the New Order Batch message |
| 58 | Text | Human-readable description of the error (optional) |

## Modify Order Request (G) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#modify-order-request-g "Direct link to Modify Order Request (G)")

Supports the [Order Replace Request](https://www.onixs.biz/fix-dictionary/4.2/msgtype_g_71.html) outlined in the FIX protocol. See also: [WebSocket Full Channel, Change](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#change).



Caution

Each Modify Order Request, per order, must be processed in turn. A client can only send a Modify Order Request after the previous request for the same order has been fully processed.

Example FIX Request:

```codeBlockLines_p187
 BeginString=FIX.4.2 BodyLength=265 MsgType=ORDER_CANCEL_REPLACE_REQUEST MsgSeqNum=17 SenderCompID=00000000100000000000000000000003 SendingTime=20220609-04:01:48.757 TargetCompID=Coinbase ClOrdID=907b6ae6-bcbe-441a-b7bb-d932afdb9edb OrderID=71de0cdf-938f-495b-9fad-108837bde704 OrderQty=2 OrdType=LIMIT OrigClOrdID=907b6ae6-bcbe-441a-b7bb-d932afdb9eda Price=100.00 Side=BUY Symbol=ETH-USD TransactTime=20220609-04:01:48.757 CheckSum=107

```

Example Execution Report:

```codeBlockLines_p187
BeginString=FIX.4.2 BodyLength=253 MsgType=EXECUTION_REPORT MsgSeqNum=18 SenderCompID=Coinbase SendingTime=20220609-04:01:48.766 TargetCompID=00000000100000000000000000000003 ExecID=450d0b12-e994-48de-9f74-0f43c74fd054 ExecTransType=NEW OrderID=71de0cdf-938f-495b-9fad-108837bde704 OrderQty=3 OrdStatus=DONE_FOR_DAY Price=100 Side=BUY Symbol=ETH-USD Text=107:Broker TransactTime=20220609-04:01:48.762 ExecType=DONE_FOR_DAY LeavesQty=0 CheckSum=150

```

| Tag | Name | Description |
| --- | --- | --- |
| 37 | OrderID | Unique identifier of most recent order as assigned by broker <br>This shouldn't match the ClOrdID of any open orders. |
| 41 | OrigClOrdID | `ClOrdID <11>` of previous order (NOT initial order of the day) when canceling or replacing an order |
| 11 | ClOrdID | Unique identifier of replacement order as assigned by institution. |
| 55 | Symbol | Must match original order |
| 54 | Side | Must match original side |
| 38 | OrderQty | Total Intended Order Quantity (including the amount already executed for this chain of orders) |
| 60 | TransactTime | Time this order request was initiated/released by the trader or trading system |
| 40 | OrdType | Only limit orders are supported for now (2) |
| 44 | Price | Price per share |

### Guidance [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#guidance "Direct link to Guidance")

#### Queue Priority [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#queue-priority "Direct link to Queue Priority")

- If you increase the quantity, or modify the price (up or down) you **lose your place and move to the back of the queue**. If you decrease the quantity you keep your place in the queue.

#### OrderQty (38) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#orderqty-38 "Direct link to OrderQty (38)")

- If you send a Modify Order request whose `OrderQty (38)` is less than the filled size of the order, **Coinbase cancels the order and marks it as filled**.

#### Matching [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#matching "Direct link to Matching")

- If your Modify Order request results in an **immediate match** and you are both the **initiator of the order** AND **subscribed to the authenticated WebSocket feed**, you should receive a change message with `"reason": "modify_order"`.

After the immediate match, if there is any **quantity remaining** on the modified order, you should receive a new change message with `"reason":"remainder_after_modification"` which reports the new / old prices as a result of the Modify Order.

- If you are **using the non-authenticated WebSocket feed** (as the initiator or not), you should receive a `match + done` message for the order at the newly modified price.




Caution

Clients may experience a non-standard FIX `OrderCancelReject` with text (when processing the last cancel replace request). This can occur when our system is backlogged and unable to process this Modify Order Request (or `OrderCancelReplaceRequest`).

## Order Cancel Reject (9) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#order-cancel-reject-9 "Direct link to Order Cancel Reject (9)")

Sent by the server when an Order Cancel Request cannot be satisfied, e.g., because the order is already canceled or completely filled.

| Tag | Name | Description |
| --- | --- | --- |
| 11 | ClOrdID | As on the cancel request |
| 37 | OrderID | As on the cancel request |
| 41 | OrigClOrdID | As on the cancel request |
| 39 | OrdStatus | `4` if too late to cancel |
| 102 | CxlRejReason | `1` if the order is unknown |
| 434 | CxlRejResponseTo | `1` (Order Cancel Request) |

## Order Cancel Batch Reject (U5) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#order-cancel-batch-reject-u5 "Direct link to Order Cancel Batch Reject (U5)")

Sent by the server when an Order Cancel Batch Request cannot be satisfied, e.g., because a Symbol was not present. This is not sent if no orders can be found.

| Tag | Name | Description |
| --- | --- | --- |
| 8014 | BatchID | BatchID from the New Order Batch message |
| 58 | Text | Human-readable description of the error (optional) |

## Reject (3) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#reject-3 "Direct link to Reject (3)")

Sent by either side upon receipt of a message which cannot be processed, e.g., due to missing fields or an unsupported message type.

| Tag | Name | Description |
| --- | --- | --- |
| 45 | RefSeqNum | MsgSeqNum of the rejected incoming message |
| 371 | RefTagID | Tag number of the field which caused the reject (optional) |
| 372 | RefMsgType | MsgType of the rejected incoming message |
| 58 | Text | Human-readable description of the error (optional) |
| 373 | SessionRejectReason | Code to identify reason for reject |

### SessionRejectReason Values [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#sessionrejectreason-values "Direct link to SessionRejectReason Values")

The following values can be sent by the server.

| Value | Description |
| --- | --- |
| 1 | Required tag missing |
| 5 | Value is incorrect (out of range) for this tag |
| 6 | Incorrect data format for value |
| 11 | Invalid MsgType (35) |

## RFQ Request (AH) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#rfq-request-ah "Direct link to RFQ Request (AH)")

Request For Quote (RFQ) allows liquidity providers to respond and interact with real-time RFQ requests. The RFQ process begins with [Quote Request (R)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#quote-request-r).

Request For Quote is enabled for users who have been approved by Coinbase as an RFQ Liquidity Provider. Once approved, clients must send an RFQ Request message (35=AH) after each successful Logon (35=A) message for any session in which you are interested in receiving RFQ requests.

- If this request is acknowledged, and no symbol is specified, this session receives all Quote requests (all assets).
- If this request is acknowledged, and symbol is specified , this session only receives requests for the specific symbols. For instance, in the scenario of subscribing to "BTC-USD," if the related products are present, quote request message for both "BTC-USD" and "USD-BTC" will be subsequently returned as responses.
- If the session submitting this request is not approved by Coinbase for participating in the RFQ program, this request is rejected with a Business Message Reject (j).

| Tag | Name | Type | Required | Notes |
| --- | --- | --- | --- | --- |
| 644 | RFQReqID | UUID | Y |  |
| 146 | NoRelatedSym | Int32 | N | Repeating group for number of symbols in the subscription message |
| 55 | Symbol | String32 | Y |  |



Tip

_Not_ receiving a response is expected and indicative of a successful request.

### RFQ Order Protections [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#rfq-order-protections "Direct link to RFQ Order Protections")

RFQ orders are subject to price protection points (PPP) at the time a quote is accepted for execution.

At Execution time:

- If an Order Book is present, RFQs fill at prices up to the PPP from the mid-point price, between the best bid and best offer.

- If an Order Book is not present, PPPs are calculated using the same mid-point price methodology but leveraging PPP settings from the higher of the two USD equivalent Order Books for the given pair (e.g., max PPP setting for SHIB-USD and DOGE-USD for a SHIB-DOGE RFQ).


If a PPP threshold is crossed, a [QuoteStatusReport (AI)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#quote-status-report-ai) is sent indicating your Quote has been canceled.

## Quote Request (R) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#quote-request-r "Direct link to Quote Request (R)")

Quote Request (R) is the start of the RFQ process. Liquidity Providers receive a Quote Request from Coinbase on behalf of a customer looking to participate in an RFQ trade. Any quote response to this request must adhere to the following rules to avoid rejections:

- Message must be well formed and complete (i.e., all required fields present).
- [Quote](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#quote-s) message must be received before the expiration time indicated on Tag=62.

| Tag | Name | Type | Required | Notes |
| --- | --- | --- | --- | --- |
| 131 | QuoteReqID | UUID | R |  |
| 146 | NoRelatedSym | Int32 | Y | Always 1 |
| 55 | Symbol | String32 | Y | Example: `BTC-AVAX` |
| 38 | OrderQty | Float64 | Y |  |
| 62 | ValidUntilTime | UTCTimestamp | Y | UTC millis<br>`20220712-00:00:00.000` |
| 126 | ExpireTime | UTCTimestamp | Y | UTC millis<br>`20220712-00:00:00.000` |
| 303 | QuoteRequestType | Char | Y | 1 = Manual Accept<br>2 = Automatic Accept (default) |
| 891 | MiscFeeBasis | INT | Y | Always 2 = Percentage |
| 137 | MiscFeeAmt | AMT | Y | Basis point fee to market makers (MMs) |
| 528 | OrderCapacity | Char | Y | A = Agency (default) <br>C = Corporate |



Caution

QuoteRequestType (303) is always `2 = Automatic Accept` for the current implementation of RFQ on Coinbase Exchange.
MiscFeeBasis (891) is always `2 = Percentage` for the current implementation of RFQ on Coinbase Exchange.

_Request For Quote Message Flow_![Request For Quote message flow in 7 steps. (1) Customer submits RFQ; (2) Exchange sends Quote Request to liquidity provider; (3) Liquidity provider sends Quote to Exchange; (4) the Exchange responds to the liquidity provider with the Quote Status Report and (5) the Execution Report and (6) the Quote Status Report; (7) the Exchange then sends the customer a fill or cancel message.](https://docs.cdp.coinbase.com/exchange/assets/images/rfq-example.png)



Info

See also the new WebSocket [RFQ Matches Channel](https://docs.cdp.coinbase.com/exchange/docs/websocket-channels#rfq-matches-channel).

## Quote (S) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#quote-s "Direct link to Quote (S)")

Quote in response to a [Quote Request](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#quote-request-r) that can be submitted up to the `ValidUntilTime` (Tag=62) specified in the Quote Request message. The Quote can be submitted as either a one-way quote or two-way quote. Only one side is actioned on if participant wins RFQ.



Info

Precision for price and size is limited to 16 decimal places and 40 digits total.

| Tag | Name | Type | Required | Notes |
| --- | --- | --- | --- | --- |
| 131 | QuoteReqID | UUID | Y |  |
| 117 | QuoteID | UUID | Y |  |
| 55 | Symbol | String32 | Y | Example: `BTC-AVAX` |
| 132 | BidPx | Float64 | C | Required if submitting a bid |
| 133 | OfferPx | Float64 | C | Required if submitting an offer |
| 134 | BidSize | Float64 | C | Required if submitting a bid. Must match OrderQty in Quote Request |
| 135 | OfferSize | Float64 | C | Required if submitting an offer. Must match OrderQty in Quote Request |

## Quote Status Report (AI) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#quote-status-report-ai "Direct link to Quote Status Report (AI)")

\`
Message sent in response to a successful or unsuccessful Quote.

- If the Quote was accepted, QuoteStatus=16 (Active).
- If the Quote was rejected, QuoteStatus=9 (Rejected).
- If the Quote was accepted and selected for execution, QuoteStatus=19 (Pending), and you receive an Execution Report.
- If the Quote was accepted but not selected for execution, QuoteStatus=17 (Canceled).
- If there is no response to a Quote request from Liquidity Providers, QuoteStatus=7 (Expired).

| Tag | Name | Type | Required | Notes |
| --- | --- | --- | --- | --- |
| 131 | QuoteReqID | UUID | Y |  |
| 117 | QuoteID | UUID | C |  |
| 55 | Symbol | String32 | Y | Example: `BTC-AVAX` |
| 38 | OrderQty | Float64 | Y | Echoed from Quote<br>35=S |
| 132 | BidPx | Float64 | Y | Echoed from Quote<br>35=S |
| 133 | OfferPx | Float64 | Y | Echoed from Quote<br>35=S |
| 134 | BidSize | Float64 | C | Must match OrderQty in Quote Request |
| 135 | OfferSize | Float64 | C | Must match OrderQty in Quote Request |
| 62 | ValidUntilTime | UTCTimestamp | Y | UTC millis<br>`20220712-00:00:00.000` |
| 126 | ExpireTime | UTCTimestamp | Y | UTC millis<br>`20220712-00:00:00.000` |
| 297 | QuoteStatus | Int32 | Y | `5` = Rejected: Insufficient funds (in response to [35=S](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#quote-s))<br>`7` = Expired:<br>▪ Either no response to [35=S](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#quote-s) from liquidity providers<br>▪ Or best quote not accepted by counterparty<br>`16` = Active: Quote successful (in response to [35=S](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#quote-s)) <br>`17` = Canceled:<br>▪ Either quoting window expired bc quote not best<br>▪ Or RFQ was unable to hold funds<br>`19` = Pending Trade: RFQ selected for execution |
| 58 | Text | String | C | Required if QuoteStatus=5, Quote action was rejected |

## Resend Request (2) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#resend-request-2 "Direct link to Resend Request (2)")

[FIX Resend Requests](https://www.onixs.biz/fix-dictionary/4.2/msgtype_2_2.html) are sent by the receiving application to initiate the retransmission of messages.

| Tag | Name | Description |
| --- | --- | --- |
| 7 | [BeginSeqNo](https://www.onixs.biz/fix-dictionary/4.2/tagnum_7.html) | Sequence number of first message in range to be resent |
| 16 | [EndSeqNo](https://www.onixs.biz/fix-dictionary/4.2/tagnum_16.html) | Sequence number of last message in range to be resent |

### Guidance [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#guidance-1 "Direct link to Guidance")

- To successfully use replay functionality, submit a unique `senderLocationID` when logging on (because you can have multiple connections per API key).

[SenderLocationID <142>](https://www.onixs.biz/fix-dictionary/4.2/tagnum_142.html) identifies the message originator's location.

- To replay messages from a previous session, include `ResetSeqNumFlag=N` in your logon message (because, by default, we clear users sessions when logging on). You must also include the same `senderLocationID` used in the previous session to continue the session.

[ResetSeqNumFlag <141>](https://www.onixs.biz/fix-dictionary/4.2/tagnum_141.html) is a boolean flag that indicates whether or not both sides of the FIX session should reset sequence numbers.


#### Sequence Numbers [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#sequence-numbers "Direct link to Sequence Numbers")

Each request must be in batches of 2000 messages or less and lookback (the duration we keep messages) is 3 hours. For example, say you received messages in sequence range 4000-10000 within the last 3 hours:

- You can retrieve all messages from 4000 to 10000 by sending 3 requests in batches of 2000.
- You cannot retrieve messages before 4000 because of the 3 hour lookback.

#### Sample Ranges [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#sample-ranges "Direct link to Sample Ranges")

- Request single: `BeginSeqNo <7>` = `EndSeqNo <16>`
- Request range: `BeginSeqNo <7>` = first message in range; `EndSeqNo <16>` = last message in range
- Request range: `BeginSeqNo <7>` = first message in range; `EndSeqNo <16>` = 2000th message from first message ( `999999` or `0`)

## Heartbeat (0) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#heartbeat-0 "Direct link to Heartbeat (0)")

Sent by both sides if no messages have been sent for (HeartBtInt x 0.75) seconds, as agreed upon during logon. May also be sent in response to a Test Request.

| Tag | Name | Description |
| --- | --- | --- |
| 112 | TestReqID | Copied from the Test Request, if any |

## Test Request (1) [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry\#test-request-1 "Direct link to Test Request (1)")

May be sent at any time by either side.

| Tag | Name | Description |
| --- | --- | --- |
| 112 | TestReqID | Free text |

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Header](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#header)
- [Logon (A)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#logon-a)
- [Logout (5)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#logout-5)
- [New Order Single (D)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#new-order-single-d)
  - [SelfTradePrevention Values](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#selftradeprevention-values)
  - [Time In Force Values](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#time-in-force-values)
  - [Errors](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#errors)
  - [Iceberg Orders](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#iceberg-orders)
  - [Take Profit Stop Loss Orders](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#take-profit-stop-loss-orders)
  - [Limit With Funds Orders](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#limit-with-funds-orders)
- [New Order Batch (U6)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#new-order-batch-u6)
- [Order Cancel Request (F)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#order-cancel-request-f)
- [Order Status Request (H)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#order-status-request-h)
  - [Response](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#response)
- [Order Cancel Batch Request (U4)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#order-cancel-batch-request-u4)
  - [Response](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#response-1)
- [Execution Report (8)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#execution-report-8)
  - [ExecType Values](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#exectype-values)
- [New Order Batch Reject (U7)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#new-order-batch-reject-u7)
- [Modify Order Request (G)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#modify-order-request-g)
  - [Guidance](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#guidance)
- [Order Cancel Reject (9)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#order-cancel-reject-9)
- [Order Cancel Batch Reject (U5)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#order-cancel-batch-reject-u5)
- [Reject (3)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#reject-3)
  - [SessionRejectReason Values](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#sessionrejectreason-values)
- [RFQ Request (AH)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#rfq-request-ah)
  - [RFQ Order Protections](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#rfq-order-protections)
- [Quote Request (R)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#quote-request-r)
- [Quote (S)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#quote-s)
- [Quote Status Report (AI)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#quote-status-report-ai)
- [Resend Request (2)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#resend-request-2)
  - [Guidance](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#guidance-1)
- [Heartbeat (0)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#heartbeat-0)
- [Test Request (1)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#test-request-1)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_websocket_errors.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/websocket-errors#__docusaurus_skipToContent_fallback)

An error message displays when the client is actively disconnected for any of these reasons:

- The client has too many backed up messages ( `ErrSlowConsume`).
- The client is sending too many messages ( `ErrSlowRead`).
- The message size is too large ( `Message too big`)
- There are intermittent network issues.

Most failure cases trigger an `error` message—specifically, a message with the `type` `"error"`. This can be helpful when implementing a client or debugging issues.

```codeBlockLines_p187
{
  "type": "error",
  "message": "error message"
  /* ... */
}

```

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_profiles.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/profiles#__docusaurus_skipToContent_fallback)

Profiles are the equivalent of portfolios on the [Coinbase Exchange](https://exchange.coinbase.com/portfolios) website. The maximum number of profiles is 100 .

## API Keys [](https://docs.cdp.coinbase.com/exchange/docs/profiles\#api-keys "Direct link to API Keys")

An API key is scoped to a specific profile. An API key can only view and create data that belongs to its own profile, unless otherwise noted. This is true for the REST API, FIX API and Websocket Feed.

To access data or actions on a different profile, create a new API key on the Coinbase Exchange website.

## Deleted Profiles [](https://docs.cdp.coinbase.com/exchange/docs/profiles\#deleted-profiles "Direct link to Deleted Profiles")

Profiles can be deleted on the Coinbase Exchange website. The permissions of an API key associatd with a deleted profile are automatically set to "View."

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [API Keys](https://docs.cdp.coinbase.com/exchange/docs/profiles#api-keys)
- [Deleted Profiles](https://docs.cdp.coinbase.com/exchange/docs/profiles#deleted-profiles)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_rate_limits.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/rate-limits#__docusaurus_skipToContent_fallback)

## Summary [](https://docs.cdp.coinbase.com/exchange/docs/rate-limits\#summary "Direct link to Summary")



Info

Private endpoints are authenticated.

### [REST API Rate Limits](https://docs.cdp.coinbase.com/exchange/docs/rest-rate-limits) [](https://docs.cdp.coinbase.com/exchange/docs/rate-limits\#rest-api-rate-limits "Direct link to rest-api-rate-limits")

#### Public Endpoints [](https://docs.cdp.coinbase.com/exchange/docs/rate-limits\#public-endpoints "Direct link to Public Endpoints")

- Requests per second per IP: 10
- Requests per second per IP in bursts: Up to 15

#### Private Endpoints [](https://docs.cdp.coinbase.com/exchange/docs/rate-limits\#private-endpoints "Direct link to Private Endpoints")

- Requests per second per profile: 15
- Requests per second per profile in bursts: Up to 30

#### Private `/fills` Endpoint [](https://docs.cdp.coinbase.com/exchange/docs/rate-limits\#private-fills-endpoint "Direct link to private-fills-endpoint")

- Requests per second per profile: 10
- Requests per second per profile in bursts: Up to 20

#### Private `/loans` Endpoint [](https://docs.cdp.coinbase.com/exchange/docs/rate-limits\#private-loans-endpoint "Direct link to private-loans-endpoint")

- Requests per second per profile: 10



Info

Rate limits do not apply to [List loan assets](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_getloanassets) ( `/loans/assets`) which is not private.

### [FIX API Rate Limits](https://docs.cdp.coinbase.com/exchange/docs/fix-rate-limits) [](https://docs.cdp.coinbase.com/exchange/docs/rate-limits\#fix-api-rate-limits "Direct link to fix-api-rate-limits")

#### FIX 4.2 Rate Limits [](https://docs.cdp.coinbase.com/exchange/docs/rate-limits\#fix-42-rate-limits "Direct link to FIX 4.2 Rate Limits")

- Requests per rolling second per session: 50
- Messages per second in bursts: 100

#### FIX 5.0 Rate Limits [](https://docs.cdp.coinbase.com/exchange/docs/rate-limits\#fix-50-rate-limits "Direct link to FIX 5.0 Rate Limits")

- 2 logons per second per API key
- 100 requests per second



Caution

Your FIX 5 session is disconnected if your messages exceed 200 messages per second

#### FIX Maximums [](https://docs.cdp.coinbase.com/exchange/docs/rate-limits\#fix-maximums "Direct link to FIX Maximums")

- Maximum API keys per session/connection: 1
- Maximum connections per profile: 75 . See [FIX Best Practices](https://docs.cdp.coinbase.com/exchange/docs/fix-best-practices).
- Maximum connections per user across all profiles: 175
- Maximum profiles per user: 100
- Maximum orders per batch message message (new and cancelled): 15

### [Websocket Rate Limits](https://docs.cdp.coinbase.com/exchange/docs/websocket-rate-limits) [](https://docs.cdp.coinbase.com/exchange/docs/rate-limits\#websocket-rate-limits "Direct link to websocket-rate-limits")

- Requests per second per IP: 8
- Requests per second per IP in bursts: Up to 20
- Messages sent by the client every second per IP: 100

### Other [](https://docs.cdp.coinbase.com/exchange/docs/rate-limits\#other "Direct link to Other")

- Maximum open orders: 500

## How Rate Limits Work [](https://docs.cdp.coinbase.com/exchange/docs/rate-limits\#how-rate-limits-work "Direct link to How Rate Limits Work")

Rate-limiting for both the Exchange REST API and the FIX API use a **lazy-fill token bucket** implementation.

A TokenBucket stores a maximum amount of tokens, which is the **burst size**, and fills at a given rate called the **refresh rate**. The bucket starts full, and as requests are received, a token is removed for each request. Tokens are continuously added to the bucket at the refresh rate until full.

When a user sends a request, the TokenBucket calculates whether or not to rate limit the user as follows:

1. Fill the user's TokenBucket to a token size based on the following formula: `token_amount = min(burst, previous_token_amount + (current_time - previous_request_time) * refresh_rate)`
2. Remove 1 token if possible, otherwise rate limit the request.
3. Repeat Steps 1 and 2 for each subsequent request.

### TokenBucket Example [](https://docs.cdp.coinbase.com/exchange/docs/rate-limits\#tokenbucket-example "Direct link to TokenBucket Example")

Let's say you have a TokenBucket with burst = 3 and refresh\_rate = 1. The table below represents the state of your token bucket after a series of requests:

| Action | Time | Tokens | Notes |
| --- | --- | --- | --- |
| Initial State | 0.0 | 3.0 | New TokenBucket is initialized to max capacity (burst) |
| Request 1 | 0.5 | 2.0 | Fill TokenBucket, then remove a token, because we are at max capacity, and subtract 1 token from 3 |
| Request 2 | 0.8 | 1.3 | Fill TokenBucket to 2.3 ( `min(3, (2 + (.8 - .5) * 1.0)) = min(3, 2.3) = 2.3`), then subtract 1 |
| Request 3 | 0.9 | 0.4 | Fill TokenBucket to 1.4 ( `min(3, (1.3 + (.9 - .8) * 1.0)) = min(3, 1.4) = 1.4`), then subtract 1 |
| Request 4 | 1.0 | 0.5 | Fill TokenBucket to 0.5 ( `min(3, (.4 + (1.0 - .9) * 1.0)) = min(3, 0.5) = 0.5`). **Ratelimit** because we don't have enough tokens available |
| Request 5 | 1.4 | 0.9 | Fill TokenBucket to 0.9 ( `min(3, (0.5 + (1.4 - 1.0) * 1.0)) = min(3, 0.9) = 0.9`). **Ratelimit** because we don't have enough tokens available |
| Request 6 | 1.8 | 0.3 | Fill TokenBucket to 1.3 ( `min(3, (0.9 + (1.8 - 1.4) * 1.0)) = min(3, 1.3) = 1.3`), then remove 1 |
| Request 7 | 5.0 | 2.0 | Fill TokenBucket to 3.0 ( `min(3, (0.3 + (5.0 - 1.8) * 1.0)) = min(3, 3.5) = 3`), since we would "overflow" with our calculations, then subtract 1 |

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Summary](https://docs.cdp.coinbase.com/exchange/docs/rate-limits#summary)
  - [REST API Rate Limits](https://docs.cdp.coinbase.com/exchange/docs/rate-limits#rest-api-rate-limits)
  - [FIX API Rate Limits](https://docs.cdp.coinbase.com/exchange/docs/rate-limits#fix-api-rate-limits)
  - [Websocket Rate Limits](https://docs.cdp.coinbase.com/exchange/docs/rate-limits#websocket-rate-limits)
  - [Other](https://docs.cdp.coinbase.com/exchange/docs/rate-limits#other)
- [How Rate Limits Work](https://docs.cdp.coinbase.com/exchange/docs/rate-limits#how-rate-limits-work)
  - [TokenBucket Example](https://docs.cdp.coinbase.com/exchange/docs/rate-limits#tokenbucket-example)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_fix_rate_limits.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/fix-rate-limits#__docusaurus_skipToContent_fallback)

## Order Entry Limits [](https://docs.cdp.coinbase.com/exchange/docs/fix-rate-limits\#order-entry-limits "Direct link to Order Entry Limits")

### FIX 4.2 [](https://docs.cdp.coinbase.com/exchange/docs/fix-rate-limits\#fix-42 "Direct link to FIX 4.2")

The [FIX 4.2 Order Entry API](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry) rate limits are:

- 50 requests per **rolling second** 1 per session
- 100 messages per second in bursts



Rolling second

The clock starts when the first command is sent. We use a lazy-fill token bucket implementation.

### FIX 5 [](https://docs.cdp.coinbase.com/exchange/docs/fix-rate-limits\#fix-5 "Direct link to FIX 5")

The [FIX 5 Order Entry API](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50) rate limits are:

- 2 logons per second per API key
- 100 requests per second



Caution

Your FIX 5 session is disconnected if your messages exceed 200 messages per second

### Maximums [](https://docs.cdp.coinbase.com/exchange/docs/fix-rate-limits\#maximums "Direct link to Maximums")

- Maximum connections per profile: 75 . See [FIX Best Practices](https://docs.cdp.coinbase.com/exchange/docs/fix-best-practices).
- Maximum connections per user across all profiles: 175
- Maximum API keys per session/connection: 1
- Maximum profiles per user: 100
- Maximum orders per batch message (new and cancelled): 15

## Market Data Limits [](https://docs.cdp.coinbase.com/exchange/docs/fix-rate-limits\#market-data-limits "Direct link to Market Data Limits")

The [FIX Market Data API](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-market-data) is limited to 1 connection per API key. It does not use FIX order entry rate limits (connections, rps, burst rps).

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Order Entry Limits](https://docs.cdp.coinbase.com/exchange/docs/fix-rate-limits#order-entry-limits)
  - [FIX 4.2](https://docs.cdp.coinbase.com/exchange/docs/fix-rate-limits#fix-42)
  - [FIX 5](https://docs.cdp.coinbase.com/exchange/docs/fix-rate-limits#fix-5)
  - [Maximums](https://docs.cdp.coinbase.com/exchange/docs/fix-rate-limits#maximums)
- [Market Data Limits](https://docs.cdp.coinbase.com/exchange/docs/fix-rate-limits#market-data-limits)

[docs_cdp_coinbase_com_exchange_docs_rest_pagination.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/rest-pagination#__docusaurus_skipToContent_fallback)

Coinbase Exchange uses cursor pagination for all REST requests which return arrays.

Cursor pagination allows for fetching results before and after the current page of results and is well suited for realtime data. Endpoints like `/trades`, `/fills`, `/orders`, return the latest items by default. To retrieve more results subsequent requests should specify which direction to paginate based on the data previously returned.

`before` and `after` cursors are available via response headers `CB-BEFORE` and `CB-AFTER`. Your requests should use these cursor values when making requests for pages after the initial request.

### Parameters [](https://docs.cdp.coinbase.com/exchange/docs/rest-pagination\#parameters "Direct link to Parameters")

| Parameter | Default | Description |
| --- | --- | --- |
| `before` |  | Request page before (newer) this pagination id |
| `after` |  | Request page after (older) this pagination id |
| `limit` | 1000 | Number of results per request. Maximum 1000 (default 1000) |

### Example [](https://docs.cdp.coinbase.com/exchange/docs/rest-pagination\#example "Direct link to Example")

`GET /orders?before=2&limit=30`

### Before and After cursors [](https://docs.cdp.coinbase.com/exchange/docs/rest-pagination\#before-and-after-cursors "Direct link to Before and After cursors")

The `before` cursor references the first item in a results page and the `after` cursor references the last item in a set of results.

#### Before Cursor [](https://docs.cdp.coinbase.com/exchange/docs/rest-pagination\#before-cursor "Direct link to Before Cursor")

To request a page of records before the current one, use the `before` query parameter. Your initial request can omit this parameter to get the default first page.

The response contains a `CB-BEFORE` header which returns the cursor id to use in your next request for the page before the current one. **The page before is a newer page and not one that happened before in chronological time.**

#### After Cursor [](https://docs.cdp.coinbase.com/exchange/docs/rest-pagination\#after-cursor "Direct link to After Cursor")

The response also contains a `CB-AFTER` header which returns the cursor id to use in your next request for the page after this one. **The page after is an older page and not one that happened after this one in chronological time.**

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Parameters](https://docs.cdp.coinbase.com/exchange/docs/rest-pagination#parameters)
- [Example](https://docs.cdp.coinbase.com/exchange/docs/rest-pagination#example)
- [Before and After cursors](https://docs.cdp.coinbase.com/exchange/docs/rest-pagination#before-and-after-cursors)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_upcoming_changes.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/upcoming-changes#__docusaurus_skipToContent_fallback)

This page provides information about upcoming changes to Coinbase Exchange.

## FIX 5.0 New Drop Copy Fleet [](https://docs.cdp.coinbase.com/exchange/docs/upcoming-changes\#fix-50-new-drop-copy-fleet "Direct link to FIX 5.0 New Drop Copy Fleet")

_Added: 2025-Apr-16_

Coinbase Exchange is introducing a dedicated FIX 5.0 Drop Copy (DC) fleet, accessible via a new URI and port. Drop copy session connected over this fleet will deliver complete execution report messages with full field parity to FIX 4.2.

- Available via a dedicated connection:
  - URI:
    - **Prod** `tcp+ssl://fix-dc.exchange.coinbase.com`
    - **Sandbox** `tcp+ssl://fix-dc.sandbox.exchange.coinbase.com`
  - Port: 6122
- New tags on Execution Reports on DC:
  - `ClOrdID <11>: (String), An identifier specified by the sender to uniquely identify other messages correlating to this request.`
  - `OrdStats <39>: (Char), Identifies current status of order.`
  - `OrdQty <38>: (Qty), Quantity ordered.`
  - `OrdType <40>: (Char), Order Type.`
  - `LeavesQty <151>: (Qty), Quantity open for further execution.`
  - `CashOrderQty <152> (Qty), Specifies the approximate order quantity desired in total monetary units vs. as a number of shares`

**Note**: Existing Order Entry drop copy functionality (via tag 9406=Y) will not change.

## FIX 4.2 Order Entry Gateway Deprecation [](https://docs.cdp.coinbase.com/exchange/docs/upcoming-changes\#fix-42-order-entry-gateway-deprecation "Direct link to FIX 4.2 Order Entry Gateway Deprecation")

_Added: 2024-Aug-21_

We will be deprecating the FIX 4.2 Order Entry Gateway on **June 3rd, 2025**. For FIX based order entry, **leverage the newer, more performant** [FIX 5 Order Entry Gateway](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50).

## Deleting travel rule fields in POST /withdrawals/crypto REST API [](https://docs.cdp.coinbase.com/exchange/docs/upcoming-changes\#deleting-travel-rule-fields-in-post-withdrawalscrypto-rest-api "Direct link to Deleting travel rule fields in POST /withdrawals/crypto REST API")

_Updated: 2025-Jan-13_

We are removing travel rule fields from `POST /withdrawals/crypto` REST API. Customers in travel rule jurisdictions can withdraw only to their allowlisted addresses.

## Adding new PUT /address-book/{id} REST endpoint [](https://docs.cdp.coinbase.com/exchange/docs/upcoming-changes\#adding-new-put-address-bookid-rest-endpoint "Direct link to adding-new-put-address-bookid-rest-endpoint")

_Added: 2025-Jan-8_

We are introducing a new REST endpoint to edit an editing existing address book entry - useful for customers in travel rule jurisdictions.
This endpoint requires the API key to have **MANAGE** permissions.

Non travel-rule jurisdictions can only edit the label of the address book entry.

Example request `PUT https://api.exchange.coinbase.com/address-book/{id}`. Here {id} refers to uuid of the crypto address.

```codeBlockLines_p187
{
  "label": "string", // label for crypto address
  "is_certified_self_send": bool // true if customer owns the address/ false if it is a third party address
  "vasp_id": "string" // optional - vasp name from supported list if the wallet address is a VASP address
  "is_verified_self_hosted_wallet": bool // optional - true if the wallet is verified self-hosted wallet
  "business_name": "lorem ipsum", // required for third-party address; ie is_certified_self_send is false
  "business_country_code": "DE" // ISO 3166-1 alpha-2 country code required for third-party address; ie is_certified_self_send is false
}

```

Sample response:

```codeBlockLines_p187
{
  "body": {
    "id": "e89b6ea2-1d73-4b3c-9f3a-3d9c8f25b7d9",
    "address": "0x6448894b9499AeebD914232483d0d0467194efcp",
    "label": "string",
    "address_info": {
      "address": "0x6448894b9499AeebD914232483d0d0467194efcp",
      "display_address": "0x6448894b9499AeebD914232483d0d0467194efcp",
      "destination_tag": "string"
    },
    "display_address": "0x6448894b9499AeebD914232483d0d0467194efcp",
    "address_booked": true,
    "address_book_added_at": "2024-03-19T12:00:00Z",
    "address_book_entry_pending_until": "2024-03-21T12:00:00Z",
    "currency": "USDC",
    "is_verified_self_hosted_wallet": false,
    "vasp_id": "string",
    "business_name": "string",
    "business_country_code": "DE"
  }
}

```

note: business name and country code are only populated for travel rule regions.

## Enabling RFQs in terms of CashOrderQty (152) [](https://docs.cdp.coinbase.com/exchange/docs/upcoming-changes\#enabling-rfqs-in-terms-of-cashorderqty-152 "Direct link to Enabling RFQs in terms of CashOrderQty (152)")

_Added: 2025-Apr-15_

- Adding `CashOrderQty (152)` to Quote\_Request (R) messages
- Adding `BidCashOrderQty (8234)` and `OfferCashOrderQty (8235)` tags to `Quote (S)` messages
- Adding `LeavesFunds (8152)` and `CashOrderQty (152)` to `Execution Reports (8)`

We will allow RFQ takers to submit orders using a quantity specified in terms of the quote\_currency. The quote\_currency refers to the USD quantity or latter currency in the product pair (e.g. for BTC-USD, quote\_currency = USD. For BTC-SOL, quote\_currency = SOL).

As a result, LPs must respond in terms of quote\_currency, as indicated by FIX tag `CashOrderQty (152)` on the `Quote_Request (R)` message.

- LPs must respond with the full `BidCashOrderQty (8234)` \| `BidPx (132)` and `OfferCashOrderQty (8235)` \| `OfferPx (133)` on their corresponding `Quote (S)` message.
- `Execution Reports (8)` for corresponding orders will reflect the `CashOrderQty (152)` and the `OrderQty (38)`, which is calculated as such: `OrderQty (38) = (CashOrderQty/ (BidPx or OfferPx))`
- `Execution Reports (8)` will also contain `LeavesFunds (8152)` field to indicate remaining `CashOrderQty (152)` that is unfilled.

Sample Execution Report:

```codeBlockLines_p187
8=FIXT.1.1|9=440|35=8|49=Coinbase|56=TARGET_COMP_ID|34=15|50=TEST|52=20250408-03:34:32.789012|369=8|6=70000|
11=CLIENT_ORDER_ID|14=0.01428|17=EXEC_ID|37=ORDER_ID|39=2|55=BTC-USD|54=2|40=2|32=0.01428|31=70000|44=70000|38=0.01428|
60=20250408-03:34:32.784254|152=999.60015994|150=F|8152=0|59=4|126=20250408-03:34:39.467|136=1|137=0.249900039985|
138=USD|139=4|891=0|10=204

```

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [FIX 5.0 New Drop Copy Fleet](https://docs.cdp.coinbase.com/exchange/docs/upcoming-changes#fix-50-new-drop-copy-fleet)
- [FIX 4.2 Order Entry Gateway Deprecation](https://docs.cdp.coinbase.com/exchange/docs/upcoming-changes#fix-42-order-entry-gateway-deprecation)
- [Deleting travel rule fields in POST /withdrawals/crypto REST API](https://docs.cdp.coinbase.com/exchange/docs/upcoming-changes#deleting-travel-rule-fields-in-post-withdrawalscrypto-rest-api)
- [Adding new PUT /address-book/{id} REST endpoint](https://docs.cdp.coinbase.com/exchange/docs/upcoming-changes#adding-new-put-address-bookid-rest-endpoint)
- [Enabling RFQs in terms of CashOrderQty (152)](https://docs.cdp.coinbase.com/exchange/docs/upcoming-changes#enabling-rfqs-in-terms-of-cashorderqty-152)

[docs_cdp_coinbase_com_exchange_docs_sandbox.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/sandbox#__docusaurus_skipToContent_fallback)

A public sandbox is available for testing API connectivity and web trading.



Sandbox is subset

The sandbox hosts a _subset_ of the production order books and supports all exchange functionality _except_ [Transfers](https://docs.cdp.coinbase.com/exchange/docs/sandbox#unsupported-features). You can add unlimited fake funds for testing.



Info

Login sessions and API keys are separate from production. Log into the [sandbox web interface](https://public.sandbox.exchange.coinbase.com/) to create an API key, deposit/withdraw funds, etc.

## Sandbox URLs [](https://docs.cdp.coinbase.com/exchange/docs/sandbox\#sandbox-urls "Direct link to Sandbox URLs")

Use the following URLs to test your API connectivity. See the [Runbook](https://docs.cdp.coinbase.com/exchange/docs/runbook#production-urls) for Production URLs.

| API | URL |
| --- | --- |
| REST API | `https://api-public.sandbox.exchange.coinbase.com ` |
| Websocket Feed | `wss://ws-feed-public.sandbox.exchange.coinbase.com ` |
| Websocket Direct Feed | `wss://ws-direct.sandbox.exchange.coinbase.com ` |
| FIX API - Order Entry 4.2 | `tcp+ssl://fix-public.sandbox.exchange.coinbase.com:4198 ` |
| FIX API - Order Entry 5.0 SP2 | `tcp+ssl://fix-ord.sandbox.exchange.coinbase.com:6121 ` |
| FIX API - Market Data 5.0 SP2 | `tcp+ssl://fix-md.sandbox.exchange.coinbase.com:6121 ` |

## Sandbox SSL Certificate [](https://docs.cdp.coinbase.com/exchange/docs/sandbox\#sandbox-ssl-certificate "Direct link to Sandbox SSL Certificate")

Your FIX SSL client must validate the following sandbox FIX server SSL certificate:

```codeBlockLines_p187
-----BEGIN CERTIFICATE-----
MIIEdDCCA1ygAwIBAgIQD03L1cHVypYSDFuvcnpAHzANBgkqhkiG9w0BAQsFADBG
MQswCQYDVQQGEwJVUzEPMA0GA1UEChMGQW1hem9uMRUwEwYDVQQLEwxTZXJ2ZXIg
Q0EgMUIxDzANBgNVBAMTBkFtYXpvbjAeFw0yMjAzMjcwMDAwMDBaFw0yMzA0MjUy
MzU5NTlaMCoxKDAmBgNVBAMMHyouc2FuZGJveC5leGNoYW5nZS5jb2luYmFzZS5j
b20wggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQC8LYRdqMoVNa/0M4MF
+Wkr8SiybZ95JycTE+0ZVmf92DKo4I8m/8fBtOrH0jgrhvamVSJ0lI6VFiAzlTd1
doUbliQ9Xm1aE/YHQO9J64AIP97peysgHBd+g3/Vhz33aaaU2vyHH5kPHiekU8n/
ObXPPoFd/Awul8uxxlXsVFx8oBWL2MeMjLNLLWNiGWq+lQloGKsQYVR/fQZizvpP
vyZO6pCLRId6+Wq3Tcb7NHQZc6+tePVi+5fovE+lm/yQrhjGqDzI7P4rWjJqCPrA
sYJeYFcVJhdSuFY2Ngm8eKeDP14TVEs9pkIWvyMGmB17QBPbRJipdoKu1N6fsx54
N9JDAgMBAAGjggF4MIIBdDAfBgNVHSMEGDAWgBRZpGYGUqB7lZI8o5QHJ5Z0W/k9
0DAdBgNVHQ4EFgQUa5RZ0yvv71YteSuqO1VRvmGGKv0wKgYDVR0RBCMwIYIfKi5z
YW5kYm94LmV4Y2hhbmdlLmNvaW5iYXNlLmNvbTAOBgNVHQ8BAf8EBAMCBaAwHQYD
VR0lBBYwFAYIKwYBBQUHAwEGCCsGAQUFBwMCMD0GA1UdHwQ2MDQwMqAwoC6GLGh0
dHA6Ly9jcmwuc2NhMWIuYW1hem9udHJ1c3QuY29tL3NjYTFiLTEuY3JsMBMGA1Ud
IAQMMAowCAYGZ4EMAQIBMHUGCCsGAQUFBwEBBGkwZzAtBggrBgEFBQcwAYYhaHR0
cDovL29jc3Auc2NhMWIuYW1hem9udHJ1c3QuY29tMDYGCCsGAQUFBzAChipodHRw
Oi8vY3J0LnNjYTFiLmFtYXpvbnRydXN0LmNvbS9zY2ExYi5jcnQwDAYDVR0TAQH/
BAIwADANBgkqhkiG9w0BAQsFAAOCAQEATpjyCMwAOSFKFTA67UaVkDCjz/ULBY6P
L4JwTJ+7kmT+HMvGimx15CsVjne64bT5twWlzqA/l4h25HGj0hD0TU2ktqmFhfAm
DpjGVp4KgIcZpvv7oRIU4e5I422Y++2UVuATwLWdELgpnm4AVq1aqI10XrQlJeHL
gRVfV5qkr9Vsc+fk7HY7YwbNQk2jXbRaj22f6GxiJ/6VmUcCD7zZ1GZtUipv0JEy
PtWD/BbSKNx1GJnLZ6L+QytPs+MW+FEetlU/oqPuyYRhmJUBUiwKkm6yKWRj9tQf
sq0a4uLI3SUgsBv/CQ/Qa9LnRdNjvlWSKLzeIX2LU9rE/3F3oQh7HQ==
-----END CERTIFICATE-----

```

## Unsupported Features [](https://docs.cdp.coinbase.com/exchange/docs/sandbox\#unsupported-features "Direct link to Unsupported Features")

The Transfer endpoints are _not_ available for testing in the Sandbox:

- [Withdraw to payment](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postwithdrawpaymentmethod)
- [Deposit from payment](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postdepositpaymentmethod)
- [Deposit from Coinbase account](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postdepositcoinbaseaccount)
- [Withdraw to crypto address](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postwithdrawcrypto)
- [Withdraw to Coinbase Account](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postwithdrawcoinbaseaccount)

## Creating API Keys [](https://docs.cdp.coinbase.com/exchange/docs/sandbox\#creating-api-keys "Direct link to Creating API Keys")

To create an API key in the sandbox web interface:

1. Go to the [sandbox web interface](https://public.sandbox.exchange.coinbase.com/)
2. Create an account or sign in.
3. Go to **API** in your profile dropdown menu.
4. Click **New API Key**.

## Managing Funds [](https://docs.cdp.coinbase.com/exchange/docs/sandbox\#managing-funds "Direct link to Managing Funds")

To add or remove funds in the sandbox web interface:

1. Go to the **Portfolios** tab.
2. Click the **Deposit** and **Withdraw** buttons as you would on the production web interface.

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Sandbox URLs](https://docs.cdp.coinbase.com/exchange/docs/sandbox#sandbox-urls)
- [Sandbox SSL Certificate](https://docs.cdp.coinbase.com/exchange/docs/sandbox#sandbox-ssl-certificate)
- [Unsupported Features](https://docs.cdp.coinbase.com/exchange/docs/sandbox#unsupported-features)
- [Creating API Keys](https://docs.cdp.coinbase.com/exchange/docs/sandbox#creating-api-keys)
- [Managing Funds](https://docs.cdp.coinbase.com/exchange/docs/sandbox#managing-funds)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

[docs_cdp_coinbase_com_exchange_docs_fix_msg_oe_iceberg.md]
[Skip to main content](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-iceberg#__docusaurus_skipToContent_fallback)

Iceberg orders are supported in New Order Single (35=D) [FIX 4.2](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#new-order-single-d) and [FIX 5.0](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry-50#newordersingle-35d) with the [Create a new order](https://docs.cdp.coinbase.com/exchange/reference/exchangerestapi_postorders) REST API.

Iceberg orders allow you to disclose fills to the market in parts, by sending a [New Order Single (D)](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-order-entry#new-order-single-d) with [MaxFloor (111)](https://fiximate.fixtrading.org/en/FIX.Latest/tag111.html):

- A quantity equal to the MaxFloor is displayed on the order book, with the remainder added to the order book at the same price level as the hidden quantity at the end of the queue.
- When the displayed quantity is fully filled, matching logic continues to execute and fill the hidden quantity.
- Once the matching event is completed, if there is still a hidden quantity left, a new displayed order is added to the end of the display order queue, for a size up to MaxFloor.

Changes to the displayed portion of the order, such as replenishes, fills, STPs, or user cancels, are supplied via ExecutionReport with [SecondaryOrderID (198)](https://fiximate.fixtrading.org/en/FIX.Latest/tag198.html).

### Supported Pairs [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-iceberg\#supported-pairs "Direct link to Supported Pairs")

See [Iceberg Orders Supported Trading Pairs](https://help.coinbase.com/en/exchange/trading-and-funding/iceberg-trading).



Note

All trading pairs have Iceberg support in sandbox.

### Sample Message Flow [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-iceberg\#sample-message-flow "Direct link to Sample Message Flow")

In this example message flow, a client submitted a buy order of quantity = 1 and while displaying only 0.3 at a time. (Non-relevant FIX fields and IDs are not shown for brevity.)

**Event 1 - Passive New Order**

A passive Iceberg order is placed with OrderQty=1 ( `38=1`) and MaxFloor=0.3 ( `111=0.3`):

`OrderID123` is _not_ in the Full channel, nor in the Level2 FIX Market Data. Instead, only the displayed portion is shown as `Order456`.

## FIX

## WebSocket Full Channel

## WebSocket Level2 Channel

```codeBlockLines_p187
-> 35=D|55=BTC-USD|40=2|38=1|44=25000|111=0.3
<- 35=8|37=OrderID123|39=New|38=1
// Event generated when the first displayed portion of the order is added to the orderbook
<- 35=8|37=OrderID123|198=OrderID456|39=Restated|378=Broker_Option|38=0.3

```

```codeBlockLines_p187
{"order_id":"OrderID456","order_type":"limit","size":"0.3","price":"25000","type":"received","side":"buy","product_id":"BTC-USD","time":...}
{"order_id":"OrderID456","order_type":"limit","remaining_size":"0.3","price":"25000","type":"open","side":"buy","product_id":"BTC-USD","time":...}

```

```codeBlockLines_p187
{"type":"l2update","product_id":"BTC-USD","changes":[["buy","25000.0000","0.3000"]]...}

```

**Event 2 - MaxFloor Match**

A match takes place with quantity = 0.3.

Once the displayed order is fully filled, a `Done_For_Day` with SecondaryOrderID is sent. This does not mean the Iceberg order is complete. Rather, a replenish event occurs with a different SecondaryOrderID. The new displayed order is added to the end of the queue of the displayed book at the price of 25000.

## FIX

## WebSocket Full Channel

## WebSocket Level2 Channel

```codeBlockLines_p187
<- 35=8|37=OrderID123|198=OrderID456|39=Partially_Filled|32=0.3|151=0.7|14=0.3|137=0.0004
<- 35=8|37=OrderID123|198=OrderID456|39=Done_For_Day|32=0|151=0.7|14=0.3
// Displayed portion replenish event
<- 35=8|37=OrderID123|198=OrderID789|39=Restated|378=Broker_Option|38=0.3

```

```codeBlockLines_p187
{"trade_id":1761595,"maker_order_id":"OrderID456","taker_order_id":"...","size":"0.3","price":"25000","type":"match","side":"buy",...}
{"order_id":"OrderID456","reason":"filled","price":"25000","remaining_size":"0","type":"done","side":"buy","product_id":"BTC-USD",...}
{"order_id":"Order789","order_type":"limit","size":"0.3","price":"25000","type":"received","side":"buy","product_id":"BTC-USD","time":...}
{"order_id":"Order789","order_type":"limit","remaining_size":"0.3","price":"25000","type":"open","side":"buy","product_id":"BTC-USD","time":...}

```

```codeBlockLines_p187
{"type":"l2update","product_id":"BTC-USD","changes":[["buy","25000.0000","0.0000"]]...} {"type":"l2update","product_id":"BTC-USD","changes":[["buy","25000.0000","0.3000"]]...}

```

**Event 3 - Aggressive Order**

An aggressive order takes place with quantity = 0.7.

In this event, a large aggressive order came in. First, the displayed `OrderID789` was filled for 0.3. Then, because the displayed book was empty at the price level of 25000, the matching logic continued to the hidden book at the price level 25000. The hidden `OrderID123` was filled for 0.4. Note that the `Done_For_Day` ExecutionReport does _not_ have a SecondaryOrderID and the the Iceberg order is complete.

## FIX

## WebSocket Full Channel

## WebSocket Level2 Channel

```codeBlockLines_p187
<- 35=8|37=OrderID123|198=OrderID789|39=Partially_Filled|32=0.3|151=0.4|14=0.6|137=0.0004
<- 35=8|37=OrderID123|198=OrderID789|39=Done_For_Day|32=0|151=0.4|14=0.6
<- 35=8|37=OrderID123|39=Partially_Filled|32=0.4|151=0|14=1.0|137=0.00045
<- 35=8|37=OrderID123|39=Done_For_Day|32=0|151=0|14=1.0

```

```codeBlockLines_p187
{"trade_id":1761596,"maker_order_id":"OrderID456","taker_order_id":"...","size":"0.3","price":"25000","type":"match","side":"buy",...}
{"order_id":"OrderID456","reason":"filled","price":"25000","remaining_size":"0","type":"done","side":"buy","product_id":"BTC-USD",...}
{"trade_id":1761596,"maker_order_id":"OrderID123","taker_order_id":"...","size":"0.4","price":"25000","type":"match","side":"buy",...}

```

```codeBlockLines_p187
{"type":"l2update","product_id":"BTC-USD","changes":[["buy","25000.0000","0.0000"]]...}

```

### Trading Rules [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-iceberg\#trading-rules "Direct link to Trading Rules")

To date, the Coinbase Exchange matching engine has followed price/time priority. With the introduction of Iceberg orders, our matching engine is changing to **price/display/time priority**. Regardless of whether they are displayed or hidden, better price orders will have higher priority. At a given price level, all displayed orders will have a higher priority than the hidden portion of the Iceberg orders. Replenish events will add a displayed order to the end of the displayed book at that price level.

### Fees for Non-displayed Fills [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-iceberg\#fees-for-non-displayed-fills "Direct link to Fees for Non-displayed Fills")

Fees are subject to change, but in general:

- Fills for displayed orders are charged with the standard taker/maker fee rate.
- Fills for non-displayed orders are charged with the standard taker/maker fee rate + a **fixed** 0.00005 (half a bps).

Fills can occur as non-displayed when an Iceberg order:

- Is executed as a taker.
- Is resting in the non-displayed book, and a significant taker order clears all displayed orders, eventually executing against this non-displayed order.

### Self Trade Prevention [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-iceberg\#self-trade-prevention "Direct link to Self Trade Prevention")

Displayed and hidden orders will be treated separately. For instance, if you have an Iceberg buy order of OrderQty=1 and MaxFloor=0.3, and you place a sell order with OrderQty=0.2 with SelfTradePrevention=O (Cancel Old), the displayed order is canceled but the hidden order is not. Instead, a replenish event will occur.

- **Cancel Old**: Once the displayed order is touched, the displayed order is canceled and matching continues. If the aggressive order hits the hidden order, the hidden order will then be canceled.
- **Decrement Cancel**: Size matters. The displayed order is first decremented and the matching logic continues. If the hidden order has quantity remaining, a replenish event occurs. If the hidden order is crossed, it will then be decremented.
- **Cancel Both**: This is similar to the approach for Cancel Old. Only the displayed portion gets canceled with the aggressive order. A replenish event occurs, if there is hidden size left.

### Allowed / Not Allowed [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-iceberg\#allowed--not-allowed "Direct link to Allowed / Not Allowed")

#### Allowed [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-iceberg\#allowed "Direct link to Allowed")

- Post Only order with MaxFloor.
- Stop order with MaxFloor.
- MaxFloor must be >= 10% of the OrderQty .

#### Not Yet Allowed [](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-iceberg\#not-yet-allowed "Direct link to Not Yet Allowed")

- Batch order with MaxFloor.
- Modifying an Iceberg order.
- Iceberg order in auction mode



Auction Mode Transition

Existing Iceberg orders will be canceled if a product is transitioned to auction mode.

Was this page helpful?



Yes



No



[Get help on Discord](https://discord.com/invite/cdp)



[Request a feature](https://coinbase-developer-platform.canny.io/cdp)

- [Supported Pairs](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-iceberg#supported-pairs)
- [Sample Message Flow](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-iceberg#sample-message-flow)
- [Trading Rules](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-iceberg#trading-rules)
- [Fees for Non-displayed Fills](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-iceberg#fees-for-non-displayed-fills)
- [Self Trade Prevention](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-iceberg#self-trade-prevention)
- [Allowed / Not Allowed](https://docs.cdp.coinbase.com/exchange/docs/fix-msg-oe-iceberg#allowed--not-allowed)

We use cookies and similar technologies on our websites to enhance and tailor your experience, analyze our traffic, and for security and marketing. You can choose not to allow some type of cookies by clicking Manage Settings. For more information see our [Cookie Policy](https://www.coinbase.com/legal/cookie).

Manage settings

Accept all

