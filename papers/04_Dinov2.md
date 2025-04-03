# DINOv2: Learning Robust Visual Features without Supervision
[Paper](https://arxiv.org/abs/2304.07193) | [GitHub](https://github.com/facebookresearch/dinov2)

## With Perplexity Deep search

1.	Augmentation Pipeline: Generates multiple views including:

	•	2 global crops (224x224 pixels)

	•	5 local crops (96x96 pixels)
2. Teacher Network: Processes only global crops using:

	•	Vision Transformer (ViT) backbone

	•	Exponential Moving Average (EMA) weights

	•	Centered features without gradient updates

3. Student Network: Processes all crops with:

	•	Identical ViT architecture

	•	Active gradient updates

	•	Combined DINO/iBOT objectives

```mermaid
%%{init: {'theme': 'forest'}}%%
flowchart TD
    A[Input Image] --> B[Augmentation Pipeline]
    B --> C[Global Crops]
    B --> D[Local Crops]
    C --> E[Teacher Network - ViT Backbone]
    D --> F[Student Network - ViT Backbone]
    E --> G[Image Level Features]
    F --> H[Patch Level Features]
    G --> I[DINO Loss]
    H --> J[iBOT Loss]
    I --> K[Total Loss Calculation]
    J --> K
    K --> L[Backpropagation]
    L --> F
    E -.-> M[EMA Weight Update]
    F -.-> M
    M --> E
```

### Multi-Resolution Training
```mermaid
%%{init: {'theme': 'forest'}}%%
flowchart LR
    A[High-Resolution Phase 518x518] --> B[Feature Alignment]
    B --> C[Low-Resolution Phase 224x224]
    C --> D[Stable Gradient Flow]

```
### KoLeo Regularization
```mermaid
%%{init: {'theme': 'forest'}}%%
flowchart TD
    A[Feature Space] --> B[Pairwise Distance Calculation]
    B --> C[Kozachenko-Leonenko Entropy]
    C --> D[Regularization Loss]
```

### Masked Image Modeling
```mermaid
%%{init: {'theme': 'forest'}}%%
flowchart LR
    A[Input Patch] --> B{Masked?}
    B -->|Yes| C[Student Prediction]
    B -->|No| D[Teacher Target]
    C --> E[Cross-Entropy Loss]
    D --> E
```


### Performance Characteristics
```mermaid
%%{init: {'theme': 'forest'}}%%
flowchart LR
    A[ViT-G/14] --> B[ViT-L/14]
    A --> C[ViT-B/14] 
    A --> D[ViT-S/14]
    B --> E[Distillation]
    C --> E
    D --> E
```

### Benchmark Results

```mermaid
%%{init: {'theme': 'forest'}}%%
flowchart TD
    A[ImageNet-1k] --> B[90.1% Linear Probe]
    C[NYUv2 Depth] --> D[δ1=0.923]
    E[ADE20K Segmentation] --> F[48.6 mIoU]
    G[Image Retrieval] --> H[Recall@1=85.3%]
```

## With ChatGPT 4o

### Overall Architecture of DINOv2

```mermaid
graph TD;
    A[Curated Image Dataset - 142M Images] -->|Input| B[Data Augmentation]
    B --> C[Vision Transformer - ViT Backbone]
    C --> D[Self-Supervised Training with DINO and iBOT Losses]
    D --> E[Robust Visual Features]
    E --> F[Evaluation on Multiple Benchmarks]
````
### Self-Supervised Training Process

```mermaid
graph TD;
    A[Input Image] -->|Augmentation| B[Global and Local Views]
    B --> C[Student Network - ViT Backbone]
    B --> D[Teacher Network - EMA of Student]
    C -->|Output| E[Student Features]
    D -->|Output| F[Teacher Features]
    E --> G[Compute DINO Loss]
    F --> G
    G --> H[Backpropagation to Student Network]
    D --> I[EMA Update of Teacher Network]
```

### Data Curation Pipeline
```mermaid
graph TD;
    A[Raw Image Collection] -->|Data Filtering| B[Quality Images]
    B -->|Clustering using FAISS| C[Image Clusters]
    C -->|Deduplication| D[Unique Images]
    D -->|Selection from Diverse Sources| E[Curated Dataset - 142M Images]

```

### Evaluation Benchmarks
```mermaid
graph TD;
    A[Robust Visual Features] --> B[Image Classification]
    A --> C[Semantic Segmentation]
    A --> D[Depth Estimation]
    A --> E[Instance Recognition]
    A --> F[Domain Generalization]
    B --> G[ImageNet]
    C --> H[ADE20K]
    D --> I[NYUv2]
    E --> J[Oxford and Paris]
    F --> K[Various Datasets]
```