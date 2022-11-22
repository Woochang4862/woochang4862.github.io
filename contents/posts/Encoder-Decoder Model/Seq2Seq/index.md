---
title: "Seq2Seq"
description: "Let's learn about Sequence-to-Sequence Model."
date: 2022-07-10
update: 2022-07-10
tags:
  - Encoder-Decoder_Model
  - Sequencial_Data
series: "Encoder-Decoder_Model"
---

## Seq2Seq

[Sequence to Sequence Learning with Neural Networks (NIPS 2014)](https://proceedings.neurips.cc/paper/2014/file/a14ac55a4f27472c5d894ec1c3c743d2-Paper.pdf)

[https://proceedings.neurips.cc/paper/2014/file/a14ac55a4f27472c5d894ec1c3c743d2-Paper.pdf](https://proceedings.neurips.cc/paper/2014/file/a14ac55a4f27472c5d894ec1c3c743d2-Paper.pdf)

RNN(1986)에서 파생된 LSTM(1997)을 활용한 Seq2Seq을 통해 기계 번역 테스크를 효율적으로 해결하고 있다. 

[Transformer (2017)](https://www.notion.so/Transformer-Attention-Is-All-You-Need-adfe62ce5ce24e22977f175afe0d1336)이 나오기 전까지 state-of-the-art(첨단기술) 로 사용되었다.

고정된 크기의 Context Vector 를 사용한다는 점에서 한계가 있다.

이런 한계점을 보완한 [Attention(ICLR 2015)](https://www.notion.so/Attention-7cfa9b129e18413cac9015e24b36a60a) 기법이 적용되었다.

이를 이용해서 Attention 기법을 적극 활용한 Transformer 가 나왔고 여기에서 GPT, BERT 등이 나왔다. 이제는 입력 시퀀스 전체에서 문맥 추출!

자연어 처리를 위한 기초 수학

언어모델

문장(Sequence)에 확률을 부여하는 모델

예를 들어, 기계번역에 경우, 

$$P(\text{{난 널 싫어해}}|\text{I love you}) > P(\text{{난 널 싫어해}}|\text{I love you})$$ 

또 단어 예측에 경우, 

$$P(\text{먹었다}|\text{나는 밥을}) > P(\text{싸웠다}|\text{나는 밥을})$$ 와 같이 표현할 수 있다.

$$P(W) = P(w_1,w_2,w_3,w_4,w_5,...,w_n)$$ 하나의 문장은 이와 같이 여러개의 단어로, 즉 Joint Probability 로 표한 가능하다.

Joint Probability Distribution(결합확률분포) : 확률변수가 여러개일때 이들을 함께 고려하는 확률 분포

이는 베이즈정리(조건부확률을 구하는 공식)와 연쇄법칙에 의해서 다음과 같이 정의된다.

$$P(w_1,w_2,w_3,...,w_n)\\=P(w_1)*P(w_2|w_1)*P(w_3|w_1,w_2),...,P(2_n|w_1,w_2,...,w_{n-1})\\=\displaystyle \prod_{i=1}^{n} P(w_{i}|w_1,...,w_{i-1})$$

RNN 기반 Seq2Seq 에서 Encoder 는 고정되 크기의 문맥벡터를 추출라고 디코더는 문맥벡터로부터 번역결과를 생성한다.