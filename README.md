# entertain_stock_2023_4

## 비금융 데이터를 활용한 엔터테인먼트 주가 예측
- 2023 명지대 SW경진대회 출품작(빅데이터 분석 부분)
- 기간: ‘23년 07월 ~ ‘23년 08월(1개월)
- 성과: 최우수상 (2등) 수상
- Tools: python
- 활용 데이터
  - entertainment 주식회사별 거래 데이터 (2016.01~2023.06)
  - 멜론음원차트 top 100 음원 순위 데이터 (2016.01~2023.06)
  - 네이버 뉴스 기사 크롤링 데이터 (2016.01~2023.06)
<br>


## 1️⃣ 프로젝트 개요
하이브,SM 인수문제 => 많은 뉴스 기사들 발생. 
해당 기사들을 통해 주가 예측이 가능할까? 라는 아이디어에서 출발한 비금융 데이터를 통한 주가예측 프로젝트

## 2️⃣ 주제 정의
주식 가격예측을 과거의 주식 거래데이터로만 예측하는 것이 아닌, **비금융 데이터를 활용한 엔터테인먼트 주가 예측**으로 정의하였음.
엔터테인먼트 분야 특성상 많은 뉴스기사가 작성되고,  음원차트를 통해 매일 음원 성적이 나오기 때문에 적합한 주식 분야로 여겨짐

## 3️⃣ 목적 및 의의
주식 가격 예측을 경제적인 부분에서 벗어나 비금융 데이터를 활용해 예측하고 모델의 정확도를 높임으로써 주식 예측을 하는데에 있어 다양한 데이터를 활용함에 의의를 둠.

## 4️⃣ 진행 과정 
❶문제정의 ❷데이터 수집 및 가공 ❸데이터 분석 ❹모델 개발 ❺가격 예측 ❺결론

### 👤담당 역할
기획,데이터 수집, 데이터 분석, 데이터 시각화, 모델개발
<br>

### 🧐 Main Issues
비금융 데이터를 뉴스기사 크롤링과 음원차트 크롤링을 통해 수집하고 가공하는 과정이 중요한 문제였음. 
특히 뉴스 크롤링한 뉴스기사를 긍정,부정,중립으로 나누는 과정에서 기존 영어 경제기사를 학습시킨 KLUE BERT-base model을 불러와서 라벨링을 할 것인지. 새롭게 모델을 만들어 라벨링을 할 것인지가 중요 쟁점으로 작용함.

### 🛠️ Resolved
크롤링한 뉴스 기사의 제목을를 토큰화하여 형태소 분석을 진행 빈도수 기준으로 내림차순 나열 후 사전 생성.
불용어 제거후 컬럼에 대해 토큰화(형태소 분석)을 재진행 하여 단어 1000개에 대해 빈도수 기준으로 정렬
긍정 166개 부정 99개로 구성된 긍∙부정 단어 리스트를 생성(단어 자체가 긍정 부정인 경우만 판별)
긍정,부정,중립으로 다시 나누고 기사별로 score를 측정해 활용하였음. 1이상이면 긍정, 0이면 중립, 0이하면 부정 으로 label column생성.

### 🎯 Result
##모델부분
lstm,gru,통계 모델 ARIMA
3가지 모델을 학습 후 비교,
MAE, RMSE, RMSLE, R2에서 모두 좋은 수치를 기록한 GRU 선택.

##분석결과

큐브엔터, 와이지엔터테인먼트
“뉴스 제목 감정”과 “음원차트 점수” 추가 사용시 모델이 개선됨
에스엠, 하이브, JYP Ent., 에프엔씨엔터는 
“뉴스 제목 감정”과 “음원차트 점수”추가 사용시 모델 개선 되지 않음

### ⭐ Learnd Lessons
시계열 데이터를 학습해 lstm,gru,arima 모델을 통해 학습해보는 경험을 하였습니다. 또한 web driver를 통해 크롤링을 하는 경험을 하였으며,
뉴스 기사 토큰화와 라벨링을 통해 감성분석을해 데이터셋을 만들어 보았습니다.
다만 아쉬운점은 시계열 데이터의 특성을 활용한 롤링변수나 sin,cos 변환을 통해 파생변수를 추가해 시계열 데이터의 특성을 살려서 더 인사이트를 도출해 내었다면 좋았을 것이라는 생각을 하였습니다.
추후에는 이러한 시계열 특성을 고려한 방법을 적용해 보고자 합니다.

![image](https://github.com/ASJ0211/entertain_stock_2023_4/assets/118821779/9f94e8b4-a882-4dbb-a665-0128fdd1938e)
![image](https://github.com/ASJ0211/entertain_stock_2023_4/assets/118821779/4a06e404-88cb-4702-b627-a3f2bcdf1e36)
![image](https://github.com/ASJ0211/entertain_stock_2023_4/assets/118821779/103af85c-74a3-44ef-a3f2-c0572225ce7f)

![image](https://github.com/ASJ0211/entertain_stock_2023_4/assets/118821779/1010517c-9da8-4e3d-828b-fad0f0771d18)
![image](https://github.com/ASJ0211/entertain_stock_2023_4/assets/118821779/714deff4-d90c-4424-a940-db030f4224f5)
![image](https://github.com/ASJ0211/entertain_stock_2023_4/assets/118821779/74dd4bd8-d014-4bc9-9773-9242b8f27b9c)
큐브엔터, 와이지엔터테인먼트
“뉴스 제목 감정”과 “음원차트 점수” 추가 사용시 모델이 개선됨

에스엠, 하이브, JYP Ent., 에프엔씨엔터는 
“뉴스 제목 감정”과 “음원차트 점수”추가 사용시 모델 개선 되지 않음

![image](https://github.com/ASJ0211/entertain_stock_2023_4/assets/118821779/6a97516a-4d50-4fe1-921c-625369643d87)
