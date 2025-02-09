# Momentum Contrast for Unsupervised Visual Representation Learning

[Paper](https://arxiv.org/pdf/1911.05722) | [GitHub](https://github.com/facebookresearch/moco)


```mermaid
graph TD;
    A[Start Input Batch - N Images] -->|Augment Twice| B[Two Views - 2N Images]
    B -->|Pass through Encoder| C[Query Encoder - f_q]
    B -->|Pass through Momentum Encoder| D[Key Encoder - f_k]
    
    C -->|Extract Query Embeddings| E[Encoded Query - q]
    D -->|Extract Key Embeddings| F[Encoded Keys - k]
    
    E -->|Compute Similarity Scores| G[Similarity Matrix - q · k]
    F -->|Store Keys in Queue| H[Dictionary Queue - Large Evolving]

    G -->|Extract Positive Pairs| I[Positive Pair Similarity]
    G -->|Extract Negative Pairs| J[Negative Pair Similarity]
    
    I -->|Compute NT-Xent Loss| K[Contrastive Loss Calculation]
    J -->|Compute NT-Xent Loss| K[Contrastive Loss Calculation]

    K -->|Backpropagation Update f_q| L[Update Query Encoder]
    L -->|Momentum Update No Gradient| M[Update Key Encoder - f_k Slow]
    
    M -->|Enqueue New Keys| H
    H -->|Dequeue Oldest Keys| N[Remove Oldest Keys]
    
    K -->|Trained Encoder Used for Downstream Tasks| O[Linear Classifier or Fine-tuning]