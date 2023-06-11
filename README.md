
# 카카오톡 대화 요약 프로젝트
## 조이름 : SpeedWagon
### Boaz base mini project - Korean text summarization


2023.05.19 ~ 2023.06.08

### 개요
- 가끔 핸드폰을 못 봐서 카카오톡이 쌓여있어서 어떤 대화가 있었는지 불편할 때가 있음
- 회의에서 일일히 모든 내용을 적기에는 불편함

![image](https://github.com/youngwoo3283/SpeedWagon/assets/69841073/10ac0f68-d9b4-47b2-b6a7-f08412915328)




### 프로젝트 과정
한국어 대화요약 모델을 가져와서 대화데이터를 학습시켜서 모델링. 이때 모델은 kobart 모델을 가져옴. 데이터는 ai_hub의 일상대화 데이터를 학습시킴으로써 카카오톡에 있는 일상 대화를 요약할 수 있게 함 또한 나타난 요약 데이터를 감성분석을 하여서 해당 요약이 제대로 되었나 검

- ai_hub데이터 전처리
- kobart fine_tuning
- rouge 스코어로 평가지표 생성

- kobart 말고 KOT5같은 다른 모델들을 허깅페이스에서 가져와서 시도해보기
  - KoT5로 해본 결과 학습은 잘 되지만 더 성능이 떨어짐 


![image](https://github.com/youngwoo3283/SpeedWagon/assets/69841073/c8a041b1-5d88-42be-ab96-4191bd1ec1e9)




데이터로 학습 시키기
![image](https://github.com/youngwoo3283/SpeedWagon/assets/69841073/4b444c3d-4cbd-4a30-9207-62728d3a91ef)

- optuna 같은 라이브러리로 하이퍼파라미터 튜닝 및 최적화
  - 학습률과 가중치 감소율을 튜닝함
  - epoch나 나머지도 튜닝할 수는 있지만 너무 시간이 오래걸려서 learning_rate와 weight_decay만 튜닝해봄
  - learning_rate': 3e-05, 'weight_decay': 0.2

![image](https://github.com/youngwoo3283/SpeedWagon/assets/69841073/192dcd64-b103-4b97-bb51-179dfe5b128c)



- 감성분석으로 요약이 잘 됬나 확인
  - 허깅페이스에 있는 bert모델로 시도해봄
  - 감성분석을 하긴 하지만 잘못되는 케이스가 많음

![image](https://github.com/youngwoo3283/SpeedWagon/assets/69841073/1f373350-98c8-4722-885f-e06db028c0a7)


![image](https://github.com/youngwoo3283/SpeedWagon/assets/69841073/1e29f3f4-5f27-4faa-a6c3-5f90d7f106b7)



### 실제 카카오톡 데이터를 사용해보기
- 실제 회의록의 내용을 모델에 넣어서 요약과 감성 분석을 해보기

데이터
![image](https://github.com/youngwoo3283/SpeedWagon/assets/69841073/1f915ea9-fb6e-4a41-a078-bf94b73b411c)

회의록
![image](https://github.com/youngwoo3283/SpeedWagon/assets/69841073/92948ba0-b427-4c66-bf35-2f0f3caffc77)


![image](https://github.com/youngwoo3283/SpeedWagon/assets/69841073/90ffad33-83b2-40eb-8c06-cc7b97ec3a52)




### 느낀점 
- 데이터를 학습시킬때 대용량이면 고성능 gpu가 필요하고, 로컬 환경설정이 필요하다는 것을 깨달음
- 로컬 환경설정을 해보게 되서 다음에는 적용할 수 있을 것 같다
- 트랜스포머 기반의 프로젝트를 해볼 수 있어서 좋았던 것 같다
- 성능 좋은 한국어 전처리 라이브러리의 필요성 



### 어려웠던 점

- 학습시에 데이터가 커서 코랩 환경에서 실행한 결과 메모리 초과로 실행 불가
- 로컬에 gpu 환경을 구성해서 하려고 하였으나 토치 환경에서 gpu적용하기 어려움
  - 텐서플로우에서는 gpu 나온 것을 확인 but torch는 cuda와 토치 버전의 문제로 계속 안됨

- 문장의 불완전성
  - 문장이 완전하게 끝나지 않는 문제점 발생

- 회의록에서의 감성분석 효율성
  - 회의록이다 보니 감정이 들어간 말이 별로 없어서 예측이 어려움
  - 일반 대화에서는 적용이 가능 할 듯

### 보완할 점 
- 기존에 사용한 모델 말고 mt5등의 요약 모델의 적용
- 30만개의 데이터를 사용했지만 더 큰 규모의 데이터를 적용
- 맞춤법 검사기등 다양한 라이브러리 적용
