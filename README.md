# ReFormer: Enhanced Transformer with Rotary Position Embedding

## Overview

### Introduction: 
Sequential order of words is of great value to natural language understanding. Transformer models require positional encoding because the Attention mechanism alone cannot capture the order of input tokens or distinguish their positions. There are two main approaches to address this:
* Absolute positional encoding: Integrate positional information directly into the input.
<img width="626" alt="Screenshot 2024-10-18 at 7 23 48 PM" src="https://github.com/user-attachments/assets/e70501c0-4b23-478f-bb56-4623e4124f10">
* Relative positional encoding: Modify the attention mechanism to enable it to distinguish tokens based on their positions.
<img width="754" alt="Screenshot 2024-10-18 at 7 24 33 PM" src="https://github.com/user-attachments/assets/51adfbbe-4287-496b-9a0c-78042b350460">

### Problem:

The 2 methods drawbacks in the following areas:

* Handling long sequences: Absolute positional encoding struggles with long sequences since it uses fixed position values that don't work well for longer contexts.
* Capturing relative positions effectively: Relative positional encoding is more complex and adds extra computation to handle the distances between tokens.
* Compatibility with efficient attention mechanisms like linear self-attention

### Approach: 

Rotary positional embedding, or RoPE, is an effective technique that combines the strengths of both absolute and relative embeddings. It encodes positional information by rotating word vectors in a high-dimensional space, with the rotation amount determined by each word's position in the sequence. This allows the model to easily compute the relative position between any two words by comparing their rotation differences. As a result, each word receives a unique rotation based on its absolute position, while the model can still capture relative positional information.

* Encodes positions using rotation matrices
* Incorporates relative position information directly into self-attention

### Evaluation: 

* Experimental Validation
  - Machine translation: sequence-to-sequence language translation tasks

     ![Screenshot 2024-10-18 at 10 45 58 AM](https://github.com/user-attachments/assets/ded9b5ba-3614-4e89-9044-6c6cdc5cee77)

  - Pre-training Language Modeling: learning contextual representations

    ![Screenshot 2024-10-18 at 10 50 07 AM](https://github.com/user-attachments/assets/327f61d0-95b4-421b-8dc6-ddba08e94184)
    
  - Fine-tuning on GLUE tasks: generalization ability on the downstream NLP tasks

    ![Screenshot 2024-10-18 at 10 49 31 AM](https://github.com/user-attachments/assets/2663e346-eea4-474b-9474-6041968296cb)

  - Long documents: text whose length exceeds 512 characters
    
    ![Screenshot 2024-10-18 at 6 25 04 PM](https://github.com/user-attachments/assets/abec11ba-4167-478a-b45a-c782391f864e)


Key finding: Rotary Position Embedding is prioritized over existing methods for its advantage in: 
1. Sequence length flexibility, with particularly strong results on long sequence tasks
2. Decaying inter-token dependency with increasing relative distances
3. Capability of equipping the linear self-attention with relative position encoding (e.g., Performers)
4. Faster convergence and lower loss in pre-training

## Architecture Overview
### A 2D case

![Screenshot 2024-10-18 at 6 09 43 PM](https://github.com/user-attachments/assets/450583f4-144f-4331-9ce0-bcc66a83d8fc)

## Critical Analysis

## Impacts

## Resource Links
https://medium.com/p/31c082e16b26

https://kexue.fm/archives/8265

