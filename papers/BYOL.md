# Bootstrap Your Own Latent A New Approach to Self-Supervised Learning
[Paper](https://arxiv.org/pdf/2006.07733) |
[GitHub](https://github.com/google-deepmind/deepmind-research/tree/master/byol)

## Flow of the main method


```mermaid
graph TD;
    A[Start Input Batch - N Images] -->|Augment Twice| B[Two Views - 2N Images]
    B -->|Pass through Online Encoder| C[Online Network - f_theta]
    B -->|Pass through Target Encoder| D[Target Network - f_xi]

    C -->|Extract Representation| E[Online Representation - y_theta]
    D -->|Extract Representation| F[Target Representation - y_xi]
    
    E -->|Project| G[Online Projection - z_theta]
    F -->|Project| H[Target Projection - z_xi]

    G -->|Predict| I[Prediction Head - q_theta]
    
    I -->|Compute Loss| J[Loss Calculation - Mean Squared Error]
    H -->|Stop Gradient| J
    
    J -->|Backpropagation| K[Update Online Network - f_theta]
    K -->|Momentum Update| L[Update Target Network - f_xi, Slow Update]
    
    L -->|Repeat for Next Batch| A
    
    K -->|Trained Encoder Used for Downstream Tasks| M[Linear Classifier or Fine Tuning]