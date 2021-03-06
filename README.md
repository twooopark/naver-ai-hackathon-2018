# 네이버 AI 해커톤 2018

[네이버 AI 해커톤 2018](https://github.com/naver/ai-hackathon-2018)

Team Sadang 팀으로 참가하여 제작한 모델입니다.

</br>

## 네이버 지식iN 질문 유사도 예측 

### 구조

- 입력을 Tab기준으로 나눠서 모델에 넘기는 방식입니다.
- 모델은 BiGRU 2layer를 사용하며, 출력은 마지막 시퀀스의 레이어만 출력합니다.
- BiGRU를 통해 출력된 두 벡터에 대해 유클리드 거리를 계산합니다.
- 계산된 값을 scale & shift 한 다음 sigmoid 에 전달합니다.



### 설정

- 기본으로 주어지는 kor_char_parser 로부터 출력되는 인덱스에 +1을 하고 embedding을 251이 아닌 252로 설정했습니다.
- GRU의 히든 사이즈를  256로 설정했습니다.
- strmaxlen을 150으로 설정했습니다.
- 배치 사이즈를 128로 설정했습니다.
- 어떠한 전처리도 수행하지 않았으며, 어떠한 regularization 기법도 사용하지 않았습니다.



### 결과

83.468% 정확도 (1위)

</br>

## 네이버 영화 평점 예측 

### 구조

- 모델은 BiGRU 2layer를 사용하며, 출력은 마지막 시퀀스의 레이어만 출력합니다.
- 최종 출력단을 2개로 구성하였습니다. 하나는 감정분석하듯이 부정, 중립, 긍정 확률을 출력하고, 나머지 하나는 평점을 출력하도록 합니다.
- 먼저 BiGRU로부터 나온 벡터에 히든 사이즈가 3인 FC를 붙였으며, 그 뒤에 softmax를 취했습니다. 그 다음, softmax를 취하기전의 logit에 히든 사이즈가 1인 FC를 붙이고, 그 뒤에 sigmoid를 취했습니다.
- loss는 cross entropy와 mse를 합친 것으로 하였습니다.



### 설정

- 기본으로 주어지는 kor_char_parser 로부터 출력되는 인덱스에 +1을 하였습니다.
- 1\~4점은 부정, 5\~7점은 중립, 8\~10점은 긍정으로 설정하였습니다.
- GRU의 히든 사이즈를 512로 설정했습니다.
- strmaxlen을 150으로 설정했습니다.
- 배치 사이즈를 512로 설정했습니다.
- gradient를 ±1로 clip하였습니다.
- 어떠한 전처리도 수행하지 않았으며, 어떠한 regularization 기법도 사용하지 않았습니다.



### 결과

2.8082 MSE (8위)

