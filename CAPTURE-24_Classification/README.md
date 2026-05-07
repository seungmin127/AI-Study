# Capture-24


## Capture-24 DataSet의 정의
이 데이터셋은 손목 착용형 3축 가속도계를 기반으로 sitting, standing, walking과 같은 정해진 행동을 통제된 환경에서 수행하도록 수집된 데이터가 아니라 참가자가 실제 일상생활을 수행하는 과정에서 자연스럽게 기록된 free-living 데이터셋이다.

- 사용 장비
    1. Axivity AX3 손목 가속도계
    2. 목걸이형 wearable camera
    3. sleep diary
- Axivity AX3 손목 가속도계 착용 위치: 우세손(주로 사용하는 손에서 활동 신호가 뚜렷하게 나타나 실제 행동을 더 잘 반영)
- 수집 시간: 약 24시간
- 참가자: 151명
- 총 데이터
    - 전체: 3,883시간
  	- 라벨 포함: 2,562시간 (실제 행동을 알고 있는 시간)

## 센서 데이터의 형태
CAPTURE-24는 시계열 데이터이기 때문에 시간 순서가 중요.
```
time        x-axis      y-axis      z-axis

t1          0.12        -0.83        0.54
```
- 100Hz로 해당 값을 1초에 100번 측정한다.
  
모델 학습을 위해 10초 길이의 비중첩 window로 잘라서 사용.

학습 샘플 1개

= 10초짜리 window

= 100Hz × 10초 × 3축

= 1000 timestep × 3축

= 입력 크기 (3, 1000)

## 라벨링 방식
CAPTURE-24의 가장 중요한 특징은 라벨 품질

일반적인 HAR 데이터셋은 참가자에게 특정 행동을 시킨 후 그 행동명 그대로 라벨링

- 예) 10:00~10:05 걷기

하지만 실제 생활에서는 행동이 이렇게 깔끔하지 않음.

- 예) 걸으면서 핸드폰 보기, 자동차 타기 등

이런 실제 활동을 정확하게 라벨링 하기 위해 wearable camera와 sleep diary를 사용

하나의 10초 window 안에는 여러 활동이 섞일 수 있음
- 0~4초: sitting
- 4~10초: standing

일반적으로 해당 window에서 가장 많이 차지하는 활동을 대표 라벨로 사용

-> **majority label 방식**

한계: 짧은 전환 행동은 사라질 수 있음

### Wearable camera의 역할
참가자는 깨어 있는 동안 목걸이형 wearable camera를 착용

가속도 데이터만 보고 라벨을 붙인 것이 아닌 해당 시간대의 실제 장면을 참고해 라벨을 부착

핵심: 손목 가속도만으로는 활동의 문맥을 알기 어렵기 때문에 wearable camera를 통해 정확한 행동에 대한 라벨을 부착

### Sleep diary의 역할
수면 시간은 wearable camera만으로 정확히 판단하기 어려움
- 잠자는 동안 카메라를 착용하지 않거나 이미지 정보가 부족할 수 있음.

따라서 수면 시간은 참가자가 sleep diary를 작성하여 보완함

**깨어 있는 시간 → wearable camera 기반**

**수면 시간 → sleep diary 기반**

CAPTURE-24의 공개 데이터에는 카메라 이미지 자체는 포함되지 않음

-> 개인정보 보호 때문에 텍스트 기반 주석만 제공

## 활동 강도 분류(Activity Intensity Classification)
-> Walmsley2020 라벨 기준
활동을 강도 기준으로 분류 진행

**클래스는 4개**
- sleep
- sedentary
- light physical activity
- moderate-to-vigorous physical activity

### sleep
수면 상태.
움직임이 매우 적고 긴 시간 동안 비슷한 패턴

but 손목을 움직이지 않는다고 항상 sleep은 아님

-> 그래서 sleep diary 기반 라벨이 중요

### sedentary
앉기, 누워 있기, 정적인 활동을 포함

-> 몸 전체 활동은 낮지만 손목 움직임은 발생

### light physical activity
천천히 걷기, 가벼운 집안일 등 가벼운 신체 활동

### moderate-to-vigorous physical activity
빠르게 걷기, 뛰기, 운동 등 중등도 이상 신체활동

-> 이 클래스는 하루에 얼마나 활동적인지 평가 가능하고 건강 지표로 사용되기에 중요

## 일상활동 분류(ADL Classification)
-> WillettsSpecific2018 라벨 기준
일상생활 활동으로 분류 진행

**클래스는 10개**
- sleep: 수면 상태로, 움직임이 적고 일정한 패턴을 보임
- sedentary-screen: TV, 스마트폰 등 화면 기반 정적 활동으로, 움직임이 적지만 미세한 손목 움직임 존재
- sedentary-non-screen: 독서, 휴식 등 비화면 정적 활동으로, 움직임이 거의 없음
- walking: 걷기 활동으로, 일정한 주기의 반복적인 패턴을 보임
- vehicle: 차량 이동 상태로, 움직임이 적어 sedentary와 혼동될 수 있음
- bicycling: 자전거 활동으로, 하체 중심 움직임이기 때문에 손목 센서에서는 패턴이 약하게 나타남
- tasks-light: 가벼운 집안일 등 비교적 작은 움직임을 포함한 활동
- tasks-moderate: 중간 강도의 집안일로, 손목 움직임이 더 크고 활발함
- sports-continuous: 지속적인 운동으로, 일정한 리듬과 큰 움직임이 특징
- sports-interrupted: 중간에 멈춤이 포함된 운동으로, 불규칙한 패턴을 보임

## CAPTURE-24는 어려운 데이터셋
CAPTURE-24는 현실적인 만큼 어려움

-> 이러한 특성 때문에 CAPTURE-24는 모델의 일반화 성능을 평가하기에 적합

### 활동 경계가 불명확 
실제 생활은 다음과 같다.
- 앉아 있다가 일어남
- 걸으면서 물건을 집음
- 서서 대화하다가 이동함
-> 활동의 시작과 끝이 애매하다.

### 클래스 불균형이 심하다
사람은 하루 중 많은 시간이 sleep, sitting, standing에 몰린다.

이 활동이 전체 활동의 60% 이상을 차지한다고 설명

-> 예를 들어 sitting이 대부분일 때 모델이 sitting만 많이 예측해도 accuracy가 좋아보일 수 있는 문제 발생

### 같은 활동도 사람마다 다름
- 팔을 크게 흔드는 사람
- 손을 주머니에 넣고 걷는 사람
- 가방을 들고 걷는 사람
  
-> 같은 walking 라벨이어도 센서 패턴은 다양

### 다른 활동이지만 센서 패턴이 비슷할 수 있음
- sitting vs vehicle
- sitting vs standing
- standing vs light household activity
- walking vs mixed-activity

-> 손목 가속도만으로 문맥을 완벽히 파악할 수 없음

## 평가 지표
CAPTURE-24 같은 데이터셋에서는 accuracy가 맞지 않음
-> 클래스 불균형이 심하기 때문이다

따라서 해당 지표들을 사용
### Macro-F1
클래스별 F1-score를 구한 뒤 평균을 낸다.

F1 = 2 × precision × recall / (precision + recall)

-> 데이터 개수가 적은 클래스도 동일하게 중요

Macro-F1은 다음 상황에서 중요
- sports 데이터는 적지만 중요하다
- bicycling 데이터는 적지만 구분해야 한다
- MVPA는 건강 모니터링에서 중요하다

### Cohen’s Kappa
Cohen’s κ는 우연히 맞출 확률(랜덤)을 제거한 진짜 분류 성능 지표

-> 그냥 찍어서 맞춘 것보다 얼마나 더 잘했는가?

κ = po-pe / 1−pe
- po: 실제 정확도
- pe: 우연히 맞출 확률
  
값의 범위: -1 ~ 1 (음수: 랜덤보다 못함, 0: 랜덤, 0.4: 보통, 0.6: 좋음, >0.8: 매우 좋음)
```
예)	| GT \ Pred | A  | B  |
	| A         | 50 | 10 |
	| B         | 5  | 35 |
```
po 공식
```
po = (대각선 합) / (전체 샘플 수)
	 = (50 + 35) / 100 
	 = 0.85
```
pe 공식
```
step 1. GT/Pred 비율 구하기
GT:
A = 60/100 = 0.6
B = 40/100 = 0.4

Pred:
A = 55/100 = 0.55
B = 45/100 = 0.45

step 2. 곱해서 더하기
pe = (0.6 × 0.55) + (0.4 × 0.45)
   = 0.33 + 0.18
   = 0.51
```
최종 공식
```
κ = (0.85 - 0.51) / (1 - 0.51)
  = 0.34 / 0.49
  ≈ 0.694
```

### MCC(Matthews Correlation Coefficient)
예측과 정답 간의 상관관계

-> 예측이 정답과 얼마나 닮았나?

MCC = TP⋅TN−FP⋅FN / root((TP+FP)(TP+FN)(TN+FP)(TN+FN))

값의 범위: -1 ~ 1 (1: 완벽, 0: 랜덤, -1: 완전 반대)

#### CAPTURE-24는 실제 일상생활 데이터를 반영한 free-living HAR 데이터셋으로 강한 클래스 불균형과 복잡한 활동 패턴을 포함하고 있어 현실적인 인간 행동 데이터를 이해하고 분석하는 데 적합하다.
