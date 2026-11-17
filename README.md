# Twitter Sentiment Analysis & Multi-Algorithm NLP Benchmark

An interactive **Streamlit** web application for end-to-end **Twitter Sentiment Analysis**, featuring automated tweet cleaning, manual & lexicon-based annotation, custom implementations of multiple classification/clustering algorithms from scratch, and side-by-side model benchmarking.

---

## 📋 Project Overview

This platform provides a modular, decoupled architecture separating pure algorithmic logic (`algorithms/` & `cleaning/`), unified model orchestration (`core/`), and an interactive 7-tab user interface (`gui/`). Users can upload raw tweet datasets, preprocess and annotate them, tune hyperparameters for four distinct sentiment analysis approaches, and evaluate their comparative performance.

---

## ✨ Key Features (7-Tab Workflow)

1. **Data & Cleaning (`gui/tabs/data_cleaning.py`):**
   * Automatic CSV validation and heuristic detection of tweet text and sentiment label columns (`cleaning/column_detection/`).
   * Rule-based tweet normalization (`cleaning/tweet_cleaning/`) removing URLs, user mentions (`@user`), RT prefixes, hashtags, special characters, and redundant whitespace, with clean dataset export.
2. **Annotation Studio (`gui/tabs/annotation.py`):**
   * Interactive interface for manually labeling and auditing tweet sentiment classes (`Positive`, `Negative`, `Neutral`).
3. **Keyword Lexicon Annotator (`gui/tabs/keywords.py`):**
   * Rule-based sentiment scoring using curated positive/negative keyword dictionaries (`data/resources/keywords.json`).
4. **K-Nearest Neighbors (`gui/tabs/knn.py`):**
   * Custom KNN classifier (`algorithms/knn/`) with configurable distance metrics (`distance.py`), synonym expansion (`synonym_mapper.py` & `synonyms.json`), and weighted/majority voting strategies (`voting.py`).
5. **Hierarchical Clustering (`gui/tabs/clustering.py`):**
   * Unsupervised hierarchical tweet clustering (`algorithms/clustering/hierarchical.py`) to group tweets by textual similarity and inspect cluster distributions.
6. **Naive Bayes Classifier (`gui/tabs/bayes.py`):**
   * Custom Multinomial / Bernoulli Naive Bayes sentiment classifier (`algorithms/bayes/bayes.py`) with Laplace smoothing and n-gram / vocabulary configuration.
7. **Model Comparison & Evaluation (`gui/tabs/comparison.py`):**
   * Unified benchmarking dashboard (`core/evaluation.py`) comparing accuracy, precision, recall, F1-score, and confusion matrices across all configured algorithms.

---

## 🏗️ Architecture & Repository Structure

The codebase enforces strict separation of concerns between business logic and UI rendering:

```text
├── main.py                     # Streamlit application entry point
├── config.toml                 # Streamlit theme & server configuration
├── requirements.txt            # Python dependencies
├── Rapport PJE.pdf             # Detailed project report & experimental analysis
├── algorithms/                 # Pure Python NLP & ML algorithms (UI-independent)
│   ├── bayes/                  # Naive Bayes classifier implementation
│   ├── clustering/             # Hierarchical clustering implementation
│   ├── keywords/               # Lexicon-based keyword annotation & evaluation
│   └── knn/                    # Custom KNN (distances, synonym mapper, voting)
├── cleaning/                   # Data ingestion, column detection & text preprocessing
│   ├── column_detection/       # Automated tweet & label column detectors
│   ├── export/                 # Cleaned dataset export utilities
│   ├── file_validation/        # Input file schema & integrity checks
│   └── tweet_cleaning/         # Regex & rule-based tweet cleaning pipeline
├── core/                       # Abstraction layer connecting algorithms to the GUI
│   ├── wrapper.py              # BaseAlgorithm wrapper classes
│   ├── manager.py              # Central AlgorithmManager registry
│   └── evaluation.py           # Cross-model metrics & evaluation engine
├── gui/                        # Streamlit frontend components
│   ├── layout.py               # Main navigation layout & 7-tab router
│   └── tabs/                   # Individual UI views for each pipeline stage
├── data/
│   └── resources/              # Sentiment keyword & synonym JSON dictionaries
├── test.csv                    # Sample tweet dataset for quick testing
└── oldreadmes/                 # Archived original French developer documentation
    └── README_fr.md
```

---

## 🚀 Getting Started

### Prerequisites

* **Python 3.10+**
* Install the required dependencies:

```bash
pip install -r requirements.txt
```

### Launching the Application

Run the Streamlit app from the repository root:

```bash
streamlit run main.py
```

The application will open automatically in your default browser (typically at `http://localhost:8501`). You can immediately test the full pipeline using the included `test.csv` dataset.

---

## 📄 Technical Report

A comprehensive overview of the system architecture, preprocessing rules, mathematical formulations of each algorithm, and experimental evaluation results is available in [`Rapport PJE.pdf`](Rapport%20PJE.pdf).

---

## 👤 Author

**Sid Ahmed Ferroudj**  
*Master in Computer Science — Université de Lille*