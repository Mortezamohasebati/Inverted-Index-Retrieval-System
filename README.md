# 📚 Inverted Index Retrieval System — Reuters-21578

> **Course:** Fundamentals of Information Retrieval  
> **University:** Khorasan Institute of Higher Education  
> **Instructor:** Prof. Mahdi Aghaei

[![Open in Colab](https://img.shields.io/badge/Open%20in%20Colab-000000?style=flat&logo=googlecolab&logoColor=ffffff)](https://colab.research.google.com/drive/1zORXTocsHNh7ZEuJAmaQyDxuZh_SUI-y?usp=sharing)
![Python](https://img.shields.io/badge/Python-3.x-blue?style=flat&logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?style=flat&logo=jupyter)
![License](https://img.shields.io/badge/License-Academic-lightgrey?style=flat)

---

## 👥 Team

| Name | GitHub |
|---|---|
| Morteza Zeynal Mohasebati | [![GitHub](https://img.shields.io/badge/Morteza's%20GitHub-181717?style=flat&logo=github&logoColor=white)](https://github.com/Mortezamohasebati) |
| Seyed Vahid Seyedi | [![GitHub](https://img.shields.io/badge/Vahid's%20GitHub-181717?style=flat&logo=github&logoColor=white)](https://github.com/vahidseyyedi) |
| Ali Miri | — |

---

## 🧭 Overview

This project processes and analyzes the **Reuters-21578** benchmark dataset — one of the most widely used corpora in Information Retrieval research, containing thousands of real-world news articles.

The core goal is to build and compare **Inverted Indexes** using three distinct tokenization strategies, then perform statistical analysis and visualization to evaluate each method's characteristics.

---

## 📂 Project Structure

```
.
├── data/            # Raw Reuters-21578 .sgm files
├── stopwords/       # English stopword list
├── output/          # Generated CSVs, inverted indexes, and plots
└── IR.ipynb         # Main Jupyter Notebook
```

---

## 🔄 Pipeline

```
Reuters-21578 (.sgm)
        │
        ▼
  Article Extraction (topics="YES" only)
        │
        ▼
  ┌─────────────────────────────┐
  │   3 Tokenization Methods    │
  │  ① Noise Removal + Stemmer  │
  │  ② WordNet Validation       │
  │  ③ KeyBERT Keyword Extract  │
  └─────────────────────────────┘
        │
        ▼
  Inverted Index Construction
        │
        ▼
  Sparse TF Matrix + PCA
        │
        ▼
  Comparative Analysis & Visualization
```

---

## ⚙️ Methodology

### 1. Data Ingestion & Preprocessing

- Downloads `reuters21578.tar.gz` from UCI KDD Archive.
- Parses `.sgm` files using **BeautifulSoup** with `latin-1` encoding.
- Filters only articles tagged `topics="YES"`.
- Each article is represented as a `ReutersArticle` object holding: `newid`, `topics`, `title`, `body`, and `tokens`.

### 2. Tokenization — Method 1: Noise Removal + Porter Stemming

- Lowercases all text and strips HTML tags and non-alphabetic characters via regex.
- Filters tokens by length (3–20 characters).
- Removes stopwords from a predefined English stopword list.
- Applies **Porter Stemmer** for root extraction.

### 3. Tokenization — Method 2: WordNet-Based Validation

- Applies the same cleaning and length-filtering as Method 1.
- Additionally validates each token against **WordNet** — only words recognized as valid English vocabulary are kept.
- Reduces index noise from rare or malformed tokens.

### 4. Tokenization — Method 3: NLP Keyword Extraction (KeyBERT)

- Uses **KeyBERT** to extract semantically meaningful keywords from each article.
- Produces a compact, high-precision token set focused on the article's core topics.

### 5. Inverted Index Construction

- Each method produces its own inverted index via `build_inverted_index()`.
- Posting lists (implemented in the `PostingList` class) store `doc_id` and term frequency (`tf`) for each term.
- All indexes are alphabetically sorted via `sort_inverted_index()`.
- Outputs are saved as CSV files in the `output/` directory.

### 6. Sparse TF Matrix & PCA

- Constructs a sparse term-frequency matrix from the inverted index.
- Applies **PCA** (via scikit-learn) for dimensionality reduction and visual inspection of term-document relationships.

### 7. Comparative Analysis

| Metric | Description |
|---|---|
| Total Terms | Vocabulary size of each index |
| Total DF | Sum of document frequencies across all terms |
| Total TTF | Sum of total term frequencies across all terms |
| Term Overlap | Common and unique terms between methods (heatmap + pairwise bar charts) |

Visualizations include bar charts, pie charts, overlap matrices, and pairwise comparison plots.

---

## 🛠️ Tech Stack

| Library | Purpose |
|---|---|
| `beautifulsoup4` + `lxml` | Parsing `.sgm` XML files |
| `nltk` | Tokenization, stemming, WordNet access |
| `keybert` | Keyword extraction (Method 3) |
| `matplotlib` + `seaborn` | Statistical visualizations |
| `scikit-learn` | PCA for matrix dimensionality reduction |
| `pandas` + `numpy` | Data manipulation and matrix construction |

---

## 🚀 Getting Started

### Run in Google Colab (recommended)

Click the badge at the top of this README, or go directly to:  
[Open in Colab](https://colab.research.google.com/drive/1zORXTocsHNh7ZEuJAmaQyDxuZh_SUI-y?usp=sharing)

### Run Locally

```bash
# Clone the repository
git clone https://github.com/Mortezamohasebati/Inverted-Index-Retrieval-System.git
cd Inverted-Index-Retrieval-System

# Install dependencies
pip install beautifulsoup4 lxml nltk seaborn scikit-learn keybert

# Launch the notebook
jupyter notebook IR.ipynb
```

The notebook will automatically download the Reuters-21578 dataset and the English stopword list on first run.

---

## 📊 Dataset

**Reuters-21578** — sourced from the [UCI KDD Archive](http://kdd.ics.uci.edu/databases/reuters21578/).  
It contains 21,578 news articles from Reuters newswire, widely used as a benchmark in IR and text classification research. This project focuses exclusively on articles with at least one assigned topic label.

---

## 📄 License

This project is submitted as an academic assignment for the *Fundamentals of Information Retrieval* course at Khorasan Institute of Higher Education. All rights reserved by the authors.
