# 📊 MobileBERT를 활용한 FIFA 게임 리뷰 긍부정 분석 프로젝트

![Python](https://img.shields.io/badge/python-%233776AB.svg?style=for-the-badge&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/pytorch-%23EE4C2C.svg?style=for-the-badge&logo=pytorch&logoColor=white)
![Pycharm](https://img.shields.io/badge/pycharm-%23000000.svg?style=for-the-badge&logo=pycharm&logoColor=white)

---

## 📌 1. 개요

**🔍 작성 방향: 왜 이 문제를 해결하고자 했는가? 이 문제를 해결하는 것이 어떤 의미가 있는가?**

영화나 게임 리뷰는 대중의 반응을 확인하고 향후 콘텐츠 개선에 중요한 지표로 활용됩니다. 본 프로젝트에서는 FIFA 시리즈 게임의 리뷰 데이터를 기반으로 긍/부정을 분류하는 감정 분석 모델을 MobileBERT를 활용해 구현했습니다.

이러한 분석은 특정 시리즈에 대한 사용자 만족도를 예측하거나 마케팅 전략 수립에도 도움을 줄 수 있습니다.

> 참고 문헌:  
> [[1] KCI 논문](https://www.kci.go.kr/kciportal/ci/sereArticleSearch/ciSereArtView.kci?sereArticleSearchBean.artiId=ART001954434)  
> [[2] 통계자료](https://the-numbers.com/movies/franchises/sort/World)

---

## 📂 2. 데이터

### 📑 2-1. 수집 및 전처리 방식
- 리뷰 데이터 출처: 아마존 상품평 데이터 (가정)
- 전처리 과정:
  - 텍스트 정제 및 소문자화
  - 토큰화 및 패딩 (max length = 256)
  - 라벨 필터링 (긍정: 1 / 부정: 0)

| 단계 | 설명 |
|------|------|
| 토큰화 | MobileBERT tokenizer 사용 |
| 라벨링 | 0: 부정, 1: 긍정 |
| 샘플 수 | 총 70,000개 중 10,000개 학습에 사용 |

※ 자세한 표는 [데이터 요약표 보기](https://github.com/yourname/project-name/blob/main/assets/data_summary_table.png)

---

## 🧠 3. 모델 학습

- 모델: `MobileBERTForSequenceClassification` (`transformers`)
- 학습 방식: 10,000개 샘플 → 80% 학습 / 20% 검증
- Optimizer: AdamW (`lr=2e-5`)
- Epochs: 4

### 📉 학습 결과 시각화

![Training Accuracy Plot](https://github.com/yourname/project-name/blob/main/assets/training_accuracy_plot.png)

---

## ✅ 4. 성능 평가

| 데이터셋 | 정확도 |
|----------|--------|
| Train | 약 95% |
| Validation | 약 93% |
| Full Test Set (70,000) | 약 92% |

---

## 📌 5. 결론 및 향후 계획

- FIFA 리뷰 감정 분석을 통해 대규모 사용자 피드백을 정량화할 수 있었음
- MobileBERT 기반 모델이 빠르고 효과적임을 확인
- 추후 Transformer 기반 다른 모델들과 비교 실험 예정 (e.g., DistilBERT, KoBERT 등)

---

## 📎 부록

- [전체 코드 보기](https://github.com/yourname/project-name/blob/main/model_training.py)
- [모델 파일 다운로드](https://github.com/yourname/project-name/releases/tag/v1.0)
