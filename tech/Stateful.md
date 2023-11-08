상태 유지

서버가 클라이언트의 상태를 보존함

단점 : 항상 같은 서버가 유지되어야 함. 중간에 다른 서버로 바뀌면 안됨. 중간에 다른 서버로 바뀌면 상태 정보를 다른 서버에게 미리 알려줘야함

ex) 사용되는곳
로그인
로그인한 사용자의 경우 로그인 했다는 상태를 서버에 유지
일반적으로 브라우저 쿠키와 서버 세션 등을 사용해서 상태 유지
상태 유지는 최소한만 사용

반의어 : [[Stateless]]

---

고객 : 이 노트북 얼마예요?
점원A : 100만원 입니다

고객 : 2개 구매하겠습니다
점원A : 200만원 입니다. 신용카드, 현금중에 어떤 방법으로 구매하시겠어요?

고객 : 신용카드로 구매하겠습니다
점원A : 200만원 결제 완료되었습니다 

---

점원이 중간에 바뀐 경우

고객 : 이 노트북 얼마예요?
점원A : 100만원 입니다 (노트북 상태 유지)

고객 : 2개 구매하겠습니다
점원A : 200만원 입니다. 신용카드, 현금중에 어떤 방법으로 구매하시겠어요? (노트북, 2개 상태 유지)

고객 : 신용카드로 구매하겠습니다
점원A : 200만원 결제 완료되었습니다 (노트북, 2개, 신용카드 상태 유지)

