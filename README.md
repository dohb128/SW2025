# Pet Eye Disease Model🐾

이 프로젝트는 **Jupyter Notebook**으로, 반려동물의 눈 질병 이미지를 분류하는 **딥러닝 모델**을 개발하고 평가합니다.  
PETCARE 안드로이드 앱의 핵심 기능인 **눈 건강 검사(Eye Health Test)**에 사용되며, **AWS EC2 서버**에 배포되어 실제 서비스에 활용됩니다.

---

## ✨ 프로젝트 개요
모델은 다음 **4가지 클래스**의 반려동물 눈 상태를 분류합니다:

1. 결막염 (Conjunctivitis)  
2. 백내장 (Cataracts)  
3. 안검종양 (Tumors)  
4. 무증상 (Asymptomatic)  

**MobileNetV2 기반 전이 학습(Transfer Learning)**을 활용하여, 데이터가 적더라도 효율적이고 정확하게 예측할 수 있습니다.

---

## 🛠️ 모델 및 학습 전략

### 1. MobileNetV2 기반 전이 학습 모델
- **구조:** 사전 학습된 MobileNetV2를 기본 모델로 사용  
- 새 **완전 연결(Fully Connected) 분류층**을 추가  
- 새 분류층만 학습, 사전 학습된 특징은 그대로 유지  
- **장점:**  
  - 경량화되어 모바일 환경에 적합  
  - 적은 데이터로도 효과적인 학습 가능  
  - 학습 시간 단축  

### 2. 데이터 전처리
- **한글 파일명 인코딩 문제**를 CP437, EUC-KR 방식으로 해결  
- 모델이 눈 특징에 집중하도록 배경 정보 학습 최소화  

### 3. 데이터 증강 (Data Augmentation)
**ImageDataGenerator**를 사용하여 다음과 같은 증강 적용:  
- 회전(Rotation)  
- 가로/세로 이동(Width/Height Shift)  
- 확대/축소(Zoom)  
- 좌우 반전(Horizontal Flip)  

> 데이터 다양성을 높여 과적합(overfitting)을 방지하고 일반화 성능을 향상

---

## 📊 성능 평가

### 1. 학습 결과
- **Epoch:** 10  
- **Validation Accuracy:** 84.56%  
- **Training Loss:** 0.4354  
- **Validation Loss:** 0.4752  

### 2. 클래스별 상세 성능
![Image](https://github.com/user-attachments/assets/6ec26042-ba0c-45a2-86e2-6cf9082712b8)


- **안검종양(Tumor)** 감지는 매우 신뢰할 수 있으며, 놓칠 가능성이 낮음  
- **백내장(Cataract)** 감지는 상대적으로 재현율이 낮아 일부 이미지가 다른 클래스와 혼동될 수 있음  

### 3. 최종 테스트 평가
- **테스트 이미지:** 13장  
- **테스트 정확도:** 84.62% (11/13 정확)  
- 실제 서비스 환경에서도 **안정적인 성능** 기대 가능

---

## 🔗 개발자 정보
- **GitHub Repository:** [https://github.com/dohb128](https://github.com/dohb128)

---

## ⚡ 주요 포인트
- PETCARE 앱의 **백엔드 진단 모델**로 활용  
- 모바일 배포 및 **실시간 사용**에 최적화  
- MobileNetV2 전이 학습으로 **효율적인 연산**과 높은 정확도 확보

---
