[apidocs_bithumb_com_v2_1_5_reference__EC_9B_90_ED_99_94__EC_9E_85_EA_B8_88__EB_A6_AC_EC_8A_A4_ED_8A_B8__EC_A1_B0_ED_9A_8C.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Request Parameters**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%9B%90%ED%99%94-%EC%9E%85%EA%B8%88-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| state | 입금 상태<br>`- PROCESSING : 진행중`<br>`- ACCEPTED : 완료`<br>`- CANCELED : 취소됨` | String |
| uuids | 입금 UUID의 목록 | Array |
| txids | 입금 TXID의 목록 | Array |
| page | 페이지 수 (default :1) | Number |
| limit | 개수 제한 (default: 100, limit: 100) | Number |
| order\_by | 정렬방식<br>`- asc : 오름차순`<br>`- desc : 내림차순 (default)` | String |

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%9B%90%ED%99%94-%EC%9E%85%EA%B8%88-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| type | 입출금 종류 | String |
| uuid | 입금에 대한 고유 아이디 | String |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| txid | 입금의 트랜잭션 아이디 | String |
| state | 입금 상태<br>`- PROCESSING : 진행중`<br>`- ACCEPTED : 완료`<br>`- CANCELED : 취소됨` | String |
| created\_at | 입금 생성 시간 | DateString |
| done\_at | 입금 완료 시간 | DateString |
| amount | 입금 수량 | NumberString |
| fee | 입금 수수료 | NumberString |
| transaction\_type | 입금 유형<br>`- default : 일반입금` | String |

state

string

입금 상태

uuids

array of strings

입금 UUID의 목록

uuids
ADD string

txids

array of strings

입금 TXID의 목록

txids
ADD string

page

int32

Defaults to 1

페이지 수

limit

int32

Defaults to 100

개수 제한

order\_by

string

Defaults to desc

정렬방식

Authorization

string

required

Authorization token (JWT)

# `` 200      200

json

# `` 400      400

object

error

object

name

string

message

string

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

48

1const jwt = require('jsonwebtoken');

2const { v4: uuidv4 } = require('uuid');

3const crypto = require('crypto');

4const querystring = require('querystring');

5const axios = require('axios')

6​

7const accessKey = '발급받은 API KEY'

8const secretKey = '발급받은 SECRET KEY'

9const apiUrl = 'https:/api.bithumb.com'

10​

11// Set API parameters

12var query = 'limit=100&page=1&order_by=desc'

13

const uuids = [\
\
14    '15371593', '15371592'\
\
15]

16const uuid_query = uuids.map(uuid => `uuids[]=${uuid}`).join('&')

17query = uuid_query ? query + "&" + uuid_query : query

18​

19// Generate access token

20const alg = 'SHA512'

21const hash = crypto.createHash(alg)

22const queryHash = hash.update(query, 'utf-8').digest('hex')

23

const payload = {

24    access_key: accessKey,

25    nonce: uuidv4(),

26    timestamp: Date.now(),

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EC_9B_94month__EC_BA_94_EB_93_A4.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Request Parameters**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%9B%94month-%EC%BA%94%EB%93%A4\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 마켓 코드 (ex. KRW-BTC) | String |
| to | 마지막 캔들 시각 (exclusive).<br>ISO8061 포맷 (yyyy-MM-dd'T'HH:mm:ss'Z' or yyyy-MM-dd HH:mm:ss). 기본적으로 KST 기준 시간이며 비워서 요청시 가장 최근 캔들 | String |
| count | 캔들 개수(최대 200개까지 요청 가능) | Integer |

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%9B%94month-%EC%BA%94%EB%93%A4\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 마켓명 | String |
| candle\_date\_time\_utc | 캔들 기준 시각(UTC 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |
| candle\_date\_time\_kst | 캔들 기준 시각(KST 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |
| opening\_price | 시가 | Double |
| high\_price | 고가 | Double |
| low\_price | 저가 | Double |
| trade\_price | 종가 | Double |
| timestamp | 캔들 종료 시각(KST 기준) | Long |
| candle\_acc\_trade\_price | 누적 거래 금액 | Double |
| candle\_acc\_trade\_volume | 누적 거래량 | Double |
| first\_day\_of\_period | 캔들 기간의 가장 첫 날 | String |

market

string

required

마켓 코드 (ex. KRW-BTC)

to

string

마지막 캔들 시각 (exclusive). 비워서 요청시 가장 최근 캔들

count

int32

Defaults to 1

캔들 개수(최대 200개까지 요청 가능)

# `` 200      200

array of objects

object

market

string

candle\_date\_time\_utc

string

candle\_date\_time\_kst

string

opening\_price

integer

Defaults to 0

high\_price

integer

Defaults to 0

low\_price

integer

Defaults to 0

trade\_price

integer

Defaults to 0

timestamp

integer

Defaults to 0

candle\_acc\_trade\_price

number

Defaults to 0

candle\_acc\_trade\_volume

number

Defaults to 0

first\_day\_of\_period

string

# `` 400      400

object

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

1const options = {method: 'GET', headers: {accept: 'application/json'}};

2​

3fetch('https://api.bithumb.com/v1/candles/months?count=1', options)

4  .then(response => response.json())

5  .then(response => console.log(response))

6  .catch(err => console.error(err));

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EC_9A_94_EC_B2_AD__ED_8F_AC_EB_A7_B7.md]
mdx

````rdmd-code lang-mdx theme-light

<h1>인증</h1>

웹소켓은 Public과 Private으로 분류됩니다. Public은 별도의 인증 없이 데이터를 수신할 수 있지만, Private은 Websocket 연결 시 진행하는 인증에 성공한 경우에만 데이터를 수신할 수 있습니다.

* REST API와 동일하게 Authorization 헤더를 통해 인증을 진행합니다.
* <a href="/docs/%EC%9D%B8%EC%A6%9D-%ED%97%A4%EB%8D%94-%EB%A7%8C%EB%93%A4%EA%B8%B0" target="_blank">인증 헤더 만들기</a> 를 확인하시기 바랍니다.

<h3>(예시) Header 에 인증 정보를 담아 Websocket 연결</h3>

```node
const jwt = require("jsonwebtoken");
const {v4: uuidv4} = require('uuid');
const WebSocket = require("ws");

const accessKey = '발급받은 API KEY'
const secretKey = '발급받은 SECRET KEY'

const payload = {
    access_key: accessKey,
    nonce: uuidv4(),
    timestamp: Date.now()
};

console.log(payload);

const jwtToken = jwt.sign(payload, secretKey);

const ws = new WebSocket("wss://ws-api.bithumb.com/websocket/v1/private", {
    headers: {
        authorization: `Bearer ${jwtToken}`
    }
});

ws.on("open", () => {
    console.log("connected!");
    // Request after connection

    ws.send('[{"ticket":"test example"},{"type":"myOrder","codes":["KRW-BTC"]}]');
});

ws.on("error", console.error);

ws.on("message", (data) => console.log(data.toString()));

ws.on("close", () => console.log("closed!"));
````

* * *

# 요청 포맷

연결이 완료되면 웹소켓 서버에 다양한 요청을 할 수 있습니다.

요청과 응답은 JSON Object를 이용합니다.

요청은 `ticket field`, `type field`, `format field` 로 분류되며 각각의 필드는 다음 요소로 구성되어 있습니다.

Shell

```rdmd-code lang-shell theme-light

[\
`{ticket field}`\
, `{type field}`\
         .\
         .\
         .\
, `{type field}`\
, `{format field}`\
]
```

### Ticket Field

요청자를 식별하기 위해 필요한 필드값으로 시세를 수신하는 대상을 식별하며 UUID와 같이 유니크한 값의 사용을 권장하고 있습니다.

| 필드명 | 타입 | 내용 | 필수 여부 |
| --- | --- | --- | --- |
| ticket | String | 요청자를 식별 할 수 있는 값 | O |

### Type Field

수신하고 싶은 시세 정보를 나열하는 필드로 하나의 요청에 `type field` 는 여러 개를 명시할 수 있습니다.

자세한 요청 방법은 [타입별 요청 및 응답](https://apidocs.bithumb.com/reference/%ED%83%80%EC%9E%85%EB%B3%84-%EC%9A%94%EC%B2%AD-%EB%B0%8F-%EC%9D%91%EB%8B%B5) 을 확인하시길 바랍니다.

`is_only_snapshot`, `is_only_realtime` 필드는 생략 가능하며 모두 생략할 경우 스냅샷과 실시간 데이터 둘 다 수신합니다.

### Format Field

트래픽 부담이 클 때 사용하는 방법으로 `simple` 로 지정할 경우 응답 필드명이 간소화됩니다.

| 필드명 | 타입 | 내용 | 필수 여부 | 기본 값 |
| --- | --- | --- | --- | --- |
| format | String | 수신할 포맷<br>\- `DEFAULT`: 기본형<br>\- `SIMPLE` : 축약형 | X | `DEFAULT` |

```rdmd-code lang-undefined theme-light

```

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EC_A0_84_EC_B2_B4__EC_9E_85_EA_B8_88__EC_A3_BC_EC_86_8C__EC_A1_B0_ED_9A_8C.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%A0%84%EC%B2%B4-%EC%9E%85%EA%B8%88-%EC%A3%BC%EC%86%8C-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| net\_type | 입금 네트워크 | String |
| deposit\_address | 입금 주소 | String |
| secondary\_address | 2차 입금 주소 | String |

Authorization

string

required

Authorization token (JWT)

# `` 200      200

array of objects

object

currency

string

net\_type

string

deposit\_address

string

secondary\_address

string

# `` 400      400

object

error

object

name

string

message

string

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

33

1const jwt = require('jsonwebtoken');

2const { v4: uuidv4 } = require('uuid');

3const axios = require('axios')

4​

5const accessKey = '발급받은 API KEY'

6const secretKey = '발급받은 SECRET KEY'

7const apiUrl = 'https:/api.bithumb.com'

8​

9// Generate access token

10

const payload = {

11    access_key: accessKey,

12    nonce: uuidv4(),

13    timestamp: Date.now()

14};

15const jwtToken = jwt.sign(payload, secretKey)

16

const config = {

17

    headers: {

18        Authorization: `Bearer ${jwtToken}`

19    }

20}

21​

22// Call API

23axios.get(apiUrl + '/v1/deposits/coin_addresses', config)

24

    .then((response) => {

25        // handle to success

26        console.log('status: ', response.status)

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EC_9B_B9_EC_86_8C_EC_BC_93__EC_97_90_EB_9F_AC.md]
# Format

에러 발생 시 JSON 형식의 에러 메시지가 내려갑니다.

# Response

| 필드명 | 내용 | 타입 |
| --- | --- | --- |
| error | 에러 객체 | `Object` |
| error.name | 종류 | `String` |
| error.message | 메세지 | `String` |

# 에러 종류

### WRONG\_FORMAT

JSON

```rdmd-code lang-json theme-light

{"error":{"name":"WRONG_FORMAT","message":"Format 이 맞지 않습니다."}}
```

### NO\_TICKET

JSON

```rdmd-code lang-json theme-light

{"error":{"name":"NO_TICKET","message":"티켓이 존재하지 않거나, 유효하지 않습니다."}}
```

### NO\_TYPE

JSON

```rdmd-code lang-json theme-light

{"error":{"name":"NO_TYPE","message":"type 필드가 존재하지 않습니다."}}
```

### NO\_CODES

JSON

```rdmd-code lang-json theme-light

{"error":{"name":"NO_CODES","message":"codes 필드가 존재하지 않습니다."}}
```

### INVALID\_PARAM

JSON

```rdmd-code lang-json theme-light

{"error":{"name":"INVALID_PARAM","message":"codes 필드가 비어 있습니다."}}
```

### INVALID\_PARAM\_FORMAT

JSON

```rdmd-code lang-json theme-light

{"error":{"name":"INVALID_PARAM","message":"{}은 지원하지 않는 포맷입니다."}}
```

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EC_A3_BCweek__EC_BA_94_EB_93_A4.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Request Parameters**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%A3%BCweek-%EC%BA%94%EB%93%A4\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 마켓 코드 (ex. KRW-BTC) | String |
| to | 마지막 캔들 시각 (exclusive).<br>ISO8061 포맷 (yyyy-MM-dd'T'HH:mm:ss'Z' or yyyy-MM-dd HH:mm:ss). 기본적으로 KST 기준 시간이며 비워서 요청시 가장 최근 캔들 | String |
| count | 캔들 개수(최대 200개까지 요청 가능) | Integer |

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%A3%BCweek-%EC%BA%94%EB%93%A4\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 마켓명 | String |
| candle\_date\_time\_utc | 캔들 기준 시각(UTC 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |
| candle\_date\_time\_kst | 캔들 기준 시각(KST 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |
| opening\_price | 시가 | Double |
| high\_price | 고가 | Double |
| low\_price | 저가 | Double |
| trade\_price | 종가 | Double |
| timestamp | 캔들 종료 시각(KST 기준) | Long |
| candle\_acc\_trade\_price | 누적 거래 금액 | Double |
| candle\_acc\_trade\_volume | 누적 거래량 | Double |
| first\_day\_of\_period | 캔들 기간의 가장 첫 날 | String |

market

string

required

마켓 코드 (ex. KRW-BTC)

to

string

마지막 캔들 시각 (exclusive). 비워서 요청시 가장 최근 캔들

count

int32

Defaults to 1

캔들 개수(최대 200개까지 요청 가능)

# `` 200      200

array of objects

object

market

string

candle\_date\_time\_utc

string

candle\_date\_time\_kst

string

opening\_price

integer

Defaults to 0

high\_price

integer

Defaults to 0

low\_price

integer

Defaults to 0

trade\_price

integer

Defaults to 0

timestamp

integer

Defaults to 0

candle\_acc\_trade\_price

number

Defaults to 0

candle\_acc\_trade\_volume

number

Defaults to 0

first\_day\_of\_period

string

# `` 400      400

object

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

1const options = {method: 'GET', headers: {accept: 'application/json'}};

2​

3fetch('https://api.bithumb.com/v1/candles/weeks?count=1', options)

4  .then(response => response.json())

5  .then(response => console.log(response))

6  .catch(err => console.error(err));

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EC_97_B0_EA_B2_B0__EA_B4_80_EB_A6_AC.md]
# Connection 관리

### PING/PONG

빗썸 API WebSocket 서버는 커넥션을 안정적으로 관리/유지하기 위해 WebSocket PING/PONG Frame을 제공합니다.

(참고 문서 : [https://tools.ietf.org/html/rfc6455#section-5.5.2](https://tools.ietf.org/html/rfc6455#section-5.5.2) )

#### Client to Server PING

- 기본적으로 서버는 아무런 데이터도 수신, 발신 되지 않은 채 약 120초가 경과하면 Idle Timeout으로 WebSocket Connection을 종료합니다.
- 이를 방지하기 위해 클라이언트에서 서버로 PING 메시지를 보내서 Connection을 유지하고, WebSocket 서버의 상태와 WebSocket Connection Status를 파악할 수 있습니다.
- 빗썸 API WebSocket 서버에서는 PING Frame 수신 대응이 준비되어 있습니다. 간단한 구현으로 클라이언트에서 PING 요청/PONG 응답(PING에 대한 응답 Frame)을 통해 서버 상태를 파악할 수 있습니다.
- 이에 대한 구성은 해당 클라이언트 개발 문서를 확인하시기 바랍니다.


(대부분의 라이브러리는 ping 함수가 내장되어 있을 가능성이 높습니다.)
- 이외 PING 메시지를 보내 Connection을 유지할 수 있습니다.


Connection이 유지되고 있으면 {"status":"UP"} 응답을 10초 간격으로 받을 수 있습니다.

Shell

```rdmd-code lang-shell theme-light

$ wscat -c wss://ws-api.bithumb.com/websocket/v1
Connected (press CTRL+C to quit)

PING

{"status":"UP"}
{"status":"UP"}
{"status":"UP"}
...
```

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__ED_85_8C_EC_8A_A4_ED_8A_B8__EB_B0_8F__EC_9A_94_EC_B2_AD__EC_98_88_EC_A0_9C.md]
WebSocket을 이용한 시세 수신 테스트를 진행할 경우 telsocket 혹은 wscat을 사용할 수 있습니다.

> wscat 을 이용하는 경우

Shell

```rdmd-code lang-shell theme-light

$ npm install -g wscat
$ wscat -c wss://ws-api.bithumb.com/websocket/v1
connected!
```

> telsocket 을 이용하는 경우

Shell

```rdmd-code lang-shell theme-light

$ telsocket -url wss://ws-api.bithumb.com/websocket/v1
connected!
```

원화-비트코인(KRW-BTC) 마켓의 실시간 정보를 조회하고 싶다면 다음과 같이 요청할 수 있습니다.

Shell

```rdmd-code lang-shell theme-light

$ wscat -c wss://ws-api.bithumb.com/websocket/v1
Connected (press CTRL+C to quit)

[{"ticket":"test example"},{"type":"ticker","codes":["KRW-BTC"]}]

{"type":"ticker","code":"KRW-BTC","opening_price":484500,"high_price":493100,"low_price":472500,"trade_price":493100,"prev_closing_price":484500,"change":"RISE","change_price":8600,"signed_change_price":8600,"change_rate":0.01775026,"signed_change_rate":0.01775026,"trade_volume":3.2529,"acc_trade_volume":220.0447,"acc_trade_volume_24h":13380.57687512,"acc_trade_price":105917424.208256,"acc_trade_price_24h":8227950466.316009,"trade_date":"20240910","trade_time":"091617","trade_timestamp":1725927377174,"ask_bid":"BID","acc_ask_volume":106.7561,"acc_bid_volume":113.2886,"highest_52_week_price":999999000,"highest_52_week_date":"2024-06-18","lowest_52_week_price":1000,"lowest_52_week_date":"2024-06-18","market_state":"ACTIVE","is_trading_suspended":false,"delisting_date":null,"market_warning":"NONE","timestamp":1725927377287,"stream_type":"SNAPSHOT"}
{"type":"ticker","code":"KRW-BTC","opening_price":484500,"high_price":493100,"low_price":472500,"trade_price":493100,"prev_closing_price":484500,"change":"RISE","change_price":8600,"signed_change_price":8600,"change_rate":0.01775026,"signed_change_rate":0.01775026,"trade_volume":1.2567,"acc_trade_volume":225.622,"acc_trade_volume_24h":13386.15417512,"acc_trade_price":108663718.238256,"acc_trade_price_24h":8230696760.346009,"trade_date":"20240910","trade_time":"091617","trade_timestamp":1725927377820,"ask_bid":"BID","acc_ask_volume":106.7561,"acc_bid_volume":118.8659,"highest_52_week_price":999999000,"highest_52_week_date":"2024-06-18","lowest_52_week_price":1000,"lowest_52_week_date":"2024-06-18","market_state":"ACTIVE","is_trading_suspended":false,"delisting_date":null,"market_warning":"NONE","timestamp":1725927377931,"stream_type":"REALTIME"}
...
```

만약 동시에 여러 마켓의 정보를 수신하고 싶다면 codes 필드에 각 마켓을 쉼표(,)로 구분하여 입력해보세요.

예를 들어 간소화된 포맷으로 원화-비트코인(KRW-BTC) 마켓과 비트코인-이더리움(BTC-ETH) 마켓의 실시간 체결 정보를 수신하고 싶은 경우 다음과 같이 요청할 수 있습니다.

Shell

```rdmd-code lang-shell theme-light

$ wscat -c wss://ws-api.bithumb.com/websocket/v1
Connected (press CTRL+C to quit)

[{"ticket":"test example"},{"type":"ticker","codes":["KRW-BTC","BTC-ETH"]},{"format":"SIMPLE"}]

{"ty":"ticker","cd":"KRW-BTC","op":484500,"hp":493100,"lp":471300,"tp":493100,"pcp":484500,"c":"RISE","cp":8600,"scp":8600,"cr":0.01775026,"scr":0.01775026,"tv":4.6191,"atv":340.7347,"atv24h":13501.26687512,"atp":164142603.957128,"atp24h":8286175646.064881,"tdt":"20240910","ttm":"091942","ttms":1725927582096,"ab":"BID","aav":172.4423,"abv":168.2924,"h52wp":999999000,"h52wdt":"2024-06-18","l52wp":1000,"l52wdt":"2024-06-18","ms":"ACTIVE","its":false,"dd":null,"mw":"NONE","tms":1725927582208,"st":"SNAPSHOT"}
{"ty":"ticker","cd":"BTC-ETH","op":47890,"hp":48310,"lp":47700,"tp":47820,"pcp":47890,"c":"FALL","cp":70,"scp":-70,"cr":0.00146168,"scr":-0.00146168,"tv":37.2703,"atv":68.2069,"atv24h":19771.65533322,"atp":3274476.3628192,"atp24h":728107452.06423197609921044,"tdt":"20240910","ttm":"092001","ttms":1725927601164,"ab":"BID","aav":34.0163,"abv":34.1906,"h52wp":774400000,"h52wdt":"2024-01-23","l52wp":254,"l52wdt":"2024-06-20","ms":"ACTIVE","its":false,"dd":null,"mw":"CAUTION","tms":1725927601272,"st":"SNAPSHOT"}
{"ty":"ticker","cd":"KRW-BTC","op":484500,"hp":493100,"lp":471300,"tp":489100,"pcp":484500,"c":"RISE","cp":4600,"scp":4600,"cr":0.00949432,"scr":0.00949432,"tv":2.0067,"atv":345.3538,"atv24h":13505.88597512,"atp":166420282.167128,"atp24h":8288453324.274881,"tdt":"20240910","ttm":"092008","ttms":1725927608215,"ab":"ASK","aav":172.4423,"abv":172.9115,"h52wp":999999000,"h52wdt":"2024-06-18","l52wp":1000,"l52wdt":"2024-06-18","ms":"ACTIVE","its":false,"dd":null,"mw":"NONE","tms":1725927608323,"st":"REALTIME"}
{"ty":"ticker","cd":"BTC-ETH","op":47890,"hp":48310,"lp":47570,"tp":47570,"pcp":47890,"c":"FALL","cp":320,"scp":-320,"cr":0.00668198,"scr":-0.00668198,"tv":12.55117013,"atv":174.6851,"atv24h":19797.96498024,"atp":8350427.8249361,"atp24h":730024172.79764567609921044,"tdt":"20240910","ttm":"092014","ttms":1725927614331,"ab":"ASK","aav":103.2242,"abv":71.4609,"h52wp":774400000,"h52wdt":"2024-01-23","l52wp":254,"l52wdt":"2024-06-20","ms":"ACTIVE","its":false,"dd":null,"mw":"CAUTION","tms":1725927614457,"st":"REALTIME"}
 ...
```

스냅샷이 먼저 내려온 뒤 실시간 체결 현황이 수신됨을 알 수 있습니다.

위의 모든 요청은 WebSocket이 정상적으로 연결되었다는 전제로 가정합니다.

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EA_B0_9C_EB_B3_84__EC_B6_9C_EA_B8_88__EC_A1_B0_ED_9A_8C.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Request Parameters**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EA%B0%9C%EB%B3%84-%EC%B6%9C%EA%B8%88-%EC%A1%B0%ED%9A%8C\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| currency \* | 화폐를 의미하는 영문 대문자 코드 | String |
| uuid | 출금의 고유 아이디 | String |
| txid | 출금의 트랜잭션 아이디 | String |

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EA%B0%9C%EB%B3%84-%EC%B6%9C%EA%B8%88-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| type | 입출금 종류 | String |
| uuid | 출금의 고유 아이디 | String |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| net\_type | 출금 네트워크 | String |
| txid | 출금의 트랜잭션 아이디 | String |
| state | 출금 상태<br>`- PROCESSING : 진행중`<br>`- DONE : 완료`<br>`- CANCELLED : 취소됨` | String |
| created\_at | 출금 생성 시간 | DateString |
| done\_at | 출금 완료 시간 | DateString |
| amount | 출금 금액/수량 | NumberString |
| fee | 출금 수수료 | NumberString |
| transaction\_type | 출금 유형<br>`- default : 일반출금` | String |

currency

string

required

화폐를 의미하는 영문 대문자 코드

uuid

string

출금 UUID

txid

string

출금 TXID

Authorization

string

required

Authorization token (JWT)

# `` 200      200

object

type

string

uuid

string

currency

string

net\_type

string

txid

string

state

string

created\_at

string

done\_at

string

amount

string

fee

string

transaction\_type

string

# `` 400      400

object

error

object

name

string

message

string

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

43

1const jwt = require('jsonwebtoken');

2const { v4: uuidv4 } = require('uuid');

3const crypto = require('crypto');

4const querystring = require('querystring');

5const axios = require('axios')

6​

7const accessKey = '발급받은 API KEY'

8const secretKey = '발급받은 SECRET KEY'

9const apiUrl = 'https://api.bithumb.com'

10​

11// Set API parameters

12const query = 'currency=MTL'

13​

14// Generate access token

15const alg = 'SHA512'

16const hash = crypto.createHash(alg)

17const queryHash = hash.update(query, 'utf-8').digest('hex')

18

const payload = {

19    access_key: accessKey,

20    nonce: uuidv4(),

21    timestamp: Date.now(),

22    query_hash: queryHash,

23    query_hash_alg: alg

24}

25const jwtToken = jwt.sign(payload, secretKey)

26

const config = {

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EA_B0_9C_EB_B3_84__EC_A3_BC_EB_AC_B8__EC_A1_B0_ED_9A_8C.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Request Parameters**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EA%B0%9C%EB%B3%84-%EC%A3%BC%EB%AC%B8-%EC%A1%B0%ED%9A%8C\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| uuid \* | 주문 UUID | String |

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EA%B0%9C%EB%B3%84-%EC%A3%BC%EB%AC%B8-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| uuid | 주문의 고유 아이디 | String |
| side | 주문 종류 | String |
| ord\_type | 주문 방식 | String |
| price | 주문 당시 화폐 가격 | NumberString |
| state | 주문 상태 | String |
| market | 마켓의 유일키 | String |
| created\_at | 주문 생성 시간 | DateString |
| volume | 사용자가 입력한 주문 양 | NumberString |
| remaining\_volume | 체결 후 남은 주문 양 | NumberString |
| reserved\_fee | 수수료로 예약된 비용 | NumberString |
| remaining\_fee | 남은 수수료 | NumberString |
| paid\_fee | 사용된 수수료 | NumberString |
| locked | 거래에 사용중인 비용 | NumberString |
| executed\_volume | 체결된 양 | NumberString |
| trades\_count | 해당 주문에 걸린 체결 수 | Integer |
| trades | 체결 | Array\[Object\] |
| trades.market | 마켓의 유일 키 | String |
| trades.uuid | 체결의 고유 아이디 | String |
| trades.price | 체결 가격 | NumberString |
| trades.volume | 체결 양 | NumberString |
| trades.funds | 체결된 총 가격 | NumberString |
| trades.side | 체결 종류 | String |
| trades.created\_at | 체결 시각 | DateString |

uuid

string

required

주문 UUID

Authorization

string

required

Authorization token (JWT)

# `` 200      200

object

uuid

string

side

string

ord\_type

string

price

string

state

string

market

string

created\_at

string

volume

string

remaining\_volume

string

reserved\_fee

string

remaining\_fee

string

paid\_fee

string

locked

string

executed\_volume

string

trades\_count

integer

Defaults to 0

trades

array of objects

trades

object

market

string

uuid

string

price

string

volume

string

funds

string

side

string

created\_at

string

# `` 400      400

object

error

object

name

string

message

string

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

43

1const jwt = require('jsonwebtoken');

2const { v4: uuidv4 } = require('uuid');

3const crypto = require('crypto');

4const querystring = require('querystring');

5const axios = require('axios')

6​

7const accessKey = '발급받은 API KEY'

8const secretKey = '발급받은 SECRET KEY'

9const apiUrl = 'https://api.bithumb.com'

10​

11// Set API parameters

12const query = 'uuid=C0295000000000100020'

13​

14// Generate access token

15const alg = 'SHA512'

16const hash = crypto.createHash(alg)

17const queryHash = hash.update(query, 'utf-8').digest('hex')

18

const payload = {

19    access_key: accessKey,

20    nonce: uuidv4(),

21    timestamp: Date.now(),

22    query_hash: queryHash,

23    query_hash_alg: alg

24}

25const jwtToken = jwt.sign(payload, secretKey)

26

const config = {

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EA_B0_9C_EB_B3_84__EC_9E_85_EA_B8_88__EC_A3_BC_EC_86_8C__EC_A1_B0_ED_9A_8C.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Request Parameters**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EA%B0%9C%EB%B3%84-%EC%9E%85%EA%B8%88-%EC%A3%BC%EC%86%8C-%EC%A1%B0%ED%9A%8C\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| currency \* | 화폐를 의미하는 영문 대문자 코드 | String |
| net\_type \* | 입금 네트워크 | String |

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EA%B0%9C%EB%B3%84-%EC%9E%85%EA%B8%88-%EC%A3%BC%EC%86%8C-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| net\_type | 입금 네트워크 | String |
| deposit\_address | 입금 주소 | String |
| secondary\_address | 2차 입금 주소 | String |

currency

string

required

화폐를 의미하는 영문 대문자 코드

net\_type

string

required

입금 네트워크

Authorization

string

required

Authorization token (JWT)

# `` 200      200

object

currency

string

net\_type

string

deposit\_address

string

secondary\_address

string

# `` 400      400

object

error

object

name

string

message

string

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

43
axios.get(apiUrl + '/v1/deposits/coin_address?' + query, config)

1const jwt = require('jsonwebtoken');

2const { v4: uuidv4 } = require('uuid');

3const crypto = require('crypto');

4const querystring = require('querystring');

5const axios = require('axios')

6​

7const accessKey = '발급받은 API KEY'

8const secretKey = '발급받은 SECRET KEY'

9const apiUrl = 'https://api.bithumb.com'

10​

11// Set API parameters

12const query = 'currency=BTC&net_type=BTC'

13​

14// Generate access token

15const alg = 'SHA512'

16const hash = crypto.createHash(alg)

17const queryHash = hash.update(query, 'utf-8').digest('hex')

18

const payload = {

19    access_key: accessKey,

20    nonce: uuidv4(),

21    timestamp: Date.now(),

22    query_hash: queryHash,

23    query_hash_alg: alg

24}

25const jwtToken = jwt.sign(payload, secretKey)

26

const config = {

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_docs__EC_9E_90_EC_A3_BC__EB_AC_BB_EB_8A_94__EC_A7_88_EB_AC_B8_faq.md]
## 출금 API를 이용하는데 invalid Parameter 에러가 확인됩니다   [Skip link to 출금 API를 이용하는데 invalid Parameter 에러가 확인됩니다](https://apidocs.bithumb.com/v2.1.5/docs/%EC%9E%90%EC%A3%BC-%EB%AC%BB%EB%8A%94-%EC%A7%88%EB%AC%B8-faq\#%EC%B6%9C%EA%B8%88-api%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%98%EB%8A%94%EB%8D%B0-invalid-parameter-%EC%97%90%EB%9F%AC%EA%B0%80-%ED%99%95%EC%9D%B8%EB%90%A9%EB%8B%88%EB%8B%A4)

Text

```rdmd-code lang-text theme-light

‘특정 금융거래 정보의 보고 및 이용에 관한 법률’에 따라 2022년 3월 25일부터 빗썸 외 지갑으로 가상자산을 출금하는 경우, 가상자산 송/수신인 정보를 제공할 수 있는 VASP로의 이전만을 허용하게 되었습니다.

출금 API를 통해 빗썸 외 지갑으로 출금을 진행하시는 경우, 아래 항목을 반드시 확인 해주세요.

◾ 개인 지갑으로 출금 시 필수 요청 변수
  - exchange_name : 출금 거래소 영문명
  - receiver_type : 수취인 개인/법인 여부 (개인: 'personal', 법인: 'corporation')
  - ko_name : 개인 수취 정보_국문 성명
  - en_name : 개인 수취 정보_영문 성명

◾ 법인 지갑으로 출금 시 필수 요청 변수
  - exchange_name : 출금 거래소 영문명
  - corp_ko_name : 법인 수취 정보_국문 법인명
  - corp_en_name : 법인 수취 정보_영문 법인명
  - corp_rep_ko_name : 법인 수취 정보_국문 법인 대표자명
  - corp_rep_en_name : 법인 수취 정보_영문 법인 대표자명

invalid Parameter 외에 ‘다시 시도’ 해달라는 에러가 확인되는 경우, 입력하신 수취인 정보와 실제 수취인 정보가 다를 수 있으니 수취인 정보를 재확인 해주시기 바랍니다.
```

## API 호출 시 IP가 차단되었다고 확인됩니다   [Skip link to API 호출 시 IP가 차단되었다고 확인됩니다](https://apidocs.bithumb.com/v2.1.5/docs/%EC%9E%90%EC%A3%BC-%EB%AC%BB%EB%8A%94-%EC%A7%88%EB%AC%B8-faq\#api-%ED%98%B8%EC%B6%9C-%EC%8B%9C-ip%EA%B0%80-%EC%B0%A8%EB%8B%A8%EB%90%98%EC%97%88%EB%8B%A4%EA%B3%A0-%ED%99%95%EC%9D%B8%EB%90%A9%EB%8B%88%EB%8B%A4)

Text

```rdmd-code lang-text theme-light

빗썸 Open API는 안정적인 서비스 제공을 위해 API 별 요청 수를 제한합니다.
제한된 요청 수 이상으로 초과 요청하시는 경우 IP가 일시적으로 차단되오니 이용에 주의하시기 바랍니다.

◾ Public API
  - 1초당 최대 150회 요청 가능
  - 초과 요청하는 경우 1분 제한

◾ Private API
  - 1초당 최대 140회 요청 가능
  - 초과 요청하는 경우 Private info : 5분 제한 / Private trade : 10분 제한

제한 시간이 경과하면 차단이 자동 해제되며, 실패 호출도 제한에 포함되오니 참고 부탁드립니다.
```

Updatedabout 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_docs_api__EC_86_8C_EA_B0_9C.md]
API 이용안내 페이지

- _![icon](https://content.bithumb.com/apidocs/img/public-api.webp)_

## PUBLIC API


  - [시세 종목 조회](https://apidocs.bithumb.com/v2.1.0/reference/%EB%A7%88%EC%BC%93%EC%BD%94%EB%93%9C-%EC%A1%B0%ED%9A%8C)
  - [시세 캔들 조회](https://apidocs.bithumb.com/v2.1.0/reference/%EB%B6%84minute-%EC%BA%94%EB%93%A4-1)
  - [시세 체결 조회](https://apidocs.bithumb.com/v2.1.0/reference/%EC%B5%9C%EA%B7%BC-%EC%B2%B4%EA%B2%B0-%EB%82%B4%EC%97%AD)
  - [시세 현재가(Ticker) 조회](https://apidocs.bithumb.com/v2.1.0/reference/%ED%98%84%EC%9E%AC%EA%B0%80-%EC%A0%95%EB%B3%B4)
  - [시세 호가 정보(Orderbook) 조회](https://apidocs.bithumb.com/v2.1.0/reference/%ED%98%B8%EA%B0%80-%EC%A0%95%EB%B3%B4-%EC%A1%B0%ED%9A%8C)
  - [서비스 정보](https://apidocs.bithumb.com/v2.1.0/reference/%EA%B2%BD%EB%B3%B4%EC%A0%9C)
- _![icon](https://content.bithumb.com/apidocs/img/private-api.webp)_

## PRIVATE API


  - [자산](https://apidocs.bithumb.com/v2.1.0/reference/%EC%A0%84%EC%B2%B4-%EA%B3%84%EC%A2%8C-%EC%A1%B0%ED%9A%8C)
  - [주문](https://apidocs.bithumb.com/v2.1.0/reference/%EC%A3%BC%EB%AC%B8-%EA%B0%80%EB%8A%A5-%EC%A0%95%EB%B3%B4)
  - [출금](https://apidocs.bithumb.com/v2.1.0/reference/%EC%B6%9C%EA%B8%88-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C)
  - [입금](https://apidocs.bithumb.com/v2.1.0/reference/%EC%9E%85%EA%B8%88-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C)
  - [서비스 정보](https://apidocs.bithumb.com/v2.1.0/reference/%EC%9E%85%EC%B6%9C%EA%B8%88-%ED%98%84%ED%99%A9)

- [_![icon](https://content.bithumb.com/apidocs/img/apikey1.png)_ \\
API KEY 발급 페이지로 이동](https://bithumb.com/react/api-support/management-api)
- [_![icon](https://content.bithumb.com/apidocs/img/apikey2.png)_ \\
API KEY 발급 방법 안내받기](https://www.bithumb.com/customer_support/info_guide?seq=6703&categorySeq=612)

Updatedabout 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_docs__EC_9D_B8_EC_A6_9D__ED_97_A4_EB_8D_94__EB_A7_8C_EB_93_A4_EA_B8_B0.md]
## REST API 요청 포맷   [Skip link to REST API 요청 포맷](https://apidocs.bithumb.com/v2.1.5/docs/%EC%9D%B8%EC%A6%9D-%ED%97%A4%EB%8D%94-%EB%A7%8C%EB%93%A4%EA%B8%B0\#rest-api-%EC%9A%94%EC%B2%AD-%ED%8F%AC%EB%A7%B7)

REST API는 HTTP를 통해 호출이 이루어집니다.

POST, PUT, DELETE 요청에 body가 존재하는 경우 JSON 형식으로 파라미터를 전송해야 합니다.

유효한 컨텐츠 타입의 예시는 다음과 같으며, 각 프로그래밍 언어 라이브러리에 따라 약간의 차이가 있을 수 있습니다.

```
Content-Type: application/json; charset=utf-8
```

## JWT 인증 토큰 만들기   [Skip link to JWT 인증 토큰 만들기](https://apidocs.bithumb.com/v2.1.5/docs/%EC%9D%B8%EC%A6%9D-%ED%97%A4%EB%8D%94-%EB%A7%8C%EB%93%A4%EA%B8%B0\#jwt-%EC%9D%B8%EC%A6%9D-%ED%86%A0%ED%81%B0-%EB%A7%8C%EB%93%A4%EA%B8%B0)

REST API 요청시, 발급받은 `API Key` 와 `Secret Key` 로 토큰을 생성하여 `Authorization` 헤더를 통해 전송합니다. 토큰은 JWT( [https://jwt.io](https://jwt.io/)) 형식을 따릅니다.

서명 방식은 `HS256` 을 권장하며, 서명에 사용할 Secret은 발급받은 `Secret Key` 를 사용합니다.

페이로드의 구성은 다음과 같습니다.

Private API 요청 시 발급받은 `API Key` 와 `Secret Key` 를 이용하여 5개의 파라미터를 헤더에 추가하여 전송합니다.

| 요청 변수 | 설명 | 타입 |
| --- | --- | --- |
| access\_key | 사용자 API Key | String / 필수 |
| nonce | 무작위의 UUID 문자열 | String / 필수 |
| timestamp | 현재의 시간을 밀리초 (millisecond, ms)로 표현한 값<br>(예 : 1655280216476) | Number / 필수 |
| query\_hash | 해싱된 query string (파라미터가 있을 경우 필수) | String / 옵션 |
| query\_hash\_alg | query\_hash를 생성하는 데에 사용한 알고리즘 (기본값 : SHA512) | String / 옵션 |

생성된 인증 헤더의 페이로드 예시입니다.

JSON

```rdmd-code lang-json theme-light

{
  "access_key": "L7rVaYfBIc2BDsnlQGfkR93d6DoOAJCw7mJr5Eso",
  "nonce": "6f5570df-d8bc-4daf-85b4-976733feb624",
  "timestamp": 1712230310689,
  "query_hash": "1c2362ca9d79947582cae192acf63efb8756caa49af1eb64b12ba45617165431a3dd3e47d0476bc2a347b7a1ea512db7f316f56144084b1493166e3c9113a8eb",
  "query_hash_alg": "SHA512"
}
```

### (예시) 파라미터가 없을 경우   [Skip link to (예시) 파라미터가 없을 경우](https://apidocs.bithumb.com/v2.1.5/docs/%EC%9D%B8%EC%A6%9D-%ED%97%A4%EB%8D%94-%EB%A7%8C%EB%93%A4%EA%B8%B0\#%EC%98%88%EC%8B%9C-%ED%8C%8C%EB%9D%BC%EB%AF%B8%ED%84%B0%EA%B0%80-%EC%97%86%EC%9D%84-%EA%B2%BD%EC%9A%B0)

NodePythonJava

```rdmd-code lang-javascript theme-light

const jwt = require('jsonwebtoken')
const { v4: uuidv4 } = require('uuid')

const accessKey = '발급받은 API KEY'
const secretKey = '발급받은 SECRET KEY'

const payload = {
    access_key: accessKey,
    nonce: uuidv4(),
    timestamp: Date.now()
};

console.log(payload);

const jwtToken = jwt.sign(payload, secretKey)
const authorizationToken = `Bearer ${jwtToken}`

console.log(authorizationToken);
```

```rdmd-code lang-python theme-light

# Python 3
# pip3 installl pyJwt
import jwt
import uuid
import time

accessKey = "발급받은 API KEY"
secretKey = "발급받은 SECRET KEY"

payload = {
    'access_key': accessKey,
    'nonce': str(uuid.uuid4()),
    'timestamp': round(time.time() * 1000)
}

print(payload, "\n")

jwt_token = jwt.encode(payload, secretKey)
authorization_token = 'Bearer {}'.format(jwt_token)

print(authorization_token)
```

```rdmd-code lang-java theme-light

// https://mvnrepository.com/artifact/com.auth0/java-jwt
import com.auth0.jwt.JWT;
import com.auth0.jwt.algorithms.Algorithm;

import java.util.UUID;

public class OpenAPIAuthSampleNoArgs {

    public static void main(String[] args) {
        String accessKey = "발급받은 API KEY";
        String secretKey = "발급받은 SECRET KEY";

        Algorithm algorithm = Algorithm.HMAC256(secretKey);

        String jwtToken = JWT.create()
                .withClaim("access_key", accessKey)
                .withClaim("nonce", UUID.randomUUID().toString())
                .withClaim("timestamp", System.currentTimeMillis())
                .sign(algorithm);

        String authenticationToken = "Bearer " + jwtToken;

        System.out.println(authenticationToken);
    }
}
```

### (예시) 파라미터가 있는 경우   [Skip link to (예시) 파라미터가 있는 경우](https://apidocs.bithumb.com/v2.1.5/docs/%EC%9D%B8%EC%A6%9D-%ED%97%A4%EB%8D%94-%EB%A7%8C%EB%93%A4%EA%B8%B0\#%EC%98%88%EC%8B%9C-%ED%8C%8C%EB%9D%BC%EB%AF%B8%ED%84%B0%EA%B0%80-%EC%9E%88%EB%8A%94-%EA%B2%BD%EC%9A%B0)

HTTP 쿼리 문자열, 혹은 body를 통해 파라미터를 전달하는 경우 모두 JWT 페이로드의 query\_hash 값을 설정해야합니다.

파라미터의 자료형 중 배열이 존재하는 경우, 올바른 query string의 형태는 다음과 같습니다.

`key[]=value1&key[]=value2 ...`

이와 다른 형태로 요청하면 토큰 검증에 실패할 수 있으니 유의하시기 바랍니다.

NodePythonJava

```rdmd-code lang-javascript theme-light

const jwt = require('jsonwebtoken');
const { v4: uuidv4 } = require('uuid');
const crypto = require('crypto');
const querystring = require('querystring');

const accessKey = '발급받은 API KEY'
const secretKey = '발급받은 SECRET KEY'

// GET (query parameters)
// const query = 'string=abc&number=123'
// POST (request body)
const query = querystring.encode({
    string: 'abc',
    number: 123
})

const alg = 'SHA512'
const hash = crypto.createHash(alg)
const queryHash = hash.update(query, 'utf-8').digest('hex')

const payload = {
    access_key: accessKey,
    nonce: uuidv4(),
    timestamp: Date.now(),
    query_hash: queryHash,
    query_hash_alg: alg
};

console.log(payload);

const jwtToken = jwt.sign(payload, secretKey)
const authorizationToken = `Bearer ${jwtToken}`

console.log(authorizationToken);
```

```rdmd-code lang-python theme-light

# Python 3
# pip3 installl pyJwt
import jwt
import uuid
import hashlib
import time
from urllib.parse import urlencode

accessKey = "발급받은 API KEY"
secretKey = "발급받은 SECRET KEY"

# GET (query parameters)
# query = 'string=abc&number=123'.encode()
# POST (request body)
query = urlencode(dict( string="abc", number=123 )).encode()

hash = hashlib.sha512()
hash.update(query)
query_hash = hash.hexdigest()

payload = {
    'access_key': accessKey,
    'nonce': str(uuid.uuid4()),
    'timestamp': round(time.time() * 1000),
    'query_hash': query_hash,
    'query_hash_alg': 'SHA512',
}

print(payload, "\n")

jwt_token = jwt.encode(payload, secretKey)
authorization_token = 'Bearer {}'.format(jwt_token)

print(authorization_token)
```

```rdmd-code lang-java theme-light

// https://mvnrepository.com/artifact/com.auth0/java-jwt
import com.auth0.jwt.JWT;
import com.auth0.jwt.algorithms.Algorithm;
// https://mvnrepository.com/artifact/org.apache.httpcomponents/httpclient
import org.apache.http.NameValuePair;
import org.apache.http.client.utils.URLEncodedUtils;
import org.apache.http.message.BasicNameValuePair;

import java.math.BigInteger;
import java.nio.charset.StandardCharsets;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;
import java.util.ArrayList;
import java.util.List;
import java.util.UUID;

public class OpenAPIAuthSampleArgs {

    public static void main(String[] args) throws NoSuchAlgorithmException {

        String accessKey = "발급받은 API KEY";
        String secretKey = "발급받은 SECRET KEY";

        // GET (query parameters)
				// String query = "string=abc&number=123";
        // POST (request body)
        List<NameValuePair> queryParams = new ArrayList<>();
        queryParams.add(new BasicNameValuePair("string", "abc"));
        queryParams.add(new BasicNameValuePair("number", "123"));
        String query = URLEncodedUtils.format(queryParams, StandardCharsets.UTF_8);

        MessageDigest md = MessageDigest.getInstance("SHA-512");
        md.update(query.getBytes(StandardCharsets.UTF_8));

        String queryHash = String.format("%0128x", new BigInteger(1, md.digest()));

        Algorithm algorithm = Algorithm.HMAC256(secretKey);
        String jwtToken = JWT.create()
                .withClaim("access_key", accessKey)
                .withClaim("nonce", UUID.randomUUID().toString())
                .withClaim("timestamp", System.currentTimeMillis())
                .withClaim("query_hash", queryHash)
                .withClaim("query_hash_alg", "SHA512")
                .sign(algorithm);

        String authenticationToken = "Bearer " + jwtToken;

        System.out.println(authenticationToken);
    }
}
```

Updatedabout 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__ED_98_B8_EA_B0_80__EC_A0_95_EB_B3_B4__EC_A1_B0_ED_9A_8C.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%ED%98%B8%EA%B0%80-%EC%A0%95%EB%B3%B4-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 마켓 코드 | String |
| timestamp | 호가 생성 시각 | Long |
| total\_ask\_size | 호가 매도 총 잔량 | Double |
| total\_bid\_size | 호가 매수 총 잔량 | Double |
| orderbook\_units | 호가 | List of Objects |
| ask\_price | 매도호가 | Double |
| bid\_price | 매수호가 | Double |
| ask\_size | 매도 잔량 | Double |
| bid\_size | 매수 잔량 | Double |

`orderbook_units` 리스트에는 15호가 정보를 차례대로(1호가, 2호가 ... 15호가) 담고 있습니다. 단, `market` 에 단일 마켓 코드만 입력 시 `orderbook_units` 리스트에 30호가까지의 정보를 제공합니다.\`

markets

array of strings

required

마켓 코드 목록 (ex. KRW-BTC,BTC-ETH)

markets\*
ADD string

# `` 200      200

array of objects

object

market

string

timestamp

integer

Defaults to 0

total\_ask\_size

number

Defaults to 0

total\_bid\_size

number

Defaults to 0

orderbook\_units

array of objects

orderbook\_units

object

ask\_price

integer

Defaults to 0

bid\_price

integer

Defaults to 0

ask\_size

number

Defaults to 0

bid\_size

number

Defaults to 0

# `` 400      400

object

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

1const options = {method: 'GET', headers: {accept: 'application/json'}};

2​

3fetch('https://api.bithumb.com/v1/orderbook', options)

4  .then(response => response.json())

5  .then(response => console.log(response))

6  .catch(err => console.error(err));

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference_api__ED_82_A4__EB_A6_AC_EC_8A_A4_ED_8A_B8__EC_A1_B0_ED_9A_8C.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

API는 [해당페이지](https://bithumb.com/react/api-support/management-api) 에서 API Key를 발급 받은 후 사용 가능합니다.
API Key 발급 시에는 API 활성 항목과 해당 API Key를 사용할 IP 주소를 등록해야 합니다.
IP 주소는 최대 5개까지 등록 가능하며 등록한 IP 주소로 접속한 경우에만 해당 API Key를 사용할 수 있습니다.
API Key는 계정당 10개까지 발급 받을 수 있으며 API Key 발급이 완료된 이후에는 Secret key를 추가로 확인할 수 없습니다. Secret key는 발급 받은 이후 안전한 곳에 별도 보관해주시기 바랍니다.
발급 받은 API Key는 발급일 기준으로 1년 동안 사용 가능하며 기간 연장은 불가능합니다. 1년 경과 시 해당 API Key는 삭제 후 재발급 받아주시기 바랍니다.
API Key 발급, 수정, 삭제 시에는 2채널 추가 인증이 진행되며, API 활성 항목 변경이 필요한 경우 [API Key 관리](https://bithumb.com/react/api-support/management-api) 에서 해당 해당 API Key를 삭제한 후 재발급 받아야 합니다.

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/api-%ED%82%A4-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| access\_key | API KEY | String |
| expire\_at | 만료일시 | DateString |

Authorization

string

required

Authorization token (JWT)

# `` 200      200

array of objects

object

access\_key

string

expire\_at

string

# `` 400      400

object

error

object

name

string

message

string

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

33

1const jwt = require('jsonwebtoken');

2const { v4: uuidv4 } = require('uuid');

3const axios = require('axios')

4​

5const accessKey = '발급받은 API KEY'

6const secretKey = '발급받은 SECRET KEY'

7const apiUrl = 'https:/api.bithumb.com'

8​

9// Generate access token

10

const payload = {

11    access_key: accessKey,

12    nonce: uuidv4(),

13    timestamp: Date.now()

14};

15const jwtToken = jwt.sign(payload, secretKey)

16

const config = {

17

    headers: {

18        Authorization: `Bearer ${jwtToken}`

19    }

20}

21​

22// Call API

23axios.get(apiUrl + '/v1/api_keys', config)

24

    .then((response) => {

25        // handle to success

26        console.log('status: ', response.status)

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EC_A3_BC_EB_AC_B8_ED_95_98_EA_B8_B0.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Request Parameters**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%A3%BC%EB%AC%B8%ED%95%98%EA%B8%B0\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market \* | 마켓 ID | String |
| side \* | 주문 종류<br>`- bid : 매수`<br>`- ask : 매도` | String |
| order\_type\* | 주문 방식 (구 ord\_type)<br>`- limit : 지정가 주문`<br>`- price : 시장가 주문(매수)`<br>`- market : 시장가 주문(매도)` | String |
| price \* | 주문 가격. (지정가, 시장가 매수 시 필수)<br>`ex) KRW-BTC 마켓에서 1BTC당 1,000 KRW로 거래할 경우, 값은 1000 이 된다.`<br>`ex) KRW-BTC 마켓에서 1BTC당 매도 1호가가 500 KRW 인 경우, 시장가 매수 시 값을 1000으로 세팅하면 2BTC가 매수된다.`<br>(수수료가 존재하거나 매도 1호가의 수량에 따라 상이할 수 있음) | NumberString |
| volume \* | 주문량 (지정가, 시장가 매도 시 필수) | NumberString |

> ### 🚧  안내사항
>
> - API로 지정가 주문시(Taker) 본인의 미체결 주문(Maker)과 체결될 확률이 높은 주문(자전거래 위험 주문)에 대하여 주문 불가 처리 됩니다. 자세한 내용은 [공지사항](https://apidocs.bithumb.com/v2.1.5/changelog/%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-api%EB%A5%BC-%ED%86%B5%ED%95%9C-%EC%A3%BC%EB%AC%B8-%EA%B4%80%EB%A0%A8-%EC%9E%90%EC%A0%84%EA%B1%B0%EB%9E%98-%EB%B0%A9%EC%A7%80-%EC%8B%9C%EC%8A%A4%ED%85%9C-%EB%8F%84%EC%9E%85-%EC%95%88%EB%82%B4#/) 을 참고하세요.
> - 요청 파라미터 "주문 방식"이 `order_type` 으로 변경되었습니다.
> - 응답 항목 "주문의 고유 아이디"는 `order_id` 로, "주문 방식"은 `order_type` 으로 변경되었습니다.

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%A3%BC%EB%AC%B8%ED%95%98%EA%B8%B0\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| order\_id | 주문의 고유 아이디 (구 uuid) | String |
| market | 마켓의 유일키 | String |
| side | 주문 종류 | String |
| order\_type | 주문 방식 (구 ord\_type) | String |
| created\_at | 주문 생성 시간 | DateString |

market

string

required

Market ID

side

string

required

주문 종류

price

string

required

유닛당 주문 가격

volume

string

required

주문 수량

order\_type

string

required

주문 방식 (구 ord\_type)

Authorization

string

required

Authorization token (JWT)

# `` 201      201

object

uuid

string

market

string

side

string

ord\_type

string

price

string

volume

string

created\_at

string

# `` 400      400

object

error

object

name

string

message

string

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

51

1const jwt = require('jsonwebtoken');

2const { v4: uuidv4 } = require('uuid');

3const crypto = require('crypto');

4const querystring = require('querystring');

5const axios = require('axios')

6​

7const accessKey = '발급받은 API KEY'

8const secretKey = '발급받은 SECRET KEY'

9const apiUrl = 'https:/api.bithumb.com'

10​

11// Set API parameters

12

const requestBody = {

13    market: 'KRW-BTC',

14    side: 'bid',

15    order_type: 'limit',

16    price: 84000000,

17    volume: 0.001

18}

19​

20// Generate access token

21const query = querystring.encode(requestBody)

22const alg = 'SHA512'

23const hash = crypto.createHash(alg)

24const queryHash = hash.update(query, 'utf-8').digest('hex')

25

const payload = {

26    access_key: accessKey,

```

Choose an example:

application/json

`` 201 - Result`` 400 - Result

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_changelog.md]
# [\[업데이트\] 신규 베타 버전 (V2.1.5) : 주문 및 취소 개선 안내](https://apidocs.bithumb.com/changelog/%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-%EC%8B%A0%EA%B7%9C-%EB%B2%A0%ED%83%80-%EB%B2%84%EC%A0%84-v215-%EC%A3%BC%EB%AC%B8-%EB%B0%8F-%EC%B7%A8%EC%86%8C-%EA%B0%9C%EC%84%A0-%EC%95%88%EB%82%B4)

about 1 month agoby bithumb api

안녕하세요.

대한민국 대표 거래소 빗썸입니다.

# [\[업데이트\] API를 통한 주문 관련 자전거래 방지 시스템 도입 안내](https://apidocs.bithumb.com/changelog/%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-api%EB%A5%BC-%ED%86%B5%ED%95%9C-%EC%A3%BC%EB%AC%B8-%EA%B4%80%EB%A0%A8-%EC%9E%90%EC%A0%84%EA%B1%B0%EB%9E%98-%EB%B0%A9%EC%A7%80-%EC%8B%9C%EC%8A%A4%ED%85%9C-%EB%8F%84%EC%9E%85-%EC%95%88%EB%82%B4)

6 months agoby bithumb api

안녕하세요.

# [\[업데이트\] Public Websocket : Snapshot 기능 지원 안내](https://apidocs.bithumb.com/changelog/%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-public-websocket-snapshot-%EA%B8%B0%EB%8A%A5-%EC%A7%80%EC%9B%90-%EC%95%88%EB%82%B4)

7 months agoby bithumb api

안녕하세요.

# [\[업데이트\] Private Websocket 오픈 : MyOrder, MyAsset 지원 안내](https://apidocs.bithumb.com/changelog/%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-private-websocket-%EC%98%A4%ED%94%88-myorder-myasset-%EC%A7%80%EC%9B%90-%EC%95%88%EB%82%B4)

7 months agoby bithumb api

안녕하세요.

# [빗썸 API Docs 업데이트 안내 (24/09/12)](https://apidocs.bithumb.com/changelog/%EB%B9%97%EC%8D%B8-api-docs-%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-%EC%95%88%EB%82%B4-240912)

8 months agoby bithumb api

안녕하세요.

No.1 가상자산 플랫폼, 빗썸입니다.

# [빗썸 API 신규 베타 버전 오픈 안내 (24/04/29)](https://apidocs.bithumb.com/changelog/%EB%B9%97%EC%8D%B8-api-%EC%8B%A0%EA%B7%9C-%EB%B2%A0%ED%83%80-%EB%B2%84%EC%A0%84-%EC%98%A4%ED%94%88-%EC%95%88%EB%82%B4-240213)

about 1 year agoby bithumb api

안녕하세요.

No.1 가상자산 플랫폼, 빗썸입니다.

# [빗썸 API Docs 업데이트 안내 (24/02/13)](https://apidocs.bithumb.com/changelog/%EB%B9%97%EC%8D%B8-api-docs-%EC%A0%9C%EA%B3%B5-%EC%A0%95%EB%B3%B4-%EA%B4%80%EB%A0%A8-%EC%95%88%EB%82%B4-240123)

about 1 year agoby bithumb api

안녕하세요.

No.1 가상자산 플랫폼, 빗썸입니다.

# [빗썸 API Docs 제공 정보 관련 안내 (24/01/23)](https://apidocs.bithumb.com/changelog/%EB%B9%97%EC%8D%B8-api-docs-%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-%EC%95%88%EB%82%B4-231207)

over 1 year agoby 빗썸 API Docs

안녕하세요.

No.1 가상자산 플랫폼, 빗썸입니다.

# [빗썸 API Docs 업데이트 안내 (23/12/07)](https://apidocs.bithumb.com/changelog/%EB%B9%97%EC%8D%B8-api-docs-%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-%EC%95%88%EB%82%B4-231207-1)

over 1 year agoby 빗썸 API Docs

> 업데이트 일자 : 2023-12-07

# [빗썸 API Docs 업데이트 안내 (23/11/03)](https://apidocs.bithumb.com/changelog/%EB%B9%97%EC%8D%B8-api-docs-%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-%EC%95%88%EB%82%B4-231103)

over 1 year agoby 빗썸 API Docs

> 업데이트 일자 : 2023-11-03

[apidocs_bithumb_com_v2_1_5_reference__EB_A7_88_EC_BC_93_EC_BD_94_EB_93_9C__EC_A1_B0_ED_9A_8C.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EB%A7%88%EC%BC%93%EC%BD%94%EB%93%9C-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 빗썸에서 제공중인 시장 정보 | String |
| korean\_name | 거래 대상 디지털 자산 한글명 | String |
| english\_name | 거래 대상 디지털 자산 영문명 | String |
| market\_warning | 유의 종목 여부<br>`NONE` (해당 사항 없음), `CAUTION`(거래유의)<br>'유의 종목' 지정 여부에 대해 반환하며, '주의 종목' 지정 여부는 [경보제 API](https://apidocs.bithumb.com/v2.1.5/reference/%EA%B2%BD%EB%B3%B4%EC%A0%9C) 를 참고하시기 바랍니다. | String |

isDetails

boolean

Defaults to false

유의종목 필드과 같은 상세 정보 노출 여부(선택 파라미터)

# `` 200      200

json

# `` 400      400

object

error

object

name

integer

Defaults to 0

message

string

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

1const options = {method: 'GET', headers: {accept: 'application/json'}};

2​

3fetch('https://api.bithumb.com/v1/market/all?isDetails=false', options)

4  .then(response => response.json())

5  .then(response => console.log(response))

6  .catch(err => console.error(err));

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com.md]
### 이용안내

- [\[API 2.0\]빗썸 API 이용 안내](https://apidocs.bithumb.com/docs/api-%EC%86%8C%EA%B0%9C)
- [View All…](https://apidocs.bithumb.com/docs)

### 공지사항

- [\[업데이트\] 신규 베타 버전 (V2.1.5) : 주문 및 취소 개선 안내](https://apidocs.bithumb.com/changelog/%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-%EC%8B%A0%EA%B7%9C-%EB%B2%A0%ED%83%80-%EB%B2%84%EC%A0%84-v215-%EC%A3%BC%EB%AC%B8-%EB%B0%8F-%EC%B7%A8%EC%86%8C-%EA%B0%9C%EC%84%A0-%EC%95%88%EB%82%B4)
- [\[업데이트\] API를 통한 주문 관련 자전거래 방지 시스템 도입 안내](https://apidocs.bithumb.com/changelog/%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-api%EB%A5%BC-%ED%86%B5%ED%95%9C-%EC%A3%BC%EB%AC%B8-%EA%B4%80%EB%A0%A8-%EC%9E%90%EC%A0%84%EA%B1%B0%EB%9E%98-%EB%B0%A9%EC%A7%80-%EC%8B%9C%EC%8A%A4%ED%85%9C-%EB%8F%84%EC%9E%85-%EC%95%88%EB%82%B4)
- [\[업데이트\] Public Websocket : Snapshot 기능 지원 안내](https://apidocs.bithumb.com/changelog/%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-public-websocket-snapshot-%EA%B8%B0%EB%8A%A5-%EC%A7%80%EC%9B%90-%EC%95%88%EB%82%B4)
- [\[업데이트\] Private Websocket 오픈 : MyOrder, MyAsset 지원 안내](https://apidocs.bithumb.com/changelog/%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-private-websocket-%EC%98%A4%ED%94%88-myorder-myasset-%EC%A7%80%EC%9B%90-%EC%95%88%EB%82%B4)
- [View All…](https://apidocs.bithumb.com/changelog)

[apidocs_bithumb_com_v2_1_5_reference__EA_B8_B0_EB_B3_B8__EC_A0_95_EB_B3_B4.md]
# 1\. API 정보

- public 타입 : `wss://ws-api.bithumb.com/websocket/v1`
- private 타입 : `wss://ws-api.bithumb.com/websocket/v1/private`

# 2\. 데이터 타입

각 정보는 스냅샷과 실시간 정보로 구분되며, WebSocket으로 각 정보를 요청할 수 있습니다.

요청 방식에 따라 받아볼 수 있는 데이터는 달라질 수 있으며 `스냅샷` 과 `실시간` 둘 다, 또는 하나의 정보만 요청할 수도 있습니다.

- 스냅샷 : 요청 당시의 상태를 의미합니다.
- 실시간 : 요청 정보가 스트림 형태로 지속적으로 전달됩니다.

#### Public 타입

별다른 인증 없이 수신할 수 있는 데이터입니다 (스냅샷, 실시간 정보 제공)

- `ticker`: 현재가
- `trade`: 체결
- `orderbook`: 호가

#### Private 타입

인증을 해야만 수신할 수 있는 데이터 타입입니다.

인증에 대한 자세한 내용은 [요청 방법 및 포맷](https://apidocs.bithumb.com/reference/%EC%9A%94%EC%B2%AD-%ED%8F%AC%EB%A7%B7) 페이지를 확인하시기 바랍니다.

- `myOrder`: 내 주문
- `myAsset`: 내 자산

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EC_9E_85_EA_B8_88__EC_A3_BC_EC_86_8C__EC_83_9D_EC_84_B1__EC_9A_94_EC_B2_AD.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Request Parameters**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%9E%85%EA%B8%88-%EC%A3%BC%EC%86%8C-%EC%83%9D%EC%84%B1-%EC%9A%94%EC%B2%AD\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| currency \* | 화폐를 의미하는 영문 대문자 코드 | String |
| net\_type \* | 입금 네트워크 | String |

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%9E%85%EA%B8%88-%EC%A3%BC%EC%86%8C-%EC%83%9D%EC%84%B1-%EC%9A%94%EC%B2%AD\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| net\_type | 입금 네트워크 | String |
| deposit\_address | 입금 주소 | String |
| secondary\_address | 2차 입금 주소 | String |

currency

string

required

화폐를 의미하는 영문 대문자 코드

net\_type

string

required

입금 네트워크

Authorization

string

required

Authorization token (JWT)

# `` 201      201

object

currency

string

net\_type

string

deposit\_address

string

secondary\_address

string

# `` 400      400

object

error

object

name

string

message

string

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

48
axios.post(apiUrl + '/v1/deposits/generate_coin_address', requestBody, config)

1const jwt = require('jsonwebtoken');

2const { v4: uuidv4 } = require('uuid');

3const crypto = require('crypto');

4const querystring = require('querystring');

5const axios = require('axios')

6​

7const accessKey = '발급받은 API KEY'

8const secretKey = '발급받은 SECRET KEY'

9const apiUrl = 'https:/api.bithumb.com'

10​

11// Set API parameters

12

const requestBody = {

13    currency: 'KLAY',

14    net_type: 'KLAY'

15}

16​

17// Generate access token

18const query = querystring.encode(requestBody)

19const alg = 'SHA512'

20const hash = crypto.createHash(alg)

21const queryHash = hash.update(query, 'utf-8').digest('hex')

22

const payload = {

23    access_key: accessKey,

24    nonce: uuidv4(),

25    timestamp: Date.now(),

26    query_hash: queryHash,

```

Choose an example:

application/json

`` 201 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EC_9D_BCday__EC_BA_94_EB_93_A4.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Request Parameters**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%9D%BCday-%EC%BA%94%EB%93%A4\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 마켓 코드 (ex. KRW-BTC) | String |
| to | 마지막 캔들 시각 (exclusive)<br>- ISO8061 포맷 (yyyy-MM-dd'T'HH:mm:ss'Z' 또는 yyyy-MM-dd HH:mm:ss)<br>- 기준 시간 KST<br>- 비워서 요청시 가장 최근 캔들로 반환됨 | String |
| count | 캔들 개수(최대 200개까지 요청 가능) | Integer |
| convertingPriceUnit | 종가 환산 화폐 단위<br>(생략할 수 있으며 KRW로 입력한 경우 원화 환산 가격으로 반환됨) | String |

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%9D%BCday-%EC%BA%94%EB%93%A4\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 마켓명 | String |
| candle\_date\_time\_utc | 캔들 기준 시각(UTC 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |
| candle\_date\_time\_kst | 캔들 기준 시각(KST 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |
| opening\_price | 시가 | Double |
| high\_price | 고가 | Double |
| low\_price | 저가 | Double |
| trade\_price | 종가 | Double |
| timestamp | 캔들 종료 시각(KST 기준) | Long |
| candle\_acc\_trade\_price | 누적 거래 금액 | Double |
| candle\_acc\_trade\_volume | 누적 거래량 | Double |
| prev\_closing\_price | 전일 종가(UTC 0시 기준) | Double |
| change\_price | 전일 종가 대비 변화 금액 | Double |
| change\_rate | 전일 종가 대비 변화량 | Double |
| converted\_trade\_price | 종가 환산 화폐 단위로 환산된 가격<br>(요청에 `convertingPriceUnit ` 파라미터가 없는 경우 해당 필드는 반환되지 않음) | Double |

`convertingPriceUnit` 파라미터의 경우, 원화 마켓이 아닌 다른 마켓(ex. BTC, ETH)의 일봉 요청시 종가를 명시된 파라미터 값으로 환산해 `converted_trade_price` 필드에 추가하여 반환합니다.

현재는 원화( `KRW`) 로 변환하는 기능만 제공하며 추후 기능을 확장할 수 있습니다.

market

string

required

마켓 코드 (ex. KRW-BTC)

to

string

마지막 캔들 시각 (exclusive). 비워서 요청시 가장 최근 캔들

count

int32

Defaults to 1

캔들 개수(최대 200개까지 요청 가능)

convertingPriceUnit

string

종가 환산 화폐 단위 (생략 가능, KRW로 명시할 시 원화 환산 가격을 반환.)

# `` 200      200

array of objects

object

market

string

candle\_date\_time\_utc

string

candle\_date\_time\_kst

string

opening\_price

integer

Defaults to 0

high\_price

integer

Defaults to 0

low\_price

integer

Defaults to 0

trade\_price

integer

Defaults to 0

timestamp

integer

Defaults to 0

candle\_acc\_trade\_price

number

Defaults to 0

candle\_acc\_trade\_volume

number

Defaults to 0

prev\_closing\_price

integer

Defaults to 0

change\_price

integer

Defaults to 0

change\_rate

number

Defaults to 0

# `` 400      400

object

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

1const options = {method: 'GET', headers: {accept: 'application/json'}};

2​

3fetch('https://api.bithumb.com/v1/candles/days?count=1', options)

4  .then(response => response.json())

5  .then(response => console.log(response))

6  .catch(err => console.error(err));

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_docs_api__EC_A3_BC_EC_9A_94__EC_97_90_EB_9F_AC__EC_BD_94_EB_93_9C.md]
API 문의 게시판 안내 페이지

API 요청값이 유효하지 않거나 처리 중 오류가 발생하는 경우
아래 에러코드 목록을 통해 원인을 확인할 수 있습니다.

에러코드 목록을 통해 문제를 해결하지 못한 경우

API 문의 게시판을 이용 해주세요.


[API 문의 게시판](https://www.bithumb.com/customer_support/question)

## **개요**   [Skip link to [object Object]](https://apidocs.bithumb.com/docs/api-%EC%A3%BC%EC%9A%94-%EC%97%90%EB%9F%AC-%EC%BD%94%EB%93%9C\#%EA%B0%9C%EC%9A%94)

API 요청값이 유효하지 않거나 처리 중 오류가 발생한 경우, HTTP 상태 코드와 함께 다음과 같은 형태의 JSON body가 리턴됩니다.

```rdmd-code lang-undefined theme-light
{
  "error": {
    "message": "&lt;오류에 대한 설명&gt;",
    "name": "&lt;오류 코드&gt;"
  }
}
```

주요 오류 코드는 다음과 같습니다.

## **400 Bad Request**   [Skip link to [object Object]](https://apidocs.bithumb.com/docs/api-%EC%A3%BC%EC%9A%94-%EC%97%90%EB%9F%AC-%EC%BD%94%EB%93%9C\#400-bad-request)

| 코드 | 설명 |
| --- | --- |
| invalid\_parameter | 잘못된 파라미터 입니다. |
| invalid\_price | 주문가격 단위를 잘못 입력하셨습니다. 확인 후 시도해주세요. |
| under\_price\_limit\_ask<br>under\_price\_limit\_bid | 주문가격은 최소 %s 이상으로 주문 가능합니다. |
| invalid\_price\_ask<br>invalid\_price\_bid | 주문가격 단위를 잘못 입력하셨습니다. 확인 후 시도해주세요. |
| bank\_account\_required | 실명확인 입출금 계좌 등록 후 이용가능합니다. |
| two\_factor\_auth\_required | 유효한 인증채널을 입력하세요. |
| currency does not have a valid value | 빗썸에서 지원하지 않는 코인 입니다. |
| cross\_trading | 제출하신 주문은 귀하가 기존에 제출하신 주문과 체결될 수 있어 취소되었습니다. |
| withdraw\_insufficient\_balance | 출금 최대 한도가 초과 되었습니다. |

## **401 Unauthorized**   [Skip link to [object Object]](https://apidocs.bithumb.com/docs/api-%EC%A3%BC%EC%9A%94-%EC%97%90%EB%9F%AC-%EC%BD%94%EB%93%9C\#401-unauthorized)

401 Unauthorized 오류는 대부분 JWT 서명이 올바르게 되지 않았을 때 발생합니다. [인증 헤더 만들기](https://apidocs.bithumb.com/v2.1.0/docs/%EC%9D%B8%EC%A6%9D-%ED%97%A4%EB%8D%94-%EB%A7%8C%EB%93%A4%EA%B8%B0) 문서를 참조하시어 서명이 올바르게 되었는지 확인해주세요.

| 코드 | 설명 |
| --- | --- |
| invalid\_query\_payload | Jwt의 query를 검증하는데 실패하였습니다. |
| jwt\_verification | Jwt 토큰 검증에 실패했습니다. |
| expired\_jwt | Jwt가 만료되었습니다. |
| NotAllowIP | not allowed client IP |
| out\_of\_scope | 권한이 부족합니다. |

## **404 Not Found**   [Skip link to [object Object]](https://apidocs.bithumb.com/docs/api-%EC%A3%BC%EC%9A%94-%EC%97%90%EB%9F%AC-%EC%BD%94%EB%93%9C\#404-not-found)

| 코드 | 설명 |
| --- | --- |
| order\_not\_found | 주문을 찾지 못했습니다. |
| deposit\_not\_found<br>withdraw\_not\_found | 입출금 정보를 찾지 못했습니다. |

Updatedabout 1 month ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5.md]
### 이용안내

- [빗썸 API 이용 안내](https://apidocs.bithumb.com/v2.1.5/docs/api-%EC%86%8C%EA%B0%9C)
- [View All…](https://apidocs.bithumb.com/v2.1.5/docs)

### 공지사항

- [\[업데이트\] 신규 베타 버전 (V2.1.5) : 주문 및 취소 개선 안내](https://apidocs.bithumb.com/v2.1.5/changelog/%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-%EC%8B%A0%EA%B7%9C-%EB%B2%A0%ED%83%80-%EB%B2%84%EC%A0%84-v215-%EC%A3%BC%EB%AC%B8-%EB%B0%8F-%EC%B7%A8%EC%86%8C-%EA%B0%9C%EC%84%A0-%EC%95%88%EB%82%B4)
- [\[업데이트\] API를 통한 주문 관련 자전거래 방지 시스템 도입 안내](https://apidocs.bithumb.com/v2.1.5/changelog/%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-api%EB%A5%BC-%ED%86%B5%ED%95%9C-%EC%A3%BC%EB%AC%B8-%EA%B4%80%EB%A0%A8-%EC%9E%90%EC%A0%84%EA%B1%B0%EB%9E%98-%EB%B0%A9%EC%A7%80-%EC%8B%9C%EC%8A%A4%ED%85%9C-%EB%8F%84%EC%9E%85-%EC%95%88%EB%82%B4)
- [\[업데이트\] Public Websocket : Snapshot 기능 지원 안내](https://apidocs.bithumb.com/v2.1.5/changelog/%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-public-websocket-snapshot-%EA%B8%B0%EB%8A%A5-%EC%A7%80%EC%9B%90-%EC%95%88%EB%82%B4)
- [\[업데이트\] Private Websocket 오픈 : MyOrder, MyAsset 지원 안내](https://apidocs.bithumb.com/v2.1.5/changelog/%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-private-websocket-%EC%98%A4%ED%94%88-myorder-myasset-%EC%A7%80%EC%9B%90-%EC%95%88%EB%82%B4)
- [View All…](https://apidocs.bithumb.com/v2.1.5/changelog)

[apidocs_bithumb_com_v2_1_5_reference__EC_9B_90_ED_99_94__EC_9E_85_EA_B8_88_ED_95_98_EA_B8_B0.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Request Parameters**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%9B%90%ED%99%94-%EC%9E%85%EA%B8%88%ED%95%98%EA%B8%B0\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| amount \* | 입금액 | NumberString |
| two\_factor\_type \* | 2차 인증 수단<br>`- kakao : 카카오 인증` | String |

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%9B%90%ED%99%94-%EC%9E%85%EA%B8%88%ED%95%98%EA%B8%B0\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| type | 입출금 종류 | String |
| uuid | 입금의 고유 아이디 | String |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| txid | 입금의 트랜잭션 아이디 | String |
| state | 입금 상태 | String |
| created\_at | 입금 생성 시간 | DateString |
| done\_at | 입금 완료 시간 | DateString |
| amount | 입금 금액/수량 | NumberString |
| fee | 입금 수수료 | NumberString |
| transaction\_type | 입금 유형<br>`- default : 일반입금` | String |

amount

string

required

출금 원화 수량

two\_factor\_type

string

required

2차 인증 수단 (kakao)

Authorization

string

required

Authorization token (JWT)

# `` 201      201

object

type

string

uuid

string

currency

string

net\_type

string

txid

string

state

string

created\_at

string

done\_at

string

amount

string

fee

string

transaction\_type

string

# `` 400      400

object

error

object

name

string

message

string

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

48
axios.post(apiUrl + '/v1/deposits/krw', requestBody, config)

1const jwt = require('jsonwebtoken');

2const { v4: uuidv4 } = require('uuid');

3const crypto = require('crypto');

4const querystring = require('querystring');

5const axios = require('axios')

6​

7const accessKey = '발급받은 API KEY'

8const secretKey = '발급받은 SECRET KEY'

9const apiUrl = 'https:/api.bithumb.com'

10​

11// Set API parameters

12

const requestBody = {

13    amount: 60000,

14    two_factor_type: 'kakao'

15}

16​

17// Generate access token

18const query = querystring.encode(requestBody)

19const alg = 'SHA512'

20const hash = crypto.createHash(alg)

21const queryHash = hash.update(query, 'utf-8').digest('hex')

22

const payload = {

23    access_key: accessKey,

24    nonce: uuidv4(),

25    timestamp: Date.now(),

26    query_hash: queryHash,

```

Choose an example:

application/json

`` 201 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EC_9B_90_ED_99_94__EC_B6_9C_EA_B8_88__EB_A6_AC_EC_8A_A4_ED_8A_B8__EC_A1_B0_ED_9A_8C.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Request Parameters**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%9B%90%ED%99%94-%EC%B6%9C%EA%B8%88-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| state | 출금 상태<br>`- PROCESSING : 진행중`<br>`- DONE : 완료`<br>`- CANCELED : 취소됨` | String |
| uuids | 출금 UUID의 목록 | Array |
| txids | 출금 TXID의 목록 | Array |
| page | 페이지 수 (default: 1) | Number |
| limit | 개수 제한 (default: 100, max: 100) | Number |
| order\_by | 정렬방식<br>`- asc : 오름차순`<br>`- desc : 내림차순 (default)` | String |

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%9B%90%ED%99%94-%EC%B6%9C%EA%B8%88-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| type | 입출금 종류 | String |
| uuid | 출금의 고유 아이디 | String |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| txid | 출금의 트랜잭션 아이디 | String |
| state | 출금 상태<br>`- PROCESSING : 진행중`<br>`- DONE : 완료`<br>`- CANCELLED : 취소됨` | String |
| created\_at | 출금 생성 시간 | DateString |
| done\_at | 출금 완료 시간 | DateString |
| amount | 출금 금액/수량 | NumberString |
| fee | 출금 수수료 | NumberString |
| transaction\_type | 출금 유형<br>`- default : 일반출금` | String |

state

string

출금 상태

uuids

array of strings

출금 UUID의 목록

uuids
ADD string

txids

array of strings

출금 TXID의 목록

txids
ADD string

page

int32

Defaults to 1

페이지 수

limit

int32

Defaults to 100

개수 제한

order\_by

string

Defaults to desc

정렬방식

Authorization

string

required

Authorization token (JWT)

# `` 200      200

array of objects

object

type

string

uuid

string

currency

string

net\_type

string

txid

string

state

string

created\_at

string

done\_at

string

amount

string

fee

string

transaction\_type

string

# `` 400      400

object

error

object

name

string

message

string

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

48

1const jwt = require('jsonwebtoken');

2const { v4: uuidv4 } = require('uuid');

3const crypto = require('crypto');

4const querystring = require('querystring');

5const axios = require('axios')

6​

7const accessKey = '발급받은 API KEY'

8const secretKey = '발급받은 SECRET KEY'

9const apiUrl = 'https:/api.bithumb.com'

10​

11// Set API parameters

12var query = 'limit=100&page=1&order_by=desc'

13

const uuids = [\
\
14    '12704033', '12812333'\
\
15]

16const uuid_query = uuids.map(uuid => `uuids[]=${uuid}`).join('&')

17query = uuid_query ? query + "&" + uuid_query : query

18​

19// Generate access token

20const alg = 'SHA512'

21const hash = crypto.createHash(alg)

22const queryHash = hash.update(query, 'utf-8').digest('hex')

23

const payload = {

24    access_key: accessKey,

25    nonce: uuidv4(),

26    timestamp: Date.now(),

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EC_B5_9C_EA_B7_BC__EC_B2_B4_EA_B2_B0__EB_82_B4_EC_97_AD.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%B5%9C%EA%B7%BC-%EC%B2%B4%EA%B2%B0-%EB%82%B4%EC%97%AD\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 마켓 구분 코드 | String |
| trade\_date\_utc | 체결 일자(UTC 기준)<br>포맷: `yyyy-MM-dd` | String |
| trade\_time\_utc | 체결 시각(UTC 기준)<br>포맷: `HH:mm:ss` | String |
| timestamp | 체결 타임스탬프 | Long |
| trade\_price | 체결 가격 | Double |
| trade\_volume | 체결량 | Double |
| prev\_closing\_price | 전일 종가(UTC 0시 기준) | Double |
| change\_price | 변화량 | Double |
| ask\_bid | 매도/매수 | String |
| sequential\_id | 체결 번호(Unique) | Long |

- `sequential_id` 필드는 체결의 유일성을 판단하기 위한 근거가 될 수 있으나 체결 순서를 보장하지 않습니다.

market

string

required

마켓 코드 (ex. KRW-BTC)

to

string

마지막 체결 시각. 형식 : `[HHmmss 또는 HH:mm:ss]`. 비워서 요청시 가장 최근 데이터

count

int32

Defaults to 1

체결 개수

cursor

string

페이지네이션 커서 (sequentialId)

daysAgo

int32

최근 체결 날짜 기준 7일 이내의 이전 데이터 조회 가능. 비워서 요청 시 가장 최근 체결 날짜 반환. (범위: 1 ~ 7)

# `` 200      200

array of objects

object

market

string

trade\_date\_utc

string

trade\_time\_utc

string

timestamp

integer

Defaults to 0

trade\_price

integer

Defaults to 0

trade\_volume

number

Defaults to 0

prev\_closing\_price

integer

Defaults to 0

chane\_price

integer

Defaults to 0

ask\_bid

string

# `` 400      400

object

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

1const options = {method: 'GET', headers: {accept: 'application/json'}};

2​

3fetch('https://api.bithumb.com/v1/trades/ticks?count=1', options)

4  .then(response => response.json())

5  .then(response => console.log(response))

6  .catch(err => console.error(err));

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EC_B6_9C_EA_B8_88__EB_A6_AC_EC_8A_A4_ED_8A_B8__EC_A1_B0_ED_9A_8C.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Request Parameters**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%B6%9C%EA%B8%88-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| state | 출금 상태<br>- `PROCESSING : 진행중`<br>- `DONE : 완료`<br>- `CANCELED : 취소됨` | String |
| uuids | 출금 UUID의 목록 | Array |
| txids | 출금 TXID의 목록 | Array |
| page | 페이지 수 (default: 1) | Number |
| limit | 개수 제한 (default: 100, max: 100) | Number |
| order\_by | 정렬방식<br>`- asc : 오름차순`<br>`- desc : 내림차순 (default)` | String |

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%B6%9C%EA%B8%88-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| type | 입출금 종류 | String |
| uuid | 출금의 고유 아이디 | String |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| net\_type | 출금 네트워크 | String |
| txid | 출금의 트랜잭션 아이디 | String |
| state | 출금 상태<br>`- PROCESSING : 진행중`<br>`- DONE : 완료`<br>`- CANCELLED : 취소됨` | String |
| created\_at | 출금 생성 시간 | DateString |
| done\_at | 출금 완료 시간 | DateString |
| amount | 출금 금액/수량 | NumberString |
| fee | 출금 수수료 | NumberString |
| transaction\_type | 출금 유형<br>`- default : 일반출금` | String |

currency

string

화폐를 의미하는 영문 대문자 코드

state

string

출금 상태

uuids

array of strings

출금 UUID의 목록

uuids
ADD string

txids

array of strings

출금 TXID의 목록

txids
ADD string

page

int32

Defaults to 1

페이지 수

limit

int32

Defaults to 100

개수 제한

order\_by

string

Defaults to desc

정렬방식

Authorization

string

required

Authorization token (JWT)

# `` 200      200

array of objects

object

type

string

uuid

string

currency

string

net\_type

string

txid

string

state

string

created\_at

string

done\_at

string

amount

string

fee

string

transaction\_type

string

# `` 400      400

object

error

object

name

string

message

string

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

48

1const jwt = require('jsonwebtoken');

2const { v4: uuidv4 } = require('uuid');

3const crypto = require('crypto');

4const querystring = require('querystring');

5const axios = require('axios')

6​

7const accessKey = '발급받은 API KEY'

8const secretKey = '발급받은 SECRET KEY'

9const apiUrl = 'https:/api.bithumb.com'

10​

11// Set API parameters

12var query = 'currency=XRP&limit=100&page=1&order_by=desc'

13

const uuids = [\
\
14    '200268229', '200268132'\
\
15]

16const uuid_query = uuids.map(uuid => `uuids[]=${uuid}`).join('&')

17query = uuid_query ? query + "&" + uuid_query : query

18​

19// Generate access token

20const alg = 'SHA512'

21const hash = crypto.createHash(alg)

22const queryHash = hash.update(query, 'utf-8').digest('hex')

23

const payload = {

24    access_key: accessKey,

25    nonce: uuidv4(),

26    timestamp: Date.now(),

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EC_A3_BC_EB_AC_B8__EA_B0_80_EB_8A_A5__EC_A0_95_EB_B3_B4.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Request Parameters**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%A3%BC%EB%AC%B8-%EA%B0%80%EB%8A%A5-%EC%A0%95%EB%B3%B4\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market \* | 마켓 ID | String |

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%A3%BC%EB%AC%B8-%EA%B0%80%EB%8A%A5-%EC%A0%95%EB%B3%B4\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| bid\_fee | 매수 수수료 비율 | NumberString |
| ask\_fee | 매도 수수료 비율 | NumberString |
| maker\_bid\_fee | 마켓 매수 수수료 비율 | NumberString |
| maker\_ask\_fee | 마켓 매도 수수료 비율 | NumberString |
| market | 마켓에 대한 정보 | Object |
| market.id | 마켓의 유일 키 | String |
| market.name | 마켓 이름 | String |
| market.order\_types | 지원 주문 방식 | Array\[String\] |
| market.ask\_types | 매도 주문 지원 방식 | Array\[String\] |
| market.bid\_types | 매수 주문 지원 방식 | Array\[String\] |
| market.order\_sides | 지원 주문 종류 | Array\[String\] |
| market.bid | 매수 시 제약사항 | Object |
| market.bid.currency | 화폐를 의미하는 영문 대문자 코드 | String |
| market.bid.price\_unit | 주문금액 단위 | NumberString |
| market.bid.min\_total | 최소 매도/매수 금액 | NumberString |
| market.ask | 매도 시 제약사항 | Object |
| market.ask.currency | 화폐를 의미하는 영문 대문자 코드 | String |
| market.ask.price\_unit | 주문금액 단위 | NumberString |
| market.ask.min\_total | 최소 매도/매수 금액 | NumberString |
| market.max\_total | 최대 매도/매수 금액 | NumberString |
| market.state | 마켓 운영 상태 | String |
| bid\_account | 매수 시 사용하는 화폐의 계좌 상태 | Object |
| bid\_account.currency | 화폐를 의미하는 영문 대문자 코드 | String |
| bid\_account.balance | 주문가능 금액/수량 | NumberString |
| bid\_account.locked | 주문 중 묶여있는 금액/수량 | NumberString |
| bid\_account.avg\_buy\_price | 매수평균가 | NumberString |
| bid\_account.avg\_buy\_price\_modified | 매수평균가 수정 여부 | Boolean |
| bid\_account.unit\_currency | 평단가 기준 화폐 | String |
| ask\_account | 매도 시 사용하는 화폐의 계좌 상태 | Object |
| ask\_account.currency | 화폐를 의미하는 영문 대문자 코드 | String |
| ask\_account.balance | 주문가능 금액/수량 | NumberString |
| ask\_account.locked | 주문 중 묶여있는 금액/수량 | NumberString |
| ask\_account.avg\_buy\_price | 매수평균가 | NumberString |
| ask\_account.avg\_buy\_price\_modified | 매수평균가 수정 여부 | Boolean |
| ask\_account.unit\_currency | 평단가 기준 화폐 | String |

market

string

required

Market ID

Authorization

string

required

Authorization token (JWT)

# `` 200      200

object

bid\_fee

string

ask\_fee

string

maker\_bid\_fee

string

maker\_ask\_fee

string

market

object

id

string

name

string

order\_types

array of strings

order\_types

order\_sides

array of strings

order\_sides

bid\_types

array of strings

bid\_types

ask\_types

array of strings

ask\_types

bid

object

bid object

ask

object

ask object

max\_total

string

state

string

bid\_account

object

currency

string

balance

string

locked

string

avg\_buy\_price

string

avg\_buy\_price\_modified

boolean

Defaults to true

unit\_currency

string

ask\_account

object

currency

string

balance

string

locked

string

avg\_buy\_price

string

avg\_buy\_price\_modified

boolean

Defaults to true

unit\_currency

string

# `` 400      400

object

error

object

name

string

message

string

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

43

1const jwt = require('jsonwebtoken');

2const { v4: uuidv4 } = require('uuid');

3const crypto = require('crypto');

4const querystring = require('querystring');

5const axios = require('axios')

6​

7const accessKey = '발급받은 API KEY'

8const secretKey = '발급받은 SECRET KEY'

9const apiUrl = 'https://api.bithumb.com'

10​

11// Set API parameters

12const query = 'market=KRW-BTC'

13​

14// Generate access token

15const alg = 'SHA512'

16const hash = crypto.createHash(alg)

17const queryHash = hash.update(query, 'utf-8').digest('hex')

18

const payload = {

19    access_key: accessKey,

20    nonce: uuidv4(),

21    timestamp: Date.now(),

22    query_hash: queryHash,

23    query_hash_alg: alg

24}

25const jwtToken = jwt.sign(payload, secretKey)

26

const config = {

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__ED_98_B8_EA_B0_80_orderbook.md]
# Request

요청은 크게 `ticket field`, `type field`, `format field` 로 분류되며 하나의 요청에 여러 개의 `type field` 를 명시할 수 있습니다. 자세한 사항은 [요청 방법 및 포맷](https://apidocs.bithumb.com/reference/%EC%9A%94%EC%B2%AD-%ED%8F%AC%EB%A7%B7) 페이지를 확인해주시기 바랍니다.

### Type Field

수신하고 싶은 시세 정보를 나열하는 필드입니다.

`is_only_snapshot`, `is_only_realtime` 필드는 생략 가능하며 모두 생략할 경우 스냅샷과 실시간 데이터 둘 다 수신합니다.

| 필드명 | 타입 | 내용 | 필수 여부 | 기본 값 |
| --- | --- | --- | --- | --- |
| type | String | 데이터 타입<br>- `orderbook`: 호가 | O |  |
| codes | List | 마켓 코드 리스트<br>\- 대문자로 요청해야 합니다. | O |  |
| level | Double | 모아보기 단위 | X | 1 |
| isOnlySanpshot | Boolean | 스냅샷 시세만 제공 | X | false |
| isOnlyRealtime | Boolean | 실시간 시세만 제공 | X | false |

# Response

| 필드명 | 축약형<br>(format<br>:SIMPLE) | 내용 | 타입 | 값 |
| --- | --- | --- | --- | --- |
| type | ty | 타입 | String | `orderbook`: 호가 |
| code | cd | 마켓 코드 (ex. KRW-BTC) | String |  |
| total\_ask\_size | tas | 호가 매도 총 잔량 | Double |  |
| total\_bid\_size | tbs | 호가 매수 총 잔량 | Double |  |
| orderbook\_units | obu | 호가 | List of Objects |  |
| orderbook\_units.ask\_price | obu.ap | 매도 호가 | Double |  |
| orderbook\_units.bid\_price | obu.bp | 매수 호가 | Double |  |
| orderbook\_units.ask\_size | obu.as | 매도 잔량 | Double |  |
| orderbook\_units.bid\_size | obu.bs | 매수 잔량 | Double |  |
| timestamp | tms | 타임스탬프 (millisecond) | Long |  |
| level | lv | 호가 모아보기 단위 (default: 1, 기본 호가단위) | Double | 모아보기 단위 |

# Example

### Request

- `level` 값은 필수가 아니며, 제외될 경우 DEFUALT(1), 기본 호가단위로 내려갑니다.

JSON

```rdmd-code lang-json theme-light

[\
  {\
    "ticket": "test example"\
  },\
  {\
    "type": "orderbook",\
    "codes": [\
      "KRW-BTC",\
      "KRW-ETH.3"\
    ],\
    "level": 10\
  },\
  {\
    "format": "DEFAULT"\
  }\
]
```

종목별로 각기 다른 모아보기 `level` 값을 지정하기 위해서는 아래와 같이 요청할 수 있습니다.

JSON

```rdmd-code lang-json theme-light

[\
    {\
        "ticket": "test example"\
    },\
    {\
        "type": "orderbook",\
        "codes": [\
            "KRW-BTC"\
        ],\
        "level": 1000\
    },\
    {\
        "type": "orderbook",\
        "codes": [\
            "KRW-XRP"\
        ],\
        "level": 1\
    },\
    {\
        "format": "DEFAULT"\
    }\
]
```

### Response

JSON

```rdmd-code lang-json theme-light

{
    "type": "orderbook",
    "code": "KRW-BTC",
    "total_ask_size": 450.3526,
    "total_bid_size": 63.3006,
    "orderbook_units": [\
        {\
            "ask_price": 478800,\
            "bid_price": 478300,\
            "ask_size": 4.3478,\
            "bid_size": 5.6370\
        },\
        {\
            "ask_price": 489700,\
            "bid_price": 477900,\
            "ask_size": 2.3642,\
            "bid_size": 0.9705\
        },\
        {\
            "ask_price": 493100,\
            "bid_price": 471200,\
            "ask_size": 411.8686,\
            "bid_size": 3.9279\
        },\
        {\
            "ask_price": 493300,\
            "bid_price": 471100,\
            "ask_size": 2.0241,\
            "bid_size": 1.4699\
        },\
        {\
            "ask_price": 493700,\
            "bid_price": 471000,\
            "ask_size": 1.7870,\
            "bid_size": 2.2573\
        },\
        {\
            "ask_price": 493800,\
            "bid_price": 470700,\
            "ask_size": 3.9372,\
            "bid_size": 9.7805\
        },\
        {\
            "ask_price": 494900,\
            "bid_price": 470400,\
            "ask_size": 5.7560,\
            "bid_size": 0.8093\
        },\
        {\
            "ask_price": 495300,\
            "bid_price": 470300,\
            "ask_size": 3.6418,\
            "bid_size": 4.6606\
        },\
        {\
            "ask_price": 495700,\
            "bid_price": 470100,\
            "ask_size": 2.9617,\
            "bid_size": 5.4907\
        },\
        {\
            "ask_price": 495800,\
            "bid_price": 469700,\
            "ask_size": 0.2349,\
            "bid_size": 2.3941\
        },\
        {\
            "ask_price": 496100,\
            "bid_price": 469600,\
            "ask_size": 2.6019,\
            "bid_size": 4.5505\
        },\
        {\
            "ask_price": 496800,\
            "bid_price": 469500,\
            "ask_size": 3.4651,\
            "bid_size": 5.4469\
        },\
        {\
            "ask_price": 496900,\
            "bid_price": 469200,\
            "ask_size": 0.8400,\
            "bid_size": 10.1685\
        },\
        {\
            "ask_price": 497400,\
            "bid_price": 469100,\
            "ask_size": 2.1924,\
            "bid_size": 5.1646\
        },\
        {\
            "ask_price": 497900,\
            "bid_price": 469000,\
            "ask_size": 2.3299,\
            "bid_size": 0.5723\
        }\
    ],
    "level": 1,
    "timestamp": 1725930007672,
    "stream_type": "REALTIME"
}
```

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EA_B2_BD_EB_B3_B4_EC_A0_9C.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EA%B2%BD%EB%B3%B4%EC%A0%9C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 빗썸에서 제공중인 시장 정보 | String |
| warning\_type | 경보 유형<br>\- `PRICE_SUDDEN_FLUCTUATION`: 가격 급등락<br>- `TRADING_VOLUME_SUDDEN_FLUCTUATION`: 거래량 급등<br>- `DEPOSIT_AMOUNT_SUDDEN_FLUCTUATION`: 입금량 급등<br>- `PRICE_DIFFERENCE_HIGH`: 가격 차이<br>- `SPECIFIC_ACCOUNT_HIGH_TRANSACTION`: 소수계좌 거래 집중<br>- `EXCHANGE_TRADING_CONCENTRATION`: 거래소 거래 집중 | String |
| end\_date | 가상 자산 경보 종료일시(KST 기준)<br>포맷: `yyyy-MM-dd HH:mm:ss` | String |

# `` 200      200

array of objects

object

market

string

warning\_type

string

end\_date

string

# `` 400      400

object

error

object

name

integer

Defaults to 0

message

string

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

1const options = {method: 'GET', headers: {accept: 'application/json'}};

2​

3fetch('https://api.bithumb.com/v1/market/virtual_asset_warning', options)

4  .then(response => response.json())

5  .then(response => console.log(response))

6  .catch(err => console.error(err));

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EC_A3_BC_EB_AC_B8__EB_A6_AC_EC_8A_A4_ED_8A_B8__EC_A1_B0_ED_9A_8C.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Request Parameters**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%A3%BC%EB%AC%B8-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 마켓 아이디 | String |
| uuids | 주문 UUID의 목록 | Array |
| state | 주문 상태<br>`- wait : 체결 대기 (default)`<br>`- watch : 예약주문 대기`<br>`- done : 전체 체결 완료`<br>`- cancel : 주문 취소` | String |
| states | 주문 상태의 목록<br>- 일반주문( `wait`, `done`, `cancel`)과 자동주문( `watch`)은 혼합하여 조회하실 수 없습니다. | Array |
| page | 페이지 수 (default :1) | Number |
| limit | 개수 제한 (default: 100, limit: 100) | Number |
| order\_by | 정렬방식<br>`- asc : 오름차순`<br>`- desc : 내림차순 (default)` | String |

## **Responses**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%A3%BC%EB%AC%B8-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C\#responses)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| uuid | 주문의 고유 아이디 | String |
| side | 주문 종류 | String |
| ord\_type | 주문 방식 | String |
| price | 주문 당시 화폐 가격 | NumberString |
| state | 주문 상태 | String |
| market | 마켓의 유일키 | String |
| created\_at | 주문 생성 시간 | DateString |
| volume | 사용자가 입력한 주문 양 | NumberString |
| remaining\_volume | 체결 후 남은 주문 양 | NumberString |
| reserved\_fee | 수수료로 예약된 비용 | NumberString |
| remaining\_fee | 남은 수수료 | NumberString |
| paid\_fee | 사용된 수수료 | NumberString |
| locked | 거래에 사용중인 비용 | NumberString |
| executed\_volume | 체결된 양 | NumberString |
| trades\_count | 해당 주문에 걸린 체결 수 | Integer |

market

string

Market ID

state

string

주문 상태

states

array of strings

주문 상태 목록

states
ADD string

uuids

array of strings

주문 UUID의 목록

uuids
ADD string

page

int32

Defaults to 1

페이지 수

limit

int32

Defaults to 100

개수 제한

order\_by

string

Defaults to desc

정렬방식

Authorization

string

required

Authorization token (JWT)

# `` 200      200

array of objects

object

uuid

string

side

string

ord\_type

string

price

string

state

string

market

string

created\_at

string

volume

string

remaining\_volume

string

reserved\_fee

string

remaining\_fee

string

paid\_fee

string

locked

string

executed\_volume

string

trades\_count

integer

Defaults to 0

# `` 400      400

object

error

object

name

string

message

string

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

48

1const jwt = require('jsonwebtoken');

2const { v4: uuidv4 } = require('uuid');

3const crypto = require('crypto');

4const querystring = require('querystring');

5const axios = require('axios')

6​

7const accessKey = '발급받은 API KEY'

8const secretKey = '발급받은 SECRET KEY'

9const apiUrl = 'https:/api.bithumb.com'

10​

11// Set API parameters

12var query = 'market=KRW-XRP&limit=100&page=1&order_by=desc'

13

const uuids = [\
\
14    'C0106000032400700021', 'C0106000043000097801'\
\
15]

16const uuid_query = uuids.map(uuid => `uuids[]=${uuid}`).join('&')

17query = uuid_query ? query + "&" + uuid_query : query

18​

19// Generate access token

20const alg = 'SHA512'

21const hash = crypto.createHash(alg)

22const queryHash = hash.update(query, 'utf-8').digest('hex')

23

const payload = {

24    access_key: accessKey,

25    nonce: uuidv4(),

26    timestamp: Date.now(),

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EB_82_B4__EC_9E_90_EC_82_B0_myasset.md]
# Request

요청은 크게 `ticket field`, `type field`, `format field` 로 분류되며 하나의 요청에 여러 개의 `type field` 를 명시할 수 있습니다. 자세한 사항은 [요청 방법 및 포맷](https://apidocs.bithumb.com/reference/%EC%9A%94%EC%B2%AD-%ED%8F%AC%EB%A7%B7) 페이지를 확인해주시기 바랍니다.

### Type Field

수신하고 싶은 시세 정보를 나열하는 필드입니다.

| 필드명 | 타입 | 내용 | 필수 여부 | 기본 값 |
| --- | --- | --- | --- | --- |
| type | String | 데이터 타입<br>- `myAsset`: 내 자산 | O |  |

# Response

| 필드명 | 축약형<br>(format<br>:SIMPLE) | 내용 | 타입 | 값 |
| --- | --- | --- | --- | --- |
| type | ty | 타입 | String | `myAsset`: 내 자산 |
| assets | ast | 자산 리스트 | List of Objects |  |
| assets.currency | ast.cu | 화폐를 의미하는 영문 대문자 코드 | String |  |
| assets.balance | ast.b | 주문가능 수량 | Double |  |
| assets.locked | ast.l | 주문 중 묶여있는 수량 | Double |  |
| asset\_timestamp | asttms | 자산 타임스탬프 (millisecond) | Long |  |
| timestamp | tms | 타임스탬프 (millisecond) | Long |  |
| stream\_type | st | 스트림 타입 | String | `REALTIME` : 실시간 |

# Example

### Request

- 모든 마켓 정보 수신

JSON

```rdmd-code lang-json theme-light

[\
  {\
    "ticket": "test example"\
  },\
  {\
    "type": "myAsset"\
  }\
]
```

### Response

JSON

```rdmd-code lang-json theme-light

{
    "type": "myAsset",
    "assets": [\
        {\
            "currency": "KRW",\
            "balance": "2061832.35",\
            "locked": "3824127.3"\
        }\
    ],
    "asset_timestamp": 1727052537592,
    "timestamp": 1727052537687,
    "stream_type": "REALTIME"
}
{
    "type": "myAsset",
    "assets": [\
        {\
            "currency": "BTC",\
            "balance": "156.70564833",\
            "locked": "38.81945789"\
        }\
    ],
    "asset_timestamp": 1727052537592,
    "timestamp": 1727052537690,
    "stream_type": "REALTIME"
}
```

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_docs_api__EC_9A_94_EC_B2_AD__EC_88_98__EC_A0_9C_ED_95_9C__EC_95_88_EB_82_B4.md]
API 요청 수 제한 안내 페이지

안정적인 Open API 서비스 제공을 위해 API별 요청 수를 제한합니다.

API 이용에 참고하여 주세요.


마지막 업데이트 : 2024.07.23

## Public / Private API 요청 수 제한 안내

- Public API


  - 1초당 150회 요청 가능합니다.
  - 초과 요청을 하시는 경우 API 사용이 일시적으로 제한됩니다.
- Private API


  - 1초당 140회 요청 가능합니다
  - 초과 요청을 하시는 경우 API 사용이 제한될 수 있으니 주의하여 주시기 바랍니다.

## 유의사항

- ※ 사용자 급증 등 과도한 트래픽이 발생할 경우 안정적인 서비스 제공을 위해 API 요청량을 별도의 공지 없이 제한 또는 하향 조정
할 수 있습니다.

- ※ 초과 요청으로 API사용이 제한된 후 자동으로 제한 해제처리가 되지 않는 경우, 고객센터(1661-5566)로 문의하여 주시기 바랍니다.


Updatedabout 2 months ago

* * *

[apidocs_bithumb_com_v2_1_5_reference__EC_B2_B4_EA_B2_B0_trade.md]
# Request

요청은 크게 `ticket field`, `type field`, `format field` 로 분류되며 하나의 요청에 여러 개의 `type field` 를 명시할 수 있습니다. 자세한 사항은 [요청 방법 및 포맷](https://apidocs.bithumb.com/reference/%EC%9A%94%EC%B2%AD-%ED%8F%AC%EB%A7%B7) 페이지를 확인해주시기 바랍니다.

### Type Field

수신하고 싶은 시세 정보를 나열하는 필드입니다.

`is_only_snapshot`, `is_only_realtime` 필드는 생략 가능하며 모두 생략할 경우 스냅샷과 실시간 데이터 둘 다 수신합니다.

| 필드명 | 타입 | 내용 | 필수 여부 | 기본 값 |
| --- | --- | --- | --- | --- |
| type | String | 데이터 타입<br>- `trade`: 체결 | O |  |
| codes | List | 마켓 코드 리스트<br>\- 대문자로 요청해야 합니다. | O |  |
| isOnlySanpshot | Boolean | 스냅샷 시세만 제공 | X | false |
| isOnlyRealtime | Boolean | 실시간 시세만 제공 | X | false |

# Response

| 필드명 | 축약형<br>(format<br>:SIMPLE) | 내용 | 타입 | 값 |
| --- | --- | --- | --- | --- |
| type | ty | 타입 | String | `trade`: 체결 |
| code | cd | 마켓 코드 (ex. KRW-BTC) | String |  |
| trade\_price | tp | 체결 가격 | Double |  |
| trade\_volume | tv | 체결량 | Double |  |
| ask\_bid | ab | 매수/매도 구분 | String | `ASK` : 매도<br>`BID` : 매수 |
| prev\_closing\_price | pcp | 전일 종가 | Double |  |
| change | c | 전일 대비 | String | `RISE`: 상승<br>`EVEN`: 보합<br>`FALL`: 하락 |
| change\_price | cp | 부호 없는 전일 대비 값 | Double |  |
| trade\_date | tdt | 최근 거래 일자(KST) | String | yyyy-MM-dd |
| trade\_time | ttm | 최근 거래 시각(KST) | String | HH:mm:ss |
| trade\_timestamp | ttms | 체결 타임스탬프 (milliseconds) | Long |  |
| timestamp | tms | 타임스탬프 (millisecond) | Long |  |
| sequential\_id | sid | 체결 번호 (Unique) | Long |  |
| stream\_type | st | 스트림 타입 | String | `SNAPSHOT` : 스냅샷<br>`REALTIME` : 실시간 |

\* `sequential_id` 필드는 체결의 유일성을 판단하기 위한 근거로 쓰일 수 있습니다. 하지만 체결 순서를 보장하지는 못합니다.

# Example

### Request

- `KRW-BTC`, `KRW-ETH`

JSON

```rdmd-code lang-json theme-light

[\
  {\
    "ticket": "test example"\
  },\
  {\
    "type": "trade",\
    "codes": [\
      "KRW-BTC",\
      "KRW-ETH"\
    ]\
  },\
  {\
    "format": "DEFAULT"\
  }\
]
```

### Response

JSON

```rdmd-code lang-json theme-light

{
    "type": "trade",
    "code": "KRW-BTC",
    "trade_price": 489700,
    "trade_volume": 1.4825,
    "ask_bid": "BID",
    "prev_closing_price": 484500,
    "change": "RISE",
    "change_price": 5200,
    "trade_date": "2024-09-10",
    "trade_time": "09:58:54",
    "trade_timestamp": 1725929934373,
    "sequential_id": 17259299343730000,
    "timestamp": 1725929934483,
    "stream_type": "REALTIME"
}
```

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_docs_api__EC_A3_BC_EC_9A_94__EC_97_90_EB_9F_AC__EC_BD_94_EB_93_9C.md]
API 문의 게시판 안내 페이지

API 요청값이 유효하지 않거나 처리 중 오류가 발생하는 경우
아래 에러코드 목록을 통해 원인을 확인할 수 있습니다.

에러코드 목록을 통해 문제를 해결하지 못한 경우

API 문의 게시판을 이용 해주세요.


[API 문의 게시판](https://www.bithumb.com/customer_support/question)

## **개요**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/docs/api-%EC%A3%BC%EC%9A%94-%EC%97%90%EB%9F%AC-%EC%BD%94%EB%93%9C\#%EA%B0%9C%EC%9A%94)

API 요청값이 유효하지 않거나 처리 중 오류가 발생한 경우, HTTP 상태 코드와 함께 다음과 같은 형태의 JSON body가 리턴됩니다.

```

  "error": {
    "message": "<오류에 대한 설명>",
    "name": "<오류 코드>"
  }

```

주요 오류 코드는 다음과 같습니다.

## **400 Bad Request**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/docs/api-%EC%A3%BC%EC%9A%94-%EC%97%90%EB%9F%AC-%EC%BD%94%EB%93%9C\#400-bad-request)

| 코드 | 설명 |
| --- | --- |
| invalid\_parameter | 잘못된 파라미터 입니다. |
| invalid\_price | 주문가격 단위를 잘못 입력하셨습니다. 확인 후 시도해주세요. |
| under\_price\_limit\_ask<br>under\_price\_limit\_bid | 주문가격은 최소 %s 이상으로 주문 가능합니다. |
| invalid\_price\_ask<br>invalid\_price\_bid | 주문가격 단위를 잘못 입력하셨습니다. 확인 후 시도해주세요. |
| bank\_account\_required | 실명확인 입출금 계좌 등록 후 이용가능합니다. |
| two\_factor\_auth\_required | 유효한 인증채널을 입력하세요. |
| currency does not have a valid value | 빗썸에서 지원하지 않는 코인 입니다. |
| cross\_trading | 제출하신 주문은 귀하가 기존에 제출하신 주문과 체결될 수 있어 취소되었습니다. |
| withdraw\_insufficient\_balance | 출금 최대 한도가 초과 되었습니다. |

## **401 Unauthorized**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/docs/api-%EC%A3%BC%EC%9A%94-%EC%97%90%EB%9F%AC-%EC%BD%94%EB%93%9C\#401-unauthorized)

401 Unauthorized 오류는 대부분 JWT 서명이 올바르게 되지 않았을 때 발생합니다. [인증 헤더 만들기](https://apidocs.bithumb.com/v2.1.0/docs/%EC%9D%B8%EC%A6%9D-%ED%97%A4%EB%8D%94-%EB%A7%8C%EB%93%A4%EA%B8%B0) 문서를 참조하시어 서명이 올바르게 되었는지 확인해주세요.

| 코드 | 설명 |
| --- | --- |
| invalid\_query\_payload | Jwt의 query를 검증하는데 실패하였습니다. |
| jwt\_verification | Jwt 토큰 검증에 실패했습니다. |
| expired\_jwt | Jwt가 만료되었습니다. |
| NotAllowIP | not allowed client IP |
| out\_of\_scope | 권한이 부족합니다. |

## **404 Not Found**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/docs/api-%EC%A3%BC%EC%9A%94-%EC%97%90%EB%9F%AC-%EC%BD%94%EB%93%9C\#404-not-found)

| 코드 | 설명 |
| --- | --- |
| order\_not\_found | 주문을 찾지 못했습니다. |
| deposit\_not\_found<br>withdraw\_not\_found | 입출금 정보를 찾지 못했습니다. |

## **422 UNPROCESSABLE\_ENTITY**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/docs/api-%EC%A3%BC%EC%9A%94-%EC%97%90%EB%9F%AC-%EC%BD%94%EB%93%9C\#422-unprocessable_entity)

| 코드 | 설명 |
| --- | --- |
| order\_not\_ready | 주문 접수 처리 중입니다. 잠시 후 다시 시도해주세요. |

Updatedabout 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EB_82_B4__EC_A3_BC_EB_AC_B8__EB_B0_8F__EC_B2_B4_EA_B2_B0_myorder.md]
# Request

요청은 크게 `ticket field`, `type field`, `format field` 로 분류되며 하나의 요청에 여러 개의 `type field` 를 명시할 수 있습니다. 자세한 사항은 [요청 방법 및 포맷](https://apidocs.bithumb.com/reference/%EC%9A%94%EC%B2%AD-%ED%8F%AC%EB%A7%B7) 페이지를 확인해주시기 바랍니다.

### Type Field

수신하고 싶은 시세 정보를 나열하는 필드입니다.

| 필드명 | 타입 | 내용 | 필수 여부 | 기본 값 |
| --- | --- | --- | --- | --- |
| type | String | 데이터 타입<br>- `myOrder`: 내 주문 | O |  |
| codes | List | 마켓 코드 리스트<br>\- 대문자로 요청해야 합니다. | X | 생략하거나 빈 배열로 요청할 경우 모든 마켓에 대한 정보를 수신합니다. |

# Response

| 필드명 | 축약형<br>(format<br>:SIMPLE) | 내용 | 타입 | 값 |
| --- | --- | --- | --- | --- |
| type | ty | 타입 | String | `myOrder`: 내 주문 |
| code | cd | 마켓 코드 (ex. KRW-BTC) | String |  |
| uuid | uid | 주문 고유 아이디 | String |  |
| ask\_bid | ab | 매수/매도 구분 | String | `ASK`: 매도<br>`BID`: 매수 |
| order\_type | ot | 주문 타입 | String | `limit`: 지정가 주문<br>`price`: 시장가 주문(매수)<br>`market`: 시장가 주문(매도) |
| state | s | 주문 상태 | String | `wait`: 체결 대기<br>`trade`: 체결 발생<br>`done`: 전체 체결 완료<br>`cancel`: 주문 취소 |
| trade\_uuid | tuid | 체결의 고유 아이디 | String |  |
| price | p | 주문 가격,<br>체결 가격 (state: trade 일 때) | Double |  |
| volume | v | 주문량,<br>체결량 (state: trade 일 때) | Double |  |
| remaining\_volume | rv | 체결 후 남은 주문 양 | Double |  |
| executed\_volume | ev | 체결된 양 | Double |  |
| trades\_count | tc | 해당 주문에 걸린 체결 수 | Double |  |
| reserved\_fee | rsf | 수수료로 예약된 비용 | Double |  |
| remaining\_fee | rmf | 남은 수수료 | Double |  |
| paid\_fee | pf | 사용된 수수료 | Double |  |
| executed\_funds | ef | 체결된 금액 | Double |  |
| trade\_timestamp | ttms | 체결 타임스탬프 (millisecond) | Long |  |
| order\_timestamp | otms | 주문 타임스탬프 (millisecond) | Long |  |
| timestamp | tms | 타임스탬프 (millisecond) | Long |  |
| stream\_type | st | 스트림 타입 | String | `REALTIME` : 실시간 |

# Example

### Request

- 모든 마켓 정보 수신

JSON

```rdmd-code lang-json theme-light

[\
  {\
    "ticket": "test example"\
  },\
  {\
    "type": "myOrder",\
    "codes": []\
  }\
]
```

- 특정 마켓 정보 수신

JSON

```rdmd-code lang-json theme-light

[\
  {\
    "ticket": "test example"\
  },\
  {\
    "type": "myOrder",\
    "codes": ["KRW-BTC"]\
  }\
]
```

### Response

JSON

```rdmd-code lang-json theme-light

{
    "type": "myOrder",
    "code": "KRW-BTC",
    "uuid": "C0101000000001818113",
    "ask_bid": "BID",
    "order_type": "limit",
    "state": "trade",
    "trade_uuid": "C0101000000001744207",
    "price": 1927000,
    "volume": 0.4697,
    "remaining_volume": 0.0803,
    "executed_volume": 0.4697,
    "trades_count": 1,
    "reserved_fee": 0,
    "remaining_fee": 0,
    "paid_fee": 0,
    "executed_funds": 905111.9000,
    "trade_timestamp": 1727052318148,
    "order_timestamp": 1727052318074,
    "timestamp": 1727052318369,
    "stream_type": "REALTIME"
}
```

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_docs__EC_9D_B8_EC_A6_9D__ED_97_A4_EB_8D_94__EB_A7_8C_EB_93_A4_EA_B8_B0.md]
## REST API 요청 포맷   [Skip link to REST API 요청 포맷](https://apidocs.bithumb.com/docs/%EC%9D%B8%EC%A6%9D-%ED%97%A4%EB%8D%94-%EB%A7%8C%EB%93%A4%EA%B8%B0\#rest-api-%EC%9A%94%EC%B2%AD-%ED%8F%AC%EB%A7%B7)

REST API는 HTTP를 통해 호출이 이루어집니다.

POST, PUT, DELETE 요청에 body가 존재하는 경우 JSON 형식으로 파라미터를 전송해야 합니다.

유효한 컨텐츠 타입의 예시는 다음과 같으며, 각 프로그래밍 언어 라이브러리에 따라 약간의 차이가 있을 수 있습니다.

```
Content-Type: application/json; charset=utf-8
```

## JWT 인증 토큰 만들기   [Skip link to JWT 인증 토큰 만들기](https://apidocs.bithumb.com/docs/%EC%9D%B8%EC%A6%9D-%ED%97%A4%EB%8D%94-%EB%A7%8C%EB%93%A4%EA%B8%B0\#jwt-%EC%9D%B8%EC%A6%9D-%ED%86%A0%ED%81%B0-%EB%A7%8C%EB%93%A4%EA%B8%B0)

REST API 요청시, 발급받은 `API Key` 와 `Secret Key` 로 토큰을 생성하여 `Authorization` 헤더를 통해 전송합니다. 토큰은 JWT( [https://jwt.io](https://jwt.io/)) 형식을 따릅니다.

서명 방식은 `HS256` 을 권장하며, 서명에 사용할 Secret은 발급받은 `Secret Key` 를 사용합니다.

페이로드의 구성은 다음과 같습니다.

Private API 요청 시 발급받은 `API Key` 와 `Secret Key` 를 이용하여 5개의 파라미터를 헤더에 추가하여 전송합니다.

| 요청 변수 | 설명 | 타입 |
| --- | --- | --- |
| access\_key | 사용자 API Key | String / 필수 |
| nonce | 무작위의 UUID 문자열 | String / 필수 |
| timestamp | 현재의 시간을 밀리초 (millisecond, ms)로 표현한 값<br>(예 : 1655280216476) | Number / 필수 |
| query\_hash | 해싱된 query string (파라미터가 있을 경우 필수) | String / 옵션 |
| query\_hash\_alg | query\_hash를 생성하는 데에 사용한 알고리즘 (기본값 : SHA512) | String / 옵션 |

생성된 인증 헤더의 페이로드 예시입니다.

JSON

```rdmd-code lang-json theme-light

{
  "access_key": "L7rVaYfBIc2BDsnlQGfkR93d6DoOAJCw7mJr5Eso",
  "nonce": "6f5570df-d8bc-4daf-85b4-976733feb624",
  "timestamp": 1712230310689,
  "query_hash": "1c2362ca9d79947582cae192acf63efb8756caa49af1eb64b12ba45617165431a3dd3e47d0476bc2a347b7a1ea512db7f316f56144084b1493166e3c9113a8eb",
  "query_hash_alg": "SHA512"
}
```

### (예시) 파라미터가 없을 경우   [Skip link to (예시) 파라미터가 없을 경우](https://apidocs.bithumb.com/docs/%EC%9D%B8%EC%A6%9D-%ED%97%A4%EB%8D%94-%EB%A7%8C%EB%93%A4%EA%B8%B0\#%EC%98%88%EC%8B%9C-%ED%8C%8C%EB%9D%BC%EB%AF%B8%ED%84%B0%EA%B0%80-%EC%97%86%EC%9D%84-%EA%B2%BD%EC%9A%B0)

NodePythonJava

```rdmd-code lang-javascript theme-light

const jwt = require('jsonwebtoken')
const { v4: uuidv4 } = require('uuid')

const accessKey = '발급받은 API KEY'
const secretKey = '발급받은 SECRET KEY'

const payload = {
    access_key: accessKey,
    nonce: uuidv4(),
    timestamp: Date.now()
};

console.log(payload);

const jwtToken = jwt.sign(payload, secretKey)
const authorizationToken = `Bearer ${jwtToken}`

console.log(authorizationToken);
```

```rdmd-code lang-python theme-light

# Python 3
# pip3 installl pyJwt
import jwt
import uuid
import time

accessKey = "발급받은 API KEY"
secretKey = "발급받은 SECRET KEY"

payload = {
    'access_key': accessKey,
    'nonce': str(uuid.uuid4()),
    'timestamp': round(time.time() * 1000)
}

print(payload, "\n")

jwt_token = jwt.encode(payload, secretKey)
authorization_token = 'Bearer {}'.format(jwt_token)

print(authorization_token)
```

```rdmd-code lang-java theme-light

// https://mvnrepository.com/artifact/com.auth0/java-jwt
import com.auth0.jwt.JWT;
import com.auth0.jwt.algorithms.Algorithm;

import java.util.UUID;

public class OpenAPIAuthSampleNoArgs {

    public static void main(String[] args) {
        String accessKey = "발급받은 API KEY";
        String secretKey = "발급받은 SECRET KEY";

        Algorithm algorithm = Algorithm.HMAC256(secretKey);

        String jwtToken = JWT.create()
                .withClaim("access_key", accessKey)
                .withClaim("nonce", UUID.randomUUID().toString())
                .withClaim("timestamp", System.currentTimeMillis())
                .sign(algorithm);

        String authenticationToken = "Bearer " + jwtToken;

        System.out.println(authenticationToken);
    }
}
```

### (예시) 파라미터가 있는 경우   [Skip link to (예시) 파라미터가 있는 경우](https://apidocs.bithumb.com/docs/%EC%9D%B8%EC%A6%9D-%ED%97%A4%EB%8D%94-%EB%A7%8C%EB%93%A4%EA%B8%B0\#%EC%98%88%EC%8B%9C-%ED%8C%8C%EB%9D%BC%EB%AF%B8%ED%84%B0%EA%B0%80-%EC%9E%88%EB%8A%94-%EA%B2%BD%EC%9A%B0)

HTTP 쿼리 문자열, 혹은 body를 통해 파라미터를 전달하는 경우 모두 JWT 페이로드의 query\_hash 값을 설정해야합니다.

파라미터의 자료형 중 배열이 존재하는 경우, 올바른 query string의 형태는 다음과 같습니다.

`key[]=value1&key[]=value2 ...`

이와 다른 형태로 요청하면 토큰 검증에 실패할 수 있으니 유의하시기 바랍니다.

NodePythonJava

```rdmd-code lang-javascript theme-light

const jwt = require('jsonwebtoken');
const { v4: uuidv4 } = require('uuid');
const crypto = require('crypto');
const querystring = require('querystring');

const accessKey = '발급받은 API KEY'
const secretKey = '발급받은 SECRET KEY'

// GET (query parameters)
// const query = 'string=abc&number=123'
// POST (request body)
const query = querystring.encode({
    string: 'abc',
    number: 123
})

const alg = 'SHA512'
const hash = crypto.createHash(alg)
const queryHash = hash.update(query, 'utf-8').digest('hex')

const payload = {
    access_key: accessKey,
    nonce: uuidv4(),
    timestamp: Date.now(),
    query_hash: queryHash,
    query_hash_alg: alg
};

console.log(payload);

const jwtToken = jwt.sign(payload, secretKey)
const authorizationToken = `Bearer ${jwtToken}`

console.log(authorizationToken);
```

```rdmd-code lang-python theme-light

# Python 3
# pip3 installl pyJwt
import jwt
import uuid
import hashlib
import time
from urllib.parse import urlencode

accessKey = "발급받은 API KEY"
secretKey = "발급받은 SECRET KEY"

# GET (query parameters)
# query = 'string=abc&number=123'.encode()
# POST (request body)
query = urlencode(dict( string="abc", number=123 )).encode()

hash = hashlib.sha512()
hash.update(query)
query_hash = hash.hexdigest()

payload = {
    'access_key': accessKey,
    'nonce': str(uuid.uuid4()),
    'timestamp': round(time.time() * 1000),
    'query_hash': query_hash,
    'query_hash_alg': 'SHA512',
}

print(payload, "\n")

jwt_token = jwt.encode(payload, secretKey)
authorization_token = 'Bearer {}'.format(jwt_token)

print(authorization_token)
```

```rdmd-code lang-java theme-light

// https://mvnrepository.com/artifact/com.auth0/java-jwt
import com.auth0.jwt.JWT;
import com.auth0.jwt.algorithms.Algorithm;
// https://mvnrepository.com/artifact/org.apache.httpcomponents/httpclient
import org.apache.http.NameValuePair;
import org.apache.http.client.utils.URLEncodedUtils;
import org.apache.http.message.BasicNameValuePair;

import java.math.BigInteger;
import java.nio.charset.StandardCharsets;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;
import java.util.ArrayList;
import java.util.List;
import java.util.UUID;

public class OpenAPIAuthSampleArgs {

    public static void main(String[] args) throws NoSuchAlgorithmException {

        String accessKey = "발급받은 API KEY";
        String secretKey = "발급받은 SECRET KEY";

        // GET (query parameters)
				// String query = "string=abc&number=123";
        // POST (request body)
        List<NameValuePair> queryParams = new ArrayList<>();
        queryParams.add(new BasicNameValuePair("string", "abc"));
        queryParams.add(new BasicNameValuePair("number", "123"));
        String query = URLEncodedUtils.format(queryParams, StandardCharsets.UTF_8);

        MessageDigest md = MessageDigest.getInstance("SHA-512");
        md.update(query.getBytes(StandardCharsets.UTF_8));

        String queryHash = String.format("%0128x", new BigInteger(1, md.digest()));

        Algorithm algorithm = Algorithm.HMAC256(secretKey);
        String jwtToken = JWT.create()
                .withClaim("access_key", accessKey)
                .withClaim("nonce", UUID.randomUUID().toString())
                .withClaim("timestamp", System.currentTimeMillis())
                .withClaim("query_hash", queryHash)
                .withClaim("query_hash_alg", "SHA512")
                .sign(algorithm);

        String authenticationToken = "Bearer " + jwtToken;

        System.out.println(authenticationToken);
    }
}
```

Updatedabout 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EB_B6_84minute__EC_BA_94_EB_93_A4_1.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Request Parameters**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EB%B6%84minute-%EC%BA%94%EB%93%A4-1\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 마켓 코드 (ex. KRW-BTC) | String |
| to | 마지막 캔들 시각 (exclusive).<br>ISO8061 포맷 (yyyy-MM-dd'T'HH:mm:ss'Z' or yyyy-MM-dd HH:mm:ss). 기본적으로 KST 기준 시간이며 비워서 요청시 가장 최근 캔들 | String |
| count | 캔들 개수(최대 200개까지 요청 가능) | Integer |

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EB%B6%84minute-%EC%BA%94%EB%93%A4-1\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 마켓명 | String |
| candle\_date\_time\_utc | 캔들 기준 시각(UTC 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |
| candle\_date\_time\_kst | 캔들 기준 시각(KST 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |
| opening\_price | 시가 | Double |
| high\_price | 고가 | Double |
| low\_price | 저가 | Double |
| trade\_price | 종가 | Double |
| timestamp | 캔들 종료 시각(KST 기준) | Long |
| candle\_acc\_trade\_price | 누적 거래 금액 | Double |
| candle\_acc\_trade\_volume | 누적 거래량 | Double |
| unit | 분 단위(유닛) | Integer |

unit

int32

required

Defaults to 1

분 단위. 가능한 값 : 1, 3, 5, 10, 15, 30, 60, 240

market

string

required

Defaults to KRW-BTC

마켓 코드 (ex. KRW-BTC)

to

string

마지막 캔들 시각 (exclusive). 비워서 요청시 가장 최근 캔들

count

int32

Defaults to 1

캔들 개수(최대 200개까지 요청 가능)

# `` 200      200

array of objects

object

market

string

candle\_date\_time\_utc

string

candle\_date\_time\_kst

string

opening\_price

integer

Defaults to 0

high\_price

integer

Defaults to 0

low\_price

integer

Defaults to 0

trade\_price

integer

Defaults to 0

timestamp

integer

Defaults to 0

candle\_acc\_trade\_price

number

Defaults to 0

candle\_acc\_trade\_volume

number

Defaults to 0

unit

integer

Defaults to 0

# `` 400      400

object

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

1const options = {method: 'GET', headers: {accept: 'application/json'}};

2​

3fetch('https://api.bithumb.com/v1/candles/minutes/1?market=KRW-BTC&count=1', options)

4  .then(response => response.json())

5  .then(response => console.log(response))

6  .catch(err => console.error(err));

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EA_B0_9C_EB_B3_84__EC_9E_85_EA_B8_88__EC_A1_B0_ED_9A_8C.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Request Parameters**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EA%B0%9C%EB%B3%84-%EC%9E%85%EA%B8%88-%EC%A1%B0%ED%9A%8C\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| currency \* | 화폐를 의미하는 영문 대문자 코드 | String |
| uuid | 입금 UUID | String |
| txid | 입금 TXID | String |

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EA%B0%9C%EB%B3%84-%EC%9E%85%EA%B8%88-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| type | 입출금 종류 | String |
| uuid | 입금에 대한 고유 아이디 | String |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| net\_type | 입금 네트워크 | String |
| txid | 입금의 트랜잭션 아이디 | String |
| state | 입금 상태 | String |
| created\_at | 입금 생성 시간 | DateString |
| done\_at | 입금 완료 시간 | DateString |
| amount | 입금 수량 | NumberString |
| fee | 입금 수수료 | NumberString |
| transaction\_type | 입금 유형<br>`- default : 일반입금` | String |

currency

string

required

화폐를 의미하는 영문 대문자 코드

uuid

string

개별 입금의 UUID

txid

string

개별 입금의 TXID

Authorization

string

required

Authorization token (JWT)

# `` 200      200

object

type

string

uuid

string

currency

string

net\_type

string

txid

string

state

string

created\_at

string

done\_at

string

amount

string

fee

string

transaction\_type

string

# `` 400      400

object

error

object

name

string

message

string

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

43

1const jwt = require('jsonwebtoken');

2const { v4: uuidv4 } = require('uuid');

3const crypto = require('crypto');

4const querystring = require('querystring');

5const axios = require('axios')

6​

7const accessKey = '발급받은 API KEY'

8const secretKey = '발급받은 SECRET KEY'

9const apiUrl = 'https://api.bithumb.com'

10​

11// Set API parameters

12const query = 'currency=BTC'

13​

14// Generate access token

15const alg = 'SHA512'

16const hash = crypto.createHash(alg)

17const queryHash = hash.update(query, 'utf-8').digest('hex')

18

const payload = {

19    access_key: accessKey,

20    nonce: uuidv4(),

21    timestamp: Date.now(),

22    query_hash: queryHash,

23    query_hash_alg: alg

24}

25const jwtToken = jwt.sign(payload, secretKey)

26

const config = {

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_changelog.md]
# [\[업데이트\] 신규 베타 버전 (V2.1.5) : 주문 및 취소 개선 안내](https://apidocs.bithumb.com/v2.1.5/changelog/%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-%EC%8B%A0%EA%B7%9C-%EB%B2%A0%ED%83%80-%EB%B2%84%EC%A0%84-v215-%EC%A3%BC%EB%AC%B8-%EB%B0%8F-%EC%B7%A8%EC%86%8C-%EA%B0%9C%EC%84%A0-%EC%95%88%EB%82%B4)

about 1 month agoby bithumb api

안녕하세요.

대한민국 대표 거래소 빗썸입니다.

# [\[업데이트\] API를 통한 주문 관련 자전거래 방지 시스템 도입 안내](https://apidocs.bithumb.com/v2.1.5/changelog/%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-api%EB%A5%BC-%ED%86%B5%ED%95%9C-%EC%A3%BC%EB%AC%B8-%EA%B4%80%EB%A0%A8-%EC%9E%90%EC%A0%84%EA%B1%B0%EB%9E%98-%EB%B0%A9%EC%A7%80-%EC%8B%9C%EC%8A%A4%ED%85%9C-%EB%8F%84%EC%9E%85-%EC%95%88%EB%82%B4)

6 months agoby bithumb api

안녕하세요.

# [\[업데이트\] Public Websocket : Snapshot 기능 지원 안내](https://apidocs.bithumb.com/v2.1.5/changelog/%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-public-websocket-snapshot-%EA%B8%B0%EB%8A%A5-%EC%A7%80%EC%9B%90-%EC%95%88%EB%82%B4)

7 months agoby bithumb api

안녕하세요.

# [\[업데이트\] Private Websocket 오픈 : MyOrder, MyAsset 지원 안내](https://apidocs.bithumb.com/v2.1.5/changelog/%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-private-websocket-%EC%98%A4%ED%94%88-myorder-myasset-%EC%A7%80%EC%9B%90-%EC%95%88%EB%82%B4)

7 months agoby bithumb api

안녕하세요.

# [빗썸 API Docs 업데이트 안내 (24/09/12)](https://apidocs.bithumb.com/v2.1.5/changelog/%EB%B9%97%EC%8D%B8-api-docs-%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-%EC%95%88%EB%82%B4-240912)

8 months agoby bithumb api

안녕하세요.

No.1 가상자산 플랫폼, 빗썸입니다.

# [빗썸 API 신규 베타 버전 오픈 안내 (24/04/29)](https://apidocs.bithumb.com/v2.1.5/changelog/%EB%B9%97%EC%8D%B8-api-%EC%8B%A0%EA%B7%9C-%EB%B2%A0%ED%83%80-%EB%B2%84%EC%A0%84-%EC%98%A4%ED%94%88-%EC%95%88%EB%82%B4-240213)

about 1 year agoby bithumb api

안녕하세요.

No.1 가상자산 플랫폼, 빗썸입니다.

# [빗썸 API Docs 업데이트 안내 (24/02/13)](https://apidocs.bithumb.com/v2.1.5/changelog/%EB%B9%97%EC%8D%B8-api-docs-%EC%A0%9C%EA%B3%B5-%EC%A0%95%EB%B3%B4-%EA%B4%80%EB%A0%A8-%EC%95%88%EB%82%B4-240123)

about 1 year agoby bithumb api

안녕하세요.

No.1 가상자산 플랫폼, 빗썸입니다.

# [빗썸 API Docs 제공 정보 관련 안내 (24/01/23)](https://apidocs.bithumb.com/v2.1.5/changelog/%EB%B9%97%EC%8D%B8-api-docs-%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-%EC%95%88%EB%82%B4-231207)

over 1 year agoby 빗썸 API Docs

안녕하세요.

No.1 가상자산 플랫폼, 빗썸입니다.

# [빗썸 API Docs 업데이트 안내 (23/12/07)](https://apidocs.bithumb.com/v2.1.5/changelog/%EB%B9%97%EC%8D%B8-api-docs-%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-%EC%95%88%EB%82%B4-231207-1)

over 1 year agoby 빗썸 API Docs

> 업데이트 일자 : 2023-12-07

# [빗썸 API Docs 업데이트 안내 (23/11/03)](https://apidocs.bithumb.com/v2.1.5/changelog/%EB%B9%97%EC%8D%B8-api-docs-%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-%EC%95%88%EB%82%B4-231103)

over 1 year agoby 빗썸 API Docs

> 업데이트 일자 : 2023-11-03

[apidocs_bithumb_com_v2_1_5_reference__ED_98_84_EC_9E_AC_EA_B0_80_ticker.md]
# Request

요청은 크게 `ticket field`, `type field`, `format field` 로 분류되며 하나의 요청에 여러 개의 `type field` 를 명시할 수 있습니다. 자세한 사항은 [요청 방법 및 포맷](https://apidocs.bithumb.com/reference/%EC%9A%94%EC%B2%AD-%ED%8F%AC%EB%A7%B7) 페이지를 확인해주시기 바랍니다.

### Type Field

수신하고 싶은 시세 정보를 나열하는 필드입니다.

`is_only_snapshot`, `is_only_realtime` 필드는 생략할 수 있으며 둘 다 생략할 경우 스냅샷과 실시간 데이터 모두 수신합니다.

| 필드명 | 타입 | 내용 | 필수 여부 | 기본 값 |
| --- | --- | --- | --- | --- |
| type | String | 데이터 타입<br>- `ticker`: 현재가 | O |  |
| codes | List | 마켓 코드 리스트<br>\- 대문자로 요청해야 합니다. | O |  |
| isOnlySanpshot | Boolean | 스냅샷 시세만 제공 | X | false |
| isOnlyRealtime | Boolean | 실시간 시세만 제공 | X | false |

# Response

| 필드명 | 축약형<br>(format<br>:SIMPLE) | 내용 | 타입 | 값 |
| --- | --- | --- | --- | --- |
| type | ty | 타입 | String | `ticker`: 현재가 |
| code | cd | 마켓 코드 (ex. KRW-BTC) | String |  |
| opening\_price | op | 시가 | Double |  |
| high\_price | hp | 저가 | Double |  |
| low\_price | lp | 고가 | Double |  |
| trade\_price | tp | 현재가 | Double |  |
| prev\_closing\_price | pcp | 전일 종가 | Double |  |
| change | c | 전일 대비 | String | `RISE`: 상승<br>`EVEN`: 보합<br>`FALL`: 하락 |
| change\_price | cp | 부호 없는 전일 대비 값 | Double |  |
| signed\_change\_price | scp | 전일 대비 값 | Double |  |
| change\_rate | cr | 부호 없는 전일 대비 등락율 | Double |  |
| signed\_change\_rate | scr | 전일 대비 등락율 | Double |  |
| trade\_volume | tv | 가장 최근 거래량 | Double |  |
| acc\_trade\_volume | atv | 누적 거래량(KST 0시 기준) | Double |  |
| acc\_trade\_volume\_24h | atv24h | 24시간 누적 거래량 | Double |  |
| acc\_trade\_price | atp | 누적 거래대금(KST 0시 기준) | Double |  |
| acc\_trade\_price\_24h | atp24h | 24시간 누적 거래대금 | Double |  |
| trade\_date | tdt | 최근 거래 일자(KST) | String | yyyyMMdd |
| trade\_time | ttm | 최근 거래 시각(KST) | String | HHmmss |
| trade\_timestamp | ttms | 체결 타임스탬프 (milliseconds) | Long |  |
| ask\_bid | ab | 매수/매도 구분 | String | `ASK` : 매도<br>`BID` : 매수 |
| acc\_ask\_volume | aav | 누적 매도량 | Double |  |
| acc\_bid\_volume | abv | 누적 매수량 | Double |  |
| highest\_52\_week\_price | h52wp | 52주 최고가 | Double |  |
| highest\_52\_week\_date | h52wdt | 52주 최고가 달성일 | String | yyyy-MM-dd |
| lowest\_52\_week\_price | l52wp | 52주 최저가 | Double |  |
| lowest\_52\_week\_date | l52wdt | 52주 최저가 달성일 | String | yyyy-MM-dd |
| market\_state | ms | 거래상태 | String |  |
| is\_trading\_suspended | its | 거래 정지 여부 | Boolean |  |
| delisting\_date | dd | 거래지원 종료일 | Date |  |
| market\_warning | mw | 유의 종목 여부 | String | `NONE` : 해당없음<br>`CAUTION` : 거래유의 |
| timestamp | tms | 타임스탬프 (millisecond) | Long |  |
| stream\_type | st | 스트림 타입 | String | `SNAPSHOT` : 스냅샷<br>`REALTIME` : 실시간 |

# Example

### Request

- `KRW-BTC`, `KRW-ETH`

JSON

```rdmd-code lang-json theme-light

[\
  {\
    "ticket": "test example"\
  },\
  {\
    "type": "ticker",\
    "codes": [\
      "KRW-BTC",\
      "KRW-ETH"\
    ]\
  },\
  {\
    "format": "DEFAULT"\
  }\
]
```

### Response

JSON

```rdmd-code lang-json theme-light

{
    "type": "ticker",
    "code": "KRW-BTC",
    "opening_price": 484500,
    "high_price": 493100,
    "low_price": 472500,
    "trade_price": 493100,
    "prev_closing_price": 484500,
    "change": "RISE",
    "change_price": 8600,
    "signed_change_price": 8600,
    "change_rate": 0.01775026,
    "signed_change_rate": 0.01775026,
    "trade_volume": 1.2567,
    "acc_trade_volume": 225.622,
    "acc_trade_volume_24h": 13386.15417512,
    "acc_trade_price": 108663718.238256,
    "acc_trade_price_24h": 8230696760.346009,
    "trade_date": "20240910",
    "trade_time": "091617",
    "trade_timestamp": 1725927377820,
    "ask_bid": "BID",
    "acc_ask_volume": 106.7561,
    "acc_bid_volume": 118.8659,
    "highest_52_week_price": 999999000,
    "highest_52_week_date": "2024-06-18",
    "lowest_52_week_price": 1000,
    "lowest_52_week_date": "2024-06-18",
    "market_state": "ACTIVE",
    "is_trading_suspended": false,
    "delisting_date": null,
    "market_warning": "NONE",
    "timestamp": 1725927377931,
    "stream_type": "REALTIME"
}
```

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EB_94_94_EC_A7_80_ED_84_B8__EC_9E_90_EC_82_B0__EC_B6_9C_EA_B8_88_ED_95_98_EA_B8_B0.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Request Parameters**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EB%94%94%EC%A7%80%ED%84%B8-%EC%9E%90%EC%82%B0-%EC%B6%9C%EA%B8%88%ED%95%98%EA%B8%B0\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| currency \* | 화폐를 의미하는 영문 대문자 코드 | String |
| net\_type \* | 출금 네트워크 | String |
| amount \* | 출금 수량 | Number |
| address \* | 출금 가능 주소에 등록된 출금 주소 | String |
| secondary\_address | 2차 출금 주소 (필요한 디지털 자산에 한해서) | String |
| exchange\_name | 출금 거래소명(영문) | String |
| receiver\_type | 수취인 개인/법인 여부<br>`- personal: 개인`<br>`- corporation: 법인` | String |
| receiver\_ko\_name | 수취인 국문명(개인 : 개인 국문명, 법인 : 법인 대표자 국문명) | String |
| receiver\_en\_name | 수취인 영문명(개인 : 개인 영문명, 법인 : 법인 대표자 영문명) | String |
| receiver\_corp\_ko\_name | 법인 국문명(수취인 법인인 경우 필수) | String |
| receiver\_corp\_en\_name | 법인 영문명(수취인 법인인 경우 필수) | String |

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EB%94%94%EC%A7%80%ED%84%B8-%EC%9E%90%EC%82%B0-%EC%B6%9C%EA%B8%88%ED%95%98%EA%B8%B0\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| type | 입출금 종류 | String |
| uuid | 출금의 고유 아이디 | String |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| net\_type | 출금 네트워크 | String |
| txid | 출금의 트랜잭션 아이디 | String |
| state | 출금 상태 | String |
| created\_at | 출금 생성 시간 | DateString |
| done\_at | 출금 완료 시간 | DateString |
| amount | 출금 금액/수량 | NumberString |
| fee | 출금 수수료 | NumberString |
| krw\_amount | 원화 환산 가격 | NumberString |
| transaction\_type | 출금유형<br>`- default : 일반출금` | String |

currency

string

required

화폐를 의미하는 영문 대문자 코드

net\_type

string

required

출금 네트워크

amount

string

required

출금 디지털 자산 수량

address

string

required

출금 지갑 주소

secondary\_address

string

2차 출금주소 (필요한 디지털 자산에 한해서)

exchange\_name

string

출금 거래소명(영문)

receiver\_type

string

수취인 개인/법인 여부

receiver\_ko\_name

string

수취인 국문명(개인 : 개인 국문명, 법인 : 법인 대표자 국문명)

receiver\_en\_name

string

수취인 영문명(개인 : 개인 영문명, 법인 : 법인 대표자 영문명)

receiver\_corp\_ko\_name

string

법인 국문명(수취인 법인인 경우 필수)

receiver\_corp\_en\_name

string

법인 영문명(수취인 법인인 경우 필수)

Authorization

string

required

Authorization token (JWT)

# `` 201      201

object

type

string

uuid

string

currency

string

net\_type

string

state

string

created\_at

string

done\_at

string

amount

string

fee

string

krw\_amount

string

transaction\_type

string

txid

string

# `` 400      400

object

error

object

name

string

message

string

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

51
axios.post(apiUrl + '/v1/withdraws/coin', requestBody, config)

1const jwt = require('jsonwebtoken');

2const { v4: uuidv4 } = require('uuid');

3const crypto = require('crypto');

4const querystring = require('querystring');

5const axios = require('axios')

6​

7const accessKey = '발급받은 API KEY'

8const secretKey = '발급받은 SECRET KEY'

9const apiUrl = 'https:/api.bithumb.com'

10​

11// Set API parameters

12

const requestBody = {

13    currency: 'XRP',

14    net_type: 'XRP',

15    amount: 100,

16    address: '출금 주소',

17    secondary_address: '2차 출금 주소'

18}

19​

20// Generate access token

21const query = querystring.encode(requestBody)

22const alg = 'SHA512'

23const hash = crypto.createHash(alg)

24const queryHash = hash.update(query, 'utf-8').digest('hex')

25

const payload = {

26    access_key: accessKey,

```

Choose an example:

application/json

`` 201 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__ED_98_84_EC_9E_AC_EA_B0_80__EC_A0_95_EB_B3_B4.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%ED%98%84%EC%9E%AC%EA%B0%80-%EC%A0%95%EB%B3%B4\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 종목 구분 코드 | String |
| trade\_date | 최근 거래 일자(UTC)<br>포맷: `yyyyMMdd` | String |
| trade\_time | 최근 거래 시각(UTC)<br>포맷: `HHmmss` | String |
| trade\_date\_kst | 최근 거래 일자(KST)<br>포맷: `yyyyMMdd` | String |
| trade\_time\_kst | 최근 거래 시각(KST)<br>포맷: `HHmmss` | String |
| trade\_timestamp | 최근 거래 일시(UTC)<br>포맷: `Unix Timestamp` | Long |
| opening\_price | 시가 | Double |
| high\_price | 고가 | Double |
| low\_price | 저가 | Double |
| trade\_price | 종가(현재가) | Double |
| prev\_closing\_price | 전일 종가(KST 0시 기준) | Double |
| change | EVEN : 보합<br>RISE : 상승<br>FALL : 하락 | String |
| change\_price | 변화액의 절대값 | Double |
| change\_rate | 변화율의 절대값 | Double |
| signed\_change\_price | 부호가 있는 변화액 | Double |
| signed\_change\_rate | 부호가 있는 변화율 | Double |
| trade\_volume | 가장 최근 거래량 | Double |
| acc\_trade\_price | 누적 거래대금(KST 0시 기준) | Double |
| acc\_trade\_price\_24h | 24시간 누적 거래대금 | Double |
| acc\_trade\_volume | 누적 거래량(KST 0시 기준) | Double |
| acc\_trade\_volume\_24h | 24시간 누적 거래량 | Double |
| highest\_52\_week\_price | 52주 신고가 | Double |
| highest\_52\_week\_date | 52주 신고가 달성일<br>포맷: `yyyy-MM-dd` | String |
| lowest\_52\_week\_price | 52주 신저가 | Double |
| lowest\_52\_week\_date | 52주 신저가 달성일<br>포맷: `yyyy-MM-dd` | String |
| timestamp | 타임스탬프 | Long |

\*위 응답의 `change`, `change_price`, `change_rate`, `signed_change_price`, `signed_change_rate ` 필드는 전일종가의 대비 값입니다.

markets

string

required

반점으로 구분되는 마켓 코드 (ex. KRW-BTC, BTC-ETH)

# `` 200      200

array of objects

object

market

string

trade\_date

string

trade\_time

string

trade\_date\_kst

string

trade\_time\_kst

string

trade\_timestamp

integer

Defaults to 0

opening\_price

integer

Defaults to 0

high\_price

integer

Defaults to 0

low\_price

integer

Defaults to 0

trade\_price

integer

Defaults to 0

prev\_closing\_price

integer

Defaults to 0

change

string

change\_price

integer

Defaults to 0

change\_rate

number

Defaults to 0

signed\_change\_price

integer

Defaults to 0

signed\_change\_rate

number

Defaults to 0

trade\_volume

number

Defaults to 0

acc\_trade\_price

number

Defaults to 0

acc\_trade\_price\_24h

number

Defaults to 0

acc\_trade\_volume

number

Defaults to 0

acc\_trade\_volume\_24h

number

Defaults to 0

highest\_52\_week\_price

integer

Defaults to 0

highest\_52\_week\_date

string

lowest\_52\_week\_price

integer

Defaults to 0

lowest\_52\_week\_date

string

timestamp

integer

Defaults to 0

# `` 400      400

object

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

1const options = {method: 'GET', headers: {accept: 'application/json'}};

2​

3fetch('https://api.bithumb.com/v1/ticker', options)

4  .then(response => response.json())

5  .then(response => console.log(response))

6  .catch(err => console.error(err));

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_docs__EC_9E_90_EC_A3_BC__EB_AC_BB_EB_8A_94__EC_A7_88_EB_AC_B8_faq.md]
## 출금 API를 이용하는데 invalid Parameter 에러가 확인됩니다   [Skip link to 출금 API를 이용하는데 invalid Parameter 에러가 확인됩니다](https://apidocs.bithumb.com/docs/%EC%9E%90%EC%A3%BC-%EB%AC%BB%EB%8A%94-%EC%A7%88%EB%AC%B8-faq\#%EC%B6%9C%EA%B8%88-api%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%98%EB%8A%94%EB%8D%B0-invalid-parameter-%EC%97%90%EB%9F%AC%EA%B0%80-%ED%99%95%EC%9D%B8%EB%90%A9%EB%8B%88%EB%8B%A4)

Text

```rdmd-code lang-text theme-light

‘특정 금융거래 정보의 보고 및 이용에 관한 법률’에 따라 2022년 3월 25일부터 빗썸 외 지갑으로 가상자산을 출금하는 경우, 가상자산 송/수신인 정보를 제공할 수 있는 VASP로의 이전만을 허용하게 되었습니다.

출금 API를 통해 빗썸 외 지갑으로 출금을 진행하시는 경우, 아래 항목을 반드시 확인 해주세요.

◾ 개인 지갑으로 출금 시 필수 요청 변수
  - exchange_name : 출금 거래소 영문명
  - receiver_type : 수취인 개인/법인 여부 (개인: 'personal', 법인: 'corporation')
  - ko_name : 개인 수취 정보_국문 성명
  - en_name : 개인 수취 정보_영문 성명

◾ 법인 지갑으로 출금 시 필수 요청 변수
  - exchange_name : 출금 거래소 영문명
  - corp_ko_name : 법인 수취 정보_국문 법인명
  - corp_en_name : 법인 수취 정보_영문 법인명
  - corp_rep_ko_name : 법인 수취 정보_국문 법인 대표자명
  - corp_rep_en_name : 법인 수취 정보_영문 법인 대표자명

invalid Parameter 외에 ‘다시 시도’ 해달라는 에러가 확인되는 경우, 입력하신 수취인 정보와 실제 수취인 정보가 다를 수 있으니 수취인 정보를 재확인 해주시기 바랍니다.
```

## API 호출 시 IP가 차단되었다고 확인됩니다   [Skip link to API 호출 시 IP가 차단되었다고 확인됩니다](https://apidocs.bithumb.com/docs/%EC%9E%90%EC%A3%BC-%EB%AC%BB%EB%8A%94-%EC%A7%88%EB%AC%B8-faq\#api-%ED%98%B8%EC%B6%9C-%EC%8B%9C-ip%EA%B0%80-%EC%B0%A8%EB%8B%A8%EB%90%98%EC%97%88%EB%8B%A4%EA%B3%A0-%ED%99%95%EC%9D%B8%EB%90%A9%EB%8B%88%EB%8B%A4)

Text

```rdmd-code lang-text theme-light

빗썸 Open API는 안정적인 서비스 제공을 위해 API 별 요청 수를 제한합니다.
제한된 요청 수 이상으로 초과 요청하시는 경우 IP가 일시적으로 차단되오니 이용에 주의하시기 바랍니다.

◾ Public API
  - 1초당 최대 150회 요청 가능
  - 초과 요청하는 경우 1분 제한

◾ Private API
  - 1초당 최대 140회 요청 가능
  - 초과 요청하는 경우 Private info : 5분 제한 / Private trade : 10분 제한

제한 시간이 경과하면 차단이 자동 해제되며, 실패 호출도 제한에 포함되오니 참고 부탁드립니다.
```

Updatedabout 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EC_9E_85_EC_B6_9C_EA_B8_88__ED_98_84_ED_99_A9.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%9E%85%EC%B6%9C%EA%B8%88-%ED%98%84%ED%99%A9\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| wallet\_state | 입출금 상태<br>`- working : 입출금 가능`<br>`- withdraw_only : 출금만 가능`<br>`- deposit_only : 입금만 가능`<br>`- paused : 입출금 중단` | String |
| block\_state | 블록 상태<br>`- normal : 정상`<br>`- delayed : 지연`<br>`- inactive : 비활성 (점검 등)` | String |
| block\_height | 블록 높이 | Integer |
| block\_updated\_at | 블록 갱신 시각 | DateString |
| block\_elapsed\_minutes | 블록 정보 최종 갱신 후 경과 시간 (분) | Integer |
| net\_type | 입출금 관련 요청 시 지정해야 할 네트워크 타입 | String |
| network\_name | 입출금 네트워크 이름 | String |

Authorization

string

required

Authorization token (JWT)

# `` 200      200

array of objects

object

currency

string

wallet\_state

string

block\_state

string

block\_height

integer

Defaults to 0

block\_updated\_at

string

block\_elapsed\_minutes

integer

Defaults to 0

net\_type

string

network\_name

string

# `` 400      400

object

error

object

name

string

message

string

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

33

1const jwt = require('jsonwebtoken');

2const { v4: uuidv4 } = require('uuid');

3const axios = require('axios')

4​

5const accessKey = '발급받은 API KEY'

6const secretKey = '발급받은 SECRET KEY'

7const apiUrl = 'https:/api.bithumb.com'

8​

9// Generate access token

10

const payload = {

11    access_key: accessKey,

12    nonce: uuidv4(),

13    timestamp: Date.now()

14};

15const jwtToken = jwt.sign(payload, secretKey)

16

const config = {

17

    headers: {

18        Authorization: `Bearer ${jwtToken}`

19    }

20}

21​

22// Call API

23axios.get(apiUrl + '/v1/status/wallet', config)

24

    .then((response) => {

25        // handle to success

26        console.log('status: ', response.status)

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EC_A0_84_EC_B2_B4__EA_B3_84_EC_A2_8C__EC_A1_B0_ED_9A_8C.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%A0%84%EC%B2%B4-%EA%B3%84%EC%A2%8C-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| balance | 주문가능 금액/수량 | NumberString |
| locked | 주문 중 묶여있는 금액/수량 | NumberString |
| avg\_buy\_price | 매수평균가 | NumberString |
| avg\_buy\_price\_modified | 매수평균가 수정 여부 | Boolean |
| unit\_currency | 평단가 기준 화폐 | String |

Authorization

string

required

Authorization token (JWT)

# `` 200      200

array of objects

object

currency

string

balance

string

locked

string

avg\_buy\_price

string

avg\_buy\_price\_modified

boolean

Defaults to true

unit\_currency

string

# `` 400      400

object

error

object

name

string

message

string

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

33

1const jwt = require('jsonwebtoken');

2const { v4: uuidv4 } = require('uuid');

3const axios = require('axios')

4​

5const accessKey = '발급받은 API KEY'

6const secretKey = '발급받은 SECRET KEY'

7const apiUrl = 'https:/api.bithumb.com'

8​

9// Generate access token

10

const payload = {

11    access_key: accessKey,

12    nonce: uuidv4(),

13    timestamp: Date.now()

14};

15const jwtToken = jwt.sign(payload, secretKey)

16

const config = {

17

    headers: {

18        Authorization: `Bearer ${jwtToken}`

19    }

20}

21​

22// Call API

23axios.get(apiUrl + '/v1/accounts', config)

24

    .then((response) => {

25        // handle to success

26        console.log('status: ', response.status)

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EC_9B_90_ED_99_94__EC_B6_9C_EA_B8_88_ED_95_98_EA_B8_B0.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Request Parameters**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%9B%90%ED%99%94-%EC%B6%9C%EA%B8%88%ED%95%98%EA%B8%B0\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| amount \* | 출금액 | NumberString |
| two\_factor\_type \* | 2차 인증 수단<br>`- kakao : 카카오 인증` | String |

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%9B%90%ED%99%94-%EC%B6%9C%EA%B8%88%ED%95%98%EA%B8%B0\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| type | 입출금 종류 | String |
| uuid | 출금의 고유 아이디 | String |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| txid | 출금의 트랜잭션 아이디 | String |
| state | 출금 상태 | String |
| created\_at | 출금 생성 시간 | DateString |
| done\_at | 출금 완료 시간 | DateString |
| amount | 출금 금액/수량 | NumberString |
| fee | 출금 수수료 | NumberString |
| transaction\_type | 출금유형<br>`- default : 일반출금` | String |

amount

string

required

출금 원화 수량

two\_factor\_type

string

required

2차 인증 수단 (kakao)

Authorization

string

required

Authorization token (JWT)

# `` 201      201

object

type

string

uuid

string

currency

string

net\_type

string

txid

string

state

string

created\_at

string

done\_at

string

amount

string

fee

string

transaction\_type

string

# `` 400      400

object

error

object

name

string

message

string

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

48
axios.post(apiUrl + '/v1/withdraws/krw', requestBody, config)

1const jwt = require('jsonwebtoken');

2const { v4: uuidv4 } = require('uuid');

3const crypto = require('crypto');

4const querystring = require('querystring');

5const axios = require('axios')

6​

7const accessKey = '발급받은 API KEY'

8const secretKey = '발급받은 SECRET KEY'

9const apiUrl = 'https:/api.bithumb.com'

10​

11// Set API parameters

12

const requestBody = {

13    amount: 60000,

14    two_factor_type: 'kakao'

15}

16​

17// Generate access token

18const query = querystring.encode(requestBody)

19const alg = 'SHA512'

20const hash = crypto.createHash(alg)

21const queryHash = hash.update(query, 'utf-8').digest('hex')

22

const payload = {

23    access_key: accessKey,

24    nonce: uuidv4(),

25    timestamp: Date.now(),

26    query_hash: queryHash,

```

Choose an example:

application/json

`` 201 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EC_B6_9C_EA_B8_88__ED_97_88_EC_9A_A9__EC_A3_BC_EC_86_8C__EB_A6_AC_EC_8A_A4_ED_8A_B8__EC_A1_B0_ED_9A_8C.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%B6%9C%EA%B8%88-%ED%97%88%EC%9A%A9-%EC%A3%BC%EC%86%8C-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| net\_type | 출금 네트워크 타입 | String |
| network\_name | 출금 네트워크 이름 | String |
| withdraw\_address | 출금 주소 | String |
| secondary\_address | 2차 출금 주소 (필요한 디지털 자산에 한해서) | String |
| exchange\_name | 출금 거래소명 (영문) | String |
| owner\_type | 주소 소유주 고객 타입<br>`- personal: 개인`<br>`- corporation: 법인` | String |
| owner\_ko\_name | 주소 소유주 국문명 | String |
| owner\_en\_name | 주소 소유주 영문명 | String |
| owner\_corp\_ko\_name | 주소 소유 법인 국문명 | String |
| owner\_corp\_en\_name | 주소 소유 법인 영문명 | String |

Authorization

string

required

Authorization token (JWT)

# `` 200      200

array of objects

object

currency

string

net\_type

string

network\_name

string

withdraw\_address

string

secondary\_address

string

exchange\_name

string

owner\_type

string

owner\_ko\_name

string

owner\_en\_name

string

owner\_corp\_ko\_name

string

owner\_corp\_en\_name

string

# `` 400      400

object

error

object

name

string

message

string

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

33

1const jwt = require('jsonwebtoken');

2const { v4: uuidv4 } = require('uuid');

3const axios = require('axios')

4​

5const accessKey = '발급받은 API KEY'

6const secretKey = '발급받은 SECRET KEY'

7const apiUrl = 'https:/api.bithumb.com'

8​

9// Generate access token

10

const payload = {

11    access_key: accessKey,

12    nonce: uuidv4(),

13    timestamp: Date.now()

14};

15const jwtToken = jwt.sign(payload, secretKey)

16

const config = {

17

    headers: {

18        Authorization: `Bearer ${jwtToken}`

19    }

20}

21​

22// Call API

23axios.get(apiUrl + '/v1/withdraws/coin_addresses', config)

24

    .then((response) => {

25        // handle to success

26        console.log('status: ', response.status)

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EC_9E_85_EA_B8_88__EB_A6_AC_EC_8A_A4_ED_8A_B8__EC_A1_B0_ED_9A_8C.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Request Parameters**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%9E%85%EA%B8%88-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| state | 입금 상태<br>- 입금신청<br>  <br>- 입금대기: `REQUESTED_PENDING`<br>- 반환신청대기: `REQUESTED_SYSTEM_REJECTED`<br>- 입금신청대기: `REQUESTED_PROCESSING`<br>- 입금심사중: `REQUESTED_PROCESSING`<br>- 입금심사반려: `REQUESTED_ADMIN_REJECTED`<br>- 입금<br>  <br>- 입금대기: `DEPOSIT_PROCESSING`<br>- 입금완료: `DEPOSIT_ACCEPTED`<br>- 입금취소: `DEPOSIT_CANCELLED`<br>- 반환신청<br>  <br>- 반환심사대기: `REFUNDING_PENDING`<br>- 반환취소: `REFUNDING_SYSTEM_REJECTED`<br>- 반환심사중: `REFUNDING_PROCESSING`<br>- 반환취소: `REFUNDING_ADMIN_REJECTED`<br>- 반환완료: `REFUNDING_ACCEPTED`<br>- 반환 신청 건 출금<br>  <br>- 반환승인: `REFUNDED_PROCESSING`<br>- 반환완료: `REFUNDED_ACCEPTED`<br>- 반환취소: `REFUNDED_CANCELLED` | String |
| uuids | 입금 UUID의 목록 | Array |
| txids | 입금 TXID의 목록 | Array |
| page | 페이지 수 (default :1) | Number |
| limit | 개수 제한 (default: 100, limit: 100) | Number |
| order\_by | 정렬방식<br>`- asc : 오름차순`<br>`- desc : 내림차순 (default)` | String |

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%9E%85%EA%B8%88-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| type | 입출금 종류 | String |
| uuid | 입금에 대한 고유 아이디 | String |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| net\_type | 입금 네트워크 | String |
| txid | 입금의 트랜잭션 아이디 | String |
| state | 입금 상태<br>- 입금신청<br>  <br>- 입금대기: `REQUESTED_PENDING`<br>- 반환신청대기: `REQUESTED_SYSTEM_REJECTED`<br>- 입금신청대기: `REQUESTED_PROCESSING`<br>- 입금심사중: `REQUESTED_PROCESSING`<br>- 입금심사반려: `REQUESTED_ADMIN_REJECTED`<br>- 입금<br>  <br>- 입금대기: `DEPOSIT_PROCESSING`<br>- 입금완료: `DEPOSIT_ACCEPTED`<br>- 입금취소: `DEPOSIT_CANCELLED`<br>- 반환신청<br>  <br>- 반환심사대기: `REFUNDING_PENDING`<br>- 반환취소: `REFUNDING_SYSTEM_REJECTED`<br>- 반환심사중: `REFUNDING_PROCESSING`<br>- 반환취소: `REFUNDING_ADMIN_REJECTED`<br>- 반환완료: `REFUNDING_ACCEPTED`<br>- 반환 신청 건 출금<br>  <br>- 반환승인: `REFUNDED_PROCESSING`<br>- 반환완료: `REFUNDED_ACCEPTED`<br>- 반환취소: `REFUNDED_CANCELLED` | String |
| created\_at | 입금 생성 시간 | DateString |
| done\_at | 입금 완료 시간 | DateString |
| amount | 입금 수량 | NumberString |
| fee | 입금 수수료 | NumberString |
| transaction\_type | 입금 유형<br>`- default : 일반입금` | String |

currency

string

화폐를 의미하는 영문 대문자 코드

state

string

입금 상태

uuids

array of strings

입금 UUID의 목록

uuids
ADD string

txids

array of strings

입금 TXID의 목록

txids
ADD string

page

int32

Defaults to 1

페이지 수

limit

int32

Defaults to 100

개수 제한

order\_by

string

Defaults to desc

정렬방식

Authorization

string

required

Authorization token (JWT)

# `` 200      200

array of objects

object

type

string

uuid

string

currency

string

net\_type

string

txid

string

state

string

created\_at

string

done\_at

string

amount

string

fee

string

transaction\_type

string

# `` 400      400

object

error

object

name

string

message

string

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

48

1const jwt = require('jsonwebtoken');

2const { v4: uuidv4 } = require('uuid');

3const crypto = require('crypto');

4const querystring = require('querystring');

5const axios = require('axios')

6​

7const accessKey = '발급받은 API KEY'

8const secretKey = '발급받은 SECRET KEY'

9const apiUrl = 'https:/api.bithumb.com'

10​

11// Set API parameters

12var query = 'currency=XRP&limit=100&page=1&order_by=desc'

13

const uuids = [\
\
14    '202603087', '202601491'\
\
15]

16const uuid_query = uuids.map(uuid => `uuids[]=${uuid}`).join('&')

17query = uuid_query ? query + "&" + uuid_query : query

18​

19// Generate access token

20const alg = 'SHA512'

21const hash = crypto.createHash(alg)

22const queryHash = hash.update(query, 'utf-8').digest('hex')

23

const payload = {

24    access_key: accessKey,

25    nonce: uuidv4(),

26    timestamp: Date.now(),

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_docs_api__EC_9A_94_EC_B2_AD__EC_88_98__EC_A0_9C_ED_95_9C__EC_95_88_EB_82_B4.md]
API 요청 수 제한 안내 페이지

안정적인 Open API 서비스 제공을 위해 API별 요청 수를 제한합니다.

API 이용에 참고하여 주세요.


마지막 업데이트 : 2024.07.23

## Public / Private API 요청 수 제한 안내

- Public API


  - 1초당 150회 요청 가능합니다.
  - 초과 요청을 하시는 경우 API 사용이 일시적으로 제한됩니다.
- Private API


  - 1초당 140회 요청 가능합니다
  - 초과 요청을 하시는 경우 API 사용이 제한될 수 있으니 주의하여 주시기 바랍니다.

## 유의사항

- ※ 사용자 급증 등 과도한 트래픽이 발생할 경우 안정적인 서비스 제공을 위해 API 요청량을 별도의 공지 없이 제한 또는 하향 조정
할 수 있습니다.

- ※ 초과 요청으로 API사용이 제한된 후 자동으로 제한 해제처리가 되지 않는 경우, 고객센터(1661-5566)로 문의하여 주시기 바랍니다.


Updatedabout 2 months ago

* * *

Did this page help you?

Yes

No

[apidocs_bithumb_com_v2_1_5_reference__EC_B6_9C_EA_B8_88__EA_B0_80_EB_8A_A5__EC_A0_95_EB_B3_B4.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Request Parameters**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%B6%9C%EA%B8%88-%EA%B0%80%EB%8A%A5-%EC%A0%95%EB%B3%B4\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| currency \* | 화폐를 의미하는 영문 대문자 코드 | String |
| net\_type \* | 출금 네트워크 | String |

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%B6%9C%EA%B8%88-%EA%B0%80%EB%8A%A5-%EC%A0%95%EB%B3%B4\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| member\_level | 사용자의 보안등급 정보 | Object |
| member\_level.security\_level | 사용자의 보안등급 | Integer |
| member\_level.fee\_level | 사용자의 수수료등급 | Integer |
| member\_level.email\_verified | 사용자의 이메일 인증 여부 | Boolean |
| member\_level.identity\_auth\_verified | 사용자의 실명 인증 여부 | Boolean |
| member\_level.bank\_account\_verified | 사용자의 계좌 인증 여부 | Boolean |
| member\_level.two\_factor\_auth\_verified | 2FA 인증 수단의 활성화 여부 | Boolean |
| member\_level.locked | 사용자의 계정 보호 상태 | Boolean |
| member\_level.wallet\_locked | 사용자의 출금 보호 상태 | Boolean |
| currency | 화폐 정보 | Object |
| currency.code | 화폐를 의미하는 영문 대문자 코드 | String |
| currency.withdraw\_fee | 해당 화폐의 출금 수수료 | NumberString |
| currency.is\_coin | 화폐의 디지털 자산 여부 | Boolean |
| currency.wallet\_state | 해당 화폐의 지갑 상태 | String |
| currency.wallet\_support | 해당 화폐가 지원하는 입출금 정보 | Array\[String\] |
| account | 사용자의 계좌 정보 | Object |
| account.currency | 화폐를 의미하는 영문 대문자 코드 | String |
| account.balance | 주문가능 금액/수량 | NumberString |
| account.locked | 주문 중 묶여있는 금액/수량 | NumberString |
| account.avg\_buy\_price | 평균매수가 | NumberString |
| account.avg\_buy\_price\_modified | 평균매수가 수정 여부 | Boolean |
| account.unit\_currency | 평단가 기준 화폐 | String |
| withdraw\_limit | 출금 제약 정보 | Object |
| withdraw\_limit.currency | 화폐를 의미하는 영문 대문자 코드 | String |
| withdraw\_limit.minimum | 출금 최소 금액/수량 | NumberString |
| withdraw\_limit.onetime | 1회 출금 한도 | NumberString |
| withdraw\_limit.daily | 1일 출금 한도 | NumberString |
| withdraw\_limit.remaining\_daily | 1일 잔여 출금 한도 | NumberString |
| withdraw\_limit.fixed | 출금 금액/수량 소수점 자리 수 | Integer |
| withdraw\_limit.can\_withdraw | 출금 지원 여부 | Boolean |
| withdraw\_limit.remaining\_daily\_krw | 통합 1일 잔여 출금 한도 | NumberString |

JavaScriptPythonJava

[apidocs_bithumb_com_v2_1_5_reference__EC_A3_BC_EB_AC_B8__EC_B7_A8_EC_86_8C__EC_A0_91_EC_88_98.md]
> 예시코드는 JavaScript, Python, JAVA에 한해서만 제공합니다.

## **Request Parameters**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%A3%BC%EB%AC%B8-%EC%B7%A8%EC%86%8C-%EC%A0%91%EC%88%98\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| order\_id \* | 취소할 주문의 고유 아이디 (구 uuid) | String |

> ### 🚧  안내사항
>
> - 요청 파라미터의 "주문의 고유 아이디"가 `order_id` 로 변경되었습니다.
> - 주문 접수 처리 중 상태를 확인할 수 있도록 에러 상태 (422)를 추가하였습니다.

## **Response**   [Skip link to [object Object]](https://apidocs.bithumb.com/v2.1.5/reference/%EC%A3%BC%EB%AC%B8-%EC%B7%A8%EC%86%8C-%EC%A0%91%EC%88%98\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| order\_id | 취소한 주문의 고유 아이디 (구 uuid) | String |
| created\_at | 주문 생성 시간 | DateString |

order\_id

string

required

취소할 주문의 고유 아이디 (구 uuid)

Authorization

string

required

Authorization token (JWT)

# `` 200      200

object

uuid

string

created\_at

string

# `` 400      400

object

error

object

name

string

message

string

# `` 404      404

object

error

object

message

string

name

string

# `` 422      422

object

error

object

message

string

name

string

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

JavaScriptPythonJava

```

xxxxxxxxxx

43

1const jwt = require('jsonwebtoken');

2const { v4: uuidv4 } = require('uuid');

3const crypto = require('crypto');

4const querystring = require('querystring');

5const axios = require('axios')

6​

7const accessKey = '발급받은 API KEY'

8const secretKey = '발급받은 SECRET KEY'

9const apiUrl = 'https://api.bithumb.com'

10​

11// Set API parameters

12const query = 'order_id=C0917000000000070001'

13​

14// Generate access token

15const alg = 'SHA512'

16const hash = crypto.createHash(alg)

17const queryHash = hash.update(query, 'utf-8').digest('hex')

18

const payload = {

19    access_key: accessKey,

20    nonce: uuidv4(),

21    timestamp: Date.now(),

22    query_hash: queryHash,

23    query_hash_alg: alg

24}

25const jwtToken = jwt.sign(payload, secretKey)

26

const config = {

```

Choose an example:

application/json

`` 200 - Result`` 400 - Result`` 404 - Result`` 422 - Result

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

