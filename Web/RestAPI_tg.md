## 💻 Rest API
### ❓ REST란 무엇인가?
- Representational State Transfer의 약자
- 자원을 이름으로 구분하여 해당 자원의 상태를 주고받는 모든 것을 의미함.
- 웹(HTTP)의 장점을 최대한 활용할 수 있는 아키텍처로서 확장성, 분산시스템, 데이터 소모량감소의 목적을 가지고 있음. (애플리케이션 분리 및 통합, 다양한 클라이언트의 등장)
- **웹 상에서 사용되는 여러 리소스를 `HTTP URI`로 표현하고, 해당 리소스에 대한 행위를 `HTTP Method`로 정의하는 방식**

### REST의 구성 요소
- 자원(Resource) : URL
    - 모든 자원에는 고유한 ID가 존재하게 되고, 이 자원은 Server에 존재함.
    - 자원을 구별하는 ID는 HTTP URL로 구분
    - Client는 URL을 이용하여 자원을 지정하고 해당 자원에 대한 조작을 Server에 요청
- 행위(Verb) : HTTP Method
    - Client는 HTTP Method(POST, GET, DELETE, PUT)을 이용하여 지정한 자원에 대한 조작을 요청
   
 
Method | 의미 | Idempotent
 ----|----|----
 POST | Create | No
 GET | Select | Yes
 PUT | Update | Yes
 DELETE | Delete | Yes
> Idempotent : 멱등성 (여러 번 수행했을 때 항상 같은 결과를 반환하냐?) 해당 개념이 중요한 이유는 트랜잭션 처리 시 재 호출 판단 여부를 결정하는 요소이기 때문


**추가적으로 알아두면 좋을 HTTP Method들**
```
    - OPTIONS
        - 현재 End-point가 제공 가능한 API Method를 응답함.
    - HEAD
        - 요청에 대한 Header 정보만 응답. (body가 없음)
    - PATCH
        - 자원의 일부를 수정할 경우 `PATCH`가 목적에 맞는 Method임
```    

- 표현 (Representation of Resource)
    - Client가 Server에 자원에 대한 조작을 요청하면 Server는 이에 대해 적절한 응답(Representation)을 보낸다.

### REST의 특징
- **REST에는 다음과 같이 크게 6가지의 특징이 있다.**
- Uniform Interface
     - URI로 지정한 Resource에 대해 조작을 통일되고 한정적인 인터페이스로 수행한다
     - HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능(특정 언어나 기술에 종속되지 않음)
- Stateless (무상태성)
    - 작업을 위한 상태정보를 별도로 저장하고, 관리하는 일을 하지 않음
    - 따라서 서비스의 자유도가 높아지고, 서버에서 불필요한 정보를 관리하지 않기 때문에 구현이 단순해짐
- Cacheable (캐시 가능)
    - REST는 웹 표준인 HTTP를 그대로 사용하기 때문에 HTTP가 가진 캐싱 기능을 적용할 수 있음
- Self-descriptiveness (자체 표현 구조)
    - REST API 스펙만 보고도 어떤 역할의 API인지 쉽게 이해할 수 있음
- Client - Server 구조
    - Server와 Client의 역할이 명확히 나뉘기 때문에 각 필드에서 개발해야할 점이 명확해지고 서로 간의 의존성이 줄어들게 됨.
- 계층형 구조
    - API Server는 순수 비즈니스 로직을 수행하고 그 앞단에 보안, 로드밸런싱, 암호화, 사용자 인증 등을 추가하여 구조상의 유연성을 줄 수 있음
    - PROXY, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있음

### REST API 설계 가이드
- 리소스에 대한 행위는 `HTTP Method(POST, GET, PUT, DELETE)`로 표현
-  /(슬래시)는 `계층 관계`를 나타낼때 사용
- URI 마지막 문자에 /(슬래시)를 사용하지 않는다.
- URI에 _(underscore)는 사용하지 않는다.
- 하이픈 (-)은 URL 가독성을 높이는데 사용한다.
- 영어 대문자보다는 `소문자`를 사용한다.
- URI는 동사형태보다 명사를 사용한한다.
- URI에 파일의 확장자를 포함 시키지 않는다.
- 실무에서는 HTTP 메서드로 해결하기 애매한 경우가 생길 수 있는데 이를 `Control URI`라고 함

- ** REST API는 설계하기 나름이지만 가급적 설계 가이드에 따라 일관되고 통일성있으며 가독성 좋은 스펙을 제공하여 Client가 예측가능하도록 설계하는 것이 좋음 **

### REST 성숙도 모델
- Level 0
    - 웹 메커니즘을 사용하지 않고 HTTP를 원격 통신을 위한 전송 시스템으로 사용함
    - 리소스 구분 없이 설계된 HTTP API
    - 단 하나의 End point를 사용하고, 전달되는 서로 다른 매개변수를 통해 하나의 End Point에서 여러 동작을 하게 됨.
    - 매개 변수를 body로 전달하기 위해 POST만 사용
```json
POST https://api/user
{
  "function": "getUser",
  "arguments" [
    "1"
  ]
}
```

- Level 1
    - 리소스의 개념을 도입
    - 모든 요청을 단일 서비스 End Point로 보내는 것이 아니라 개별 리소스와 통신하게 됨
    - 리소스별로 고유한 URI를 사용해서 식별
    - HTTP Method로 GET, POST만 사용하며 Response error인 경우에도 200으로 응답
    - HTTP headers에 Content-Type이나 Cache 관련 정보를 제공하지 않음
```json
POST https://api/users/create
{
  "name": "yoonyoung"
}
```

- Level 2
    - HTTP Method Get, Post, Put, Delete를 사용해 CRUD를 나타내고 각 응답에 맞는 Status Code를 사용
    - URI에 action이 담기지 않고, 멱등성을 보장하는 GET에 캐시가 적용됨
```json
HTTP/1.1 201 Created
Content-Type: application/json
{
  "result" {
    "id": "1",
    "name": "yoonyoung"
  }
}
```

- Level 3
    - Hypermedia As Engine of Application State 개념을 도입 (HAETEOS)
    - 진정한 REST API라고 할 수 있음
    - API 서비스의 모든 end point를 최초 진입점이 되는 URI를 통해 Hypertext Link 형태로 제공
    - 어떤 Request에 대한 Response에 해당 리소스의 상태에따라 가능한 다음 요청 URI도 제공함
    - 클라이언트는 HAETEOS를 통해 서버와 완전 동적인 상호작용이 가능함
```json
201 Created
{
    "id": 1,
    "name": "hak",
    "createdAt": "2018-07-04 14:00:00"
    "links": [
        {
            "rel": "self",
            "href": "http://api.test.com/users/1",
            "method": "GET"
        },
        {
            "rel": "delete",
            "href": "http://api.test.com/users/1",
            "method": "DELETE"
        },
        {
            "rel": "update",
            "href": "http://api.test.com/users/1",
            "method": "PATCH",
            "more_info": "http://api.test.com/docs/user-update"
            "body": {
                "name": "{The value to be modified}"
            }
        },
        {
            "rel": "user.posts",
            "href": "http://api.test.com/users/1/posts",
            "method": "GET"
        }
    ]
}
```


> 참고 URL : 

https://velog.io/@younge/REST-API-성숙도-모델-Maturity-Model-eqqyjqff

https://sanghaklee.tistory.com/57
   