# UCI HAR Dataset
   - 스마트폰 센서 데이터를 이용해 사람의 행동을 분류하기 위해 만들어진 대표적인 시계열 분류 데이터셋

### Dataset에 활용된 센서
  - 가속도 센서 (accelerometer)
    - 움직임에 따른 가속도, 중력 방향 측정
  - 자이로 센서 (gyroscope)
    - 회전 속도 측정
### 센서를 통해 수집된 데이터
- WALKING : 걷기
- WALKING_UPSTAIRS : 계단 오르기
- WALKING_DOWNSTAIRS : 계단 내려가기
- SITTING : 앉기
- STANDING : 서있기
- LAYING : 눕기

### 데이터 설명

- body_acc_x, y, z : 몸의 순수 가속도
- body_gyro_x, y, z : 각속도
- total_acc_x, y, z : 전체 가속도

하나의 샘플은 **(128, 9)** 형태로 구성

- 128: 시간 길이  
- 9: 센서 특성 수
