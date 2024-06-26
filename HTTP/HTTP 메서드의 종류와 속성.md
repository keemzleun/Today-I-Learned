## HTTP 메서드의 종류와 속성

### 메서드의 종류

- **GET**: 리소스 조회
- **POST**: 요청 데이터 처리, 주로 등록에 사용
- **PUT**: 리소스 덮어쓰기. 리소스를 대체 해당 리소스가 없으면 생성
- **PATCH**: 리소스 부분 변경(PUT은 전체 변경, PATCH는 일부 변경)
- **DELETE**: 리소스 삭제
- **HEAD:** GET과 동일하지만 메시지 부분을 제외하고, 상태 줄과 헤더만 반환
- **OPTIONS:** 대상 리소스에 대한 통신 가능 옵션(메서드)을 설명(주로 CORS에서 사용)
- **CONNECT:** 대상 리소스로 식별되는 서버에 대한 터널을 설정
- **TRACE:** 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행

### 메서드의 속성
- 안전(Safe Methods)
- 멱등(Idempotent Methods)
- 캐시가능(Cacheable Methods)

![http메서드](/img/http메서드.png)

1. **안전(Safe)**
- 호출해도 리소스를 변경하지 않음

2. **멱등(Idempotent)**
- 연산을 여러 번 적용하더라도 결괏값이 달라지지 않는 일
- 한 번 호출하든 두 번 호출하든 100번 호출하든 결과가 똑같음
- 멱등 메서드
    - **GET**: 한 번 조회하든, 두 번 조회하든 같은 결과가 조회됨
    - **PUT**: 결과를 대체. 따라서 같은 요청을 여러번 해도 최종 결과는 같음
    - **DELETE**: 결과를 삭제. 같은 요청을 여러번 해도 삭제된 결과는 똑같음
    - **POST**: 멱등X! 두 번 호출하면 같은 결제가 중복해서 발생할 수 있음
- 활용
    - 자동 복구 메커니즘
    - 서버가 TIMEOUT 등으로 정상 응답을 못주었을 때, 클라이언트가 같은 요청을 다시 해도 되는가? 판단 근거
- **멱등은 외부 요인으로 중간에 리소스가 변경되는 것 까지는 고려하지는 않음**

3. **캐시가능(Cacheable)**
- 응답 결과 리소스를 캐시해서 사용해도 되는 메서드
- GET, HEAD, POST, PATCH 캐시가능
- POST, PATCH는 본문 내용까지 캐시 키로 고려해야 해서 구현이 쉽지 않기 때문에 실제로는 **GET, HEAD** 정도만 캐시로 사용
