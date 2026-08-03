# TikTok Claims Classification - Milestone 4: Regression Analysis (Logistic Regression)

Part of the TikTok Claims Classification Project | Google Advanced Data Analytics Certificate - Course 4: Regression Analysis

## Business Problem

TikTok's data team is building a model to automatically classify video submissions as claims or opinions. As a stepping stone toward that classification model, this milestone builds a logistic regression model to predict whether a video's creator is verified or not verified, using video engagement metrics and behavioral features.

This matters because previous analysis showed verified_status is strongly correlated with content type - verified accounts post more opinions, unverified accounts post more claims. Predicting verification status helps streamline the claims classification workflow.

## Model Results

| Metric | Verified | Not Verified | Overall |
|---|---|---|---|
| Precision | 74% | 59% | |
| Recall | 38% | 87% | |
| F1-Score | 0.51 | 0.70 | |
| Accuracy | | | 63% |

**Test set size:** 7,154 records (balanced)

## Key Challenge: Class Imbalance

The raw dataset was heavily imbalanced: 93.7% not verified vs. 6.3% verified. Training on this imbalanced data would produce a model biased toward predicting "not verified" for everything.

**Solution:** Upsampled the minority class (verified) to achieve a 50/50 balanced training set before splitting into train/test sets.

## Feature Selection

Started with all engagement metrics but identified severe multicollinearity (correlations of 0.75-0.86 among view count, like count, share count, download count, comment count). Kept only video_like_count as the representative engagement feature to avoid violating the logistic regression assumption of no severe multicollinearity.

**Final features used:**
- video_duration_sec
- video_like_count
- text_length (engineered: length of video transcription text)
- claim_status (one-hot encoded: opinion vs claim)
- author_ban_status (one-hot encoded: banned, under review, active)

## Modeling Pipeline

1. Dropped 298 rows with missing values
2. Capped outliers in video_like_count and video_comment_count (Q3 + 1.5*IQR)
3. Engineered text_length feature from video_transcription_text
4. Upsampled minority class (verified) to balance training data
5. OneHotEncoder fitted on training set, applied to test set (no leakage)
6. LogisticRegression (max_iter=1000, random_state=0)

## Key Insights

- The model catches 87% of unverified accounts (high recall) but only 38% of verified accounts - it is biased toward predicting "not verified"
- This bias makes sense given that even after upsampling, verified account behavior patterns are harder to distinguish from unverified ones based on engagement metrics alone
- Accounts posting opinion content are significantly more likely to be verified - confirmed by the claim_status feature being meaningful
- **Next steps:** Try non-linear algorithms (Random Forest, XGBoost) and engineer composite engagement ratios; adjust decision threshold to better balance recall for the verified class

## Deliverables

- Activity_Course_5_TikTok_project_lab.ipynb - Logistic regression notebook
- TikTok_Course_4_executive_summary.pdf - Stakeholder executive summary with confusion matrix

## Tools

Python, Pandas, NumPy, Scikit-learn (LogisticRegression, OneHotEncoder, train_test_split, confusion_matrix, classification_report), Matplotlib, Seaborn
