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


## Tssk
- Feature들을 바탕으로 Binary Classification Task를 수행
- 이후 Softmax 함수를 통해 최종 label이 나온 확률을 추출하여 이를 바탕으로 Softmax 값(발병 확률)을 낮추는 활동 추천
