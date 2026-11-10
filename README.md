# Detecting and Prioritizing User Concerns in Mobile Apps

**MSc thesis · Computer Engineering (Algorithms & Computation)**  
**Sharif University of Technology · Defended 22 October 2025**  
**Author:** Shima Rezai · **Supervisor:** Dr. Abbas Heydarnoori

## Overview

How can software teams distinguish recurring, high-impact user concerns from millions of app reviews—and identify which issues deserve attention first?

This thesis presents a data-driven framework that combines user feedback from **Google Play**, technical evidence from **GitHub issue trackers**, and feedback about similar applications. It brings together natural language processing, semantic representation learning, clustering, automatic labelling, and machine-learning-based prioritisation to organise large-scale feedback into interpretable concerns and track them across application releases.

## Data

The study draws on the DATAR collection of **1,363 mobile applications**, from which **228 applications** with suitable release histories were selected for longitudinal analysis. The dataset includes approximately **1.34 million Google Play reviews** for these applications.

To enrich the analysis, five similar applications were identified for each selected app using TF–IDF and cosine similarity, and up to 30 highly liked reviews were collected from each. GitHub issue data provided complementary technical signals, including bugs, feature requests, issue status, and release-related activity.

## Method

1. **Phrase extraction.** Reviews and app descriptions were cleaned and normalised using NLP techniques. Frequent, syntactically filtered bigrams were extracted to represent concise expressions of user concerns.
2. **Semantic representation.** Alternative embedding approaches were compared, and a pretrained FastText model was adapted to the study text to represent the extracted phrases.
3. **Concern discovery.** K-Means was applied to the phrase vectors, with silhouette analysis guiding the selection of 10 clusters.
4. **Automatic labelling.** Flan-T5-Large generated concise, zero-shot labels from representative cluster keywords. Semantic-similarity and label-quality checks supported the interpretation of the resulting concern groups.
5. **Prioritisation across releases.** User-feedback signals were combined with historical patterns and technical indicators from GitHub. A central measure was the **Negativity Ratio (NR)**, which captures the share of negative reviews associated with a concern in a release in relation to its historical pattern. I implemented the NR-based prioritisation measure and incorporated it into the analysis alongside previous-release indicators, bug and feature-request ratios, issue status, and developer responses.

## Evaluation and findings

The evaluation compares classical machine-learning approaches—including Decision Tree, Random Forest, CatBoost, XGBoost, SVM, and Logistic Regression—with MLP, LSTM, and a stacking approach. Models were assessed using precision, recall, F1-score, accuracy, and AUC-ROC, alongside cluster-quality analysis and error analysis.

**Random Forest and CatBoost were among the strongest-performing models**, each achieving a reported F1-score of **0.83**. The findings also show the strong performance of classical machine-learning approaches compared with deep-learning models in this experimental setting.

## My contribution

My primary contributions were **research design, experimental evaluation, and analysis**. I designed and conducted the experiments, implemented the NR-based prioritisation measure, and analysed and interpreted the findings. The thesis was successfully defended and formally approved at Sharif University of Technology.

## Research outlook

The framework offers a foundation for further research on user-concern discovery and prioritisation across additional application domains, including iOS and desktop software.

## Citation

Rezai, Shima (2025). *Detecting and Prioritizing User Concerns in Mobile Apps*. MSc thesis, Department of Computer Engineering, Sharif University of Technology. Supervisor: Dr. Abbas Heydarnoori. Thesis in Persian; defended 22 October 2025.

For research enquiries, please use the contact details on my [GitHub profile](https://github.com/shimynimi).
