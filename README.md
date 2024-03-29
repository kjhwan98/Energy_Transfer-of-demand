## Energy_Transfer-of-demand

paper link: https://www.kci.go.kr/kciportal/ci/sereArticleSearch/ciSereArtiView.kci?sereArticleSearchBean.artiId=ART002956737

### 기술 개요
우리나라는 빠른 GDP 성장과 함께 에너지 소비량이 계속해서 증가하고 있다. 이에 따라 에너지 효율화가 중요시되고 있다. 이에 따라 에너지 효율 향상으로 소비감축을 시행하는 새로운 에너지 시스템이 대두
<br/>현재 수집되고 있는 에너지 사용량을 비롯한 다양한 정보들을 활용하여 솔루션을 확대하면서 사용자에게 DB에 있는 정보들을 활용하여 유의미한 데이터를 전달해줄 수 있는 서비스가 필요
<br/>기업에서 보유하고 있는 스마트플러그와 게이트웨이를 활용하여 운영중인 에너지 사용량 예측 모델에 기반한 기기별/수용가별 사용 요금을 예측하고 수용가별 맞춤형 수요이전 서비스의 구현을 위하여 사용패턴 학습관리를 통한 지능형 수요이전 제안 알고리듬 구현이 필요

### 기술 프로세스
사용자의 전력 데이터 사용량을 기반으로 사용량과 사용 요금을 예측하고, 패턴화 하여 맞춤형 수요이전 서비스를 제공하여 똑같은 전력량을 사용하더라도 요금절감을 통하여 효과적인 전력 사용 도모
<br/> (1) 에너지 사용량 예측
<br/>   · 각 사용자 및 전기기기별 에너지 사용량 예측 모델 개발
<br/>   · 예측 데이터 기반 예상 전기요금 산출(수치화) 모델 개발
<br/> (2) 맞춤형 수요이전 제안 시스템
<br/>   · 에너지 사용 학습관리 및 위 (1)과 연계되는 수요이전 제안 시스템
<br/> (3) 위 (2)를 위한 연동 제어 시스템(지능형 스케쥴 제어) 설계
<br/> <p align="left"> <img src = "https://user-images.githubusercontent.com/104756502/217471745-52e326e9-85ab-497f-8882-4dd6eb3ffad0.png" width="250" height="300"> <br/>

### 사용데이터
Smart Home Dataset with weather Information(https://www.kaggle.com/datasets/taranvee/smart-home-dataset-with-weather-information/code?select=HomeC.csv)
<br/> <img src =https://user-images.githubusercontent.com/104756502/217474586-9cd20ef2-7eb8-4588-9ee5-57cd0cd97ec5.png width="400" height="150">

### 파일 설명
1. Device predict file
<br/> 12개 기기별 전력 사용량을 lstm모델을 활용하여 1월부터 10월까지의 데이터를 학습시켜 11월 1달간의 사용량(1분단위)을 예측
<br/> 수요이전을 하기 위해서는 기기별로 클러스터링을 진행해야하기 때문

2. A_DTW_FARE
<br/> K-means를 사용하여 최대부하시간대에서의 수요이전할 전력량과 남아있어야할 전력량의 요금계산

3. A_Energy_predict
<br/> 다변량 LSTM모델을 사용하여 1~10월까지 1분단위로 외부요인들과 함께 학습시키고 11월 한달의 전력 샤용량을 예측

4. A_trans_ex
<br/> 총 전체 사용량으로 수요이전 (기준치는 한달 전력사용량의 평균 값)
<br/> 절감율이 원하는 만큼 안나와서 기기별로 수요이전으로 프로세스 변경

5. Device_all
<br/> 앞서 기기별로 다변량 LSTM 모델을 사용하여 예측했던 값들을 통합

6. M_dtw
<br/> 모든 기기들의 한달동안의 사용 예측량을 클러스터링
<br/> 최대부하 시간에서의 기기별 예측값을 Timeseries K-means로 클러스터링
<br/> 클러스터터를 2로 설정하여 0,1 중에서 1로 분류된 항목들이 수요이전할 항목

7. mape
<br/> 에너시 사용량 예측 모델 정확도와 에너지 요금 예측 모델 정확도를 mape로 계산

8. transfer
<br/> 최대부하시간에서의 클러스터링이 1인 전력량들을 경부하시간대로 이전

9. Savingrate
<br/> 수요이전을 통한 요금절감률 계산
