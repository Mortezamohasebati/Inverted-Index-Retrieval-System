# 🔍 Inverted Index Information Retrieval System

A Python-based **Information Retrieval (IR)** system built from scratch inside a Jupyter Notebook, implementing the classic **Inverted Index** data structure for efficient full-text search and document retrieval. This project covers the complete IR pipeline — from raw text preprocessing to indexed query evaluation with ranking.

---

## 📂 Repository Structure

```
Inverted-Index-Retrieval-System/
└── IR.ipynb    # Full IR system implementation in Jupyter Notebook
```

---

## 🧠 What Is an Inverted Index?

An **Inverted Index** is the core data structure behind every major search engine (Google, Elasticsearch, Lucene). Instead of mapping documents → words, it maps each **word → the list of documents that contain it**, called a **Posting List**.

```
"python"  →  [doc1, doc3, doc7]
"search"  →  [doc1, doc2, doc5, doc7]
"index"   →  [doc2, doc4, doc7]
```

This allows lightning-fast lookups: instead of scanning every document for a query word, you simply look up the term in the index — O(1) access — and get the matching document IDs instantly.

---

## ⚙️ System Pipeline

```
Raw Documents
      │
      ▼
 Text Preprocessing
  ├─ Tokenization       → split text into individual tokens
  ├─ Lowercasing        → normalize case
  ├─ Stop Word Removal  → filter out common words (the, is, at, ...)
  └─ Stemming / Lemmatization → reduce words to their root form
      │
      ▼
 Inverted Index Construction
  ├─ Term → Posting List (document IDs)
  ├─ Term Frequency (TF) per document
  └─ Document Frequency (DF) per term
      │
      ▼
 Query Processing
  ├─ Boolean Retrieval  → AND, OR, NOT queries
  ├─ Phrase Queries     → positional index
  └─ Ranked Retrieval   → TF-IDF / BM25 scoring
      │
      ▼
 Results (ranked or matched documents)
```

---

## 🔬 Key Components

### 1. Text Preprocessing

| Step | Description | Example |
|------|-------------|---------|
| **Tokenization** | Splits raw text into individual tokens | `"Hello World"` → `["Hello", "World"]` |
| **Lowercasing** | Normalizes all tokens to lowercase | `"Python"` → `"python"` |
| **Stop Word Removal** | Removes common non-informative words | `"the"`, `"is"`, `"and"` → removed |
| **Stemming** | Reduces words to their root/stem | `"running"` → `"run"` |
| **Lemmatization** | Reduces words to their dictionary form | `"better"` → `"good"` |

---

### 2. Inverted Index Structure

```python
inverted_index = {
    "term": {
        "doc_freq": 3,          # number of documents containing the term
        "postings": {
            "doc1": {"tf": 2, "positions": [4, 17]},
            "doc3": {"tf": 1, "positions": [9]},
            "doc7": {"tf": 3, "positions": [1, 45, 88]},
        }
    },
    ...
}
```

Each entry stores:
- **Document Frequency (DF)** — how many documents contain this term
- **Posting List** — the list of documents and where the term appears in each
- **Term Frequency (TF)** — how many times the term appears in each document
- **Positions** — exact positions for phrase/proximity queries

---

### 3. Query Types

**Boolean Retrieval:**
```
"python AND search"    → intersection of posting lists
"python OR java"       → union of posting lists
"search NOT spam"      → difference of posting lists
```

**Phrase Query:**
```
"information retrieval" → uses positional index to find adjacent terms
```

**Ranked Retrieval (TF-IDF):**

$$\text{TF-IDF}(t, d) = \text{TF}(t, d) \times \log\left(\frac{N}{\text{DF}(t)}\right)$$

Where:
- `TF(t, d)` = frequency of term `t` in document `d`
- `N` = total number of documents
- `DF(t)` = number of documents containing term `t`

Higher TF-IDF = more relevant to the query.

---

### 4. Ranking & Scoring

Documents are ranked by relevance using:

| Method | Description |
|--------|-------------|
| **TF-IDF** | Balances term frequency against how common the term is across all documents |
| **Cosine Similarity** | Measures angle between query vector and document vector |
| **BM25** | Probabilistic ranking function — improved TF-IDF used in modern search engines |

---

## 🛠️ Technologies Used

| Library | Purpose |
|---------|---------|
| `Python 3` | Core implementation |
| `NLTK` | Tokenization, stop words, stemming, lemmatization |
| `re` | Regular expressions for text cleaning |
| `collections` | `defaultdict` for efficient index construction |
| `math` | TF-IDF and scoring calculations |
| `pandas` | Document collection management and display |
| `numpy` | Vector operations for cosine similarity |
| `matplotlib` / `seaborn` | Visualizations (term distributions, etc.) |
| `Jupyter Notebook` | Interactive development and presentation |

---

## 🚀 Setup & Usage

**1. Clone the repository:**
```bash
git clone https://github.com/Mortezamohasebati/Inverted-Index-Retrieval-System.git
cd Inverted-Index-Retrieval-System
```

**2. Install dependencies:**
```bash
pip install nltk numpy pandas matplotlib seaborn jupyter
```

**3. Download NLTK resources (first time only):**
```python
import nltk
nltk.download('stopwords')
nltk.download('punkt')
nltk.download('wordnet')
```

**4. Launch the notebook:**
```bash
jupyter notebook IR.ipynb
```

**5. Run all cells:**
`Kernel → Restart & Run All`

---

## 📊 Example

Given a small corpus:

| Doc ID | Content |
|--------|---------|
| doc1 | "Python is a powerful programming language" |
| doc2 | "Information retrieval uses inverted index" |
| doc3 | "Python is used for information retrieval" |

After indexing:

```
"python"      → [doc1(tf=1), doc3(tf=1)]
"information" → [doc2(tf=1), doc3(tf=1)]
"retrieval"   → [doc2(tf=1), doc3(tf=1)]
"inverted"    → [doc2(tf=1)]
"index"       → [doc2(tf=1)]
```

Query: `"python AND retrieval"`
→ Intersection: `[doc1] ∩ [doc2, doc3]` = `[doc3]`
→ Result: **doc3** ✅

---

## 📚 Concepts Covered

- Information Retrieval (IR) fundamentals
- Inverted Index construction from scratch
- Text preprocessing pipeline — tokenization, stop words, stemming, lemmatization
- Boolean retrieval model — AND / OR / NOT
- Positional index — phrase and proximity queries
- TF-IDF weighting scheme
- Cosine similarity for ranked retrieval
- BM25 probabilistic ranking
- Posting list intersection and merging algorithms
- Document frequency and term frequency analysis

---

## 📜 License

This project is open source and free to use for educational and research purposes.
