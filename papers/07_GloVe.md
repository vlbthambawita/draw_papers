# GloVe: Global Vectors for Word Representation

This document explains the key steps in the GloVe paper using multiple **Mermaid diagrams** with example dimensions for clarity.

---

## 1. Overview of GloVe Architecture
```mermaid
graph TD
    A[Corpus: Large Text Data] --> B[Build Word Co-occurrence Matrix X]
    B --> C[Apply Weighting and Log Transform]
    C --> D[Optimize Least Squares Objective]
    D --> E[Obtain Word Vectors w and Context Vectors w_tilde]
    E --> F[Final Word Embeddings = w + w_tilde]
```

GloVe builds on **global co-occurrence statistics** of word pairs and directly **factorizes a log-transformed co-occurrence matrix**.

---

## 2. Co-occurrence Matrix Construction
```mermaid
graph TD
    A[Text Corpus] --> B[Sliding Context Window]
    B --> C[Count Co-occurrences Xij]
    C --> D[Construct Matrix X - V by V]
```

**Example**: For a vocabulary of size `V = 100,000`, the resulting co-occurrence matrix `X` would be `100,000 × 100,000` but sparse.

---

## 3. Core GloVe Objective Function
```mermaid
graph TD
    A[Xij Co-occurrence Count] --> B[Log of Xij]
    B --> C[Dot Product: w_i times w_tilde_j]
    C --> D[Add Bias Terms: b_i and b_tilde_j]
    D --> E[Squared Loss: dot plus bias minus log squared]
    E --> F[Weighted by f of Xij]
```

$$
J = \sum_{i,j} f(X_{ij}) \cdot (w_i^\top \tilde{w}_j + b_i + \tilde{b}_j - \log(X_{ij}))^2
$$

---

## 4. Weighting Function f(Xij)
```mermaid
graph TD
    A[If Xij is less than xmax] --> B[f of Xij is Xij divided by xmax raised to alpha]
    A2[If Xij is greater than or equal to xmax] --> C[f of Xij is 1]
```

**Default Parameters**:
- `xmax = 100`
- `α = 3/4`

---

## 5. Training Process
```mermaid
graph TD
    A[Initialize w, w_tilde, b, b_tilde randomly] --> B[Iterate over nonzero Xij]
    B --> C[Compute weighted squared loss]
    C --> D[Use AdaGrad optimizer]
    D --> E[Update w, w_tilde, b, b_tilde]
    E --> F[Repeat for multiple epochs]
```

---

## 6. Evaluation Workflow
```mermaid
graph TD
    A[Trained Word Vectors] --> B[Word Analogy: king - man + woman is ?]
    A --> C[Word Similarity: cosine comparison]
    A --> D[NER Features: input to CRF]
```

GloVe vectors are tested on:
- **Word analogy tasks**
- **Semantic similarity**
- **Named Entity Recognition** (NER)

---

## ✅ Summary of Benefits
- Combines **count-based** and **predictive** models.
- Learns **linear substructures** in word space.
- Efficient: only uses **nonzero co-occurrence values**.
- Strong performance on various **NLP tasks**.

---

Generated using Mermaid for clarity and educational purposes.

