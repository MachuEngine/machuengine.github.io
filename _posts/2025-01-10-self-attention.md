---
layout: single
title: "[AI][Transformer] Self-Attention"
categories:
  - transformer
tags:
  - Self-Attention Mechanism
  - transformer
description: "Self-Attention Mechanism"
author: "안종민"
date: "2025-01-10"
---
# **🔍 Self-Attention Mechanism**  

- **Self-Attention Mechanism**은 **트랜스포머(Transformer) 모델의 핵심 요소**.       
- **문장 내 단어들 간의 의존 관계를 거리와 상관없이 학습할 수 있도록 도움**.    
- 전통적인 RNN은 단어를 순차적으로 처리하지만, **Self-Attention은 병렬 처리를 가능하게 하여 연산 효율성을 크게 향상**.   

---

## **1️⃣ Self-Attention이란?**
Self-Attention은 **각 단어가 문장 내 다른 단어들과 얼마나 연관이 있는지를 계산하는 메커니즘**.

<img src="/assets/images/self-Attention1.png" alt="Self-Attention">


💡 **예제 문장:**  
*"그 동물은 너무 피곤해서 길을 건너지 않았다."*  
➡ 여기서 *"그"*는 *"동물"*을 가리키는지? 아니면 *"길"*을 의미하는지?  
➡ **Self-Attention은 이러한 관계를 올바르게 학습할 수 있도록 도움!**  

---

## **2️⃣ Scaled Dot-Product Attention**
두 단어의 유사도를 측정한다. 트랜스포머에서는 두 단어 벡터의 내적을 통해 유사도를 측정한다.   

트랜스포머의 **Self-Attention Mechanism**은 **Scaled Dot-Product Attention**을 기반으로 동작.

$$
\text{Attention}(Q, K, V) = \text{softmax} \left(\frac{QK^T}{\sqrt{d_k}}\right) V
$$

여기서:

| 기호 | 의미 |
|--------|---------|
| **\(Q\) (Query)** | 현재 단어의 표현 벡터 |
| **\(K\) (Key)** | 문장에서 모든 단어의 표현 벡터 |
| **\(V\) (Value)** | 모든 단어의 정보가 담긴 벡터 |
| **\(d_k\)** | Key 벡터의 차원 수 |
| **Softmax** | 어텐션 점수를 확률 분포로 변환 |

---

## **3️⃣ Self-Attention 동작 과정**
### **🔹 Step 1: Query, Key, Value 벡터 계산**
입력된 문장의 각 단어(토큰)는 **세 개의 벡터로 변환됨**:  
**Query (\(Q\)), Key (\(K\)), Value (\(V\))**

$$
Q = XW_q, \quad K = XW_k, \quad V = XW_v
$$

여기서 \( W_q, W_k, W_v \)는 **학습 가능한 가중치 행렬**.

---

### **🔹 Step 2: 어텐션 점수(유사도) 계산**
- **Query 벡터(\(Q\))**와 **Key 벡터(\(K\))** 간의 유사도를 점곱(dot product) 연산으로 계산:

<img src="/assets/images/self-attention2.png" alt="Self-Attention">

---

$$
\frac{QK^T}{\sqrt{d_k}}
$$

- **\( \sqrt{d_k} \)로 나누는 이유:**  
  → 값이 너무 커지는 것을 방지하고, 학습 안정성을 높이기 위함.

---

### **🔹 Step 3: Softmax 적용**
- 어텐션 점수를 **Softmax 함수**에 통과시켜 확률 분포를 생성:

$$
\text{Softmax} \left( \frac{QK^T}{\sqrt{d_k}} \right)
$$

- 높은 값일수록 해당 단어가 더 중요한 의미를 가짐.

---

### **🔹 Step 4: Value 벡터와 가중합**
- Softmax에서 얻은 가중치를 **Value 벡터(\(V\))에 곱하여 최종 결과를 생성**:

$$
\text{Output} = \text{Softmax} \left(\frac{QK^T}{\sqrt{d_k}}\right) V
$$

- 이 과정을 통해 **각 단어가 다른 단어들과 얼마나 관련이 있는지 반영된 새로운 벡터가 생성됨**.

---

## **4️⃣ Self-Attention 실제 동작 예제**
### **예제 문장**
**"고양이가 매트 위에 앉아 있다."**  

| 단어 | Query (\(Q\)) | Key (\(K\)) | Value (\(V\)) |
|--------|-------------|-------------|-------------|
| **고양이** | \(Q_1\) | \(K_1\) | \(V_1\) |
| **앉다** | \(Q_2\) | \(K_2\) | \(V_2\) |
| **매트** | \(Q_3\) | \(K_3\) | \(V_3\) |
| **위에** | \(Q_4\) | \(K_4\) | \(V_4\) |

1. **각 단어의 Query와 모든 단어의 Key를 점곱(dot product)하여 유사도 계산**  
2. **Softmax로 정규화하여 어텐션 점수 계산**  
3. **어텐션 점수를 Value 벡터에 곱하여 최종 출력 벡터 생성**  

➡ **결과적으로, 문맥을 고려하여 "고양이"와 "앉다"가 더 강한 연관성을 가지도록 학습할 수 있음!**

---

## **5️⃣ Self-Attention이 중요한 이유**
✅ **문맥(Context)을 잘 이해할 수 있음** (기존 RNN보다 더 강력한 관계 학습 가능)  
✅ **병렬 연산이 가능** (기존 RNN은 순차적 처리이지만, Self-Attention은 병렬 처리 지원)  
✅ **긴 문장에서도 멀리 떨어진 단어 간 관계를 학습 가능**  
✅ **번역, 질의응답, 요약, 대화 모델 등 다양한 NLP 작업에서 필수적**   


