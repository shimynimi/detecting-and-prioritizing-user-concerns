# Detecting and Prioritizing User Concerns in Mobile Apps

**MSc thesis · Computer Engineering (Algorithms & Computation)**  
**Sharif University of Technology · Defended 22 October 2025**  
**Author:** Shima Rezai · **Supervisor:** Dr. Abbas Heydarnoori

## Overview

How can software teams distinguish recurring, high-impact user concerns from millions of app reviews—and understand which issues deserve attention first?

This thesis presents a data-driven approach that combines user feedback from **Google Play** with technical evidence from **GitHub issue trackers** and feedback about similar applications. It brings together natural language processing, semantic representation learning, clustering, automatic labelling, and machine-learning-based prioritisation to organise fragmented feedback into interpretable concerns across application releases.

## Data

The study used the DATAR collection, covering **1,363 mobile applications**, and selected **228 applications** with release histories suitable for analysing changes over time. Approximately **1.335 million Google Play reviews** were collected for the selected applications.

For additional context, five similar applications were identified for each selected app using TF–IDF and cosine similarity, and up to 30 highly liked reviews were collected from each. GitHub issue data supplied complementary signals, including bugs, feature requests, issue status, and release-related activity.

## Method

1. **Prepare and extract phrases.** Reviews and app descriptions were cleaned and normalised using NLP techniques. The workflow extracted frequent, syntactically filtered bigrams to represent concise expressions of user concerns.
2. **Learn semantic representations.** Alternative embedding approaches were compared, and a pretrained FastText model was adapted to the study text for the final workflow.
3. **Discover concern groups.** K-Means was applied to the phrase vectors, with silhouette analysis guiding the selection of 10 clusters.
4. **Make clusters interpretable.** Flan-T5-Large generated short, zero-shot labels from representative cluster keywords. Semantic-similarity and label-quality checks supported clear and consistent cluster labels.
5. **Prioritise concerns over time.** User-feedback signals were combined with historical and technical indicators from GitHub. A central measure was the **Negativity Ratio (NR)**, which compares the share of negative reviews for a concern in a release with its historical pattern. The thesis supervisor proposed this measure; **I implemented it** and analysed it alongside previous-release indicators, bug and feature-request ratios, issue status, and developer responses.

## Evaluation and findings

The thesis evaluates classical machine-learning approaches—including Decision Tree, Random Forest, CatBoost, XGBoost, SVM, and Logistic Regression—alongside MLP, LSTM, and a stacking approach. Evaluation uses precision, recall, F1-score, accuracy, and AUC-ROC, together with cluster-quality analysis and error analysis.

**Random Forest and CatBoost were among the strongest-performing models**, each achieving a reported F1-score of **0.83**. The results highlight the effectiveness of classical machine-learning approaches for this task and experimental setting.

## My contribution

My primary contributions were **research design, experimental evaluation, and analysis**. I designed and conducted the experiments, analysed and interpreted the findings, and implemented the NR-based prioritisation measure proposed by my supervisor. The thesis was successfully defended and formally approved at Sharif University of Technology.

## Research outlook

The framework provides a foundation for further research across iOS, desktop software, and other application domains, and for continued exploration of data-driven methods for understanding and prioritising user concerns.

## Citation

Rezai, Shima (2025). *Detecting and Prioritizing User Concerns in Mobile Apps*. MSc thesis, Department of Computer Engineering, Sharif University of Technology. Supervisor: Dr. Abbas Heydarnoori. Thesis in Persian; defended 22 October 2025.

For research enquiries, please use the contact details on my [GitHub profile](https://github.com/shimynimi).
