# DNS (Domain Name System)

## 도메인 이름 공간 DNS

---

> 도메인을 사용하면서 유저는 IP주소를 몰라도 웹 페이지에 접근할 수 있게 되었습니다.
계층적인 구조로 이루어져 (.)으로 구분됩니다.
> 

| www | helloworld | com | . (빈문자 or .) |
| --- | --- | --- | --- |
| 하위 도메인 | 2차 도메인 | 최상위 도메인 | 루트 도메인 |

## 레코드 Record

---

> 도메인 이름과 IP 주소 간의 매핑 정보를 저장합니다. @ : 도메인의 약어, this, self
> 

| 레코드 유형 | 용도 | 도메인 / 서브 | 매핑할 주소 | 캐시 유효 기간 | 우선 순위 |
| --- | --- | --- | --- | --- | --- |
| A (Address) | IPv4 연결 | @ | www | 192.0.0.1 | Auto / Custom |  |
| AAAA (Address * 4) | IPv6 연결 | @ | www | 2001:0db8…. | Auto / Custom |  |
| CNAME (Canonical Name) | 도메인 별칭 지정 | www | example.com | Auto / Custom |  |
| MX (Mail Exchange) | 메일 서버 지정 | @ | mail.example.com | Auto / Custom | 1 ~ 10 |
| TXT (Text) | 이메일 발송 정책,
디지털 서명,
기타 인증정보 | @ | www | “v=spf1 include:_spf.example.com ~all” | Auto / Custom |  |