# Energy_Transfer-of-demand

paper link:

1. Device predict file
<br/> 12개 기기별 전력 사용량을 lstm모델을 활용하여 1월부터 10월까지의 데이터를 학습시켜 11월 1달간의 사용량(1분단위)을 예측
<br/> 수요이전을 하기 위해서는 기기별로 클러스터링을 진행해야하기 때문

2. A_clustering
<br/> 최대부하 시간에서의 기기별 예측값을 Timeseries K-means로 클러스터링

4. A_DTW_FARE
<br/> K-means를 사용하여 최대부하시간대에서의 수요이전할 전력량과 남아있어야할 전력량의 요금계산

6. A_Energy_predict
<br/> 다변량 LSTM모델을 사용하여 1~10월까지 1분단위로 외부요인들과 함께 학습시키고 11월 한달의 전력 샤용량을 예측

8. A_trans_ex
<br/> 총 전체 사용량으로 수요이전 (기준치는 한달 전력사용량의 평균 값)
<br/> 절감율이 원하는 만큼 안나와서 기기별로 수요이전으로 프로세스 변경

11. D_dtw

13. Device_all

15. Energy_Day2

17. M_dtw

19. mape

21. transfer
