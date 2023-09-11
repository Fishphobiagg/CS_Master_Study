### CORS와 SOP
* SOP
(Same-Origin Policy)
  * 동일 출처 정책을 의미
  * ‘같은 출처의 리소스만 공유가 가능하다'라는 정책
> URL의 origin: https://www.google.com
프로토콜: https
호스트: www.google.com
포트 (기본값): HTTPS의 경우 443 포트를 사용하며, 이는 일반적으로 생략

  * 출처
    * 프로토콜, 호스트, 포트의 조합
    * 세 가지 중 하나라도 다르면 동일 출처로 보지 않습니다

> 💡 예시
  - `https://google.com` **vs** `http://google.com`
⇒ 두 URI는 **프로토콜**이 다르기 때문에 동일 출처가 아닙니다. ( https / http )
- `https://google.com` **vs** `https://store.google.com`
⇒ 두 URI는 **호스트**가 다르기 때문에 동일 출처가 아닙니다. ( google.com / store.google.com )
- `http://google.com:81` **vs** `http://google.com`
    - http 프로토콜의 기본 포트는 80입니다. 따라서 `http://google.com` 는 `http://google.com:80` 과 동일합니다.
    ⇒ 두 URI는 **포트**가 다르기 때문에 동일 출처가 아닙니다. ( :81 / :80 )
- `https://google.com:443` **vs** `https://google.com`
    - https 프로토콜의 기본 포트는 443입니다. 따라서 `https://google.com` 는 `https://google.com:443` 과 동일합니다.
    ⇒ 두 URI는 프로토콜, 호스트, 포트가 모두 같은 **동일 출처**입니다.
  
* SOP이 생겨난 이유
    * 동일 출처 정책인 SOP은 잠재적으로 해로울 수 있는 문서를 분리함으로써 공격받을 수 있는 경로를 줄입니다
    * 즉, 해킹 등의 위협에서 보다 더 안전해질 수 있습니다
* SOP이 없을 경우
  * 웹페이지 로그인 서비스 이용 > 로그아웃 깜빡하거나 자동 로그인 기능으로 브라우저에 로그인 정보가 남아있을 때 > <br>내 로그인 정보를 노리는 코드가 있는 다른 사이트에 방문 > <br>해커가 로그인 정보 이용해서 네이버에서 사용할 수 있는 모든 기능 이용 > 나도 모르는 사이 내 계정으로 블로그나 카페에 나쁜 글을 올리거나 수 천명에게 스팸 메일을 보낼 수도 있습니다 
* SOP이 있는 경우
    * 애초에 **다른 사이트와의 리소스 공유를 제한**해서 로그인 정보가 타 사이트의 코드에 의해 새어나가는 것을 방지합니다
    * 이런 **보안상의 이점** 때문에 SOP은 모든 브라우저에서 기본적으로 사용합니다

* CORS
(Cross-Origin Resource Sharing)
  * 교차 출처 리소스 공유를 의미
  * 다른 출처의 리소스를 받아올 때 필요한 것
* CORS의 관점에서 에러를 해석한다면
    * 다른 출처의 리소스를 가져오려고 했지만 **SOP(동일 출처 정책)**때문에 접근이 불가능합니다
    CORS 설정을 통해 서버의 응답 헤더에 ‘Access-Control-Allow-Origin’을 작성하면 접근 권한을 얻을 수 있습니다
    * 이 에러의 원인은 **SOP**
    * **CORS**는 에러를 해결할 수 있는 방안

### CORS 동작 방식
1. 프리플라이트 요청
(Preflight Request)
> 실제 요청 보내기 전, OPTIONS 메서드로 사전 요청을 보내 해당 출처 리소스에 접근 권한이 있는지부터 확인하는 것
  
  * 실제 요청 전 > Preflight 요청 전송 > 응답 헤더의 Access-Control-Allow-Origin으로 요청을 보낸 출처가 돌아오면 실제 요청을 보냅니다
* 접근 권한이 없는 경우
  *  CORS 에러를 띄우고, 실제 요청은 전달되지 않습니다
* 프리플라이트 요청이 필요한 이유
    * 실제 요청 보내기 전 미리 권한을 확인할 수 있기 때문에 실제 요청을 처음부터 보내는 것보다 리소스 측면에서 효율적 (거름망처럼 거른다)
    * CORS에 대비가 되어있지 않은 서버 보호
         * CORS 이전에 만들어진 서버들은 SOP 요청만 들어오는 상황을 고려하고 만들어졌습니다
        * 따라서 다른 출처에서 들어오는 요청에 대한 대비가 되어있지 않습니다 이런 서버에 요청을 바로 보내면, 응답 보내기 전 우선 요청을 처리 > 브라우저는 응답 받은 후에야 CORS 권한이 없다는 것을 인지 > 에러 띄웠을 때는 이미 요청이 수행된 상태 > 요청이 DELETE나 PUT처럼 서버 정보를 삭제 / 수정하는 경우라면 ? … 이미 소잃은 상태
  
      *  이렇듯 CORS에 대비가 되어있지 않은 서버라도 프리플라이트 요청을 먼저 보내면 거기서부터 CORS 에러를 띄웁니다
      * 예시와 같이 실행되어서는 안되는 Cross-Origin 요청이 실행되는 것을 방지할 수 있습니다
    * 이러한 이유로 프리플라이트 요청이 CORS의 기본 사양이 되었습니다
2. 단순 요청
(Simple Request)
> 특정 조건이 만족되면, 프리플라이트 요청을 생략하고 요청을 보내는 것
  
  > 💡 조건
    - **`GET`, `HEAD`, `POST`** 요청 중 하나여야 합니다.
    - GET: 정보를 가져오는 요청
    - HEAD: 정보의 헤더(크기, 유형, 수정 날짜 등)만 가져오는 요청
    - POST: 데이터를 서버로 보내는 요청
    - 자동으로 설정되는 헤더 외에, `Accept`, `Accept-Language`, `Content-Language`, `Content-Type` 헤더의 값만 수동으로 설정할 수 있습니다.
    - `Content-Type` 헤더에는 `application/x-www-form-urlencoded`, `multipart/form-data`, `text/plain` 값만 허용됩니다.
  
3. 인증정보를 포함한 요청
(Credentialed Request)
    - 요청 헤더에 인증 정보를 담아 보내는 요청
    - 출처가 다를 경우에는 민감한 정보이기 때문에 별도 설정 하지 않으면 쿠키 보낼 수 없습니다 > 
    이 경우, 프론트, 서버 양측 모두 CORS 설정이 필요

> 💡 CORS 설정
  - **프론트** 측에서는 요청 헤더에 `withCredentials : true` 를 넣어줘야 합니다.
  - **서버** 측에서는 응답 헤더에 `Access-Control-Allow-Credentials : true` 를 넣어줘야 합니다.
  - 서버 측에서 `Access-Control-Allow-Origin` 을 설정할 때, 모든 출처를 허용한다는 뜻의 와일드카드(*)로 설정하면 에러가 발생합니다. 인증 정보를 다루는 만큼 출처를 정확하게 설정해주어야 합니다.
  
### HTTP 요청/응답 주요 헤더
#### 요청(Request)에서 사용되는 헤더
  * **From: 유저 에이전트의 이메일 정보**
    * 일반적으로 잘 사용하지 않음
    * 검색 엔진에서 주로 사용
    * 요청에서 사용
  * **Referer: 이전 웹 페이지 주소**
    * 현재 요청된 페이지의 이전 웹 페이지 주소
    * A → B로 이동하는 경우 B를 요청할 때 `Referer: A`를 포함해서 요청
    * `Referer`를 사용하면 유입경로 수집 가능
    * 요청에서 사용
    * referer는 단어 referrer의 오탈자이지만 스펙으로 굳어짐
  * **User-Agent: 유저 에이전트 애플리케이션 정보**
    * 클라이언트의 애플리케이션 정보(웹 브라우저 정보, 등등)
    * 통계 정보
    * 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능
    * 요청에서 사용
    * e.g. user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/
            537.36 (KHTML, like Gecko) Chrome/86.0.4240.183 Safari/537.36
  * **Host: 요청한 호스트 정보(도메인)**
    * 요청에서 사용
    * 필수 헤더
    * 하나의 서버가 여러 도메인을 처리해야 할 때 호스트 정보를 명시하기 위해 사용
    * 하나의 IP 주소에 여러 도메인이 적용되어 있을 때 호스트 정보를 명시하기 위해 사용
    * 여기서 요청을 보낸 주소와 받는 주소가 다르면 CORS 에러가 발생한다.
    * 응답 헤더의 Access-Control-Allow-Origin와 관련
* **Authorization: 인증 토큰(e.g. JWT)을 서버로 보낼 때 사용하는 헤더**
    * “토큰의 종류(e.g. Basic) + 실제 토큰 문자”를 전송
    * e.g. Authorization: Basic YWxhZGRpbjpvcGVuc2VzYW1l
<br >
#### 응답(Response)에서 사용되는 헤더
  * **Server: 요청을 처리하는 ORIGIN 서버의 소프트웨어 정보**
    * 응답에서 사용
    * e.g.
      * server: Apache/2.2.22 (Debian)
      * Server: nginx
  * **Date: 메시지가 발생한 날짜와 시간**
    * 응답에서 사용
    * e.g.
    Date: Tue, 15 Nov 1994 08:12:31 GMT
  * **Location: 페이지 리디렉션**
    * 웹 브라우저는 3xx 응답의 결과에 `Location` 헤더가 있으면, `Location` 위치로 리다이렉트(자동 이동)
    * 201(Created): `Location` 값은 요청에 의해 생성된 리소스 URI
    * 3xx(Redirection): `Location` 값은 요청을 자동으로 리디렉션하기 위한 대상 리소스를 가리킴
  * **Allow: 허용 가능한 HTTP 메서드**
    * 405(Method Not Allowed)에서 응답에 포함
    * e.g.
  Allow: GET, HEAD, PUT
  * **Retry-After: 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간**
    * 503(Service Unavailable): 서비스가 언제까지 불능인지 알려줄 수 있음
    * e.g.
      Retry-After: Fri, 31 Dec 2020 23:59:59 GMT(날짜 표기)
      Retry-After: 120(초 단위 표기)
  *  **Reference**
    * [List of HTTP headers](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields)
