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

## WISDM Dataset의 주요 난제
**유사한 활동 간의 미세한 차이를 구분하기 어려움**
1. Walking, Upstairs, Downstairs가 모두 보행 계열 활동이기 때문에 가속도 센서 패턴이 유사하게 나타날 수 있음
2. 특히 Upstairs와 Downstairs는 모두 계단 이동 활동이므로 센서 신호가 매우 비슷함
   - 둘 다 주기적 패턴
   - x, y, z축 가속도 변화가 반복
   - 걷기와 유사한 패턴
   - 차이는 주로 충격 강도, 리듬, 축 방향 변화의 미세한 차이에서 나타남
<img width="850" height="542" alt="image" src="https://github.com/user-attachments/assets/120bd32d-0f98-4ca3-bf62-8eb36eac20db" />

3. 클래스 불균형 문제
   
   WISDM은 walking, jogging 데이터가 많고 sitting, standing 데이터가 적음
   
```text
Activity counts:
activity
Walking      424397
Jogging      342176
Upstairs     122869
Downstairs   100427
Sitting       59939
Standing      48395
```
  - 모델이 데이터가 많은 활동에 치우쳐 학습될 가능성이 있음
  따라서 class_weight를 부여하여 데이터가 적은 클래스의 loss를 더 크게 반영하고 모델이 다수 클래스에 치우쳐 학습되는 것을 막음
