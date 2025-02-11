# Goku: Flow Based Video Generative Foundation Models
[Paper](https://www.arxiv.org/pdf/2502.04896) |
[Project Page](https://saiyan-world.github.io/goku/)

```mermaid
graph TD;
    A[Start: Input Text Prompt] -->|Tokenize| B[Text Encoder - FLAN-T5]
    
    B -->|Extract Text Features| C[Transformer-based Model - Goku]
    
    C -->|Latent Space Encoding| D[Image-Video Joint VAE]
    
    subgraph "Training with Rectified Flow"
        D -->|Compress into Latent Space| E[Latent Representations]
        E -->|Apply Rectified Flow| F[Transform Prior Distribution]
        F -->|Learn Temporal-Spatial Dependencies| G[Transformer Blocks]
        G -->|Decode into Pixel Space| H[Image/Video Generation]
    end
    
    H -->|Generate Image| I[Text-to-Image Output]
    H -->|Generate Video| J[Text-to-Video Output]
    
    I & J -->|Evaluate Quality| K[GenEval, VBench, DPG-Bench]
    
    K -->|Fine-tune Model| C

