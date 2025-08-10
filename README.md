# 🚀 Hybrid Learning-to-Rank Architecture for Offer Personalization  
### **American Express Campus Challenge 2025**  
#### Submission by **Team Spacebar Sketchers**  

---

## 📌 Overview  
This repository contains the complete solution for the **American Express Campus Challenge 2025**.  
Our project introduces a **state-of-the-art Hybrid Learning-to-Rank (LTR) system** designed to deliver **highly personalized commercial offers** and significantly enhance customer engagement.  

At its core, the system is an **innovative ensemble** pairing a **LightGBM ranker** with a **Transformer network** for **advanced residual correction**, validated through a **rigorous, production-ready pipeline**.  

---

## 🎯 Project Goals  
- **Predict** which commercial offers a customer is most likely to engage with.  
- **Optimize** the entire ranked list instead of just binary classification.  
- **Deliver** a scalable, end-to-end pipeline ready for business integration.  

---

## 🛠 End-to-End Pipeline  
1. **Ingest** raw customer and offer data.  
2. **Engineer** a rich set of features to capture complex behaviors.  
3. **Train** a novel hybrid ranking model.  
4. **Validate** with a time-sensitive, leak-proof strategy.  
5. **Output** a calibrated, ranked list of offers ready for deployment.  

**✅ Core Achievement:**  
A **high-precision ranking system** that consistently outperforms traditional models, delivering **actionable intelligence** for offer personalization.

---

## ⚙️ Technical Architecture  

### **1. Primary Model: LightGBM with LambdaRank**  
- **Gradient-Boosted Decision Tree (GBDT)** model using `lambdarank` objective.  
- Directly optimizes **MAP@7** ranking metric.  
- Excels at **tabular feature learning** from our extensive engineered dataset.  

### **2. Residual Correction: Transformer Network**  
- **Step 1:** LightGBM generates initial ranking scores.  
- **Step 2:** Residuals (errors) are fed into a **Transformer**.  
- **Step 3:** The Transformer captures complex sequential patterns missed by GBDT.  
- **Step 4:** Final prediction is a **weighted ensemble** of both outputs.  

**💡 Why Hybrid?**  
Combines **GBDT's tabular strength** with **Transformers’ sequential pattern recognition** → resulting in **more accurate, nuanced rankings**.

---

## 🏗 Feature Engineering  

| Category              | Description |
|-----------------------|-------------|
| **Vectorized Features** | Cyclical time encodings (day-of-week, hour), basic text vectorization from offer descriptions. |
| **Static Offer Profiles** | Intrinsic attributes like duration, brand, industry category, delivery channel. |
| **Dynamic Customer Profiles** | Time-aware aggregated metrics: CTR, session frequency, brand affinity over multiple time windows. |

---

## 🔍 Validation Strategy  

**1. Time-Based Split**  
- 85% training, 15% recent data as final test (simulates real-world).  

**2. Stratified Group K-Fold**  
- **Grouping:** All interactions from a single customer stay in one fold → prevents leakage.  
- **Stratification:** Maintains click-through rate balance for **stable MAP@7 scores**.  

---

## 📏 Performance Metric  
- **Mean Average Precision @ 7 (MAP@7)**  
- Rewards ranking relevant offers higher in the top 7.  
- Directly aligns with **maximizing engagement on visible offers**.  

---

## 🚀 Future Enhancements  
1. **Two-Stage Re-ranking**  
   - First: Fast candidate selection (~50 offers).  
   - Second: Complex ensemble for high-precision re-ranking.  

2. **Model Diversity**  
   - Add **CatBoost**, **TabNet**, or other models into ensemble.  

3. **Advanced Feature Engineering**  
   - **Semantic Embeddings** (Sentence-BERT for offer descriptions).  
   - **Graph-Based Features** (Node2Vec on customer-offer-brand networks).  

---

## 👥 Team  
**Team Spacebar Sketchers** – pushing the limits of personalization through **hybrid AI architectures**.  

---
