# wav2vec 2.0: A Framework for Self-Supervised Learning of Speech Representations
[Paper](https://arxiv.org/pdf/2006.11477) |
[GitHub](https://github.com/facebookresearch/fairseq)
## ✨ 1. Overall Flow of Wav2Vec 2.0 ✨
```mermaid
graph TD;
    A[Raw Audio Input] -->|Feature Extraction| B[Multi-Layer CNN Encoder]
    B -->|Outputs Latent Representations z| C[Latent Speech Representations]
    C -->|Masking Applied| D[Masked Representations]
    D -->|Passed to Transformer| E[Contextualized Representations c]
    E -->|Quantization Module| F[Discrete Speech Units q]
    
    subgraph "Self-Supervised Training"
        E -->|Contrastive Loss| G[Predict True q vs Distractors]
        F -->|Diversity Loss| H[Encourage Balanced Codebook Use]
        G & H -->|Optimize Model| I[Update CNN & Transformer]
    end

    I -->|Fine-tune on Transcribed Speech| J[CTC-based Speech Recognition]
```

## ✨ 2. Feature Extraction & Masking Process ✨
```mermaid
graph TD;
    A[Raw Audio Input - 16kHz Waveform] -->|Normalize and Convert| B[Multi Layer CNN Encoder]
    B -->|Extracts Latent Representations| C[Latent Speech Representations z]
    C -->|Apply Masking| D[Masked Representations]
    
    subgraph Masking Strategy
        D -->|Randomly Mask p Percent of Timesteps| E[Replaces Masked Frames]
        E -->|Trained Masked Vector| F[Fixed Learnable Vector]
    end

    D -->|Pass to Transformer| G[Contextualized Representation c]
```

## ✨ 3. Contrastive Training with Quantization ✨
```mermaid
graph TD;
    A[Contextualized Representation c] -->|Compare Against Candidates| B[Quantized Representation q]
    
    subgraph "Contrastive Loss"
        B -->|Identify True q| C[Positive Example]
        B -->|Distractors K| D[Negative Samples]
        C & D -->|Cosine Similarity| E[Compute Similarity Score]
        E -->|Loss Function| F[Contrastive Loss Optimization]
    end

    F -->|Update Model Weights| G[Improved Feature Representations]
```
## ✨ 4. Fine-Tuning for Downstream Tasks ✨
```mermaid
graph TD;
    A[Pre-trained Wav2Vec 2.0 Model] -->|Add Linear Classifier| B[Fine-Tuning with Labeled Data]
    B -->|CTC Loss| C[Optimize for Speech Transcription]
    C -->|Trained Speech Model| D[Speech-to-Text Output]
```

---
