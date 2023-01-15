# KAU-RecSys
## 2022-1 학기 추천시스템

심장질환 예방을 위한 추천시스템 (2022.04 ~ 2022.06) / 

## Data 
- 319.7k 명의 17가지 feature들에 대한 정보로 구성
- 미국질병통제예방센터에서 제작 (CDC, Centers for Disease Control and Prevention)
https://www.kaggle.com/datasets/kamilpytlak/personal-key-indicators-of-heart-disease

![Heart_disease_prediction_9조](https://user-images.githubusercontent.com/94584793/212479049-cca39ed7-6d0f-4345-9359-4b62fed96735.jpg)

- Correlation matrix를 바탕으로 심장질환과 연관성이 높은 feature들을 파악
![Heart_disease_prediction_9조](https://user-images.githubusercontent.com/94584793/212479602-80ecf43e-7125-4a54-9b9b-36f3b15bf40f.jpg)

- EDA를 통해 feature들에서 다음과 같은 특징을 확인
1. Smoking (흡연 유무) 
심장질환이 발병된 사람 중 58.6 %가 흡연, 심장질환이 없지만 흡연하는 사람은 5.5%

2. Diffwalking(계단을 오를 때 어려움을 느끼는 유므)
심장질환이 발병된 사람 중 Diffwalking이 True인 사람은 36.6%

3. Diabetic (당뇨 유무)
심장질환이 발병된 사람 중 Diabetic이 True인 사람은 32.7%

4. PhysicalActivity (최근 30일 중 육체적인 운동 유무)
심장질환이 True인 사람 중 63.9%가 False로 응답

5. 연령이 높아질수록 심장질환 환자수가 증가


## Task
- Feature들을 바탕으로 Binary Classification Task를 수행
- 이후 Softmax 함수를 통해 최종 출력값이 나오게 된 확률을 추출 
- 이를 바탕으로 Softmax 값(발병 확률)을 낮추는 활동 추천


## t-SNE
- t-SNE를 활용하여 고차원 데이터를 시각화
- 데이터가 어떠한 기준으로 군집을 이루고 있음을 확인
![Heart_disease_prediction_9조](https://user-images.githubusercontent.com/94584793/212541192-d82767f7-b64c-4f58-b12d-531c2b2f6f0c.jpg)

## Logistic Regression
- 선형회귀를 이용하여 발병 가능성 수치화 시도
- 아래 이미지에서 확인 가능하듯이 이상치가 많으며, 이를 수치화하기 어려움
![Heart_disease_prediction_9조](https://user-images.githubusercontent.com/94584793/212541380-61993d03-1472-4c1d-ab6b-aafcfde57f5a.jpg)

- SVM (Support Vector Machine), K-NN (K-Nearest Neighbor)을 진행하였지만, 유의미한 결과를 얻지 못함

## Custom Model (Fully Connected Network)
- FC Layer와 ReLU로 이뤄진 모델로 실험을 진행
- 당시에는 Batch Normalizatiokn에 대한 이해도 낮아 비교 실험 대상으로 FC Layer + Batch Normalization + ReLU 구조의 모델을 선택
(Batch Normalization을 적용하면 배치별로 정규화가 적용되는데, 정규화된 값에 ReLU를 적용하면 데이터의 절반인 0 이하의 값은 손실되는 문제가 발생)
- 모델은 12개의 Hidden Layer와 ReLU가 적용된 단순한 구조
- Weight 값의 초기화를 위해 Xavier와 Kaiming 초기화를 사용

## Application for RecSys
- 학습 결과 중 가장 높은 정확도를 보인 Weight를 저장 후, 출력값에 Softmax 함수를 적용시켜 발병 가능성을 추출
- 발병 가능성을 확인 후, 어떤 Input (Feature)를 조절하면 발병 가능성이 줄어드는지 확인

![Heart_disease_prediction_9조](https://user-images.githubusercontent.com/94584793/212544613-4915c8bf-a5ba-48b3-82e2-d005bb4b2079.jpg)


