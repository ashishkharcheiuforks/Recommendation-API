# API

추가 api를 정리하는 글입니다

### Recommandation API

딥 러닝을 이용한 물품 추천 api입니다. DsmMarket의 사용자가 물품을 열람할 때마다 로그가 api로 전송되고, 전송된 로그는 data.csv에 축적됩니다. 참고로 로그는 물품의 카테고리, 사용자 정보를 담고 있습니다. 자세한 내용은 밑에서 설명하겠습니다. 

현재 서비스를 시작하지 않아 데이터를 축적하지 못한 상태입니다. 일단 예시 데이터를 data.csv파일에 저장해 놓았으니, 궁금하신 분은 열람해 주시길 바랍니다.

정석은 물품마다 태그를 달아 상품을 추천하지만, 사용자 폭이 200명 내외라는 것, 올라올 물품이 한정되어있다는 점에서 태그가 아닌 카테고리를 추천하게 되었습니다.

추천 api는 데이터가 일정량 모일 때마다 학습 코드를 실행해주어야 합니다. 추후 자동화 프로그램을 만드는 것을 계획 중입니다.

데이터의 형식은 다음과 같습니다. [1, 2, 3, 4, 5, 6, 1, 2]. 여기서 처음부터 6번째까지의 항목, 즉 1~6은 상품 열람 기록 카테고리입니다. 7번째 1은 성별을 나타냅니다. 1은 남성, 2는 여성, 3은 선택하지 않음을 나타냅니다. 마지막 항목은 학년입니다. 1, 2, 3은 각 학년을 나타내고, 4 이상은 졸업생을 나타냅니다. 정리하자면, 위의 예시는 2학년 남학생이 1, 2, 3, 4, 5번 카테고리 상품을 보고, 6번 상품을 열람중임을 나타냅니다.

로그를 전송할 때는 다음과 같이 주시면 됩니다.
`get_log?category=[1, 2, 3, 4, 5, 6]&sex=1$grade=2`

### Harmful Photo detector API

딥 러닝을 이용한 유해사진 검출 api입니다. DsmMarket의 사용자가 대여/판매 포스트를 올릴 때마다 사진이 api로 전송되어 검사합니다. object detection model은 yolo(darkflow)를 사용했습니다. 현재 검출하기로 한 유해 물품은 다음과 같습니다.

1. 담배, 담배곽
2. 소주, 양주
3. 날붙이(추가 예정)

이 중 하나의 물품이 포함되어있다고 판단되면 게시자에게 사진에 유해 물품이 검출되어 게시가 보류되었다고 알립니다. 