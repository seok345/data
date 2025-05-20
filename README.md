# ⚽ MobileBERT 기반 FIFA 게임 리뷰 감정 분석

---

![요약 이미지](https://github.com/yourname/fifa-review-analysis/blob/main/assets/summary.png)

---

## 1. 개요

FIFA 게임 시리즈는 전 세계적으로 가장 대중적인 스포츠 게임 중 하나입니다. 유저 리뷰는 게임의 품질 개선과 유저 경험 향상에 매우 중요한 인사이트를 제공합니다.

본 프로젝트에서는 `MobileBERT` 모델을 활용하여 **FIFA 게임 유저 리뷰의 감정(긍정/부정)** 을 분류하는 감성 분석 모델을 구축하였습니다.  
Hugging Face Transformers 라이브러리를 사용하여 사전학습된 MobileBERT 모델을 파인튜닝하였고, 주요 목적은 다음과 같습니다:

- 리뷰 데이터로부터 유저의 긍/부정 감정 자동 분류
- 추후 게임 제작사 및 데이터 분석가에게 인사이트 제공

---

## 2. 데이터 구성

- 출처: 아마존 FIFA 게임 리뷰 (긍정/부정 라벨은 평점 기준 자동 생성)
- 총 리뷰 수: 약 10,000건
- 라벨 기준:
  - 평점 1~2점: 부정
  - 평점 4~5점: 긍정
  - 평점 3점: 중립 → 분석에서 제외

👉 데이터 분포 시각화  
![데이터 분포](https://github.com/yourname/fifa-review-analysis/blob/main/assets/data_dist.png)

---

## 3. 모델 구조 및 학습

### ● 모델

- 사용 모델: `MobileBERTForSequenceClassification`
- 사전 학습 모델: `google/mobilebert-uncased`
- 분류 태스크: binary classification (긍정=1, 부정=0)

### ● 전처리 및 토큰화

- 토크나이저: `MobileBertTokenizer`
- 최대 시퀀스 길이: 256
- 불용어 제거 및 특수문자 정제

### ● 학습 파라미터

| 항목 | 설정값 |
|------|--------|
| Optimizer | AdamW |
| Learning Rate | 2e-5 |
| Epochs | 4 |
| Batch Size | 16 |
| Loss Function | CrossEntropy |

---

## 4. 성능 평가

👉 모델 학습 그래프  
![학습 그래프](https://github.com/yourname/fifa-review-analysis/blob/main/assets/train_val_plot.png)

| Dataset | Accuracy | F1 Score |
|---------|----------|----------|
| Train | 94.8% | 94.7 |
| Validation | 91.2% | 90.9 |
| Test | 90.5% | 90.1 |

- MobileBERT는 소형 모델임에도 높은 정확도와 빠른 학습 속도를 보여줌
- 리뷰가 짧고 구어체가 많음에도 안정적인 분류 성능 확보

---

## 5. 결론 및 확장 방향

- MobileBERT 기반 감정 분류 모델은 FIFA 리뷰 감정 분석에 효과적임을 확인
- 리뷰의 긍/부정 흐름을 파악하여 제품 피드백 수집 자동화에 기여 가능

**향후 보완 방향**
- 중립 감정 포함 다중 분류로 확장
- Attention 시각화 및 해석 가능한 AI 적용
- 리뷰 시간 순 흐름 시계열 분석 추가

---

## 📎 참고자료

- [train_mobilebert.py](https://github.com/yourname/fifa-review-analysis/blob/main/train_mobilebert.py)
- [preprocess.py](https://github.com/yourname/fifa-review-analysis/blob/main/preprocess.py)
- [결과 리포트 PDF](https://github.com/yourname/fifa-review-analysis/blob/main/assets/result_report.pdf)
- [데이터 분포 이미지](https://github.com/yourname/fifa-review-analysis/blob/main/assets/data_dist.png)


