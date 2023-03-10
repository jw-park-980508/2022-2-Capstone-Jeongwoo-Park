# **Design of a Small-Scaled Wind Turbine Testbed for Bearing Fault Diagnosis** 

***School of Mechanical and Control Engineering***

***2022-2 Mechatronics Integration Project***



**Student: Jeongwoo Park**

**Advisor:**  **Prof.Youngkeun** **Kim**

-----------------------

본 연구는 풍력발전기의 실시간 모니터링의 필요성으로 인해 풍력발전기를 축소화한 테스트 벤치를 통해 데이터를 취득하고 풍력발전기의 부품인 베어링의 고장진단을 수행한 연구입니다. 



# Testbench

Testbench는 아래의 사진과  같이 3가지 유형의 실험(베어링 고장, 축정렬 불량, 질량 불균형)이 가능합니다. 이번 연구에서는 베어링의 고장, 축정렬 불량에 대한 실험만 진행했습니다.

#### 0. 사용방법

- 파워 서플라이 On
- 가변저항을 조절하여 입력 모터의 속도조절

![image](https://user-images.githubusercontent.com/84221531/208964624-de3da554-c9ac-42ee-81f6-416f54acf72c.png)

#### 1. Bearing Fault Test

- 베어링 결함의 종류는 Inner Fault, Ball Fault, Outer Fault 3가지 입니다. 

- 베어링 하우징을 모듈형태로 교체해서 12시 방향으로 가속도 센서를 고정하여 데이터를 취득하면 됩니다.

- 모든 가공은 EDM 방전가공 했습니다.

   **Inner, Outer Fault size**: 폭 1mm, 2.3mm        /       **Ball Fault**: 폭 1mm, 깊이 1mm



#### 2. Misalignment Fault Test

- 베어링 하우징을 좌우로 움직여 최대 3mm까지 축의 Offset 불량을 구현할 수 있습니다.

- 주의: 3mm까지 Offset을 가하면 부품의 파손이 있을수 있습니다.



#### 3. Mass Imbalance Fault Test

- Flywheel을 통해 윈드터빈의 블레이드를 모사했습니다. 

- 블레이드의 질량 불균형을 모사하기 위해 Flywheel에는 총 12개의 M6볼트 체결 탭이 있습니다.



# Bearing Fault Diagnosis

#### 1. Data Spec

- Sampling Frequency: 12[kHz]
- Total Time: 10[sec]
- Shaft(고속축) Speed: 500[rpm] 

  **CWRU data셋은 모델 성능의 비교를 위해 사용하였습니다.**



#### 2. Data Type

- 데이터의 분류는 아래의 테이블과 같이 3가지 Case로 구분하여 취득했습니다.

- 이후 사용되어질 Deep Learning 모델의 입력과 맞추기 위하여 1차원 : 1x4000   /    2 차원: 64x64 로 전처리 했습니다.



![image](https://user-images.githubusercontent.com/84221531/209155443-00c24ebb-ac87-4ce6-bdb8-752478637d92.png)



#### 3. Deep-Learning Model

- 베어링 고장진단을 위해 CWRU dataset을 사용했을 때 99%이상의 성능을 보였던 최신기법 1D- CNN, 2D-CNN, CNN-LSTM 3가지를 선정했습니다. 

![image](https://user-images.githubusercontent.com/84221531/209174875-e43218e6-635f-4f3a-9e6e-6b0855751428.png)

####   Reference

​	**[1]** **Chen et al, An improved fault diagnosis using 1D-convolutional neural network model, 2020**

​    **[2] Wen et al, A new convolutional neural network-based data-driven fault diagnosis method, 2017**

​	**[3]** **Chen et al, Bearing fault diagnosis base on multi-scale CNN and LSTM model, 2021**



#### 4. Result

- 1D - CNN

|               | **CASE  1** | **CASE  2** | **CASE  3** |
| ------------- | ----------- | ----------- | ----------- |
| Accuracy (%)  | 100         | 80.33       | 71.00       |
| Precision (%) | 100         | 81.40       | 71.39       |
| Recall (%)    | 100         | 80.33       | 71.06       |
| F1_score (%)  | 100         | 80.51       | 70.39       |

- 2D - CNN

|               | **CASE  1** | **CASE  2** | **CASE  3** |
| ------------- | ----------- | ----------- | ----------- |
| Accuracy (%)  | **100**     | **100**     | **97.64**   |
| Precision (%) | **100**     | **100**     | **97.64**   |
| Recall (%)    | **100**     | **100**     | **97.64**   |
| F1_score (%)  | **100**     | **100**     | **97.63**   |

- CNN - LSTM

|               | **CASE  1** | **CASE  2** | **CASE  3** |
| ------------- | ----------- | ----------- | ----------- |
| Accuracy (%)  | 99.00       | 84.67       | 63.00       |
| Precision (%) | 99.09       | 85.45       | 67.05       |
| Recall (%)    | 99.00       | 84.67       | 63.14       |
| F1_score (%)  | 99.00       | 84.90       | 61.23       |

















