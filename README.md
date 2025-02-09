# draw_papers

```mermaid
---
config:
  look: handDrawn
  theme: neutral
---

graph TD;
    A[Start Input Batch - N Images] -->|Augment Twice| B[Two Views - 2N Images]
    B -->|Pass through Encoder| C[Feature Extraction - h_i, h_j]
    C -->|Pass through Projection Head| D[Projection to Contrastive Space - z i, z j]
    
    D -->|Compute Pairwise Similarity| E[Similarity Matrix - 32x32]
    E -->|Extract Positive Pairs| F[Positive Pair Similarity]
    E -->|Extract Negative Pairs| G[Negative Pair Similarity]
    
    F -->|Compute NT-Xent Loss| H[Contrastive Loss Calculation]
    G -->|Compute NT-Xent Loss| H[Contrastive Loss Calculation]

    H -->|Backpropagation| I[Update Encoder and Projection Head]
    I -->|Repeat for Next Batch| A
    
    H -->|Trained Encoder| J[Linear Classifier or Fine-tuning]
