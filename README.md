
# 카카오톡 대화 요약 프로젝트
## 조이름 : SpeedWagon
### Boaz base mini project - Korean text summarization


2023.05.19 ~

### 개요
- 가끔 핸드폰을 못 봐서 카카오톡이 쌓여있어서 어떤 대화가 있었는지 불편할 때가 있음
- 회의에서 일일히 모든 내용을 적기에는 불편함


### 프로젝트 과정
한국어 대화요약 모델을 가져와서 대화데이터를 학습시켜서 모델링. 이때 모델은 kobart 모델을 가져옴. 데이터는 ai_hub의 일상대화 데이터를 학습시킴으로써 카카오톡에 있는 일상 대화를 요약할 수 있게 함 또한 나타난 요약 데이터를 감성분석을 하여서 해당 요약이 제대로 되었나 검

- ai_hub데이터 전처리
- kobart fine_tuning
- rouge 스코어로 평가지표 생성

데이터로 학습 시키기
![image](https://github.com/youngwoo3283/SpeedWagon/assets/69841073/4b444c3d-4cbd-4a30-9207-62728d3a91ef)



### 이후 계획
- optuna 같은 라이브러리로 하이퍼파라미터 튜닝 및 최적화
- 감성분석으로 요약이 잘 됬나 확인
- kobart 말고 KOT5같은 다른 모델들을 허깅페이스에서 가져와서 시도해보기


### 어려웠던 점

- 학습시에 데이터가 커서 코랩 환경에서 실행한 결과 메모리 초과로 실행 불가
- 로컬에 gpu 환경을 구성해서 하려고 하였으나 토치 환경에서 gpu적용하기 어려움
  - 텐서플로우에서는 gpu 나온 것을 확인 but torch는 cuda와 토치 버전의 문제로 계속 안됨

- 문장의 불완전성
  - 문장이 완전하게 끝나지 않는 문제점 발생

### 보완할 점 
- kobart말고도 kot5나 mt5등의 요약 모델의 적용
- 
