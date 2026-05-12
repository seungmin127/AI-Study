# WISDM Dataset
스마트폰 가속도 센서 데이터를 이용해 사람의 일상 행동을 분류하기 위해 만들어진 HAR 시계열 분류 데이터셋

### Dataset에 활용된 센서
 - 가속도 센서 (accelerometer)
 - 움직임에 따른 x, y, z축 가속도 측정
    
### 센서를 통해 수집된 데이터
 - Walking : 걷기
 - Jogging : 조깅
 - Upstairs : 계단 오르기
 - Downstairs : 계단 내려가기
 - Sitting : 앉기
 - Standing : 서있기

### 데이터 설명
 - user : 참가자 ID
 - activity : 수행한 행동 label
 - timestamp : 센서 데이터가 기록된 시간
 - x-acceleration : x축 가속도
 - y-acceleration : y축 가속도
 - z-acceleration : z축 가속도

하나의 raw data는 다음 형태로 구성됨
(user, activity, timestamp, x, y, z)

실제 데이터
33,Jogging,49105962326000,-0.6946377,12.680544,0.50395286;
