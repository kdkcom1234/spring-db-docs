- Account 클래스
- ConcurrentHashMap, AtomicLong
- React Controller 개발

---

1. Account 클래스

- ano: String, 계좌번호(10자리고정, not nullable)
- name: String, 계좌주이름(최대 20자리, not nullable)
- balance: long, 잔액(초기값 0)

2. Account Controller

1. 1건의 계좌정보 추가 기능

- 계좌번호 값이 조건에 맞는지 검증 후 400 예외처리
- 기존목록에 있는 계좌번호이면 409 예외처리

2. 전체 계좌 목록 조회 기능

- JSON형태로 전체 계좌목록을 응답 처리한다.

3. 잔액 기준으로 검색할 수 있는 기능

- 예) 잔액이 0원인 계좌 목록을 조회
- 예) 잔액이 100,000 이상인 계좌목록을 조회
- 예) 잔액이 300,000 이하인 계좌목록을 조회

- 매개변수 이름: eq(동일), from(이상), to(이하)

4. 계좌번호로 계좌 1건을 조회할 수 있는 기능

5. 계좌주의 이름을 변경하는 기능

- PUT /accounts/1/name

7. 계좌의 잔고를 증가 또는 감소 시키는 기능

- PUT /accounts/1/balance/increase
- PUT /accounts/1/balance/decrease

8. 계좌를 현재 계좌목록에서 삭제하고, 삭제된 목록에 추가하는 기능
