# 🐾 Pet Eye & Skin Disease Models

AI 기반 반려동물 **안구(Eye)** 및 **피부(Skin)** 질환 자동 진단 모델 개발 프로젝트입니다.  
모델은 **Jupyter Notebook** 환경에서 학습되었으며, PetCare 안드로이드 앱의 핵심 기능인  
**눈 건강 검사(Eye Health Test)** 및 **피부 건강 검사(Skin Health Test)** 기능에 활용됩니다.

모든 모델은 **AWS EC2 서버**에 배포되어 실제 서비스에서 inference 기능을 제공합니다.

---

## ✨ 프로젝트 개요

### 👁️ 안구 질환 (4-Class)
1. 결막염 (Conjunctivitis)  
2. 백내장 (Cataracts)  
3. 안검종양 (Tumors)  
4. 무증상 (Asymptomatic)

### 🐶 피부 질환 (2 그룹, 각 3-Class)

#### **A. Protruding_P 그룹**
- 구진·플라그 (Papule/Plaque)  
- 태선화·과다색소침착 (Lichenification/Hyperpigmentation)  
- 결절·종괴 (Nodule/Mass)

#### **B. Inflammatory_I 그룹**
- 농포·여드름 (Pustule/Acne)  
- 미란·궤양 (Erosion/Ulcer)  
- 결절·종괴 (Nodule/Mass)

> 피부 질환은 질환 특성이 달라 **P 그룹**, **I 그룹** 두 개로 구분하여 별도 모델로 학습합니다.

---

## 🛠️ 모델 및 학습 전략

![Model](https://github.com/user-attachments/assets/d10db915-d7b3-4a3f-90fb-9d9b8b71b4a5)

### 1. MobileNetV2 전이 학습 기반 모델
- ImageNet 사전 학습 모델 사용  
- 분류층(Fully Connected Layer)만 재학습  
- 경량·고속 구조로 모바일 서비스에 적합  
- 적은 데이터에서도 높은 성능 보유

---

## 🧹 데이터 전처리

### 안구 질환
- 이미지 정규화 및 크기 통일
- 다양한 촬영 환경 대응용 전처리

### 피부 질환
- 한글 파일명 인코딩 문제(CP437/EUC-KR) 처리  
- 병변 중심 이미지 전처리  
- 클래스 불균형 대응(샘플 균형 조정)

---

## 🔄 데이터 증강 (Augmentation)

- 회전(Rotation)  
- 이동(Shift)  
- 확대/축소(Zoom)  
- 좌우반전(Horizontal Flip)  

→ 데이터 다양성 증가  
→ 과적합 방지  
→ 일반화 성능 향상

---

## 📊 성능 평가

---

# 👁️ 1. 안구 질환 모델 성능

### 🔸 학습 결과
- Epoch: 10  
- Validation Accuracy: **84.56%**  
- Training Loss: 0.4354  
- Validation Loss: 0.4752  

### Confusion Matrix
<img width="650" height="544" alt="download" src="https://github.com/user-attachments/assets/c5c83619-34fe-4b1d-bd5f-8362b3fe3024" />


### 🔸 클래스별 성능

| Class | Precision | Recall | F1-score | Data Count |
|-------|-----------|---------|-----------|-------------|
| 결막염 | 0.89 | 0.77 | 0.83 | 239 |
| 백내장 | 0.80 | 0.71 | 0.76 | 168 |
| 안검종양 | 0.90 | 0.90 | 0.90 | 114 |
| 무증상 | 0.77 | 1.00 | 0.87 | 172 |
| **Accuracy** | | | **0.84** | **693** |

### 🔸 최종 테스트
- Test images: 13  
- Test accuracy: **84.62% (11/13)**  
- 실서비스 환경에서도 안정적 성능 확인

---

# 🐶 2. 피부 질환 모델 성능

---

## 🔥 A. Protruding_P (P 그룹)

### ✔ 클래스 구성
- 구진·플라그  
- 태선화·과다색소침착  
- 결절·종괴  

### ✔ 핵심 결과
- Epoch: 7  
- Best Validation Accuracy: **61.43%**

### Confusion Matrix
<img width="650" height="1180" alt="download" src="https://github.com/user-attachments/assets/39ea008f-a755-40e2-925a-7d43b7f86e9d" />


### ✔ 클래스별 성능

| Class | Precision | Recall | F1 | Data Count |
|-------|-----------|--------|-----|------------|
| 구진·플라그 | 0.73 | 0.69 | 0.71 | 450 |
| 태선화·색소침착 | 0.98 | 0.63 | 0.65 | 450 |
| 결절·종괴 | 0.67 | 0.77 | 0.72 | 397 |
| **Accuracy** ||| ||**0.69**   |   **1297** |

---

## 🔥 B. Inflammatory_I (I 그룹)

### ✔ 클래스 구성
- 농포·여드름  
- 미란·궤양  
- 결절·종괴  

### ✔ 핵심 결과
- Epoch: 6  
- Best Validation Accuracy: **65.08%**

### Confusion Matrix
<img width="650" height="1179" alt="download" src="https://github.com/user-attachments/assets/49f7e07d-8018-4203-bf26-d4a035cea78c" />


### ✔ 클래스별 성능

| Class | Precision | Recall | F1 | Data Count |
|-------|-----------|--------|-----|------------|
| 농포·여드름 | 0.72 | 0.66 | 0.69 | 296 |
| 미란·궤양 | 0.51 | 0.67 | 0.58 | 150 |
| 결절·종괴 | 0.74 | 0.69 | 0.72 | 265 |
| **Accuracy** | | | **0.67** | **711** |

---

# 🧪 결론

- **안구 모델:** 실서비스 활용 가능한 수준의 안정성과 정확도 확보  
- **피부 모델:** 데이터 편차·난이도 대비 양호한 성능 기록  
- **모든 모델:** AWS EC2 환경에서 평균 1~2초 내 응답 가능  

---

# 🔗 개발자 정보
- GitHub Repository: https://github.com/dohb128

---

# ⚡ 주요 포인트
- PetCare 앱의 **AI 진단 백엔드 핵심 모델**  
- 눈 + 피부 질환을 모두 자동 분류  
- MobileNetV2 기반 경량 모델 → 모바일 친화적  
- AWS 서버에 탑재되어 실시간 inference 수행  

