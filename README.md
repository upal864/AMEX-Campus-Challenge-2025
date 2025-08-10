Hybrid Learning-to-Rank Architecture for Offer Personalization
AMEX Campus Challenge 2025 Submission by Team Spacebar Sketchers
This repository contains the complete solution for the American Express Campus Challenge 2025. Our project introduces a state-of-the-art, hybrid learning-to-rank (LTR) system designed to significantly enhance customer engagement by delivering highly personalized commercial offers. The core of our solution is an innovative ensemble model that pairs a powerful LightGBM ranker with a Transformer network for advanced residual correction, all validated through a rigorous, production-ready pipeline.

1. Project Overview
The challenge was to develop a model that could accurately predict which commercial offers a customer is most likely to engage with. Our goal was to move beyond simple classification and build a system that optimizes the entire ranked list of offers presented to a user.

Our final solution is an end-to-end pipeline that:

Ingests raw customer and offer data.

Engineers a rich set of features to capture complex behaviors.

Trains a novel hybrid ranking model.

Validates performance using a time-sensitive, leak-proof strategy.

Outputs a calibrated, ranked list of offers ready for business integration.

Core Achievement: We successfully developed a high-precision ranking system that demonstrably improves upon traditional models, culminating in a robust pipeline that provides actionable intelligence for offer personalization.

2. Technical Architecture
Our solution's primary innovation lies in its hybrid model architecture, which addresses the limitations of standalone models.

Primary Model: LightGBM with LambdaRank
The foundation of our system is a Gradient-Boosted Decision Tree (GBDT) model, specifically LightGBM, configured with a lambdarank objective. This LTR approach directly optimizes for ranking metrics like MAP@7, making it far more effective than binary classification for this problem. It excels at learning from the vast set of tabular features we engineered.

Residual Correction: Transformer Network
While LightGBM is powerful, it can miss complex, sequential patterns in a user's interaction history. To address this, we introduced a Transformer Network.

The LightGBM model first generates an initial ranking score for all offers.

The residuals (the errors between the LGBM scores and the true labels) are then fed into a Transformer network.

The Transformer, with its self-attention mechanism, learns the complex, non-linear patterns in the ranking errors that the GBDT model missed.

The final prediction is a weighted ensemble of the initial LightGBM score and the Transformer's corrective output, resulting in a more accurate and nuanced final ranking.

This hybrid approach allows us to combine the speed and power of GBDTs on tabular data with the sequential pattern recognition capabilities of deep learning.

3. Feature Engineering
A robust feature set was critical to our success. We developed three categories of features:

Vectorized Features: Fast, efficient features derived from raw data, including cyclical time-based encodings (e.g., day of the week, hour of the day) and basic text vectorization from offer descriptions.

Static Offer Profiles: Intrinsic, unchanging attributes for each offer, such as its duration, the associated brand, industry category, and the channel through which it's delivered.

Dynamic Customer Profiles: Time-aware, aggregated features that create a rich profile of each customer's historical behavior. This includes metrics like click-through rates, session frequency, and brand affinity over various time windows.

4. Validation Strategy
To ensure our model's performance is reliable and generalizes to unseen data, we designed a stringent, multi-step validation framework.

Time-Based Split: We first performed a global 85/15 split on the data based on time. The most recent 15% of interactions were held out as a final, "real-world" test set to simulate predicting on new customers.

Stratified Group K-Fold: On the remaining 85% training data, we used Stratified Group K-Fold cross-validation.

Grouping: All interactions from a single customer (id2) were kept within the same fold. This is crucial to prevent data leakage, where the model learns from a customer's future behavior.

Stratification: We stratified the folds based on the click-through rate (y=1). This ensures that the class balance is consistent across all folds, leading to stable and reliable MAP@7 scores during training.

5. Performance Metric
The primary evaluation metric for this challenge was Mean Average Precision @ 7 (MAP@7). This metric measures the quality of the ranked list of the top 7 recommended offers. It rewards models that place relevant items higher up in the list, which directly aligns with the business goal of maximizing customer engagement with the most prominent offers.

6. Future Enhancements
While our model achieved strong performance, we identified several avenues for future improvement:

Two-Stage Re-ranking: Implement a cascaded architecture where a fast, lightweight model first selects a larger pool of ~50 candidate offers, and our complex, resource-intensive ensemble then re-ranks this smaller set for maximum precision.

Model Diversity: Incorporate different model types like CatBoost or TabNet into the final ensemble to leverage their unique approaches to handling data, potentially improving robustness.

Advanced Feature Engineering:

Semantic Embeddings: Use language models like Sentence-BERT on offer descriptions to capture deeper semantic meaning.

Graph-Based Features: Model the customer-offer-brand ecosystem as a graph and use algorithms like Node2Vec to generate features that capture multi-step relationships.
