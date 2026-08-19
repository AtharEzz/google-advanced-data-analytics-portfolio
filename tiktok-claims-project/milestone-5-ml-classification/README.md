# TikTok Claims Classification - Milestone 5: ML Classification (Random Forest & XGBoost)

Part of the TikTok Claims Classification Project | Google Advanced Data Analytics Certificate - Course 5: The Nuts and Bolts of Machine Learning

## Business Problem

TikTok receives a high volume of user-reported videos requiring manual moderation review. Manually checking every video is slow, costly, and inefficient. Videos making claims require faster moderation than opinions to prevent the spread of misinformation.

**Goal:** Build a model to automatically classify videos as claims or opinions, enabling TikTok to triage incoming reports and prioritize claim videos for faster human review.

## Model Results

| Model | Set | Precision | Recall | F1 | Accuracy |
|---|---|---|---|---|---|
| Random Forest (CV best) | Train (CV) | 0.999 | 0.995 | not scored | not scored |
| Random Forest | Validation | 1.00 | 1.00 | 1.00 | 1.00 |
| XGBoost | Validation | 0.99 | 0.99 | 0.99 | 0.99 |
| **Random Forest (champion)** | **Test holdout** | **1.00** | **1.00** | **1.00** | **1.00** |

*CV scoring only included precision and recall (not F1 or accuracy) — full metrics computed on validation and test sets.*

**Champion model: Random Forest** — near-perfect performance on both validation and test sets, with only 6 misclassified samples out of 3,817 test records.

**Test holdout classification report:**
- Opinion: Precision 1.00, Recall 1.00, F1 1.00 (1,928 samples)
- Claim: Precision 1.00, Recall 1.00, F1 1.00 (1,889 samples)
- Overall accuracy: **1.00** across 3,817 test samples

**Confusion matrix (from test holdout plot):**
- TN: 1,925 | FP: 3 | FN: 3 | TP: 1,886

## Why Recall Was Prioritized

Recall was the primary optimization metric because a false negative (missing a claim video) is the more costly error in content moderation:
- A missed claim video continues circulating without review, potentially spreading misinformation
- A false positive (flagging an opinion as a claim) only adds one unnecessary review to the queue

## Feature Engineering

**NLP feature extraction from transcription text:**
- CountVectorizer with bigrams and trigrams (ngram_range=(2,3)), max_features=15, stop_words='english'
- Extracted 15 text n-gram features from video_transcription_text
- CountVectorizer fitted on training data only, then transformed validation and test sets (no leakage)
- Engineered description_length (character count of transcription text)

**Encoded features:**
- verified_status (one-hot)
- author_ban_status (one-hot)

**Dropped:** video_id, raw transcription text (replaced by n-gram features and description_length)

## Modeling Pipeline

1. Dropped 298 rows with missing values
2. No outlier capping (no outliers in video_duration_sec; engagement metric outliers retained)
3. Class balance confirmed: 50.35% claims vs. 49.65% opinions - no resampling needed
4. Three-way split: 60% train / 20% validation / 20% test (stratified, random_state=0)
5. CountVectorizer fitted on training set, transformed validation and test sets
6. GridSearchCV with 5-fold CV for both models, optimizing for recall
7. Final evaluation on held-out test set using champion model only

## Best Hyperparameters

**Random Forest (champion):**
- max_depth=None, max_features=0.6, max_samples=0.8
- min_samples_leaf=1, min_samples_split=2, n_estimators=300

**XGBoost:**
- learning_rate=0.1, max_depth=2, min_child_weight=5, n_estimators=300

## Feature Importances (Champion RF Model)

- **video_view_count: ~60%** - by far the strongest predictor
- **video_like_count: ~25%** - second strongest
- video_share_count, video_download_count, video_comment_count: smaller contributions
- Text n-gram features and description_length: minor contributions

**Why view count dominates:** From earlier EDA (Milestone 1), claim videos average 501,029 views vs. opinion videos at 4,956 views - a 100x difference. The model learned this pattern, which explains both its near-perfect accuracy and why view count has ~60% feature importance.

## Key Insights

- The near-perfect accuracy is expected and explainable, not suspicious: the 100x view count gap between claims and opinions means this is a naturally separable problem once the right features are included
- Both Random Forest and XGBoost performed near-perfectly; RF was selected as champion for higher recall on validation data
- False positives (opinions flagged as claims) are the model's primary error type - acceptable given that false negatives (missed claims) would be more harmful

## Business Recommendations

- **Deploy to production:** Integrate the RF model into TikTok's moderation pipeline to automatically triage incoming reports - near-perfect accuracy justifies automated pre-screening
- **Monitor performance:** Track prediction accuracy on live data continuously - model performance may degrade as content patterns evolve
- **Feature expansion:** Add NLP-based features (sentiment analysis, text embeddings from transcriptions) to improve edge-case performance on ambiguous videos

## Deliverables

- Activity_Course_6_TikTok_project_lab.ipynb - RF and XGBoost classification notebook
- TikTok-Course-5-executive-summary.pdf - Stakeholder executive summary

## Tools

Python, Pandas, NumPy, Scikit-learn (RandomForestClassifier, GridSearchCV, CountVectorizer, confusion_matrix, classification_report, train_test_split), XGBoost (XGBClassifier), Matplotlib, Seaborn
