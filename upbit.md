[docs_upbit_com_kr_reference__EC_A3_BC_EB_AC_B8__EB_A6_AC_EC_8A_A4_ED_8A_B8__EC_A1_B0_ED_9A_8C.md]
> ## ❗️  [Deprecated (2024.06~)](https://docs.upbit.com/kr/changelog/new_get_orders)
>
> GET `v1/orders` 를 사용중이실 경우, 용도에 따라 [`v1/orders/uuids`](https://docs.upbit.com/kr/reference/id%EB%A1%9C-%EC%A3%BC%EB%AC%B8-%EC%A1%B0%ED%9A%8C) , [`v1/orders/open`](https://docs.upbit.com/kr/reference/%EB%8C%80%EA%B8%B0-%EC%A3%BC%EB%AC%B8-%EC%A1%B0%ED%9A%8C) , [`v1/orders/closed`](https://docs.upbit.com/kr/reference/%EC%A2%85%EB%A3%8C-%EC%A3%BC%EB%AC%B8-%EC%A1%B0%ED%9A%8C) 로 변경해주시기 바랍니다.
>
> 정확한 지원종료 예정일은 추후 공지사항을 통해 다시 안내드리겠습니다.

## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EC%A3%BC%EB%AC%B8-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C\#request-parameters)

> ## 🚧  states 파라미터 변경 안내 (2021. 03. 22 ~)
>
> 2021년 3월 22일부터 미체결 주문(wait, watch)과 완료 주문(done, cancel)을 혼합하여 조회하실 수 없습니다.
>
> 예시1) done, cancel 주문을 한 번에 조회 => **가능**
>
> 예시2) wait, done 주문을 한 번에 조회 => **불가능** (각각 API 호출 필요)
>
> 자세한 내용은 개발자 센터 공지사항을 참조 부탁드립니다.

| Name | 설명 | 타입 |
| --- | --- | --- |
| market | 마켓 아이디 | String |
| uuids\[\] | 주문 UUID의 목록 | Array |
| identifiers\[\] | 주문 identifier의 목록 | Array |
| state | 주문 상태<br>\- `wait` : 체결 대기 (default)<br>\- `watch` : 예약주문 대기<br>\- `done` : 전체 체결 완료<br>\- `cancel` : 주문 취소<br>\- **주문 리스트 조회 API에서 시장가 주문이 조회되지 않는경우**: 시장가 매수 주문은 체결 후 주문 상태가 `cancel`, `done` 두 경우 모두 발생할 수 있습니다.<br>\- 시장가로 체결이 일어난 후 주문 잔량이 발생하는 경우, 남은 잔량이 반환되며 `cancel` 처리됩니다. 대부분의 경우 소수점 아래 8자리까지 나누어 떨어지지 않는 미미한 금액이 주문 잔량으로 발생하게 됩니다.<br>\- 만일 주문 잔량 없이 딱 맞아떨어지게 체결이 발생한 경우에는 주문 상태가 `done` 이 됩니다. | String |
| states\[\] | 주문 상태의 목록<br>\\* 미체결 주문(wait, watch)과 완료 주문(done, cancel)은 혼합하여 조회하실 수 없습니다.<br>\\* state와 states는 동시에 사용할 수 없습니다. 둘 중 하나만 지정하시기를 바랍니다. | Array |
| page | 페이지 수, default: 1 | Number |
| limit | 요청 개수, default: 100 | Number |
| order\_by | 정렬 방식<br>\- `asc` : 오름차순<br>\- `desc` : 내림차순 (default) | String |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EC%A3%BC%EB%AC%B8-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C\#response)

> ## 📘  신규 주문 타입 및 조건 지원 ( [지원 마켓은 공지참고](https://docs.upbit.com/kr/changelog/new_ord_type))
>
> - 신규 주문 타입이 추가되었습니다: 최유리 지정가 (ord\_type 필드에 `best` 타입 추가)
>
> - 신규 주문 조건이 추가 되었습니다: IOC (Immediate or Cancel), FOK (Fill or Kill)
>   - time\_in\_force 필드가 신규로 추가되며, 가능한 타입은 `ioc` 와 `fok` 입니다.
>
> ![](https://files.readme.io/9912934-image.png)

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
| time\_in\_force | IOC, FOK 설정 | String |

market

string

Market ID

state

string

주문 상태

states\[\]

array of strings

주문 상태 목록

states\[\]
ADD string

uuids\[\]

array of strings

주문 UUID의 목록

uuids\[\]
ADD string

identifiers\[\]

array of strings

주문 identifier의 목록

identifiers\[\]
ADD string

page

int32

Defaults to 1

요청 페이지

limit

int32

Defaults to 100

요청 개수 (1 ~ 100)

order\_by

string

Defaults to desc

정렬

Authorization

string

Authorization token (JWT)

# `` 200      200

json

# `` 4XX      4XX

object

error

object

name

string

message

string

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

53
const uuid_query = uuids.map(uuid => `uuids[]=${uuid}`).join('&')

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const queryEncode = require("querystring").encode

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11const state = 'done'

12

const uuids = [\
\
13    '9ca023a5-851b-4fec-9f0a-48cd83c2eaae',\
\
14    //...\
\
15]

16​

17

const non_array_body = {

18    state: state,

19}

20

const array_body = {

21    uuids: uuids,

22}

23

const body = {

24    ...non_array_body,

25    ...array_body

26}

```

```

xxxxxxxxxx

20



1

[\
\
2\
\
  {\
\
3    "uuid": "9ca023a5-851b-4fec-9f0a-48cd83c2eaae",\
\
4    "side": "ask",\
\
5    "ord_type": "limit",\
\
6    "price": "4280000.0",\
\
7    "state": "done",\
\
8    "market": "KRW-BTC",\
\
9    "created_at": "2019-01-04T13:48:09+09:00",\
\
10    "volume": "1.0",\
\
11    "remaining_volume": "0.0",\
\
12    "reserved_fee": "0.0",\
\
13    "remaining_fee": "0.0",\
\
14    "paid_fee": "2140.0",\
\
15    "locked": "0.0",\
\
16    "executed_volume": "1.0",\
\
17    "trades_count": 1,\
\
18  }\
\
19  # ....\
\
20]

```

Updated 3 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EC_A0_84_EC_B2_B4__EC_9E_85_EA_B8_88__EC_A3_BC_EC_86_8C__EC_A1_B0_ED_9A_8C.md]
## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EC%A0%84%EC%B2%B4-%EC%9E%85%EA%B8%88-%EC%A3%BC%EC%86%8C-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| net\_type | 입금 네트워크 | String |
| deposit\_address | 입금 주소 | String |
| secondary\_address | 2차 입금 주소 | String |

> ## 📘  입금 주소 조회 요청 API 유의사항
>
> 입금 주소 생성 요청 이후 아직 발급되지 않은 상태일 경우 deposit\_address가 null일 수 있습니다.

Authorization

string

required

Authorization token (JWT)

# `` 200      200

array of objects

object

currency

string

deposit\_address

string

secondary\_address

string

# `` 4XX      4XX

object

error

object

name

string

message

string

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

25

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const sign = require('jsonwebtoken').sign

4​

5const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

6const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

7const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

8​

9

const payload = {

10    access_key: access_key,

11    nonce: uuidv4(),

12}

13​

14const token = sign(payload, secret_key)

15​

16

const options = {

17    method: "GET",

18    url: server_url + "/v1/deposits/coin_addresses",

19    headers: {Authorization: `Bearer ${token}`},

20}

21​

22

request(options, (error, response, body) => {

23    if (error) throw new Error(error)

24    console.log(body)

25})

```

```

xxxxxxxxxx

17



1

[\
\
2\
\
  {\
\
3    "currency": "BTC",\
\
4    "deposit_address": "3EusRwybuZUhVDeHL7gh3HSLmbhLcy7NqD",\
\
5    "secondary_address": null\
\
6  },\
\
7\
\
  {\
\
8    "currency": "ETH",\
\
9    "deposit_address": "0x0d73e0a482b8cf568976d2e8688f4a899d29301c",\
\
10    "secondary_address": null\
\
11  },\
\
12\
\
  {\
\
13    "currency": "XRP",\
\
14    "deposit_address": "rN9qNpgnBaZwqCg8CvUZRPqCcPPY7wfWep",\
\
15    "secondary_address": "3057887915"\
\
16  }\
\
17]

```

Updated 3 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EC_9E_85_EC_B6_9C_EA_B8_88__ED_98_84_ED_99_A9.md]
> ## ❗️  입출금 현황 데이터는 실제 서비스 상태와 다를 수 있습니다.
>
> 입출금 현황 API에서 제공하는 입출금 및 블록 상태 정보는 **실제 서비스 상태 보다 수 분 정도 지연되어 반영** 될 수 있으니 오로지 참고용으로 사용하시기를 바라며 **거래 전략의 일부로 사용하지 마시기를 바랍니다.**
>
> 실제 입출금을 수행하기 전에는 반드시 업비트 공지사항 및 입출금 현황 페이지를 참고해 주시기를 바랍니다.

> ## 🚧  네트워크 타입(net\_type) vs. 네트워크 명(network\_name)
>
> - **네트워크 타입( `net_type`)이란?**
>
>
>   디지털 자산 **입출금에 활용되는 블록체인 네트워크** 를 뜻하며, 디지털 자산의 종류에 따라 활용되는 네트워크(체인)가 다를 수 있습니다. **_\*네트워크가 일치하지 않는 경우 정상 입출금이 어려울 수 있으니 사용하는 주소와 네트워크가 정확히 일치하는지 확인해 주세요._**
>
>   **디지털 자산 출금 시 네트워크 타입 (net\_type) 값이 필수입니다.**
> - **네트워크 명( `network_name`)이란?**
>
>
>   업비트에서 지원하고 있는 디지털 자산의 **블록체인 네트워크 이름을 확인** 할 수 있는 기능입니다.
>
>   [업비트 고객센터에서 제공되는 입출금 현황 페이지](https://upbit.com/service_center/wallet_status) 의 '네트워크'와 동일한 값입니다.

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EC%9E%85%EC%B6%9C%EA%B8%88-%ED%98%84%ED%99%A9\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| wallet\_state | 입출금 상태<br>\- `working` : 입출금 가능<br>\- `withdraw_only` : 출금만 가능<br>\- `deposit_only` : 입금만 가능<br>\- `paused` : 입출금 중단<br>\- `unsupported` : 입출금 미지원 | String |
| block\_state | 블록 상태<br>\- `normal` : 정상<br>\- `delayed` : 지연<br>\- `inactive` : 비활성 (점검 등) | String |
| block\_height | 블록 높이 | Integer |
| block\_updated\_at | 블록 갱신 시각 | DateString |
| block\_elapsed\_minutes | 블록 정보 최종 갱신 후 경과 시간 (분) | Integer |
| net\_type | 입출금 관련 요청 시 지정해야 할 네트워크 타입 | String |
| network\_name | 입출금 네트워크 이름 | String |

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

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

25

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const sign = require('jsonwebtoken').sign

4​

5const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

6const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

7const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

8​

9

const payload = {

10    access_key: access_key,

11    nonce: uuidv4(),

12}

13​

14const token = sign(payload, secret_key)

15​

16

const options = {

17    method: "GET",

18    url: server_url + "/v1/status/wallet",

19    headers: {Authorization: `Bearer ${token}`},

20}

21​

22

request(options, (error, response, body) => {

23    if (error) throw new Error(error)

24    console.log(body)

25})

```

```

xxxxxxxxxx

62
]

1

[\
\
2\
\
  {\
\
3    "currency": "KLAY",\
\
4    "wallet_state": "working",\
\
5    "block_state": "normal",\
\
6    "block_height": 7235123,\
\
7    "block_updated_at": "2019-02-18T07:08:50.499+00:00",\
\
8    "block_elapsed_minutes": 2502349,\
\
9    "net_type": "KLAY",\
\
10    "network_name": "Klaytn"\
\
11  },\
\
12\
\
  {\
\
13    "currency": "BTG",\
\
14    "wallet_state": "deposit_only",\
\
15    "block_state": "delayed",\
\
16    "block_height": 556154,\
\
17    "block_updated_at": "2018-11-19T17:00:15.690+00:00",\
\
18    "block_elapsed_minutes": 2632797,\
\
19    "net_type": "BTG",\
\
20    "network_name": "Bitcoin Gold"\
\
21  },\
\
22\
\
  {\
\
23    "currency": "ADD",\
\
24    "wallet_state": "withdraw_only",\
\
25    "block_state": "inactive",\
\
```\
\
Updated 3 months ago\
\
* * *\
\
Did this page help you?\
\
Yes\
\
No\
\
## Open API 이용약관\
\
본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.\
\
제 1조 (목적)\
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.\
\
제 2조 (정의)\
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.\
\
2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.\
\
3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.\
\
제 3조 (면책사항)\
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.\
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.\
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.\
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.\
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.\
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.\
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.\
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.\
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.\
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.\
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.\
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.\
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.\
\
제 4조 (Open API 서비스 제공의 제한 및 해지)\
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.\
1\. 본 이용약관 제6조를 위반한 경우\
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우\
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우\
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우\
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우\
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.\
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.\
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.\
\
제 5조 (저작권)\
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.\
\
제 6조 (사용자의 의무와 책임)\
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.\
1\. API 업데이트 및 변경 사항에 대한 공지\
2\. 제도 변경 공지\
3\. 두나무-업비트 정책 반영에 따른 공지\
4\. 기타 긴급 공지\
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.\
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.\
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.\
\
제 7조 (약관의 변경 등)\
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.\
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).\
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.\
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.\
\
제 8조 (효력 발생 및 유효기간)\
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.\
\
제 9조 (기타)\
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.\
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.\
\
제 10조 (관할법원)\
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.\
\
<부칙>\
본 이용약관은 2024년 10월 30일부터 적용됩니다.\
이전의 이용약관은 아래에서 확인하실 수 있습니다.\
\
\
[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)\
\
[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)\
\
[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)\
\
[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)\
\
동의

[docs_upbit_com_kr_reference__EC_B7_A8_EC_86_8C__ED_9B_84__EC_9E_AC_EC_A3_BC_EB_AC_B8.md]
## Request Parameter   [Skip link to Request Parameter](https://docs.upbit.com/kr/reference/%EC%B7%A8%EC%86%8C-%ED%9B%84-%EC%9E%AC%EC%A3%BC%EB%AC%B8\#request-parameter)

| Name | 설명 | 타입 |
| --- | --- | --- |
| prev\_order\_uuid | 취소할 주문의 UUID | String |
| prev\_order\_identifier | 취소할 주문의 사용자 지정값 | String |
| new\_ord\_type \* | 신규 주문의 주문 타입<br>\- `limit` : 지정가 주문<br>\- `price` : 시장가 주문(매수)<br>\- `market` : 시장가 주문(매도)<br>\- `best` : 최유리 주문 ( `time_in_force` 설정 필수) | String |
| new\_volume \* | 신규 주문량 (지정가, 시장가 매도 시 필수)<br>\- **신규 주문 시 이전 주문의 잔여 수량을 사용하려면 remain\_only 값을 입력해 주시기를 바랍니다.**<br>\- remain\_only 는 **지정가 주문, 지정가 IOC/FOK 주문, 시장가 매도, 최유리 매도 주문** 만 지원합니다. | NumberString or `remain_only` |
| new\_price \* | 주문 가격. (지정가, 시장가 매수 시 필수)<br>ex) KRW-BTC 마켓에서 1BTC당 1,000 KRW로 거래할 경우, 값은 1000<br>ex) KRW-BTC 마켓에서 1BTC당 매도 1호가가 500 KRW 인 경우, 시장가 매수 시 값을 1000으로 세팅하면 2BTC가 매수 됩니다. (단, 수수료와 매도 1호가의 수량에 따라 매수되는 수량은 상이할 수 있습니다) | NumberString |
| new\_identifier | 신규 주문의 조회용 사용자 지정값 (선택) | String (Uniq 값 사용) |
| new\_time\_in\_force | 신규 주문의 IOC, FOK 주문 설정\*<br>\- `ioc` : Immediate or Cancel<br>\- `fok` : Fill or Kill<br>\* **`new_ord_type` 이 `best` 혹은 `limit` 일때만 지원** 됩니다. | String |

\* _필수_

\* _특정 조건에서 필수_

> ## ❗️
>
> 이 API 는 application/json 형식의 Content-Type 만 지원합니다. Query Parameter, Form Data 등 다른 형식의 요청은 지원하지 않으니 유의해주시기 바랍니다.

> ## ❗️
>
> `prev_order_uuid` 혹은 `prev_order_identifier` 둘 중 하나의 값이 반드시 포함되어야 합니다.

> ## ❗️  new\_identifier는 prev\_order\_identifier와 달라야 합니다
>
> identifier는 서비스에서 발급하는 uuid가 아닌 이용자가 직접 발급하는 키값으로, 주문을 조회하기 위해 할당하는 값입니다. 해당 값은 사용자의 전체 주문 내 유일한 값을 전달해야하므로 취소 후 재주문시에도 새로운 값이 필요합니다.
>
> 또한 주문 요청시 오류가 발생하더라도 같은 값으로 다시 요청을 보낼 수 없으니 매 요청시 새로운 값을 생성해주세요.

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EC%B7%A8%EC%86%8C-%ED%9B%84-%EC%9E%AC%EC%A3%BC%EB%AC%B8\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| uuid | 취소할 주문의 고유 아이디 | String |
| side | 취소할 주문의 주문 종류 | String |
| ord\_type | 취소할 주문의 주문 방식 | String |
| price | 취소할 주문의 가격 | NumberString |
| state | 취소할 주문의 주문의 상태 | String |
| market | 취소할 주문 마켓의 유일키 | String |
| created\_at | 취소할 주문의 주문 생성 시간 | String |
| volume | 취소할 주문의 사용자가 입력한 주문 양 | NumberString |
| remaining\_volume | 취소할 주문의 체결 후 남은 주문 양 | NumberString |
| reserved\_fee | 취소할 주문의 수수료로 예약된 비용 | NumberString |
| remaining\_fee | 취소할 주문의 남은 수수료 | NumberString |
| paid\_fee | 취소할 주문의 사용된 수수료 | NumberString |
| locked | 취소할 주문의 거래에 사용중인 비용 | NumberString |
| executed\_volume | 취소할 주문의 체결된 양 | NumberString |
| trades\_count | 취소할 주문의 해당 주문에 걸린 체결 수 | Integer |
| time\_in\_force | 취소할 주문의 IOC, FOK 설정 | String |
| identifier | 취소할 주문의 조회용 사용자 지정값<br>\*identifier 필드는 2024-10-18 이후에 생성된 주문에 대해서만 제공합니다. | String |
| new\_order\_uuid | 주문 성공 시 신규 주문의 UUID | String |
| new\_order\_identifier | 주문 성공 시 신규 주문의 조회용 사용자 지정값 | String |

> ## ❗️  신규 주문
>
> 신규 주문은 취소할 주문과 같은 마켓에 접수되며, 기존 주문( `prev_order_uuid` 또는 `prev_order_identifier` 에 해당하는 주문)이 취소된 후 주문이 접수됩니다.
>
> 신규 주문이 성공적으로 생성되었을 경우, `new_order_uuid` 또는 사용자가 요청 시 지정한 `new_identifier` 로 주문을 조회할 수 있습니다.
>
> 취소 후 신규 주문이 성공적으로 요청되더라도, 기존 주문의 취소 처리가 완료되기 전에 전량체결된 경우 신규 주문은 생성되지 않습니다.

NodePythonRubyJava

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EB_85_84year__EC_BA_94_EB_93_A4.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EB%85%84year-%EC%BA%94%EB%93%A4\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 마켓 코드 (ex. KRW-BTC) | String |
| to | 마지막 캔들 시각 (exclusive).<br>ISO8061 포맷 (yyyy-MM-dd'T'HH:mm:ss'Z' or yyyy-MM-dd HH:mm:ss). 기본적으로 UTC 기준 시간이며 `2023-01-01T00:00:00+09:00` 과 같이 KST 시간으로 요청 가능.<br>비워서 요청시 가장 최근 캔들 | String |
| count | 캔들 개수(최대 200개까지 요청 가능) | Integer |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EB%85%84year-%EC%BA%94%EB%93%A4\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 종목 코드 | String |
| candle\_date\_time\_utc | 캔들 기준 시각(UTC 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |
| candle\_date\_time\_kst | 캔들 기준 시각(KST 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |
| opening\_price | 시가 | Double |
| high\_price | 고가 | Double |
| low\_price | 저가 | Double |
| trade\_price | 종가 | Double |
| timestamp | 마지막 틱이 저장된 시각 | Long |
| candle\_acc\_trade\_price | 누적 거래 금액 | Double |
| candle\_acc\_trade\_volume | 누적 거래량 | Double |
| first\_day\_of\_period | 캔들 기간의 가장 첫 날 | String |

market

string

required

종목 코드 (ex. KRW-BTC)

to

string

마지막 캔들 시각 (exclusive). 비워서 요청시 가장 최근 캔들

count

int32

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

number

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

Updated 6 months ago

* * *

Did this page help you?

Yes

No

ShellPythonNode

```

xxxxxxxxxx

10

1# KRW-BTC 마켓에 가장 최근 년봉 1개를 요청

2curl --request GET \

3     --url 'https://api.upbit.com/v1/candles/years?market=KRW-BTC&count=1' \

4     --header 'accept: application/json'

5​

6# KRW-BTC 마켓에 2024년 10월 1일(UTC) 이전 가장 최근 년봉 1개를 요청

7curl --request GET \

8     --url 'https://api.upbit.com/v1/candles/years?market=KRW-BTC&count=1&to=2024-10-01%2000%3A00%3A00' \

9     --header 'accept: application/json'

10

```

```

xxxxxxxxxx

15



1

[\
\
2\
\
  {\
\
3    "market": "KRW-BTC",\
\
4    "candle_date_time_utc": "2024-01-01T00:00:00",\
\
5    "candle_date_time_kst": "2024-01-01T09:00:00",\
\
6    "opening_price": 96290000,\
\
7    "high_price": 1231356000,\
\
8    "low_price": 124.5,\
\
9    "trade_price": 85375000,\
\
10    "timestamp": 1727845502277,\
\
11    "candle_acc_trade_price": 60613272545.65653,\
\
12    "candle_acc_trade_volume": 708.81714523,\
\
13    "first_day_of_period": "2024-01-01"\
\
14  }\
\
15]

```

Updated 6 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EB_B6_84minute__EC_BA_94_EB_93_A4_1.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EB%B6%84minute-%EC%BA%94%EB%93%A4-1\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 마켓 코드 (ex. KRW-BTC) | String |
| to | 마지막 캔들 시각 (exclusive).<br>ISO8061 포맷 (yyyy-MM-dd'T'HH:mm:ss'Z' or yyyy-MM-dd HH:mm:ss). 기본적으로 UTC 기준 시간이며 `2023-01-01T00:00:00+09:00` 과 같이 KST 시간으로 요청 가능.<br>비워서 요청시 가장 최근 캔들 | String |
| count | 캔들 개수(최대 200개까지 요청 가능) | Integer |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EB%B6%84minute-%EC%BA%94%EB%93%A4-1\#response)

> ## 🚧  캔들은 해당 시간대에 체결이 발생한 경우에만 생성됩니다.
>
> - 예를 들어, 5분봉 캔들의 경우, candle\_date\_time이 2024-08-31T22:25:00인 캔들은 2024-08-31T22:25:00 (이상) ~ 2024-08-31T22:30:00 (미만)의 체결로 구성됩니다.
> - 해당 시간 동안 체결이 발생하지 않을 경우, 2024-08-31T22:25:00 캔들은 생성되지 않으며 응답에 포함되지 않습니다.

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 종목 코드 | String |
| candle\_date\_time\_utc | 캔들 기준 시각(UTC 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |
| candle\_date\_time\_kst | 캔들 기준 시각(KST 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |
| opening\_price | 시가 | Double |
| high\_price | 고가 | Double |
| low\_price | 저가 | Double |
| trade\_price | 종가 | Double |
| timestamp | 해당 캔들에서 마지막 틱이 저장된 시각 | Long |
| candle\_acc\_trade\_price | 누적 거래 금액 | Double |
| candle\_acc\_trade\_volume | 누적 거래량 | Double |
| unit | 분 단위(유닛) | Integer |

unit

int32

required

Defaults to 1

분 단위. 가능한 값 : 1, 3, 5, 15, 10, 30, 60, 240

market

string

required

종목 코드 (ex. KRW-BTC)

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

Updated 5 months ago

* * *

Did this page help you?

Yes

No

ShellPythonNode

```

xxxxxxxxxx

10

1# KRW-BTC 마켓에 가장 최근 1분봉 1개를 요청

2curl --request GET \

3     --url 'https://api.upbit.com/v1/candles/minutes/1?market=KRW-BTC&count=1' \

4     --header 'accept: application/json'

5​

6# KRW-BTC 마켓에 2024년 10월 1일(UTC) 이전 가장 최근 1분봉 1개를 요청

7curl --request GET \

8     --url 'https://api.upbit.com/v1/candles/minutes/1?market=KRW-BTC&count=1&to=2024-10-01%2000%3A00%3A00' \

9     --header 'accept: application/json'

10

```

```

xxxxxxxxxx

15



1

[\
\
2\
\
  {\
\
3    "market": "KRW-BTC",\
\
4    "candle_date_time_utc": "2018-04-18T10:16:00",\
\
5    "candle_date_time_kst": "2018-04-18T19:16:00",\
\
6    "opening_price": 8615000,\
\
7    "high_price": 8618000,\
\
8    "low_price": 8611000,\
\
9    "trade_price": 8616000,\
\
10    "timestamp": 1524046594584,\
\
11    "candle_acc_trade_price": 60018891.90054,\
\
12    "candle_acc_trade_volume": 6.96780929,\
\
13    "unit": 1\
\
14  }\
\
15]

```

Updated 5 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EC_A0_84_EC_B2_B4__EC_B6_9C_EA_B8_88__EC_A1_B0_ED_9A_8C.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EC%A0%84%EC%B2%B4-%EC%B6%9C%EA%B8%88-%EC%A1%B0%ED%9A%8C\#request-parameters)

| Name | 설명 | 타입 |
| --- | --- | --- |
| currency | Currency 코드 | String |
| state | 출금 상태 | String |
| uuids\[\] | 출금 UUID의 목록 | Array |
| txids\[\] | 출금 TXID의 목록 | Array |
| limit | 개수 제한 (default: 100, max: 100) | Number |
| page | 페이지 수, default: 1 | Number |
| order\_by | 정렬<br>\- `asc` : 오름차순<br>\- `desc` : 내림차순 (default) | String |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EC%A0%84%EC%B2%B4-%EC%B6%9C%EA%B8%88-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| type | 입출금 종류 | String |
| uuid | 출금의 고유 아이디 | String |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| net\_type | 출금 네트워크 | String |
| txid | 출금의 트랜잭션 아이디 | String |
| state | 출금 상태<br>\- `WAITING` : 대기중<br>\- `PROCESSING` : 진행중<br>\- `DONE` : 완료<br>\- `FAILED` : 실패<br>\- `CANCELLED` : 취소됨<br>\- `REJECTED` : 거절됨 | String |
| created\_at | 출금 생성 시간 | DateString |
| done\_at | 출금 완료 시간 | DateString |
| amount | 출금 금액/수량 | NumberString |
| fee | 출금 수수료 | NumberString |
| transaction\_type | 출금 유형<br>_`default` : 일반출금_ `internal` : 바로출금 | String |

currency

string

Currency 코드

state

string

출금 상태

uuids\[\]

array of strings

출금 UUID의 목록

uuids\[\]
ADD string

txids\[\]

array of strings

출금 TXID의 목록

txids\[\]
ADD string

limit

int32

Defaults to 100

갯수 제한

page

int32

Defaults to 1

order\_by

string

Defaults to desc

정렬

Authorization

string

required

Authorization token (JWT)

# `` 200      200

json

# `` 4XX      4XX

object

error

object

name

string

message

string

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

55

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const queryEncode = require("querystring").encode

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11const currency = 'XRP'

12const state = 'DONE'

13

const txids = [\
\
14    '98c15999f0bdc4ae0e8a-ed35868bb0c204fe6ec29e4058a3451e-88636d1040f4baddf943274ce37cf9cc',\
\
15    // ...\
\
16]

17​

18

const non_array_body = {

19    currency: currency,

20    state: state,

21}

22

const array_body = {

23    txids: txids,

24}

25

const body = {

26    ...non_array_body,

```

```

xxxxxxxxxx

16



1

[\
\
2\
\
  {\
\
3    "type": "withdraw",\
\
4    "uuid": "35a4f1dc-1db5-4d6b-89b5-7ec137875956",\
\
5    "currency": "XRP",\
\
6    "net_type": "XRP",\
\
7    "txid": "98c15999f0bdc4ae0e8a-ed35868bb0c204fe6ec29e4058a3451e-88636d1040f4baddf943274ce37cf9cc",\
\
8    "state": "DONE",\
\
9    "created_at": "2019-02-28T15:17:51+09:00",\
\
10    "done_at": "2019-02-28T15:22:12+09:00",\
\
11    "amount": "1.00",\
\
12    "fee": "0.0",\
\
13    "transaction_type": "default"\
\
14  }\
\
15  # ....\
\
16]

```

Updated 3 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EA_B0_9C_EB_B3_84__EC_9E_85_EA_B8_88__EC_A1_B0_ED_9A_8C.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EA%B0%9C%EB%B3%84-%EC%9E%85%EA%B8%88-%EC%A1%B0%ED%9A%8C\#request-parameters)

| Name | 설명 | 타입 |
| --- | --- | --- |
| uuid | 입금 UUID | String |
| txid | 입금 TXID | String |
| currency | Currency 코드 | String |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EA%B0%9C%EB%B3%84-%EC%9E%85%EA%B8%88-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| type | 입출금 종류 | String |
| uuid | 입금에 대한 고유 아이디 | String |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| net\_type | 입금 네트워크 | String |
| txid | 입금의 트랜잭션 아이디 | String |
| state | 입금 상태<br>\- `PROCESSING` : 입금 진행중<br>\- `ACCEPTED` : 완료<br>\- `CANCELLED` : 취소됨<br>\- `REJECTED` : 거절됨<br>\- `TRAVEL_RULE_SUSPECTED` : 트래블룰 추가 인증 대기중<br>\- `REFUNDING` : 반환절차 진행중<br>\- `REFUNDED` : 반환됨 | String |
| created\_at | 입금 생성 시간 | DateString |
| done\_at | 입금 완료 시간 | DateString |
| amount | 입금 수량 | NumberString |
| fee | 입금 수수료 | NumberString |
| transaction\_type | 입금 유형<br>_`default` : 일반입금_ `internal` : 바로입금 | String |

uuid

string

개별 입금의 UUID

txid

string

개별 입금의 TXID

currency

string

Currency 코드

Authorization

string

required

Authorization token (JWT)

# `` 200      200

json

# `` 400      400

object

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

39

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const queryEncode = require("querystring").encode

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11

const body = {

12    uuid: '94332e99-3a87-4a35-ad98-28b0c969f830'

13}

14​

15const query = queryEncode(body)

16​

17const hash = crypto.createHash('sha512')

18const queryHash = hash.update(query, 'utf-8').digest('hex')

19​

20

const payload = {

21    access_key: access_key,

22    nonce: uuidv4(),

23    query_hash: queryHash,

24    query_hash_alg: 'SHA512',

25}

26​

```

```

xxxxxxxxxx

13



1

{

2  "type": "deposit",

3  "uuid": "94332e99-3a87-4a35-ad98-28b0c969f830",

4  "currency": "KRW",

5  "net_type": None,

6  "txid": "BKD-2000-12-29-aeked29c05eadac293b4214994",

7  "state": "ACCEPTED",

8  "created_at": "2017-12-08T15:38:02+09:00",

9  "done_at": "2017-12-08T15:38:02+09:00",

10  "amount": "100000.0",

11  "fee": "0.0",

12  "transaction_type": "default"

13}

```

Updated 3 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EC_A2_85_EB_A3_8C__EC_A3_BC_EB_AC_B8__EC_A1_B0_ED_9A_8C.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EC%A2%85%EB%A3%8C-%EC%A3%BC%EB%AC%B8-%EC%A1%B0%ED%9A%8C\#request-parameters)

> ## 📘  해당 API를 통해 **종료된 상태(done, cancel)** 인 주문을 조회할 수 있습니다.
>
> - [uuid 또는 identifiers 기준 조회](https://docs.upbit.com/kr/reference/id%EB%A1%9C-%EC%A3%BC%EB%AC%B8-%EC%A1%B0%ED%9A%8C) 가 필요시 `v1/orders/uuids` 를 이용해 주세요.
> - [체결 대기 주문 조회](https://docs.upbit.com/kr/reference/%EB%8C%80%EA%B8%B0-%EC%A3%BC%EB%AC%B8-%EC%A1%B0%ED%9A%8C) 필요시 `v1/orders/open` 을 이용해 주세요.

| Name | 설명 | 타입 |
| --- | --- | --- |
| market | 마켓 ID | String |
| state | 주문 상태<br>`done` : 전체 체결 완료<br>`cancel` : 주문 취소<br>\- 시장가 주문이 조회되지 않는 경우: 시장가 매수 주문은 체결 후 주문 상태가 cancel, done 두 경우 모두 발생할 수 있습니다.<br>\- 시장가로 체결이 일어난 후 주문 잔량이 발생하는 경우, 남은 잔량이 반환되며 cancel 처리됩니다. 대부분의 경우 소수점 아래 8자리까지 나누어떨어지지 않는 미미한 금액이 주문 잔량으로 발생하게 됩니다.<br>\- 만일 주문 잔량 없이 딱 맞아떨어지게 체결이 발생한 경우에는 주문 상태가 done이 됩니다. | String |
| states\[\] | 주문 상태의 목록, **default: \['done', 'cancel'\]**<br>\* **기본값은 `done`, `cancel` 둘 다** 조회됩니다.<br>\\* state와 states는 동시에 사용할 수 없습니다. 둘 중 하나만 지정하시기를 바랍니다. | Array\[String\] |
| start\_time | 조회 시작 시각 (주문 생성시각 기준)<br>\- start\_time 과 end\_time 은 Time Zone 이 포함된 **ISO-8601 포맷**(ex. 2024-12-09T13:56:53+09:00) 혹은 [밀리세컨드 단위의 **Timestamp**(ex.1733720213791)](https://docs.upbit.com/kr/changelog/closed_order_support_timestamp) 여야 합니다.<br>\- **start\_time, end\_time이 둘 다 정의되지 않은 경우 현재 시각으로부터 최대 7일 전까지의 주문이 조회** 됩니다.<br>\- start\_time만 정의한 경우 start\_time으로부터 최대 7일 후까지의 주문이 조회됩니다.<br>\- end\_time만 정의한 경우 end\_time으로부터 최대 7일 전까지의 주문이 조회됩니다.<br>\- start\_time과 end\_time을 둘 다 정의할 경우 최대 7일 범위까지의 주문만 조회가 가능합니다.<br>\- \*조회 시간 내의 주문 건이라도 limit 개수를 초과한 범위일 경우 조회되지 않으니 이 경우 나누어서 조회하여야 합니다. | String |
| end\_time | 조회 종료 시각 (주문 생성시각 기준) | String |
| limit | 요청 개수, **default: 100**, max: 1,000<br>\- 주문 조회 가능한 최대 개수는 1,000개이며, 시간 범위 내 주문 개수가 1,000개가 넘어갈 경우 시간 범위를 나누어 조회하여야 합니다. | Number |
| order\_by | 정렬 방식<br>\- `asc` : 오름차순<br>\- `desc` : 내림차순 **(default)** | String |

\*default 값에 따라, **어떤 파라미터도 명시하지 않으시면 최근 7일 이내의 종료된 주문 100개** 가 응답됩니다.

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EC%A2%85%EB%A3%8C-%EC%A3%BC%EB%AC%B8-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| uuid | 주문의 고유 아이디 | String |
| side | 주문 종류 | String |
| ord\_type | 주문 방식<br>\- `limit` : 지정가 주문<br>\- `price` : 시장가 주문(매수)<br>\- `market` : 시장가 주문(매도)<br>\- `best` : [최유리 주문](https://docs.upbit.com/kr/changelog/new_ord_type_expand) | String |
| price | 주문 당시 화폐 가격 | NumberString |
| state | 주문 상태 | String |
| market | 마켓 ID | String |
| created\_at | 주문 생성 시각 | DateString |
| volume | 사용자가 입력한 주문 양 | NumberString |
| remaining\_volume | 체결 후 남은 주문 양 | NumberString |
| reserved\_fee | 수수료로 예약된 비용 | NumberString |
| remaining\_fee | 남은 수수료 | NumberString |
| paid\_fee | 사용된 수수료 | NumberString |
| locked | 거래에 사용 중인 비용 | NumberString |
| executed\_volume | 체결된 양 | NumberString |
| executed\_funds | 현재까지 체결된 금액 | NumberString |
| trades\_count | 해당 주문에 걸린 체결 수 | Integer |
| time\_in\_force | [IOC, FOK 설정](https://docs.upbit.com/kr/changelog/new_ord_type_expand)<br>\- `ioc` : Immediate or Cancel<br>\- `fok` : Fill or Kill | String |
| identifier | 조회용 사용자 지정값<br>\*identifier 필드는 2024-10-18 이후에 생성된 주문에 대해서만 제공합니다. | String |

\*null인 필드는 응답에서 제외됩니다. (예: IOC or FOK 설정이 없었던 주문의 경우 해당 필드는 응답되지 않습니다.

market

string

마켓 아이디

state

string

주문 상태

states\[\]

array of strings

Defaults to done,cancel

주문 상태의 목록

states\[\]
ADD string

start\_time

string

Defaults to 7일 전

조회 시작 시각

end\_time

string

조회 종료 시각

limit

float

Defaults to 100

요청 개수

order\_by

string

Defaults to desc

정렬 방식

Authorization

string

Authorization token (JWT)

# `` 200      200

json

# `` 4XX      4XX

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

NodePythonRubyJava

```

xxxxxxxxxx

51

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const queryEncode = require("querystring").encode

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11const endTime = '2023-01-01T10:00:00+09:00'

12const market = 'KRW-BTC'

13const states = ['done', 'cancel']

14​

15

const non_array_body = {

16    market: market,

17}

18

const array_body = {

19    states: states,

20}

21

const body = {

22    ...non_array_body,

23    ...array_body

24}

25​

26const states_query = states.map(state => `states[]=${state}`).join('&')

```

```

xxxxxxxxxx

21



1

[\
\
2\
\
  {\
\
3    "uuid": "e5715c44-2d1a-41e6-91d8-afa579e28731",\
\
4    "side": "ask",\
\
5    "ord_type": "limit",\
\
6    "price": "103813000",\
\
7    "state": "done",\
\
8    "market": "KRW-BTC",\
\
9    "created_at": "2024-06-13T10:28:36+09:00",\
\
10    "volume": "0.00039132",\
\
11    "remaining_volume": "0",\
\
12    "reserved_fee": "0",\
\
13    "remaining_fee": "0",\
\
14    "paid_fee": "20.44627434",\
\
15    "locked": "0",\
\
16    "executed_volume": "0.00039132",\
\
17    "executed_funds": "40892.54868",\
\
18    "trades_count": 2\
\
19  },\
\
20  # ....\
\
21]

```

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EB_94_94_EC_A7_80_ED_84_B8_EC_9E_90_EC_82_B0__EC_B6_9C_EA_B8_88_ED_95_98_EA_B8_B0.md]
> ## 📘  허용된 지갑 주소로만 출금을 진행할 수 있습니다.
>
> Open API를 이용하여 출금을 진행하기 위해서는 출금허용주소 등록이 필요합니다. 다음 페이지에서 출금 주소를 등록해주시길 바랍니다.
>
> 업비트 웹 \[마이페이지\] \> \[Open API 관리\] > \[디지털 자산 출금주소 관리\] 탭

> ## 📘  업비트 회원의 지갑 주소로만 바로출금을 진행할 수 있습니다.
>
> 업비트 회원의 주소가 아닌 주소로 바로출금을 요청하는 경우, 출금이 정상적으로 수행되지 않습니다. 반드시 주소를 확인 후 출금을 진행하시기 바랍니다.

> ## 🚧  (2023-05-23) 출금 네트워크( `net_type`) 파라미터가 추가됩니다.
>
> 멀티체인 입출금 지원에 따라, 디지털 자산 출금 요청 시 출금 네트워크( `net_type`) 파라미터가 필수로 입력되어야 합니다. 출금하실 네트워크의 `net_type` 값은 [출금 허용 주소 리스트 조회 API](https://docs.upbit.com/kr/reference/%EC%B6%9C%EA%B8%88-%ED%97%88%EC%9A%A9-%EC%A3%BC%EC%86%8C-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C) 를 통해 확인 가능합니다.
>
> 자세한 내용은 [공지사항](https://docs.upbit.com/kr/changelog/net_type) 을 참조 부탁드립니다.

## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EB%94%94%EC%A7%80%ED%84%B8%EC%9E%90%EC%82%B0-%EC%B6%9C%EA%B8%88%ED%95%98%EA%B8%B0\#request-parameters)

| Name | 설명 | 타입 |
| --- | --- | --- |
| currency \* | Currency 코드 | String |
| net\_type \* | 출금 네트워크 | String |
| amount \* | 출금 수량 | NumberString |
| address \* | 출금 가능 주소에 등록된 출금 주소 | String |
| secondary\_address | 2차 출금 주소 (필요한 디지털 자산에 한해서) | String |
| transaction\_type | 출금 유형<br>_`default` : 일반출금_ `internal` : 바로출금 | String |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EB%94%94%EC%A7%80%ED%84%B8%EC%9E%90%EC%82%B0-%EC%B6%9C%EA%B8%88%ED%95%98%EA%B8%B0\#response)

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
| transaction\_type | 출금 유형 | String |

currency

string

required

Currency symbol

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

transaction\_type

string

Defaults to default

출금 유형

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

krw\_amount

string

transaction\_type

string

# `` 4XX      4XX

object

error

object

name

string

message

string

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

42

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const queryEncode = require("querystring").encode

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11

const body = {

12    currency: 'BTC',

13    net_type: 'BTC',

14    amount: '0.01',

15    address: '3EusRwybuZUhVDeHL7gh3HSLmbhLcy7NqD'

16}

17​

18const query = queryEncode(body)

19​

20const hash = crypto.createHash('sha512')

21const queryHash = hash.update(query, 'utf-8').digest('hex')

22​

23

const payload = {

24    access_key: access_key,

25    nonce: uuidv4(),

26    query_hash: queryHash,

```

```

xxxxxxxxxx

14



1

{

2  "type": "withdraw",

3  "uuid": "9f432943-54e0-40b7-825f-b6fec8b42b79",

4  "currency": "BTC",

5  "net_type": "BTC",

6  "txid": "ebe6937b-130e-4066-8ac6-4b0e67f28adc",

7  "state": "processing",

8  "created_at": "2018-04-13T11:24:01+09:00",

9  "done_at": null,

10  "amount": "0.01",

11  "fee": "0.0",

12  "krw_amount": "80420.0",

13  "transaction_type": "default"

14}

```

Updated 3 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EC_9E_85_EA_B8_88__EB_A6_AC_EC_8A_A4_ED_8A_B8__EC_A1_B0_ED_9A_8C.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EC%9E%85%EA%B8%88-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C\#request-parameters)

| Name | 설명 | 타입 |
| --- | --- | --- |
| currency | Currency 코드 | String |
| state | 입금 상태 | String |
| uuids\[\] | 입금 UUID의 목록 | Array |
| txids\[\] | 입금 TXID의 목록 | Array |
| limit | 개수 제한 (default: 100, limit: 100) | Number |
| page | 페이지 수, default: 1 | Number |
| order\_by | 정렬<br>\- `asc` : 오름차순<br>\- `desc` : 내림차순 (default) | String |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EC%9E%85%EA%B8%88-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| type | 입출금 종류 | String |
| uuid | 입금에 대한 고유 아이디 | String |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| net\_type | 입금 네트워크 | String |
| txid | 입금의 트랜잭션 아이디 | String |
| state | 입금 상태<br>\- `PROCESSING` : 입금 진행중<br>\- `ACCEPTED` : 완료<br>\- `CANCELLED` : 취소됨<br>\- `REJECTED` : 거절됨<br>\- `TRAVEL_RULE_SUSPECTED` : 트래블룰 추가 인증 대기중<br>\- `REFUNDING` : 반환절차 진행중<br>\- `REFUNDED` : 반환됨 | String |
| created\_at | 입금 생성 시간 | DateString |
| done\_at | 입금 완료 시간 | DateString |
| amount | 입금 수량 | NumberString |
| fee | 입금 수수료 | NumberString |
| transaction\_type | 입금 유형<br>_`default` : 일반입금_ `internal` : 바로입금 | String |

currency

string

Currency 코드

state

string

입금 상태

uuids\[\]

array of strings

입금 UUID의 목록

uuids\[\]
ADD string

txids\[\]

array of strings

입금 TXID의 목록

txids\[\]
ADD string

limit

int32

Defaults to 100

페이지당 개수

page

int32

Defaults to 1

페이지 번호

order\_by

string

Defaults to desc

정렬 방식

Authorization

string

required

Authorization token(JWT)

# `` 200      200

json

# `` 400      400

object

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

53
const txid_query = txids.map(txid => `txids[]=${txid}`).join('&')

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const queryEncode = require("querystring").encode

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11const currency = 'KRW'

12

const txids = [\
\
13    '9e37c537-6849-4c8b-a134-57313f5dfc5a',\
\
14    // ...\
\
15]

16​

17

const non_array_body = {

18    currnecy: currency,

19}

20

const array_body = {

21    txids: txids,

22}

23

const body = {

24    ...non_array_body,

25    ...array_body

26}

```

```

xxxxxxxxxx

15



1

[\
\
2\
\
  {\
\
3    "type": "deposit",\
\
4    "uuid": "94332e99-3a87-4a35-ad98-28b0c969f830",\
\
5    "currency": "KRW",\
\
6    "txid": "9e37c537-6849-4c8b-a134-57313f5dfc5a",\
\
7    "state": "ACCEPTED",\
\
8    "created_at": "2017-12-08T15:38:02+09:00",\
\
9    "done_at": "2017-12-08T15:38:02+09:00",\
\
10    "amount": "100000.0",\
\
11    "fee": "0.0",\
\
12    "transaction_type": "default"\
\
13  }\
\
14  #....\
\
15]

```

Updated 3 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EC_9B_94month__EC_BA_94_EB_93_A4_1.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EC%9B%94month-%EC%BA%94%EB%93%A4-1\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 종목 코드 (ex. KRW-BTC) | String |
| to | 마지막 캔들 시각 (exclusive).<br>ISO8061 포맷 (yyyy-MM-dd'T'HH:mm:ss'Z' or yyyy-MM-dd HH:mm:ss). 기본적으로 UTC 기준 시간이며 `2023-01-01T00:00:00+09:00` 과 같이 KST 시간으로 요청 가능.<br>비워서 요청시 가장 최근 캔들 | String |
| count | 캔들 개수(최대 200개까지 요청 가능) | Integer |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EC%9B%94month-%EC%BA%94%EB%93%A4-1\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 종목 코드 | String |
| candle\_date\_time\_utc | 캔들 기준 시각(UTC 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |
| candle\_date\_time\_kst | 캔들 기준 시각(KST 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |
| opening\_price | 시가 | Double |
| high\_price | 고가 | Double |
| low\_price | 저가 | Double |
| trade\_price | 종가 | Double |
| timestamp | 마지막 틱이 저장된 시각 | Long |
| candle\_acc\_trade\_price | 누적 거래 금액 | Double |
| candle\_acc\_trade\_volume | 누적 거래량 | Double |
| first\_day\_of\_period | 캔들 기간의 가장 첫 날 | String |

market

string

required

종목 코드 (ex. KRW-BTC)

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

Updated 7 months ago

* * *

Did this page help you?

Yes

No

ShellPythonNode

```

xxxxxxxxxx

10

1# KRW-BTC 마켓에 가장 최근 월봉 1개를 요청

2curl --request GET \

3     --url 'https://api.upbit.com/v1/candles/months?market=KRW-BTC&count=1' \

4     --header 'accept: application/json'

5​

6# KRW-BTC 마켓에 2024년 10월 1일(UTC) 이전 가장 최근 월봉 1개를 요청

7curl --request GET \

8     --url 'https://api.upbit.com/v1/candles/months?market=KRW-BTC&count=1&to=2024-10-01%2000%3A00%3A00' \

9     --header 'accept: application/json'

10

```

```

xxxxxxxxxx

15



1

[\
\
2\
\
  {\
\
3    "market": "KRW-BTC",\
\
4    "candle_date_time_utc": "2018-04-01T00:00:00",\
\
5    "candle_date_time_kst": "2018-04-01T09:00:00",\
\
6    "opening_price": 7688000,\
\
7    "high_price": 8840000,\
\
8    "low_price": 7087000,\
\
9    "trade_price": 8614000,\
\
10    "timestamp": 1524046761201,\
\
11    "candle_acc_trade_price": 2665448149094.0195,\
\
12    "candle_acc_trade_volume": 336501.67751807,\
\
13    "first_day_of_period": "2018-04-01"\
\
14  }\
\
15]

```

Updated 7 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference_websocket_request_format.md]
연결이 성공적으로 이루어졌다면 웹소켓 서버에 여러가지 요청을 할 수 있습니다.

요청은 JSON Object를 이용하며 응답 또한 JSON Object 입니다.

요청은 크게 ticket field, type field, format field 로 나누어지며 각각의 필드는 다음 구성요소로 이루어져 있습니다.

> ## 📘  Request format
>
> **\[{Ticket Field},{Type Field},....,{Type Field},{Format Field}\]**

### **Ticket Field**   [Skip link to [object Object]](https://docs.upbit.com/kr/reference/websocket-request-format\#ticket-field)

일반적으로 용도를 식별하기 위해 ticket 이라는 필드값이 필요합니다.

이 값은 시세를 수신하는 대상을 식별하며 되도록 유니크한 값을 사용하도록 권장합니다. (UUID 등)

| 필드명 | 타입 | 내용 | 필수 여부 |
| --- | --- | --- | --- |
| ticket | String | 요청자를 식별할 수 있는 값 | O |

### **Type Field**   [Skip link to [object Object]](https://docs.upbit.com/kr/reference/websocket-request-format\#type-field)

수신하고 싶은 시세 정보를 나열하는 필드입니다.

is\_only\_snapshot, is\_only\_realtime 필드는 생략 가능하며 모두 생략시 스냅샷과 실시간 데이터 모두를 수신합니다.

하나의 요청에 {type field}는 여러개를 명시할 수 있습니다. 자세한 요청 방법은 타입별 요청 및 응답을 참고하시길 바랍니다.

### **Format Field**   [Skip link to [object Object]](https://docs.upbit.com/kr/reference/websocket-request-format\#format-field)

마지막으로 포맷 정보입니다. Simple로 지정될 경우 응답의 필드명이 모두 간소화됩니다. 트래픽 부담이 클 때 사용하는 방법입니다.

| 필드명 | 타입 | 내용 | 필수 여부 | 기본 값 |
| --- | --- | --- | --- | --- |
| format | String | 수신할 포맷<br>\- `DEFAULT`: 기본형<br>\- `SIMPLE`: 축약형 | X | `DEFAULT` |

Updated 7 months ago

* * *

Did this page help you?

Yes

No

Updated 7 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EC_9E_85_EA_B8_88__EC_A3_BC_EC_86_8C__EC_83_9D_EC_84_B1__EC_9A_94_EC_B2_AD.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EC%9E%85%EA%B8%88-%EC%A3%BC%EC%86%8C-%EC%83%9D%EC%84%B1-%EC%9A%94%EC%B2%AD\#request-parameters)

| Name | 설명 | 타입 |
| --- | --- | --- |
| currency \* | Currency 코드 | String |
| net\_type \* | 입금 네트워크 | String |

## Response1   [Skip link to Response1](https://docs.upbit.com/kr/reference/%EC%9E%85%EA%B8%88-%EC%A3%BC%EC%86%8C-%EC%83%9D%EC%84%B1-%EC%9A%94%EC%B2%AD\#response1)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| success | 요청 성공 여부 | Boolean |
| message | 요청 결과에 대한 메세지 | String |

## Response2   [Skip link to Response2](https://docs.upbit.com/kr/reference/%EC%9E%85%EA%B8%88-%EC%A3%BC%EC%86%8C-%EC%83%9D%EC%84%B1-%EC%9A%94%EC%B2%AD\#response2)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| net\_type | 입금 네트워크 | String |
| deposit\_address | 입금 주소 | String |
| secondary\_address | 2차 입금 주소 | String |

> ## 📘  입금 주소 생성 요청 API 유의사항
>
> 입금 주소의 생성은 서버에서 비동기적으로 이뤄집니다.
>
> 비동기적 생성 특성상 요청과 동시에 입금 주소가 발급되지 않을 수 있습니다.
>
> 주소 발급 요청 시 결과로 Response1이 반환되며 주소 발급 완료 이전까지 계속 Response1이 반환됩니다.
>
> 주소가 발급된 이후부터는 새로운 주소가 발급되는 것이 아닌 이전에 발급된 주소가 Response2 형태로 반환됩니다.
>
> 정상적으로 주소가 생성되지 않는다면 일정 시간 이후 해당 API를 다시 호출해주시길 부탁드립니다.

currency

string

required

Currency symbol

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

success

boolean

Defaults to true

message

string

# `` 4XX      4XX

object

error

object

name

string

message

string

Updated 22 days ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

40

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const queryEncode = require("querystring").encode

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11

const body = {

12    currency: 'BTC',

13    net_type: 'BTC'

14}

15​

16const query = queryEncode(body)

17​

18const hash = crypto.createHash('sha512')

19const queryHash = hash.update(query, 'utf-8').digest('hex')

20​

21

const payload = {

22    access_key: access_key,

23    nonce: uuidv4(),

24    query_hash: queryHash,

25    query_hash_alg: 'SHA512',

26}

```

```

xxxxxxxxxx



1

{

2  "success": true,

3  "message": "BTC 입금주소를 생성중입니다."

4}

```

Updated 22 days ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference_supported_levels.md]
> ## 📘  v1.4.4 호가 모아보기 기능 추가 (원화마켓만 지원)
>
> v1.4.4 부터 **[v1/orderbook](https://docs.upbit.com/kr/reference/%ED%98%B8%EA%B0%80-%EC%A0%95%EB%B3%B4-%EC%A1%B0%ED%9A%8C)** 에서 `level` 항목을 통해 호가 모아보기를 지원합니다.
>
> 각 종목별 지원하는 호가 모아보기 단위를 **v1/orderbook/supported\_levels** 에서 확인하실 수 있습니다.

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/supported_levels\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 종목 코드 | String |
| supported\_levels | 해당 종목에서 지원하는 모아보기 단위<br>\*0: 기본 호가단위<br>\*호가 모아보기 기능은 원화마켓(KRW)에서만 지원하므로 BTC, USDT 마켓의 경우 0만 존재합니다. | Array\[Double\] |

markets

array of strings

required

종목 코드 목록 (ex. markets=KRW-BTC&markets=KRW-ETH)

markets\*
ADD string

# `` 200      200

array of objects

object

market

string

supported\_levels

array of integers

supported\_levels

# `` 4XX      4XX

json

Updated 3 months ago

* * *

Did this page help you?

Yes

No

ShellPythonNode

```

xxxxxxxxxx

1curl -X GET "https://api.upbit.com/v1/orderbook/supported_levels?markets=KRW-BTC&markets=KRW-ETH&markets=KRW-BTT&markets=BTC-XRP" -H "accept: */*"

```

```

xxxxxxxxxx

34
]

1

[\
\
2\
\
  {\
\
3    "market": "KRW-BTC",\
\
4\
\
    "supported_levels": [\
\
5      0,\
\
6      10000,\
\
7      100000,\
\
8      1000000,\
\
9      10000000\
\
10    ]\
\
11  },\
\
12\
\
  {\
\
13    "market": "KRW-ETH",\
\
14\
\
    "supported_levels": [\
\
15      0,\
\
16      10000,\
\
17      100000,\
\
18      1000000\
\
19    ]\
\
20  },\
\
21\
\
  {\
\
22    "market": "KRW-BTT",\
\
23\
\
    "supported_levels": [\
\
24      0,\
\
25      0.001\
\
```\
\
Updated 3 months ago\
\
* * *\
\
Did this page help you?\
\
Yes\
\
No\
\
## Open API 이용약관\
\
본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.\
\
제 1조 (목적)\
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.\
\
제 2조 (정의)\
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.\
\
2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.\
\
3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.\
\
제 3조 (면책사항)\
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.\
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.\
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.\
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.\
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.\
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.\
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.\
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.\
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.\
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.\
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.\
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.\
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.\
\
제 4조 (Open API 서비스 제공의 제한 및 해지)\
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.\
1\. 본 이용약관 제6조를 위반한 경우\
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우\
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우\
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우\
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우\
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.\
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.\
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.\
\
제 5조 (저작권)\
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.\
\
제 6조 (사용자의 의무와 책임)\
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.\
1\. API 업데이트 및 변경 사항에 대한 공지\
2\. 제도 변경 공지\
3\. 두나무-업비트 정책 반영에 따른 공지\
4\. 기타 긴급 공지\
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.\
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.\
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.\
\
제 7조 (약관의 변경 등)\
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.\
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).\
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.\
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.\
\
제 8조 (효력 발생 및 유효기간)\
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.\
\
제 9조 (기타)\
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.\
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.\
\
제 10조 (관할법원)\
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.\
\
<부칙>\
본 이용약관은 2024년 10월 30일부터 적용됩니다.\
이전의 이용약관은 아래에서 확인하실 수 있습니다.\
\
\
[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)\
\
[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)\
\
[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)\
\
[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)\
\
동의

[docs_upbit_com_kr_reference__EC_A3_BC_EB_AC_B8__EC_B7_A8_EC_86_8C.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EC%A3%BC%EB%AC%B8-%EC%B7%A8%EC%86%8C\#request-parameters)

| Name | 설명 | 타입 |
| --- | --- | --- |
| uuid | 취소할 주문의 UUID | String |
| identifier | 조회용 사용자 지정값 | String |

> ## 🚧
>
> `uuid` 혹은 `identifier` 둘 중 하나의 값이 반드시 포함되어야 합니다.

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EC%A3%BC%EB%AC%B8-%EC%B7%A8%EC%86%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| uuid | 주문의 고유 아이디 | String |
| side | 주문 종류 | String |
| ord\_type | 주문 방식 | String |
| price | 주문 당시 화폐 가격 | NumberString |
| state | 주문 상태 | String |
| market | 마켓의 유일키 | String |
| created\_at | 주문 생성 시간 | String |
| volume | 사용자가 입력한 주문 양 | NumberString |
| remaining\_volume | 체결 후 남은 주문 양 | NumberString |
| reserved\_fee | 수수료로 예약된 비용 | NumberString |
| remaining\_fee | 남은 수수료 | NumberString |
| paid\_fee | 사용된 수수료 | NumberString |
| locked | 거래에 사용중인 비용 | NumberString |
| executed\_volume | 체결된 양 | NumberString |
| trades\_count | 해당 주문에 걸린 체결 수 | Integer |
| identifier | 조회용 사용자 지정값<br>\*identifier 필드는 2024-10-18 이후에 생성된 주문에 대해서만 제공합니다. | String |

uuid

string

주문 UUID

identifier

string

조회용 사용자 지정값

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

# `` 4XX      4XX

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

NodePythonRubyJava

```

xxxxxxxxxx

38

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const queryEncode = require("querystring").encode

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11

const body = {

12    uuid: 'cdd92199-2897-4e14-9448-f923320408ad'

13}

14​

15const query = queryEncode(body)

16​

17const hash = crypto.createHash('sha512')

18const queryHash = hash.update(query, 'utf-8').digest('hex')

19​

20

const payload = {

21    access_key: access_key,

22    nonce: uuidv4(),

23    query_hash: queryHash,

24    query_hash_alg: 'SHA512',

25}

26​

```

```

xxxxxxxxxx

17



1

{

2  "uuid": "cdd92199-2897-4e14-9448-f923320408ad",

3  "side": "bid",

4  "ord_type": "limit",

5  "price": "100.0",

6  "state": "wait",

7  "market": "KRW-BTC",

8  "created_at": "2018-04-10T15:42:23+09:00",

9  "volume": "0.01",

10  "remaining_volume": "0.01",

11  "reserved_fee": "0.0015",

12  "remaining_fee": "0.0015",

13  "paid_fee": "0.0",

14  "locked": "1.0015",

15  "executed_volume": "0.0",

16  "trades_count": 0

17}

```

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EB_A7_88_EC_BC_93__EC_BD_94_EB_93_9C__EC_A1_B0_ED_9A_8C.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EB%A7%88%EC%BC%93-%EC%BD%94%EB%93%9C-%EC%A1%B0%ED%9A%8C\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| is\_details | 유의종목 필드과 같은 상세 정보 노출 여부 (default: false) | Boolean |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EB%A7%88%EC%BC%93-%EC%BD%94%EB%93%9C-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 업비트에서 제공중인 시장 정보 | String |
| korean\_name | 거래 대상 디지털 자산 한글명 | String |
| english\_name | 거래 대상 디지털 자산 영문명 | String |
| market\_event.warning | 업비트 시장경보 \> **유의종목** 지정 여부<br>\*유의, 주의 경보에 대한 구분은 [관련 공지사항을 참고](https://upbit.com/service_center/notice?id=3482) 하시기 바랍니다. | Boolean |
| market\_event.caution | 업비트 시장경보 \> **주의종목** 지정 여부<br>\*주의 경보 타입은 아래와 같으며, 자세한 정보는 [관련 공지사항을 참고](https://upbit.com/service_center/notice?id=3606) 하시기 바랍니다.<br>\- `PRICE_FLUCTUATIONS`: 가격 급등락 경보 발령 여부<br>\- `TRADING_VOLUME_SOARING`: 거래량 급등 경보 발령 여부<br>\- `DEPOSIT_AMOUNT_SOARING`: 입금량 급등 경보 발령 여부<br>\- `GLOBAL_PRICE_DIFFERENCES`: 가격 차이 경보 발령 여부<br>\- `CONCENTRATION_OF_SMALL_ACCOUNTS`: 소수 계정 집중 경보 발령 여부 | Object |

is\_details

boolean

Defaults to false

유의종목 필드과 같은 상세 정보 노출 여부 (선택 파라미터)

# `` 200      200

json

# `` 400      400

json

Updated 3 months ago

* * *

Did this page help you?

Yes

No

ShellPythonNode

```

xxxxxxxxxx

1curl -X GET "https://api.upbit.com/v1/market/all?is_details=true" -H "accept: */*"

```

```

xxxxxxxxxx

33
]

1

[\
\
2\
\
  {\
\
3    "market": "KRW-BTC",\
\
4    "korean_name": "비트코인",\
\
5    "english_name": "Bitcoin",\
\
6\
\
    "market_event": {\
\
7      "warning": false,\
\
8\
\
      "caution": {\
\
9        "PRICE_FLUCTUATIONS": false,\
\
10        "TRADING_VOLUME_SOARING": false,\
\
11        "DEPOSIT_AMOUNT_SOARING": true,\
\
12        "GLOBAL_PRICE_DIFFERENCES": false,\
\
13        "CONCENTRATION_OF_SMALL_ACCOUNTS": false\
\
14      }\
\
15    }\
\
16  },\
\
17\
\
  {\
\
18    "market": "KRW-ETH",\
\
19    "korean_name": "이더리움",\
\
20    "english_name": "Ethereum",\
\
21\
\
    "market_event": {\
\
22      "warning": true,\
\
23\
\
      "caution": {\
\
24        "PRICE_FLUCTUATIONS": false,\
\
25        "TRADING_VOLUME_SOARING": false,\
\
```\
\
Updated 3 months ago\
\
* * *\
\
Did this page help you?\
\
Yes\
\
No\
\
## Open API 이용약관\
\
본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.\
\
제 1조 (목적)\
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.\
\
제 2조 (정의)\
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.\
\
2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.\
\
3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.\
\
제 3조 (면책사항)\
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.\
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.\
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.\
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.\
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.\
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.\
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.\
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.\
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.\
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.\
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.\
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.\
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.\
\
제 4조 (Open API 서비스 제공의 제한 및 해지)\
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.\
1\. 본 이용약관 제6조를 위반한 경우\
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우\
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우\
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우\
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우\
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.\
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.\
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.\
\
제 5조 (저작권)\
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.\
\
제 6조 (사용자의 의무와 책임)\
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.\
1\. API 업데이트 및 변경 사항에 대한 공지\
2\. 제도 변경 공지\
3\. 두나무-업비트 정책 반영에 따른 공지\
4\. 기타 긴급 공지\
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.\
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.\
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.\
\
제 7조 (약관의 변경 등)\
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.\
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).\
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.\
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.\
\
제 8조 (효력 발생 및 유효기간)\
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.\
\
제 9조 (기타)\
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.\
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.\
\
제 10조 (관할법원)\
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.\
\
<부칙>\
본 이용약관은 2024년 10월 30일부터 적용됩니다.\
이전의 이용약관은 아래에서 확인하실 수 있습니다.\
\
\
[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)\
\
[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)\
\
[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)\
\
[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)\
\
동의

[docs_upbit_com_kr_reference__ED_98_B8_EA_B0_80__EC_A0_95_EB_B3_B4__EC_A1_B0_ED_9A_8C.md]
> ## 📘  v1.4.4 호가 모아보기 기능 추가 (원화마켓만 지원)
>
> v1.4.4 부터 `level` 항목을 통해 호가 모아보기를 지원합니다.
>
> 지원하는 전체 단위는 아래와 같으며 **각 종목별 호가 단위에 따라 지원하는 단위가 다릅니다.**
>
> **\*종목별로 지원하는 모아보기 단위는 [v1/orderbook/supported\_levels 에서 확인](https://docs.upbit.com/kr/reference/supported_levels) 하실 수 있습니다.**
>
> 해당 종목에서 지원하지 않는 `level` 단위를 넣을 경우 **빈 리스트가 내려가니 주의** 해주세요
>
> ```rdmd-code lang- theme-light
> - 100000000
> - 10000000
> - 1000000
> - 100000
> - 10000
> - 1000
> - 100
> - 10
> - 1
> - 0
> - 0.1
> - 0.01
> - 0.001
> - 0.0001
> - 0.00001
> - 0.000001
> - 0.0000001
>
> ```

## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%ED%98%B8%EA%B0%80-%EC%A0%95%EB%B3%B4-%EC%A1%B0%ED%9A%8C\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| markets \* | 반점으로 구분되는 마켓 코드 (ex. KRW-BTC, BTC-ETH) | String |
| level | 호가 모아보기 단위 (0인 경우 기본 호가 단위. 해당 기능은 원화마켓(KRW)에서만 지원) | Double |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%ED%98%B8%EA%B0%80-%EC%A0%95%EB%B3%B4-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 종목 코드 | String |
| timestamp | 호가 생성 시각 | Long |
| total\_ask\_size | 호가 매도 총 잔량 | Double |
| total\_bid\_size | 호가 매수 총 잔량 | Double |
| orderbook\_units | 호가 | List of Objects |
| ask\_price | 매도 호가 | Double |
| bid\_price | 매수 호가 | Double |
| ask\_size | 매도 잔량 | Double |
| bid\_size | 매수 잔량 | Double |
| level | 호가 모아보기 단위 (default: 0, 기본 호가단위)<br>\*호가 모아보기 기능은 원화마켓(KRW)에서만 지원하므로 BTC, USDT 마켓의 경우 0만 존재합니다.<br>\*종목별 지원하는 모아보기 단위는 [v1/orderbook/supported\_levels 에서 확인](https://docs.upbit.com/kr/reference/supported_levels) 하실 수 있습니다. | Double |

`orderbook_unit ` 리스트에는 30호가 정보가 들어가며 차례대로 1호가, 2호가 ... 30호가의 정보를 담고 있습니다.

markets

string

required

반점으로 구분되는 종목 코드 (ex. KRW-BTC, BTC-ETH)

level

double

호가 모아보기 단위 (0인 경우 기본 호가 단위. 해당 기능은 원화마켓(KRW)에서만 지원)

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

level

integer

Defaults to 0

# `` 4XX      4XX

json

Updated 3 days ago

* * *

Did this page help you?

Yes

No

ShellPythonNode

```

xxxxxxxxxx

1curl -X GET "https://api.upbit.com/v1/orderbook?level=0&markets=KRW-BTC" -H "accept: */*"

```

```

xxxxxxxxxx

101
]

1

[\
\
2\
\
  {\
\
3    "market": "KRW-BTC",\
\
4    "timestamp": 1720597558776,\
\
5    "total_ask_size": 1.20339227,\
\
6    "total_bid_size": 1.08861101,\
\
7\
\
    "orderbook_units": [\
\
8\
\
      {\
\
9        "ask_price": 83186000,\
\
10        "bid_price": 83184000,\
\
11        "ask_size": 0.02565269,\
\
12        "bid_size": 0.07744926\
\
13      },\
\
14\
\
      {\
\
15        "ask_price": 83206000,\
\
16        "bid_price": 83182000,\
\
17        "ask_size": 0.02656392,\
\
18        "bid_size": 0.51562837\
\
19      },\
\
20\
\
      {\
\
21        "ask_price": 83207000,\
\
22        "bid_price": 83181000,\
\
23        "ask_size": 0.00172255,\
\
24        "bid_size": 0.00173694\
\
25      },\
\
```\
\
Updated 3 days ago\
\
* * *\
\
Did this page help you?\
\
Yes\
\
No\
\
## Open API 이용약관\
\
본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.\
\
제 1조 (목적)\
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.\
\
제 2조 (정의)\
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.\
\
2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.\
\
3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.\
\
제 3조 (면책사항)\
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.\
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.\
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.\
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.\
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.\
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.\
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.\
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.\
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.\
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.\
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.\
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.\
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.\
\
제 4조 (Open API 서비스 제공의 제한 및 해지)\
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.\
1\. 본 이용약관 제6조를 위반한 경우\
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우\
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우\
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우\
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우\
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.\
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.\
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.\
\
제 5조 (저작권)\
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.\
\
제 6조 (사용자의 의무와 책임)\
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.\
1\. API 업데이트 및 변경 사항에 대한 공지\
2\. 제도 변경 공지\
3\. 두나무-업비트 정책 반영에 따른 공지\
4\. 기타 긴급 공지\
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.\
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.\
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.\
\
제 7조 (약관의 변경 등)\
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.\
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).\
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.\
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.\
\
제 8조 (효력 발생 및 유효기간)\
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.\
\
제 9조 (기타)\
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.\
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.\
\
제 10조 (관할법원)\
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.\
\
<부칙>\
본 이용약관은 2024년 10월 30일부터 적용됩니다.\
이전의 이용약관은 아래에서 확인하실 수 있습니다.\
\
\
[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)\
\
[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)\
\
[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)\
\
[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)\
\
동의

[docs_upbit_com_kr_reference_authentication.md]
앞서 "기본 정보"에서 확인한것과 같이 웹소켓은 Public 데이터와 Private 데이터로 나누어져있습니다. Public 데이터를 수신하기 위해서는 별다른 인증이 필요 없습니다. Private 데이터를 수신하기 위해서는 Websocket 연결 시 인증에 성공해야합니다.

- REST API 에서와 동일하게 `Authorization` 헤더를 통해 인증을 진행합니다.
- [인증 가능한 요청 만들기](https://docs.upbit.com/kr/docs/create-authorization-request) 의 "JWT 인증 토큰 만들기" 를 참고하시기 바랍니다.

## (예시) Header 에 인증 정보를 담아 Websocket 연결   [Skip link to (예시) Header 에 인증 정보를 담아 Websocket 연결](https://docs.upbit.com/kr/reference/authentication\#%EC%98%88%EC%8B%9C-header-%EC%97%90-%EC%9D%B8%EC%A6%9D-%EC%A0%95%EB%B3%B4%EB%A5%BC-%EB%8B%B4%EC%95%84-websocket-%EC%97%B0%EA%B2%B0)

NodePython

```rdmd-code lang-javascript theme-light

const jwt = require("jsonwebtoken");
const {v4: uuidv4} = require('uuid');
const WebSocket = require("ws");

const payload = {
    access_key: "발급받은 Access key",
    nonce: uuidv4(),
};

const jwtToken = jwt.sign(payload, "발급받은 Secret key");

const ws = new WebSocket("wss://api.upbit.com/websocket/v1/private", {
    headers: {
        authorization: `Bearer ${jwtToken}`
    }
});

ws.on("open", () => {
    console.log("connected!");
    // Request after connection
    ws.send('[{"ticket":"test example"},{"type":"myOrder"}]');

});

ws.on("error", console.error);

ws.on("message", (data) => console.log(data.toString()));

ws.on("close", () => console.log("closed!"));

```

```rdmd-code lang-python theme-light

import jwt  # PyJWT
import uuid
import websocket  # websocket-client

def on_message(ws, message):
    # do something
    data = message.decode('utf-8')
    print(data)

def on_connect(ws):
    print("connected!")
    # Request after connection
    ws.send('[{"ticket":"test example"},{"type":"myOrder"}]')

def on_error(ws, err):
    print(err)

def on_close(ws, status_code, msg):
    print("closed!")

payload = {
    'access_key': "발급받은 Access key",
    'nonce': str(uuid.uuid4()),
}

jwt_token = jwt.encode(payload, "발급받은 Secret key");
authorization_token = 'Bearer {}'.format(jwt_token)
headers = {"Authorization": authorization_token}

ws_app = websocket.WebSocketApp("wss://api.upbit.com/websocket/v1/private",
                                header=headers,
                                on_message=on_message,
                                on_open=on_connect,
                                on_error=on_error,
                                on_close=on_close)
ws_app.run_forever()

```

Updated 6 months ago

* * *

Did this page help you?

Yes

No

Updated 6 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EC_B5_9C_EA_B7_BC__EC_B2_B4_EA_B2_B0__EB_82_B4_EC_97_AD.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EC%B5%9C%EA%B7%BC-%EC%B2%B4%EA%B2%B0-%EB%82%B4%EC%97%AD\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market \* | 종목 코드 (ex. KRW-BTC) | String |
| to | 마지막 체결 시각. 형식 : `[HHmmss 또는 HH:mm:ss]`. 비워서 요청시 가장 최근 데이터 | String |
| count | 체결 개수 | Integer |
| cursor | 페이지네이션 커서 (sequential\_id) | String |
| days\_ago | 최근 체결 날짜 기준 7일 이내의 이전 데이터 조회 가능. 비워서 요청 시 가장 최근 체결 날짜 반환. (범위: 1 ~ 7)) | Integer |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EC%B5%9C%EA%B7%BC-%EC%B2%B4%EA%B2%B0-%EB%82%B4%EC%97%AD\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 종목 코드 | String |
| trade\_date\_utc | 체결 일자(UTC 기준)<br>포맷: `yyyy-MM-dd` | String |
| trade\_time\_utc | 체결 시각(UTC 기준)<br>포맷: `HH:mm:ss` | String |
| timestamp | 체결 타임스탬프 | Long |
| trade\_price | 체결 가격 | Double |
| trade\_volume | 체결량 | Double |
| prev\_closing\_price | 전일 종가(UTC 0시 기준) | Double |
| change\_price | 변화량 | Double |
| ask\_bid | 매도/매수 | String |
| sequential\_id | 체결 번호(Unique) | Long |

- `sequential_id` 필드는 체결의 유일성 판단을 위한 근거로 쓰일 수 있습니다. 하지만 체결의 순서를 보장하지는 못합니다.

market

string

required

종목 코드 (ex. KRW-BTC)

to

string

마지막 체결 시각. 형식 : `[HHmmss 또는 HH:mm:ss]`. 비워서 요청시 가장 최근 데이터

count

int32

체결 개수

cursor

string

페이지네이션 커서 (sequential\_id)

days\_ago

int32

최근 체결 날짜 기준 7일 이내의 이전 데이터 조회 가능. 비워서 요청 시 가장 최근 체결 날짜 반환. (범위: 1 ~ 7))

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

change\_price

integer

Defaults to 0

ask\_bid

string

sequential\_id

integer

Defaults to 0

# `` 400      400

object

Updated 7 months ago

* * *

Did this page help you?

Yes

No

ShellNodeRubyPHPPython

```

xxxxxxxxxx

1curl --request GET \

2     --url https://api.upbit.com/v1/trades/ticks \

3     --header 'accept: application/json'

```

```

xxxxxxxxxx

14



1

[\
\
2\
\
  {\
\
3    "market": "KRW-BTC",\
\
4    "trade_date_utc": "2018-04-18",\
\
5    "trade_time_utc": "10:19:58",\
\
6    "timestamp": 1524046798000,\
\
7    "trade_price": 8616000,\
\
8    "trade_volume": 0.03060688,\
\
9    "prev_closing_price": 8450000,\
\
10    "change_price": 166000,\
\
11    "ask_bid": "ASK",\
\
12    "sequential_id": 15240467980000022\
\
13  }\
\
14]

```

Updated 7 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference_websocket_orderbook.md]
# Request   [Skip link to Request](https://docs.upbit.com/kr/reference/websocket-orderbook\#request)

요청은 JSON Object를 이용하며 응답 또한 JSON Object 입니다. 요청은 크게 ticket field, type field, format field 로 나누어지며 하나의 요청에 여러 개의 type field 를 명시할 수 있습니다. ticket field 와 format field 에 대해서는 [요청 방법 및 포맷](https://docs.upbit.com/kr/reference/websocket-request-format) 을 참고해주시기 바랍니다.

> ## 📘  Request format
>
> **\[{Ticket Field},{Type Field},....,{Type Field},{Format Field}\]**

### **Type Field**   [Skip link to [object Object]](https://docs.upbit.com/kr/reference/websocket-orderbook\#type-field)

수신하고 싶은 시세 정보를 나열하는 필드입니다.

is\_only\_snapshot, is\_only\_realtime 필드는 생략 가능하며 모두 생략시 스냅샷과 실시간 데이터 모두를 수신합니다.

| 필드명 | 타입 | 내용 | 필수 여부 | 기본 값 |
| --- | --- | --- | --- | --- |
| type | String | 데이터 타입<br>- `orderbook`: 호가 | O |  |
| codes | List | 마켓 코드 리스트<br>\*대문자로 요청해야 합니다. | O |  |
| level | Double | 모아보기 단위 | X |  |
| is\_only\_snapshot | Boolean | 스냅샷 시세만 제공 | X | false |
| is\_only\_realtime | Boolean | 실시간 시세만 제공 | X | false |

> ## 📘  v1.4.4 호가 모아보기 기능 추가 (원화마켓만 지원)
>
> v1.4.4 부터 `level` 항목을 통해 호가 모아보기를 지원합니다.
>
> 지원하는 전체 단위는 아래와 같으며 **각 종목별 호가 단위에 따라 지원하는 단위가 다릅니다.**
>
> **\*종목별로 지원하는 모아보기 단위는 [v1/orderbook/supported\_levels 에서 확인](https://docs.upbit.com/kr/reference/supported_levels) 하실 수 있습니다.**
>
> 해당 종목에서 지원하지 않는 `level` 단위를 넣을 경우 수신받으실 데이터가 없으니 주의해주세요
>
> ```rdmd-code lang- theme-light
> - 100000000
> - 10000000
> - 1000000
> - 100000
> - 10000
> - 1000
> - 100
> - 10
> - 1
> - 0
> - 0.1
> - 0.01
> - 0.001
> - 0.0001
> - 0.00001
> - 0.000001
> - 0.0000001
>
> ```

> ## 📘  v1.1.0 Orderbook Unit 갯수 커스텀 수신기능 추가
>
> v1.1.0 부터 orderbook 타입의 패킷에 한하여 Orderbook Unit의 갯수를 최대 제공 갯수 (30개) 안에서 원하는 만큼 조절하여 호출 가능합니다. 기존의 `codes` 항목에 시세 종목과 원하는 Unit 갯수를 넣어주시면 됩니다.
>
> 형식: `{code}.{count}`
>
> ex) "KRW-BTC.5", "BTC-XRP.3"

# Response   [Skip link to Response](https://docs.upbit.com/kr/reference/websocket-orderbook\#response)

| 필드명 | 축약형 (format: SIMPLE) | 내용 | 타입 | 값 |
| --- | --- | --- | --- | --- |
| type | ty | 타입 | String | `orderbook` : 호가 |
| code | cd | 마켓 코드 (ex. KRW-BTC) | String |  |
| total\_ask\_size | tas | 호가 매도 총 잔량 | Double |  |
| total\_bid\_size | tbs | 호가 매수 총 잔량 | Double |  |
| orderbook\_units | obu | 호가 | List of Objects |  |
| orderbook\_units.ask\_price | obu.ap | 매도 호가 | Double |  |
| orderbook\_units.bid\_price | obu.bp | 매수 호가 | Double |  |
| orderbook\_units.ask\_size | obu.as | 매도 잔량 | Double |  |
| orderbook\_units.bid\_size | obu.bs | 매수 잔량 | Double |  |
| timestamp | tms | 타임스탬프 (millisecond) | Long |  |
| level | lv | 호가 모아보기 단위 (default: 0, 기본 호가단위)<br>\*호가 모아보기 기능은 원화마켓(KRW)에서만 지원하므로 BTC, USDT 마켓의 경우 0만 존재합니다.<br>\*종목별 지원하는 모아보기 단위는 [v1/orderbook/supported\_levels 에서 확인](https://docs.upbit.com/kr/reference/supported_levels) 하실 수 있습니다. | Double | 모아보기 단위 |

# Example   [Skip link to Example](https://docs.upbit.com/kr/reference/websocket-orderbook\#example)

### Request   [Skip link to Request](https://docs.upbit.com/kr/reference/websocket-orderbook\#request-1)

`level` 값은 필수가 아니며, 제외될 경우 DEFUALT(0), 기본 호가단위로 내려갑니다.

JSON

```rdmd-code lang-json theme-light

[\
  {\
    "ticket": "test"\
  },\
  {\
    "type": "orderbook",\
    "codes": [\
      "KRW-BTC",\
      "KRW-ETH.3"\
    ],\
    "level": 10000\
  },\
  {\
    "format": "DEFAULT"\
  }\
]

```

종목별로 각기다른 모아보기 `level` 값을 지정하기 위해서는 아래와 같이 요청할 수 있습니다.

JSON

```rdmd-code lang-json theme-light

[\
    {\
        "ticket": "test"\
    },\
    {\
        "type": "orderbook",\
        "codes": [\
            "KRW-BTC"\
        ],\
        "level": 10000\
    },\
    {\
        "type": "orderbook",\
        "codes": [\
            "KRW-BTT"\
        ],\
        "level": 0\
    },\
    {\
        "format": "DEFAULT"\
    }\
]

```

### Response   [Skip link to Response](https://docs.upbit.com/kr/reference/websocket-orderbook\#response-1)

JSON

```rdmd-code lang-json theme-light

{
  "type": "orderbook",
  "code": "KRW-BTC",
  "timestamp": 1746601573804,
  "total_ask_size": 4.79158413,
  "total_bid_size": 2.65609625,
  "orderbook_units": [\
    {\
      "ask_price": 137002000,\
      "bid_price": 137001000,\
      "ask_size": 0.10623869,\
      "bid_size": 0.03656812\
    },\
    {\
      "ask_price": 137023000,\
      "bid_price": 137000000,\
      "ask_size": 0.06144079,\
      "bid_size": 0.33543284\
    },\
    {\
      "ask_price": 137050000,\
      "bid_price": 136999000,\
      "ask_size": 0.0055433,\
      "bid_size": 0.00104379\
    },\
    {\
      "ask_price": 137052000,\
      "bid_price": 136980000,\
      "ask_size": 0.00452071,\
      "bid_size": 0.32709281\
    },\
    {\
      "ask_price": 137053000,\
      "bid_price": 136978000,\
      "ask_size": 0.12781487,\
      "bid_size": 0.00875219\
    },\
    {\
      "ask_price": 137054000,\
      "bid_price": 136976000,\
      "ask_size": 0.03777519,\
      "bid_size": 0.01867952\
    },\
    {\
      "ask_price": 137055000,\
      "bid_price": 136975000,\
      "ask_size": 0.06073315,\
      "bid_size": 0.04379996\
    },\
    {\
      "ask_price": 137056000,\
      "bid_price": 136971000,\
      "ask_size": 0.00372511,\
      "bid_size": 0.00036504\
    },\
    {\
      "ask_price": 137060000,\
      "bid_price": 136970000,\
      "ask_size": 0.00308733,\
      "bid_size": 0.15547631\
    },\
    {\
      "ask_price": 137065000,\
      "bid_price": 136969000,\
      "ask_size": 0.04218546,\
      "bid_size": 0.00036504\
    },\
    {\
      "ask_price": 137070000,\
      "bid_price": 136942000,\
      "ask_size": 0.01172394,\
      "bid_size": 0.00021907\
    },\
    {\
      "ask_price": 137071000,\
      "bid_price": 136931000,\
      "ask_size": 0.001,\
      "bid_size": 0.00260654\
    },\
    {\
      "ask_price": 137076000,\
      "bid_price": 136930000,\
      "ask_size": 0.00120371,\
      "bid_size": 0.00014606\
    },\
    {\
      "ask_price": 137079000,\
      "bid_price": 136924000,\
      "ask_size": 0.00007303,\
      "bid_size": 0.00004381\
    },\
    {\
      "ask_price": 137080000,\
      "bid_price": 136911000,\
      "ask_size": 0.01051428,\
      "bid_size": 0.09531\
    },\
    {\
      "ask_price": 137084000,\
      "bid_price": 136910000,\
      "ask_size": 0.00004,\
      "bid_size": 0.01354743\
    },\
    {\
      "ask_price": 137086000,\
      "bid_price": 136906000,\
      "ask_size": 0.00643152,\
      "bid_size": 0.00519774\
    },\
    {\
      "ask_price": 137091000,\
      "bid_price": 136902000,\
      "ask_size": 0.0105,\
      "bid_size": 0.00485\
    },\
    {\
      "ask_price": 137098000,\
      "bid_price": 136898000,\
      "ask_size": 4.0534502,\
      "bid_size": 0.01017513\
    },\
    {\
      "ask_price": 137099000,\
      "bid_price": 136897000,\
      "ask_size": 0.00995,\
      "bid_size": 0.0002599\
    },\
    {\
      "ask_price": 137100000,\
      "bid_price": 136895000,\
      "ask_size": 0.14272057,\
      "bid_size": 0.01245\
    },\
    {\
      "ask_price": 137104000,\
      "bid_price": 136893000,\
      "ask_size": 0.0012294,\
      "bid_size": 0.01468299\
    },\
    {\
      "ask_price": 137109000,\
      "bid_price": 136892000,\
      "ask_size": 0.009,\
      "bid_size": 0.0042\
    },\
    {\
      "ask_price": 137112000,\
      "bid_price": 136890000,\
      "ask_size": 0.03154608,\
      "bid_size": 0.00385\
    },\
    {\
      "ask_price": 137113000,\
      "bid_price": 136881000,\
      "ask_size": 0.00136546,\
      "bid_size": 0.00080361\
    },\
    {\
      "ask_price": 137120000,\
      "bid_price": 136880000,\
      "ask_size": 0.00325241,\
      "bid_size": 0.01460539\
    },\
    {\
      "ask_price": 137123000,\
      "bid_price": 136879000,\
      "ask_size": 0.02020901,\
      "bid_size": 1.203\
    },\
    {\
      "ask_price": 137124000,\
      "bid_price": 136874000,\
      "ask_size": 0.00734507,\
      "bid_size": 0.00791911\
    },\
    {\
      "ask_price": 137135000,\
      "bid_price": 136868000,\
      "ask_size": 0.0002192,\
      "bid_size": 0.01735219\
    },\
    {\
      "ask_price": 137137000,\
      "bid_price": 136861000,\
      "ask_size": 0.01674565,\
      "bid_size": 0.31730166\
    }\
  ],
  "stream_type": "SNAPSHOT",
  "level": 0
}

```

Updated 3 days ago

* * *

Did this page help you?

Yes

No

Updated 3 days ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EA_B0_9C_EB_B3_84__EC_B6_9C_EA_B8_88__EC_A1_B0_ED_9A_8C.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EA%B0%9C%EB%B3%84-%EC%B6%9C%EA%B8%88-%EC%A1%B0%ED%9A%8C\#request-parameters)

| Name | 설명 | 타입 |
| --- | --- | --- |
| uuid | 출금 UUID | String |
| txid | 출금 TXID | String |
| currency | Currency 코드 | String |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EA%B0%9C%EB%B3%84-%EC%B6%9C%EA%B8%88-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| type | 입출금 종류 | String |
| uuid | 출금의 고유 아이디 | String |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| net\_type | 출금 네트워크 | String |
| txid | 출금의 트랜잭션 아이디 | String |
| state | 출금 상태<br>\- `WAITING` : 대기중<br>\- `PROCESSING` : 진행중<br>\- `DONE` : 완료<br>\- `FAILED` : 실패<br>\- `CANCELLED` : 취소됨<br>\- `REJECTED` : 거절됨 | String |
| created\_at | 출금 생성 시간 | DateString |
| done\_at | 출금 완료 시간 | DateString |
| amount | 출금 금액/수량 | NumberString |
| fee | 출금 수수료 | NumberString |
| transaction\_type | 출금 유형<br>_`default` : 일반출금_ `internal` : 바로출금 | String |

uuid

string

출금 UUID

txid

string

출금 TXID

currency

string

Currency 코드

Authorization

string

Authorization (JWT)

# `` 200      200

object

type

string

uuid

string

currency

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

# `` 4XX      4XX

object

error

object

name

string

message

string

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

39

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const queryEncode = require("querystring").encode

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11

const body = {

12    uuid: '9f432943-54e0-40b7-825f-b6fec8b42b79'

13}

14​

15const query = queryEncode(body)

16​

17const hash = crypto.createHash('sha512')

18const queryHash = hash.update(query, 'utf-8').digest('hex')

19​

20

const payload = {

21    access_key: access_key,

22    nonce: uuidv4(),

23    query_hash: queryHash,

24    query_hash_alg: 'SHA512',

25}

26​

```

```

xxxxxxxxxx

12



1

{

2  "type": "withdraw",

3  "uuid": "9f432943-54e0-40b7-825f-b6fec8b42b79",

4  "currency": "BTC",

5  "txid": null,

6  "state": "processing",

7  "created_at": "2018-04-13T11:24:01+09:00",

8  "done_at": null,

9  "amount": "0.01",

10  "fee": "0.0",

11  "transaction_type": "default"

12}

```

Updated 3 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__ED_8A_B8_EB_9E_98_EB_B8_94_EB_A3_B0__EA_B0_80_EB_8A_A5__EA_B1_B0_EB_9E_98_EC_86_8C.md]
> ## 📘
>
> - [계정주 확인 서비스에 대한 자세한 내용은 링크를 참고해 주세요](https://upbitcs.zendesk.com/hc/ko/articles/5127318107033-%EA%B3%84%EC%A0%95%EC%A3%BC-%ED%99%95%EC%9D%B8-%EC%84%9C%EB%B9%84%EC%8A%A4%EA%B0%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80%EC%9A%94)
> - 해당 리스트는 [입출금 가능 가상자산사업자 리스트](https://upbitcs.zendesk.com/hc/ko/articles/5048002559897-%EC%9E%85%EC%B6%9C%EA%B8%88-%EA%B0%80%EB%8A%A5-%EA%B0%80%EC%83%81%EC%9E%90%EC%82%B0%EC%82%AC%EC%97%85%EC%9E%90-%EB%A6%AC%EC%8A%A4%ED%8A%B8) 의 '계정주 확인 서비스 연동 VASP' 내용을 반영합니다

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%ED%8A%B8%EB%9E%98%EB%B8%94%EB%A3%B0-%EA%B0%80%EB%8A%A5-%EA%B1%B0%EB%9E%98%EC%86%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| vasp\_name | 거래소 이름 | String |
| vasp\_uuid | 거래소의 고유 식별자 | String |
| depositable | 입금 가능 여부 | Boolean |
| withdrawable | 출금 가능 여부 | Boolean |

Authorization

string

required

Authorization token (JWT)

# `` 200      200

object

name

string

uuid

string

depositable

boolean

Defaults to true

withdrawable

boolean

Defaults to true

# `` 4XX      4XX

object

error

object

name

string

message

string

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

25

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const sign = require('jsonwebtoken').sign

4​

5const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

6const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

7const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

8​

9

const payload = {

10    access_key: access_key,

11    nonce: uuidv4(),

12}

13​

14const token = sign(payload, secret_key)

15​

16

const options = {

17    method: "GET",

18    url: server_url + "/v1/travel_rule/vasps",

19    headers: {Authorization: `Bearer ${token}`},

20}

21​

22

request(options, (error, response, body) => {

23    if (error) throw new Error(error)

24    console.log(body)

25})

```

```

xxxxxxxxxx



1

{

2  "name": "업비트",

3  "uuid": "00000000-0000-0000-0000-000000000000",

4  "depositable": true,

5  "withdrawable": true

6}

```

Updated 3 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EC_A0_84_EC_B2_B4__EA_B3_84_EC_A2_8C__EC_A1_B0_ED_9A_8C.md]
## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EC%A0%84%EC%B2%B4-%EA%B3%84%EC%A2%8C-%EC%A1%B0%ED%9A%8C\#response)

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

json

# `` 4XX      4XX

object

error

object

name

string

message

string

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

25

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const sign = require('jsonwebtoken').sign

4​

5const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

6const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

7const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

8​

9

const payload = {

10    access_key: access_key,

11    nonce: uuidv4(),

12}

13​

14const token = sign(payload, secret_key)

15​

16

const options = {

17    method: "GET",

18    url: server_url + "/v1/accounts",

19    headers: {Authorization: `Bearer ${token}`},

20}

21​

22

request(options, (error, response, body) => {

23    if (error) throw new Error(error)

24    console.log(body)

25})

```

```

xxxxxxxxxx

18



1

[\
\
2\
\
  {\
\
3    "currency":"KRW",\
\
4    "balance":"1000000.0",\
\
5    "locked":"0.0",\
\
6    "avg_buy_price":"0",\
\
7    "avg_buy_price_modified":false,\
\
8    "unit_currency": "KRW",\
\
9  },\
\
10\
\
  {\
\
11    "currency":"BTC",\
\
12    "balance":"2.0",\
\
13    "locked":"0.0",\
\
14    "avg_buy_price":"101000",\
\
15    "avg_buy_price_modified":false,\
\
16    "unit_currency": "KRW",\
\
17  }\
\
18]

```

Updated 3 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EC_9B_90_ED_99_94__EC_9E_85_EA_B8_88_ED_95_98_EA_B8_B0.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EC%9B%90%ED%99%94-%EC%9E%85%EA%B8%88%ED%95%98%EA%B8%B0\#request-parameters)

> ## ❗️  v1.4.1 업데이트 : two\_factor\_type 필수 지정 필요 & 2채널 인증 '카카오 페이 인증' 종료 및 '카카오톡 인증' 신규지원 (적용 완료)
>
> - 11월 20일 이후 2채널 인증 수단 타입으로 `kakao` 가 추가되었습니다.
> - 12월 18일 이후, `two_factor_type` 필드는 **디폴트 값이 없는 필수 필드가 되므로 원화 입금 요청 시 `two_factor_type` 값을 반드시 지정하여 요청** 해주셔야 합니다.
> - 12월 18일 이후 **2채널 인증 수단 타입으로 `kakao_pay` 를 더이상 사용하실 수 없습니다.**
>
> 자세한 변경사항은 [공지사항](https://docs.upbit.com/kr/changelog/kakao_auth) 을 참조해주세요.

| Name | 설명 | 타입 |
| --- | --- | --- |
| amount \* | 입금액 | Number |
| two\_factor\_type \* | 2차 인증 수단 | `kakao`: 카카오 인증<br>`naver` : 네이버 인증<br>`hana` : 하나인증서 인증 |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EC%9B%90%ED%99%94-%EC%9E%85%EA%B8%88%ED%95%98%EA%B8%B0\#response)

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
| transaction\_type | 입금 유형<br>_`default` : 일반출금_ `internal` : 바로출금 | String |

amount

string

required

입금 원화 수량

two\_factor\_type

string

required

2차 인증 수단 (kakao, naver, hana)

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

# `` 4XX      4XX

object

error

object

name

string

message

string

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

40

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const queryEncode = require("querystring").encode

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11

const body = {

12    amount: '10000',

13    two_factor_type: 'naver'

14}

15​

16const query = queryEncode(body)

17​

18const hash = crypto.createHash('sha512')

19const queryHash = hash.update(query, 'utf-8').digest('hex')

20​

21

const payload = {

22    access_key: access_key,

23    nonce: uuidv4(),

24    query_hash: queryHash,

25    query_hash_alg: 'SHA512',

26}

```

```

xxxxxxxxxx

12



1

{

2  "type": "deposit",

3  "uuid": "9f432943-54e0-40b7-825f-b6fec8b42b79",

4  "currency": "KRW",

5  "txid": "ebe6937b-130e-4066-8ac6-4b0e67f28adc",

6  "state": "processing",

7  "created_at": "2018-04-13T11:24:01+09:00",

8  "done_at": null,

9  "amount": "10000",

10  "fee": "0.0",

11  "transaction_type": "default"

12}

```

Updated 3 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EC_A3_BC_EB_AC_B8__EA_B0_80_EB_8A_A5__EC_A0_95_EB_B3_B4.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EC%A3%BC%EB%AC%B8-%EA%B0%80%EB%8A%A5-%EC%A0%95%EB%B3%B4\#request-parameters)

| Name | 설명 | 타입 |
| --- | --- | --- |
| market \* | 마켓 ID | String |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EC%A3%BC%EB%AC%B8-%EA%B0%80%EB%8A%A5-%EC%A0%95%EB%B3%B4\#response)

> ## 📘  신규 주문 타입 및 조건 지원 ( [지원 마켓은 공지참고](https://docs.upbit.com/kr/changelog/new_ord_type))
>
> ‘ **ask\_types**’, ‘ **bid\_types**’ 필드의 주문 지원 방식이 추가되었습니다.
>
> - ask\_types: `limit_ioc`, `limit_fok`, `best_ioc`, `best_fok`
> - bid\_types: `limit_ioc`, `limit_fok`, `best_ioc`, `best_fok`
>
> ![](https://files.readme.io/9912934-image.png)

> ## 🚧
>
> `market.order_types` 필드는 만료되오니, Open API를 이용해 주문을 넣을 시 ' `ask_types`', ' `bid_types`' 필드를 사용하시기 바랍니다.

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| bid\_fee | 매수 수수료 비율 | NumberString |
| ask\_fee | 매도 수수료 비율 | NumberString |
| market | 마켓에 대한 정보 | Object |
| market.id | 마켓의 유일 키 | String |
| market.name | 마켓 이름 | String |
| market.order\_types | 지원 주문 방식 **(만료)** | Array\[String\] |
| ask\_types | 매도 주문 지원 방식 | Array\[String\] |
| bid\_types | 매수 주문 지원 방식 | Array\[String\] |
| market.order\_sides | 지원 주문 종류 | Array\[String\] |
| market.bid | 매수 시 제약사항 | Object |
| market.bid.currency | 화폐를 의미하는 영문 대문자 코드 | String |
| market.bid.price\_unit | 주문금액 단위 | String |
| market.bid.min\_total | 최소 매도/매수 금액 | Number |
| market.ask | 매도 시 제약사항 | Object |
| market.ask.currency | 화폐를 의미하는 영문 대문자 코드 | String |
| market.ask.price\_unit | 주문금액 단위 | String |
| market.ask.min\_total | 최소 매도/매수 금액 | Number |
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

# `` 4XX      4XX

object

error

object

name

string

message

string

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

39

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const queryEncode = require("querystring").encode

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11

const body = {

12    market: 'KRW-BTC'

13}

14​

15const query = queryEncode(body)

16​

17const hash = crypto.createHash('sha512')

18const queryHash = hash.update(query, 'utf-8').digest('hex')

19​

20

const payload = {

21    access_key: access_key,

22    nonce: uuidv4(),

23    query_hash: queryHash,

24    query_hash_alg: 'SHA512',

25}

26​

```

```

xxxxxxxxxx

59
}

1

{

2  "bid_fee": "0.0005",

3  "ask_fee": "0.0005",

4  "maker_bid_fee": "0.0005",

5  "maker_ask_fee": "0.0005",

6

  "market": {

7    "id": "KRW-BTC",

8    "name": "BTC/KRW",

9

    "order_types": [\
\
10      "limit"\
\
11    ],

12

    "order_sides": [\
\
13      "ask",\
\
14      "bid"\
\
15    ],

16

    "bid_types": [\
\
17      "best_fok",\
\
18      "best_ioc",\
\
19      "limit",\
\
20      "limit_fok",\
\
21      "limit_ioc",\
\
22      "price"\
\
23    ],

24

    "ask_types": [\
\
25      "best_fok",\
\
```\
\
Updated 3 months ago\
\
* * *\
\
Did this page help you?\
\
Yes\
\
No\
\
## Open API 이용약관\
\
본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.\
\
제 1조 (목적)\
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.\
\
제 2조 (정의)\
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.\
\
2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.\
\
3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.\
\
제 3조 (면책사항)\
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.\
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.\
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.\
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.\
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.\
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.\
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.\
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.\
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.\
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.\
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.\
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.\
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.\
\
제 4조 (Open API 서비스 제공의 제한 및 해지)\
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.\
1\. 본 이용약관 제6조를 위반한 경우\
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우\
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우\
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우\
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우\
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.\
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.\
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.\
\
제 5조 (저작권)\
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.\
\
제 6조 (사용자의 의무와 책임)\
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.\
1\. API 업데이트 및 변경 사항에 대한 공지\
2\. 제도 변경 공지\
3\. 두나무-업비트 정책 반영에 따른 공지\
4\. 기타 긴급 공지\
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.\
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.\
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.\
\
제 7조 (약관의 변경 등)\
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.\
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).\
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.\
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.\
\
제 8조 (효력 발생 및 유효기간)\
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.\
\
제 9조 (기타)\
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.\
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.\
\
제 10조 (관할법원)\
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.\
\
<부칙>\
본 이용약관은 2024년 10월 30일부터 적용됩니다.\
이전의 이용약관은 아래에서 확인하실 수 있습니다.\
\
\
[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)\
\
[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)\
\
[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)\
\
[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)\
\
동의

[docs_upbit_com_kr_reference__EA_B0_9C_EB_B3_84__EC_A3_BC_EB_AC_B8__EC_A1_B0_ED_9A_8C.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EA%B0%9C%EB%B3%84-%EC%A3%BC%EB%AC%B8-%EC%A1%B0%ED%9A%8C\#request-parameters)

| Name | 설명 | 타입 |
| --- | --- | --- |
| uuid | 주문 UUID | String |
| identifier | 조회용 사용자 지정 값 | String |

> ## 🚧
>
> `uuid` 혹은 `identifier` 둘 중 하나의 값이 반드시 포함되어야 합니다.

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EA%B0%9C%EB%B3%84-%EC%A3%BC%EB%AC%B8-%EC%A1%B0%ED%9A%8C\#response)

> ## 📘  신규 주문 타입 및 조건 지원 ( [지원 마켓은 공지참고](https://docs.upbit.com/kr/changelog/new_ord_type))
>
> - 신규 주문 타입이 추가되었습니다: 최유리 지정가 (ord\_type 필드에 `best` 타입 추가)
>
> - 신규 주문 조건이 추가 되었습니다: IOC (Immediate or Cancel), FOK (Fill or Kill)
>   - time\_in\_force 필드가 신규로 추가되며, 가능한 타입은 `ioc` 와 `fok` 입니다.
>
> ![](https://files.readme.io/9912934-image.png)

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
| time\_in\_force | IOC, FOK 설정 | String |
| identifier | 조회용 사용자 지정값<br>\*identifier 필드는 2024-10-18 이후에 생성된 주문에 대해서만 제공합니다. | String |

uuid

string

주문 UUID

identifier

string

조회용 사용자 지정 값

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

# `` 4XX      4XX

object

error

object

name

string

message

string

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

39

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const queryEncode = require("querystring").encode

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11

const body = {

12    uuid: '9ca023a5-851b-4fec-9f0a-48cd83c2eaae'

13}

14​

15const query = queryEncode(body)

16​

17const hash = crypto.createHash('sha512')

18const queryHash = hash.update(query, 'utf-8').digest('hex')

19​

20

const payload = {

21    access_key: access_key,

22    nonce: uuidv4(),

23    query_hash: queryHash,

24    query_hash_alg: 'SHA512',

25}

26​

```

```

xxxxxxxxxx

27
}

1

{

2  "uuid": "9ca023a5-851b-4fec-9f0a-48cd83c2eaae",

3  "side": "ask",

4  "ord_type": "limit",

5  "price": "4280000.0",

6  "state": "done",

7  "market": "KRW-BTC",

8  "created_at": "2019-01-04T13:48:09+09:00",

9  "volume": "1.0",

10  "remaining_volume": "0.0",

11  "reserved_fee": "0.0",

12  "remaining_fee": "0.0",

13  "paid_fee": "2140.0",

14  "locked": "0.0",

15  "executed_volume": "1.0",

16  "trades_count": 1,

17

  "trades": [\
\
18\
\
    {\
\
19      "market": "KRW-BTC",\
\
20      "uuid": "9e8f8eba-7050-4837-8969-cfc272cbe083",\
\
21      "price": "4280000.0",\
\
22      "volume": "1.0",\
\
23      "funds": "4280000.0",\
\
24      "side": "ask"\
\
25    }\
\
```\
\
Updated 3 months ago\
\
* * *\
\
Did this page help you?\
\
Yes\
\
No\
\
## Open API 이용약관\
\
본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.\
\
제 1조 (목적)\
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.\
\
제 2조 (정의)\
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.\
\
2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.\
\
3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.\
\
제 3조 (면책사항)\
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.\
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.\
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.\
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.\
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.\
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.\
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.\
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.\
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.\
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.\
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.\
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.\
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.\
\
제 4조 (Open API 서비스 제공의 제한 및 해지)\
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.\
1\. 본 이용약관 제6조를 위반한 경우\
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우\
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우\
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우\
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우\
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.\
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.\
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.\
\
제 5조 (저작권)\
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.\
\
제 6조 (사용자의 의무와 책임)\
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.\
1\. API 업데이트 및 변경 사항에 대한 공지\
2\. 제도 변경 공지\
3\. 두나무-업비트 정책 반영에 따른 공지\
4\. 기타 긴급 공지\
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.\
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.\
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.\
\
제 7조 (약관의 변경 등)\
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.\
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).\
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.\
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.\
\
제 8조 (효력 발생 및 유효기간)\
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.\
\
제 9조 (기타)\
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.\
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.\
\
제 10조 (관할법원)\
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.\
\
<부칙>\
본 이용약관은 2024년 10월 30일부터 적용됩니다.\
이전의 이용약관은 아래에서 확인하실 수 있습니다.\
\
\
[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)\
\
[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)\
\
[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)\
\
[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)\
\
동의

[docs_upbit_com_kr_reference__ED_8A_B8_EB_9E_98_EB_B8_94_EB_A3_B0_uuid.md]
> ## 📘  1회의 요청으로 계정주 확인\*이 가능합니다. 검증에 실패한 경우, 업비트와 상대 거래소의 계정 정보 동일 여부를 다시 확인하고 요청해 주세요.
>
> - 트래블룰 정보 검증에 성공하면 입금 반영을 진행합니다.
> - 해당 입금 건이 아직 처리 중인 경우, 입금 처리가 완료된 후에 반영이 진행됩니다.
> - **동일한 입금 건**(입금 UUID, 상대 거래소 UUID 조합이 동일)에 대해서 **10분당 1회 요청**이 가능합니다.
>
> [_\*계정주 확인 서비스에 대한 자세한 내용은 링크를 참고해 주세요_](https://upbitcs.zendesk.com/hc/ko/articles/5127318107033-%EA%B3%84%EC%A0%95%EC%A3%BC-%ED%99%95%EC%9D%B8-%EC%84%9C%EB%B9%84%EC%8A%A4%EA%B0%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80%EC%9A%94)

## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%ED%8A%B8%EB%9E%98%EB%B8%94%EB%A3%B0-uuid\#request-parameters)

| Name | 설명 | 타입 |
| --- | --- | --- |
| deposit\_uuid | 입금 UUID<br>\* [입금 리스트 조회](https://docs.upbit.com/kr/reference/%EC%9E%85%EA%B8%88-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C) 에서 확인하실 수 있습니다 | String |
| vasp\_uuid \* | 상대 거래소 UUID<br>\* [계정주 확인 가능 거래소 리스트 조회](https://docs.upbit.com/kr/reference/%ED%8A%B8%EB%9E%98%EB%B8%94%EB%A3%B0-%EA%B0%80%EB%8A%A5-%EA%B1%B0%EB%9E%98%EC%86%8C) 에서 확인하실 수 있습니다 | String |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%ED%8A%B8%EB%9E%98%EB%B8%94%EB%A3%B0-uuid\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| deposit\_uuid | 입금 UUID | String |
| deposit\_state | 입금 상태 | String |
| verification\_result | 검증 결과 | String |

deposit\_uuid

string

입금 UUID

vasp\_uuid

string

required

상대 거래소 UUID

Authorization

string

required

Authorization token (JWT)

# `` 201      201

object

deposit\_uuid

string

verification\_result

string

deposit\_state

string

# `` 4XX      4XX

object

error

object

name

string

message

string

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

40

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const queryEncode = require("querystring").encode

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11

const body = {

12    deposit_uuid: '00000000-0000-0000-0000-000000000000',

13    vasp_uuid: '00000000-0000-0000-0000-000000000000',

14}

15​

16const query = queryEncode(body)

17​

18const hash = crypto.createHash('sha512')

19const queryHash = hash.update(query, 'utf-8').digest('hex')

20​

21

const payload = {

22    access_key: access_key,

23    nonce: uuidv4(),

24    query_hash: queryHash,

25    query_hash_alg: 'SHA512',

26}

```

```

xxxxxxxxxx



1

{

2  "deposit_uuid": "00000000-0000-0000-0000-000000000000",

3  "verification_result": "verified",

4  "deposit_state": "PROCESSING"

5}

```

Updated 3 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EC_A3_BC_EB_AC_B8_ED_95_98_EA_B8_B0.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EC%A3%BC%EB%AC%B8%ED%95%98%EA%B8%B0\#request-parameters)

| Name | 설명 | 타입 |
| --- | --- | --- |
| market \* | 마켓 ID (필수) | String |
| side \* | 주문 종류 (필수)<br>\- `bid` : 매수<br>\- `ask` : 매도 | String |
| volume \* | 주문량 (지정가, 시장가 매도 시 필수) | NumberString |
| price \* | 주문 가격. (지정가, 시장가 매수 시 필수)<br>ex) KRW-BTC 마켓에서 1BTC당 1,000 KRW로 거래할 경우, 값은 1000 이 된다.<br>ex) KRW-BTC 마켓에서 1BTC당 매도 1호가가 500 KRW 인 경우, 시장가 매수 시 값을 1000으로 세팅하면 2BTC가 매수된다.<br>(수수료가 존재하거나 매도 1호가의 수량에 따라 상이할 수 있음) | NumberString |
| ord\_type \* | 주문 타입 (필수)<br>\- `limit` : 지정가 주문<br>\- `price` : 시장가 주문(매수)<br>\- `market` : 시장가 주문(매도)<br>\- `best` : 최유리 주문 ( `time_in_force` 설정 필수) | String |
| identifier | 조회용 사용자 지정값 (선택) | String (Uniq 값 사용) |
| time\_in\_force | IOC, FOK 주문 설정\*<br>\- `ioc` : Immediate or Cancel<br>\- `fok` : Fill or Kill<br>\* **`ord_type` 이 `best` 혹은 `limit` 일때만 지원** 됩니다. | String |

> ## 🚧  원화 마켓 가격 단위를 확인하세요.
>
> 원화 마켓에서 주문을 요청 할 경우, [원화 마켓 주문 가격 단위](https://docs.upbit.com/kr/docs/market-info-trade-price-detail) 를 확인하여 값을 입력해주세요.

> ## 🚧  identifier 파라미터 사용
>
> `identifier` 는 서비스에서 발급하는 `uuid` 가 아닌 이용자가 직접 발급하는 키값으로, 주문을 조회하기 위해 할당하는 값입니다. 해당 값은 사용자의 전체 주문 내 유일한 값을 전달해야하며, 비록 주문 요청시 오류가 발생하더라도 같은 값으로 다시 요청을 보낼 수 없습니다.
>
> 주문의 성공 / 실패 여부와 관계없이 중복해서 들어온 `identifier` 값에서는 중복 오류가 발생하니, 매 요청시 새로운 값을 생성해주세요.

> ## 🚧  시장가 주문
>
> | 주문 설정 방법 | 시장가 |
> | --- | --- |
> | 매수 | \- ord\_type: `price`<br>\- side: `bid`<br>\- volume: `null` or 제외<br>\- price: 필수 입력 |
> | 매도 | \- ord\_type: `market`<br>\- side: `ask`<br>\- volume: 필수 입력<br>\- price: `null` or 제외 |
>
> - **시장가 주문은 `ioc`, `fok` 를 지원하지 않습니다.**

> ## 📘  신규 주문 타입 및 조건 지원 ( [전체 마켓 지원 2024\. 04. 22 ~](https://docs.upbit.com/kr/changelog/new_ord_type_expand))
>
> - 신규 주문 타입이 추가되었습니다: 최유리 지정가 (ord\_type 필드에 `best` 타입 추가)
>
> - 신규 주문 조건이 추가 되었습니다: IOC (Immediate or Cancel), FOK (Fill or Kill)
>   - time\_in\_force 필드가 신규로 추가되며, 가능한 타입은 `ioc` 와 `fok` 입니다.
>
> | 주문 설정 방법 | 지정가 (Limit) | 최유리 지정가 (Best Order) |
> | --- | --- | --- |
> | 보통 | \- ord\_type: `limit`<br>\- side: `bid` or `ask`<br>\- volume: 필수 입력<br>\- price: 필수 입력 | X |
> | IOC | \- ord\_type: `limit`<br>\- side: `bid` or `ask`<br>\- volume: 필수 입력<br>\- price: 필수 입력<br>\- time\_in\_force: `ioc` | \- ord\_type: `best`<br>\- time\_in\_force: `ioc` **\[매수 시\]**<br>\- side: `bid`<br>\- volume: `null` or 제외<br>\- price: 필수 입력 **\[매도 시\]**<br>\- side: `ask`<br>\- volume: 필수 입력<br>\- price: `null` or 제외 |
> | FOK | \- ord\_type: `limit`<br>\- side: `bid` or `ask`<br>\- volume: 필수 입력<br>\- price: 필수 입력<br>\- time\_in\_force: `fok` | \- ord\_type: `best`<br>\- time\_in\_force: `fok` **\[매수 시\]**<br>\- side: `bid`<br>\- volume: `null` or 제외<br>\- price: 필수 입력 **\[매도 시\]**<br>\- side: `ask`<br>\- volume: 필수 입력<br>\- price: `null` or 제외 |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EC%A3%BC%EB%AC%B8%ED%95%98%EA%B8%B0\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| uuid | 주문의 고유 아이디 | String |
| side | 주문 종류 | String |
| ord\_type | 주문 방식 | String |
| price | 주문 당시 화폐 가격 | NumberString |
| state | 주문 상태 | String |
| market | 마켓의 유일키 | String |
| created\_at | 주문 생성 시간 | String |
| volume | 사용자가 입력한 주문 양 | NumberString |
| remaining\_volume | 체결 후 남은 주문 양 | NumberString |
| reserved\_fee | 수수료로 예약된 비용 | NumberString |
| remaining\_fee | 남은 수수료 | NumberString |
| paid\_fee | 사용된 수수료 | NumberString |
| locked | 거래에 사용중인 비용 | NumberString |
| executed\_volume | 체결된 양 | NumberString |
| trades\_count | 해당 주문에 걸린 체결 수 | Integer |
| time\_in\_force | IOC, FOK 설정 | String |
| identifier | 조회용 사용자 지정값<br>\*identifier 필드는 2024-10-18 이후에 생성된 주문에 대해서만 제공합니다. | String |

market

string

required

Market ID

side

string

required

주문 종류

volume

string

required

주문 수량

price

string

required

유닛당 주문 가격

ord\_type

string

required

주문 타입

identifier

string

조회용 사용자 지정 값

time\_in\_force

string

IOC, FOK 주문 설정

# `` 201      201

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

# `` 4XX      4XX

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

NodePythonRubyJava

```

xxxxxxxxxx

43

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const queryEncode = require("querystring").encode

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11

const body = {

12    market: 'KRW-BTC',

13    side: 'bid',

14    volume: '0.01',

15    price: '100',

16    ord_type: 'limit',

17}

18​

19const query = queryEncode(body)

20​

21const hash = crypto.createHash('sha512')

22const queryHash = hash.update(query, 'utf-8').digest('hex')

23​

24

const payload = {

25    access_key: access_key,

26    nonce: uuidv4(),

```

```

xxxxxxxxxx

17



1

{

2  "uuid": "cdd92199-2897-4e14-9448-f923320408ad",

3  "side": "bid",

4  "ord_type": "limit",

5  "price": "100.0",

6  "state": "wait",

7  "market": "KRW-BTC",

8  "created_at": "2018-04-10T15:42:23+09:00",

9  "volume": "0.01",

10  "remaining_volume": "0.01",

11  "reserved_fee": "0.0015",

12  "remaining_fee": "0.0015",

13  "paid_fee": "0.0",

14  "locked": "1.0015",

15  "executed_volume": "0.0",

16  "trades_count": 0

17}

```

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EB_94_94_EC_A7_80_ED_84_B8_EC_9E_90_EC_82_B0__EC_9E_85_EA_B8_88__EC_A0_95_EB_B3_B4__EC_A1_B0_ED_9A_8C.md]
## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EB%94%94%EC%A7%80%ED%84%B8%EC%9E%90%EC%82%B0-%EC%9E%85%EA%B8%88-%EC%A0%95%EB%B3%B4-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| net\_type | 입금 네트워크 | String |
| is\_deposit\_possible | 입금 가능여부 | Boolean |
| deposit\_impossible\_reason | 입금 불가사유 | String |
| minimum\_deposit\_amount | 최소 입금 수량<br>\* [최소 입금 수량 미만으로 입금하시면 잔고에 반영되지 않으며 입금 취소도 불가합니다.](https://support.upbit.com/hc/ko/articles/900006890963-%EC%B5%9C%EC%86%8C-%EC%9E%85%EA%B8%88-%EC%88%98%EB%9F%89-%EB%AF%B8%EB%A7%8C%EC%9C%BC%EB%A1%9C-%EC%9E%85%EA%B8%88%ED%96%88%EC%96%B4%EC%9A%94) | Decimal |
| minimum\_deposit\_confirmations | 최소 입금 컨펌 수 | Int |
| decimal\_precision | 입금 소수점 자릿수 | Int |

> ## ❗️  디지털 자산 입금 정보 조회 데이터는 실제 서비스 상태와 다를 수 있습니다.
>
> 디지털 자산 입금 정보 조회 API에서 제공하는 입금 상태 정보는 **실제 서비스 상태 보다 수 분 정도 지연되어 반영** 될 수 있으니 오로지 참고용으로 사용하시기를 바라며 **거래 전략의 일부로 사용하지 마시기를 바랍니다.**
>
> 실제 입금을 수행하기 전에는 반드시 [업비트 공지사항](https://upbit.com/service_center/notice) 및 [입출금 현황 페이지](https://upbit.com/service_center/wallet_status) 를 참고해 주시기를 바랍니다.

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

is\_deposit\_possible

boolean

Defaults to true

deposit\_impossible\_reason

string

minimum\_deposit\_amount

integer

Defaults to 0

minimum\_deposit\_confirmations

integer

Defaults to 0

decimal\_precision

integer

Defaults to 0

# `` 4XX      4XX

object

error

object

name

string

message

string

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

40

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const queryEncode = require("querystring").encode

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11

const body = {

12    currency: 'BTC',

13    net_type: 'BTC'

14}

15​

16const query = queryEncode(body)

17​

18const hash = crypto.createHash('sha512')

19const queryHash = hash.update(query, 'utf-8').digest('hex')

20​

21

const payload = {

22    access_key: access_key,

23    nonce: uuidv4(),

24    query_hash: queryHash,

25    query_hash_alg: 'SHA512',

26}

```

```

xxxxxxxxxx



1

{

2  "currency": "BTC",

3  "net_type": "BTC",

4  "is_deposit_possible": false,

5  "deposit_impossible_reason": "네트워크 업그레이드로 인한 입출금 일시중단",

6  "minimum_deposit_amount": 0,

7  "minimum_deposit_confirmations": 1,

8  "decimal_precision": 8

9}

```

Updated 3 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference_websocket_trade.md]
# Request   [Skip link to Request](https://docs.upbit.com/kr/reference/websocket-trade\#request)

요청은 JSON Object를 이용하며 응답 또한 JSON Object 입니다. 요청은 크게 ticket field, type field, format field 로 나누어지며 하나의 요청에 여러 개의 type field 를 명시할 수 있습니다. ticket field 와 format field 에 대해서는 [요청 방법 및 포맷](https://docs.upbit.com/kr/reference/websocket-request-format) 을 참고해주시기 바랍니다.

> ## 📘  Request format
>
> **\[{Ticket Field},{Type Field},....,{Type Field},{Format Field}\]**

### **Type Field**   [Skip link to [object Object]](https://docs.upbit.com/kr/reference/websocket-trade\#type-field)

수신하고 싶은 시세 정보를 나열하는 필드입니다.

is\_only\_snapshot, is\_only\_realtime 필드는 생략 가능하며 모두 생략시 스냅샷과 실시간 데이터 모두를 수신합니다.

| 필드명 | 타입 | 내용 | 필수 여부 | 기본 값 |
| --- | --- | --- | --- | --- |
| type | String | 데이터 타입<br>- `trade`: 체결 | O |  |
| codes | List | 마켓 코드 리스트<br>\*대문자로 요청해야 합니다. | O |  |
| is\_only\_snapshot | Boolean | 스냅샷 시세만 제공 | X | false |
| is\_only\_realtime | Boolean | 실시간 시세만 제공 | X | false |

# Response   [Skip link to Response](https://docs.upbit.com/kr/reference/websocket-trade\#response)

> ## 👍  [체결시점의 1호가 정보가 추가될 예정입니다.(2024-11-27 예정)](https://docs.upbit.com/kr/changelog/best_bid_ask)
>
> `best_ask_price`, `best_ask_size`, `best_bid_price`, `best_bid_size` 를 통해 최우선 매수/매도 호가와 잔량을 확인하실 수 있습니다.

| 필드명 | 축약형 (format: SIMPLE) | 내용 | 타입 | 값 |
| --- | --- | --- | --- | --- |
| type | ty | 타입 | String | `trade` : 체결 |
| code | cd | 마켓 코드 (ex. KRW-BTC) | String |  |
| trade\_price | tp | 체결 가격 | Double |  |
| trade\_volume | tv | 체결량 | Double |  |
| ask\_bid | ab | 매수/매도 구분 | String | `ASK` : 매도<br>`BID` : 매수 |
| prev\_closing\_price | pcp | 전일 종가 | Double |  |
| change | c | 전일 대비 | String | `RISE` : 상승<br>`EVEN` : 보합<br>`FALL` : 하락 |
| change\_price | cp | 부호 없는 전일 대비 값 | Double |  |
| trade\_date | td | 체결 일자(UTC 기준) | String | yyyy-MM-dd |
| trade\_time | ttm | 체결 시각(UTC 기준) | String | HH:mm:ss |
| trade\_timestamp | ttms | 체결 타임스탬프 (millisecond) | Long |  |
| timestamp | tms | 타임스탬프 (millisecond) | Long |  |
| sequential\_id | sid | 체결 번호 (Unique) | Long |  |
| best\_ask\_price | bap | 최우선 매도 호가 | Double |  |
| best\_ask\_size | bas | 최우선 매도 잔량 | Double |  |
| best\_bid\_price | bbp | 최우선 매수 호가 | Double |  |
| best\_bid\_size | bbs | 최우선 매수 잔량 | Double |  |
| stream\_type | st | 스트림 타입 | String | `SNAPSHOT` : 스냅샷<br>`REALTIME` : 실시간 |

\* `sequential_id` 필드는 체결의 유일성 판단을 위한 근거로 쓰일 수 있습니다. 하지만 체결의 순서를 보장하지는 못합니다.

# Example   [Skip link to Example](https://docs.upbit.com/kr/reference/websocket-trade\#example)

### Request   [Skip link to Request](https://docs.upbit.com/kr/reference/websocket-trade\#request-1)

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

### Response   [Skip link to Response](https://docs.upbit.com/kr/reference/websocket-trade\#response-1)

JSON

```rdmd-code lang-json theme-light

{
  "type": "trade",
  "code": "KRW-BTC",
  "timestamp": 1730336862082,
  "trade_date": "2024-10-31",
  "trade_time": "01:07:42",
  "trade_timestamp": 1730336862047,
  "trade_price": 100473000.00000000,
  "trade_volume": 0.00014208,
  "ask_bid": "BID",
  "prev_closing_price": 100571000.00000000,
  "change": "FALL",
  "change_price": 98000.00000000,
  "sequential_id": 17303368620470000,
  "best_ask_price": 100473000,
  "best_ask_size": 0.43139478,
  "best_bid_price": 100465000,
  "best_bid_size": 0.01990656,
  "stream_type": "SNAPSHOT"
}
{
  "type": "trade",
  "code": "KRW-ETH",
  "timestamp": 1730336862120,
  "trade_date": "2024-10-31",
  "trade_time": "01:07:42",
  "trade_timestamp": 1730336862080,
  "trade_price": 3700000.00000000,
  "trade_volume": 0.02207517,
  "ask_bid": "BID",
  "prev_closing_price": 3695000.00000000,
  "change": "RISE",
  "change_price": 5000.00000000,
  "sequential_id": 17303368620800006,
  "best_ask_price": 3700000,
  "best_ask_size": 0.39101775,
  "best_bid_price": 3699000,
  "best_bid_size": 0.13499454,
  "stream_type": "SNAPSHOT"
}

```

Updated 4 months ago

* * *

Did this page help you?

Yes

No

Updated 4 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EB_8C_80_EA_B8_B0__EC_A3_BC_EB_AC_B8__EC_A1_B0_ED_9A_8C.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EB%8C%80%EA%B8%B0-%EC%A3%BC%EB%AC%B8-%EC%A1%B0%ED%9A%8C\#request-parameters)

> ## 📘  해당 API를 통해 **대기상태(open)** 인 주문을 조회할 수 있습니다.
>
> - [uuid 또는 identifiers 기준 조회](https://docs.upbit.com/kr/reference/id%EB%A1%9C-%EC%A3%BC%EB%AC%B8-%EC%A1%B0%ED%9A%8C) 가 필요시 `v1/orders/uuids` 를 이용해 주세요.
> - [종료된 주문 조회](https://docs.upbit.com/kr/reference/%EC%A2%85%EB%A3%8C-%EC%A3%BC%EB%AC%B8-%EC%A1%B0%ED%9A%8C) 필요시 `v1/orders/closed` 를 이용해 주세요.

| Name | 설명 | 타입 |
| --- | --- | --- |
| market | 마켓 ID | String |
| state | 주문 상태<br>\- `wait` : 체결 대기 **(default)**<br>\- `watch` : 예약주문 대기 | String |
| states\[\] | 주문 상태의 목록<br>\* **기본값은 `wait`** 이며, 아직 대기 상태인 예약 주문과 함께 조회하고자 하는 경우 wait, watch를 둘 다 조회해야 합니다.<br>\\* state와 states는 동시에 사용할 수 없습니다. 둘 중 하나만 지정하시기를 바랍니다. | Array\[String\] |
| page | 페이지 수, **default: 1**<br>\*페이지 당 조회건수에 대해서는 limit 파라미터로 조절할 수 있습니다. | Number |
| limit | 요청 개수, **default: 100**, max: 100 | Number |
| order\_by | 정렬 방식<br>\- `asc` : 오름차순<br>\- `desc` : 내림차순 **(default)** | String |

\*default 값에 따라, 어떤 파라미터도 명시하지 않으시면 체결 대기상태의 가장 최근 주문 100개가 응답됩니다.

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EB%8C%80%EA%B8%B0-%EC%A3%BC%EB%AC%B8-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| uuid | 주문의 고유 아이디 | String |
| side | 주문 종류 | String |
| ord\_type | 주문 방식<br>\- `limit` : 지정가 주문<br>\- `price` : 시장가 주문(매수)<br>\- `market` : 시장가 주문(매도)<br>\- `best` : [최유리 주문](https://docs.upbit.com/kr/changelog/new_ord_type_expand) | String |
| price | 주문 당시 화폐 가격 | NumberString |
| state | 주문 상태 | String |
| market | 마켓 ID | String |
| created\_at | 주문 생성 시간 | DateString |
| volume | 사용자가 입력한 주문 양 | NumberString |
| remaining\_volume | 체결 후 남은 주문 양 | NumberString |
| reserved\_fee | 수수료로 예약된 비용 | NumberString |
| remaining\_fee | 남은 수수료 | NumberString |
| paid\_fee | 사용된 수수료 | NumberString |
| locked | 거래에 사용 중인 비용 | NumberString |
| executed\_volume | 체결된 양 | NumberString |
| executed\_funds | 현재까지 체결된 금액 | NumberString |
| trades\_count | 해당 주문에 걸린 체결 수 | Integer |
| time\_in\_force | [IOC, FOK 설정](https://docs.upbit.com/kr/changelog/new_ord_type_expand)<br>\- `ioc` : Immediate or Cancel<br>\- `fok` : Fill or Kill | String |
| identifier | 조회용 사용자 지정값<br>\*identifier 필드는 2024-10-18 이후에 생성된 주문에 대해서만 제공합니다. | String |

\*null인 필드는 응답에서 제외됩니다. (예: IOC or FOK 설정이 없었던 주문의 경우 해당 필드는 응답되지 않습니다.

market

string

마켓 아이디

state

string

Defaults to wait

주문 상태

states\[\]

array of strings

Defaults to wait

주문 상태의 목록

states\[\]
ADD string

page

float

Defaults to 1

limit

float

Defaults to 100

요청 개수

order\_by

string

Defaults to desc

정렬 방식

Authorization

string

Authorization token (JWT)

# `` 200      200

json

# `` 4XX      4XX

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

NodePythonRubyJava

```

xxxxxxxxxx

50

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const queryEncode = require("querystring").encode

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11const market = 'KRW-BTC'

12const states = ['wait', 'watch']

13​

14

const non_array_body = {

15    market: market,

16}

17

const array_body = {

18    states: states,

19}

20

const body = {

21    ...non_array_body,

22    ...array_body

23}

24​

25const states_query = states.map(state => `states[]=${state}`).join('&')

26const query = queryEncode(non_array_body) +  '&' + states_query

```

```

xxxxxxxxxx

21



1

[\
\
2\
\
  {\
\
3    "uuid": "d098ceaf-6811-4df8-97f2-b7e01aefc03f",\
\
4    "side": "bid",\
\
5    "ord_type": "limit",\
\
6    "price": "104812000",\
\
7    "state": "wait",\
\
8    "market": "KRW-BTC",\
\
9    "created_at": "2024-06-13T10:26:21+09:00",\
\
10    "volume": "0.00101749",\
\
11    "remaining_volume": "0.00006266",\
\
12    "reserved_fee": "53.32258094",\
\
13    "remaining_fee": "3.28375996",\
\
14    "paid_fee": "50.03882098",\
\
15    "locked": "6570.80367996",\
\
16    "executed_volume": "0.00095483",\
\
17    "executed_funds": "100077.64196",\
\
18    "trades_count": 1\
\
19  },\
\
20  # ....\
\
21]

```

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference_tickers_by_quote.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/tickers_by_quote\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| quote\_currencies | 반점으로 구분되는 거래 화폐 코드 (ex. KRW, BTC, USDT) | String |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/tickers_by_quote\#response)

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
| prev\_closing\_price | 전일 종가(UTC 0시 기준) | Double |
| change | EVEN : 보합<br>RISE : 상승<br>FALL : 하락 | String |
| change\_price | 변화액의 절대값 | Double |
| change\_rate | 변화율의 절대값 | Double |
| signed\_change\_price | 부호가 있는 변화액 | Double |
| signed\_change\_rate | 부호가 있는 변화율 | Double |
| trade\_volume | 가장 최근 거래량 | Double |
| acc\_trade\_price | 누적 거래대금(UTC 0시 기준) | Double |
| acc\_trade\_price\_24h | 24시간 누적 거래대금 | Double |
| acc\_trade\_volume | 누적 거래량(UTC 0시 기준) | Double |
| acc\_trade\_volume\_24h | 24시간 누적 거래량 | Double |
| highest\_52\_week\_price | 52주 신고가 | Double |
| highest\_52\_week\_date | 52주 신고가 달성일<br>포맷: `yyyy-MM-dd` | String |
| lowest\_52\_week\_price | 52주 신저가 | Double |
| lowest\_52\_week\_date | 52주 신저가 달성일<br>포맷: `yyyy-MM-dd` | String |
| timestamp | 타임스탬프 | Long |

\*위 응답의 change, change\_price, change\_rate, signed\_change\_price, signed\_change\_rate 필드들은 전일종가 대비 값입니다.

quote\_currencies

string

required

반점으로 구분되는 거래 화폐 코드 (ex. KRW, BTC, USDT)

# `` 200      200

json

# `` 400      400

object

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePython

```

xxxxxxxxxx

15

1const request = require('request')

2​

3const server_url = "https://api.upbit.com"

4​

5

const options = {

6    method: "GET",

7    url: server_url + "/v1/ticker/all",

8    qs: {quote_currencies: "KRW,BTC"}

9}

10​

11

request(options, (error, response, body) => {

12    if (error) throw new Error(error)

13    console.log(body)

14})

15​

```

```

xxxxxxxxxx

59
]

1

[\
\
2\
\
  {\
\
3    "market": "KRW-BTC",\
\
4    "trade_date": "20240822",\
\
5    "trade_time": "071602",\
\
6    "trade_date_kst": "20240822",\
\
7    "trade_time_kst": "161602",\
\
8    "trade_timestamp": 1724310962713,\
\
9    "opening_price": 82900000.00000000,\
\
10    "high_price": 83000000.00000000,\
\
11    "low_price": 81280000.00000000,\
\
12    "trade_price": 82324000.00000000,\
\
13    "prev_closing_price": 82900000.00000000,\
\
14    "change": "FALL",\
\
15    "change_price": 576000.00000000,\
\
16    "change_rate": 0.0069481303,\
\
17    "signed_change_price": -576000.00000000,\
\
18    "signed_change_rate": -0.0069481303,\
\
19    "trade_volume": 0.00042335,\
\
20    "acc_trade_price": 66058843588.4690600000000000,\
\
21    "acc_trade_price_24h": 250206655398.15126000,\
\
22    "acc_trade_volume": 803.00214714,\
\
23    "acc_trade_volume_24h": 3047.01625142,\
\
24    "highest_52_week_price": 105000000.00000000,\
\
25    "highest_52_week_date": "2024-03-14",\
\
```\
\
Updated 3 months ago\
\
* * *\
\
Did this page help you?\
\
Yes\
\
No\
\
## Open API 이용약관\
\
본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.\
\
제 1조 (목적)\
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.\
\
제 2조 (정의)\
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.\
\
2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.\
\
3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.\
\
제 3조 (면책사항)\
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.\
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.\
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.\
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.\
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.\
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.\
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.\
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.\
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.\
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.\
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.\
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.\
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.\
\
제 4조 (Open API 서비스 제공의 제한 및 해지)\
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.\
1\. 본 이용약관 제6조를 위반한 경우\
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우\
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우\
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우\
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우\
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.\
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.\
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.\
\
제 5조 (저작권)\
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.\
\
제 6조 (사용자의 의무와 책임)\
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.\
1\. API 업데이트 및 변경 사항에 대한 공지\
2\. 제도 변경 공지\
3\. 두나무-업비트 정책 반영에 따른 공지\
4\. 기타 긴급 공지\
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.\
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.\
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.\
\
제 7조 (약관의 변경 등)\
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.\
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).\
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.\
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.\
\
제 8조 (효력 발생 및 유효기간)\
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.\
\
제 9조 (기타)\
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.\
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.\
\
제 10조 (관할법원)\
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.\
\
<부칙>\
본 이용약관은 2024년 10월 30일부터 적용됩니다.\
이전의 이용약관은 아래에서 확인하실 수 있습니다.\
\
\
[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)\
\
[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)\
\
[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)\
\
[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)\
\
동의

[docs_upbit_com_kr_reference__EA_B0_9C_EB_B3_84__EC_9E_85_EA_B8_88__EC_A3_BC_EC_86_8C__EC_A1_B0_ED_9A_8C.md]
## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EA%B0%9C%EB%B3%84-%EC%9E%85%EA%B8%88-%EC%A3%BC%EC%86%8C-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| currency | 화폐를 의미하는 영문 대문자 코드 | String |
| net\_type | 입금 네트워크 | String |
| deposit\_address | 입금 주소 | String |
| secondary\_address | 2차 입금 주소 | String |

> ## 📘  입금 주소 조회 요청 API 유의사항
>
> 입금 주소 생성 요청 이후 아직 발급되지 않은 상태일 경우 deposit\_address가 null일 수 있습니다.

currency

string

required

Currency symbol

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

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

40

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const queryEncode = require("querystring").encode

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11

const body = {

12    currency: 'BTC',

13    net_type: 'BTC'

14}

15​

16const query = queryEncode(body)

17​

18const hash = crypto.createHash('sha512')

19const queryHash = hash.update(query, 'utf-8').digest('hex')

20​

21

const payload = {

22    access_key: access_key,

23    nonce: uuidv4(),

24    query_hash: queryHash,

25    query_hash_alg: 'SHA512',

26}

```

```

xxxxxxxxxx



1

{

2  "currency": "BTC",

3  "net_type": "BTC",

4  "deposit_address": "3EusRwybuZUhVDeHL7gh3HSLmbhLcy7NqD",

5  "secondary_address": null

6}

```

Updated 3 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EC_A3_BC_EB_AC_B8__EC_9D_BC_EA_B4_84__EC_B7_A8_EC_86_8C__EC_A0_91_EC_88_98.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EC%A3%BC%EB%AC%B8-%EC%9D%BC%EA%B4%84-%EC%B7%A8%EC%86%8C-%EC%A0%91%EC%88%98\#request-parameters)

| Name | 설명 | 타입 |
| --- | --- | --- |
| cancel\_side | 주문 종류<br>\- `all` : 매수, 매도 전체 (default)<br>\- `ask` : 매도<br>\- `bid` : 매수 | String |
| pairs | 반점으로 구분되는 주문 **취소할 종목** 리스트 (ex. `KRW-BTC,KRW-ETH`)<br>\*최대 20개까지의 pairs 를 지원합니다.<br>\*값이 주어질 경우 해당 종목만 cancel\_side에 따라 처리됩니다<br>(e.x. cancel\_side = `all`, pairs = `KRW-BTC,KRW-ETH` 면 두 종목의 미체결 매수/매도 주문 취소) | String |
| excluded\_pairs | 반점으로 구분되는 일괄 취소 대상에서 ' **제외**'할 종목 리스트 (ex. `KRW-BTC,KRW-ETH`)<br>\*최대 20개까지의 excluded\_pairs 를 지원합니다.<br>\*값이 주어질 경우 해당 종목은 취소대상에서 제외됩니다.<br>(e.x. cancel\_side = `ask`, excluded\_pairs = `KRW-BTC` 면 해당 종목만 제외 후 미체결 매도 주문 취소) | String |
| quote\_currencies | 반점으로 구분되는 **주문 취소할 거래 화폐** 리스트 (ex. `KRW,BTC,USDT`)<br>\*값이 주어질 경우 해당 화폐로 거래하는 종목들만 cancel\_side에 따라 처리됩니다.<br>(e.x. cancel\_side = `bid`, quote\_currencies = `KRW` 이면 원화마켓의 미체결 매수 주문 취소) | String |
| count | 취소 접수할 주문의 최대 개수 (default : 20, max : 300) | Number |
| order\_by | 취소할 주문의 정렬 방식<br>\- asc : 오래된 주문 순대로 주문 취소 접수 요청<br>\- desc : 최근 주문 순대로 주문 취소 접수 요청 (default) | String |

**\*어떤 파라미터도 포함하지 않고 요청 시, default값에 따라 '매수/매도 전체' 대상 '최근' '20개' 주문에 대해 취소 요청 됩니다.**

> ## ❗️
>
> 이 API 는 Query Parameter 형식의 요청만 지원합니다. Request Body 를 통한 요청은 지원하지 않으니 유의해주시기 바랍니다.

> ## ❗️  유의해 주세요
>
> - `pairs` 혹은 `quote_currencies` 둘 중 하나의 파라미터만 포함될 수 있으며, 둘 다 미포함 시 전체 마켓을 대상으로 주문 취소가 접수됩니다.
> - `order_by` 값에 따라 `asc` 일 경우, 생성 시점이 오래된 주문 순서대로, `desc` 일 경우, 생성 시점이 최근인 주문 순서대로 `count` 개수만큼 주문 취소가 접수됩니다.
> - 미체결(WAIT) 상태의 주문만 취소되며, **예약주문(WATCH)은 주문 일괄 취소 접수 기능에서 취소할 수 없습니다.**
>
>
>   → [id로 주문리스트 취소 접수(DELETE /v1/orders/uuids)](https://docs.upbit.com/kr/reference/id%EB%A1%9C-%EC%A3%BC%EB%AC%B8%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%B7%A8%EC%86%8C-%EC%A0%91%EC%88%98) 혹은 [주문 취소 접수(DELETE /v1/order)](https://docs.upbit.com/kr/reference/%EC%A3%BC%EB%AC%B8-%EC%B7%A8%EC%86%8C) 를 이용해 주세요
> - 별도 rate limit 적용: **2초당 1회 요청**이 가능합니다.
> - 취소 처리 중 미체결 주문의 체결이 발생할 수 있기 때문에, 취소요청을 보내는 시점의 주문 잔량과 완료된 후 취소된 주문의 주문 잔량은 다를 수 있습니다.
> - pairs, quote\_currencies 중에 포함되어 있으나, excluded\_pairs에도 포함된 요청의 경우 해당 종목은 취소되지 않습니다. ( **취소 대상 제외가 우선**)

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EC%A3%BC%EB%AC%B8-%EC%9D%BC%EA%B4%84-%EC%B7%A8%EC%86%8C-%EC%A0%91%EC%88%98\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| success | 취소 요청 성공한 주문 리스트 정보 | Object |
| success.count | 취소 요청 성공한 주문의 개수 | Number |
| success.orders | 취소 요청 성공한 주문 정보 | Array\[Object\] |
| success.orders.uuid | 취소 요청 성공한 주문의 UUID | String |
| success.orders.identifier | 조회용 사용자 지정값<br>\*identifier 필드는 2024-10-18 이후에 생성된 주문에 대해서만 제공합니다. | String |
| success.orders.market | 취소 요청 성공한 주문의 마켓 아이디 | String |
| failed | 취소 요청 실패한 주문 리스트 정보 | Object |
| failed.count | 취소 요청 실패한 주문의 개수 | Number |
| failed.orders | 취소 요청 실패한 주문 정보 | Array\[Object\] |
| failed.orders.uuid | 취소 요청 실패한 주문의 UUID | String |
| failed.orders.market | 취소 요청 실패한 주문의 마켓 아이디 | String |
| failed.orders.identifier | 조회용 사용자 지정값<br>\*identifier 필드는 2024-10-18 이후에 생성된 주문에 대해서만 제공합니다. | String |

> ## ❗️  취소 실패
>
> 취소 접수가 되기 전에 이미 체결이 완료된 경우, 이미 취소된 주문인 경우, 리브랜딩 등의 이유로 인한 마켓 일시 중단 등의 사유로 일부 주문에 대해서 주문 취소 접수가 실패될 수 있습니다.

cancel\_side

string

Defaults to all

주문 종류

pairs

string

반점으로 구분되는 주문 취소할 종목 리스트

excluded\_pairs

string

반점으로 구분되는 일괄 취소 대상에서 '제외'할 종목 리스트

quote\_currencies

string

반점으로 구분되는 주문 취소할 거래 화폐 리스트 (ex. KRW, BTC, USDT)

count

string

취소 접수할 주문의 최대 개수, default : 20, max : 300

order\_by

string

취소할 주문의 정렬 방식

# `` 200      200

object

success

object

count

integer

Defaults to 0

orders

array of objects

orders

object

uuid

string

market

string

failed

object

count

integer

Defaults to 0

orders

array of objects

orders

object

uuid

string

market

string

# `` 400      400

object

error

object

name

string

message

string

Updated 25 days ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

40

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const querystring = require("querystring")

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11

const params = {

12    quote_currencies: 'KRW,BTC',

13    excluded_pairs: 'KRW-BTC,BTC-ETH',

14}

15​

16const query = querystring.unescape(querystring.encode(params))

17​

18const hash = crypto.createHash('sha512')

19const queryHash = hash.update(query, 'utf-8').digest('hex')

20​

21

const payload = {

22    access_key: access_key,

23    nonce: uuidv4(),

24    query_hash: queryHash,

25    query_hash_alg: 'SHA512',

26}

```

```

xxxxxxxxxx

24



1

{

2

  "success": {

3    "count": 2,

4

    "orders": [\
\
5\
\
      {\
\
6        "uuid": "bbbb8e07-1689-4769-af3e-a117016623f8",\
\
7        "market": "KRW-ETH"\
\
8      },\
\
9\
\
      {\
\
10        "uuid": "4312ba49-5f1a-4a01-9f3b-2d2bce17267e",\
\
11        "market": "KRW-ETH"\
\
12      }\
\
13    ]

14  },

15

  "failed": {

16    "count": 1,

17

    "orders": [\
\
18\
\
      {\
\
19        "uuid": "bdb49a54-de36-4eb4-a963-9c8d4337a9da",\
\
20        "market": "BTC-XRP"\
\
21      }\
\
22    ]

23  }

24}

```

Updated 25 days ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference_websocket_ticker.md]
# Request   [Skip link to Request](https://docs.upbit.com/kr/reference/websocket-ticker\#request)

요청은 JSON Object를 이용하며 응답 또한 JSON Object 입니다. 요청은 크게 ticket field, type field, format field 로 나누어지며 하나의 요청에 여러 개의 type field 를 명시할 수 있습니다. ticket field 와 format field 에 대해서는 [요청 방법 및 포맷](https://docs.upbit.com/kr/reference/websocket-request-format) 을 참고해주시기 바랍니다.

> ## 📘  Request format
>
> **\[{Ticket Field},{Type Field},....,{Type Field},{Format Field}\]**

### **Type Field**   [Skip link to [object Object]](https://docs.upbit.com/kr/reference/websocket-ticker\#type-field)

수신하고 싶은 시세 정보를 나열하는 필드입니다.

is\_only\_snapshot, is\_only\_realtime 필드는 생략 가능하며 모두 생략시 스냅샷과 실시간 데이터 모두를 수신합니다.

| 필드명 | 타입 | 내용 | 필수 여부 | 기본 값 |
| --- | --- | --- | --- | --- |
| type | String | 데이터 타입<br>- `ticker`: 현재가 | O |  |
| codes | List | 마켓 코드 리스트<br>\*대문자로 요청해야 합니다. | O |  |
| is\_only\_snapshot | Boolean | 스냅샷 시세만 제공 | X | false |
| is\_only\_realtime | Boolean | 실시간 시세만 제공 | X | false |

# Response   [Skip link to Response](https://docs.upbit.com/kr/reference/websocket-ticker\#response)

| 필드명 | 축약형 (format: SIMPLE) | 내용 | 타입 | 값 |
| --- | --- | --- | --- | --- |
| type | ty | 타입 | String | `ticker` : 현재가 |
| code | cd | 마켓 코드 (ex. KRW-BTC) | String |  |
| opening\_price | op | 시가 | Double |  |
| high\_price | hp | 고가 | Double |  |
| low\_price | lp | 저가 | Double |  |
| trade\_price | tp | 현재가 | Double |  |
| prev\_closing\_price | pcp | 전일 종가 | Double |  |
| change | c | 전일 대비 | String | `RISE` : 상승<br>`EVEN` : 보합<br>`FALL` : 하락 |
| change\_price | cp | 부호 없는 전일 대비 값 | Double |  |
| signed\_change\_price | scp | 전일 대비 값 | Double |  |
| change\_rate | cr | 부호 없는 전일 대비 등락율 | Double |  |
| signed\_change\_rate | scr | 전일 대비 등락율 | Double |  |
| trade\_volume | tv | 가장 최근 거래량 | Double |  |
| acc\_trade\_volume | atv | 누적 거래량(UTC 0시 기준) | Double |  |
| acc\_trade\_volume\_24h | atv24h | 24시간 누적 거래량 | Double |  |
| acc\_trade\_price | atp | 누적 거래대금(UTC 0시 기준) | Double |  |
| acc\_trade\_price\_24h | atp24h | 24시간 누적 거래대금 | Double |  |
| trade\_date | tdt | 최근 거래 일자(UTC) | String | yyyyMMdd |
| trade\_time | ttm | 최근 거래 시각(UTC) | String | HHmmss |
| trade\_timestamp | ttms | 체결 타임스탬프 (milliseconds) | Long |  |
| ask\_bid | ab | 매수/매도 구분 | String | `ASK` : 매도<br>`BID` : 매수 |
| acc\_ask\_volume | aav | 누적 매도량 | Double |  |
| acc\_bid\_volume | abv | 누적 매수량 | Double |  |
| highest\_52\_week\_price | h52wp | 52주 최고가 | Double |  |
| highest\_52\_week\_date | h52wdt | 52주 최고가 달성일 | String | yyyy-MM-dd |
| lowest\_52\_week\_price | l52wp | 52주 최저가 | Double |  |
| lowest\_52\_week\_date | l52wdt | 52주 최저가 달성일 | String | yyyy-MM-dd |
| trade\_status | ts | 거래상태 (\*Deprecated) | String |  |
| market\_state | ms | 거래상태 | String | `PREVIEW` : 입금지원<br>`ACTIVE` : 거래지원가능<br>`DELISTED` : 거래지원종료 |
| market\_state\_for\_ios | msfi | 거래 상태 (\*Deprecated) | String |  |
| is\_trading\_suspended | its | 거래 정지 여부 (\*Deprecated) | Boolean |  |
| delisting\_date | dd | 거래지원 종료일 | Date |  |
| market\_warning | mw | 유의 종목 여부<br>'유의 종목' 지정 여부에 대해 반환하며, '주의 종목' 지정 여부는 지원하지 않습니다. 업비트 시장경보에 대한 자세한 정보는 [관련 공지사항을 참고](https://upbit.com/service_center/notice?id=3482) 하시기 바랍니다. | String | `NONE` : 해당없음<br>`CAUTION` : 투자유의 |
| timestamp | tms | 타임스탬프 (millisecond) | Long |  |
| stream\_type | st | 스트림 타입 | String | `SNAPSHOT` : 스냅샷<br>`REALTIME` : 실시간 |

# Example   [Skip link to Example](https://docs.upbit.com/kr/reference/websocket-ticker\#example)

### Request   [Skip link to Request](https://docs.upbit.com/kr/reference/websocket-ticker\#request-1)

- `KRW-BTC`, `KRW-ETH` 의 현재가 수신

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

### Response   [Skip link to Response](https://docs.upbit.com/kr/reference/websocket-ticker\#response-1)

JSON

```rdmd-code lang-json theme-light

{
  "type": "ticker",
  "code": "KRW-BTC",
  "opening_price": 31883000,
  "high_price": 32310000,
  "low_price": 31855000,
  "trade_price": 32287000,
  "prev_closing_price": 31883000.00000000,
  "acc_trade_price": 78039261076.51241000,
  "change": "RISE",
  "change_price": 404000.00000000,
  "signed_change_price": 404000.00000000,
  "change_rate": 0.0126713295,
  "signed_change_rate": 0.0126713295,
  "ask_bid": "ASK",
  "trade_volume": 0.03103806,
  "acc_trade_volume": 2429.58834336,
  "trade_date": "20230221",
  "trade_time": "074102",
  "trade_timestamp": 1676965262139,
  "acc_ask_volume": 1146.25573608,
  "acc_bid_volume": 1283.33260728,
  "highest_52_week_price": 57678000.00000000,
  "highest_52_week_date": "2022-03-28",
  "lowest_52_week_price": 20700000.00000000,
  "lowest_52_week_date": "2022-12-30",
  "market_state": "ACTIVE",
  "is_trading_suspended": false,
  "delisting_date": null,
  "market_warning": "NONE",
  "timestamp": 1676965262177,
  "acc_trade_price_24h": 228827082483.70729000,
  "acc_trade_volume_24h": 7158.80283560,
  "stream_type": "REALTIME"
}

```

Updated 7 months ago

* * *

Did this page help you?

Yes

No

Updated 7 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference_websocket_error.md]
# Format   [Skip link to Format](https://docs.upbit.com/kr/reference/websocket-error\#format)

에러가 발생할 경우 JSON 형식의 에러 메시지가 내려갑니다.

# Response   [Skip link to Response](https://docs.upbit.com/kr/reference/websocket-error\#response)

| 필드명 | 내용 | 타입 |
| --- | --- | --- |
| error | 에러 객체 | Object |
| error.name | 종류 | String |
| error.message | 메시지 | String |

# 에러 종류   [Skip link to 에러 종류](https://docs.upbit.com/kr/reference/websocket-error\#%EC%97%90%EB%9F%AC-%EC%A2%85%EB%A5%98)

### INVALID\_AUTH   [Skip link to INVALID_AUTH](https://docs.upbit.com/kr/reference/websocket-error\#invalid_auth)

- private type 인데 인증 없이 요청했을 경우


\*인증 방법은 `Websocket -> 요청 방법` 페이지를 참고하시기 바랍니다.

JSON

```rdmd-code lang-json theme-light

{"error":{"name":"INVALID_AUTH","message":"인증 정보가 올바르지 않습니다."}}

```

### WRONG\_FORMAT   [Skip link to WRONG_FORMAT](https://docs.upbit.com/kr/reference/websocket-error\#wrong_format)

JSON

```rdmd-code lang-json theme-light

{"error":{"name":"WRONG_FORMAT","message":"Format 이 맞지 않습니다."}}

```

### NO\_TICKET   [Skip link to NO_TICKET](https://docs.upbit.com/kr/reference/websocket-error\#no_ticket)

JSON

```rdmd-code lang-json theme-light

{"error":{"name":"NO_TICKET","message":"티켓이 존재하지 않거나, 유효하지 않습니다."}}

```

### NO\_TYPE   [Skip link to NO_TYPE](https://docs.upbit.com/kr/reference/websocket-error\#no_type)

JSON

```rdmd-code lang-json theme-light

{"error":{"name":"NO_TYPE","message":"type 필드가 존재하지 않습니다."}}

```

### NO\_CODES   [Skip link to NO_CODES](https://docs.upbit.com/kr/reference/websocket-error\#no_codes)

JSON

```rdmd-code lang-json theme-light

{"error":{"name":"NO_CODES","message":"codes 필드가 존재하지 않습니다."}}

```

### INVALID\_PARAM   [Skip link to INVALID_PARAM](https://docs.upbit.com/kr/reference/websocket-error\#invalid_param)

JSON

```rdmd-code lang-json theme-light

{"error":{"name":"INVALID_PARAM","message":"codes 필드가 비어 있습니다."}}

```

Updated almost 2 years ago

* * *

Did this page help you?

Yes

No

Updated almost 2 years ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference_test_and_request_sample.md]
WebSocket을 이용한 시세 수신 테스트를 위해서는 여러 가지 방법을 사용할 수 있습니다.

알려진 방법으로는 telsocket 혹은 wscat을 사용할 수 있습니다.

> wscat 을 이용하는 경우

Shell

```rdmd-code lang-shell theme-light

$ npm install -g wscat
$ wscat -c wss://api.upbit.com/websocket/v1
connected (press CTRL+C to quit)

```

> telsocket 을 이용하는 경우

Shell

```rdmd-code lang-shell theme-light

$ telsocket -url wss://api.upbit.com/websocket/v1
Connected!

```

만약 원화-비트코인(KRW-BTC) 마켓의 실시간 정보를 알고싶다면 다음과 같이 요청할 수 있습니다.

Shell

```rdmd-code lang-shell theme-light

$ telsocket -url wss://api.upbit.com/websocket/v1
Connected!
[{"ticket":"test"},{"type":"ticker","codes":["KRW-BTC"]}]
{"market":"KRW-BTC","opening_price":8450000.00000000,"high_price":8679000.00000000,"low_price":8445000.00000000,"trade_price":8629000.0,"prev_closing_price":8450000.00000000,"acc_trade_price":105514711074.18726000,"change":"RISE","change_price":179000.00000000,"signed_change_price":179000.00000000,"change_rate":0.0211834320,"signed_change_rate":0.0211834320,"ask_bid":"ASK","trade_volume":0.0105675,"acc_trade_volume":12312.36058857,"trade_date":"20180418","trade_time":"100729","trade_timestamp":1524046049000,"acc_ask_volume":5703.42273172,"acc_bid_volume":6608.93785685,"highest_52_week_price":28885000.00000000,"highest_52_week_date":"2018-01-06","lowest_52_week_price":3286000.00000000,"lowest_52_week_date":"2017-09-15","trade_status":"ACTIVE","market_state":"ACTIVE","market_state_for_ios":"ACTIVE","is_trading_suspended":false,"delisting_date":null,"market_warning":"NONE","timestamp":1524046049766,"acc_trade_price_24h":55330325803.78210000,"acc_trade_volume_24h":6448.96200341}
 {"market":"KRW-BTC","opening_price":8450000.00000000,"high_price":8679000.00000000,"low_price":8445000.00000000,"trade_price":8629000.0,"prev_closing_price":8450000.00000000,"acc_trade_price":105515441503.850220000,"change":"RISE","change_price":179000.00000000,"signed_change_price":179000.00000000,"change_rate":0.0211834320,"signed_change_rate":0.0211834320,"ask_bid":"ASK","trade_volume":0.08464824,"acc_trade_volume":12312.44523681,"trade_date":"20180418","trade_time":"100730","trade_timestamp":1524046050000,"acc_ask_volume":5703.50737996,"acc_bid_volume":6608.93785685,"highest_52_week_price":28885000.00000000,"highest_52_week_date":"2018-01-06","lowest_52_week_price":3286000.00000000,"lowest_52_week_date":"2017-09-15","trade_status":"ACTIVE","market_state":"ACTIVE","market_state_for_ios":"ACTIVE","is_trading_suspended":false,"delisting_date":null,"market_warning":"NONE","timestamp":1524046050758,"acc_trade_price_24h":55330325803.78210000,"acc_trade_volume_24h":6448.96200341}
...

```

특별히 스냅샷만, 혹은 실시간 정보만 받겠다고 명시하지 않았기 때문에 맨 처음 **스냅샷 정보** 가 내려오고 뒤를 이어 **실시간 정보** 를 계속해서 수신할 수 있습니다. 만약 여러 마켓의 정보를 동시에 수신하고 싶은 경우 `codes` 필드에 여러 개의 마켓을 반점(,)으로 구분하여 명시하면 됩니다.

예를 들어 원화-비트코인(KRW-BTC) 마켓과 비트코인-비트코인캐시(KRW-BCH) 마켓의 **실시간 체결정보** 만을 **간소화된 포맷** 으로 수신하고 싶은 경우 다음과 같이 요청할 수 있습니다.

Shell

```rdmd-code lang-shell theme-light

$ telsocket -url wss://api.upbit.com/websocket/v1
Connected!
[{"ticket":"test"},{"type":"trade","codes":["KRW-BTC","BTC-BCH"]},{"format":"SIMPLE"}]
{"mk":"KRW-BTC","tms":1523531768829,"td":"2018-04-12","ttm":"11:16:03","ttms":1523531763000,"tp":7691000.0,"tv":0.00996719,"ab":"BID","pcp":7429000.00000000,"c":"RISE","cp":262000.00000000,"sid":1523531768829000,"st":"SNAPSHOT"}
 {"mk":"BTC-BCH","tms":1523531745481,"td":"2018-04-12","ttm":"11:15:48","ttms":1523531748370,"tp":0.09601999,"tv":0.18711789,"ab":"BID","pcp":0.09618000,"c":"FALL","cp":0.00016001,"sid":15235317454810000,"st":"SNAPSHOT"}
 {"mk":"KRW-BTC","tms":1523531769250,"td":"2018-04-12","ttm":"11:16:04","ttms":1523531764000,"tp":7691000.0,"tv":0.07580113,"ab":"BID","pcp":7429000.00000000,"c":"RISE","cp":262000.00000000,"sid":1523531769250000,"st":"REALTIME"}
 ...

```

마찬가지로 스냅샷이 먼저 내려온 뒤 실시간 체결 현황을 수신할 수 있음을 알 수 있습니다.

위의 모든 요청은 WebSocket 연결이 제대로 된 후를 가정합니다.

이 외에도 몇 가지 요청 예시를 소개하자면,

1. KRW-BTC, BTC-XRP 마켓의 `체결` 정보


\[{"ticket":"UNIQUE\_TICKET"},{"type":"trade","codes":\["KRW-BTC","BTC-XRP"\]}\]

2. KRW-BTC, BTC-XRP 마켓의 `호가` 정보


\[{"ticket":"UNIQUE\_TICKET"},{"type":"orderbook","codes":\["KRW-BTC","BTC-XRP"\]}\]

3. KRW-BTC 마켓의 `1~3호가`, BTC-XRP 마켓의 `1~5호가` 정보


\[{"ticket":"UNIQUE\_TICKET"},{"type":"orderbook","codes":\["KRW-BTC.3","BTC-XRP.5"\]}\]

4. KRW-BTC 마켓의 `체결` 정보, KRW-ETH 마켓의 `호가` 정보


\[{"ticket":"UNIQUE\_TICKET"},{"type":"trade","codes":\["KRW-BTC"\]},{"type":"orderbook","codes":\["KRW-ETH"\]}\]

5. KRW-BTC 마켓의 `체결` 정보, KRW-ETH 마켓의 `호가` 정보, KRW-EOS 마켓의 `현재가` 정보


\[{"ticket":"UNIQUE\_TICKET"},{"type":"trade","codes":\["KRW-BTC"\]},{"type":"orderbook","codes":\["KRW-ETH"\]},{"type":"ticker", "codes":\["KRW-EOS"\]}\]


한 번에 여러 종류의 정보를 요청할 시 `type` 필드를 통해 정보의 타입을 구분할 수 있습니다.

Updated almost 2 years ago

* * *

Did this page help you?

Yes

No

Updated almost 2 years ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EC_9D_BCday__EC_BA_94_EB_93_A4_1.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EC%9D%BCday-%EC%BA%94%EB%93%A4-1\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 마켓 코드 (ex. KRW-BTC) | String |
| to | 마지막 캔들 시각 (exclusive).<br>ISO8061 포맷 (yyyy-MM-dd'T'HH:mm:ss'Z' or yyyy-MM-dd HH:mm:ss). 기본적으로 UTC 기준 시간이며 `2023-01-01T00:00:00+09:00` 과 같이 KST 시간으로 요청 가능.<br>비워서 요청시 가장 최근 캔들 | String |
| count | 캔들 개수(최대 200개까지 요청 가능) | Integer |
| converting\_price\_unit | 종가 환산 화폐 단위 (생략 가능, KRW로 명시할 시 원화 환산 가격을 반환.) | String |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EC%9D%BCday-%EC%BA%94%EB%93%A4-1\#response)

> ## 🚧  캔들은 해당 시간대에 체결이 발생한 경우에만 생성됩니다.
>
> - candle\_date\_time이 2024-08-31T00:00:00인 일봉 캔들은 2024-08-31T00:00:00 (이상) ~ 2024-09-01T00:00:00 (미만) 사이의 체결로 구성됩니다.
> - 해당 기간 동안 체결이 없을 경우, 2024-08-31T00:00:00 캔들은 생성되지 않으며 응답에 포함되지 않습니다.

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 종목 코드 | String |
| candle\_date\_time\_utc | 캔들 기준 시각(UTC 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |
| candle\_date\_time\_kst | 캔들 기준 시각(KST 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |
| opening\_price | 시가 | Double |
| high\_price | 고가 | Double |
| low\_price | 저가 | Double |
| trade\_price | 종가 | Double |
| timestamp | 마지막 틱이 저장된 시각 | Long |
| candle\_acc\_trade\_price | 누적 거래 금액 | Double |
| candle\_acc\_trade\_volume | 누적 거래량 | Double |
| prev\_closing\_price | 전일 종가(UTC 0시 기준) | Double |
| change\_price | 전일 종가 대비 변화 금액 | Double |
| change\_rate | 전일 종가 대비 변화량 | Double |
| converted\_trade\_price | 종가 환산 화폐 단위로 환산된 가격(요청에 convertingPriceUnit 파라미터 없을 시 해당 필드 포함되지 않음.) | Double |

`converting_price_unit` 파라미터의 경우, 원화 마켓이 아닌 다른 마켓(ex. BTC, ETH)의 일봉 요청시 종가를 명시된 파라미터 값으로 환산해 `converted_trade_price` 필드에 추가하여 반환합니다.

현재는 원화( `KRW`) 로 변환하는 기능만 제공하며 추후 기능을 확장할 수 있습니다.

market

string

required

종목 코드 (ex. KRW-BTC)

to

string

마지막 캔들 시각 (exclusive). 비워서 요청시 가장 최근 캔들

count

int32

Defaults to 1

캔들 개수(최대 200개까지 요청 가능)

converting\_price\_unit

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

Updated 5 months ago

* * *

Did this page help you?

Yes

No

ShellPythonNode

```

xxxxxxxxxx

10

1# KRW-BTC 마켓에 가장 최근 1개 일봉을 요청

2curl --request GET \

3     --url 'https://api.upbit.com/v1/candles/days?market=KRW-BTC&count=1' \

4     --header 'accept: application/json'

5​

6# KRW-BTC 마켓에 2024년 10월 1일(UTC) 이전 가장 최근 일봉 하나를 요청

7curl --request GET \

8     --url 'https://api.upbit.com/v1/candles/days?market=KRW-BTC&count=1&to=2024-10-01%2000%3A00%3A00' \

9     --header 'accept: application/json'

10

```

```

xxxxxxxxxx

17



1

[\
\
2\
\
  {\
\
3    "market": "KRW-BTC",\
\
4    "candle_date_time_utc": "2018-04-18T00:00:00",\
\
5    "candle_date_time_kst": "2018-04-18T09:00:00",\
\
6    "opening_price": 8450000,\
\
7    "high_price": 8679000,\
\
8    "low_price": 8445000,\
\
9    "trade_price": 8626000,\
\
10    "timestamp": 1524046650532,\
\
11    "candle_acc_trade_price": 107184005903.68721,\
\
12    "candle_acc_trade_volume": 12505.93101659,\
\
13    "prev_closing_price": 8450000,\
\
14    "change_price": 176000,\
\
15    "change_rate": 0.0208284024\
\
16  }\
\
17]

```

Updated 5 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference_websocket_candle.md]
> ## 🚧  이 기능은 현재 베타 버전으로 제공됩니다.

> ## 🚧  캔들은 해당 시간대에 체결이 발생한 경우에만 생성됩니다.
>
> - candle\_date\_time이 2024-08-31T22:25:00인 초봉 캔들은 2024-08-31T22:25:00 (이상) ~ 2024-08-31T22:25:01 (미만) 사이의 체결로 구성됩니다.
> - 해당 시간 동안 체결이 없을 경우, 2024-08-31T22:25:00 캔들은 생성되지 않으며 웹소켓으로 데이터가 내려가지 않습니다.

# Request   [Skip link to Request](https://docs.upbit.com/kr/reference/websocket-candle\#request)

요청은 JSON Object를 이용하며 응답 또한 JSON Object 입니다. 요청은 크게 ticket field, type field, format field 로 나누어지며 하나의 요청에 여러 개의 type field 를 명시할 수 있습니다. ticket field 와 format field 에 대해서는 [요청 방법 및 포맷](https://docs.upbit.com/kr/reference/websocket-request-format) 을 참고해주시기 바랍니다.

> ## 📘  Request format
>
> **\[{Ticket Field},{Type Field},....,{Type Field},{Format Field}\]**

### **Type Field**   [Skip link to [object Object]](https://docs.upbit.com/kr/reference/websocket-candle\#type-field)

수신하고 싶은 시세 정보를 나열하는 필드입니다.

is\_only\_snapshot, is\_only\_realtime 필드는 생략 가능하며 모두 생략시 스냅샷과 실시간 데이터 모두를 수신합니다.

| 필드명 | 타입 | 내용 | 필수 여부 | 기본 값 |
| --- | --- | --- | --- | --- |
| type | String | 데이터 타입<br>- `candle.1s`: 초봉 | O |  |
| codes | List | 마켓 코드 리스트<br>\*대문자로 요청해야 합니다. | O |  |
| is\_only\_snapshot | Boolean | 스냅샷 시세만 제공 | X | false |
| is\_only\_realtime | Boolean | 실시간 시세만 제공 | X | false |

# Response   [Skip link to Response](https://docs.upbit.com/kr/reference/websocket-candle\#response)

- 데이터 전송 주기: 1초

> ## 🚧  같은 candle\_date\_time 데이터가 여러 번 내려갈 수 있습니다.
>
> - 데이터 전송 주기를 완벽하게 보장하지 않으며, 같은 시간대의 캔들 데이터가 여러 번 내려갈 수 있습니다.
> - 가장 마지막 데이터가 가장 최신 데이터 입니다.

| 필드명 | 축약형 (format: SIMPLE) | 내용 | 타입 | 값 |
| --- | --- | --- | --- | --- |
| type | ty | 타입 | String | `candle.1s` : 초봉 |
| code | cd | 마켓 코드 (ex. KRW-BTC) | String |  |
| candle\_date\_time\_utc | cdttmu | 캔들 기준 시각(UTC 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |  |
| candle\_date\_time\_kst | cdttmk | 캔들 기준 시각(KST 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |  |
| opening\_price | op | 시가 | Double |  |
| high\_price | hp | 고가 | Double |  |
| low\_price | lp | 저가 | Double |  |
| trade\_price | tp | 종가 | Double |  |
| candle\_acc\_trade\_volume | catv | 누적 거래 금액 | Double |  |
| candle\_acc\_trade\_price | catp | 누적 거래량 | Double |  |
| timestamp | tms | 타임스탬프 (millisecond) | Long |  |
| stream\_type | st | 스트림 타입 | String | `SNAPSHOT` : 스냅샷<br>`REALTIME` : 실시간 |

# Example   [Skip link to Example](https://docs.upbit.com/kr/reference/websocket-candle\#example)

### Request   [Skip link to Request](https://docs.upbit.com/kr/reference/websocket-candle\#request-1)

- `KRW-BTC`, `KRW-ETH` 의 초봉 수신

JSON

```rdmd-code lang-json theme-light
[\
  {\
    "ticket": "test"\
  },\
  {\
    "type": "candle.1s",\
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

### Response   [Skip link to Response](https://docs.upbit.com/kr/reference/websocket-candle\#response-1)

JSON

```rdmd-code lang-json theme-light
{
  "type": "candle.1s",
  "code": "KRW-BTC",
  "candle_date_time_utc": "2025-01-02T04:28:05",
  "candle_date_time_kst": "2025-01-02T13:28:05",
  "opening_price": 142009000.00000000,
  "high_price": 142009000.00000000,
  "low_price": 142009000.00000000,
  "trade_price": 142009000.00000000,
  "candle_acc_trade_volume": 0.00606119,
  "candle_acc_trade_price": 860743.5307100000000000,
  "timestamp": 1735792085824,
  "stream_type": "REALTIME"
}
{
  "type": "candle.1s",
  "code": "KRW-ETH",
  "candle_date_time_utc": "2025-01-02T04:28:05",
  "candle_date_time_kst": "2025-01-02T13:28:05",
  "opening_price": 5059000.00000000,
  "high_price": 5059000.00000000,
  "low_price": 5059000.00000000,
  "trade_price": 5059000.00000000,
  "candle_acc_trade_volume": 0.08158869,
  "candle_acc_trade_price": 412757.1827100000000000,
  "timestamp": 1735792085749,
  "stream_type": "REALTIME"
}

```

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference_list_subscriptions.md]
# Request   [Skip link to Request](https://docs.upbit.com/kr/reference/list-subscriptions\#request)

요청은 JSON Object를 이용하며 응답 또한 JSON Object 입니다. 요청은 크게 ticket field, method field, format field 로 나누어집니다.

> ## 📘  Request format
>
> **\[{Ticket Field},{Method Field},{Format Field}\]**

### **Ticket Field**   [Skip link to [object Object]](https://docs.upbit.com/kr/reference/list-subscriptions\#ticket-field)

| 필드명 | 타입 | 내용 | 필수 여부 | 기본 값 |
| --- | --- | --- | --- | --- |
| ticket | String | 요청자를 식별할 수 있는 값 | O |  |

### **Method Field**   [Skip link to [object Object]](https://docs.upbit.com/kr/reference/list-subscriptions\#method-field)

| 필드명 | 타입 | 내용 | 필수 여부 | 기본 값 |
| --- | --- | --- | --- | --- |
| method | String | 요청 메서드<br>\- `LIST_SUBSCRIPTIONS`: 구독중인 타입 조회 | O |  |

### **Format Field**   [Skip link to [object Object]](https://docs.upbit.com/kr/reference/list-subscriptions\#format-field)

Simple로 지정될 경우 응답의 필드명이 모두 간소화됩니다.

| 필드명 | 타입 | 내용 | 필수 여부 | 기본 값 |
| --- | --- | --- | --- | --- |
| format | String | 수신할 포맷<br>\- `DEFAULT`: 기본형<br>\- `SIMPLE`: 축약형 | X | `DEFAULT` |

> ## ❗️  주의 사항 \- Format Field
>
> 실시간 데이터를 수신할 때와 동일한 Format Field 로 요청하시길 권장드립니다.
>
> Format Field 는 현재 연결에 대한 전체 포맷을 지정합니다. 따라서 `SIMPLE` 포맷으로 웹소켓 데이터를 수신하다가 `LIST_SUBSCRIPTIONS` 요청을 `DEFAULT` 포맷으로 요청할 경우, 이전에 요청한 데이터가 `DEFAULT` 포맷으로 변경되어 내려가게 됩니다.

# Response   [Skip link to Response](https://docs.upbit.com/kr/reference/list-subscriptions\#response)

| 필드명 | 축약형 (format: SIMPLE) | 내용 | 타입 | 값 |
| --- | --- | --- | --- | --- |
| method | mthd | 요청 메서드 | String | `LIST_SUBSCRIPTIONS` |
| result | rslt | 요청 결과 | List of Objects |  |
| result.type | rslt.ty | 데이터 타입 | String |  |
| result.codes | rslt.cds | 마켓 코드 리스트 | List of String |  |
| result.level | rslt.lv | 호가 모아보기 단위 | Double |  |
| ticket | tckt | 요청자를 식별할 수 있는 값 | Long |  |

> ## ❗️  주의 사항 \- 요청 수 제한
>
> `LIST_SUBSCRIPTIONS` 역시 요청 수 제한에 포함됩니다. 자세한 기준은 [요청 수 제한 페이지](https://docs.upbit.com/kr/docs/user-request-guide) 의 "WebSocket 데이터 요청"을 참고하시길 바랍니다.

# Example   [Skip link to Example](https://docs.upbit.com/kr/reference/list-subscriptions\#example)

### Request   [Skip link to Request](https://docs.upbit.com/kr/reference/list-subscriptions\#request-1)

예제 1\. `LIST_SUBSCRIPTIONS` 요청

JSON

```rdmd-code lang-json theme-light

[\
  {\
    "method": "LIST_SUBSCRIPTIONS"\
  },\
  {\
    "ticket": "unique uuid"\
  }\
]

```

### Response   [Skip link to Response](https://docs.upbit.com/kr/reference/list-subscriptions\#response-1)

예제 1\. public 데이터

JSON

```rdmd-code lang-json theme-light

{
  "method": "LIST_SUBSCRIPTIONS",
  "result": [\
    {\
      "type": "ticker",\
      "codes": ["KRW-BTC", "KRW-ETH"]\
    },\
    {\
      "type": "orderbook",\
      "codes": ["KRW-BTC", "KRW-ETH"],\
      "level": 0\
    }\
  ],
  "ticket": "unique uuid"
}

```

예제 2\. private 데이터

JSON

```rdmd-code lang-json theme-light

{
  "method": "LIST_SUBSCRIPTIONS",
  "result": [\
    {\
      "type": "myAsset"\
    },\
    {\
      "type": "myOrder",\
      "codes": ["KRW-BTC", "KRW-ETH"]\
    }\
  ],
  "ticket": "unique uuid"
}

```

Updated 9 months ago

* * *

Did this page help you?

Yes

No

Updated 9 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference_connection.md]
# Connection 관리   [Skip link to Connection 관리](https://docs.upbit.com/kr/reference/connection\#connection-%EA%B4%80%EB%A6%AC)

### PING/PONG   [Skip link to PING/PONG](https://docs.upbit.com/kr/reference/connection\#pingpong)

업비트 OpenAPI WebSocket 서버는 2019년 3월 27일부터 안정적인 커넥션 관리와 유지를 위해 WebSocket PING/PONG Frame을 지원합니다.

(참고 문서 : [https://tools.ietf.org/html/rfc6455#section-5.5.2](https://tools.ietf.org/html/rfc6455#section-5.5.2) )

#### Client to Server PING   [Skip link to Client to Server PING](https://docs.upbit.com/kr/reference/connection\#client-to-server-ping)

- 서버에서는 기본적으로 아무런 데이터도 수/발신 되지 않은 채 약 120초가 경과하면 Idle Timeout으로 WebSocket Connection을 종료합니다.
- 이를 방지하기 위해 클라이언트에서 서버로 PING 메시지를 보내서 Connection을 유지하고, WebSocket 서버의 상태와 WebSocket Connection Status를 파악할 수 있습니다.
- 현재 업비트 OpenAPI WebSocket 서버에서는 **PING Frame 수신 대응 준비가 되어있는 상황** 이며, 클라이언트에서 간단한 구현으로 PING 요청/PONG 응답 _(PING에 대한 응답 Frame)_ 을 통해 서버의 상태를 파악할 수 있습니다.
- 이에 대한 구성은 해당 클라이언트 개발문서를 참고 바랍니다.


(대부분 라이브러리의 경우, ping 함수가 내장되어 있을 가능성이 큽니다.)

> ## 📘  v1.1.6 PING Frame 요청이 어려운 경우
>
> 다른 방법으로는 `PING` 메시지를 보냄으로써 Connection을 유지할 수 있습니다.
>
> 정상적으로 Connection이 유지되어 있을 경우 10초 간격으로 `{"status":"UP"}` 응답이 오게됩니다.
>
> ```rdmd-code lang- theme-light
> $ telsocket -url wss://api.upbit.com/websocket/v1
> Connected!
> PING
> {"status":"UP"}
> {"status":"UP"}
> {"status":"UP"}
> ...
>
> ```

# WebSocket Compression   [Skip link to WebSocket Compression](https://docs.upbit.com/kr/reference/connection\#websocket-compression)

업비트 OpenAPI WebSocket 서버에서는 더 빠른 데이터 전송을 위해 WebSocket Compression을 제공하고 있습니다.

(참고 문서 : [https://tools.ietf.org/html/rfc7692](https://tools.ietf.org/html/rfc7692) )

- WebSocket Compression을 지원하는 WebSocket 클라이언트에서는, 클라이언트별로 정해진 옵션을 활성화하면 압축된 상태로 통신이 지속됩니다. 사용자의 코드 레벨에는 압축 해제된 상태의 raw data가 제공되기 때문에 **사용자는 설정 옵션 활성화 외에 다른 대응 코드를 작성할 필요가 없습니다.**
- WebSocket Compression을 지원하지 않는 WebSocket 클라이언트 에서는 해당 기능을 사용할 수 없으며, Raw JSON 형태의 데이터를 주고받게 됩니다. 해당 기능을 사용하기 위해서는 WebSocket Client 교체가 필요합니다.

Updated almost 2 years ago

* * *

Did this page help you?

Yes

No

Updated almost 2 years ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference_id_EB_A1_9C__EC_A3_BC_EB_AC_B8__EC_A1_B0_ED_9A_8C.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/id%EB%A1%9C-%EC%A3%BC%EB%AC%B8-%EC%A1%B0%ED%9A%8C\#request-parameters)

> ## 📘  해당 API를 통해 **uuid**(또는 **identifier**) 기준으로 주문을 조회할 수 있습니다.
>
> 마켓 아이디(종목) 기준의 조회가 필요하신 경우 주문 상태에 따라
>
> - [체결 대기 주문](https://docs.upbit.com/kr/reference/%EB%8C%80%EA%B8%B0-%EC%A3%BC%EB%AC%B8-%EC%A1%B0%ED%9A%8C) ( `v1/orders/open`) 조회 혹은
> - [종료된 주문](https://docs.upbit.com/kr/reference/%EC%A2%85%EB%A3%8C-%EC%A3%BC%EB%AC%B8-%EC%A1%B0%ED%9A%8C) ( `v1/orders/closed`) 조회기능을 이용해 주세요.
>
>
>   \*시간기준 조회 필요시 해당 기능을 이용해 주세요

| Name | 설명 | 타입 |
| --- | --- | --- |
| market | 마켓 ID | String |
| uuids\[\]\* | 주문 UUID의 목록 (최대 100개) | Array\[String\] |
| identifiers\[\]\* | 주문 identifier의 목록 (최대 100개)<br>\*uuids 또는 identifiers 중 **한 가지 필드는 필수** 이며, **두 가지 필드를 함께 사용할 수 없습니다**. | Array\[String\] |
| order\_by | 정렬 방식<br>\- `asc` : 오름차순<br>\- `desc` : 내림차순 **(default)** | String |

\*표시된 필드는 요청 시 필수 입력입니다.

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/id%EB%A1%9C-%EC%A3%BC%EB%AC%B8-%EC%A1%B0%ED%9A%8C\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| uuid | 주문의 고유 아이디 | String |
| side | 주문 종류 | String |
| ord\_type | 주문 방식<br>\- `limit` : 지정가 주문<br>\- `price` : 시장가 주문(매수)<br>\- `market` : 시장가 주문(매도)<br>\- `best` : [최유리 주문](https://docs.upbit.com/kr/changelog/new_ord_type_expand) | String |
| price | 주문 당시 화폐 가격 | NumberString |
| state | 주문 상태 | String |
| market | 마켓 ID | String |
| created\_at | 주문 생성 시간 | DateString |
| volume | 사용자가 입력한 주문 양 | NumberString |
| remaining\_volume | 체결 후 남은 주문 양 | NumberString |
| reserved\_fee | 수수료로 예약된 비용 | NumberString |
| remaining\_fee | 남은 수수료 | NumberString |
| paid\_fee | 사용된 수수료 | NumberString |
| locked | 거래에 사용 중인 비용 | NumberString |
| executed\_volume | 체결된 양 | NumberString |
| executed\_funds | 현재까지 체결된 금액 | NumberString |
| trades\_count | 해당 주문에 걸린 체결 수 | Integer |
| time\_in\_force | [IOC, FOK 설정](https://docs.upbit.com/kr/changelog/new_ord_type_expand)<br>\- `ioc` : Immediate or Cancel<br>\- `fok` : Fill or Kill | String |
| identifier | 조회용 사용자 지정값<br>\*identifier 필드는 2024-10-18 이후에 생성된 주문에 대해서만 제공합니다. | String |

\*null인 필드는 응답에서 제외됩니다. (예: IOC or FOK 설정이 없었던 주문의 경우 해당 필드는 응답되지 않습니다.

market

string

마켓 아이디

uuids\[\]

array of strings

required

주문 UUID의 목록

uuids\[\]\*
ADD string

identifiers\[\]

array of strings

required

주문 identifier의 목록

identifiers\[\]\*
ADD string

order\_by

string

Defaults to desc

정렬 방식

Authorization

string

Authorization token (JWT)

# `` 200      200

json

# `` 4XX      4XX

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

NodePythonRubyJava

```

xxxxxxxxxx

47

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const queryEncode = require("querystring").encode

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11

const uuids = [\
\
12    '9ca023a5-851b-4fec-9f0a-48cd83c2eaae',\
\
13    //...\
\
14]

15​

16

const array_body = {

17    uuids: uuids,

18}

19

const body = {

20    ...array_body

21}

22​

23const query = uuids.map(uuid => `uuids[]=${uuid}`).join('&')

24​

25const hash = crypto.createHash('sha512')

26const queryHash = hash.update(query, 'utf-8').digest('hex')

```

```

xxxxxxxxxx

21



1

[\
\
2\
\
  {\
\
3    "uuid": "d098ceaf-6811-4df8-97f2-b7e01aefc03f",\
\
4    "side": "bid",\
\
5    "ord_type": "limit",\
\
6    "price": "104812000",\
\
7    "state": "wait",\
\
8    "market": "KRW-BTC",\
\
9    "created_at": "2024-06-13T10:26:21+09:00",\
\
10    "volume": "0.00101749",\
\
11    "remaining_volume": "0.00006266",\
\
12    "reserved_fee": "53.32258094",\
\
13    "remaining_fee": "3.28375996",\
\
14    "paid_fee": "50.03882098",\
\
15    "locked": "6570.80367996",\
\
16    "executed_volume": "0.00095483",\
\
17    "executed_funds": "100077.64196",\
\
18    "trades_count": 1\
\
19  }\
\
20  # ....\
\
21]

```

Updated about 1 month ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference_open_api__ED_82_A4__EB_A6_AC_EC_8A_A4_ED_8A_B8__EC_A1_B0_ED_9A_8C.md]
> ## ❗️  v1.4.1 업데이트 : 요청 수 제한 정책 '계정 단위'로 변경 (적용 일자 2023.10.24)
>
> - Exchange API는 개별 Open API Key에 대해 요청 수를 제한해 왔으나 변경 이후 계정 단위로 요청 횟수가 측정됩니다.
> - 분당 요청 수 제한이 없어지고, 초당으로만 책정하게 되며 실질적인 분당 요청량이 늘었습니다.
>   - 기존 주문요청 API 분당 200회 → 분당 480회로 상향
>   - 주문요청 외 API 분당 900회 → 분당 1,800회로 상향
>
> 자세한 변경사항은 [공지사항](https://docs.upbit.com/kr/changelog/change_on_ratelimit) 을 참조해주세요.

- Open API를 사용하기 위해선 사용기능 선택과 사용하실 IP 주소를 반드시 입력해야 Open API Key 발급이 가능합니다. Key발급과 관리는 [해당페이지](https://upbit.com/mypage/open_api_management) 에서 가능합니다.
- Open API Key 발급 당시 입력한 IP 주소로만 접속해야 Open API 사용이 가능하며, Key당 최대 5개까지 등록할 수 있습니다.
- Open API Key는 계정당 10개까지 발급이 가능합니다.
- Secret key는 최초 1회에 한해 발급되며 추가로 확인하실 수 없으니, 발급받으신 Secret key는 반드시 안전한 곳에 별도로 보관하여 주시기 바랍니다.
- Open API Key 토큰의 유효 기간은 1년이며 연장은 불가합니다. 유효 기간 만료 후 Open API Key를 삭제하여 추가로 발급받아 주시기 바랍니다.
- Open API Key 발급, 수정 및 삭제 시에는 2채널 추가 인증이 필요하며, 필요한 기능의 변경 발생 시에는 [Open API Key 관리](https://upbit.com/mypage/open_api_management) 에서 해당 Key를 삭제하신 뒤 다시 등록해 주시기 바랍니다.

# `` 200      200

array of objects

object

access\_key

string

expire\_at

string

# `` 400      400

object

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

25

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const sign = require('jsonwebtoken').sign

4​

5const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

6const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

7const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

8​

9

const payload = {

10    access_key: access_key,

11    nonce: uuidv4(),

12}

13​

14const token = sign(payload, secret_key)

15​

16

const options = {

17    method: "GET",

18    url: server_url + "/v1/api_keys",

19    headers: {Authorization: `Bearer ${token}`},

20}

21​

22

request(options, (error, response, body) => {

23    if (error) throw new Error(error)

24    console.log(body)

25})

```

```

xxxxxxxxxx



1

[\
\
2\
\
  {\
\
3    "access_key": "xxxxxxxxxxxxxxxxxxxxxxxx",\
\
4    "expire_at": "2021-03-09T12:39:39+00:00"\
\
5  }\
\
6]

```

Updated 3 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__ED_8A_B8_EB_9E_98_EB_B8_94_EB_A3_B0__EA_B2_80_EC_A6_9D.md]
# 업비트 계정주 확인 서비스는 무엇인가요?   [Skip link to 업비트 계정주 확인 서비스는 무엇인가요?](https://docs.upbit.com/kr/reference/%ED%8A%B8%EB%9E%98%EB%B8%94%EB%A3%B0-%EA%B2%80%EC%A6%9D\#%EC%97%85%EB%B9%84%ED%8A%B8-%EA%B3%84%EC%A0%95%EC%A3%BC-%ED%99%95%EC%9D%B8-%EC%84%9C%EB%B9%84%EC%8A%A4%EB%8A%94-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80%EC%9A%94)

- VV(베리파이바스프) 트래블룰 솔루션을 통해 가상자산사업자(VASP) 간 시스템을 연동하여 업비트 계정과 연동된 거래소의 계정, 즉 **상호 계정의 계정주 동일 여부를 확인하는 서비스** 입니다.
- [계정주 확인 서비스에 연동된 거래소](https://upbitcs.zendesk.com/hc/ko/articles/5048002559897-%EC%9E%85%EC%B6%9C%EA%B8%88-%EA%B0%80%EB%8A%A5-%EA%B0%80%EC%83%81%EC%9E%90%EC%82%B0%EC%82%AC%EC%97%85%EC%9E%90-%EB%A6%AC%EC%8A%A4%ED%8A%B8) 계정의 계정주와 업비트 계정의 계정주 성명(한글 또는 영문) 및 생년월일 정보가 일치하면 정상적으로 입출금이 완료됩니다.

# Open API를 통해 계정주 확인을 할 수 있습니다   [Skip link to Open API를 통해 계정주 확인을 할 수 있습니다](https://docs.upbit.com/kr/reference/%ED%8A%B8%EB%9E%98%EB%B8%94%EB%A3%B0-%EA%B2%80%EC%A6%9D\#open-api%EB%A5%BC-%ED%86%B5%ED%95%B4-%EA%B3%84%EC%A0%95%EC%A3%BC-%ED%99%95%EC%9D%B8%EC%9D%84-%ED%95%A0-%EC%88%98-%EC%9E%88%EC%8A%B5%EB%8B%88%EB%8B%A4)

1. [트래블룰 검증 가능 해외 거래소 리스트](https://docs.upbit.com/kr/reference/%ED%8A%B8%EB%9E%98%EB%B8%94%EB%A3%B0-%EA%B0%80%EB%8A%A5-%EA%B1%B0%EB%9E%98%EC%86%8C) 에서 입금하고자 하시는 해외 거래소의 uuid를 찾으시고
2. 트래블룰 검증요청을 하시면 됩니다.
1. [입금 uuid로 검증하고 싶으신 경우 해당 문서](https://docs.upbit.com/kr/reference/%ED%8A%B8%EB%9E%98%EB%B8%94%EB%A3%B0-uuid) 를 참고해 주세요.
2. [입금 TxID로 검증하고 싶으신 경우 해당 문서](https://docs.upbit.com/kr/reference/%ED%8A%B8%EB%9E%98%EB%B8%94%EB%A3%B0-txid) 를 참고해 주세요.

Updated 3 months ago

* * *

Did this page help you?

Yes

No

Updated 3 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EC_B6_9C_EA_B8_88__EA_B0_80_EB_8A_A5__EC_A0_95_EB_B3_B4.md]
## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EC%B6%9C%EA%B8%88-%EA%B0%80%EB%8A%A5-%EC%A0%95%EB%B3%B4\#response)

> ## ❗️  v1.4.1 업데이트 : 2채널 인증 '카카오 페이 인증' 종료 (적용 완료)
>
> - 출금 가능 정보 API 응답의 `member_level.kakao_pay_auth_verified` 필드가 삭제되었습니다.
> - `two_factor_auth_verified` 필드를 통해 2FA 인증 수단의 활성화 여부를 확인하실 수 있습니다. 2FA 인증 수단 중 하나 이상이 활성화 되어 있을 경우 True로 안내됩니다.
>
> 자세한 변경사항은 [공지사항](https://docs.upbit.com/kr/changelog/kakao_auth) 을 참조해주세요.

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
| currency.wallet\_state | 해당 화폐의 지갑 상태<br>\*입출금 지원 여부를 나타내며, 현시점의 **입출금 '가능'여부를 보시고 싶은 경우 아래의 currency.wallet\_support** 를 참고하시기를 바랍니다. | String |
| currency.wallet\_support | 해당 화폐 입출금 가능 여부<br>\***입금가능한 상태인 경우 'deposit'**, **출금가능한 상태인 경우 'withdraw'** 가 추가되며, **빈 리스트일 경우 입출금 모두 불가** 한 상태입니다. | Array\[String\] |
| account | 사용자의 계좌 정보 | Object |
| account.currency | 화폐를 의미하는 영문 대문자 코드 | String |
| account.balance | 주문가능 금액/수량 | NumberString |
| account.locked | 주문 중 묶여있는 금액/수량 | NumberString |
| account.avg\_buy\_price | 매수평균가 | NumberString |
| account.avg\_buy\_price\_modified | 매수평균가 수정 여부 | Boolean |
| account.unit\_currency | 평단가 기준 화폐 | String |
| withdraw\_limit | 출금 제약 정보 | Object |
| withdraw\_limit.currency | 화폐를 의미하는 영문 대문자 코드 | String |
| withdraw\_limit.minimum | 출금 최소 금액/수량 | NumberString |
| withdraw\_limit.onetime | 1회 출금 한도 (\*Deprecated) | NumberString |
| withdraw\_limit.daily | 1일 출금 한도 (\*Deprecated) | NumberString |
| withdraw\_limit.remaining\_daily | 1일 잔여 출금 한도 (\*Deprecated) | NumberString |
| withdraw\_limit.remaining\_daily\_krw | 통합 1일 잔여 출금 한도 (\*Deprecated) | NumberString |
| withdraw\_limit.remaining\_daily\_fiat | 통합 1일 잔여 출금 한도<br>**\*출금 한도는 해당 필드로 확인해주시기 바랍니다.** | NumberString |
| withdraw\_limit.fiat\_currency | 해당 자산을 구매할 수 있는 법정 화폐 (KRW) | String |
| withdraw\_limit.withdraw\_delayed\_fiat | [24시간 출금지연제](https://upbit.com/service_center/notice?id=1621) 에 의해 출금 제한되어 있는 금액 | NumberString |
| withdraw\_limit.fixed | 출금 금액/수량 소수점 자리 수 | Integer |
| withdraw\_limit.can\_withdraw | 출금 지원 여부<br>\*해당 자산에 대한 출금을 '지원'하는지에 대한 정보이며 **현재 출금 '가능'여부를 확인하시고 싶은 경우 currency.wallet\_support에 'withdraw'의 존재 여부로 확인하실 수 있습니다.** | Boolean |

currency

string

required

Currency symbol

net\_type

string

required

출금 네트워크

Authorization

string

required

Authorization token (JWT)

# `` 200      200

json

# `` 4XX      4XX

object

error

object

name

string

message

string

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

40

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const queryEncode = require("querystring").encode

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11

const body = {

12    currency: 'BTC',

13    net_type: 'BTC'

14}

15​

16const query = queryEncode(body)

17​

18const hash = crypto.createHash('sha512')

19const queryHash = hash.update(query, 'utf-8').digest('hex')

20​

21

const payload = {

22    access_key: access_key,

23    nonce: uuidv4(),

24    query_hash: queryHash,

25    query_hash_alg: 'SHA512',

26}

```

```

xxxxxxxxxx

30
  'remaining_daily_krw': '5000000000.0'}}

1

{'member_level': {'security_level': 0,

2  'fee_level': 0,

3  'email_verified': True,

4  'identity_auth_verified': True,

5  'bank_account_verified': False,

6  'two_factor_auth_verified': True,

7  'locked': False,

8  'wallet_locked': False},

9

 'currency': {'code': 'BTC',

10  'withdraw_fee': '0.0008',

11  'is_coin': True,

12  'wallet_state': 'working',

13  'wallet_support': ['deposit', 'withdraw']},

14

 'account': {'currency': 'BTC',

15  'balance': '0.0',

16  'locked': '0.0',

17  'avg_buy_price': '0',

18  'avg_buy_price_modified': False,

19  'unit_currency': 'KRW'},

20

 'withdraw_limit': {'currency': 'BTC',

21  'onetime': '50.0',

22  'daily': None,

23  'remaining_daily': '0.0',

24  'remaining_daily_fiat': '5000000000.0',

25  'fiat_currency': 'KRW',

```

Updated 3 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EC_B4_88second__EC_BA_94_EB_93_A4.md]
> ## 📘  초봉 지원 범위
>
> 초봉 API는 `요청 시점으로부터 최근 3개월 이내` 의 초봉을 제공합니다. 초봉 API 가 빈 리스트를 반환하거나, 요청한 개수 만큼 반환하지 않는 경우 `to` 파라미터를 확인해 보세요.

## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EC%B4%88second-%EC%BA%94%EB%93%A4\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 마켓 코드 (ex. KRW-BTC) | String |
| to | 마지막 캔들 시각 (exclusive).<br>ISO8061 포맷 (yyyy-MM-dd'T'HH:mm:ss'Z' or yyyy-MM-dd HH:mm:ss). 기본적으로 UTC 기준 시간이며 `2023-01-01T00:00:00+09:00` 과 같이 KST 시간으로 요청 가능.<br>비워서 요청시 가장 최근 캔들 | String |
| count | 캔들 개수(최대 200개까지 요청 가능) | Integer |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EC%B4%88second-%EC%BA%94%EB%93%A4\#response)

> ## 🚧  캔들은 해당 시간대에 체결이 발생한 경우에만 생성됩니다.
>
> - candle\_date\_time이 2024-08-31T22:25:00인 초봉 캔들은 2024-08-31T22:25:00 (이상) ~ 2024-08-31T22:25:01 (미만) 사이의 체결로 구성됩니다.
> - 해당 시간 동안 체결이 없을 경우, 2024-08-31T22:25:00 캔들은 생성되지 않으며 응답에 포함되지 않습니다.

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 종목 코드 | String |
| candle\_date\_time\_utc | 캔들 기준 시각(UTC 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |
| candle\_date\_time\_kst | 캔들 기준 시각(KST 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |
| opening\_price | 시가 | Double |
| high\_price | 고가 | Double |
| low\_price | 저가 | Double |
| trade\_price | 종가 | Double |
| timestamp | 마지막 틱이 저장된 시각 | Long |
| candle\_acc\_trade\_price | 누적 거래 금액 | Double |
| candle\_acc\_trade\_volume | 누적 거래량 | Double |

market

string

required

종목 코드 (ex. KRW-BTC)

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

# `` 400      400

object

Updated 25 days ago

* * *

Did this page help you?

Yes

No

ShellPythonNode

```

xxxxxxxxxx

10

1# KRW-BTC 마켓에 가장 최근 초봉 1개를 요청

2curl --request GET \

3     --url 'https://api.upbit.com/v1/candles/seconds?market=KRW-BTC&count=1' \

4     --header 'accept: application/json'

5​

6# KRW-BTC 마켓에 2024년 10월 1일(UTC) 이전 초봉 1개를 요청

7curl --request GET \

8     --url 'https://api.upbit.com/v1/candles/seconds?market=KRW-BTC&count=1&to=2024-10-01%2000%3A00%3A00' \

9     --header 'accept: application/json'

10

```

```

xxxxxxxxxx

14



1

[\
\
2\
\
  {\
\
3    "market": "KRW-BTC",\
\
4    "candle_date_time_utc": "2024-07-30T09:32:41",\
\
5    "candle_date_time_kst": "2024-07-30T18:32:41",\
\
6    "opening_price": 93557000,\
\
7    "high_price": 93557000,\
\
8    "low_price": 93551000,\
\
9    "trade_price": 93551000,\
\
10    "timestamp": 1722331961297,\
\
11    "candle_acc_trade_price": 485957.73742,\
\
12    "candle_acc_trade_volume": 0.0051944\
\
13  }\
\
14]

```

Updated 25 days ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference_general_info.md]
# 1\. API 정보   [Skip link to 1. API 정보](https://docs.upbit.com/kr/reference/general-info\#1-api-%EC%A0%95%EB%B3%B4)

- public 타입: `wss://api.upbit.com/websocket/v1`
- private 타입: `wss://api.upbit.com/websocket/v1/private`

# 2\. Rate limit   [Skip link to 2. Rate limit](https://docs.upbit.com/kr/reference/general-info\#2-rate-limit)

- [요청 수 제한 페이지](https://docs.upbit.com/kr/docs/user-request-guide) 참고

# 3\. 데이터 타입   [Skip link to 3. 데이터 타입](https://docs.upbit.com/kr/reference/general-info\#3-%EB%8D%B0%EC%9D%B4%ED%84%B0-%ED%83%80%EC%9E%85)

각각의 정보는 `스냅샷` 과 `실시간` 데이터로 나뉘며 요청 방법에 따라 수신할 수 있는 데이터가 달라집니다.

`스냅샷` 정보란 요청 당시의 상태를 의미합니다.

`실시간` 정보란 요청 정보가 스트림 형태로 지속적으로 제공되는 것을 의미합니다.

WebSocket을 이용하여 `스냅샷` 정보와 `실시간` 정보를 요청할 수 있으며 둘 중 하나의 정보만을 요청할 수도 있습니다.

### Public 타입   [Skip link to Public 타입](https://docs.upbit.com/kr/reference/general-info\#public-%ED%83%80%EC%9E%85)

별다른 인증 없이 수신할 수 있는 데이터 타입입니다.

- `ticker`: 현재가 (스냅샷, 실시간 정보 제공)
- `trade`: 체결 (스냅샷, 실시간 정보 제공)
- `orderbook`: 호가 (스냅샷, 실시간 정보 제공)
- `candle.1s`: 초봉 (스냅샷, 실시간 정보 제공)

### Private 타입   [Skip link to Private 타입](https://docs.upbit.com/kr/reference/general-info\#private-%ED%83%80%EC%9E%85)

인증을 해야만 수신할 수 있는 데이터 타입입니다.

인증에 대한 자세한 내용은 [Websocket > 요청 방법](https://docs.upbit.com/kr/reference/websocket-request-format) 페이지를 참고하시기 바랍니다.

- `myOrder`: 내 주문 (실시간 정보 제공)
- `myAsset`: 내 자산 (실시간 정보 제공)

Updated 4 months ago

* * *

Did this page help you?

Yes

No

Updated 4 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference_websocket_myasset.md]
> ## 📘  Private 타입 endpoint
>
> 새롭게 추가된 `myOrder` 와 `myAsset` 타입의 경우 `wss://api.upbit.com/websocket/v1/private` 으로 요청하셔야 합니다. 자세한 내용은 [기본 정보](https://docs.upbit.com/kr/reference/general-info) 를 참고해주시기 바랍니다.

# Request   [Skip link to Request](https://docs.upbit.com/kr/reference/websocket-myasset\#request)

요청은 JSON Object를 이용하며 응답 또한 JSON Object 입니다. 요청은 크게 ticket field, type field, format field 로 나누어지며 하나의 요청에 여러 개의 type field 를 명시할 수 있습니다. ticket field 와 format field 에 대해서는 [요청 방법 및 포맷](https://docs.upbit.com/kr/reference/websocket-request-format) 을 참고해주시기 바랍니다.

> ## 📘  Request format
>
> **\[{Ticket Field},{Type Field},....,{Type Field},{Format Field}\]**

### **Type Field**   [Skip link to [object Object]](https://docs.upbit.com/kr/reference/websocket-myasset\#type-field)

수신하고 싶은 시세 정보를 나열하는 필드입니다.

| 필드명 | 타입 | 내용 | 필수 여부 | 기본 값 |
| --- | --- | --- | --- | --- |
| type | String | 데이터 타입<br>- `myAsset`: 내 자산 | O |  |

# Response   [Skip link to Response](https://docs.upbit.com/kr/reference/websocket-myasset\#response)

> ## ❗️  `myAsset` 타입의 경우 특정 이벤트가 발생할 때만 데이터를 전송합니다.
>
> 따라서, **연결 후 즉시 데이터가 수신되지 않는 경우는 정상적인 동작** 입니다. 주문의 체결/입출금과 같이 자산이 변동되는 이벤트가 발생할 때 데이터가 전송됩니다.
>
> 데이터 없이도 연결을 유지하고 싶으신 경우 [주기적으로 ping/pong 을 통해 connection 관리](https://docs.upbit.com/kr/reference/connection) 를 하실 수 있습니다.

| 필드명 | 축약형 (format: SIMPLE) | 내용 | 타입 | 값 |
| --- | --- | --- | --- | --- |
| type | ty | 타입 | String | `myAsset` : 내 자산 |
| asset\_uuid | astuid | 자산 고유 아이디 | String |  |
| assets | ast | 자산 리스트 | List of Objects |  |
| assets.currency | ast.cu | 화폐를 의미하는 영문 대문자 코드 | String |  |
| assets.balance | ast.b | 주문가능 수량 | Double |  |
| assets.locked | ast.l | 주문 중 묶여있는 수량 | Double |  |
| asset\_timestamp | asttms | 자산 타임스탬프 (millisecond) | Long |  |
| timestamp | tms | 타임스탬프 (millisecond) | Long |  |
| stream\_type | st | 스트림 타입 | String | `REALTIME` : 실시간 |

> ## 🚧  최초 이용 시 주의 사항
>
> 최초 이용 시 수 분간 데이터 전송이 이뤄지지 않을 수 있습니다. 따라서 개발 시 데이터 수신을 1회 꼭 확인하시길 바랍니다.
>
> 예를 들어 2024년 5월 1일 00시 00분 최초 이용 시 자산 변동이 있더라도 00시 05분부터 데이터를 전송받을 수 있습니다. 이후 00시 10분에 재접속을 할 경우 이는 최초 이용이 아니므로 자산 변동 시 바로 데이터를 수신하실 수 있습니다.

# Example   [Skip link to Example](https://docs.upbit.com/kr/reference/websocket-myasset\#example)

### Request   [Skip link to Request](https://docs.upbit.com/kr/reference/websocket-myasset\#request-1)

예제 1\. 모든 마켓 정보 수신

**\*주의사항: codes 필드를 요청하실 수 없습니다. 이 경우 `WRONG_FORMAT` 에러가 내려가게 됩니다.**

JSON

```rdmd-code lang-json theme-light

[\
  {\
    "ticket": "test-myAsset"\
  },\
  {\
    "type": "myAsset"\
  }\
]

```

### Response   [Skip link to Response](https://docs.upbit.com/kr/reference/websocket-myasset\#response-1)

JSON

```rdmd-code lang-json theme-light

{
  "type": "myAsset",
  "asset_uuid": "e635f223-1609-4969-8fb6-4376937baad6",
  "assets": [\
    {\
      "currency": "KRW",\
      "balance": 1386929.37231066771348207123,\
      "locked": 10329.670127489597585685\
    }\
  ],
  "asset_timestamp": 1710146517259,
  "timestamp": 1710146517267,
  "stream_type": "REALTIME"
}

```

Updated 3 months ago

* * *

Did this page help you?

Yes

No

Updated 3 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__ED_8A_B8_EB_9E_98_EB_B8_94_EB_A3_B0_txid.md]
> ## 📘  1회의 요청으로 계정주 확인\*이 가능합니다. 검증에 실패한 경우, 업비트와 상대 거래소의 계정 정보 동일 여부를 다시 확인하고 요청해 주세요.
>
> - 트래블룰 정보 검증에 성공하면 입금 반영을 진행합니다.
> - 해당 입금 건이 아직 처리 중인 경우, 입금 처리가 완료된 후에 반영이 진행됩니다.
> - **동일한 입금 건**(상대 거래소 UUID, 입금 TxID, 화폐, 네트워크 타입 조합이 동일)에 대해서 **10분당 1회 요청**이 가능합니다.
>
> [_\*계정주 확인 서비스에 대한 자세한 내용은 링크를 참고해 주세요_](https://upbitcs.zendesk.com/hc/ko/articles/5127318107033-%EA%B3%84%EC%A0%95%EC%A3%BC-%ED%99%95%EC%9D%B8-%EC%84%9C%EB%B9%84%EC%8A%A4%EA%B0%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80%EC%9A%94)

## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%ED%8A%B8%EB%9E%98%EB%B8%94%EB%A3%B0-txid\#request-parameters)

| Name | 설명 | 타입 |
| --- | --- | --- |
| vasp\_uuid \* | 상대 거래소 UUID<br>\* [계정주 확인 가능 거래소 리스트 조회](https://docs.upbit.com/kr/reference/%ED%8A%B8%EB%9E%98%EB%B8%94%EB%A3%B0-%EA%B0%80%EB%8A%A5-%EA%B1%B0%EB%9E%98%EC%86%8C) 에서 확인하실 수 있습니다 | String |
| txid | 입금 TxID | String |
| currency | 입금 화폐 | String |
| net\_type | 입금 네트워크 타입<br>\* [입금 리스트 조회](https://docs.upbit.com/kr/reference/%EC%9E%85%EA%B8%88-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C) 혹은 [입출금 현황](https://docs.upbit.com/kr/reference/%EC%9E%85%EC%B6%9C%EA%B8%88-%ED%98%84%ED%99%A9) 에서 적절한 네트워크 타입을 찾아 넣어주세요 | String |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%ED%8A%B8%EB%9E%98%EB%B8%94%EB%A3%B0-txid\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| deposit\_uuid | 입금 UUID | String |
| deposit\_state | 입금 상태 | String |
| verification\_result | 검증 결과 | String |

vasp\_uuid

string

required

상대 거래소 UUID

txid

string

입금 TxID

currency

string

입금 화폐

net\_type

string

입금 네트워크 타입

Authorization

string

required

Authorization token (JWT)

# `` 201      201

object

deposit\_uuid

string

verification\_result

string

deposit\_state

string

# `` 4XX      4XX

object

error

object

name

string

message

string

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

42

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const queryEncode = require("querystring").encode

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11

const body = {

12    vasp_uuid: '00000000-0000-0000-0000-000000000000',

13    txid: '4a5e1e4baab89f3a32518a88c31bc87f618f76673e2cc77ab2127b7afdeda33b',

14    currency: 'BTC',

15    net_type: 'BTC',

16}

17​

18const query = queryEncode(body)

19​

20const hash = crypto.createHash('sha512')

21const queryHash = hash.update(query, 'utf-8').digest('hex')

22​

23

const payload = {

24    access_key: access_key,

25    nonce: uuidv4(),

26    query_hash: queryHash,

```

```

xxxxxxxxxx



1

{

2  "deposit_uuid": "00000000-0000-0000-0000-000000000000",

3  "verification_result": "verified",

4  "deposit_state": "PROCESSING"

5}

```

Updated 3 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference_ticker_ED_98_84_EC_9E_AC_EA_B0_80__EC_A0_95_EB_B3_B4.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/ticker%ED%98%84%EC%9E%AC%EA%B0%80-%EC%A0%95%EB%B3%B4\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| markets \* | 반점으로 구분되는 종목 코드 (ex. KRW-BTC, BTC-ETH) | String |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/ticker%ED%98%84%EC%9E%AC%EA%B0%80-%EC%A0%95%EB%B3%B4\#response)

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
| prev\_closing\_price | 전일 종가(UTC 0시 기준) | Double |
| change | EVEN : 보합<br>RISE : 상승<br>FALL : 하락 | String |
| change\_price | 변화액의 절대값 | Double |
| change\_rate | 변화율의 절대값 | Double |
| signed\_change\_price | 부호가 있는 변화액 | Double |
| signed\_change\_rate | 부호가 있는 변화율 | Double |
| trade\_volume | 가장 최근 거래량 | Double |
| acc\_trade\_price | 누적 거래대금(UTC 0시 기준) | Double |
| acc\_trade\_price\_24h | 24시간 누적 거래대금 | Double |
| acc\_trade\_volume | 누적 거래량(UTC 0시 기준) | Double |
| acc\_trade\_volume\_24h | 24시간 누적 거래량 | Double |
| highest\_52\_week\_price | 52주 신고가 | Double |
| highest\_52\_week\_date | 52주 신고가 달성일<br>포맷: `yyyy-MM-dd` | String |
| lowest\_52\_week\_price | 52주 신저가 | Double |
| lowest\_52\_week\_date | 52주 신저가 달성일<br>포맷: `yyyy-MM-dd` | String |
| timestamp | 타임스탬프 | Long |

\*위 응답의 change, change\_price, change\_rate, signed\_change\_price, signed\_change\_rate 필드들은 전일종가 대비 값입니다.

markets

string

required

반점으로 구분되는 종목 코드 (ex. KRW-BTC, KRW-ETH)

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

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePython

```

xxxxxxxxxx

14

1const request = require('request')

2​

3const server_url = "https://api.upbit.com"

4​

5

const options = {

6    method: "GET",

7    url: server_url + "/v1/ticker",

8    qs: {markets: "KRW-BTC,KRW-ETH"}

9}

10​

11

request(options, (error, response, body) => {

12    if (error) throw new Error(error)

13    console.log(body)

14})

```

```

xxxxxxxxxx

58
]

1

[\
\
2\
\
  {\
\
3    "market": "KRW-BTC",\
\
4    "trade_date": "20240822",\
\
5    "trade_time": "071602",\
\
6    "trade_date_kst": "20240822",\
\
7    "trade_time_kst": "161602",\
\
8    "trade_timestamp": 1724310962713,\
\
9    "opening_price": 82900000,\
\
10    "high_price": 83000000,\
\
11    "low_price": 81280000,\
\
12    "trade_price": 82324000,\
\
13    "prev_closing_price": 82900000,\
\
14    "change": "FALL",\
\
15    "change_price": 576000,\
\
16    "change_rate": 0.0069481303,\
\
17    "signed_change_price": -576000,\
\
18    "signed_change_rate": -0.0069481303,\
\
19    "trade_volume": 0.00042335,\
\
20    "acc_trade_price": 66058843588.46906,\
\
21    "acc_trade_price_24h": 250206655398.15125,\
\
22    "acc_trade_volume": 803.00214714,\
\
23    "acc_trade_volume_24h": 3047.01625142,\
\
24    "highest_52_week_price": 105000000,\
\
25    "highest_52_week_date": "2024-03-14",\
\
```\
\
Updated 3 months ago\
\
* * *\
\
Did this page help you?\
\
Yes\
\
No\
\
## Open API 이용약관\
\
본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.\
\
제 1조 (목적)\
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.\
\
제 2조 (정의)\
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.\
\
2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.\
\
3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.\
\
제 3조 (면책사항)\
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.\
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.\
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.\
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.\
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.\
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.\
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.\
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.\
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.\
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.\
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.\
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.\
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.\
\
제 4조 (Open API 서비스 제공의 제한 및 해지)\
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.\
1\. 본 이용약관 제6조를 위반한 경우\
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우\
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우\
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우\
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우\
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.\
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.\
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.\
\
제 5조 (저작권)\
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.\
\
제 6조 (사용자의 의무와 책임)\
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.\
1\. API 업데이트 및 변경 사항에 대한 공지\
2\. 제도 변경 공지\
3\. 두나무-업비트 정책 반영에 따른 공지\
4\. 기타 긴급 공지\
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.\
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.\
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.\
\
제 7조 (약관의 변경 등)\
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.\
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).\
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.\
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.\
\
제 8조 (효력 발생 및 유효기간)\
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.\
\
제 9조 (기타)\
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.\
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.\
\
제 10조 (관할법원)\
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.\
\
<부칙>\
본 이용약관은 2024년 10월 30일부터 적용됩니다.\
이전의 이용약관은 아래에서 확인하실 수 있습니다.\
\
\
[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)\
\
[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)\
\
[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)\
\
[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)\
\
동의

[docs_upbit_com_kr_reference__EC_B6_9C_EA_B8_88__ED_97_88_EC_9A_A9__EC_A3_BC_EC_86_8C__EB_A6_AC_EC_8A_A4_ED_8A_B8__EC_A1_B0_ED_9A_8C.md]
> ## 📘  출금 기능을 이용하기 위해서는 주소 등록이 필요합니다.
>
> Open API를 통해 디지털 자산을 출금하기 위해서는 출금 허용 주소 등록이 필요합니다.
>
> 등록은 업비트 웹 \> \[MY\] > \[Open API 관리\] > \[디지털 자산 출금주소 관리\] 페이지에서 진행하실 수 있습니다.

> ## 🚧  네트워크 타입(net\_type) vs. 네트워크 명(network\_name)
>
> - **네트워크 타입( `net_type`)이란?**
>
>
>   디지털 자산 **입출금에 활용되는 블록체인 네트워크** 를 뜻하며, 디지털 자산의 종류에 따라 활용되는 네트워크(체인)가다를 수 있습니다. **_\*네트워크가 일치하지 않는 경우 정상 입출금이 어려울 수 있으니 사용하는 주소와 네트워크가 정확히 일치하는지 확인해 주세요._**
>
>   **디지털 자산 출금 시 네트워크 타입 (net\_type) 값이 필수입니다.**
> - **네트워크 명( `network_name`)이란?**
>
>
>   업비트에서 지원하고 있는 디지털 자산의 **블록체인 네트워크 이름을 확인** 할 수 있는 기능입니다.
>
>   [업비트 고객센터에서 제공되는 입출금 현황 페이지](https://upbit.com/service_center/wallet_status) 의 '네트워크'와 동일한 값입니다.

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EC%B6%9C%EA%B8%88-%ED%97%88%EC%9A%A9-%EC%A3%BC%EC%86%8C-%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%A1%B0%ED%9A%8C\#response)

| Name | 설명 | 타입 |
| --- | --- | --- |
| currency | 출금 화폐 | String |
| net\_type | 출금 네트워크 타입 | String |
| network\_name | 출금 네트워크 이름 | String |
| withdraw\_address | 출금 주소 | String |
| secondary\_address | 2차 출금 주소 (필요한 디지털 자산에 한해서) | String |

# `` 200      200

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

# `` 4XX      4XX

object

error

object

name

string

message

string

Updated 1 day ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

25

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const sign = require('jsonwebtoken').sign

4​

5const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

6const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

7const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

8​

9

const payload = {

10    access_key: access_key,

11    nonce: uuidv4(),

12}

13​

14const token = sign(payload, secret_key)

15​

16

const options = {

17    method: "GET",

18    url: server_url + "/v1/withdraws/coin_addresses",

19    headers: {Authorization: `Bearer ${token}`},

20}

21​

22

request(options, (error, response, body) => {

23    if (error) throw new Error(error)

24    console.log(body)

25})

```

```

xxxxxxxxxx



1

{

2  "currency": "BTC",

3  "net_type": "BTC",

4  "network_name": "Bitcoin",

5  "withdraw_address": "1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa",

6  "secondary_address": null

7}

```

Updated 1 day ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference_id_EB_A1_9C__EC_A3_BC_EB_AC_B8_EB_A6_AC_EC_8A_A4_ED_8A_B8__EC_B7_A8_EC_86_8C__EC_A0_91_EC_88_98.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/id%EB%A1%9C-%EC%A3%BC%EB%AC%B8%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%B7%A8%EC%86%8C-%EC%A0%91%EC%88%98\#request-parameters)

| Name | 설명 | 타입 |
| --- | --- | --- |
| uuids\[\]\* | 취소할 주문 UUID의 목록 (최대 20개) | Array\[String\] |
| identifiers\[\]\* | 취소할 주문 identifier의 목록 (최대 20개)<br>\*uuids 또는 identifiers 중 **한 가지 필드는 필수** 이며, **두 가지 필드를 함께 사용할 수 없습니다**. | Array\[String\] |

> ## ❗️
>
> 이 API 는 Query Parameter 형식의 요청만 지원합니다. Request Body 를 통한 요청은 지원하지 않으니 유의해주시기 바랍니다.

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/id%EB%A1%9C-%EC%A3%BC%EB%AC%B8%EB%A6%AC%EC%8A%A4%ED%8A%B8-%EC%B7%A8%EC%86%8C-%EC%A0%91%EC%88%98\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| success | 취소 요청 성공한 주문 리스트 정보 | Object |
| success.count | 취소 요청 성공한 주문의 개수 | Number |
| success.orders | 취소 요청 성공한 주문 정보 | Array\[Object\] |
| success.orders.uuid | 취소 요청 성공한 주문의 UUID | String |
| success.orders.market | 취소 요청 성공한 주문의 마켓 아이디 | String |
| success.orders.identifier | 조회용 사용자 지정값<br>\*identifier 필드는 2024-10-18 이후에 생성된 주문에 대해서만 제공합니다. | String |
| failed | 취소 요청 실패한 주문 리스트 정보 | Object |
| failed.count | 취소 요청 실패한 주문의 개수 | Number |
| failed.orders | 취소 요청 실패한 주문 정보 | Array\[Object\] |
| failed.orders.uuid | 취소 요청 실패한 주문의 UUID | String |
| failed.orders.market | 취소 요청 실패한 주문의 마켓 아이디 | String |
| failed.orders.identifier | 조회용 사용자 지정값<br>\*identifier 필드는 2024-10-18 이후에 생성된 주문에 대해서만 제공합니다. | String |

> ## ❗️  취소 실패
>
> 취소 접수가 되기 전에 이미 체결이 완료된 경우, 이미 취소된 주문인 경우, 리브랜딩 등의 이유로 인한 마켓 일시 중단 등의 사유로 일부 주문에 대해서 주문 취소 접수가 실패될 수 있습니다.

uuids\[\]

string

취소할 주문 UUID의 목록

identifiers\[\]

string

취소할 주문 identifier의 목록

# `` 200      200

object

success

object

count

integer

Defaults to 0

orders

array of objects

orders

object

uuid

string

market

string

failed

object

count

integer

Defaults to 0

orders

array

orders

# `` 400      400

object

error

object

name

string

message

string

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

44

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const querystring = require("querystring")

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11

const params = {

12

    'uuids[]': [\
\
13        '6c1eac69-b9bc-4fbf-9982-e9c4641c453f',\
\
14        'e7f41e24-7199-4cf4-9b02-72971cb69a4d',\
\
15        '1fc8d0bb-95c2-4116-96d8-6e2aa82200ba',\
\
16        '34c52f5d-e4c8-4217-a6a8-0f7a06bf4c63',\
\
17        '5767ea2c-451b-47f4-8a3d-009a5e08db5e',\
\
18    ],

19}

20​

21const queryParams = querystring.unescape(querystring.encode(params))

22​

23const hash = crypto.createHash('sha512')

24const queryHash = hash.update(queryParams, 'utf-8').digest('hex')

25​

26

const payload = {

```

```

xxxxxxxxxx

31
}

1

{

2

  "success": {

3    "count": 5,

4

    "orders": [\
\
5\
\
      {\
\
6        "uuid": "6c1eac69-b9bc-4fbf-9982-e9c4641c453f",\
\
7        "market": "BTC-ADA"\
\
8      },\
\
9\
\
      {\
\
10        "uuid": "e7f41e24-7199-4cf4-9b02-72971cb69a4d",\
\
11        "market": "BTC-ADA"\
\
12      },\
\
13\
\
      {\
\
14        "uuid": "1fc8d0bb-95c2-4116-96d8-6e2aa82200ba",\
\
15        "market": "BTC-ADA"\
\
16      },\
\
17\
\
      {\
\
18        "uuid": "34c52f5d-e4c8-4217-a6a8-0f7a06bf4c63",\
\
19        "market": "BTC-ADA"\
\
20      },\
\
21\
\
      {\
\
22        "uuid": "5767ea2c-451b-47f4-8a3d-009a5e08db5e",\
\
23        "market": "BTC-ADA"\
\
24      }\
\
25    ]

```

Updated 3 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EC_9B_90_ED_99_94__EC_B6_9C_EA_B8_88_ED_95_98_EA_B8_B0.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EC%9B%90%ED%99%94-%EC%B6%9C%EA%B8%88%ED%95%98%EA%B8%B0\#request-parameters)

> ## ❗️  v1.4.1 업데이트 : two\_factor\_type 필수 지정 필요 & 2채널 인증 '카카오 페이 인증' 종료 및 '카카오톡 인증' 신규지원 (적용 완료)
>
> - 11월 20일 이후 2채널 인증 수단 타입으로 `kakao` 가 추가되었습니다.
> - 12월 18일 이후, `two_factor_type` 필드는 **디폴트 값이 없는 필수 필드가 되므로 원화 출금 요청 시 `two_factor_type` 값을 반드시 지정하여 요청** 해주셔야 합니다.
> - 12월 18일 이후 **2채널 인증 수단 타입으로 `kakao_pay` 를 더이상 사용하실 수 없습니다.**
>
> 자세한 변경사항은 [공지사항](https://docs.upbit.com/kr/changelog/kakao_auth) 을 참조해주세요.

| Name | 설명 | 타입 |
| --- | --- | --- |
| amount\* | 출금액 | Number |
| two\_factor\_type\* | 2차 인증 수단 | `kakao`: 카카오 인증<br>`naver` : 네이버 인증<br>`hana` : 하나인증서 인증 |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EC%9B%90%ED%99%94-%EC%B6%9C%EA%B8%88%ED%95%98%EA%B8%B0\#response)

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
| transaction\_type | 출금 유형<br>_`default` : 일반출금_ `internal` : 바로출금 | String |

amount

string

required

출금 원화 수량

two\_factor\_type

string

required

2차 인증 수단 (kakao, naver, hana)

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

# `` 4XX      4XX

object

error

object

name

string

message

string

Updated 3 months ago

* * *

Did this page help you?

Yes

No

NodePythonRubyJava

```

xxxxxxxxxx

40

1const request = require('request')

2const uuidv4 = require("uuid/v4")

3const crypto = require('crypto')

4const sign = require('jsonwebtoken').sign

5const queryEncode = require("querystring").encode

6​

7const access_key = process.env.UPBIT_OPEN_API_ACCESS_KEY

8const secret_key = process.env.UPBIT_OPEN_API_SECRET_KEY

9const server_url = process.env.UPBIT_OPEN_API_SERVER_URL

10​

11

const body = {

12    amount: '10000',

13    two_factor_type: 'naver'

14}

15​

16const query = queryEncode(body)

17​

18const hash = crypto.createHash('sha512')

19const queryHash = hash.update(query, 'utf-8').digest('hex')

20​

21

const payload = {

22    access_key: access_key,

23    nonce: uuidv4(),

24    query_hash: queryHash,

25    query_hash_alg: 'SHA512',

26}

```

```

xxxxxxxxxx

12



1

{

2  "type": "withdraw",

3  "uuid": "9f432943-54e0-40b7-825f-b6fec8b42b79",

4  "currency": "KRW",

5  "txid": "ebe6937b-130e-4066-8ac6-4b0e67f28adc",

6  "state": "processing",

7  "created_at": "2018-04-13T11:24:01+09:00",

8  "done_at": null,

9  "amount": "10000",

10  "fee": "0.0",

11  "transaction_type": "default"

12}

```

Updated 3 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference_websocket_myorder.md]
> ## 📘  Private 타입 endpoint
>
> 새롭게 추가된 `myOrder` 와 `myAsset` 타입의 경우 `wss://api.upbit.com/websocket/v1/private` 으로 요청하셔야 합니다. 자세한 내용은 [기본 정보](https://docs.upbit.com/kr/reference/general-info) 를 참고해주시기 바랍니다.

# Request   [Skip link to Request](https://docs.upbit.com/kr/reference/websocket-myorder\#request)

요청은 JSON Object를 이용하며 응답 또한 JSON Object 입니다. 요청은 크게 ticket field, type field, format field 로 나누어지며 하나의 요청에 여러 개의 type field 를 명시할 수 있습니다. ticket field 와 format field 에 대해서는 [요청 방법 및 포맷](https://docs.upbit.com/kr/reference/websocket-request-format) 을 참고해주시기 바랍니다.

> ## 📘  Request format
>
> **\[{Ticket Field},{Type Field},....,{Type Field},{Format Field}\]**

### **Type Field**   [Skip link to [object Object]](https://docs.upbit.com/kr/reference/websocket-myorder\#type-field)

수신하고 싶은 시세 정보를 나열하는 필드입니다.

| 필드명 | 타입 | 내용 | 필수 여부 | 기본 값 |
| --- | --- | --- | --- | --- |
| type | String | 데이터 타입<br>- `myOrder`: 내 주문 | O |  |
| codes | List | 마켓 코드 리스트<br>\*대문자로 요청해야 합니다. | X | 생략하거나 빈 배열로 요청할 경우 모든 마켓에 대한 정보를 수신합니다. |

# Response   [Skip link to Response](https://docs.upbit.com/kr/reference/websocket-myorder\#response)

> ## ❗️  `myOrder` 타입의 경우 특정 이벤트가 발생할 때만 데이터를 전송합니다.
>
> 따라서, **연결 후 즉시 데이터가 수신되지 않는 경우는 정상적인 동작** 입니다. 주문의 생성/체결/취소와 같은 이벤트가 발생할 때 데이터가 전송됩니다.
>
> 데이터 없이도 연결을 유지하고 싶으신 경우 [주기적으로 ping/pong 을 통해 connection 관리](https://docs.upbit.com/kr/reference/connection) 를 하실 수 있습니다.

| 필드명 | 축약형 (format: SIMPLE) | 내용 | 타입 | 값 |
| --- | --- | --- | --- | --- |
| type | ty | 타입 | String | `myOrder` : 내 주문 |
| code | cd | 마켓 코드 (ex. KRW-BTC) | String |  |
| uuid | uid | 주문 고유 아이디 | String |  |
| ask\_bid | ab | 매수/매도 구분 | String | `ASK` : 매도<br>`BID` : 매수 |
| order\_type | ot | 주문 타입 | String | `limit`: 지정가 주문<br>`price`: 시장가 매수 주문<br>`market`: 시장가 매도 주문<br>`best`: 최유리 지정가 주문 |
| state | s | 주문 상태 | String | `wait`: 체결 대기<br>`watch`: 예약 주문 대기<br>`trade`: 체결 발생<br>`done`: 전체 체결 완료<br>`cancel`: 주문 취소 |
| trade\_uuid | tuid | 체결의 고유 아이디 | String |  |
| price | p | 주문 가격,<br>체결 가격 (state: trade 일 때) | Double |  |
| avg\_price | ap | 평균 체결 가격 | Double |  |
| volume | v | 주문량,<br>체결량 (state: trade 일 때) | Double |  |
| remaining\_volume | rv | 체결 후 남은 주문 양 | Double |  |
| executed\_volume | ev | 체결된 양 | Double |  |
| trades\_count | tc | 해당 주문에 걸린 체결 수 | Integer |  |
| reserved\_fee | rsf | 수수료로 예약된 비용 | Double |  |
| remaining\_fee | rmf | 남은 수수료 | Double |  |
| paid\_fee | pf | 사용된 수수료 | Double |  |
| locked | l | 거래에 사용중인 비용 | Double |  |
| executed\_funds | ef | 체결된 금액 | Double |  |
| time\_in\_force | tif | IOC, FOK 설정 | String | `ioc`<br>`fok` |
| trade\_fee | tf | 체결 시 발생한 수수료<br>( `trade` 타입이 아닐 경우 null 값) | Double |  |
| is\_maker | im | 체결이 발생한 주문의 maker / taker 여부<br>( `trade` 타입이 아닐 경우 null 값) | Boolean | `true` : 메이커 주문<br>`false` : 테이커 주문 |
| identifier | id | 조회용 사용자 지정값<br>\*identifier 필드는 2024-10-18 이후에 생성된 주문에 대해서만 제공합니다. | String |  |
| trade\_timestamp | ttms | 체결 타임스탬프 (millisecond) | Long |  |
| order\_timestamp | otms | 주문 타임스탬프 (millisecond) | Long |  |
| timestamp | tms | 타임스탬프 (millisecond) | Long |  |
| stream\_type | st | 스트림 타입 | String | `REALTIME` : 실시간 |

# Example   [Skip link to Example](https://docs.upbit.com/kr/reference/websocket-myorder\#example)

### Request   [Skip link to Request](https://docs.upbit.com/kr/reference/websocket-myorder\#request-1)

예제 1\. 모든 마켓 정보 수신 (codes 필드 제외)

JSON

```rdmd-code lang-json theme-light

[\
  {\
    "ticket": "test-myOrder"\
  },\
  {\
    "type": "myOrder"\
  }\
]

```

예제 2\. 모든 마켓 정보 수신 (codes 에 빈 배열)

JSON

```rdmd-code lang-json theme-light

[\
  {\
    "ticket": "test-myOrder"\
  },\
  {\
    "type": "myOrder",\
    "codes": []\
  }\
]

```

예제 3\. 특정 마켓 정보 수신

JSON

```rdmd-code lang-json theme-light

[\
  {\
    "ticket": "test-myOrder"\
  },\
  {\
    "type": "myOrder",\
    "codes": ["KRW-BTC"]\
  }\
]

```

### Response   [Skip link to Response](https://docs.upbit.com/kr/reference/websocket-myorder\#response-1)

JSON

```rdmd-code lang-json theme-light

{
  "type": "myOrder",
  "code": "KRW-BTC",
  "uuid": "ac2dc2a3-fce9-40a2-a4f6-5987c25c438f",
  "ask_bid": "BID",
  "order_type": "limit",
  "state": "trade",
  "trade_uuid": "68315169-fba4-4175-ade3-aff14a616657",
  "price": 0.001453,
  "avg_price": 0.00145372,
  "volume": 30925891.29839369,
  "remaining_volume": 29968038.09235948,
  "executed_volume": 30925891.29839369,
  "trades_count": 1,
  "reserved_fee": 44.23943970238218,
  "remaining_fee": 21.77177967409916,
  "paid_fee": 22.467660028283017,
  "locked": 43565.33112787242,
  "executed_funds": 44935.32005656603,
  "time_in_force": null,
  "trade_fee": 22.467660028283017,
  "is_maker": true,
  "identifier": "test-1",
  "trade_timestamp": 1710751590421,
  "order_timestamp": 1710751590000,
  "timestamp": 1710751597500,
  "stream_type": "REALTIME"
}

```

Updated 3 months ago

* * *

Did this page help you?

Yes

No

Updated 3 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

[docs_upbit_com_kr_reference__EC_A3_BCweek__EC_BA_94_EB_93_A4_1.md]
## Request Parameters   [Skip link to Request Parameters](https://docs.upbit.com/kr/reference/%EC%A3%BCweek-%EC%BA%94%EB%93%A4-1\#request-parameters)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 마켓 코드 (ex. KRW-BTC) | String |
| to | 마지막 캔들 시각 (exclusive).<br>ISO8061 포맷 (yyyy-MM-dd'T'HH:mm:ss'Z' or yyyy-MM-dd HH:mm:ss). 기본적으로 UTC 기준 시간이며 `2023-01-01T00:00:00+09:00` 과 같이 KST 시간으로 요청 가능.<br>비워서 요청시 가장 최근 캔들 | String |
| count | 캔들 개수(최대 200개까지 요청 가능) | Integer |

## Response   [Skip link to Response](https://docs.upbit.com/kr/reference/%EC%A3%BCweek-%EC%BA%94%EB%93%A4-1\#response)

| 필드 | 설명 | 타입 |
| --- | --- | --- |
| market | 종목 코드 | String |
| candle\_date\_time\_utc | 캔들 기준 시각(UTC 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |
| candle\_date\_time\_kst | 캔들 기준 시각(KST 기준)<br>포맷: `yyyy-MM-dd'T'HH:mm:ss` | String |
| opening\_price | 시가 | Double |
| high\_price | 고가 | Double |
| low\_price | 저가 | Double |
| trade\_price | 종가 | Double |
| timestamp | 마지막 틱이 저장된 시각 | Long |
| candle\_acc\_trade\_price | 누적 거래 금액 | Double |
| candle\_acc\_trade\_volume | 누적 거래량 | Double |
| first\_day\_of\_period | 캔들 기간의 가장 첫 날 | String |

market

string

required

종목 코드 (ex. KRW-BTC)

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

Updated 7 months ago

* * *

Did this page help you?

Yes

No

ShellPythonNode

```

xxxxxxxxxx

10

1# KRW-BTC 마켓에 가장 최근 주봉 1개를 요청

2curl --request GET \

3     --url 'https://api.upbit.com/v1/candles/weeks?market=KRW-BTC&count=1' \

4     --header 'accept: application/json'

5​

6# KRW-BTC 마켓에 2024년 10월 1일(UTC) 이전 가장 최근 주봉 1개를 요청

7curl --request GET \

8     --url 'https://api.upbit.com/v1/candles/weeks?market=KRW-BTC&count=1&to=2024-10-01%2000%3A00%3A00' \

9     --header 'accept: application/json'

10

```

```

xxxxxxxxxx

15



1

[\
\
2\
\
  {\
\
3    "market": "KRW-BTC",\
\
4    "candle_date_time_utc": "2018-04-16T00:00:00",\
\
5    "candle_date_time_kst": "2018-04-16T09:00:00",\
\
6    "opening_price": 8665000,\
\
7    "high_price": 8840000,\
\
8    "low_price": 8360000,\
\
9    "trade_price": 8611000,\
\
10    "timestamp": 1524046708995,\
\
11    "candle_acc_trade_price": 466989414916.1301,\
\
12    "candle_acc_trade_volume": 54410.56660813,\
\
13    "first_day_of_period": "2018-04-16"\
\
14  }\
\
15]

```

Updated 7 months ago

* * *

Did this page help you?

Yes

No

## Open API 이용약관

본 이용약관은 두나무 주식회사(이하 "두나무"라 한다)과 업비트 Open API 서비스 사용자(이하 "사용자"라 한다)간의 업비트 Open API 서비스(이하 "Open API서비스"라 한다) 사용에 관한 이용약관입니다. 본 이용약관의 내용에 동의하여, 동의 버튼을 누르는 것은 사용자가 본 이용약관 내용에 이의가 없음을 의미합니다.

제 1조 (목적)
본 이용약관은 사용자가 두나무의 업비트 Open API 서비스를 이용하는 데 필요한 사항을 규정함을 목적으로 합니다.

제 2조 (정의)
1\. "Open API 서비스"라 함은 두나무가 제공하는 연결모듈로서, 사용자가 직접 제작하거나 제공하는 웹 서비스, 모바일 애플리케이션 및 기타 응용 프로그램 등(이하 “프로그램 등”이라 한다)을 두나무에서 제공하는 업비트 시스템에 연결하여, 시세 및 잔고 조회, 주문 기능(주문조회, 주문하기) 및 입출금 기능(입출금조회, 입출금하기)을 실행할 수 있도록 하는 Open API 서비스를 뜻합니다.

2\. "중요 제휴사"라 함은 "두나무"와 제휴 계약을 체결하여 업비트 서비스 또는 Open API 서비스의 중요한 일부 기능(로그인 기능, 디지털 자산 거래소 연동, 디지털 자산 지갑을 포함하며, 이에 한정하지 않습니다)을 제공하는 회사를 의미합니다.

3\. "Open API Docs (업비트 개발자 센터 문서)"라 함은 사용자의 Open API 서비스의 이용에 편의를 제공하기 위하여 두나무가 제공하는 API에 대한 설명, 예제 코드 및 그에 대한 예시 응답을 의미합니다.

제 3조 (면책사항)
➀ 두나무는 사용자가 Open API 서비스를 사용한 프로그램 등으로 인하여 발생하는 모든 결과에 대해 책임을 지지 않으며, 그 책임은 사용자에게 있습니다.
➁ 사용자가 Open API 서비스를 이용하여 작성한 프로그램 등을 제3자에게 제공하여 문제가 발생할 경우 그로 인한 책임은 사용자가 부담합니다.
➂ 정전, 화재, 전산장애, 통신장애, 기타 천재지변 등으로 인해 발생하는 Open API 서비스의 장애 또는 중단으로 손해가 발생한 경우 두나무가 책임지지 않습니다.
➃ 사용자의 컴퓨터 상태, 통신회선의 문제 또는 전산기기의 조작오류 등 사용자의 귀책사유로 인하여 발생하는 손해에 대하여 두나무는 책임을 지지 않습니다.
➄ 사용자가 계정 비밀번호, API key를 포함하여 계정 접근을 위해 필요한 일체의 정보를 누설하거나 이를 부주의하게 관리함으로 인하여 발생하는 손해 등에 대하여 두나무는 책임을 지지 않습니다.
➅ 시세급변, 주문 폭주 및 아래 각호의 오류가 발생할 경우 두나무는 책임을 지지 않습니다.
1\. 시세 전송 지연 및 급변 혹은 중요 제휴사의 처리 오류 등으로 인하여 주문의 미처리 및 미체결 등의 오류가 발생할 수 있습니다.
2\. 주문 응답 지연, 체결 수신 누락 및 지연으로 인한 주문의 미처리, 미체결 및 주문체결의 처리 결과가 상이하게 나타날 수 있습니다.
3\. 시스템 장애로 인한 백업서버 전환 처리 시 주문중지 등으로 처리될 수 있습니다.
4\. 시스템 전체 혹은 부분 장애, 특정 부분의 오류(운영 장비, 프로그램, 시세), 시스템 백업 전환 등으로 서비스 중지가 필요하다고 판단되는 경우 주문의 전부 또는 일부를 정지시킬 수 있습니다.
사용자가 Open API 서비스를 이용함에 있어 행한 불법행위 또는 본 이용약관 위반행위로 인하여 두나무가 당해 사용자 이외의 제3자로부터 손해배상청구 또는 소송을 비롯한 각종 이의제기를 받는 경우 당해 사용자는 자신의 책임과 비용으로 두나무를 면책시켜야 하며, 당해 사용자는 그로 인하여 두나무에게 발생한 모든 손해를 배상해야 합니다.
➆ 본 조 제1항부터 제7항에 해당하는 경우이더라도 두나무의 고의 또는 과실로 인해 손해가 발생하는 경우에는 해당 손해 범위에 대하여는 두나무가 책임을 부담합니다.
➇ 본 조는 업비트 이용약관 제20조(책임 제한)를 배제하지 않습니다.

제 4조 (Open API 서비스 제공의 제한 및 해지)
➀ 사용자가 Open API 서비스를 사용함에 있어, 다음 각 호의 하나에 해당하는 행위를 하였을 경우, 두나무는 사용자의 업비트 서비스 또는 Open API 서비스 접속 차단, 사용자의 IP 주소 차단, Open API 서비스 사용 전부 또는 일부 제한(API 요청 수 제한 포함) 등의 조치를 취하여 사용자에 대한 업비트 서비스 또는 Open API 서비스 제공을 제한할 수 있습니다.
1\. 본 이용약관 제6조를 위반한 경우
2\. 업비트 이용약관 제10조(회원의 의무)를 위반한 경우
3\. 업비트 이용약관 제17조(이용제한 등), 제18조(이용계약 해지) 제2항에서 정하는 각 사유에 해당하는 경우
4\. 하나의 IP에서 여러 계정이 가입하거나 접속하는 등 특정 개인 또는 집단에 의하여 타인 명의의 계정이 이용되고 있는 것으로 판단되는 경우
5\. 기타 두나무의 정상적인 전산 시스템 운영, 보안 관리 등에 부정적인 영향을 줄 수 있는 행위를 한 것으로 판단되는 경우
➁ 두나무는 사용자가 본 조 제1항 각 호의 하나에 해당하는 행위를 하였을 경우 시간을 정하여 업비트 서비스 또는 Open API 서비스 이용을 제한하거나 API 요청 수를 제한함과 동시에 시정요구를 할 수 있습니다. 시정 요구에도 불구하고 상당한 기간 내에 시정되지 않거나 2회 이상 반복적으로 동일한 위반행위를 하는 경우에는 이용계약을 해지할 수 있습니다.
➂ 사용자는 사전에 등록한 IP주소에서만 Open API 서비스를 사용할 수 있으며, 범죄에 활용되었거나 활용될 가능성이 높은 IP주소 또는 본 이용약관 위반 행위에 연관된 IP주소 등 위험성이 높은 IP주소의 경우 등록이 거부될 수 있습니다. 사용자가 등록이 거부된 IP주소를 이용하여야 할 부득이한 사정이 있고 해당 IP 주소의 위험성을 달리 판단할 만한 상당한 사정이 있는 경우, 사용자는 고객센터를 통하여 해당 IP 주소의 위험성에 관해 재심사를 신청할 수 있습니다. 이때 회사는 IP주소의 위험성에 관해 달리 판단함이 상당한지 여부를 결정하기 위하여 회원에게 관련 자료를 요청할 수 있습니다.
➃ 본 조는 업비트 이용약관 제10조, 제17조, 제18조, 제20조의 적용을 배제하지 않습니다.

제 5조 (저작권)
Open API 서비스, Open API Docs상에서 제공되는 모든 데이터 및 내용에 대한 저작권은 두나무에 있으므로 사용자가 이를 무단으로 사용, 복제, 배포, 변경하거나 영리목적으로 이용하는 것은 금지됩니다.

제 6조 (사용자의 의무와 책임)
➀ 다음 각 호의 변경사항들에 관한 공지는 업비트 개발자센터 공지 게시판 등을 통하여 사전에 제공되므로 사용자는 이를 반드시 확인하여야 하며, Open API 서비스 내용 변경 시, 사용자는 변경 내용을 제작한 프로그램 등에 직접 반영하여야 합니다.
1\. API 업데이트 및 변경 사항에 대한 공지
2\. 제도 변경 공지
3\. 두나무-업비트 정책 반영에 따른 공지
4\. 기타 긴급 공지
➁ 사용자는 Open API 서비스를 사용함에 있어 관련 법령, 본 이용약관 및 업비트 개발자 센터(https://docs.upbit.com) 내 각 Open API 사용을 위한 안내, 가이드, 사용량 제한(쿼터) 등을 준수하여야 합니다.
➂ 사용자는 Open API 서비스를 이용할 수 있는 프로그램 등을 타인에게 유상으로 양도, 배포, 이용 허락할 수 없고, Open API 서비스를 이용함에 있어 타인이 유상으로 양도, 배포, 이용, 허락한 프로그램 등을 사용할 수 없습니다.
➃ 사용자의 계정 접근을 위해 필요한 일체의 정보(API key를 포함하며 이에 한정하지 않음)는 사용자 본인만이 사용할 수 있고 타인에게 제공, 공개, 공유, 양도 또는 위임할 수 없으며, 사용자는 기타의 방법을 통해 타인으로 하여금 회사의 Open API 서비스에 접근하도록 할 수 없습니다.

제 7조 (약관의 변경 등)
➀ 두나무는 필요한 경우 관련 법령을 위배하지 않는 범위에서 본 이용약관을 개정할 수 있습니다.
➁ 두나무가 본 이용약관을 개정할 경우에는 개정내용과 적용일자를 명시하여 적용일자 30일 이전부터 적용일자 전날까지 사용자에게 공지(업비트 개발자 센터(https://docs.upbit.com) 초기화면, 게시판에 게시하거나 팝업화면 등을 제시하여 모든 사용자들에게 안내하는 행위, 이하 같음) 또는 통지(업비트 이용약관 제19조 제1항에 따라 사용자가 두나무에 제공한 전자우편주소, 전자메모, 서비스 내 메시지, 문자메시지(LMS/SMS) 등으로 개별 사용자에게 안내하는 행위, 이하 같음)합니다. 단, 제⋅개정된 관계 법령, 국가기관의 정책⋅명령 등을 준수하기 위하여 약관을 긴급하게 개정 및 시행해야 하는 경우에는 약관 개정내용을 회원에게 공지 및 개별 통지함과 동시에 시행할 수 있습니다(개정내용이 회원에게 부당하게 불리하지 않은 경우에 한함).
➂ 두나무가 본 조에 따라 공지 또는 통지하면서 사용자에게 적용일자 전일까지 의사표시를 하지 않으면 의사표시가 표명된 것으로 본다는 뜻을 명확하게 알렸음에도 사용자가 명시적으로 거부의 의사표시를 하지 아니한 경우 사용자가 개정약관에 동의한 것으로 봅니다.
➃ 사용자는 개정 약관에 동의하지 않는 경우 적용일자 전날까지 두나무에 거부 의사를 표시하고 서비스 이용계약을 해지할 수 있습니다.

제 8조 (효력 발생 및 유효기간)
본 이용약관은 사용자의 동의와 동시에 그 효력이 발생하며, 사용자 및 두나무의 업비트 서비스 또는 Open API 서비스 해지 등의 사유로 효력이 상실할 때까지 유효합니다.

제 9조 (기타)
➀ 본 이용약관에 명시되지 않은 사항은 업비트 이용약관 및 관계 법령에서 정하는 바에 따르며, 관계 법령에서 정하지 아니한 사항은 일반적 관례를 따릅니다.
➁ 본 이용약관과 업비트 이용약관이 충돌할 경우 본 이용약관이 우선합니다.

제 10조 (관할법원)
본 이용약관에 의한 거래와 관련하여 발생된 분쟁에 대하여 두나무와 사용자 사이에 소송의 필요가 생긴 경우에는 그 관할법원은 「민사소송법」이 정한 바에 따릅니다.

<부칙>
본 이용약관은 2024년 10월 30일부터 적용됩니다.
이전의 이용약관은 아래에서 확인하실 수 있습니다.


[OPEN API 이용약관 (2023.12.15 ~ 2024.10.29) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231215.html)

[OPEN API 이용약관 (2023.10.11 ~ 2023.12.14) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20231011.html)

[OPEN API 이용약관 (2021.05.07 ~ 2023.10.10) 바로 가기 >](https://static.upbit.com/terms/legacy/openapi_agreement_20210507.html)

[OPEN API 이용약관 (2018.06.21 ~ 2021.05.06) 바로 가기 >](https://static.upbit.com/terms/legacy/open_api_terms_20180621.html)

동의

