# mHealth Dataset
MHEALTH Dataset은 wearable body sensor를 이용해 사람의 신체 움직임과 생체 신호를 함께 측정한 HAR 시계열 분류 데이터셋

### Dataset에 활용된 센서
 - 가슴 센서
	- 3축 가속도 센서
	- ECG 2채널
 - 왼쪽 발목 센서
	- 3축 가속도 센서
	- 3축 자이로스코프
	- 3축 자기장 센서
 - 오른쪽 아래팔 센서
	- 3축 가속도 센서
	- 3축 자이로스코프
	- 3축 자기장 센서
    
### 센서를 통해 수집된 데이터
 - Standing still : 가만히 서 있기
 - Sitting and relaxing : 앉아서 쉬기
 - Lying down : 누워 있기
 - Walking : 걷기
 - Climbing stairs : 계단 오르기
 - Waist bends forward : 허리 앞으로 굽히기
 - Frontal elevation of arms : 팔 앞으로 올리기
 - Knees bending : 무릎 굽히기
 - Cycling : 자전거 타기
 - Jogging : 조깅
 - Running : 달리기
 - Jump front and back : 앞뒤로 점프하기

### 데이터 설명
여러 센서 값이 숫자 column으로 저장된 형태
 - column 1~3	가슴 센서의 x, y, z축 가속도
 - column 4~5	ECG lead 1, ECG lead 2
 - column 6~8	왼쪽 발목 센서의 x, y, z축 가속도
 - column 9~11	왼쪽 발목 센서의 x, y, z축 자이로스코프
 - column 12~14	왼쪽 발목 센서의 x, y, z축 자기장
 - column 15~17	오른쪽 아래팔 센서의 x, y, z축 가속도
 - column 18~20	오른쪽 아래팔 센서의 x, y, z축 자이로스코프
 - column 21~23	오른쪽 아래팔 센서의 x, y, z축 자기장
 - column 24	activity label
   
하나의 raw data는 다음 형태로 구성
```
(
chest_acc_x, chest_acc_y, chest_acc_z,
ecg_1, ecg_2,
left_ankle_acc_x, left_ankle_acc_y, left_ankle_acc_z,
left_ankle_gyro_x, left_ankle_gyro_y, left_ankle_gyro_z,
left_ankle_mag_x, left_ankle_mag_y, left_ankle_mag_z,
right_arm_acc_x, right_arm_acc_y, right_arm_acc_z,
right_arm_gyro_x, right_arm_gyro_y, right_arm_gyro_z,
right_arm_mag_x, right_arm_mag_y, right_arm_mag_z,
label
)
```
실제 데이터
```
-9.8184	0.009971	0.29563	0.0041863	0.0041863	2.1849	-9.6967	0.63077	0.1039	-0.84053	-0.68762	-0.37	-0.36327	0.29963	-8.6499	-4.5781	0.18776	-0.44902	-1.0103	0.034483	-2.35	-1.6102	-0.030899	0
```
