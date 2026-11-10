# Detecting and Prioritizing User Concerns in Mobile Apps

**MSc thesis · Computer Engineering (Algorithms & Computation)**  
**Sharif University of Technology · Defended 22 October 2025**  
**Author:** Shima Rezai · **Supervisor:** Dr. Abbas Heydarnoori

## Overview

How can software teams distinguish recurring, high-impact user concerns from millions of app reviews—and understand which issues deserve attention first?

This thesis investigates a data-driven approach that combines user feedback from **Google Play** with technical evidence from **GitHub issue trackers** and feedback about similar applications. It brings together natural language processing, semantic representation learning, clustering, automatic labelling, and machine-learning-based prioritisation to organise fragmented feedback into interpretable concerns across application releases.

## Data

The study used the DATAR collection, covering **1,363 mobile applications**, and selected **228 applications** with release histories suitable for analysing changes over time. The thesis reports collecting approximately **1.335 million Google Play reviews** for the selected applications.

For additional context, five similar applications were identified for each selected app using TF–IDF and cosine similarity, and up to 30 highly liked reviews were collected from each. GitHub issue data supplied complementary signals, including bugs, feature requests, issue status, and release-related activity.

## Method

1. **Prepare and extract phrases.** Reviews and app descriptions were cleaned and normalised using NLP techniques. The workflow extracted frequent, syntactically filtered bigrams to represent concise expressions of user concerns.
2. **Learn semantic representations.** A pretrained FastText model was adapted to the study text. The thesis reports comparing alternative embedding approaches and selecting FastText for the final workflow.
3. **Discover concern groups.** K-Means was applied to the phrase vectors; the thesis reports selecting 10 clusters using silhouette analysis.
4. **Make clusters interpretable.** Flan-T5-Large generated short, zero-shot labels from representative cluster keywords. Semantic-similarity and label-quality checks were used to identify unclear or unsuitable labels.
5. **Prioritise concerns over time.** User-feedback signals were combined with historical and technical indicators from GitHub. A central measure was the **Negativity Ratio (NR)**, which compares the share of negative reviews for a concern in a release with its historical pattern. The thesis supervisor proposed this measure; **I implemented it** and analysed it alongside previous-release indicators, bug and feature-request ratios, issue status, and developer responses.

## Evaluation and findings

The thesis compares classical machine-learning approaches—including Random Forest, CatBoost, XGBoost, SVM, and Logistic Regression—with MLP, LSTM, and a stacking approach. Evaluation uses classification metrics such as precision, recall, F1-score, accuracy, and AUC-ROC, alongside cluster-quality analysis and error analysis.

The thesis identifies **Random Forest and CatBoost among the strongest-performing models**, with a reported F1-score of **0.83** for each. It also reports stronger performance by the classical approaches than by the deep-learning models in this experimental setting.

## My contribution

My primary contributions were **research design, experimental evaluation, and analysis**. I designed and conducted the experiments, analysed and interpreted the findings, and implemented the NR-based prioritisation measure proposed by my supervisor. The thesis was successfully defended and formally approved at Sharif University of Technology.

## Scope and research opportunities

The study focuses on Android applications. Extending the approach to iOS, desktop software, and other application domains offers a direction for further evaluation. The thesis also identifies opportunities to strengthen analysis for concern clusters with relatively few reviews and to investigate model performance with larger and more balanced datasets.

## Repository note

This repository is a concise research record rather than a software release. It currently documents the approved study and its thesis-reported findings; the full implementation, source datasets, trained models, and complete experiment artefacts are not distributed here. The reported results have not been independently reproduced from the public repository.

## Citation

Rezai, Shima (2025). *Detecting and Prioritizing User Concerns in Mobile Apps*. MSc thesis, Department of Computer Engineering, Sharif University of Technology. Supervisor: Dr. Abbas Heydarnoori. Thesis in Persian; defended 22 October 2025.

For research enquiries, please use the contact details on my [GitHub profile](https://github.com/shimynimi).
