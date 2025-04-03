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
```

<br>
<br>
<br>
<br>
<br>


# Flow with example shapes and batchsize of 8

```mermaid
graph TD;
    A[Start Input Batch - MNIST 8x1x28x28] -->|Augment Twice| B[Two Views - 16x1x224x224]
    
    B -->|Pass through Online Encoder| C[Online Network f_theta - 16x512]
    B -->|Pass through Target Encoder| D[Target Network f_xi - 16x512]

    C -->|Extract Representation| E[Online Representation y_theta - 16x512]
    D -->|Extract Representation| F[Target Representation y_xi - 16x512]
    
    E -->|Project| G[Online Projection z_theta - 16x128]
    F -->|Project| H[Target Projection z_xi - 16x128]

    G -->|Predict| I[Prediction Head q_theta - 16x128]
    
    I -->|Compute Loss| J[Loss Calculation - Mean Squared Error]
    H -->|Stop Gradient| J
    
    J -->|Backpropagation| K[Update Online Network f_theta]
    K -->|Momentum Update| L[Update Target Network f_xi - Slow Update]
    
    L -->|Repeat for Next Batch| A
    
    K -->|Trained Encoder Used for Downstream Tasks| M[Linear Classifier - MNIST 8x10]
```