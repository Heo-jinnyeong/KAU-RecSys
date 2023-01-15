# KAU-RecSys
## 2022-1 학기 추천시스템

심장질환 예방을 위한 추천시스템 (2022.04 ~ 2022.06) / 

## Data 
- 319.7k 명의 17가지 feature들에 대한 정보로 구성
- 미국질병통제예방센터에서 제작 (CDC, Centers for Disease Control and Prevention)
https://www.kaggle.com/datasets/kamilpytlak/personal-key-indicators-of-heart-disease

![Heart_disease_prediction_9조](https://user-images.githubusercontent.com/94584793/212547373-4c82e802-ce7b-4d83-a7a5-1495045e795b.jpg)

- Correlation matrix를 바탕으로 심장질환과 연관성이 높은 feature들을 파악

![Heart_disease_prediction_9조](https://user-images.githubusercontent.com/94584793/212547393-396ea1a0-1c62-4a53-9f72-f7cb59b03a8e.jpg)

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
![Heart_disease_prediction_9조](https://user-images.githubusercontent.com/94584793/212547411-b6cfd810-9333-4162-a523-235c2949fc1b.jpg)

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
- 학습 결과 중 가장 높은 정확도를 보인 Weight를 저장 후, 이를 적용시킨 모델의 출력값에 Softmax 함수를 적용시켜 발병 가능성을 추출
- 발병 가능성을 확인 후, 어떤 Input (Feature)를 조절하면 발병 가능성이 줄어드는지 확인

![Heart_disease_prediction_9조](https://user-images.githubusercontent.com/94584793/212544613-4915c8bf-a5ba-48b3-82e2-d005bb4b2079.jpg)

![Heart_disease_prediction_9조](https://user-images.githubusercontent.com/94584793/212545002-83c7a144-4bb9-4618-8b79-f7537d9f9619.jpg)

- 심장질환이 있는 사람의 Softmax를 거친 결과와 그렇지 않은 사람의 결과를 비교해보면, 아래 그림처럼 유의미한 차이를 확인 가능
![Heart_disease_prediction_9조](https://user-images.githubusercontent.com/94584793/212545853-9980fcdf-0ec9-4981-98c3-e2c9c3bd7598.jpg)

- 임의로 1명을 선택하여 Correlation Matrix와 EDA 결과를 바탕으로 Key Feature라 할 수 있는 몇 개 Feature를 조절하여 발병 가능성의 변환을 관찰
- Dataset에는 존재하지 않는 4명에 대해 설문조사를 실시 후, 발병 가능성이 가장 높은 1명의 Feature를 조절
- EDA 결과에서 연령대가 높아질수록 발병 환자가 많기 때문에 20대에서는 다소 낮은 발병 가능성을 보이지만, 연령이 증가할수록 발병 가능성이 높아짐을 확인
- 발병 가능성이 가장 높은 연령대로 고정시킨 후, 어떤 Feature를 조절해야 발병 가능성이 낮아짐을 확인



![Heart_disease_prediction_9조](https://user-images.githubusercontent.com/94584793/212546477-8715cc57-533a-4ce1-92aa-982fc9f9a318.jpg)
![Heart_disease_prediction_9조](https://user-images.githubusercontent.com/94584793/212546524-b7bf2251-a685-4107-aecf-f8958dc5d672.jpg)
![Heart_disease_prediction_9조](https://user-images.githubusercontent.com/94584793/212546622-6b5cc61c-df19-4f30-ba27-7eaa57336073.jpg)
![Heart_disease_prediction_9조](https://user-images.githubusercontent.com/94584793/212546639-24c23476-5894-4efd-aea1-3a6d2d4957da.jpg)
![Heart_disease_prediction_9조](https://user-images.githubusercontent.com/94584793/212546655-495a3e43-7405-4b4f-aa12-fe0c423a285c.jpg)
![Heart_disease_prediction_9조](https://user-images.githubusercontent.com/94584793/212546668-7bd0b204-fc86-461b-857a-5c43eaa61c6d.jpg)


## Conclusion
- EDA와 Correlation Matrix를 통해 얻은 Feature들로 심장질환 발병 가능성을 낮추는 활동 추천 가능함을 도출
![Heart_disease_prediction_9조](https://user-images.githubusercontent.com/94584793/212546899-da6a9af6-8998-4fd8-a138-2a4360a87463.jpg)

## Limitation
- 발병 유무의 불균형과 인종에 대한 불균형으로 성능을 일반화하기에는 한계가 존재
- 추후 불균형 해소를 위한 데이터 수집이 필요

![Heart_disease_prediction_9조](https://user-images.githubusercontent.com/94584793/212547065-f19298a4-305f-4cb7-bb70-549299b6ba92.jpg)
![Heart_disease_prediction_9조](https://user-images.githubusercontent.com/94584793/212547084-f2975be4-139f-4012-a5b0-a2d1ea47f62d.jpg)

reference
Data - https://www.kaggle.com/datasets/kamilpytlak/personal-key-indicators-of-heart-disease



