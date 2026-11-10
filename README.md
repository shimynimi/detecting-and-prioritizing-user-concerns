# Detecting and Prioritizing User Concerns in Mobile Apps

**MSc thesis · Computer Engineering (Algorithms & Computation)**  
**Sharif University of Technology · Defended 22 October 2025**  
**Author:** Shima Rezai  
**Supervisor:** Dr. Abbas Heydarnoori

## Overview

Mobile-app developers receive large volumes of user feedback through app-store reviews. These reviews contain bug reports, feature requests, and suggestions for improvement, while issue-tracking systems provide complementary information about the technical work associated with an application. Analysing either source in isolation can leave important parts of a user's concern unexplored.

This thesis investigates a multi-source approach to identifying, semantically grouping, and prioritising user concerns in mobile applications. It combines Google Play reviews with GitHub issue-tracking information and feedback from similar applications. The workflow uses natural language processing, phrase representations, semantic clustering, automatic cluster labelling, and machine-learning models to support the analysis of concerns across application versions.

The work was completed as an MSc thesis in Computer Engineering (Algorithms & Computation) at Sharif University of Technology and successfully defended on **22 October 2025**.

## Research problem and questions

The research addresses three connected tasks:

1. **Concern identification:** How can meaningful concerns be extracted from large collections of unstructured app reviews?
2. **Semantic organisation:** How can phrases that express similar concerns be grouped into interpretable, higher-level themes?
3. **Concern prioritisation:** How can user-feedback signals, historical patterns, and technical issue-tracking information be combined to estimate which concerns deserve attention?

The thesis also examines whether information from similar applications can enrich the analysis, particularly when an individual application has limited feedback.

## Data sources and study scope

The thesis reports using the DATAR collection, which contains information about **1,363 mobile applications** and their releases. From this collection, **228 applications** were selected for the study. The selection criteria included information such as release history, review volume, and issue-tracking activity; applications needed more than one release to support comparisons across versions.

The study reports collecting approximately **1,335,327 Google Play reviews** for the selected applications. The collected information included review text, ratings, dates, application descriptions, and release-related information.

To incorporate evidence from similar applications, the study:

- Identified five similar applications for each selected application using TF–IDF representations of app descriptions and cosine similarity.
- Collected up to 30 highly liked reviews from each similar application.
- Combined these reviews with application-specific feedback for subsequent semantic analysis and prioritisation.

GitHub data supplied complementary technical signals, including issue reports, feature requests, issue status, and release-related information.

> **Scope note:** These figures and collection steps are reported in the thesis. The underlying datasets and collection scripts are not currently included in this public repository.

## Methodology

### 1. Text preprocessing and phrase extraction

The review and description text was prepared for analysis using Python NLP tools, including NLTK and WordNet. The thesis describes tokenisation, part-of-speech tagging, lemmatisation, removal of standard and custom stop words, normalisation of case, and removal of punctuation and other unwanted characters.

Negation expressions were normalised to a common token (not) so that negative meaning would be handled more consistently.

The workflow then extracted **bigrams** (two-word expressions) as candidate descriptions of user concerns. The thesis describes filtering these candidates using frequency, syntactic patterns, duplicate and similarity checks, and evidence from similar applications. Prominent bigrams were selected using frequency quartiles, including the upper quartile, followed by min–max normalisation.

### 2. FastText representations

The selected bigrams were converted into vector representations so that semantically related phrases could be compared. The thesis evaluates alternative word-embedding approaches, including Word2Vec, GloVe, FastText, ELMo, and Universal Sentence Encoder.

FastText was selected for the final workflow. The thesis describes adapting a pretrained FastText model to the study text over **10 training epochs**. It also reports testing 16 textual formats for representing bigrams; the simple space-separated form (for example, "app good") achieved the highest reported silhouette score in that format experiment (**0.85**).

### 3. Semantic clustering

The FastText vectors were grouped using **K-Means**. The thesis reports selecting **10 clusters** based on the silhouette criterion. The goal was to consolidate varied, fine-grained expressions into broader concern groups that could be interpreted and compared across application releases.

### 4. Automatic cluster labelling

To make the clusters easier to interpret, the workflow generated short labels from representative keywords. The thesis describes selecting up to 10 representative keywords for a cluster and using **Flan-T5-Large** in a zero-shot labelling step to produce a concise label of approximately two to five words.

The proposed quality checks included semantic similarity between the cluster representation and its label, handling ambiguous or unrelated labels, and checking for unintended duplicate labels. Labels judged unsuitable could be replaced with a general "Other" label.

### 5. Concern prioritisation and the Negativity Ratio

After concern clusters were formed, the study assessed their priority using user-feedback and technical indicators.

A central measure was the **Negativity Ratio (NR)**, a methodology proposed by the thesis supervisor and implemented by the author. It compares the share of negative reviews for a concern cluster in a particular application release with the historical pattern for that cluster.

The thesis defines:

- **RNR:** the proportion of reviews rated two stars or lower within a concern cluster for a particular release.
- **MRNR:** the median RNR across previous releases.
- **NR:** a normalised measure, using the hyperbolic tangent function, of how the current negative-feedback level compares with its historical baseline.

The thesis also describes special handling for cases such as releases with no reviews or no historical negative-review baseline. Priority labels are assigned by comparing the current NR with a threshold informed by historical variability.

Additional features described in the thesis include:

- Previous-release RNR and NR.
- Bug-report and feature-request ratios.
- Ratios of created and closed GitHub issues.
- The proportion of user reviews receiving developer responses.
- Historical application and release indicators.

This component connects current user feedback with the history of a concern and the technical activity recorded for an application.

### 6. Model evaluation

The thesis compares classical machine-learning models and deep-learning approaches for the concern-identification and prioritisation tasks. Models reported include Decision Tree, Random Forest, Support Vector Machine, Logistic Regression, XGBoost, CatBoost, Multilayer Perceptron (MLP), LSTM, and a stacking approach.

Reported evaluation measures include accuracy, precision, recall, F1-score, and AUC-ROC. Cluster analysis also considers measures such as silhouette and Davies–Bouldin, together with qualitative assessment of cluster coherence and interpretability.

The thesis describes an 80/20 training–test split and also discusses stratified cross-validation. Full experiment configurations, seeds, fold-level outputs, and executable evaluation scripts are not currently available in this repository.

## Reported findings

The thesis reports that **Random Forest and CatBoost were among the strongest-performing models** in the comparison. Random Forest is reported with an F1-score of **0.83**, while CatBoost is also reported with an F1-score of **0.83**. The thesis discusses better performance by the classical machine-learning models than by the deep-learning models in this experimental setting, and identifies limited data and overfitting as possible explanations for the weaker deep-learning results.

There is an inconsistency in the reported Random Forest accuracy: the abstract gives **0.7906**, while the detailed model-comparison results give **0.86**. The thesis does not explain the difference. For that reason, this README does not present either accuracy figure as a definitive headline result. The discrepancy should be clarified before a single accuracy value is used in an external application or publication.

The thesis also reports using paired t-tests, one-way ANOVA, and the Friedman test to compare model performance, with statistically significant differences (p < 0.05) reported between the classical models highlighted in the discussion and the deep-learning models. The detailed test statistics and underlying repeated-run outputs are not included in this repository.

> **Reproduction status:** These are findings reported in the approved thesis. They have not been independently reproduced from the contents of this public repository.

## My research contribution

My main contribution to this MSc thesis was in **research design, experimental work, and analysis**. I designed and conducted the experiments and analysed and interpreted the results. I also implemented the Negativity Ratio methodology proposed by my supervisor, Dr. Abbas Heydarnoori.

The thesis was successfully defended and formally approved at Sharif University of Technology.

## Limitations and future work

The thesis identifies several limitations and directions for further work:

- The study focuses primarily on Android applications; transfer to iOS and desktop software requires further evaluation.
- Applications and concern clusters with few reviews can be difficult to classify reliably.
- Deep-learning models showed weaker performance in the reported experiments, with overfitting discussed as a contributing factor; larger and more balanced datasets may help.
- The preprocessing and concern-grouping stages could be further improved.
- Future work could expand the data sources and application domains, improve cluster interpretability, and evaluate the approach in larger-scale real-world settings.

## Repository status and reproducibility

This repository currently contains an **English research overview** of the MSc thesis. It does not yet contain the complete thesis implementation, source datasets, trained model files, or all experiment configurations.

For that reason:

- The README documents the workflow and results described in the thesis; it is not an executable implementation.
- The reported results should not be interpreted as reproduced by this repository.
- Code, data, and model artefacts will only be added if they can be shared appropriately and safely.
- Missing implementation details will be documented rather than inferred.

## Citation

Rezai, Shima (2025). *Detecting and Prioritizing User Concerns in Mobile Apps*. MSc thesis, Department of Computer Engineering, Sharif University of Technology. Supervisor: Dr. Abbas Heydarnoori. Thesis in Persian; defended 22 October 2025.

---

For questions about the research, please contact the author through the email address listed on the [GitHub profile](https://github.com/shimynimi).
