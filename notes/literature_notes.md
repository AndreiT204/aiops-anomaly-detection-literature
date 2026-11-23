# Literature Review Notes

**Project:** Evaluating Unsupervised Machine Learning for Real-Time Anomaly Detection in AIOps Pipelines

Each entry matches its corresponding PDF in `papers/<filename>.pdf` and its full bibliographic record in [`references.bib`](../references.bib).

---

## Section 1: AIOps Foundations and Automated Log Analysis Surveys

### [1] `he2021survey`
* **Key:** `he2021survey`
* **File:** [`papers/01_he2021_automated_log_analysis_survey.pdf`](../papers/01_he2021_automated_log_analysis_survey.pdf)
* **Source:** He et al. (2021) - A Survey on Automated Log Analysis for Reliability Engineering (*ACM Computing Surveys*)
* **Relevant Information:**
  * Organizes the full automated log analysis lifecycle into logging practices, log compression, log parsing, log mining (anomaly detection, failure prediction, failure diagnosis), and public benchmarks.
  * Explains why manual rule-writing and keyword matching fail to scale in modern distributed systems due to high log volume and evolving formats.
* **Used For:**
  * Background / State of the Art: Provides the authoritative pipeline taxonomy for situating log-based anomaly detection within reliability engineering and AIOps.

### [2] `zhang2024aiopsllm`
* **Key:** `zhang2024aiopsllm`
* **File:** [`papers/02_zhang2024_aiops_llm_survey.pdf`](../papers/02_zhang2024_aiops_llm_survey.pdf)
* **Source:** Zhang et al. (2024) - A Survey of AIOps for Failure Management in the Era of Large Language Models (*arXiv:2406.11213*)
* **Relevant Information:**
  * Categorizes AIOps failure management into four stages: data preprocessing (log parsing), failure perception (anomaly detection and prediction), root cause analysis, and auto-remediation.
  * Contrasts classical machine learning, deep learning, and LLM-based approaches on compute cost, inference latency, and maintenance burden.
* **Used For:**
  * Problem Statement & Motivation: Establishes modern AIOps terminology and motivates evaluating lightweight, low-latency unsupervised ML models rather than resource-heavy LLMs for real-time log pipelines.

### [3] `cabello2026aiops`
* **Key:** `cabello2026aiops`
* **File:** [`papers/03_cabello2026_aiops_realworld_llm.pdf`](../papers/03_cabello2026_aiops_realworld_llm.pdf)
* **Source:** De la Cruz Cabello et al. (2026) - Log Anomaly Detection in AIOps: A Real-World Implementation Using Large Language Models (*Systems and Soft Computing*)
* **Relevant Information:**
  * Evaluates a production-oriented Linux log anomaly detection pipeline under strict operational continuity and data confidentiality limits.
  * Examines sliding-window ingestion, Mean Time to Detect (MTTD) reduction, alert triage, and on-premise deployment trade-offs.
* **Used For:**
  * Related Work & Discussion: Provides a contemporary real-world AIOps deployment benchmark for discussing operational constraints, windowing, and privacy requirements in self-hosted pipelines.

---

## Section 2: Online Log Parsing and Benchmark Datasets

### [4] `he2017drain`
* **Key:** `he2017drain`
* **File:** [`papers/04_he2017_drain_log_parsing.pdf`](../papers/04_he2017_drain_log_parsing.pdf)
* **Source:** He et al. (2017) - Drain: An Online Log Parsing Approach with Fixed Depth Tree (*IEEE ICWS*)
* **Relevant Information:**
  * Introduces Drain, a streaming online log parser that uses a fixed-depth parse tree to extract structured log event templates from raw text logs in constant traversal depth.
  * Achieves 51.85% to 81.47% faster runtime than competing online parsers across over 10 million log lines while maintaining high parsing accuracy.
* **Used For:**
  * System Architecture (Log Ingestion): Core theoretical and algorithmic reference for the Drain log parsing stage, including tuning parse tree depth and similarity threshold (`st`) for near real-time throughput.

### [5] `zhu2019logparsing`
* **Key:** `zhu2019logparsing`
* **File:** [`papers/05_zhu2019_log_parsing_benchmarks.pdf`](../papers/05_zhu2019_log_parsing_benchmarks.pdf)
* **Source:** Zhu et al. (2019) - Tools and Benchmarks for Automated Log Parsing (*ICSE-SEIP*)
* **Relevant Information:**
  * Benchmarks 13 automated log parsers across 16 real-world system log datasets on grouping accuracy, runtime efficiency, and robustness.
  * Demonstrates empirically that Drain delivers the strongest overall trade-off between template accuracy and linear streaming speed.
* **Used For:**
  * Methodology (Component Selection): Justifies choosing Drain over alternative heuristic or offline log parsers for a real-time AIOps pipeline.

### [6] `zhu2023loghub`
* **Key:** `zhu2023loghub`
* **File:** [`papers/06_zhu2023_loghub_datasets.pdf`](../papers/06_zhu2023_loghub_datasets.pdf)
* **Source:** Zhu et al. (2023) - Loghub: A Large Collection of System Log Datasets for AI-Driven Log Analytics (*IEEE ISSRE*)
* **Relevant Information:**
  * Documents 19 real-world system log datasets spanning distributed systems (HDFS, Hadoop), supercomputers (BGL), operating systems (Linux), and server software (Apache, OpenSSH).
  * Details structural log characteristics, template diversity, and the scarcity of labeled anomaly data in operational environments.
* **Used For:**
  * Background & Experimental Setup: Contextualizes standard public log benchmarks and contrasts static offline corpora against dynamically generated live traffic and fault-injection logs.

### [7] `jiang2024loghub2`
* **Key:** `jiang2024loghub2`
* **File:** [`papers/07_jiang2024_loghub2_evaluation.pdf`](../papers/07_jiang2024_loghub2_evaluation.pdf)
* **Source:** Jiang et al. (2024) - A Large-Scale Evaluation for Log Parsing Techniques: How Far Are We? (*ACM ISSTA*)
* **Relevant Information:**
  * Introduces Loghub-2.0 (14 datasets averaging 3.6 million log lines each) and re-evaluates 15 log parsers at production scale.
  * Shows that small 2,000-line benchmarks hide parser degradation on rare templates and parameter-heavy logs, directly impacting downstream anomaly detectors.
* **Used For:**
  * Error Analysis & Threats to Validity: Explains how rare anomalous log templates can be misparsed or over-grouped in high-volume streams, affecting feature quality before anomaly scoring.

---

## Section 3: Isolation-Based and Streaming Unsupervised Machine Learning

### [8] `liu2008iforest`
* **Key:** `liu2008iforest`
* **File:** [`papers/08_liu2008_isolation_forest.pdf`](../papers/08_liu2008_isolation_forest.pdf)
* **Source:** Liu, Ting, & Zhou (2008) - Isolation Forest (*IEEE ICDM*)
* **Relevant Information:**
  * Introduces Isolation Forest (iForest), an unsupervised tree ensemble that isolates anomalies through random recursive feature partitioning rather than distance or density estimation.
  * Proves linear time complexity with a low constant and small memory footprint via sub-sampling, defining path length and normalized anomaly scores.
* **Used For:**
  * Core Methodology (Anomaly Scoring Engine): Primary algorithmic foundation for the Isolation Forest detector, explaining sub-sampling size, path-length scoring, and why it fits real-time CPU execution.

### [9] `hariri2019eif`
* **Key:** `hariri2019eif`
* **File:** [`papers/09_hariri2019_extended_isolation_forest.pdf`](../papers/09_hariri2019_extended_isolation_forest.pdf)
* **Source:** Hariri, Kind, & Brunner (2021) - Extended Isolation Forest (*IEEE TKDE / arXiv:1811.02141*)
* **Relevant Information:**
  * Demonstrates that standard Isolation Forest produces scoring artifacts ("ghost clusters") due to axis-parallel random cuts in feature space.
  * Proposes Extended Isolation Forest (EIF) using random hyperplane slopes to eliminate bias on correlated multivariate features.
* **Used For:**
  * Methodology & Future Work: Supports critical analysis of standard `scikit-learn` Isolation Forest limitations on correlated log-count features and identifies EIF as a targeted future improvement.

### [10] `guha2016rrcf`
* **Key:** `guha2016rrcf`
* **File:** [`papers/10_guha2016_robust_random_cut_forest.pdf`](../papers/10_guha2016_robust_random_cut_forest.pdf)
* **Source:** Guha et al. (2016) - Robust Random Cut Forest Based Anomaly Detection on Streams (*ICML / PMLR*)
* **Relevant Information:**
  * Formulates Robust Random Cut Forest (RRCF), a tree-based streaming sketch supporting dynamic insertion and deletion without full model retraining.
  * Addresses concept drift and evolving distributions in continuous operational telemetry streams.
* **Used For:**
  * Streaming Architecture & Discussion: Contrasts periodic sliding-window retraining of batch Isolation Forest against continuously updated streaming tree structures under concept drift.

---

## Section 4: Classical and Deep Learning Log Anomaly Detection Baselines

### [11] `xu2009console`
* **Key:** `xu2009console`
* **File:** [`papers/11_xu2009_console_log_mining_pca.pdf`](../papers/11_xu2009_console_log_mining_pca.pdf)
* **Source:** Xu et al. (2009) - Detecting Large-Scale System Problems by Mining Console Logs (*ACM SOSP*)
* **Relevant Information:**
  * Establishes the foundational unsupervised log-mining workflow: log parsing, windowed feature vector creation (event count and state ratio vectors), and Principal Component Analysis (PCA) anomaly detection.
  * Demonstrates that meaningful operational faults can be detected without labeled failure data.
* **Used For:**
  * Feature Engineering & Classical Baseline: Justifies transforming Drain templates into windowed event-count vectors and establishes PCA as a canonical unsupervised baseline.

### [12] `he2016experience`
* **Key:** `he2016experience`
* **File:** [`papers/12_he2016_experience_report_log_ad.pdf`](../papers/12_he2016_experience_report_log_ad.pdf)
* **Source:** He et al. (2016) - Experience Report: System Log Analysis for Anomaly Detection (*IEEE ISSRE*)
* **Relevant Information:**
  * Formalizes the four-stage log anomaly detection framework: log collection, log parsing, feature extraction (fixed, sliding, and session windows), and anomaly detection.
  * Benchmarks three supervised and three unsupervised algorithms in Python using `scikit-learn` on real-world log datasets.
* **Used For:**
  * Pipeline Design & Windowing Strategy: Directly informs the thesis pipeline architecture, time-window feature aggregation, and classical unsupervised benchmarking approach.

### [13] `du2017deeplog`
* **Key:** `du2017deeplog`
* **File:** [`papers/13_du2017_deeplog.pdf`](../papers/13_du2017_deeplog.pdf)
* **Source:** Du et al. (2017) - DeepLog: Anomaly Detection and Diagnosis from System Logs through Deep Learning (*ACM CCS*)
* **Relevant Information:**
  * Models normal log template sequences with an LSTM neural network, flagging events outside the top-g predicted next templates as anomalous.
  * Incorporates an online user-feedback update mechanism to adapt to new execution patterns.
* **Used For:**
  * Related Work (Deep Learning Baseline): Represents the canonical sequence-based deep learning approach, highlighting trade-offs in training time, inference cost, and sensitivity to unseen templates.

### [14] `meng2019loganomaly`
* **Key:** `meng2019loganomaly`
* **File:** [`papers/14_meng2019_loganomaly.pdf`](../papers/14_meng2019_loganomaly.pdf)
* **Source:** Meng et al. (2019) - LogAnomaly: Unsupervised Detection of Sequential and Quantitative Anomalies in Unstructured Logs (*IJCAI*)
* **Relevant Information:**
  * Distinguishes sequential anomalies (abnormal execution order) from quantitative anomalies (abnormal event counts within a window).
  * Proposes `template2Vec` semantic embeddings to handle unseen log templates without false alarms.
* **Used For:**
  * Analysis of Fault Coverage: Frames which anomaly classes an event-count Isolation Forest pipeline detects reliably (quantitative spikes, error floods) versus where sequence models excel.

### [15] `guo2021logbert`
* **Key:** `guo2021logbert`
* **File:** [`papers/15_guo2021_logbert.pdf`](../papers/15_guo2021_logbert.pdf)
* **Source:** Guo, Yuan, & Wu (2021) - LogBERT: Log Anomaly Detection via BERT (*arXiv:2103.04475*)
* **Relevant Information:**
  * Applies a self-supervised BERT model trained solely on normal log sequences using masked log key prediction and hypersphere volume minimization.
  * Achieves strong accuracy on static benchmarks but requires GPU compute and higher inference latency than classical detectors.
* **Used For:**
  * Related Work (Transformer Baseline): Positions modern transformer-based unsupervised log detection against lightweight tree ensembles in latency- and resource-constrained AIOps pipelines.

---

## Section 5: Evaluation Methodology, Benchmark Pitfalls, and Chaos Testing

### [16] `le2022howfar`
* **Key:** `le2022howfar`
* **File:** [`papers/16_le2022_dl_log_ad_how_far.pdf`](../papers/16_le2022_dl_log_ad_how_far.pdf)
* **Source:** Le & Zhang (2022) - Log-based Anomaly Detection with Deep Learning: How Far Are We? (*ACM/IEEE ICSE*)
* **Relevant Information:**
  * Demonstrates empirically that near-100% F1 scores reported in deep log anomaly detection rely heavily on random train/test splits (causing data leakage), log grouping, and dataset selection.
  * Shows sharp performance degradation under realistic chronological splits and severe class imbalance.
* **Used For:**
  * Evaluation Protocol: Justifies strict chronological train/test splitting, reporting precision/recall/F1 alongside false-positive rates, and avoiding optimistic offline evaluation bias.

### [17] `schmidl2022evaluation`
* **Key:** `schmidl2022evaluation`
* **File:** [`papers/17_schmidl2022_tsad_comprehensive_eval.pdf`](../papers/17_schmidl2022_tsad_comprehensive_eval.pdf)
* **Source:** Schmidl, Wenig, & Papenbrock (2022) - Anomaly Detection in Time Series: A Comprehensive Evaluation (*PVLDB*)
* **Relevant Information:**
  * Evaluates 71 anomaly detection algorithms across 976 time-series datasets on effectiveness (AUC-PR, AUC-ROC), runtime efficiency, and robustness.
  * Finds that no single deep learning model universally dominates classical unsupervised methods across operational regimes.
* **Used For:**
  * Evaluation Metrics & Runtime Analysis: Supports using Precision-Recall metrics (F1, AUC-PR) for imbalanced anomaly streams and validates measuring end-to-end scoring latency alongside detection quality.

### [18] `basiri2016chaos`
* **Key:** `basiri2016chaos`
* **File:** [`papers/18_basiri2016_chaos_engineering.pdf`](../papers/18_basiri2016_chaos_engineering.pdf)
* **Source:** Basiri et al. (2016) - Chaos Engineering (*IEEE Software*)
* **Relevant Information:**
  * Formalizes Chaos Engineering principles: defining a measurable steady-state baseline, hypothesizing steady-state continuity, injecting realistic production faults, and verifying system behavior experimentally.
  * Covers controlled injection of latency, resource exhaustion, and service failures to uncover hidden weaknesses before outages occur.
* **Used For:**
  * Experimental Setup & Validation: Provides the academic foundation for evaluating the live pipeline against load-tested steady-state baselines (JMeter) and controlled fault-injection (chaos) scripts.
